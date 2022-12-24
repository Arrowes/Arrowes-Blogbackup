---
title: Embedded：嵌入式应用知识
date: 2022-12-11 20:54:34
tags:
- 嵌入式
---
# 相关常识
## 电容
电容是电路设计中最为普通常用的器件，是无源元件之一，有源器件简单地说就是需能(电)源的器件叫有源器件，无需能(电)源的器件就是无源器件。
电容的作用和用途一般都有好多种，如：在旁路、去耦、滤波、储能方面的作用；在完成振荡、同步以及时间常数的作用：
**隔直流**：作用是阻止直流通过而让交流通过。![图 23](/images/685acd9502b523b1ad4c60f8841f253820460a46961942d9d064915d5d9c2569.png)  
**旁路（去耦）**：为交流电路中某些并联的元件提供低阻抗通路。![图 24](/images/e1ca270364f9eecc8b62658996dfed21c018ee3691ea2d1c9c74e9de6654be0b.png)  
**旁路电容**：旁路电容，又称为退耦电容，是为某个器件提供能量的储能器件。
它利用了电容的频率阻抗特性，理想电容的频率特性随频率的升高，阻抗降低，就像一个水塘，它能使输出电压输出均匀，降低负载电压波动。
旁路电容要尽量靠近负载器件的供电电源管脚和地管脚，这是阻抗要求。
在画PCB时候特别要注意，只有靠近某个元器件时候才能抑制电压或其他输信号因过大而导致的地电位抬高和噪声。
说白了就是把直流电源中的交流分量，通过电容耦合到电源地中，起到了净化直流电源的作用。如图为旁路电容，画图时候要尽量靠近IC1。![图 25](/images/0a4bc3d9c1194a0f7fcdd755bd79b48782488782e111218f3c9785b1e2e83c8f.png)  
**去耦电容**：去耦电容，是把输出信号的干扰作为滤除对象，去耦电容相当于电池，利用其充放电，使得放大后的信号不会因电流的突变而受干扰。
它的容量根据信号的频率、抑制波纹程度而定，去耦电容就是起到一个“电池”的作用，满足驱动电路电流的变化，避免相互间的耦合干扰。
**旁路电容实际也是去耦合的**，只是旁路电容一般是指高频旁路，也就是给高频的开关噪声提高一条低阻抗泄防途径。
高频旁路电容一般比较小，根据谐振频率一般取 0.1μF、0.01μF 等。
而去耦合电容的容量一般较大，可能是 10μF 或者更大，依据电路中分布参数、以及驱动电流的变化大小来确定。上图C3为去耦电容
**区别**：旁路是把输入信号中的干扰作为滤除对象，而去耦是把输出信号的干扰作为滤除对象，防止干扰信号返回电源。
**耦合**：作为两个电路之间的连接，允许交流信号通过并传输到下一级电路 。
![图 26](/images/46e04bdeeed43d3b70755a04ec96b2085cac0b8af0b4f045a4713c509f160368.png)  
用电容做耦合的元件，是为了将前级信号传递到后一级，并且隔断前一级的直流对后一级的影响，使电路调试简单，性能稳定。
如果不加电容交流信号放大不会改变，只是各级工作点需重新设计，由于前后级影响，调试工作点非常困难，在多级时几乎无法实现。
**滤波**：这个对电路而言很重要，CPU背后的电容基本都是这个作用。
即频率f越大，电容的阻抗Z越小。当低频时，电容C由于阻抗Z比较大，有用信号可以顺利通过；当高频时，电容C由于阻抗Z已经很小了，相当于把高频噪声短路到GND上去了。
![图 27](/images/95b5c2765b6a8ea02741e983fb78885d2c85478ae1c116b2f032f66689ba0a31.png) ![图 28](/images/3a7874de3aaa4d76c2582df477563a03a08b2277fb02137421c47ff7e808a852.png)  
**滤波作用**：理想电容，电容越大，阻抗越小，通过的频率也越高。
电解电容一般都是超过 1uF ，其中的电感成份很大，因此频率高后反而阻抗会大。
我们经常看见有时会看到有一个电容量较大电解电容并联了一个小电容，其实大的电容通低频，小电容通高频，这样才能充分滤除高低频。
电容频率越高时候则衰减越大，电容像一个水塘，几滴水不足以引起它的很大变化，也就是说电压波动不是你很大时候电压可以缓冲，如图C2：![图 29](/images/158c15af5eace10b04f9f4e8c1cd2d74cd2e481f0edbbff2e54ce793df684ade.png)  
**温度补偿**：针对其它元件对温度的适应性不够带来的影响，而进行补偿，改善电路的稳定性。![图 30](/images/4b7c34fcaf3df2820be7fbf0f6d5b97a67344c7ae9b2b2b3aeed01d0b8b8f8fa.png)  
**分析**：由于定时电容的容量决定了行振荡器的振荡频率，所以要求定时电容的容量非常稳定，不随环境湿度变化而变化，这样才能使行振荡器的振荡频率稳定。
因此采用正、负温度系数的电容释联，进行温度互补。
当工作温度升高时，Cl的容量在增大，而C2的容量在减小，两只电容并联后的总容量为两只电容容量之和，由于一个容量在增大而另一个在减小，所以总容量基本不变。
同理，在温度降低时，一个电容的容量在减小而另一个在增大，总的容量基本不变，稳定了振荡频率，实现温度补偿目的。
**计时**：电容器与电阻器配合使用，确定电路的时间常数。![图 31](/images/6ddf1893b1eb05c8e81791fd84087c60eab61bdc31d02454fa15e77e315f18f3.png)  
输入信号由低向高跳变时，经过缓冲1后输入RC电路。
电容充电的特性使B点的信号并不会跟随输入信号立即跳变，而是有一个逐渐变大的过程。
当变大到一定程度时，缓冲2翻转，在输出端得到了一个延迟的由低向高的跳变。
**时间常数**：以常见的 RC 串联构成积分电路为例，当输入信号电压加在输入端时，电容上的电压逐渐上升。
而其充电电流则随着电压的上升而减小，电阻R和电容C串联接入输入信号VI，由电容C输出信号V0，当RC (τ)数值与输入方波宽度tW之间满足：τ》》tW，这种电路称为积分电路。
**调谐**：对与频率相关的电路进行系统调谐，比如手机、收音机、电视机。![图 32](/images/9583af04fd08345d4a2cd72350e921cfc725d277f6520357dec844e6cbf8968a.png)  
因为lc调谐的振荡电路的谐振频率是lc的函数，我们发现振荡电路的最大与最小谐振频率之比随着电容比的平方根变化。
此处电容比是指反偏电压最小时的电容与反偏电压最大时的电容之比。
因而，电路的调谐特征曲线（偏压一谐振频率）基本上是一条抛物线。
**整流**：在预定的时间开或者关半闭导体开关元件。![图 33](/images/2a2a2af5cce9cbe1cf3e6dd6aab20aa5a38092ebb92af8c4885675a3f57d4b56.png)  
**储能**：储存电能，用于必须要的时候释放。
例如相机闪光灯，加热设备等等．（如今某些电容的储能水平己经接近锂电池的水准，一个电容储存的电能可以供一个手机使用一天。
一般地，电解电容都会有储能的作用，对于专门的储能作用的电容，电容储能的机理为双电层电容以及法拉第电容。
其主要形式为超级电容储能，其中超级电容器是利用双电层原理的电容器。
当外加电压加到超级电容器的两个极板上时，与普通电容器一样，极板的正电极存储正电荷，负极板存储负电荷。
在超级电容器的两极板上电荷产生的电场作用下，在电解液与电极间的界面上形成相反的电荷，以平衡电解液的内电场。
这种正电荷与负电荷在两个不同相之间的接触面上，以正负电荷之间极短间隙排列在相反的位置上，这个电荷分布层叫做双电层，因此电容量非常大。


