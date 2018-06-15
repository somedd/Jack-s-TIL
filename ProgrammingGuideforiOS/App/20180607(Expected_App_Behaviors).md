# App Programming Guide for iOS
## 2018/06/07

## Expected App Behaviors

> This chapter describes the behaviors that all apps are expected to handle and that you should consider early in the planning process.


### Providing the Required Resources

> 앱에서 제공해야하는 리소스와 메타데이터에 대한 설명

- An information property-list file : Info.plist,  If you want to view or modify the contents of this file directly, you can do so from the Info tab of your project
- A declaration of the app’s required capabilities. : hardware capabilities or features that it requires to run. 이 정보를 기반으로 앱스토어는 특정 디바이스에서 앱이 구동 가능한지를 결정한다.
- One or more icons.
- One or more launch images.

### The App Bundle

- iOS앱을 빌드할 때 Xcode는 bundle을 생성.
	- 번들? A bundle is a directory in the file system taht groups executable code and related resources such as images and sounds together in one place.
- Table 1-1의 A typical app bundle 참고. (각 항목에 대해 자세한 링크가 걸려있음.)
	- App executable
	- Info.plist : he system uses this data to determine how to interact with the app.
	- App icons
	- Launch Images
	- Storyboard files (or nib files)
	- Ad hoc distribution icon (iTunesArtwork)
		- The filename of this icon must be iTunesArtwork and must not include a filename extension. This file is required for ad hoc distribution but is optional otherwise.
	- Settings bundle (This bundle contains the property list data and other resource files that define your app preferences.)
	- Nonlocalized resource files
	- Subdirectories for localized resources.

### The Information Property List File

> plist 주요 키와 상황에 대한 설명 및 링크

* Declare your app’s required capabilities in the Info tab. (특히 device level)

* Apps must provide purpose strings (sometimes called “usage descriptions”) for accessing user data and certain app features.


### Declaring the Required Device Capabilities

- UIRequiredDeviceCapabilities

### App Icons

### Supporting User Privacy

- Bestpriacties -> Review guidelines from government or industry sources, including the following documents
- iOS 시스템 권한 설정으로부터 보호받는 디바이스나 유저의 민감한 데이터에는 데이터가 필요한 시기에만 요청할 것. (must apply a purpose string in your app's Info.plist)
- Be transparent with users about how their data is going to be used.
- 사용자 또는 기기에 대한 통제권을 제공할 것.(사용자의 필요에 의해서 액세서 허용이 가능하지않도록)
- ASIdentifierManager class를 사용할 경우 advertisingTrackingEnabled property를 지킬것.
- UDID는 deprecated됏으므로 idnetifierForVendor propert나 advertisingIdentifier를 사용할 것.
- audio관련도 실제 사용하는 시기에만.
- Table 1-2 lists the types of resource and data authorizations supported by iOS.

### Internationalizing Your App
- When you factor your user-facing content into resource files, localizing that content is a relatively simple process.
- .lproj(language-specific project)
- A typical iOS app requires localized versions of the following types of resource files
	- Storyboard files (or nib files)
	- Strings files
	- Image files
	- Video and audio files
