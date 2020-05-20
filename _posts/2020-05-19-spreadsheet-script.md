---
author: lydxlx
date: 2020-05-19
layout: post
title: "A Case Study of Google Spreadsheet Script"
description: ""
mathjax: true
tipue_search_active: true
categories: google-script
tags: google spreadsheet javascript json base64 regex
---

* content
{:toc}

## Problem
I would like to port the data of the following table on [https://www.etf.com/stock/FB](https://www.etf.com/stock/FB) into Google Spreadsheet using a programmatic manner.

![](/images/2020-05-19_01.png)

I have tried Google's built functions `IMPORTHTML` and `IMPORTXML`, but they do not work as expected.
The former can extract some lists / tables, but the target one is missed.
For the latter, I tried to query the element using filter like `//table[@id='xxx']`, where `xxx` is the id I obtained from Inspect tool, but failed again.
I suspect this is because that table is dynamically generated using some js function.

## Solution
By inspecting the page source, it looks like the table data is driven by the following div element, where the giant [`base64Data` attributes](https://paste.ubuntu.com/p/M4Fy2j5FCF/) seems to contain promising information.
```html
<div id="etf-finder-results" data-react='{"page": "stock", "fundsTotal": "229", "tableTitle": "List of ETFs That Hold FB", "base64Data": "W3siY29sXzEiOiJUaWNrZXIiLCJjb2xfMiI6IkZ1bmQgTmFtZSIsImNvbF8zIjoiU2VnbWVudCIsImNvbF80IjoiRkIgQWxsb2NhdG...
```

After decoding, I was able to obtain the original json string of the entire table! I tried to `curl` the url immediately and verified that the same base64 string can be retrieved.

![](/images/2020-05-19_02.png){:height="600px"}



This gives me some hope, and my idea goes as follows.

1. Fetch the raw html response and extract that base64 string.
2. Decode the base64 string and parse it as a json object.
3. Convert the json object into a 2D value array.
4. Set the range (of the same dimension) value according to the value array.

The steps above seem pretty straightforward, but it is truly a nightmare to me since I have absolutely **zero** knowledge on frontend.
The journey was indeed painful -- I searched the Internet so hard and encountered so many problems.
But I'm glad that I could make it work eventually...
Here is a good summary on how I conquer all the challenges.

1. Google provides `UrlFetchApp` class for url fetching, which is great.
   However, my first attempt (by passing only the url as parameter) was not successful that the base64 string was not returned somehow.
   After some trials, it seems like it would work if we explicitly specify "post" as the fetching method.
2. The returned response is not JSON and is not XML neither, so parsers like `JSON` and `XmlService` will fail to parse the string.
   I cannot find any HTML parser (maybe because I'm a n00b) so I just use a regular expression to extract the base64 string...
   (I also learned how to capture RE groups in js.)
3. Google provides `Utilities.base64Decode` to decode a base64 string into a byte array.
   To convert it back as an ASCII string, one can use the method `Utilities.newBlob(decoded).getDataAsString()`.
4. `JSON.parse(str)` will parse a json string into json-object, which is nice.
5. `CacheService` and `Cache` are two handy classes provided by Google that can be used to reduce number of HTML requests.
6. `for (.. in ..)` is different from `for (.. of ..)` in Javascript... I was so confused by them. LOL
7. `[]` defines an empty Javascript array and `push` is the right method to append / push_back new elements to the back of the array.
   `concat` is the method to concatenate two arrays.
8. To write data into Google Spreadsheet, we need to obtain the current sheet by calling `SpreadsheetApp.getActiveSheet`.
9. Then we need to get the range (with the same dimension of the data) to write the values.
   One possible way is `sheet.getActiveCell().offset(0, 0, num_row, num_col)`.
10. Finally, `range.setValue()` writes the values in order to the range.

My final google script is shown as follows.
```js
function myFunction() {
  var cache = CacheService.getScriptCache();
  if (cache.get("etf_fb_json_string") == null) {
    var formData = {
    };
    var options = {
      'method' : 'post',
      'payload' : formData
    };

    var response = UrlFetchApp.fetch("https://www.etf.com/stock/FB", options);
    var myRe = /"base64Data": "(.+)"}'/g;
    var base64 = myRe.exec(response.getContentText())[1];
    var decoded = Utilities.base64Decode(base64);
    var json_string = Utilities.newBlob(decoded).getDataAsString();
    cache.put("etf_fb_json_string", json_string);
  }
  var json = JSON.parse(cache.get("etf_fb_json_string"));

  var keys = ["col_1", "col_2", "col_3", "col_4", "col_5"];
  var values = [];
  for (var i=0; i<json.length; i++) {
    data = [];
    for (key of keys) {
      data.push(json[i][key]);
    }
    values.push(data);
  }

  var sheet = SpreadsheetApp.getActiveSheet();
  var range = sheet.getActiveCell().offset(0, 0, values.length, values[0].length);
  range.setValues(values);
}
```

Running the script, and result is looking good.

![](/images/2020-05-19_03.png){:height="300px"}