# PCB布局布线
## 布局
元器件布局的10条规则：

1. 遵照**先大后小，先难后易**的布置原则，即重要的单元电路、核心元器件应当优先布局。
2. 布局中应参考原理框图，根据单板的主信号流向规律安排主要元器件。
3. 元器件的排列要便于调试和维修，亦即小元件周围不能放置大元件、需调试的元器件周围要有足够的空间。 
4. 相同结构电路部分，尽可能采用“对称式”标准布局。
5. 按照均匀分布、重心平衡、版面美观的标准优化布局。 
6. 同类型插装元器件在X或Y方向上应朝一个方向放置。同一种类型的有极性分立元件也要力争在X或Y方向上保持一致，便于生产和检验。 
7. 发热元件一般应均匀分布，以利于单板和整机的散热，除温度检测元件以外的温度敏感器件应远离发热量大的元器件。 
8. 布局应尽量满足以下要求：总的连线尽可能短，关键信号线最短；高电压、大电流信号与小电流，低电压的弱信号完全分开；模拟信号与数字信号分开；高频信号与低频信号分开；高频元器件的间隔要充分。
9. 去耦电容的布局要尽量靠近IC的电源管脚，并使之与电源和地之间形成的回路最短。 
10. 元件布局时，应适当考虑使用同一种电源的器件尽量放在一起, 以便于将来的电源分隔。 
## 布线
### （1）布线优先次序
关键信号线优先：模拟小信号、高速信号、时钟信号和同步信号等关键信号优先布线 
密度优先原则：从单板上连接关系最复杂的器件优先布线。从单板上连线 最密集的区域开始布线 
注意点：
> a. 尽量为时钟信号、高频信号、敏感信号等关键信号提供专门的布线层，并保证其最小的回路面积。必要时应采取手工优先布线、屏蔽和加大安全间距等方法。保证信号质量。 
b. 电源层和地层之间的EMC环境较差，应避免布置对干扰敏感的信号。
c. 有阻抗控制要求的网络应尽量按线长线宽要求布线。 

