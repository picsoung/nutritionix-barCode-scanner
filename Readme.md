# Barcode scanner in PhoneGap linked to Nutritionix API

This is an example app to get nutrition facts by scanning a product's barcode.
It uses [Scandit SDK](www.scandit.com) for the Barcode scanner part and [Nutritionix API](https://developer.nutritionix.com/) to retrieve the nutrition facts.
This app is build using [Phonegap](www.phonegap.com) technology.

## Config
Get APIs keys from Scandit and Nutritionix and put them into the `www/config.json` file.

```json
{
    "scandit_key": "YOUR_SCANDIT_KEY",
    "nutri_key":"YOUR_NUTRITIONIX_APPKEY",
    "nutri_id":"YOUR_NUTRITIONIX_APPID"
}
```

##Test it
I only tested it on iOS device. You will need an iOS device and a registered Apple Developer Account.
it **can't** be tested on emulator because it requires to access the camera.

1. to test it clone the repo

  ```bash
  git clone git@github.com:picsoung/nutritionix-barCode-scanner.git
  cd nutritionix-barCode-scanner/
  ```

2. build the ios project

  `phonegap build ios`

3. launch the Xcode project in `platforms/ios/HelloWorld.xcodeproj` *apologies for the helloworld name*
4. plug your iOS device
5. press play button on Xcode and test it.