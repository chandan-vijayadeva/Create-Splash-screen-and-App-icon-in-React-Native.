# Create-Splash-screen-and-App-icon-in-React-Native.

# Step 1:  yarn add react-native-splash-screen

# Step 2:  Plugin installation

## Automatic installation: 

    react-native link react-native-splash-screen or rnpm link react-native-splash-screen

## Manual installation:

# Android:

1.	In your android/settings.gradle file, make the following additions:
include ':react-native-splash-screen'   
project(':react-native-splash-screen').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-splash-screen/android')
2.	In your android/app/build.gradle file, add the :react-native-splash-screen project as a compile-time dependency:
    ...
    dependencies {
        ...
        implementation project(':react-native-splash-screen')
    }

# iOS:

1.	cd ios
2.	run pod install
in  ios after yarn add react-native-splash-screen , cd to ios and do pod install, that will take care of all the linking operations.
OR
1.	In XCode, in the project navigator, right click Libraries ➜ Add Files to [your project's name]
2.	Go to node_modules ➜ react-native-splash-screen and add SplashScreen.xcodeproj
3.	In XCode, in the project navigator, select your project. Add libSplashScreen.a to your project's Build Phases ➜ Link Binary With Libraries
4.	To fix 'RNSplashScreen.h' file not found, you have to select your project → Build Settings → Search Paths → Header Search Paths to add:
$(SRCROOT)/../node_modules/react-native-splash-screen/ios


# Step 3: Plugin Configuration

## Android:

Update the MainActivity.java to use react-native-splash-screen via the following changes:

    import android.os.Bundle; // to be added
    import com.facebook.react.ReactActivity;
    // react-native-splash-screen >= 0.3.1
    import org.devio.rn.splashscreen.SplashScreen; // here
    // react-native-splash-screen < 0.3.1
    import com.cboy.rn.splashscreen.SplashScreen; // here

    public class MainActivity extends ReactActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        SplashScreen.show(this);  // to be added
        super.onCreate(null);
    }
    // ...other code
    }


## iOS:

Update AppDelegate.m with the following additions:

    #import "AppDelegate.h"

    #import <React/RCTBundleURLProvider.h>
    #import "RNSplashScreen.h"  // to be added

    @implementation AppDelegate

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      self.moduleName = @"YOUR_APP_NAME";
      // You can add your custom initial props in the dictionary below.
      // They will be passed down to the ViewController used by React Native.
      self.initialProps = @{};
      [super application:application didFinishLaunchingWithOptions:launchOptions];
      [RNSplashScreen show];   // to be added
       return YES;
    }



# Step 4:

Import react-native-splash-screen in your JS file.
import SplashScreen from 'react-native-splash-screen'

## Android:
Create a file called launch_screen.xml in app/src/main/res/layout (create the layout-folder if it doesn't exist). The contents of the file should be the following:

    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical" android:layout_width="match_parent"
        android:layout_height="match_parent">
        <ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/image_name"  android:scaleType="centerCrop" />
    </RelativeLayout>



Add splash screen image in drawable folder and provide the name in launch_screen.xml 


# Step 5: Implementation in React native

	Inside AppStackNavigator.js or in App.js

    ...
    import SplashScreen from 'react-native-splash-screen';
    ...

    const AppStackNavigator = () => {

    // To  hide splash screen
      useEffect(() => {
        setTimeout(() => {
          SplashScreen.hide(); //
        }, 3000);
      }, []);

      return (
        <NavigationContainer>
          <Stack.Navigator
            screenOptions={{
              headerShown: false,
            }}>
            <Stack.Screen name="login" component={login} />
          </Stack.Navigator>
        </NavigationContainer>
      );
    };

    export default AppStackNavigator;





# To add app icon 

## Android:

Step 1: Visit https://icon.kitchen/ or any other appicon builder website and download the generated zip folder.
Step 2: Extract the zip folder, open android folder -> open res folder -> copy all files present inside res folder and paste inside “android/app/src/main/res”
Step 3: open AndroidManifest.xml present in “android/app/src/main” 

And replace below name with the name that are present inside mipmap folders

Example : android:icon = “@mipmap/image-name.png

    android:icon="@mipmap/ic_launcher"
    android:roundIcon="@mipmap/ic_launcher"

Uninstall the app and rerun the app


## iOS:

Step 1: Visit https://icon.kitchen/ or any other appicon builder website and download the generated zip file

	
Step 2:  Extract Zip folder,  open ios folder -> AppIcon.appiconset , drag AppIcon.appiconset to image assets folder.

Uninstall the app and rerun the app.


# Reference:

-> https://icon.kitchen/ 

