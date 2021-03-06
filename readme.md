Admob ANE for Flash Air
==============================
1. [Admob ANE Description](#admob-ane-description)
2. [Admob ANE For Air Features](#admob-ane-for-air-features)
3. [Quick Start](#quick-start)    
	1.[Init Admob ANE ](#1init-admob-ane)     
	2.[Add Admob Banner in adobe Air App](#2add-admob-banner-in-adobe-air-app)    
	3.[Remove Banner](#3remove-banner)    
	4.[Admob Native Express Ads](#4admob-native-express-ads)    
	5.[Admob ANE Show Interstitial ](#5admob-ane-show-interstitial )    
	6.[Custom Admob Banner Ad Sizes](#6custom-admob-banner-ad-sizes)    
	7.[Set Admob Target Param](#7set-admob-target-param)    
	8.[Ad Events](#8ad-events)    
	9.[IOS  permission config](#9ios-permission-config)    
	10.[android permission config](#10android-permission-config)    
	11.[Screen size function](#11screen-size-function)    
	12.[ANE ID](#12ane-id)    
4. [change log](#change-log)
5. [Screenshots](#screenshots)
6. [Links](#links)
7. [License](#license)

## Admob ANE Description
Admob Air Native Extention(Admob ANE) provides a way to integrate admob ads in Air ios and Air Android Game and app.
You can use it for Air iOS and Android App with the same actionscript  code,not need any change ,not need java
or oc.You not need Admob ANE for ios and Admob ANE for android Separate version any more with this Ane.

The Google Mobile Ads SDK is the latest generation in Google mobile advertising featuring refined ad formats and streamlined APIs for access to mobile ad networks and advertising solutions. The SDK enables Air mobile app developers to maximize their monetization in native mobile apps.

This Admob ANE  was published  since Sep, 2012, and has been downloaded more than 100,000 times. Now it's the No. 1 monetization ANE plugin for Flash Air community,More people use, making the api more friendly,the plugin more stable.Thank you for feedback questions and provide advice, thank you for the support and donations.


## Admob ANE For Air Features
- [x] Support IOS and Android in one ane with the same api
- [x] Support banner(All Banner Sizes)
- [x] Support Intersitial
- [x] Support native express ads
- [x] Support all native events
- [x] Support landscape and portrait  and autoOrient
- [x] Support AdRequest targeting methods,such as children target,test mode
- [x] Support Air SDK 17 to the last version 
- [x] Support IOS 7 to the last version 
- [x] Very simple API


## Quick Start
#### 1.Init Admob ANE 
Add Admob ane to air project build path , add the follow code in the script file
```
    import so.cuo.platform.admob.*;
    Admob.getInstance().setKeys("your admob banner id","your admob institial id");

```
#### 2.Add Admob Banner in adobe Air App 
Here is the minimal code needed to show admob banner.
```
    Admob.getInstance().showBanner(AdmobSize.BANNER_320x50,AdmobPosition.BOTTOM_CENTER);

```

The AdmobPosition class specifies where to place the banner. AdmobSize specifies witch size banner to show

#### 3.Remove Banner 
By default, banners are visible. To  hide a banner,
```
    Admob.getInstance().hideBanner();
```

#### 4.Admob Native Express Ads
How to show native express ads in flash air ios and android application?    
native express ads is a admob new ad format similar to banner,so the api is similar too    
Show admob native banner.        
```
    Admob.getInstance().showNativeBannerAbsolute(nativeID,new AdmobSize(320,132),0,260);
```

nativeID is got from apps.admob.com format like ca-app-pub-3940256099942544/2562852117    
AdSize is the value you set in apps.admob.com    
if you want to show multi native banner ,you can pass a instanceName value


Hide admob native banner
```
    Admob.getInstance().hideNativeBanner();
```

#### 5.Admob ANE Show Interstitial 
How to integrate Interstitial into Air ios  app or flex android app?
Here is the minimal  code to create an interstitial.
```
    Admob.getInstance().cacheInterstitial(); 
```
interstitials need to be loaded before shown. show at an appropriate
stopping point in your app, check that the interstitail is ready before
showing it:
```
    if (Admob.getInstance().isInterstitialReady()) {
      Admob.getInstance().showInterstitial();
    }
```
#### 6.Custom Admob Banner Ad Sizes
In addition to constants on _AdSize_, you can also create a custom size:
```
    //Create a 320x250 banner.
    AdSize adSize = new AdSize(320, 250);
    Admob.getInstance().showBannerAbsolute(adSize,0,30);
```
#### 7.Set Admob Target Param
set Admob target param such as test Ads and children app
If you want to test the ads or the your app with children target,you can set with admob ANE easy
```
       extraParam=new ExtraParameter();
	extraParam.testDeviceID="true";
	extraParam.isChildApp=true;
	Admob.getInstance().showBanner(AdmobSize.BANNER_320x50,AdmobPosition.BOTTOM_CENTER,80,extraParam);
```
#### 8.Ad Events
Both _Banner_ and _Interstitial_ contain the many ad events that you can
register for.    
Here we'll demonstrate setting ad events on a interstitial,and show interstitial when load success:
```
    Admob.getInstance().addEventListener(AdmobEvent.onInterstitialReceive, onAdEvent);
	private function onAdEvent(event:AdmobEvent):void
	{
		if (event.type == AdmobEvent.onBannerReceive)
		{
			trace(event.instanceName,event.data.width, event.data.height);
		}
		if (event.type == AdmobEvent.onInterstitialReceive)
		{
			Admob.getInstance().showInterstitial();
		}
	}
```



###  9.IOS  permission config
NSAppTransportSecurity is required for ios 9,if you compile with air 21,it is required to add NSAppTransportSecurity key
```
	<key>NSAppTransportSecurity</key>
			<dict>
			 <key>NSAllowsArbitraryLoads</key>
			 <true/>
			</dict>
```
simple example
```
 <iPhone>
        <InfoAdditions><![CDATA[
			<key>UIDeviceFamily</key>
			<array>
				<string>1</string>
				<string>2</string>
			</array>
			<key>NSAppTransportSecurity</key>
			<dict>
			 <key>NSAllowsArbitraryLoads</key>
			 <true/>
			</dict>
		]]></InfoAdditions>
        <requestedDisplayResolution>high</requestedDisplayResolution>
    </iPhone>
```


### 10.android permission config
```
<android>
        <manifestAdditions><![CDATA[
			<manifest android:installLocation="auto">
			    <uses-permission android:name="android.permission.INTERNET"/>
			    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
			    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
			     <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
			     <application>
 <meta-data android:name="com.google.android.gms.version"
        android:value="@integer/google_play_services_version" />
			  	   <activity android:name="com.google.android.gms.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" android:theme="@android:style/Theme.Translucent"/>
			     </application>
			</manifest>
		]]></manifestAdditions>
    </android>
```

### 11.Screen size function
this will get  screen size ,unit is dp
```
Admob.getInstance().getScreenSize()

```

### 12.ANE ID
```
<extensionID>so.cuo.platform.admob</extensionID>
```
## change log
1.upgrade ios(7.8) and android sdk(9.2)
2.fix android resource not found error
[more](https://github.com/lilili87222/admob-for-flash/blob/master/changelog.txt)    

## Screenshots
![ScreenShot](https://github.com/lilili87222/admob-for-flash/blob/master/images/screen.jpg?raw=true)

## Links
Download  https://github.com/lilili87222/admob-for-flash/archive/master.zip    
Our Games https://itunes.apple.com/us/artist/phonegame/id553087275?mt=8    
donation paypal li_li_li87222@163.com     
admob http://apps.admob.com    

## License
[Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0.html)