# Kaixin4IOS #
kaixin-ios-sdk-oauth1.0a是一个开源的objectC库，通过这个库，你可以登录到开心网，并调用开心网开放的rest API。


## 最新版本下载地址 ##
http://code.google.com/p/kaixin4ios/downloads/list
## API文档 ##

开发者可以参考开心网开放平台提供的api文档http://wiki.open.kaixin001.com/index.php?id=API%E6%96%87%E6%A1%A3
## 意见与反馈 ##

如果对sdk有更好的意见或是想法以及bug提交都可以反馈到这里
http://www.kaixin001.com/home/?uid=100038315
http://www.kaixin001.com/group/group.php?gid=1060588
## 简单的示例 ##
### oauth认证： ###
```
1.	首先, 在你的应用委托里面创建一个实例:
  if (!_engine){
		_engine = [[OAuthEngine alloc] initOAuthWithDelegate: self andScope: kOAuthScope];
		_engine.consumerKey = kOAuthConsumerKey;
		_engine.consumerSecret = kOAuthConsumerSecret;
     }
	 其中的kOAuthConsumerKey, kOAuthConsumerSecret是你在开心网开放平台里面注册应用时获取到的API Key和Secret Key。kOAuthScope是接口访问权限，只有包含所需要的权限，才能正常调用该API，否则就无法正常调用。
  
2.	UIViewController *controller = [OAuthController controllerToEnterCredentialsWithEngine: _engine delegate: self]; 如果返回值不为nil则需要用户登录授权，否则就是已经登录授权了
   
3.	通过[self presentModalViewController: controller animated: YES];用户可以进行登录论证授权. 

4.	另外你还应该在你的应用中实现的几个方法:
  
- (void) OAuthController: (OAuthController *) controller authenticatedWithUsername: (NSString *) username;用户授权成功
- (void) OAuthControllerFailed: (OAuthController *) controller;用户授权失败
- (void) OAuthControllerCanceled: (OAuthController *) controller;用户取消授权过程  
```

### 调用api： ###
```
1.	开心 API的调用需要首先完成上一步的用户登录授权，方可调用
2.	此SDK调用api的数据返回格式为JSON串
3.	调用开心API 
　比如调用个人信息接口的方法为：
首先生成一个client对象，并且传进去一个返回数据的回调函数
appDelegate.kaixinClient = [[kxClient alloc] initWithTarget:self engine:_engine action:@selector(timelineDidReceive:obj:)];
通过这个对象调用相应的方法。可以根据需要在kxClient这个类里面添加进去对需要的api的调用
       [appDelegate.kaixinClient getUserInfo];                       
  其它api调用与此类似，请参照各个api的具体参数，酌情在kxClient类里面加上相应的函数。    
```

### 取出当前用户的好友信息： ###
```
首先生成一个client对象，并且传进去一个返回数据的回调函数
appDelegate.kaixinClient = [[kxClient alloc] initWithTarget:self engine:_engine action:@selector(handleFriendInfoList:obj:)];
通过这个对象调用相应的方法。可以根据需要在kxClient这个类里面添加进去对需要的api的调用
       [appDelegate.kaixinClient getUserFriendList:0 num:20];                       
  其它api调用与此类似，请参照各个api的具体参数，酌情在kxClient类里面加上相应的函数。    
```

### 写记录： ###
```
首先生成一个client对象，并且传进去一个返回数据的回调函数
appDelegate.kaixinClient = [[kxClient alloc] initWithTarget:self engine:_engine action:@selector(handleRecord:obj:)];
通过这个对象调用相应的方法。可以根据需要在kxClient这个类里面添加进去对需要的api的调用
       [appDelegate.kaixinClient sendRecord:params];                       
  其它api调用与此类似，请参照各个api的具体参数，酌情在kxClient类里面加上相应的函数。    
```