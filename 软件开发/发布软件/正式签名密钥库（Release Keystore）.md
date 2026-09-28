
Android软件开发中来给发布正式版App签名的加密文件

## 签名（Signature）：
是用私钥对App安装包计算出来的一段加密信息，

## 文件形式：
通常是一个.jks或.keystore文件，配合一组别名和密码使用
	- 可以放在项目文件夹里也可以放在项目外面
	- 路径最好用英文

## 密钥的引路文件：
```
storePassword=你的密钥库密码
keyPassword=你的密钥密码
keyAlias=你的别名
storeFile=密钥文件的路径
```
## 在构建脚本中加入读取配置文件的代码：
- 在app/build.gradle或build.gradle.kts的android{}块前面加入读取配置文件的代码，并在signingConfigs中引用它

## applicationId：
应用ID，这是App在手机系统和应用商店里的唯一身份证号，通常域名(com)在前

## versionCode:
内部版本号，应用商店和系统靠它来判断新旧，必须为递增的整数

## versionName:
外部版本号，给用户看的

## minSdk:
App能运行的最低安卓版本

## targetSdk:
App专门适配的目标安卓版本

## release签名：
发布的正式签名，发布到应用商店必须使用正式签名（.jks)文件，而调试签名（debug）仅供本地测试。

## isMinifyEnabled
是否开启代码混淆与压缩，开启后，代码会被压缩，优化，类名和方法名会被替换成无意义的字母，这能大大减少安装包的体积，并增加他人反编译破解的难度

## Android Studio：
一个安装在电脑上的应用程序，能读取指定的文件，帮我写代码，打包成APK文件
在Android Studio里选择Build>Build Bundle(s)/APK(s)，生成的正式安装包就会自动用你的密钥签好名

- 应用商店通过它确认这个App是你发布的，丢失后无法找回，无法更新已上架的App

- 密钥：控制加密，解密，签名，验证等操作的秘密参数，分为对称密钥和非对称密钥
	- 对称密钥：加密和解密用同一把钥匙，比如AES加密，用密钥k加密也必须要密钥k解密
	- 非对称密钥（公钥+私钥）：签名用的就是这种，一次生成一个私钥和一个公钥
		- 公钥和私钥在数学上配对，但无法从公钥反推出私钥
		- 私钥用来“签”，公钥用来“验”

## 操作
在Android Studio里

### module：
这里显示的是项目里有一个叫app的1主模块，这里告诉打包工具需要打包的代码，和你最终的apk文件名字叫什么无关，保持默认选中即可

### key store path（密钥库路径）
这是生成的.jks文件的保存路径
1.点击creat new
2.在里面选择key store path的路径
3.填password和confirm，上面的是打开文件需要的密码（保险箱：里面包含了你的信息），下面的是key(构建工具会用key里的密码，路径等信息找到保险箱，并给App正式签名)
4.选择打包版本（Build Variants）：选择release，下面的Select App ID就会自动变成applicationID（域名在前那个），千万不要选调试版（debug）

### 用正式签名去打包
让AI改build.gradle等文件，让软件能用正式签名发布