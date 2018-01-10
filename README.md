知乎连接：https://zhuanlan.zhihu.com/p/32754893

#Update

*  2018-01-10 : 一直读取图片的话会报异常，现在改为输入回车才回开始。更加稳定
             尝试了一下午汉王的OCR，识别率还是比较低啊。
             但是tessOCR运行时间确实有点长了。有好的OCR推荐下
*  2018-01-09 : 修改了启用多线程后带来的bug，新增gitee仓库地址(国内下载更快）

# MillionHero
今日头条的百万英雄答题助手

《百万英雄》是一档全民知识互动游戏，在《百万英雄》里每场12道题目全部回答正确的人，将瓜分奖金。
游戏模式
  
  一共12道题，全部答对就可以平分奖金

如果可以把直播中的问题和答案提取出来，然后百度，然后统计一下哪个更相关，就可以辅助你答题了。
当然也可以直接把百度出来题目和答案都展示出来。本文用的第一种简单粗暴。

#工具介绍
* JAVA8
* Android 手机
* Adb 驱动

#原理说明

1. 将手机点击到直播界面（在这里我们先打开一张图片）；
2. 用Adb 工具获取当前手机截图，并用adb将截图pull上来
   >     adb shell screencap -p /sdcard/1.png
   >     adb pull /sdcard/1.png .
3. 用tessOCR进行图像识别，提取文字；
4. 将文字中的问题和答案提取出来；
5. 使用百度搜索并统计搜索得到结果数量
   1. 问题+各个答案count(q&a)；
   2. 问题 count(q)；
   3. 答案 count(a)；
6. 计算匹配值pmi: pmi[i]=count(q&a[i])/(count(q)*count(a[i]))
7. 选择pmi值最高的为答案。

>#使用步骤
1. 安卓手机打开USB调试，设置》开发者选项》USB调试
2. 电脑与手机USB线连接，确保执行adb devices可以找到设备id
3. 打开百万直播
4. 运行我们的java程序，当弹出题目时，输入1回车

  
>PS:注意程序中的adb驱动目录要更换成自己的目录
  
  > 我的屏幕是1920*1080，如果是别的分辨率，暂时需要修改一下代码中的图片参数等。
    

>PPS:
  无奈本人在出差，笔记本速度和网速都比较慢，比较好的电脑和网速肯定能很大的提升。
  
#TODO
1. 可以增加一个图形化界面，分别对题目和答案进行搜索并进行展示。
