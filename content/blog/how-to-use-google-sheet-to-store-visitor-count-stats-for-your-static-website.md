---
title: "How to Use Google Sheet to Store Visitor Count for Your Static Website"
date: 2019-01-03T21:29:44+05:30
description: "Summary: This post walks you through the steps to setup a google spreadsheet to hold your live visitor count. The count will be updated each time someone opens your page."
draft: false

---

P.S. This post assumes that the reader is aware of Google Spreadsheets, integration with Google App Scripts, how to publish a Google Script as Web App and has somewhat familiarity with JavaScript. If not then please google for these, there are tons of good quality posts that walks you through these features in detail. 

Recently while working on a static site (of course generated using Hugo), I needed to add Visitor Count information on it. It looks something like this:

<img src="/images/visitorcount.png" alt="Visitor Count Image" class="responsive-post-image" style="border:1px solid #cdcdcd;width:100%;max-width:300px;"/>

I also wanted to keep full control on how I manage the count, so did not want to use a '*specialized*' 3rd party site or library just for this. I am somewhat comfortable with Google Scripts as I have fiddled with it in past, so I though why not use Google Spreadsheet to store my data. I just had to expose (in Google Script world they call it publishing the script) a URL that simply increments the count by 1 each time the URL is accessed.

Here's the **JavaScript code** that's responsible for invoking the published GoogleScript URL each time the website loads (or reloads, yeah, I know that's not perfect).

<div class="code">
{{< highlight javascript>}}
// Invoke this method as soon as your website loads
function incrementVisitorCount() {
    $.ajax({
      url: "https://script.google.com/macros/s/ADS2123121AD_ofCourseThis1sFakeID_xyzAbc/exec",
      method: "GET",
    }).done(function(res) {
      if (res && res.count) {
        $(".js-counter").attr("data-to", res.count);
      }
    });

{{< / highlight >}}
</div>   

Here's the corresponding not so optimum **Google App Script**. This can be probably heavily optimized and refactored into a more elegant code but hey, I did not want to spend too much time and energy coding this. Feel free to optimize this to your heart's content.

<div class="code">
{{< highlight javascript>}}

//Credit: http://mashe.hawksey.info/2014/07/google-sheets-as-a-database-insert-with-apps-script-using-postget-methods-with-ajax-example/
function doGet(e){
  return handleResponse(e);
}

//  Enter sheet name where data is to be written below
var SHEET_NAME = "Sheet1";

var SCRIPT_PROP = PropertiesService.getScriptProperties(); // new property service

function handleResponse(e) {
  // Prevent concurrent access or overwritting data issues
  // Ref: http://googleappsdeveloper.blogspot.co.uk/2011/10/concurrency-and-google-apps-script.html
  var lock = LockService.getPublicLock();
  lock.waitLock(30000);  // wait 30 seconds before conceding defeat.
  
  try {
    // next set where we write the data - you could write to multiple/alternate destinations
    var doc = SpreadsheetApp.openById(SCRIPT_PROP.getProperty("key"));
    var sheet = doc.getSheetByName(SHEET_NAME);
    
    // we'll assume header is in row 1 but you can override with header_row in GET/POST data
    var headRow = e.parameter.header_row || 1;
    var headers = sheet.getRange(1, 1, 1, sheet.getLastColumn()).getValues()[0];
    var lastRow = sheet.getLastRow();
    var nextRow = sheet.getLastRow()+1; // get next row
    var row = []; 
    
    var lastVisitorCount = sheet.getRange(lastRow, 1).getValue();
    // loop through the header columns
    for (i in headers){
      if (headers[i] == "Timestamp"){ // special case if you include a 'Timestamp' column
        row.push(new Date());
      } else { // else use header name to get data
        //row.push(e.parameter[headers[i]]);
        row.push(lastVisitorCount+1)
      }
    }
    // more efficient to set values as [][] array than individually
    sheet.getRange(nextRow, 1, 1, row.length).setValues([row]);
    // return json success results
    return ContentService
          .createTextOutput(JSON.stringify({"result":"success", "count": sheet.getRange(nextRow, 1).getValue()}))
          .setMimeType(ContentService.MimeType.JSON);
  } catch(e){
    // if error return this
    return ContentService
          .createTextOutput(JSON.stringify({"result":"error", "error": e}))
          .setMimeType(ContentService.MimeType.JSON);
  } finally { //release lock
    lock.releaseLock();
  }
}

function setup() {
    var doc = SpreadsheetApp.getActiveSpreadsheet();
    SCRIPT_PROP.setProperty("key", doc.getId());
}

{{< / highlight >}}
</div>   