Android Basic Fragment Example
==============================

Simple example of an activity launching another activity via an implicit and explicit intent.

If explicit button is clicked an explicit intent is used to call another class.

If implicit button is clicked an implicit intent is used to call another the app MyBrowser.

![implicit explicit screenshot](https://github.com/joninvski/android_intent_explicit_implicit_example/raw/master/images/app.png)


Compile
-------

    # Optional
    ANDROID_HOME=/home/.../android/sdk; export ANDROID_HOME

    ./gradlew compileDebug

Test
----

    # Make sure emulator is running or connected to real device
    ./gradlew connectedInstrumentTest


Code highlights
---------------

When the explicit button is clicked:

    // TODO - Create a new intent to launch the ExplicitlyLoadedActivity
    Intent intent = new Intent(this, ExplicitlyLoadedActivity.class);

    // TODO - Start an Activity using that intent and the request code
    startActivityForResult(intent, GET_TEXT_REQUEST_CODE);


When the implicit button is clicked

    // TODO - Create a base intent for viewing a URL
    Uri uri = Uri.parse("http://www.google.com");
    Intent baseIntent = new Intent(Intent.ACTION_VIEW, uri);

    // TODO - Create a chooser intent, for choosing which Activity
    // will carry out the baseIntent. Store the Intent in the
    // chooserIntent variable below.
    Intent chooserIntent = Intent.createChooser(baseIntent, "Load the link with: ");

    // TODO - Start the chooser Activity, using the chooser intent
    startActivity(chooserIntent);

In the App accepting this intent (MyBrowser in this case) add to AndroidManifest.xml

    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="http" />
    </intent-filter>
