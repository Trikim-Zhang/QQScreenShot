运行Init.bat创建桌面快捷方式(或者主程序是Bin\QQScreenShot.exe, 自己手动运行)  
**!!!请以兼容性模式运行!!!(右键->属性->兼容性->以兼容模式运行这个程序)**  
单击托盘图标, 或默认使用快捷键Ctrl+Alt+A截图

注意:
1. 必须以兼容模式运行, 要不然QQ内部dll创建线程后WaitForSingleObject API会出错, 不知道为啥
2. 每次运行第一次录屏有时是无法用的, 只能录到鼠标, 但第二次及以后肯定就没问题了  

说明:
1. 滚轮音量功能开启后, 鼠标放到任务栏最下面可以通过滚动鼠标中键控制系统总音量大小 (win7/win10下测试可用)

2. 默认不再使用PaddleOCR, 如有需要, 请自行下载并解压,
下载链接:
链接：https://pan.baidu.com/s/1yENiFF3KDdZTDfqig6X98A 
提取码：oa7c  
下载ocr_system.zip后解压到 Bin\ocr_system 文件夹下, 然后 右键托盘图标 -> 切换OCR引擎 -> 选择PaddleOCR -> 确定 即可

3. 如果采用软件自身的贴图功能, 将不能编辑图片, 但可以缩放改变透明度等, 贴图的"鼠标穿透"功能开启后将不能取消, 开启"开启阴影"功能后图片将更清晰但透明度将失效

4. 若要使用网络OCR(OCRSpace、BaiduOCR)需要自行在Bin\config.ini中填写配置(OCRSpace只需填写OSApikey, 百度OCR需要填写BDApikey和BDSecretkey), OCRSpace不能识别中文, 且经常响应超时, 百度OCR挺好使的
(OCRSpace的apikey在[OCRSpaec Apikey](https://ocr.space/ocrapi/freekey)申请; 百度OCR使用的是 通用文字识别(标准版), 在[BaiduOCR Apikey](https://ai.baidu.com/tech/ocr)申请)

5. PaddleOCR启动参数在Bin\config.ini的StartCmd项,可自行修改, ppocr启动后会在后台常驻90s, 90s后自动退出(因为有内存泄露不能一直常驻),
   若win7下不能运行, 可下载win7\_ppocr\_env.7z并解压到ocr_system文件夹下即可

---------
更新事项(v3.0)  
1. 录屏功能逆出来了, 预览界面点右下角那个对勾后会保存到临时文件夹
2. 新增命令行参数oneshot, noplugin, noconfig 例如:  
QQScreenShot --oneshot=10, 执行一次截图并在10s后退出程序(截图Call是异步的,采用这种方式也是没办法的办法)   
QQScreenShot --noplugin(或-p), 不加载录屏插件  
QQScreenShot --noconfig(或-c), 不加载配置文件即使用默认配置
3. "切换热键"新增NULL选择, 即可以设置一个键的热键
4. 消息循环改用QQ的MessgeLoopForUI类
5. 托盘菜单新增"打开临时文件夹"选项, 有时OCR失败或者录屏导致没有删除的临时文件可手动删除  


---------

更新事项(v2.5):

1. "切换热键"功能新增F1-F9按键
2. 新增"接管贴图"功能, 开启后将使用软件自身的贴图程序替代QQ的"钉在桌面上"(软件自身的贴图程序可以缩放、改变透明度、取消/设置置顶等, 但不能编辑图片)
3. 新增网络OCR接口(OCRSpace、BaiduOCR)
4. PaddleOCR更新为v2.5, 预测库v2.3
5. 优化PaddleOCR执行(改为在后台等待消息)与获取结果逻辑

---------

更新事项(v2.4.1):

1.修复了获取PaddleOCR结果长度为0时构造字符串导致崩溃


----------

更新事项(v2.4):

1. 新增"切换OCR引擎"功能 (可以使用QQ自带的OCR识别啦!, 逆向的时候发现其实是可以本地调用QQ的OCR的)
2. "切换热键"功能改成了选择组合键的方式
3. 消息提醒不再使用托盘气泡, 全面改成用QQ的dll中的ShowResultTipsWin函数实现
4. PaddleOCR改成了线程中获取OCR结果, 不会再有卡顿了(PaddleOCR默认不再集成, 请查看第0x3节在网盘里自行下载并解压)

--------------

更新事项(v2.3):

1. 修复百度识图问题 (百度识图不再接受HTTP的POST请求, 修复为用libcurl发送HTTPS的POST请求)
2. 点击OCR按钮后不再需要手动关闭截图
3. 增加"切换热键"功能, 共Ctrl+Alt+A/Ctrl+Q/Ctrl+Shift+A三种热键
4. 增加"滚轮音量"功能, 可以通过在任务栏底部滑动鼠标滚轮来控制系统音量大小

--------------
