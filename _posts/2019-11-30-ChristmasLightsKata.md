---
layout:     post
title:      Christmas Lights Kata练习
subtitle:   tdd练习
date:       2019-11-29
author:     冯
header-img: img/post-bg-2015.jpg
catalog: true
tags:
  - TDD
---

> 这是一个tdd练习题目，本文记录了本次kata的思考和练习过程。

# 描述

你的邻居每年都能在度假屋装饰大赛中打败你，你觉得很没面子。现在，你决定搞一个1000 x 1000的灯光网格（light grid)打败他。由于今年你表现的特别棒，圣诞老人给你发了关于如何配置灯光的说明。网格中的灯光在每个方向上的编号为0到999。每个角的坐标为(0,0),(0,999),(999,999)和(999,0)。说明中包括对给出的坐标对(coordinate pairs)范围内，进行打开(trun on)、关闭(turn off)和切换（toggle)的操作。每个坐标对表示了一个矩形的两个对角，像(0,0)到(2,2)这样的坐标对表示的是一个3x3的正方形中的9盏灯。所有的灯开始的时候是关闭的。为了将你的邻居按在地上摩擦，你需要做的就是按照圣诞老人给的说明来设置灯光。

* 对(0,0)到（999,999)做打开操作点亮所有的灯。
* 对(0,0)到（999,0)做切换操作将影响第一行的灯，关闭的灯打开 ，打开的灯关闭。
* 对(499,499)到(500,500)做关闭操作，关闭中间的4盏灯。

按照说明操作后，有多少灯是点亮的？

经过一阵忙活，你终于完成了。但是。。。你发现你貌似误解了圣诞老人的意思。你购买的灯光网格实际上有单独的亮度(brightness)控制。每盏灯都有0或更高的亮度值，亮度从0开始。

* 打开操作实际上是将亮度增加1
* 关闭操作实际上是将亮度减少1，最小值是0
* 切换操作实际上是将	亮度增加2

经过以上操作后灯光的总亮度是多少？

比如：

* 对(0,0)到(0,0)做打开操作后总亮度为1
* 对(0,0)到(999,999)做切换操作后总亮度为2000000

![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/default.jpg)

# 计划列表

动手之前需要列出完成这个灯光网格需要做哪些事，先列出要做的任务：

* 打开所有的灯
* 对第一行的灯做切换操作，效果是只点亮第一行的灯
* 对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯

# 开始写程序

## 第一个测试

没有测试代码之前不要写任何生产代码，所以第一个测试就是创建灯光网格（LightGrid)。

做法：创建LightGridTest,并写出创建LightGrid类的代码，这样就得到了第一个测试。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-142040@2x.png)
现在只要让这个测试通过就可以了，为了让测试通过，只需要创建一个LightGrid类就可以了。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-142222@2x.png)
然后我们就得到了LightGrid类。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-142248@2x.png)
现在第一个测试就完成了，运行测试，测试通过。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-142624@2x.png)

## 第二个测试

这个测试中我们要完成任务列表中的第一个任务，先看一下任务列表：

* 打开所有的灯
* 对第一行的灯做切换操作，效果是只点亮第一行的灯
* 对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯

现在开始做第一个任务，打开所有的灯。

根据上面的描述，写出这样一个测试：

![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-143012@2x.png)

现在主要任务是尽快让这个测试通过，先创建CoordinatePair类
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/carbon (1).png)

> 只写可以通过测试的代码，不要写额外的功能

为LightGrid创建trunOn方法

![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-144727@2x.png)

为LightGrid创建getLight方法
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-145411@2x.png)

现在，还需要再创建一个Light类，并且给Light类创建一个isOn方法
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-145145@2x.png)
目前可以通过编译了，运行测试
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-145540@2x.png)
测试失败了，因为Light.isOn()方法返回了false,为了让测试通过，只需要将isOn()方法改成ture即可
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-145701@2x.png)
运行测试，测试通过。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-145739@2x.png)
列表中的第一个任务完成了，现在可以将其划掉了

* ~~打开所有的灯~~
* 对第一行的灯做切换操作，效果是只点亮第一行的灯
* 对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯

## 第三个测试

对第一行的灯做切换操作，效果是只点亮第一行的灯

老规矩，先写测试。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-150806@2x.png)
为了让编译通过，需要给LightGrid创建toggle方法
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-150511@2x.png)
运行测试，失败了
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-150859@2x.png)
现在，想办法让这个测试通过。LightGrid现在为止只有一个骨架，还没有任何实质上的功能实现。先思考一下，LightGrid里面应该有很多Light,这些Light应该由一个二维数组表示。
进行到这里，我们需要对已经存在的代码进行重构，以方便添加新的功能。所以，我们先将第三个测试相关的代码注释掉，专注的进行重构。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-151657@2x.png)
LightGrid的toggle方法也注释掉。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-153921@2x.png)
运行测试，测试通过，我们没有破坏任何功能。Light类我们需要实现真实的行为。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-154424@2x.png)
运行测试，失败了。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-154837@2x.png)
失败的原因是，在LightGrid中，我们还没有对Light的trunOn方法进行调用，所以我们来搞定这件事。对turnOn方法的调用，我们需要接照给出的坐标对，对范围的所有Light进行trunOn操作就可以了。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-162852@2x.png)
因为实现这个方法，还驱动出了CoordinatePair的新方法。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/carbon (2).png)
LightGrid的getLight()也需要修改实现了
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-164338@2x.png)
运行测试，测试通过！
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-160005@2x.png)

