## Fastlane--Packaging
* 自动化打包，通过fastlane自动发布

## 安装不在这里详细罗列，参照一下链接流程
*  https://www.jianshu.com/p/0a113f754c09



## 操作步骤


### 1.检查Fastlane是否正确安装。输入以下命令：

```objc
fastlane --version
```
      //可以看到Fastlane版本信息，我的是fastlane 2.84.0
      
### 2.打开终端，进入你的项目工程的根目录，输入以下命令

      cd到你项目的目录,执行命令
      
```objc       
fastlane init
```
* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_01.png)

* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_02.png)

*  bundl update ---这一步可能时间较长
* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_03.png)

* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_04.png)

* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_05.png)

* ![(icon)](https://github.com/daniulaolu/Fastlane--Packaging/blob/master/fastlane%20init_resource/fastlane%20init_06.png)

### 3.编辑.podspec
      
      按照上面的样式来编辑
      
```objc       
s.name：名称，pod search搜索的关键词,注意这里一定要和.podspec的名称一样,否则报错
s.version：版本号，to_s：返回一个字符串
s.author:作者
s.homepage:项目主页地址
s.summary: 项目简介
s.source:项目源码所在地址
s.license:许可证
s.platform:项目支持平台
s.requires_arc: 是否支持ARC
s.source_files:需要包含的源文件
s.public_header_files:需要包含的头文件
s.ios.deployment_target:支持的pod最低版本
其他一些非必要字段

s.social_media_url:社交网址
s.resources:资源文件
s.dependency:依赖库，不能依赖未发布的库
s.license= { :type => “MIT”, :file => “LICENSE” }
这里建议这样写,如果写别的会报警告,导致后面一直提交失败
```

### 4.验证.podspec

      到此检查一下你工程中有以下文件：
      
      .podspec文件,
  
      LICENSE文件

```objc
pod spec lint lujhPrivate.podspec --verbose
```

### 5.trunk需要CocoaPods 

```objc 
pod trunk me
```
      若未注册，执行以下命令，邮箱以及用户名请对号入座。用户名我使用的是Github上的用户名。
 
```objc
 // 加上--verbose可以输出详细错误信息，方便出错时查看。
      
pod trunk register example@example.com 'lujhPrivate'  --verbose
```

      注册完成之后会给你的邮箱发个邮件,进入邮箱邮件里面有个链接,需要点击确认一下。
      
      注册完成后使用pod trunk me检验注册是否成功
      
 ### 6.将自己的项目打成tag
   
      因为cocoapods是依赖tag版本的,所以必须打tag,以后再次更新只需要把你的项目打一个tag，然后修改.podspec文件中的版本接着提交到cocoapods官方就可以了,提交命令请看下面
    
      在终端执行以下命令：为git打tag, 第一次需要在前面加一个v
      
```objc 
git tag "v1.0.0" 
      
git push --tags
```
### 7.发布

```objc 
pod trunk push lujh.podspec
```
      时间较长，耐性等待，大概5-10分钟
      
###8.测试自己的cocoapods

     这个时候使用pod search搜索的话会提示搜索不到，可以执行以下命令更新本地search_index.json文件
  
```objc 
rm ~/Library/Caches/CocoaPods/search_index.json
```
     然后
     
```objc 
pod search lujhPrivate
```

## 完整命令

```objc 
pod trunk register example@example.com 'lujhPrivate'  --verbose
pod trunk me
pod spec create lujhPrivate
 
//编辑 lujhPrivate.podspec
 
pod spec lint lujhPrivate.podspec
git tag "v1.0.0"
git push --tags
pod trunk push lujhPrivate.podspec 
rm ~/Library/Caches/CocoaPods/search_index.json
pod search lujhPrivate
```

## My weixin
![(author)](https://github.com/daniulaolu/PushParameterWithDict-/blob/master/xiaolu.jpg)
