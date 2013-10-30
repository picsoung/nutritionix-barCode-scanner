BarcodeScannerPlugin
====================

Cross platform Phonegap/Cordova Plugin of the Scandit Barcode Scanner SDK for iOS and Android

Follow the detailed instructions below to add a high-performance barcode scanner to your app in 5 min using [Plugman](https://github.com/apache/cordova-plugman/).

If you don't have a Phonegap app yet, but want to try out our Phonegap/Cordova Plugins anyway, [follow the instructions on phonegap.com](http://docs.phonegap.com/) to generate a sample app. 


Scandit SDK Plugin Integration with Plugman 
------------------------

The easiest way to install the Scandit plugin into your Phonegap/Cordova project is to use [Plugman](https://github.com/apache/cordova-plugman/). 

* Sign up and download the Scandit SDK Cordova Plugins for iOS and Android from your Scandit SDK account.
* Generate a sample Cordova project or use your existing Cordova project

```
	cordova create .
	cordova platform add ios
	cordova platform add android
```

* Install Android and iOS Scandit SDK Plugin using [Plugman](https://github.com/apache/cordova-plugman/)

```
        plugman install --platform android --project <your project dir> --plugin <path to unzipped ScanditSDK Plugin for Android> 
```

```
        plugman install --platform ios --project <your project dir> --plugin <path to unzipped ScanditSDK Plugin for iOS> 
```
 
* Start using the Scandit SDK in your html code 
    * Get the app key from your Scandit SDK account
    * Invoke the Scandit SDK scanner by invoking the cordova.exec() function with the following parameters:

	`cordova.exec(function(success), function(cancel), "ScanditSDK", "scan", ["ENTER YOUR APP KEY HERE",{}]);`

    * See full example and API below for a detailed list of options. 

To install [Plugman](https://github.com/apache/cordova-plugman/):

         npm install -g plugman



Manual Scandit SDK Plugin Integration for iOS 
------------------------

* Download and add the Scandit SDK for iOS library to your Xcode Cordova Project:
    * Sign up for a free community license (or one of the enterprise packages) at http://www.scandit.com. 
    * Download the Scandit SDK Cordova Plugin for iOS version from your Scandit account and unzip it. 
    * Open your project in Xcode, right-click on the `Plugins` group in the navigation pane and select "Add Files to <name of your project>" 
    * Choose the files folders below from the zip you downloaded above (make sure you select the options `create group for added folders` and the `copy items to destination group's folder`):
         * ScanditSDK.h
         * ScanditSDK.mm
         * ScanditSDKRotatingBarcodePicker.h
         * ScanditSDKRotatingBarcodePicker.m
         * ScanditSDK folder (which includes the libscanditsdk-iphone-<version>.a static lib)

* Add frameworks needed by Scandit Barcode Scanner SDK:
    * Click on your project in the navigation pane of Xcode, then select your target and the tab "Build Phases" 
    * Under the entry "Link Binary with Libraries", add the following libraries by clicking the "+" button (most of them will already be listed):
         * AudioToolbox.framework
         * AVFoundation.framework
         * CoreGraphics.framework
         * CoreLocation.framework
         * CoreMedia.framework
         * CoreVideo.framework
         * QuartzCore.framework
         * SystemConfiguration.framework
         * libiconv.dylib
         * libz.dylib 
         * libc++.dylib
   
* Register the Plugin with your Cordova App:

    * Open the config.xml file and add the following xml element to the widget element

    ```
	<feature name="ScanditSDK" >
		<param name="ios-package" value="ScanditSDK" />
	</feature>
    ```


* Start using the Scandit SDK in your html code 
    * Get the app key from your Scandit SDK account
    * Invoke the Scandit SDK scanner by invoking the cordova.exec() function with the following parameters:
	Sample (minimal) `scan` usage: `cordova.exec(function(success), function(cancel), "ScanditSDK", "scan", ["ENTER YOUR APP KEY HERE",{}]);`
    * See full example and API below for a detailed list of options.  
         

Manual Scandit SDK Plugin Integration for Android
------------------------

* Download and add the Scandit SDK library for Android to your Eclipse Cordova Project:
    * Sign up for a free community license (or one of the enterprise packages) at http://www.scandit.com. 
    * Download the latest Scandit SDK Phonegap/Cordova for Android from your Scandit account. 
    * Unzip the downloaded zip file 
    * Copy the contents of the "libs" folder from the unzipped folder to the `libs` folder of your Phonegap/Cordova project. The `libs` folder includes the shared library libscanditsdk-android-*.so (in a folder called armeabi)
and the scanditsdk-barcodepicker-android-*.jar.
    * Copy the `res/raw` folder to the `res` folder of your Phonegap/Cordova project 
    * Copy the classes ScanditSDK.java and ScanditSDKActivity.java from the src/android folder (in the com.mirasense.scanditsdk.plugin package) into your project preserving the package hierarchy.
    * Refresh your eclipse project for the files to show up in Eclipse

* Add ScanditSDK jar file to your build path:
    * Right-click on the scanditsdk-barcodepicker-android-*.jar file in the libs folder and select "Add to Build Path"
   
* Register the Plugin with your Cordova App and set the permissions correctly:
    * Add ScanditSDK Activity to the "application" section of your app's AndroidManifest.xml file

    ```
     <activity android:name="com.mirasense.scanditsdk.plugin.ScanditSDKActivity"/>
    ```
    * Make sure the following permissions are listed in your AndroidManifest.xml file 

    ```
	<uses-permission android:name="android.permission.CAMERA" />
	<uses-permission android:name="android.permission.VIBRATE" />
	<uses-permission android:name="android.permission.INTERNET" />
    ```
    * Add the following xml element to the res/xml/config.xml resource's widget element

    ```

     <feature name="ScanditSDK">
                <param name="android-package" value="com.mirasense.scanditsdk.plugin.ScanditSDK"/>
     </feature>
    ```


* Start using the Scandit SDK in your html code 
    * Get the app key from your Scandit SDK account
    * Invoke the Scandit SDK scanner by invoking the cordova.exec() function with the following parameters:

	Sample (minimal) `scan` usage: 
```
cordova.exec(function(success), function(cancel), "ScanditSDK", "scan", ["YOUR APP KEY HERE",{}]);
```
    * See full example and API below for a detailed list of options. 


### Sample HTML + JS

```html
<!DOCTYPE html>
<html>
    <!--
     #
     # Licensed to the Apache Software Foundation (ASF) under one
     # or more contributor license agreements.  See the NOTICE file
     # distributed with this work for additional information
     # regarding copyright ownership.  The ASF licenses this file
     # to you under the Apache License, Version 2.0 (the
     # "License"); you may not use this file except in compliance
     # with the License.  You may obtain a copy of the License at
     #
     # http://www.apache.org/licenses/LICENSE-2.0
     #
     # Unless required by applicable law or agreed to in writing,
     # software distributed under the License is distributed on an
     # "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
     #  KIND, either express or implied.  See the License for the
     # specific language governing permissions and limitations
     # under the License.
     #
     -->
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <meta name = "format-detection" content = "telephone=no"/>
        <meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width;" />
        <link rel="stylesheet" type="text/css" href="css/index.css" />
        <title>Scandit SDK</title>
    </head>
    <body onload="onBodyLoad()" style="background: url(img/ScanditSDKDemo-Splash.png) no-repeat;background-size: 100%;background-color: #000000">
        <script type="text/javascript" src="cordova.js"></script>
        <script type="text/javascript" src="js/index.js"></script>
        <script type="text/javascript">
            function onBodyLoad()
            {
                document.addEventListener("deviceready", onDeviceReady, false);
            }
            
	    function success(resultArray) {

		alert("Scanned " + resultArray[0] + " code: " + resultArray[1]);

            	// NOTE: Scandit SDK Phonegap Plugin Versions 1.* for iOS report
            	// the scanning result as a concatenated string.
            	// Starting with version 2.0.0, the Scandit SDK Phonegap
            	// Plugin for iOS reports the result as an array
            	// identical to the way the Scandit SDK plugin for Android reports results.
            
            	// If you are running the Scandit SDK Phonegap Plugin Version 1.* for iOS,
            	// use the following approach to generate a result array from the string result returned:
            	// resultArray = result.split("|");
            }
            
            function failure(error) {
                alert("Failed: " + error);
            }
            
            function scan() {
                // See below for all available options. 
                cordova.exec(success, failure, "ScanditSDK", "scan",
                             ["ENTER YOUR APP KEY HERE",
                              {"beep": true,
                              "1DScanning" : true,
                              "2DScanning" : true}]);
            }
            
            app.initialize();
            </script>
        
        <div align="center" valign="center">
            <input type="button" value="scan" onclick="scan()" style="margin-top: 230px; width: 100px; height: 30px; font-size: 1em"/>
        </div>
    </body>
</html>

```


Changelog
------------------------

**Scandit SDK Phonegap Plugin for iOS and Android (2.2.0) - September 30th 2013**

 * upgraded to Scandit SDK for iOS 3.1.1 and Scandit SDK for Android 3.5.1 (see release notes in download section of your Scandit SDK for details)


**Scandit SDK Phonegap Plugin for iOS (2.1.0) and Android (1.2.0) - August 6th 2013**

 * support for Phonegap/Cordova 3.0 

 * upgraded to Scandit SDK 3.0.4 for iOS (for details see release notes in download section of your Scandit SDK account), Android version of plugin still uses Scandit SDK 3.3.1 for Android


**Scandit SDK Phonegap Plugin 2.0.1 for iOS only - June 17th 2013**

 * upgraded to Scandit SDK 3.0.3 for iOS which is a new bug fix release (see release notes of native iOS version for details)

**Scandit SDK Phonegap Plugin 2.0.0 for iOS only - May 11th 2013**

 * upgraded to new Scandit SDK 3.0.1 for iOS which comprises various new features: full screen scanning, 
   improved autofocus management, better scan performance and robustness, new cleaner scan screen interface 
   with the option to add a button to switch cameras and new symbologies (PDF417 beta and MSI-Plessey).

 * IMPORTANT: updated Scandit SDK Phonegap Plugin API to reflect updates in Scandit SDK 3.0.1 for iOS. 
   This includes a number of new API options (see below), a number of options have also disappeared. 

 * harmonized return results of Android and iPhone Plugin. In previous versions, 
   the iOS Plugin would return a string, while the Android Plugin would return an array. 
   Starting with Scandit SDK Phonegap Plugin for iOS 2.0.0, the iOS Plugin will also return an array. 



**Scandit SDK Phonegap Plugin 1.1.0 for Android & iOS - April 2nd 2013**

 * upgraded to native Scandit SDK 2.2.7 for iOS and 3.3.1 for Android
 
 * includes support PLUGMAN

 * Fixed a bug that would freeze and stop the modal view from closing.

 * Scandit SDK Phonegap Plugin for Android now also supports barcode scanning in landscape mode.

 * Minor changes to ScanditSDKActivity.java 




API for Scandit SDK Phonegap Plugin iOS and Android  
------------------------

See http://www.scandit.com/support for more information 



License
-------
* This plug-in is released under the Apache 2.0 license: http://www.apache.org/licenses/LICENSE-2.0



Questions? Contact `info@scandit.com`.




