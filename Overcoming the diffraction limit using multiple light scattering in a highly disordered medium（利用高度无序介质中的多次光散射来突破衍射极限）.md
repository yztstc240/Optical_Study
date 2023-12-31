# Overconming the diffraction limit using multiple light scattering in a highly disordered medium(利用高度无序介质中的多次光散射来突破衍射极限)

## 绪论

本文通过开发一种从混浊介质引起的多次散射中提取原始图像信息的方法，显着增加了成像系统的数值孔径。结果，分辨率提高了衍射极限的五倍以上，并且视野扩展到相机的物理区域。该技术为使用混浊介质作为远场超透镜奠定了基础。

    衍射极限是指在一定波长的光照射下，能够有效聚焦的最小斑点大小。它是由光学衍射效应所限制的，即当光线穿过一个孔径或通过一个物体时，光波将会发生衍射现象，导致聚焦的斑点受到限制。根据瑞利判据，衍射极限的大小与入射光的波长和系统的孔径大小有关。在光学成像中，如果想要获得高分辨率的图像，就需要将衍射极限控制在一个足够小的范围内。

## 介绍目前无序介质成像相关成果

&emsp;&emsp;传统镜头通过物体散射的波聚焦到检测器成像，如果物体与透镜间存在内部结构高度无序的浑浊介质，则由于介质的散射，来自物体的图像会严重受损或消失。

&emsp;&emsp;目前有许多消除由介质浑浊引起图像劣化的方法。传统方法使用统计校正或波前控制来消除浊度引起的图像恶化。然而，最近的研究表明，无序介质可以捕获隐失波并将其转化为远场传播波，可用于亚波长聚焦。时间反演镜和反馈控制已用于扫描显微镜，但使用浊介质来克服宽场成像的衍射极限是一个相对未被探索的领域。

## 概述无序介质的特性以及浑浊透镜成像（TLI）技术的实现

