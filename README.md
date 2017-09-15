# Telstra-API - *v0.2.1*

**Telstra-API** is a [node.js](https://nodejs.org/) module that takes the hard work out of using [Telstra Developer APIs](https://dev.telstra.com/).

### Included APIs

  - [SMS API](https://dev.telstra.com/content/sms-api-0)
  - [WiFi API](https://dev.telstra.com/content/wifi-api)

**The Connect API and Mobile Connect API will not be included in this module.**

## Installation
The easiest (and only supported) way to install Telstra-API is by using [NPM](https://www.npmjs.com/) (Node Package Manager) from the command line.
```sh
$ npm install telstra-api
```

## Usage
```javascript
// Obtain these keys from the Telstra Developer Portal
export TELSTRA_API_CONSUMER_KEY = "U62RDEGRxb4Jw2p30oHkMnBLJaSJG5IS";
export TELSTRA_API_CONSUMER_SECRET = "PTbyss26edeKr1cs";
export TELSTRA_API_SCOPE = "SMS WIFI";

TelstraAPI = require('telstra-api');
var t = new TelstraAPI();
```

**NOTE:** It is important to make sure you're using the correct CONSUMER_KEY and CONSUMER_SECRET, as well as specifying only the scope(s) that your application has access to in the Telstra Developer Portal, as all authentication failures (not API errors) will result in a printed stack trace, and the application exiting.*

### SMS API - t.sms

#### t.sms.send(string &lt;target&gt;, string &lt;message&gt;);
- **target**: Australian telephone phone number to deliver SMS.
- **message**: The message to be delivered.

**Returns**: (String) The message ID of the pending SMS.

#### t.sms.getFullReplies(String &lt;messageId&gt;);
**messageID**: The message ID received from a previous call to t.sms.send()

**Returns**: An object containing:
- String **from**: The number from which the SMS is received.
- String **acknowledgedTimestamp**: The time that the message was received by the SMS service.
- String **content**: The content of the SMS.

[\[Example Request &amp; Result\]](https://gist.github.com/ozjd/34f546812a709c490dc0)

#### t.sms.getFullStatus(String &lt;messageId&gt;);
**messageID**: The message ID received from a previous call to t.sms.send()

**Returns**: An object containing:
- String **to**: The target number supplied to t.sms.send().
- String **receivedTimestamp**: The time that the message was received by the target network.
- String **sentTimestamp**: The time that the message was sent.
- String **status**: A status representing the current send status of the message.

[\[Example Request &amp; Result\]](https://gist.github.com/ozjd/29bba80b5ca882def733)

#### t.sms.getReplies(String &lt;messageId&gt;);
**messageID**: The message ID received from a previous call to t.sms.send()

**Returns**: An array of (String) **reply**s - See: t.sms.getFullReplies()

#### t.sms.getStatus(String &lt;messageId&gt;);
**messageID**: The message ID received from a previous call to t.sms.send()

**Returns**: (String) **status** - See: **status** in t.sms.getFullStatus()

&nbsp;

### WiFi API - t.wifi

##### t.wifi.getHotspots(Number &lt;latitude&gt;, Number &lt;longitude&gt;, Number [radius]);
Retrieves the location of nearby Telstra owned WiFi Hotspots in Australia ([Telstra AIR](https://www.telstra.com.au/broadband/telstra-air)).
- **Latitude**: The latitude of the centre of the search area.
- **Longitude**: The longitude of the centre of the search area.
- **Radius**: The radius (in metres) of the area to be searched. Defaults to 2000.

**Returns**: (Array) An array of up to 10 Objects containing:
- Number **lat**: The latitude of the hotspot
- Number **long**: The longitude of the hotspot.
- String **address**: A description of the hotspot's location.
- String **city**: The suburb containing the hotspot.
- String **state**: The state containing the hotspot.

[\[Example Request &amp; Result\]](https://gist.github.com/ozjd/fbf03ff2aa2c713cf0cf)

### Promises
Due to the asynchronous nature of this module, we have chosen to implement all methods using Promises. When we refer to a method returning a value, the method will return a promise that should resolve to that value if no error has occured. If an error occurs, the promise will be rejected with an error object containing a descriptive message.

Here's a quick example on how to use a promise returned by a method in this module. For more information on Promises and their usage, please refer to [Promises on MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise).

```javascript
t.<api>.<method>([arguments]).then(function (result) {
  //Successful call
  console.log("Result: " + result);
}, function (error) {
  //An error has occured.
  console.log("Error: " + error);
});
```

## License - MIT License (MIT)

```text
Copyright (c) 2016 Joshua 'JD' Davison

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