### （2）四种具体走线方式
#### 1. 时钟的布线：
时钟线是对EMC 影响最大的因素之一。在时钟线上应少打过孔，尽量避免和其它信号线并行走线，且应远离一般信号线，避免对信号线的干扰。同时应避开板上的电源部分，以防止电源和时钟互相干扰。
如果板上有专门的时钟发生芯片，其下方不可走线，应在其下方铺铜，必要时还可以对其专门割地。对于很多芯片都有参考的晶体振荡器，这些晶振下方也不应走线，要铺铜隔离。![图 1](/images/9a446328891042cdc8948f359a5c372759df00f0084dbbbed565452c34a1446d.png)  
#### 2. 直角走线:
直角走线一般是PCB布线中要求尽量避免的情况，也几乎成为衡量布线好坏的标准之一，那么直角走线究竟会对信号传输产生多大的影响呢？从原理上说，直角走线会使传输线的线宽发生变化，造成阻抗的不连续。其实不光是直角走线，顿角，锐角走线都可能会造成阻抗变化的情况。

直角走线的对信号的影响就是主要体现在三个方面：
> 一是拐角可以等效为传输线上的容性负载，减缓上升时间；
二是阻抗不连续会造成信号的反射；
三是直角尖端产生的EMI。

#### 3. 差分走线:

参看：Altium Designer -- 差分布线和阻抗匹配

**差分信号**（Differential Signal）在高速电路设计中的应用越来越广泛，电路中最关键的信号往往都要采用差分结构设计.定义:通俗地说，就是驱动端发送两个等值、反相的信号，接收端通过比较这两个电压的差值来判断逻辑状态“0”还是“1”。而承载差分信号的那一对走线就称为差分走线。
差分信号和普通的单端信号走线相比，最明显的优势体现在以下三个方面：
```
a.抗干扰能力强，因为两根差分走线之间的耦合很好，当外界存在噪声干扰时，几乎是同时被耦合到两条线上，而接收端关心的只是两信号的差值，所以外界的共模噪声可以被完全抵消。
b.能有效抑制EMI，同样的道理，由于两根信号的极性相反，他们对外辐射的电磁场可以相互抵消，耦合的越紧密，泄放到外界的电磁能量越少。
c.时序定位精确，由于差分信号的开关变化是位于两个信号的交点，而不像普通单端信号依靠高低两个阈值电压判断，因而受工艺，温度的影响小，能降低时序上的误差，同时也更适合于低幅度信号的电路。目前流行的LVDS（low voltage differential signaling）就是指这种小振幅差分信号技术。
```
对于PCB工程师来说，最关注的还是如何确保在实际走线中能完全发挥差分走线的这些优势。也许只要是接触过Layout的人都会了解差分走线的一般要求，那就是“等长、等距”。

等长是为了保证两个差分信号时刻保持相反极性，减少共模分量；等距则主要是为了保证两者差分阻抗一致，减少反射。“尽量靠近原则”有时候也是差分走线的要求之一。

#### 4. 蛇形线:
蛇形线是Layout中经常使用的一类走线方式。其主要目的就是为了调节延时，满足系统时序设计要求。
设计者首先要有这样的认识：
蛇形线会破坏信号质量，改变传输延时，布线时要尽量避免使用。但实际设计中，为了保证信号有足够的保持时间，或者减小同组信号之间的时间偏移，往往不得不故意进行绕线。
注意点:
成对出现的差分信号线，一般平行走线，尽量少打过孔，必须打孔时，应两线一同打孔，以做到阻抗匹配。
相同属性的一组总线，应尽量并排走线，做到尽量等长。从贴片焊盘引出的过孔尽量离焊盘远些。![图 2](/images/d2a5e8b322378f0374c95c329d613c1e28cd2256530fe7445220b76f1cdf304b.png)  

