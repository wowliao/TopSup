
# 答题辅助
这两天冲顶大会直播答题 APP 突然火了起来，萌生了使用截图，文字识别，搜索来做个小辅助的想法。使用文字识别搜索，只能增加准确率，保证不了全对。



**非常感谢关注，欢迎大家PR新的想法和优化。**

![](/resources/screenshot.png)

灵感来自：
> [微信跳一跳辅助 ](https://github.com/wangshub/wechat_jump_game)
>
> [程序员如何玩转《冲顶大会》？](https://livc.io/blog/204)


## 更新日志
- 2018.01.12
  - 修复 windows 命令行颜色乱码，处理一些识别错误
- 2018.01.11
  - 修复搜索可能的乱码等一些问题，多线程加快执行
- 2018.01.10
  - 增加循环，无需重复加载，优化逻辑和显示 来自 [issue #7](https://github.com/Skyexu/TopSup/issues/7)。增加部分手机截图设置
  - 增加了截图传输效率，修改了识别参数，对图像进行灰度转化，去干扰，增加了识别准确率。结果判断使用了三种方式，对不同问题可以参考不同结果。


## 版本说明
- 谷歌 Tesseract
  - [简单访问浏览器版本](/simpleVersion)
  - 最新版本：本目录
- [百度 OCR 版本](https://github.com/Skyexu/TopSup/tree/master/baiduApiVersion)：只实现了简单浏览器搜索，参考本目录代码可改



## 具体做法

1. 获取手机截屏

2. OCR 识别题目与选项文字   

  ![](/resources/cut.png)

  ​
  两个方法：

  - 谷歌 [Tesseract](https://github.com/madmaze/pytesseract) ，安装软件即可，接下来主要使用这个方法
  - [百度 OCR](https://cloud.baidu.com/product/ocr) ，[需要]()注册百度 API，每天调用次数有限

3. 搜索判断

## 结果判断方式

1. 直接打开浏览器搜索问题
  ![](./resources/result.png)
2. 题目+每个选项都通过搜索引擎搜索，从网页代码中提取搜索结果计数
3. 只用题目进行搜索，统计结果页面代码中包含选项的词频

以下为两个示例结果

![](./resources/result2.png)

![](./resources/result3.png)

参考了 [I Hacked HQ Trivia But Here’s How They Can Stop Me](https://hackernoon.com/i-hacked-hq-trivia-but-heres-how-they-can-stop-me-68750ed16365)

## 使用步骤 (谷歌 [Tesseract](https://github.com/madmaze/pytesseract)) 
### Mac+IOS

#### 1. 安装 WebDriverAgent
参考
  -  [iOS 真机如何安装 WebDriverAgent](https://testerhome.com/topics/7220) 
  -  [Android 和 iOS 操作步骤](https://github.com/wangshub/wechat_jump_game/wiki/Android-%E5%92%8C-iOS-%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4)
#### 2. 安装 python 3
#### 3. 安装所需 python 包
pip install pytesseract
pip install pillow  
pip install requests
pip install colorama
#### 4. 安装 python-wda
安装 [python-wda](https://github.com/openatx/facebook-wda)



#### 5. 安装 谷歌 Tesseract

https://github.com/tesseract-ocr/tesseract/wiki

#### 6. 修改  `common/ocr.py` 代码相应目录信息
```

# mac 环境 记得自己安装训练文件
# tesseract 路径
#pytesseract.pytesseract.tesseract_cmd = '/usr/local/Cellar/tesseract/3.05.01/bin/tesseract'
# 语言包目录和参数
#tessdata_dir_config = '--tessdata-dir "/usr/local/Cellar/tesseract/3.05.01/share/tessdata/" --psm 6'
```

#### 7. 运行脚本
`python GetQuestionTessIos.py`
会自动识别文字并打开浏览器

**注： 可以用 `GetImgTool.py` 调整题目截取位置**
可以到[这里](/config/devicesCutConfig.txt)查看部分手机截图设置
若屏幕分辨率不同，请在 `ocr.py` 中自行修改代码即可
```
# 切割题目和选项位置，左上角坐标和右下角坐标,自行测试分辨率
question_im = image.crop((50, 350, 1000, 560)) # 坚果 pro1
choices_im = image.crop((75, 535, 990, 1150))
# question = img.crop((75, 315, 1167, 789)) # iPhone 7P
```

