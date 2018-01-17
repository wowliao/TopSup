
# 答题辅助(Mac+iOS）
可用APP：冲顶大会、芝士超人、西瓜视频。
注：不同的APP需更改 common/ocr.py 中的分辨率。


**非常感谢关注，欢迎大家PR新的想法和优化。**

![](/resources/screenshot.png)


## 版本说明
- 谷歌 Tesseract


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
教程：https://github.com/wowliao/TopSup/wiki/WebDriveAgent%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B
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
注：若Mac中有Python2和Python3：`python3 GetQuestionTessIos.py`
会自动识别文字并打开浏览器

**注： 可以用 `GetImgTool.py` 调整题目截取位置**

若屏幕分辨率不同，请在 `ocr.py` 中自行修改代码即可
```
 # 切割题目和选项位置，左上角坐标和右下角坐标,自行测试分辨率
    #question_im = image.crop((45, 425, 1150, 780)) # iPhone 7P 冲顶大会
    question_im = image.crop((45, 240, 1200, 600)) # iPhone 7P 芝士超人，西瓜视频
    
    #choices_im = image.crop((45, 790, 1167, 1450)) # iPhone 7P 冲顶大会
    choices_im = image.crop((58, 580, 1216, 1280)) # iPhone 7P 芝士超人，西瓜视频