### （3）布线常用规则
1. 走线的方向控制规则： 
即相邻层的走线方向成正交结构。避免将不同的信号线在相邻层走成同一方向，以减少不必要的层间串扰；
当由于板结构限制（如某些背板）难以避免出现该情况，特别是信号速率较高时，应考虑用地平面隔离各布线层，用地信号线隔离各信号线。 ![图 3](/images/d4a7cd6dc62aa281ceb9a31a2dc787d4ff4c154e6bf2ac34703d36351b596fb8.png)  
2. 走线的开环检查规则：
一般不允许出现一端浮空的布线（Dangling Line), 主要是为了避免产生"天线效应"，减少不必要的干扰辐射和接受，否则可能带来不可预知的结果。 ![图 4](/images/cedb027afef39327b7211c6ea8ab22995e9ec6d1ab3dc05061f2a9d2eee7dfbc.png)  
3. 阻抗匹配检查规则： 
同一网络的布线宽度应保持一致，线宽的变化会造成线路特性阻抗的不均匀，当传输的速度较高时会产生反射，在设计中应该尽量避免这种情况。
在某些条件下，如接插件引出线，BGA封装的引出线类似的结构时，可能无法避免线宽的变化，应该尽量减少中间不一致部分的有效长度。![图 5](/images/e98b495e0928bb84cef6a67e6b3ba86d23338d81e2ebd6747cc4c84f8936a6ea.png)  
4. 走线长度控制规则： 
即短线规则，在设计时应该尽量让布线长度尽量短，以减少由于走线过长带来的干扰问题，特别是一些重要信号线，如时钟线，务必将其振荡器放在离器件很近的地方。对驱动多个器件的情况，应根据具体情况决定采用何种网络拓扑结构。 ![图 6](/images/2f2712b920b2ef1a17051164bfb460657f58bd9f28ffb7bc9dc8e640974b7913.png)  
5. 倒角规则： 
PCB设计中应避免产生锐角和直角， 产生不必要的辐射，同时工艺性能也不好。![图 7](/images/30af6bcd52ad1edc186f75f548bbd01a49386e05b2d492595a9d42a853bab626.png)  
6. 器件去耦规则： 
A. 在印制版上增加必要的去耦电容，滤除电源上的干扰信号，使电源信号稳定。
在多层板中，对去耦电容的位置一般要求不太高，但对双层板，去耦电容的布局及电源的布线方式将直接影响到整个系统的稳定性，有时甚至关系到设计的成败。 
B. 在双层板设计中，一般应该使电流先经过滤波电容滤波再供器件使用。 
C. 在高速电路设计中，能否正确地使用去耦电容，关系到整个板的稳定性。 ![图 8](/images/a9f69b0bc3976fcb6441829e554398bcb792a5e7348c597dd3d7f3e0e7c54e8f.png)  
7. 器件布局分区/分层规则： 
A. 主要是为了防止不同工作频率的模块之间的互相干扰，同时尽量缩短高频部分的布线长度。
B. 对混合电路，也有将模拟与数字电路分别布置在印制板的两面，分别使用不同的层布线，中间用地层隔离的方式。 ![图 9](/images/de907aaee955c5d88bd046037daeab30d9882e0be37f2af8a342d2b5c7f1239a.png)  
8. 地线回路规则：
环路最小规则，即信号线与其回路构成的环面积要尽可能小，环面积越小，对外的辐射越少，接收外界的干扰也越小。 ![图 10](/images/1c58802203d0ceb52af81f957068154b7c409eb701a4b86beb4a8c73797bdbad.png)  
9. 电源与地线层的完整性规则： 
对于导通孔密集的区域，要注意避免孔在电源和地层的挖空区域相互连接，形成对平面层的分割，从而破坏平面层的完整性，并进而导致信号线在地层的回路面积增大。![图 11](/images/7956cb4e6d91da3956e52eca5a3d7e963363bfa905f3c6fb968eec9b13d41cc0.png)  
10. 3W规则：
为了减少线间串扰，应保证线间距足够大，当线中心间距不少于3倍线宽时，则可保持70%的电场不互相干扰，称为3W规则。如要达到98%的电场不互相干扰，可使用10W的间距。![图 12](/images/a5190860105961677ec97dfee5f305a1081424fce353c1d93c5f280edf7d955d.png)  
11. 屏蔽保护：
对应地线回路规则，实际上也是为了尽量减小信号的回路面积，多见于一些比较重要的信号，如时钟信号，同步信号；
对一些特别重要，频率特别高的信号，应该考虑采用铜轴电缆屏蔽结构设计，即将所布的线上下左右用地线隔离，而且还要考虑好如何有效的让屏蔽地与实际地平面有效结合。 ![图 13](/images/b73512a32176ce2e26bea628dbecf5d80cf618927675ac109e3237eb303aded3.png)  
12. 走线终结网络规则：
在高速数字电路中， 当PCB布线的延迟时间大于信号上升时间（或下降时间） 的1/4时，该布线即可以看成传输线，为了保证信号的输入和输出阻抗与传输线的阻抗正确匹配，可以采用多种形式的匹配方法， 所选择的匹配方法与网络的连接方式和布线的拓朴结构有关。
A. 对于点对点（一个输出对应一个输入） 连接， 可以选择始端串联匹配或终端并联匹配。前者结构简单，成本低，但延迟较大。后者匹配效果好，但结构复杂，成本较高。
B. 对于点对多点（一个输出对应多个输出） 连接， 当网络的拓朴结构为菊花链时，应选择终端并联匹配。
当网络为星型结构时，可以参考点对点结构。星形和菊花链为两种基本的拓扑结构, 其他结构可看成基本结构的变形, 可采取一些灵活措施进行匹配。
在实际操作中要兼顾成本、 功耗和性能等因素， 一般不追求完全匹配，只要将失配引起的反射等干扰限制在可接受的范围即可。![图 14](/images/e33a9a8e942c90b9ba35587114e0282707541faa4830dfe525c83c3190d80dbc.png)  
13. 走线闭环检查规则：
防止信号线在不同层间形成自环。在多层板设计中容易发生此类问题， 自环将引起辐射干扰。![图 15](/images/c885c96dbf7ab6b02422db4f2994f3d55ea47c280975f464028cd72af9d4f4cf.png)  
14. 走线的分枝长度控制规则：
尽量控制分枝的长度，一般的要求是Tdelay<=Trise/20。![图 16](/images/a77c0592085fe218e9b982c479257b1e52ff0c2ebf1bb61718c2187f67bd4310.png)  
15. 走线的谐振规则：
主要针对高频信号设计而言， 即布线长度不得与其波长成整数倍关系， 以免产生谐振现象。![图 17](/images/487075fd441bb1c2e98d64171ca25e5f99043cdad0b46a556b517495ad0aeeb1.png)  
16. 孤立铜区控制规则：
孤立铜区的出现， 将带来一些不可预知的问题， 因此将孤立铜区与别的信号相接， 有助于改善信号质量，通常是将孤立铜区接地或删除。
在实际的制作中， PCB厂家将一些板的空置部分增加了一些铜箔，这主要是为了方便印制板加工，同时对防止印制板翘曲也有一定的作用。![图 18](/images/440ffb6c3a862cbd2f4670a3a8056d776b9cd77ed105b005d2b9b3987dd487da.png)  
17. 重叠电源与地线层规则：
不同电源层在空间上要避免重叠。主要是为了减少不同电源之间的干扰， 特别是一些电压相差很大的电源之间， 电源平面的重叠问题一定要设法避免， 难以避免时可考虑中间隔地层。![图 19](/images/1f2db0734dc551cee2436fcb2e0e79eac248321ee0625989b38d5a4b609857e3.png)  
18. 20H规则：
由于电源层与地层之间的电场是变化的， 在板的边缘会向外辐射电磁干扰。称为边沿效应。
解决的办法是将电源层内缩， 使得电场只在接地层的范围内传导。以一个H（电源和地之间的介质厚度）为单位，若内缩20H则可以将70%的电场限制在接地层边沿内；内缩100H则可以将98%的电场限制在内。 ![图 20](/images/c047ed585330bfe6a93ab82f5a294290b7c06c5ac615fa89a6dcadce0d153cd2.png)  
### （4）其他
对于单双层板电源线应尽量粗而短。电源线和地线的宽度要求可以根据1mm的线宽最大对应1A 的电流来计算，电源和地构成的环路尽量小。![图 21](/images/892163613c41be93c760b7b81286d42b7071fe1417ee517fab982ef9c9350e39.png)  
为了防止电源线较长时，电源线上的耦合杂讯直接进入负载器件，应在进入每个器件之前，先对电源去耦。且为了防止它们彼此间的相互干扰，对每个负载的电源独立去耦，并做到先滤波再进入负载。
在布线中应保持接地良好。如下图。![图 22](/images/ef6ac6fa34a2d4749851a5b3505019be0a813f2d58d6fb01e9335b08b3c3093b.png)  
