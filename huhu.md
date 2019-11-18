安装
===
1. 安装uiautomator2  
```
pip install --upgrade uiautomator2  
pip install pillow
```
2. 部署守护进程  
```  
python -m uiautomator2 init  
```
3. 安装weditor UI查看器  
```
pip install -U weditor
python -m weditor 
备注：每次启动时运行python -m uiautomator2 init 和 python -m weditor就可以了
```

连接设备
===
1. 通过wifi连(要求设备IP和PC在同一网络中） 
```    
import uiautomator2 as u2  
d = u2.connect(‘设备ip’)  
print(d.info)  
```

2.通过usb连接  
```
import uiautomator2 as u2    
d = u2.connect(‘设备序列号’)    
print(d.info)   
```
启动应用程序
===
```
# 默认的这种方法是先通过atx-agent解析apk包的mainActivity，然后调用am start -n $package/$activity启动
d.app_start(packge_name)

# 使用 monkey -p com.example.hello_world -c android.intent.category.LAUNCHER 1 启动
# 这种方法有个附带的问题，它自动会将手机的旋转锁定给关掉
d.app_start("com.example.hello_world", use_monkey=True) # start with package name

# 通过指定main activity的方式启动应用，等价于调用am start -n com.example.hello_world/.MainActivity
d.app_start("com.example.hello_world", ".MainActivity")
```

停止应用程序
===
```
# 相当于 `am force-stop`, 可能会丢失数据
d.app_stop("com.example.hello_world") 
# 相当于 `pm clear`
d.app_clear('com.example.hello_world')
```
停止所有正在运行的应用
===
```
d.app_stop_all()

d.app_stop_all(excludes=['com.examples.demo'])
```

启动媒体中心、谷歌setting页面
===
1. 启动媒体中心  
```
{'package':'com.tcl.ui_mediaCenter','activity':'com.tcl.ui_mediaCenter.main.MainActivity'}
```
2.启动谷歌setting页面  
```
# 在主页下，获取driver要延时
dg = DemoGoogle()
time.sleep(5)
driver = dg.get_driver()
# 启动谷歌setting页面
dg.start_app(package_name="com.android.tv.settings",activity="com.android.tv.settings.MainSettings")
```
`注：package_name的获取方式为：在CMD输入：adb shell dumpsys activity | findstr  "realActivity"  或者 点开setting页面，运行代码driver.current_app()也可以获取到`


