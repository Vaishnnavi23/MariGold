# Marigold Bank (Android WebView shell)

Open this folder in Android Studio (Koala or newer), let it sync, then Run.
Build > Build APK(s) produces app/build/outputs/apk/debug/app-debug.apk.

## Where to add your SDK
1. settings.gradle        - add your SDK's maven repo (or drop an .aar in app/libs).
2. app/build.gradle       - add the `implementation` line in dependencies.
3. AndroidManifest.xml    - add permissions / meta-data your SDK requires.
4. App.java / SdkBridge.init() - initialise the SDK once with your key.
5. SdkBridge.java         - call the SDK from track(), identify(), and add more methods.

## How the web screens talk to the SDK
index.html (app/src/main/assets) calls window.NativeSdk through a small `sdk()` helper:
screen_view, transfer_submitted, loan_submitted, loan_validation_failed.
Add more calls anywhere in the script, e.g. sdk('card_frozen', {on: v}).
The helper does nothing in a normal browser, so the page still works unchanged.

## Release
Create your own keystore and signing config before publishing; the APK I shared
was signed with a throwaway demo key.
