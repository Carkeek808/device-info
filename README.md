# DeviceInfo

#### Library size is : 31Kb

Android library to get device information in a super easy way.
DeviceInfo library gives you details of Hardware & Software configurations of your Android device.
This detail specifications includes information of CPU, RAM, Storage, OS, Sensors, Core, Battery, Data Network, WiFi, SIM, Bluetooth, Display, Supported features, Manufacturer, Installed Apps.


Add this to your project build.gradle
``` gradle
allprojects {
    repositories {
        maven {
            url "https://jitpack.io"
        }
    }
}
```
 
#### Dependency
[![](https://jitpack.io/v/appsfeature/device-info.svg)](https://jitpack.io/#appsfeature/device-info)
```gradle
dependencies {
    implementation 'com.github.appsfeature:device-info:x.y'
}
```

#### Usage method
In your activity class:
```java 
      DeviceInfo.getInstance()
              .setEnablePermissionRequiredInfo(true)
              .setDebugMode(true)
              .setPermission(Manifest.permission.ACCESS_FINE_LOCATION)
              .addCallback(new DeviceInfoCallback<DeviceInfoResult>() {
                  @Override
                  public void onSuccess(DeviceInfoResult response) {
                      Log.d("onSuccess",response.toString());
                  }

                  @Override
                  public void onError(Exception e) {
                      Log.d("onError",e.getMessage());
                  }
              });

      // call this method from Main thread.
      DeviceInfo.getInstance().fetch(this);
                       -OR-
      // call this method from Worker thread.
      DIResult result = DeviceInfo.getInstance().fetchEnqueue(this);
```


#### Permissions Required
Add following Permission in your Manifest file if need the following details(Network, SIM, Bluetooth).
## Network
```xml
    Normal Permission
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

    Runtime Permission
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```
## SIM
```xml
    Runtime Permission
        <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```
## Bluetooth
```xml
    Normal Permission
        <uses-permission android:name="android.permission.BLUETOOTH"/>
```
## Application
```xml
    Normal Permission
        <uses-permission android:name="android.permission.QUERY_ALL_PACKAGES"
                tools:ignore="QueryAllPackagesPermission" />

        <queries>
            <intent>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="https" />
            </intent>
            <intent>
                <action android:name="android.intent.action.VIEW" />
                <!-- If you don't know the MIME type in advance, set "mimeType" to "*/*". -->
                <data android:mimeType="application/pdf" />
            </intent>
            <intent>
                <action android:name="android.intent.action.TTS_SERVICE" />
            </intent>
            <intent>
                <action android:name="android.speech.RecognitionService" />
            </intent>
            <intent>
                <action android:name="android.media.browse.MediaBrowserService" />
            </intent>
            <intent>
                <action android:name="android.intent.action.SENDTO"/>
                <data android:scheme="smsto" android:host="*" />
            </intent>
        </queries>
```


Device Info provides following information of your Android device which grouped as below.

## Android Device Information
```  
UserDeviceInfo.get().getInfo(context)               : HashMap<String, String>
UserDeviceInfo.get().getBuildSDKVersion()           : int
UserDeviceInfo.get().getAndroidOSName()             : String
UserDeviceInfo.get().getOSVersion()                 : String
UserDeviceInfo.get().getBaseOSVersion()             : String
UserDeviceInfo.get().getDisplayVersion()            : String
UserDeviceInfo.get().getBoard()                     : String
UserDeviceInfo.get().getBootloader()                : String
UserDeviceInfo.get().getBuildBrand()                : String
UserDeviceInfo.get().getBuildHost()                 : String
UserDeviceInfo.get().getBuildTags()                 : String
UserDeviceInfo.get().getBuildUser()                 : String
UserDeviceInfo.get().getBuildVersionCodename()      : String
UserDeviceInfo.get().getBuildVersionIncremental()   : String
UserDeviceInfo.get().getBuildVersionRelease()       : String  
UserDeviceInfo.get().getDevice()                    : String
UserDeviceInfo.get().getFingerprint()               : String
UserDeviceInfo.get().getHardware()                  : String
UserDeviceInfo.get().getLanguage()                  : String
UserDeviceInfo.get().getManufacturer()              : String
UserDeviceInfo.get().getModel()                     : String
UserDeviceInfo.get().getDeviceId(context)           : String
UserDeviceInfo.get().getPhoneNo(context)            : String
UserDeviceInfo.get().getProduct()                   : String
UserDeviceInfo.get().getRadioVer()                  : String
UserDeviceInfo.get().getScreenDisplayID(context)    : String
UserDeviceInfo.get().getSerial(context)             : String
UserDeviceInfo.get().getDeviceType(context)         : String
UserDeviceInfo.get().getPhoneType(context)          : String
UserDeviceInfo.get().getPhoneTypeMod(context)       : int
UserDeviceInfo.get().getBuildID()                   : String
UserDeviceInfo.get().getBuildTime()                 : long
UserDeviceInfo.get().getOrientation(context)        : int
UserDeviceInfo.get().isDeviceRooted()               : boolean
UserDeviceInfo.get().isDeveloperModeEnabled(context): boolean
UserDeviceInfo.get().isWifiAdbEnabled(context)      : boolean   
UserDeviceInfo.get().isRunningOnEmulator()          : boolean   
```
## Battery
```
Battery.get().getInfo(context)                      : HashMap<String, String>
Battery.get().getBatteryTechnology(context)         : String
Battery.get().getBatteryTemperature(context)        : float
Battery.get().getBatteryVoltage(context)            : int
Battery.get().getDeviceChargingState(context)       : String
Battery.get().getChargingSource(context)            : String
Battery.get().getChargingSourceIndexDetail(context) : String
Battery.get().isBatteryPresent(context)             : boolean
Battery.get().getBatteryPercentage(context)         : int
Battery.get().getBatteryHealth(context)             : String
```
## Sensor
```
Sensors.get().getAllSensors(context)            : List<Sensor>
```
## CPU
```
CPU.get().getInfo()                             : HashMap<String, String>
CPU.get().getCPUInfo()                          : HashMap<String, String>
CPU.get().getStringSupported32bitABIS()         : String
CPU.get().getStringSupported64bitABIS()         : String
CPU.get().getStringSupportedABIS()              : String
CPU.get().getSupportedABIS()                    : String[]
CPU.get().getNumCores()                         : int 
```
## Network (permission required)
```
Network.get().getInfo(context)                  : HashMap<String, String>
Network.get().getAllCellInfo(context)           : List<CellInfo>
Network.get().loadCellTowerInfo(context)        : String
Network.get().isWifiEnabledDetail(context)      : String
Network.get().getMACAddress(context)            : String
Network.get().getWifiBSSID(context)             : String
Network.get().isNetworkAvailable(context)       : String
Network.get().isInternetConnected(context)      : boolean
Network.get().getIPv4Address(context)           : String
Network.get().getIPv6Address(context)           : String
Network.get().getDataType(context)              : String
Network.get().getWifiSSID(context)              : String
Network.get().getWifiLinkSpeed(context)         : String
```
## SIM (permission required)
```
DeviceSim.get().getInfo(context)                : HashMap<String, String> 
DeviceSim.get().getActiveMultiSimInfo(context)  : List<SubscriptionInfo>
DeviceSim.get().getCarrier(context)             : String
DeviceSim.get().isSimNetworkLocked(context)     : String
DeviceSim.get().getIMEI(context)                : String
DeviceSim.get().getIMSI(context)                : String
DeviceSim.get().getNumberOfActiveSim(context)   : String
DeviceSim.get().getSIMSerial(context)           : String
DeviceSim.get().getSIMSerial(context)           : String
```
## Storage
```
DeviceMemory.get().getInfo(context)                 : HashMap<String, String>
DeviceMemory.get().getTotalInternalMemorySize()     : long 
DeviceMemory.get().getAvailableInternalMemorySize() : long 
DeviceMemory.get().getTotalRAM()                    : long 
DeviceMemory.get().totalRamMemorySize()             : long 
DeviceMemory.get().freeRamMemorySize()              : long 
DeviceMemory.get().externalMemoryAvailable()        : String 
DeviceMemory.get().getTotalExternalMemorySize()     : long 
DeviceMemory.get().getAvailableExternalMemorySize() : long 
DeviceMemory.get().convertToGbFormatted()           : String 
```
## Bluetooth (permission required)
```
Bluetooth.get().getInfo(context)                    : HashMap<String, String> 
Bluetooth.get().hasBluetoothLe(context)             : Boolean
Bluetooth.get().hasBluetoothLeDetail(context)       : String
Bluetooth.get().hasBluetoothLeAdvertising(context)  : String
```
## Display
```
DeviceDisplay.get().getInfo(context)                : HashMap<String, String> 
DeviceDisplay.get().getDisplayObject(context)       : Display 
DeviceDisplay.get().getDensity(context)             : String 
DeviceDisplay.get().getPhysicalSize(context)        : String 
DeviceDisplay.get().getOrientation(context)         : int 
DeviceDisplay.get().getDeviceOrientation(context)   : String 
DeviceDisplay.get().getLayoutDirection(context)     : int 
DeviceDisplay.get().getResolution(context)          : String 
DeviceDisplay.get().isScreenRound(context)          : boolean 
DeviceDisplay.get().getRefreshRate(context)         : String 
DeviceDisplay.get().getDisplayXYCoordinates(context) : int[] 
```
## Features
```
Feature.get().getInfo(context)                      : HashMap<String, String>   
Feature.get().getDeviceList(context)                : HashMap<String, UsbDevice>
Feature.get().getConnectedDevicesList(context)      : String
Feature.get().isNfcEnabled(context)                 : boolean
Feature.get().checkMultiTouchSupport(context)       : boolean
```
## DeviceConfig
```
DeviceConfig.get().getInfo(context)                 : HashMap<String, String>    
DeviceConfig.get().getCurrentDate()                 : String
DeviceConfig.get().getDeviceRingerMode(context)     : String
DeviceConfig.get().getFormattedDate()               : String
DeviceConfig.get().getFormattedTime()               : String
DeviceConfig.get().getFormattedUpTime()             : String
DeviceConfig.get().hasSdCard()                      : String

DeviceConfig.isDeveloperModeEnabled(context)        : boolean
DeviceConfig.isWifiAdbEnabled(context)              : boolean   
DeviceConfig.isDeviceRooted()                       : boolean
DeviceConfig.isRunningOnEmulator()                  : boolean   
```

```json
{
  "applicationInfo": [
    {
      "activities": "org.chromium.chrome.browser.document.ChromeLauncherActivity,com.google.android.apps.chrome.TranslateDispatcher,com.google.android.apps.chrome.IntentDispatcher,org.chromium.chrome.browser.media.PictureInPictureActivity,org.chromium.chrome.browser.LauncherShortcutActivity,org.chromium.chrome.browser.incognito.IncognitoTabLauncher,org.chromium.chrome.browser.app.reengagement.ReengagementActivity,org.chromium.chrome.browser.customtabs.CustomTabActivity,org.chromium.chrome.browser.customtabs.TranslucentCustomTabActivity,org.chromium.chrome.browser.ChromeTabbedActivity,com.google.android.apps.chrome.Main,org.chromium.chrome.browser.ChromeTabbedActivity2,org.chromium.chrome.browser.multiwindow.MultiInstanceChromeTabbedActivity,org.chromium.chrome.browser.sync.ui.SyncTrustedVaultProxyActivity,org.chromium.chrome.browser.sync.ui.PassphraseActivity,org.chromium.chrome.browser.firstrun.LightweightFirstRunActivity,org.chromium.chrome.browser.firstrun.FirstRunActivity,org.chromium.chrome.browser.firstrun.TabbedModeFirstRunActivity,org.chromium.chrome.browser.vr.VrFirstRunActivity,org.chromium.chrome.browser.signin.SyncConsentActivity,org.chromium.chrome.browser.settings.SettingsActivity,org.chromium.chrome.browser.site_settings.ManageSpaceActivity,org.chromium.chrome.browser.app.bookmarks.BookmarkActivity,org.chromium.chrome.browser.app.bookmarks.BookmarkEditActivity,org.chromium.chrome.browser.app.bookmarks.BookmarkAddEditFolderActivity,org.chromium.chrome.browser.app.bookmarks.BookmarkFolderSelectActivity,org.chromium.chrome.browser.app.video_tutorials.VideoTutorialListActivity,org.chromium.chrome.browser.app.download.home.DownloadActivity,org.chromium.chrome.browser.download.DownloadActivity,org.chromium.chrome.browser.app.feed.feedmanagement.FeedManagementActivity,org.chromium.chrome.browser.app.feed.followmanagement.FollowManagementActivity,org.chromium.chrome.browser.app.creator.CreatorActivity,org.chromium.chrome.browser.app.video_tutorials.VideoPlayerActivity,org.chromium.chrome.browser.history.HistoryActivity,org.chromium.chrome.browser.webapps.WebappLauncherActivity,com.google.android.apps.chrome.webapps.WebappManager,org.chromium.chrome.browser.webapps.SecureWebAppLauncher,org.chromium.chrome.browser.webapps.WebappActivity,com.google.android.apps.chrome.webapps.WebappActivity,org.chromium.chrome.browser.webapps.SameTaskWebApkActivity,org.chromium.chrome.browser.webapps.ActivateWebApkActivity,org.chromium.components.media_router.caf.remoting.CafExpandedControllerActivity,org.chromium.chrome.browser.BrowserRestartActivity,org.chromium.chrome.browser.vr.VrCancelAnimationActivity,org.chromium.chrome.browser.browserservices.ClearDataDialogActivity,org.chromium.chrome.browser.browserservices.ManageTrustedWebActivityDataActivity,org.chromium.chrome.browser.webauth.authenticator.CableAuthenticatorActivity,org.chromium.chrome.browser.webauth.authenticator.CableAuthenticatorUSBActivity,org.chromium.chrome.browser.bookmarkswidget.BookmarkWidgetProxy,org.chromium.chrome.browser.searchwidget.SearchActivity,org.chromium.chrome.browser.notifications.NotificationIntentInterceptor$TrampolineActivity,org.chromium.chrome.browser.price_tracking.PriceDropNotificationManagerImpl$TrampolineActivity,org.chromium.chrome.browser.price_tracking.PriceDropNotificationManagerImpl$DismissNotificationChromeActivity,org.chromium.chrome.browser.test_dummy.TestDummyActivity,org.chromium.chrome.browser.abp.onboarding.OnboardingActivity,org.chromium.chrome.browser.abp.feedback.StillSeeAdsActivity,org.chromium.chrome.browser.abp.feedback.FeedbackActivity,org.chromium.chrome.browser.abp.preferences_ui.DefaultBrowserBottomSheetActivity,org.crumbs.ui.CrumbsSettingsActivity,org.crumbs.ui.relay.CrumbsRelayLoginActivity,org.adblockplus.browser.modules.crumbs.onboarding.CrumbsOnboardingActivity,org.adblockplus.browser.modules.onboarding.OnboardingActivity,com.google.android.gms.common.api.GoogleApiActivity,org.adblockplus.browser.modules.issue_reporter.IssueReporterActivity,com.google.firebase.auth.internal.GenericIdpActivity,com.google.firebase.auth.internal.RecaptchaActivity,org.adblockplus.browser.modules.feedback.FeedbackActivity",
      "app_installed_date_formatted": "22-02-2023 | 12:02 pm",
      "app_last_modified_date_formatted": "28-04-2024 | 02:55 pm",
      "icon": {
        "mSrcDensityOverride": 0
      },
      "installedDate": 1677047523452,
      "label": "com.google.android.apps.chrome.Main",
      "lastModified": 1714296323330,
      "launchActivity": "com.google.android.apps.chrome.Main",
      "name": "Adblock Browser",
      "packageName": "org.adblockplus.browser",
      "providers": "org.chromium.chrome.browser.util.ChromeFileProvider,org.chromium.chrome.browser.download.DownloadFileProvider,org.chromium.ui.dragdrop.DropDataContentProvider,org.chromium.chrome.browser.provider.ChromeBrowserProvider,com.google.firebase.provider.FirebaseInitProvider",
      "reqPermission": "ACCESS_WIFI_STATE, ACCESS_NETWORK_STATE, BLUETOOTH, REORDER_TASKS, DOWNLOAD_WITHOUT_NOTIFICATION, FOREGROUND_SERVICE, INTERNET, MODIFY_AUDIO_SETTINGS, NFC, POST_NOTIFICATIONS, QUERY_ALL_PACKAGES, RECEIVE_BOOT_COMPLETED, USE_CREDENTIALS, USE_BIOMETRIC, USE_FINGERPRINT, VIBRATE, WAKE_LOCK, C2D_MESSAGE, READ_WRITE_BOOKMARK_FOLDERS, TOS_ACKED, RECEIVE, INSTALL_SHORTCUT, AD_ID, BIND_GET_INSTALL_REFERRER_SERVICE",
      "services": "org.chromium.chrome.browser.photo_picker.DecoderService,org.chromium.chrome.browser.download.DownloadForegroundService,org.chromium.chrome.browser.download.DownloadBroadcastManager,org.chromium.chrome.browser.bookmarkswidget.BookmarkWidgetService,com.google.ipc.invalidation.ticl.android2.channel.GcmRegistrationTaskService,org.chromium.chrome.browser.services.gcm.ChromeGcmListenerService,org.chromium.chrome.browser.services.gcm.GCMBackgroundService,org.chromium.chrome.browser.services.gcm.InvalidationGcmUpstreamSender,org.chromium.chrome.browser.notifications.NotificationService,org.chromium.chrome.browser.notifications.NotificationJobService,org.chromium.components.background_task_scheduler.internal.BackgroundTaskJobService,org.chromium.chrome.browser.ChromeBackgroundService,org.chromium.chrome.browser.prerender.ChromePrerenderService,org.chromium.chrome.browser.customtabs.CustomTabsConnectionService,androidx.browser.customtabs.PostMessageService,org.chromium.chrome.browser.crash.ChromeMinidumpUploadJobService,org.chromium.chrome.browser.crash.MinidumpUploadService,org.chromium.chrome.browser.incognito.IncognitoNotificationService,org.chromium.components.payments.PaymentDetailsUpdateService,org.chromium.chrome.browser.webapps.WebApkInstallCoordinatorService,org.chromium.chrome.browser.media.MediaCaptureNotificationService,org.chromium.chrome.browser.media.ui.ChromeMediaNotificationControllerServices$PlaybackListenerService,org.chromium.chrome.browser.media.ui.ChromeMediaNotificationControllerServices$PresentationListenerService,org.chromium.chrome.browser.media.ui.ChromeMediaNotificationControllerServices$CastListenerService,org.chromium.chrome.browser.tracing.TracingNotificationService,org.chromium.chrome.browser.app.bluetooth.BluetoothNotificationService,org.chromium.chrome.browser.app.usb.UsbNotificationService,org.chromium.content.app.SandboxedProcessService0,org.chromium.content.app.SandboxedProcessService1,org.chromium.content.app.SandboxedProcessService2,org.chromium.content.app.SandboxedProcessService3,org.chromium.content.app.SandboxedProcessService4,org.chromium.content.app.SandboxedProcessService5,org.chromium.content.app.SandboxedProcessService6,org.chromium.content.app.SandboxedProcessService7,org.chromium.content.app.SandboxedProcessService8,org.chromium.content.app.SandboxedProcessService9,org.chromium.content.app.SandboxedProcessService10,org.chromium.content.app.SandboxedProcessService11,org.chromium.content.app.SandboxedProcessService12,org.chromium.content.app.SandboxedProcessService13,org.chromium.content.app.SandboxedProcessService14,org.chromium.content.app.SandboxedProcessService15,org.chromium.content.app.SandboxedProcessService16,org.chromium.content.app.SandboxedProcessService17,org.chromium.content.app.SandboxedProcessService18,org.chromium.content.app.SandboxedProcessService19,org.chromium.content.app.SandboxedProcessService20,org.chromium.content.app.SandboxedProcessService21,org.chromium.content.app.SandboxedProcessService22,org.chromium.content.app.SandboxedProcessService23,org.chromium.content.app.SandboxedProcessService24,org.chromium.content.app.SandboxedProcessService25,org.chromium.content.app.SandboxedProcessService26,org.chromium.content.app.SandboxedProcessService27,org.chromium.content.app.SandboxedProcessService28,org.chromium.content.app.SandboxedProcessService29,org.chromium.content.app.SandboxedProcessService30,org.chromium.content.app.SandboxedProcessService31,org.chromium.content.app.SandboxedProcessService32,org.chromium.content.app.SandboxedProcessService33,org.chromium.content.app.SandboxedProcessService34,org.chromium.content.app.SandboxedProcessService35,org.chromium.content.app.SandboxedProcessService36,org.chromium.content.app.SandboxedProcessService37,org.chromium.content.app.SandboxedProcessService38,org.chromium.content.app.SandboxedProcessService39,org.chromium.content.app.PrivilegedProcessService0,org.chromium.content.app.PrivilegedProcessService1,org.chromium.content.app.PrivilegedProcessService2,org.chromium.content.app.PrivilegedProcessService3,org.chromium.content.app.PrivilegedProcessService4,com.google.firebase.components.ComponentDiscoveryService,com.google.firebase.messaging.FirebaseMessagingService,com.google.android.gms.cast.framework.media.MediaNotificationService,com.google.android.gms.cast.framework.ReconnectionService,com.google.android.datatransport.runtime.scheduling.jobscheduling.JobInfoSchedulerService,com.google.android.datatransport.runtime.backends.TransportBackendDiscovery,com.google.android.gms.measurement.AppMeasurementService,com.google.android.gms.measurement.AppMeasurementJobService,com.google.firebase.auth.api.fallback.service.FirebaseAuthFallbackService",
      "version": "3.4.5",
      "versionCode": "2064000053"
    },
    {
      "activities": "com.amazon.mShop.navigation.MainActivity,com.amazon.mShop.splashscreen.StartupActivity,com.amazon.windowshop.home.HomeLauncherActivity,com.amazon.mShop.aiv.AIVGatewayStartupActivity,com.amazon.mShop.storefront.StorefrontActivity,com.amazon.mShop.android.home.PublicUrlActivity,com.amazon.mShop.home.HomeActivity,com.amazon.mShop.android.home.HomeActivity,org.npci.upi.security.pinactivitycomponent.GetCredential,aips.upiIssuance.mShop.android.interceptor.permissions.NpciGetCredentialInterceptor,org.npci.upi.security.pinactivitycomponent.GetCredential,com.amazon.mShop.alexa.audio.ux.PlaybackSheetActivity,com.amazon.mShop.alexa.AlexaActivity,com.amazon.mShop.alexa.onboarding.PermissionRequestActivity,com.amazon.android.oma.hub.NotificationHubActivity,com.amazon.traffic.automation.notification.util.PushNotificationContentActivity,com.amazon.mShop.push.registration.NotificationContentActivity,com.amazon.mShop.push.registration.WebNotificationsSettingsActivity,com.amazon.mShop.push.registration.educationalprompt.EducationalPromptPermissionHelper$PermissionRequestActivity,com.amazon.mShop.weblab.MShopChromeBetaTogglesActivity,com.amazon.mShop.permission.v2.storage.PermissionCheckerImpl$SystemPermissionRequestActivity,com.amazon.mShop.storemodes.StoreModesActivity,com.amazon.mobile.floatingnativeviews.smash.ext.pictureinpicture.PictureInPictureSupportedActivity,com.amazon.customwebview.CustomWebViewActivity,com.amazon.customwebview.EnableGPSActivity,com.amazon.mShop.amazonpay.SimpleRedirectActivity,com.amazon.mShop.amazonpay.AmazonPayHomeActivity,com.amazon.mShop.share.ingress.ShareActivity,com.amazon.mShop.share.ingress.ImageAndTextShareActivity,com.amazon.vsearch.galleryshare.StyleSnapGalleryShareActivity,com.amazon.vsearch.VSearchEntryActivity,com.amazon.mShop.kuber.rendering.activity.KuberRenderingActivity,com.amazon.mShop.httpUrlDeepLink.DeepLinkingActivity,com.amazon.mShop.httpUrlDeepLink.SecureDeepLinkingActivity,com.amazon.mShop.httpUrlDeepLink.DeepLinkingProxyActivity,com.amazon.mShop.httpUrlDeepLink.PublicUrlActivity,com.amazon.mShop.appgrade.ui.AppgradeMASHModalActivity,com.amazon.mShop.juspay.JuspayActivity,com.amazon.languageMenu.lopscreen.menu.fragment.LanguageMenuViewActivity,com.amazon.mShop.voice.assistant.debug.DebugActivity,com.amazon.mShop.voice.assistant.VoiceActivity,com.amazon.mShop.autorefresh.NotificationHandlerActivity,com.amazon.mShop.shortcut.ShortcutTrackingRedirectActivity,com.amazon.appunique.appwidget.DiscoverWidgetProxyNavActivity,com.amazon.mobile.smash.ext.diagnosticsplatform.device.mobile.assessment.assisted.TouchScreenAssessment,com.amazon.mShop.blankdetection.DebugBlankPageActivity,com.amazon.mShop.AmazonShareActivity,com.amazon.mShop.AmazonNativeShareActivity,com.amazon.mShop.share.copy.ShareToClipboardActivity,com.amazon.mShop.publicurl.PublicURLActivity,com.amazon.mShop.details.ProductDetailsActivity,com.amazon.mShop.startup.StartupLocalizationSelectionActivity,com.amazon.mShop.AmazonChooserActivity,com.amazon.mShop.mash.ui.MShopMashModalActivity,com.amazon.mShop.sso.DistributedSSOLoginActivity,com.amazon.mShop.sso.SSOBootstrapScreenActivity,com.amazon.mShop.sso.CentralSSOLoginActivity,com.amazon.mShop.sso.DistributedSSOLogoutActivity,com.amazon.mShop.sso.CentralSSOLogoutActivity,com.amazon.mShop.sso.SSOSplashScreenActivity,com.amazon.mShop.sso.SSOSplashScreenMigrationActivity,com.amazon.mShop.primeupsell.PrimeUpsellMashActivity,com.amazon.mShop.wolfgang.activity.FileWriteActivity,com.amazon.mShop.payment.googlebilling.sdk.GoogleBillingHeadlessActivity,com.amazon.mobile.mash.embeddedbrowser.EmbeddedBrowserActivity,com.alipay.sdk.app.AlipayResultActivity,com.amazon.identity.auth.device.AuthPortalUIActivity,com.amazon.identity.auth.device.activity.GetAuthenticatorResultsActivity,com.amazon.identity.auth.device.activity.AuthChallengeHandleActivity,com.amazon.identity.auth.device.activity.ActorSignUpAndEnrollActivity,com.amazon.identity.auth.device.activity.ActorEnrollActivity,com.amazon.identity.auth.device.activity.ActorUpdatePinPreferenceActivity,com.amazon.identity.auth.device.activity.ActorUpdatePhoneNumberActivity,com.amazon.identity.auth.device.activity.ActorUpdatePinActivity,com.amazon.identity.auth.device.authorization.AuthzDialogActivity,com.amazon.identity.auth.device.workflow.WorkflowDialogActivity,com.amazonaws.mobileconnectors.cognitoauth.activities.CustomTabsManagerActivity,com.google.ar.core.InstallActivity,androidx.credentials.playservices.HiddenActivity,androidx.test.core.app.InstrumentationActivityInvoker$BootstrapActivity,androidx.test.core.app.InstrumentationActivityInvoker$EmptyActivity,androidx.test.core.app.InstrumentationActivityInvoker$EmptyFloatingActivity,com.google.android.gms.auth.api.signin.internal.SignInHubActivity,com.google.android.gms.common.api.GoogleApiActivity,com.google.android.gms.ads.AdActivity,com.android.billingclient.api.ProxyBillingActivity,com.amazon.identity.mobi.authenticator.ui.TIVApprovalWebActivity,com.amazon.identity.mobi.browsersso.ui.ATBSSOUIActivity,org.npci.upi.security.pinactivitycomponent.UserAuthInfoActivity",
      "app_installed_date_formatted": "22-02-2023 | 11:53 am",
      "app_last_modified_date_formatted": "04-05-2024 | 02:05 am",
      "icon": {
        "mSrcDensityOverride": 0
      },
      "installedDate": 1677046992068,
      "label": "com.amazon.mShop.home.HomeActivity",
      "lastModified": 1714768546840,
      "launchActivity": "com.amazon.mShop.home.HomeActivity",
      "name": "Amazon",
      "packageName": "in.amazon.mShop.android.shopping",
      "providers": "com.reactnativecommunity.webview.RNCWebViewFileProvider,com.burnweb.rnsendintent.FileProvider,com.imagepicker.ImagePickerProvider,cl.json.RNShareFileProvider,com.amazon.mobile.koko.ShareAndroidFileProvider,com.a9.fez.share.ARFileProvider,androidx.startup.InitializationProvider,com.amazon.mShop.marketplace.provider.MarketplaceProvider,com.amazon.mShop.sso.MShopMAPInformationProvider,com.amazon.mShop.util.AssetContentProvider,com.amazon.mShop.util.AttachmentContentProvider,com.amazon.mShop.webview.util.ConfigurableFileProvider,com.amazon.mobile.mash.util.MASHFileProvider,com.google.firebase.provider.FirebaseInitProvider,com.amazon.mls.config.internal.sushi.background.ProcessLifecycleTrackerInitialization",
      "reqPermission": "INSTALL_SHORTCUT, VIBRATE, ACCESS_NETWORK_STATE, INTERNET, RECEIVE_SMS, READ_SMS, SEND_SMS, WAKE_LOCK, MODIFY_AUDIO_SETTINGS, CHECK_LICENSE, FOREGROUND_SERVICE, ACCESS_WIFI_STATE, RECEIVE, POST_NOTIFICATIONS, USE_FINGERPRINT, CAMERA, FLASHLIGHT, READ_BASIC_PHONE_STATE, HIGH_SAMPLING_RATE_SENSORS, CHANGE_WIFI_STATE, Permission, Permission, permission, CAN_CALL_MAP_INFORMATION_PROVIDER, USE_CREDENTIALS, MANAGE_ACCOUNTS, AUTHENTICATE_ACCOUNTS, AUTH_SDK, changed, changed, CALL_AMAZON_DEVICE_INFORMATION_PROVIDER, READ_PRELOAD_DEVICE_INFO_PROVIDER, RECEIVE_BOOT_COMPLETED, REORDER_TASKS, AD_ID, BIND_GET_INSTALL_REFERRER_SERVICE, BILLING",
      "services": "com.amazon.identity.auth.device.bootstrapSSO.BootstrapSSOService,com.amazon.whisperjoin.deviceprovisioningservice.service.whitelist.FFSWhiteListJobService,com.amazon.whisperjoin.deviceprovisioningservice.service.FFSBackgroundProvisioningServiceBinder,aips.upiIssuance.mShop.android.sdk.SDKService,org.npci.upi.security.pinactivitycomponent.CLRemoteServiceImpl,com.amazon.mShop.pushnotification.fcm.FCMMessagingService,com.amazon.mShop.pushnotification.PushReceivedOrchestrator$PushReceivedJobService,com.amazon.mShop.pushnotification.PushTokenRegistrationOrchestrator$PushTokenRegistrationJobService,com.amazon.mShop.goals.orchestrator.GoalsIntentService,com.amazon.mShop.goals.location.LocationUpdatesService,com.amazon.mShop.goals.orchestrator.GoalsJobService,com.amazon.traffic.automation.notification.geofence.NotificationGeofenceTransition,com.burnweb.rnsendintent.RNSendIntentModule,com.amazon.mShop.kuber.service.PrefetchService,com.amazon.appunique.appwidget.DiscoverWidgetCardsProvider,com.amazon.alexa.sdk.audio.channel.content.amp.service.AmpService,com.amazon.mShop.sso.SSOBackgroundAccountService,com.amazon.mShop.payment.googlebilling.sdk.GoogleBillingClientService,com.amazon.whisperjoin.deviceprovisioningservice.arcus.FFSArcusSyncJobService,com.amazon.identity.auth.device.storage.DirtyDataSyncingService,com.amazon.identity.auth.device.storage.DatabaseCleaner$DatabaseCleaningService,com.amazon.identity.auth.device.authorization.AmazonAuthorizationService1stParty,com.amazon.client.metrics.nexus.EventUploadService,com.amazon.client.metrics.nexus.UploadJobService,androidx.credentials.playservices.CredentialProviderMetadataHolder,androidx.work.impl.background.systemjob.SystemJobService,androidx.work.impl.foreground.SystemForegroundService,com.google.android.gms.auth.api.signin.RevocationBoundService,com.google.firebase.messaging.FirebaseMessagingService,com.google.firebase.components.ComponentDiscoveryService,androidx.room.MultiInstanceInvalidationService,com.google.android.datatransport.runtime.backends.TransportBackendDiscovery,com.google.android.datatransport.runtime.scheduling.jobscheduling.JobInfoSchedulerService,com.amazon.mls.config.internal.sushi.uploader.BackupUploaderService",
      "version": "28.9.0.300",
      "versionCode": "1241271011"
    }
  ],
  "batteryInfo": {
    "charging_source": "Source-AC",
    "charging_source_index": "AC",
    "temperature": "33.0",
    "health": "Battery health Good",
    "technology": "Li-ion",
    "charging_state": "Charging",
    "charged_percentage": "99",
    "is_battery_present": "true",
    "voltage": "4500"
  },
  "bluetoothInfo": {
    "has_bluetooth_le": "YES",
    "has_bluetooth_le_advertising": "YES"
  },
  "cpuInfo": {
    "CPU_revision": "1",
    "num_of_cores": "8",
    "CPU_architecture": "8",
    "supported_ABIS": "arm64-v8a_armeabi-v7a_armeabi",
    "processor": "7",
    "supported_32": "armeabi-v7a_armeabi",
    "BogoMIPS": "38.40",
    "supported_64": "arm64-v8a",
    "CPU_part": "0xd41",
    "Features": "fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp",
    "CPU_implementer": "0x41",
    "CPU_variant": "0x1",
    "supported_ABIS_details": "[arm64-v8a, armeabi-v7a, armeabi]"
  },
  "deviceConfigInfo": {
    "current_date": "05-05-2024 | 01:24 pm",
    "is_device_rooted": "false",
    "formatted_time": "1:24:19 pm",
    "is_running_on_emulator": "false",
    "formatted_up_time": "3:17:02 am",
    "is_developer_mode_enabled": "true",
    "sd_card_available": "YES",
    "formatted_date": "05-May-2024",
    "device_ringer_mode": "NORMAL",
    "is_wifi_adb_enabled": "false"
  },
  "deviceInfo": {
    "phone_no": "getLine1NumberForDisplay: Neither user 10687 nor current process has android.permission.READ_PHONE_STATE, android.permission.READ_SMS, or android.permission.READ_PHONE_NUMBERS",
    "device_unique_fingerprint": "motorola/dubai_g/dubai:13/T1RDS33.116-55-88-5/cf6dc6-fb8h3:user/release-keys",
    "android_base_os_version_name": "motorola/dubai_g/dubai:13/T1RD33.146-44-88/441420-2d5he8:user/release-keys",
    "device_model": "motorola_edge_30",
    "build_board": "dubai",
    "version_release": "13",
    "build_time": "20-03-2024 | 09:55 pm",
    "build_user": "hudsoncm",
    "language": "en",
    "device_type": "PHONE",
    "phone_type_mod": "GSM",
    "manufacturer": "motorola",
    "build_device": "dubai",
    "host": "iscublg239",
    "radio_version": "M7334_HI455_35.41.08.87R DUBAI_ROWDSDS_PVT_CUST",
    "hardware": "qcom",
    "product": "dubai_g",
    "phone_type": "GSM",
    "orientation": "PORTRAIT",
    "is_device_rooted": "false",
    "screen_display_id": "0",
    "version_incremental": "cx7dc6-fb4k3",
    "brand_name": "motorola",
    "build_version_sdk": "33",
    "serial": "getSerial: The uid 10687 does not meet the requirements to access device identifiers.",
    "build_id": "T1RDS37.116-66-18-8",
    "display_version": "T1RDS37.116-66-18-8",
    "android_os_version_name": "13",
    "android_os_name": "Android 13(Tiramisu)",
    "version_code_name": "REL",
    "device_unique_id": "346e22d171ff04be",
    "system_boot_loader_version": "MBM-3.0-dubai_g-1dr3ts7k46-240720",
    "build_tags": "release-keys"
  },
  "deviceMemoryInfo": {
    "total_internal_memory_size": "108.34862 Gb",
    "total_ram_memory_size": "7.209423 Gb",
    "available_internal_memory_size": "13.472279 Gb",
    "available_external_memory_size": "13.472279 Gb",
    "external_memory_available": "YES",
    "total_external_memory_size": "108.34862 Gb",
    "total_ram": "7.209423 Gb",
    "free_ram_memory_size": "2.9585266 Gb"
  },
  "deviceSimInfo": {
    "country": "in",
    "carrier": "jio_4g",
    "IMSI": "getSubscriberIdForSubscriber: The uid 10687 does not meet the requirements to access device identifiers.",
    "IMEI": "getImeiForSlot: The uid 10687 does not meet the requirements to access device identifiers.",
    "number_of_active_sim": "1",
    "sim_subscription": "[{\"carrier_name\":\"JIO 4G\",\"country_iso\":\"in\",\"display_name\":\"JIO Main\",\"icc_id\":\"\",\"mcc\":405,\"number\":\"\",\"sim_slot_index\":0,\"subscription_id\":4}]",
    "sim_network_locked": "NO",
    "sim_serial": "getIccSerialNumber: The uid 10687 does not meet the requirements to access device identifiers."
  },
  "displayInfo": {
    "orientation": "portrait",
    "density": "XMHDPI",
    "screen_round": "false",
    "layout_direction": "0",
    "refresh_rate": "90.0",
    "physical_size": "6.1825423",
    "resolution": "2235x1080"
  },
  "networkInfo": {
    "wifi_enabled": "YES",
    "cell_tower": "{\"signal_strength\":\"-98\",\"gsm_cell_identity\":\"1372177\",\"mobile_country_code\":\"405\",\"mobile_network_code\":\"872\",\"location_area_code\":\"unknown\"}",
    "mac_address": "",
    "bssid": "55:0c:88:00:4a:d9",
    "connection_status": "Connected",
    "ip_v4_address": "192.0.3.4",
    "ip_v6_address": "2409:4446:6567:6CBD:D:7666:FE57:F687",
    "data_type": "WiFi",
    "is_internet_connected": "true",
    "link_speed": "780 Mbps",
    "ssid": "\"AKR WiFi.5G\""
  },
  "featureInfo": {
    "multi_touch": "Supported",
    "is_nfc_enabled": "false",
    "connected_devices_list": "No device connected"
  },
  "sensorsInfo": [
    {
      "mFlags": 2432
    }
  ]
}
```


## ChangeLog

#### Version 1.01:
* Initial build
* compileSdkVersion 30, Java Version 1.8