![实验示意图](https://i.ibb.co/hMYcj7H/image.png)图1：实验示意图。 (a) 带有目标（LO）和筒（LT）镜头的传统成像方式。θmax 是物镜能接受的最大角度。(b) 插入一个无序介质可以捕获其角度θT超过θmax的散射波。(c) 散射波通过多次散射过程（实线红线）到达相机传感器，即使物体偏离了传统视场（灰色区域）。

&emsp;&emsp;浑浊透镜成像（TLI）技术通过插入浑浊介质使得较小NA的透镜可以捕获来自物体的高角散射波，打破传统透镜的衍射极限，实现广角成像，极大地改善了成像系统的空间分辨率和可视范围

    在光学中，NA（数值孔径）是一个常用的指标，用于描述光路系统的光收集能力。它是一个纯量，定义为介质中的最大孔径直径与镜头焦距的比值。数值孔径越大，相应的光路系统就能收集到更多的光线，从而具有更好的分辨率和灵敏度。例如，高数值孔径的物镜通常能够提供更高的分辨率和对微小样品的更好观察能力。NA的计算公式为NA=n*sinθ，其中n是介质的折射率，θ是半孔角，即从物镜前焦面到最大孔径所夹的角度。

 &emsp;&emsp;在传统成像中，视场大小由图像传感器的尺寸L和成像系统的放大倍数M决定，即视场大小为L/M。然而，插入无序介质可以将成像区域扩大超过这个关系式所设定的限制。如图 1(c) 所示，位于视野外的物体中某个点的散射波在普通成像中不会到达相机传感器（蓝色虚线）。但是当引入混浊介质时，它会通过多次散射将一些传输波重定向到相机传感器。无序介质可以收集来自常规视野外的物体的光.

 &emsp;&emsp;利用浊度的两个独特优势——突破衍射极限和扩大视场的关键挑战是从多次散射的波中提取图像信息。通过计算传输矩阵与失真图像的相关性使得可以从多次散射的波中提取出图像信息

## TLI的具体实现过程

![TLI原理示意图](https://i.ibb.co/WH84bRn/image.png)图2：混浊透镜成像（TLI）的原理示意图。（a）记录混乱介质的透射矩阵。使用He-Ne激光器（λ=633 nm）从平面波的入射角（θx，θy）扫描，并记录每个入射角下的透射波。 （b）构成透射矩阵的记录的透射图像。这里只显示振幅图像，尽管同时记录了共轭相位图像。 （c）按照图1（b）的配置记录目标图像。（d）物体的扭曲图像，即分辨率目标图案。 （e）由投影操作获取的物体的角谱图（详见正文）。这里只显示幅度分量，尽管相位信息也很重要（详见补充材料）。比例尺：0.5 μm-1。（f）在插入ZnO层之前拍摄的分辨率目标图像。比例尺：10 μm。（g）从（e）中的角谱重建的目标图像。

### 1.记录传输矩阵并通过层析相位显微镜在无序介质的输入与输出建立确定性联系

&emsp;&emsp;为了记录混沌介质的传输矩阵，我们用激光束照亮介质，并在扫描照明角度（θx，θy）的同时记录输出图像Etrans（x，y; θx，θy）。  
&emsp;&emsp;对于此记录，我们使用了层析相位显微镜，这是一种配备散斑场成像能力的高速干涉显微镜系统 。它通过数字全息术快速扫描照明并记录输出波的电场图像，而不是强度图像。记录覆盖对应于 0.5 NA 的照明角度范围的 20000 张图像需要 40 秒。一组输出图像形成一个基集，在无序介质的输入和输出之间建立确定性联系。  
&emsp;&emsp;一旦确定了该传输矩阵，无序介质就不再是成像的障碍，而是可以充当具有有趣特性的非常规透镜。

### 2，通过将散射获得的物体失真图像Ed与传输矩阵的各角度分量Etrans进行投影操作，获得图像的角度波谱

&emsp;&emsp;通过将传输矩阵的每个角度分量 Etrans(x, y; θx, θy) 与物体的畸变图像进行投影操作，我们恢复了构成物体图像的角度波谱 A(θx, θy)。  
![传输矩阵投影得到图像的角度波谱](https://i.ibb.co/nM9q4rv/image.png)
&emsp;&emsp;角谱的角度范围对应于记录的传输矩阵的角度范围。图2（e）显示了从物体的扭曲图像获得的角谱，从这个角谱重建的图像（图2（g））与原始物体具有良好的结构对应关系。  

## TLI关于克服衍射极限的限制

![TLI克服衍射极限的限制](https://i.ibb.co/Cm5Kch3/image.png)使用高数值孔径（NA=1.0）的物镜成像（图3(a)），并使用低数值孔径（NA=0.15）的物镜成像（图3(b)），可以看到红色箭头所示的细小标记在后者中不可见。  
图3(c)显示了在插入ZnO层（T=6%）后，使用低数值孔径物镜成像的物体的失真图像。通过TLI从失真图像中恢复出的物体图像如图3(d)所示。即使使用0.15 NA的物镜成像，也可以看到细小的标记。  
图3(e)显示了从最细线条（图3(a)中的红色框）处分别采用高NA（蓝色曲线）和低NA（绿色曲线）物镜获得的角谱，其中橙色箭头所示的峰值是与结构的周期性共轭的。  
图3(f)显示了对高浊度（T=6%，红色曲线）和低浊度（T=70%，黑色曲线）浊介质获得的角谱。图3(g)显示了各种浊介质的归一化信噪比。  

&emsp;&emsp;首先，我们记录 ZnO 层的传输矩阵。尽管物镜 NA 限制为 0.15，但传输矩阵可以记录高达 0.85 NA，因为无序介质将高角度分量转换为低角度分量。如果未插入 ZnO 层，则传输矩阵将被限制在对应于 0.15 NA 的角度范围内。  
&emsp;&emsp;接下来，拍摄被 ZnO 层扭曲的物体图像：该图像显示出散斑图案，其平均散斑尺寸对应于 0.15 NA 设置的衍射极限（图 3（c））。然而，它包含高角度散射波和低角度散射波。使用投影操作，我们提取物体的角谱 A(θx, θy)，嵌入到失真图像中，并从 A(θx, θy) 重建物体图像（图 3（d））。  
&emsp;&emsp;在记录传输矩阵时，我们沿着垂直于目标中的条形码线的方向，扫描输入波的角度从-53°到53°（0.85 NA），共计5000步。因此，我们从失真图像中获得高达 0.85 NA 的物体光谱，而不是 0.15 NA。数值孔径增加了 5 倍以上，空间分辨率增加了相同的倍数。  
&emsp;&emsp;由于无序介质的特性，高角度分量转换为了低角度分量。因此低NA的传输矩阵可以获得更高NA的记录，因此可以克服衍射极限的限制。接着使用投影操作对图像进行重建，可以达到很好的效果  

## 介质浑浊程度与TLI成像的关系

### 与成像保真度的关系

&emsp;&emsp;在该研究中，改变ZnO层的厚度并使用它们的平均透射作为浊度的标准：透射越低，介质的浑浊度越高。随着浊度的增加，无序介质将高角度输入波转换为低角度输出的能力增加。  
&emsp;&emsp;随着浊度的降低，信噪比下降，重建图像中的噪声增加。这表明对于 TLI 技术来说，高浊度是有利的。  

### 与视野（FOV）的关系

![TLI扩大了视野](https://i.ibb.co/0B6dV58/image.png)(a)一个没有浑浊度的目标物体，(b) 有浑浊度的目标物体。只有实心红框是记录区域。比例尺：10微米。(c)-(e) 在不同浑浊度下的重建图像，T=100％ ((c)，无浑浊度)，T=20％ (d) 和T=6％ (e)。(f) 扩大视场与斑点扩散程度的关系，对比度下降一半作为视场扩大的标准。通过一种无序介质透过的斑点 (直径为5微米) 的透射图像的HWHM用于确定斑点扩散程度。代表性的扩展斑点图像在底部显示。从左到右，分别为T=100％、20％和6％的透射率。数据点分别对应于透射率T=100％、70％、50％、30％、20％、10％和6％。

&emsp;&emsp;随着浑浊程度的增加，通过散射获得的信息就更多，传感器能够接收的视野范围也就更大。因此利用传输矩阵恢复图像时的保真度也就更高

## 对TLI技术的具体介绍

&emsp;&emsp;当平面波入射到目标物体时，包含物体图像的透射波 Es(x,y) 可以分解为具有不同传播角度的平面波。换句话说，透射波可以描述为角谱AS(kx,ky)，它是构成透射波的每个角平面波的复振幅。因此，Es(x,y)和AS(kx,ky)具有以下关系。  
![透射波公式](https://i.ibb.co/W2LnSCt/image.png)  
&emsp;&emsp;其中，kx和ky是分别沿x和y方向的散射波的波矢分量（光轴沿z方向）。通过 kx/2π= sin θx/λ 和 ky/2π= sin θy/λ，kx和ky可以分别与主文中的θx和θy相关联。当物体波通过一个无序介质传播时，它会被扭曲成一个复杂的散斑图案。图像扭曲可以被视为构成物体波的各个角度波的扭曲的结果。假设每个角度平面波，exp(ikxx+ikyy)，都被扭曲成一个独特的散斑图案，Etrans(x, y; kx, ky)。那么经过传输后的Es(x,y)就被转换成了扭曲波Ed(x,y)。  
&emsp;&emsp;因此，一组Etrans (x, y; kx, ky)，也称为传输矩阵，决定了无序介质在扰乱物体图像方面的作用。  
![散斑图像中包含传输信息](https://i.ibb.co/XCsbZxV/image.png)  
&emsp;&emsp;为了从畸变的图像 Ed(x,y) 中获取原始图像 Es(x,y)，我们需要在 Ed(x,y) 上进行一个投影操作，将其投影到传输矩阵 Etrans(x,y;kx,ky) 的 (kx,ky) 分量上。由于无序介质对于不同输入平面波的角度生成完全不同的输出场，因此传输矩阵的各个分量相对于彼此是正交的。因此，可以通过投影操作来恢复角谱。  
![通过投影恢复角谱](https://i.ibb.co/XD4yJ81/image.png)  
&emsp;&emsp;通过将扭曲图像投影到传输矩阵的所有(kx, ky)分量上进行多次投影操作，可以获得物体波的角谱(y,x,Sk,kA)，只要测量传输矩阵的程度足够。然后，可以从式（S1）中重建物体波。总之，通过记录传输矩阵来表征无序介质，可以将复杂的随机介质转化为有用的确定性光学元件，从而可以进行成像。  
