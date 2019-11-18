#安装
1. 装uiautomator2  
`pip install --upgrade uiautomator2`  
`pip install pillow`  
2. 部署守护进程  
`python -m uiautomator2 init`
3. 装weditor UI查看器  
`pip install -U weditor`  
4. 运行python -m weditor  
备注：每次启动时运行python -m uiautomator2 init 和 python -m weditor就可以了
<br>
#连接设备
1. 通过wifi连  
要求设备IP和PC在同一网络中    
`import uiautomator2 as u2 `  
`d = u2.connect(‘设备ip’)  `  
`print(d.info)`   

2. 通过usb连  
`import uiautomator2 as u2`  
`d = u2.connect(‘设备序列号’)`  
`print(d.info)`  
