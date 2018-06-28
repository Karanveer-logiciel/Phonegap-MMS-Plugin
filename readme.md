MMS Plugin to support Android JobProgress App. Modified according to our needs.


Phonegap-MMS-Plugin
=====================

This Android Phonegap plugin allows you to easily send MMS in android using both native SMS Manager or by invoking the default android SMS app. This plugin works with PhoneGap 3.x version.

The Android portion was forked from https://github.com/aharris88/phonegap-sms-plugin by aharris88
and then modified to support sending Multimedia Files and Text SMS.

Only Android support this time.

Installation
=================

Using the Phonegap CLI run:

    Cordova plugin add https://github.com/Karanveer-logiciel/Phonegap-MMS-Plugin

This will place the plugin in your plugins directory and update your android.json file that keeps track of installed plugins.


Example Usage
=================

HTML

    <input type="text" id="sendToNumber" placeholder="Send To" />
	</br>
	<input type="text" id="messageBody" placeholder="Message" />
	</br>
	<img id="myImage" style="border: 1px solid black; width: 125px; height: 75px;" />
	</br>
	<input type="button" value="Pick" onclick="pick()" />
	</br>
	</br>
	<input type="button" value="sendSms" onclick="sendSms()" />

Javascript

    
function sendSms() {
	var number = document.getElementById('sendToNumber').value;
	var message = document.getElementById('messageBody').value;

	var imageFile = document.getElementById("myImage").src;

	var intent = 'INTENT'; //leave empty for sending sms using default intent       
	sms.send(number, message, imageFile, intent, success, error);

	var success = function() {
		alert('Message sent successfully');
	};
	var error = function(e) {
		alert('Message Failed:' + e);
	};
}

function pick() {
	navigator.camera.getPicture(onSuccess, onFail, {
		quality: 50,
		destinationType: Camera.DestinationType.DATA_URL,
		sourceType: Camera.PictureSourceType.PHOTOLIBRARY
	});
	
function onSuccess(imageData) {
	var image = document.getElementById('myImage');
	image.src = "data:image/jpeg;base64," + imageData;
}

	function onFail(message) {
		alert('Failed because: ' + message);
	}
}

function base64() {
	var imgsrc = document.getElementById("myImage").src;
	alert(imgsrc);
}

Concept
=================
When you click pick, it will open up the file browser using camera plugin.
There you can insert image to an image source as Base64.

When you click Send SMS, the Send To, message & img src (base64) are passed to sms.java

Then the base64 is converted to bitmap & stored in sdcard and then open in native sms composer.

Always put “var intent = 'INTENT';“ in sendSms, so that the message would not be directly send.

** i haven't done any validation to check if the "To" or "Message" or "image src" is empty or not. 


License
=================

The MIT License (MIT)

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
