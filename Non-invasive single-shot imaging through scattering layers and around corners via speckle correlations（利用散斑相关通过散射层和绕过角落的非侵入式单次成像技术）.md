# Non-invasive single-shot imaging through scattering layers and around corners via speckle correlations（利用散斑相关通过散射层和绕过角落的非侵入式单次成像技术）

## 绪论

该技术利用散斑相关性的记忆效应，使用标准相机捕获散射光的单张高分辨率图像，通过在视觉上的不透明层以及绕过角落，以分辨率极限进行成像。并不需要波前整形、时间门控等技术，由一台手机相机进行单次拍摄即可实现成像。

## 对该领域之前技术的优缺点进行概述

弹道光成像会受到介质深度影响；自适应光学技术需要“导星”或高初始图像对比度；受控波前整形需要已知对象或大量光学模型长时间采集，成本过高；Bertolotti方法仅适用于完全静止物体，对动态物体以及快速成像场景不适用

## 对该技术的具体内容进行介绍

![基于散斑相关的非入侵式散射层成像](https://i.ibb.co/F5X3XTY/image.png)图1 | 基于散斑相关的非侵入式散射层成像：概念和数值示例。a，实验装置。目标物体（数字示例中的一组细胞器）被隐藏在一个不透明的散射介质后面。目标物体由一个空间上不相干的窄带光源照明，高分辨率相机记录散射介质另一侧的散射光模式。 b，原始相机图像I(θ)。在记忆效应范围内，这个图像是目标强度分布O(θ)与随机散斑图案S(θ)的卷积结果。 c，看似没有信息的原始相机图像的自相关，I*I，与目标物体的自相关基本相同(g)，就像它被替换了散射介质，被一个无象差光学系统成像的结果一样（e-g），这是由于散斑图案的尖峰自相关性质27,29,30。d，通过迭代相位恢复算法，从b的自相关中获取目标物体的图像。比例尺：30个相机像素。

&emsp;&emsp;该技术通过使用空间非相干光与数码相机通过不透明散射介质拍摄图片，并通过对自相关后的图像进行迭代Fienup算法进行图像恢复。  
    在光学中，自相关是指一幅图像与其本身通过一定的移动偏移后的重叠部分所计算得到的相关性函数。它可以用于描述图像中的统计特征，比如对称性、周期性等。在计算机视觉和图像处理中，自相关也经常用于图像匹配、物体识别、图像修复等领域。在光学中，自相关通常被用来描述散斑图案的统计特性。  
&emsp;&emsp;虽然拍摄的图像低对比度且看起来没有信息，但其自相关与对象自相关基本相同，通过自相关进行算法计算即可恢复图像  

### 对自相关公式的解释

&emsp;&emsp;**该部分通过公式解释漫反射光的自相关与物体自相关之间的关系：物体图像的自相关可以看做物体自相关与散斑自相关的卷积，即相机图像的自相关相当于物体的自相关**  
&emsp;&emsp;漫射光的自相关与物体的自相关基本相同”的原因是由于“角度记忆效应”引起的固有等像性（isoplanatism），即漫反射光的自相关与物体的自相关之间具有一定的相关性。  
&emsp;&emsp;物体平面上位于记忆效应范围内的相对距离 Δx 处的点 (Δx < u·λ/πL) 在相机上生成几乎相同的散斑图案。这些图案在相机平面上相对于彼此移动距离Δy=Δx·v/u（u 物体与散射介质的距离，L散射介质厚度，v介质与相机的距离）  
对于空间非相干的照明（以及荧光发射），不会在不同的模式之间产生干涉，相机图像只是这些相同的偏移散斑强度模式S(θ)和S(θ + Δθ)的叠加，其中Δθ = Δx/u是视角。  
&emsp;&emsp;因此，这使得图1a中的系统可以被视为一个具有平移不变点扩散函数（PSF）的非相干成像系统，该点扩散函数等于这个随机斑图S（θ），并且具有一个放大倍率为M = v/u。  
&emsp;&emsp;相机图像I(y)是由物体强度图案O(x)与该点扩散函数（PSF）进行卷积得到的，其中PSF是随机斑图S(θ)：I(vθ) = O(uθ) ∗ S(θ)——其中符号∗表示卷积运算。对相机图像进行自相关，再使用卷积定理，得到：
![漫反射自相关与物体自相关之间的联系](https://i.ibb.co/yhdqgK5/image.png)
&emsp;&emsp;由于散斑图案的自相关函数(S★S)是一个锐峰函数，即本质上是宽带噪声的自相关函数，因此公式右侧的部分实际上等于物体图像的自相关函数O★O  
&emsp;&emsp;等式右边的内容相当于物体图像的自相关，更准确地说，相机图像的自相关等于物体的自相关，因为它本应由替代散射介质的无像差成像系统成像  
![相机图片自相关等于物体自相关](https://i.ibb.co/QP2gLZ9/image.png)更确切地说，相机图像的自相关等于物体在取代散射介质的无像差成像系统下成像的自相关（如图1e-g所示），其中还有一个常数背景项C，它来自散斑自相关的2：1峰值-背景比率。

### 相比之前技术的优势

&emsp;&emsp;这种方法使得不透明层有效充当了完美的薄透镜，且不需要侵入式校准映射样品的散射特性，且成像过程对介质微观结构变化不敏感  
&emsp;&emsp;相比之前方法需要从多个图像中进行平均，利用散斑在漫射状态的类遍历特性和现代数码相机的高像素，使得人们可以对单个图像中的数百万个散斑相关函数进行平均  
&emsp;&emsp;通过散射介质成像相比传统基于透镜成像的系统无论距离如何散射光的点扩散函数始终是一个具有尖锐峰值自相关函数的散斑，而传统系统只有在较小范围内具有衍射极限，因此这种方式的成像具有无限景深的特征  

### 该方法的限制

1.视场角在散射媒介的扩散区域内受到记忆效应范围的限制，与介质厚度L成反比。  
2.从散射介质收集光线的孔径决定了成像的分辨率  

## 具体实验验证

&emsp;&emsp;**使用不透明光学扰动器和生物样品作为散射介质，对各种物体成像。使用各种形状和复杂度的多个物体进行重建，其原始相机的图像对比度不同**

![通过一个不透明的光学扰动器和两个生物样品的实验成像](https://i.ibb.co/G2ChFtx/image.png)图2 | 通过一个不透明的光学扰动器和两个生物样品的实验成像。a. 所散射光的原始相机图像（仅显示中心部分）。b. 相应的相机图像自相关，显示出清晰的独特图案。c. 通过相位恢复从b的自相关中重建的物体。d. 直接在没有散射介质的情况下成像的物体。e-l，不同成像物体和散射介质的实验结果：约300 μm厚的鸡胸肉（e-h）；一片新鲜的80 μm厚的葱皮（i-l）。在i-l中，自相关是从十个不同时间拍摄的图像集成平均得到的（参见补充视频1）。比例尺：相当于200 μm（a-c）的20个相机像素，在物体平面上为700 μm（e-g）和450 μm（i-k）。  

**多次获取图像进行平均可以得到更好的效果**  
&emsp;&emsp;由于只需要一次相机拍摄，该技术可用于通过动态变化的样本进行成像。有趣的是，通过在不同时间获取一组散射光的图像，可以利用样本的动态来更好地估计自相关。  
&emsp;&emsp;尽管隐藏的物体可以从此图像集合中的任何一幅图像中进行重建，但将自相关值在所有获得的十幅图像上进行平均会得到一个更好的自相关值估计，因为它对不同的散斑实现进行了集合平均，这正如在恒星斑点干涉术中所做的那样。这样一种技术可以利用自然样品的动态性质进行成像，而不是与之对抗。  

## 两个散射体之间的非侵入式成像

![两个散射体之间的非侵入式成像](https://i.ibb.co/jRyv5Xf/image.png)a，实验示意图（见补充图1b）。被成像的目标物放置在两个视觉上不透明的散射体之间（分别在20毫米和18.5厘米处）。透过第一个散射体对目标物进行照明，观察通过第二个散射体散射的光图案。b，散射光的原始相机图像（仅展示中央部分）。c，由b的自相关重建的成像结果。d，没有任何散射体的直接成像图像。e，通过第一个散射体对目标物进行常规成像（背照明）。f-i，用于不同目标物的b-e。比例尺：20个相机像素，相当于目标平面上的270微米。

&emsp;&emsp;目标对象隐藏于两个视觉上不透明的漫射器间，记录散射光通过第二个漫射器的图像，并通过自相关成像  

## 拐角成像的实验

![利用反射散射光单次拍摄实现“角落”成像](https://i.ibb.co/0CJC0yc/image.png)图4 | 利用反射散射光单次拍摄实现“角落里”的成像。 a，来自一个空间不相干被照射物体的光线击中高度散射的氧化锌“白漆”层。高分辨率相机记录给定偏振下反射散射光图案的单张图像。 b，相机图像的中心部分。 c，通过相机图像的自相关重建的物体图像。 d，真实的隐藏物体图像。刻度尺：20个相机像素，相当于物体平面上的400微米。Pol，线偏振器。  

&emsp;&emsp;通过漫反射墙面反射回来的光成像被遮挡物体。在反射模式下，成像分辨率和视场大小的计算公式与透射模式相同，但需要将介质厚度 L 替换为输运平均自由程 l*。值得注意的是，散射越强（平均自由程越短），FOV 越大。对于高度散射的白色油漆颜料，传输平均自由程l*在1μm左右，相应的角度视场超过几度。在这里，仅使用标准相机，散射墙就可以有效地充当镜子。这是对以前“拐角处”成像方法的重大简化。  

## 使用智能手机代替数码相机进行散射介质成像

![用智能手机相机穿透视觉障碍层进行成像](https://i.ibb.co/0CJC0yc/image.png)图5 | 用智能手机相机穿透视觉障碍层进行成像。a，实验照片：使用一部智能手机相机（Nokia Lumia 1020）通过高度散射的地面玻璃漫射器拍摄物体（在该图像中为字母“X”）。 b，以线性强度比例显示的原始相机图像（比例尺：500像素）。 c，左列：计算出b中图像的自相关。中列：从图像自相关重建的物体。右列：真实隐藏物体的图像。 d-g，与a-c类似但为不同的物体。在g中，处理了一个非线性伽马校正的JPEG图像。比例尺：50个相机像素，相当于物体平面上的1.7毫米。  
&emsp;&emsp;在使用低成本成像设备进行这些实验时需要考虑的主要障碍是它们固定的微型光学器件，它们规定了视角和放大倍数，可能会引入像差，从而限制视场。
&emsp;&emsp;此外，拜耳彩色滤光片传感器阵列在插值到全分辨率时会引入像素级伪像。
&emsp;&emsp;最后，在处理使用常见的 JPEG 压缩和伽马校正保存的图像时，额外的伪影和动态范围限制会干扰重建。
&emsp;&emsp;然而，这些仍然允许重建简单的对象，如图 5g 所示。  

## 实现散射介质成像需要满足的几个条件

1.通过介质看到的物体尺寸必须小于记忆效应范围（FOV）,当物体与散射层的距离远大于有效层厚度时有效。  
2.散斑粒子至少是像素尺寸的两倍大。  
    通过调整相机与散射介质的距离和/或通过在散射介质后面放置适当的孔径光阑，很容易满足这种条件。
3.要在物体平面上获得足够多的分辨率单元。  
    增加分辨率的一个实际限制是原始图像对比度降低，这是由于物体上明亮分辨率单元的数量增加（N，总和移动散斑图案的数量）。
4.用于成像的光谱带宽应比散斑光谱相关宽度更窄，保证PSF为高对比度的散斑模式  
    通过控制照明带宽（如此处所做的那样）或在使用时间不相干信号（例如荧光）时在相机前放置窄带滤波器，可以轻松满足对有限检测光谱宽度的要求。这一步骤通常使用自然光进行恒星斑点干涉术，并且最近还演示了使用散射的宽带白光和埋在0.5毫米厚的散射生物组织中的荧光发射。  
    重要的是要注意，并非必须将光过滤到小于 δω 的带宽，并且可以使用更大的带宽。这会降低原始图像对比度，但不应影响成像分辨率，因为 S(θ) 的自相关仍然是一个尖锐的峰值函数。或者，可以通过将多个光谱带分离到多个相机来同时处理多个光谱带，从而允许进行额外的整体平均或多光谱成像。

&emsp;&emsp;以上条件都是为了保证采样和处理的散斑数量最大化，这对准确估计自相关函数以及减去背景噪声都有重要作用。  

## 对该方法的改进

&emsp;&emsp;在这个概念验证中，我们使用了 Fienup 的基本相位检索算法，并且没有特别努力来克服这些简单算法的常见停滞和伪影问题。通过应用更先进的方法，例如多数表决和减少支持约束，预计可以实现更高保真度的重建  
&emsp;&emsp;此外，通过使用不同的散斑干涉分析技术，例如三重相关分析，在某些情况下可以从可用数据中获得额外的相位信息。  
&emsp;&emsp;另一个潜在的改进可能是通过应用压缩相位检索算法来减少采集时间并提高重建保真度。特别是，在涉及复杂对象和低 SNR 条件的场景中需要进行此类改进，其中对象的高强度特征往往主导重建  
&emsp;&emsp;有趣的是，如果只想追踪未知物体而不需要重构其形状，可以在不需要任何相位恢复算法的情况下，在不同时间拍摄的图像之间进行简单的互相关操作。  

## 两篇非侵入式成像的对比

相同之处：

1. 两篇论文都探讨了通过散射介质进行非侵入式成像的方法。
2. 两篇论文都是基于散射介质中的光学多次散射和随机相位的效应，通过利用光子的统计特性来重构目标图像。
3. 两篇论文都使用了类似的实验装置和处理算法。

不同之处：

1. 两篇论文的应用场景不同。《Non-invasive imaging through opaque scattering layers》侧重于在不移动或干扰样品的情况下实现穿透不透明散射介质的成像，而《Non-invasive single-shot imaging through scattering layers and around corners via speckle correlations》则更注重在散射介质内进行成像，包括在目标周围和通过多次散射后的目标内部。
2. 两篇论文采用的成像方法不同。《Non-invasive imaging through opaque scattering layers》使用了多次扫描和反演算法来重构图像，而《Non-invasive single-shot imaging through scattering layers and around corners via speckle correlations》则采用了一次拍摄和Gerchberg-Saxton类型算法来重构图像。
3. 两篇论文的实验数据来源不同。《Non-invasive imaging through opaque scattering layers》的实验数据来自不同的物体，而《Non-invasive single-shot imaging through scattering layers and around corners via speckle correlations》的实验数据则来自不同的散射介质和不同的目标。
4. 《Non-invasive imaging through opaque scattering layers》 仅介绍了通过散射介质多重散射的成像。而《Non-invasive single-shot imaging through scattering layers and around corners via speckle correlations》还使用了介质表面的漫反射来进行图像恢复。  

## MSO和自相关这两种图像恢复技术的异同点

&emsp;&emsp;MSO和自相关都是图像恢复中常用的方法，它们各自有其优缺点。  
&emsp;&emsp;MSO方法是通过测量样品在多个不同位置的点扩散函数（PSF）并通过求解矩阵伪逆来重构出样品的高分辨率图像。相对于自相关方法，MSO具有更高的灵活性，能够处理不同类型的样品和测量系统，而且适用于任意形状的点扩散函数，而自相关方法则需要假设点扩散函数是旋转对称的。但是，MSO需要测量多个PSF来构建测量矩阵，这需要较长的测量时间，因此不适用于需要实时重构图像的应用。  
&emsp;&emsp;自相关方法则可以通过单次测量直接得到样品的高分辨率图像，适用于需要实时重构图像的应用。另外，自相关方法对测量系统的要求相对较低，只需要保证测量系统的点扩散函数是旋转对称的即可。但是，自相关方法对样品的假设比较严格，需要假设样品是平移对称的，如果样品不满足这个假设，自相关方法的精度会受到影响。  