现在重构完毕了，打开刚才注释掉的和toggle有关的代码，现在开始实现toggle。toggle和turnOn类似，只需要遍历坐标对范围内的Light进行toggle操作就可以了。LightGrid里我们只需复制turnOn的代码，然后修改一下就好了。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-163045@2x.png)
有人可能会对复制代码的行为嗤之以鼻，没关系，我们一会儿会重构它，现在先专注实现功能。给Light添加toggle方法。根据描述，toggle的意思是，打开的灯关闭，关闭的灯打开。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-160902@2x.png)
我们又驱动出了一个Light的turnOff方法 : )

完成了，运行测试，通过！
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-163226@2x.png)

列表中的第二个任务完成了。

* ~~打开所有的灯~~
* ~~对第一行的灯做切换操作，效果是只点亮第一行的灯~~
* 对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯

## 再次重构

现在完成了两个任务了，离目标只差一步了。目前的代码中已经出现了一些重复代码，所以现在我们暂时停下前进的脚步进行重构，重构完成后我们再继续。
观察一下LightGrid类。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/carbon (3).png)
trunOn和toggle里面有重复代码，我想我可以把遍历LightGrid中所有Light的方法抽出到一个eachLight方法中。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-164945@2x.png)
运行测试，不出所料，测试通过。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-165309@2x.png)
修改turnOn，测试。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-165354@2x.png)
修改toggle,测试。
最终效果：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/carbon (4).png)

测试代码也是代码，以后也需要修改和添加新测试。所以，再来看一下测试代码。

1. LigthGrid的创建，每个单元测试都需要创建，这里可以用JUnit的@setup方法，把LightGrid的创建集中在此。
2. should_create_light_grid()方法现在看起来有点多余了，删除之。
3. 有关遍历Light的方法可以用LightGrid.eachLight()替代。经过这样的修改后，LightGrid.getLight()方法不再被外部引用了，可以接访问级别改成private。

最终效果：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/carbon (5).png)

## 最后一个任务

对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯

先写测试：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-171840@2x.png)
这里就有个问题了，只验证中间的4盏灯是否能保证正确性？我感觉不能，如果保证正确，需要验证其它5个矩形区域的灯的关着的。如图：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/IMG_0440.JPG)
完善一下测试：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-181642@2x.png)
turnOff实现：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-181852@2x.png)

运行测试，测试通过！
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-181952@2x.png)
将最后一个任务划掉

* ~~打开所有的灯~~
* ~~对第一行的灯做切换操作，效果是只点亮第一行的灯~~
* ~~对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯~~


## 补充测试用例 
到这里，第一部分就完成了。但是描述中还有一个问题没有解决，就是“按照说明操作后，有多少灯是点亮的？”再添加一个任务。

* ~~打开所有的灯~~
* ~~对第一行的灯做切换操作，效果是只点亮第一行的灯~~
* ~~对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯~~
* 打开所有灯；对第一行做切换操作；关闭中间的4盏灯；应该点亮998996盏灯。

写测试：
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-183209@2x.png)
运行测试，测试通过。
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-183343@2x.png)

任务列表状态：

* ~~打开所有的灯~~
* ~~对第一行的灯做切换操作，效果是只点亮第一行的灯~~
* ~~对(499,499)到(500,500)做关闭操作，效果是关闭中间的4盏灯~~
* ~~打开所有灯；对第一行做切换操作；关闭中间的4盏灯；应该点亮998996盏灯~~

# 第二部分

根据描述，灯是有亮度的，而且之前所说的turnOn,turnOff,toggle等操作的含义也完全不一样了。经过分析只大部分的变化都在Light中，先改造Light类使之复合需求。

因为对灯的操作意义的变化，之前的should_998996_lights_on_after_instructions测试就不再有意义 了，所以将其删除。

之前是用一个布尔值来表示灯的开闭状态的，现在应该把内部状态改成一个亮度值。还需要添加一个获取亮度的方法，先列出任务：

* 改造Light类，内部状态改为用亮度(brightness)表示
* 对(0,0)到(0,0)做打开操作后总亮度为1
* 对(0,0)到(999,999)做切换操作后总亮度为2000000

先改造Light类

![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-190740@2x.png)

* ~~改造Light类，内部状态改为用亮度(brightness)表示~~
* 对(0,0)到(0,0)做打开操作后总亮度为1
* 对(0,0)到(999,999)做切换操作后总亮度为2000000

对任务二添加一个测试:
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-191151@2x.png)
给Light类添加brightness方法
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-185536@2x.png)
运行测试，通过！

* ~~改造Light类，内部状态改为用亮度(brightness)表示~~
* ~~~对(0,0)到(0,0)做打开操作后总亮度为1~~
* 对(0,0)到(999,999)做切换操作后总亮度为2000000

对任务三添加一个测试
![](https://ynfeng-blog.oss-cn-beijing.aliyuncs.com/WX20191201-191239@2x.png)

运行测试，通过！

* ~~改造Light类，内部状态改为用亮度(brightness)表示~~
* ~~~对(0,0)到(0,0)做打开操作后总亮度为1~~
* ~~对(0,0)到(999,999)做切换操作后总亮度为2000000~~

打完收工。PS：还没做参数的边界检查

