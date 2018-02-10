*有一个项目需求：可以画出四方形、圆形、三角形；用户选择相应的形状，顺时针旋转360度，然后根据不同的形状播放不同的aif文件*

---

1. 面向过程思维（阿朱）：考虑这个程序需要执行什么动作：旋转（rotate）,播放（playSound）
2. 面向对象思维（阿紫）：首先考虑这个需求中有什么对象，首先考虑有形状对象，还有用户，声响等对象，但是这些对象都已经建立完毕了

---
###### 面向过程高手
![image](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1518200068995&di=43046d287a84301ce725050a2f44d4b5&imgtype=0&src=http%3A%2F%2Fimg2.dwstatic.com%2Fwebgame%2F1312%2F251206632950%2F251206633194.jpg)
- 阿朱：
```
    rotate(shapeNum){
        //旋转360
    }
    playSound(shapeNum){
        //播放声音
    }
```
###### 面向对象高手
![image](http://05.imgmini.eastday.com/mobile/20160519/20160519172614_361953d7e0ff5d790d5d39e10d7eb48d_1.jpeg)
- 阿紫：

```
    square{
        rotate(){
            //code to rotate a square
        }    
        
        playSound(){
            //code to play the aif sound for square
        }
    }
```

```
    circle{
        rotate(){
            //code to rotate a circle
        }
        
        playSound(){
            //code to play the aif sound for circle
        }
    }
```

```
    Triangle{
        rotate(){
            //code to rotate a Triangle
        }
        
        playSound(){
            //code to play the aif sound for Triangle
        }
    }
```

---
*阿朱认为自己赢定了，但是甲方需求改了，现在加入阿米巴原虫形状，用户点选也是旋转播放.hif声音*


![image](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=9a6e04dd730e0cf3b4fa46a96b2f997a/9358d109b3de9c82db6450406d81800a18d843ff.jpg)
# 就是这个丑样子，哈哈哈
- 阿朱：

```
    //旋转形状还可以使用，可以通过一个码表查找特定编号的形状，但是播放.hif文件是什么鬼
    playSound(shapeNum){
        if(不是阿米巴原虫){
            播放指定格式的aif的文件
        }
        if(是阿米巴原虫){
            播放hif格式的文件
        }
    }
```
- 阿紫

```
    //阿紫只好苦笑一声
    amoeba{
        rotate(){
            //旋转
        }
        playSound(){
            //播放指定格式的声音
        }
    }
```

---
*不好意思，甲方爸爸的需求又改了，阿米巴原虫的旋转不是按照中心点的形式旋转的，阿朱和阿紫都搞错了，而是以一个轴进行旋转*
![image](http://img1.3lian.com/2015/w4/37/d/126.jpg)
###### 就是这酱紫，有点扭曲
- 阿朱

```
    //现在旋转的方法也需要改了
    rotate(shapeNum,xpt,ypt){
        if(!阿米巴原虫){
            //计算中心点
            //按照中心点进行旋转
            }
        else{
            //以xpt,ypt旋转
            //旋转
        }
        
    }
```
- 阿紫

```
    // 只需要修改阿米巴原虫部分旋转的方法，其余编译完成的代码不需要修改
    amoeba{
        int xPoint;
        int yPoint;
        rotate(){
            //使用阿米巴原虫的x,y进行选抓
        }
        
        playSound(){
            //code不需要修改
        }
    }
```

---
阿紫赢了，求豆妈哋  
阿朱发现你有太多重复的代码了，4个shape中都有rotate方法
# 最终设计
![image](https://thumbnail0.baidupcs.com/thumbnail/0fec3dc29cea930d909918b5241e18e8?fid=4128578276-250528-1104213305959447&time=1518228000&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-xXS9azQPPM78ivu1mL6KbkQBLq8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=938092231216212746&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)  
**阿朱有问题：那阿米巴原虫的rotate，playSound怎么办呢?**  
![image](https://thumbnail0.baidupcs.com/thumbnail/c582b94adc7ef8f912ad4227fa14b9ea?fid=4128578276-250528-379221541768829&time=1518228000&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-jLgTHlcZQfFGV2OLda1ZQJQbKs8%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=938211645375851623&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video)  
###### 可以看出来，阿米巴原虫覆盖了父类方法，jvm虚拟机遇到amoeba使用不同的rotate，playSound方法
---
覆盖：子类重新定义方法的含义，以改变方法的含义或者延伸

面向对象核心就是：每个人管好自己的事情，别人要让你干啥，你自己知道就行

---
## 对象和类的区别
类就是对象的蓝图，jvm虚拟机可以根据类生成对象的实例， 类似通讯簿中的每一个记录页，你可以往里面数据填写数据‘

---
## 全局变量
public static final x  
x变量基本就可以视为全局变量了
## 大量的类怎样运行呢？
需要一个manifest，类似一个文本，里面记录了哪个类有这个main方法
