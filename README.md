## Bitcoin Signature App

This app takes the bitcoin signature tool standalone web app and turns it into a basic Android app.

For more information about the app and the protocol it was built for visit https://bitcointalk.org/index.php?topic=1232915

## Building From Source
###Prerequisites

* Install Java SDK
* Install Android SDK
* From the Android SDK Manager make sure you have:
    * Tools/Android SDK Tools
    * Tools/Android SDK Platform-tools
    * API 22/SDK Platform
* Install Node.js

    npm install -g phonegap

### Building with signature (using temporary keystore)

    cd platforms/android
    phonegap build android --release
    mv "build/outputs/apk/android-release-unsigned.apk" "build/outputs/apk/bitcoinsignaturetool-release-u.apk"
    jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore "tempkey.keystore" \
        "build/outputs/apk/bitcoinsignaturetool-release-u.apk" alias_name
    jarsigner -verify -verbose -certs "build/outputs/apk/bitcoinsignaturetool-release-u.apk"
    zipalign -v 4 "build/outputs/apk/bitcoinsignaturetool-release-u.apk" \
        "build/outputs/apk/bitcoinsignaturetool-release.apk"

Built files are at platforms/android/build/outputs/apk/ and bitcoinsignaturetool-release.apk is the release one that we have just created above.
