### iOS 9 的适配
- 1 `iOS 9 网络请求 默认 必须 使用 HTTPS 协议`

		有几种 解决办法:
		
		1. 服务端 升级使用TLS 1.2 (TLS 是 SSL 新版本 的别称, TLS 1.0 ＝ SSL 3.1)
	
		2. 在 Info.plist 中 声明, 依然使用 HTTP.

	![依然使用HTTP](https://github.com/someValue/Note/blob/master/iOS/src/依然使用HTTP.png)
	
		3. 还可以 针对 特定的 URL 不使用 ATS.	
	[搜索ATS](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40016240)
	
- 2 `定位`

		导入 CoreLocation.framework
		
		#import <CoreLocation/CoreLocation.h>

		@interface ViewController () <CLLocationManagerDelegate>

		@property (strong, nonatomic) CLLocationManager *mng;
		
	---
	
		self.mng = [[CLLocationManager alloc] init];
		
	    self.mng.delegate = self;
	    
	    [self.mng startUpdatingLocation];	
	    
	---
	
		-(void)locationManager:(CLLocationManager *)manager didUpdateLocations:(NSArray<CLLocation *> *)locations
		{
		    //...
		}
	    
	 2.1 `前台定位`
		
		[self.mng requestWhenInUseAuthorization];
		
		在 Info.plist 中 添加一个 key: NSLocationWhenInUseUsageDescription
	 2.2 `前台 + 后台 定位`
		
		[self.mng requestAlwaysAuthorization];
		
		在 Info.plist 中 添加一个 key: NSLocationAlwaysUsageDescription
				
- 3 `使用URL Scheme 需要在 Info.plist 中 将它们列为白名单`

		<key>LSApplicationQueriesSchemes</key>
	    <array>
	        <string>wechat</string>
	        <string>mqq</string>
	        <string>alipay</string>
	        <string>sinaweibo</string>
	    </array>	
	---
	
		NSURL *url = [NSURL URLWithString:@"wechat://"];

        // 如果已经安装了这个应用,就跳转
        if ([[UIApplication sharedApplication] canOpenURL:url]) 
        {
            [[UIApplication sharedApplication] openURL:url];
        }
