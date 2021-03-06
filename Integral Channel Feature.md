# Integral Channel Feature

1. Aggregate Channel Feature(聚合通道特征)， 积分通道特征的一种新变体

2. integral channel features（ICF， 积分通道特征）:我理解是可以通过积分图像计算的一类特征

   #### Haar 特征

   1. Haar-like矩形特征是用于物体检测的数字图像特征
   2. 这类矩形特征模板由两个或多个全等的黑白矩形相邻组合而成，而矩形特征值是白色矩形的灰度值的和减去黑色矩形的灰度值的和
   3. 矩形特征对一些简单的图形结构，如线段、边缘比较敏感。如果把这样的矩形放在一个非人脸区域，那么计算出的特征值应该和人脸特征值不一样，所以这些矩形就是为了把人脸特征量化，以区分人脸和非人脸

   #### Local sums

   1. 局部区域像素和

   #### Gradient histogram

   1.  梯度直方图
   2. 求出原始图像的gradient angle 和gradient magnitude,这个角度的值会决定对应像素落在直方图的那个bin上，而这个像素的gradient magnitude值会决定这个像素对这个bin的贡献

   #### Integral images

   ​		它的积分图也是同样大小的图片，即4*4大小，在积分图中，每个像素的的值，是原始图像中该位置	左上角区域内所有的像素和。可以通过积分图像（Integral images）计算其他特征，比如local sums。

   ## Paper

   ### Abstract

   1. 我们研究图像分类任务中“积分通道特征”的性能，特别关注行人检测
   2. 积分通道特征背后的一般思想是使用输入图像的线性和非线性变换计算多个注册图像通道，然后使用积分图像高效地计算local sums、histograms和Haar特征及其各种泛化。
   3. 这些特性在最近的文献中被用于各种各样的任务——实际上，变体似乎是独立地发明了多次。
   4. 虽然集成通道特性已经被证明是有效的，但是很少有人对其本身进行分析或优化
   5. 在这项工作中，我们对这一领域的相关工作提出了统一的看法，并进行了详细的实验评估。
   6. 我们证明,如果设计得当,Integral channel feature不仅胜过其他feature，包括直方图的梯度(HOG),他们也自然(1)集成异构数据源的信息,(2)更少的参数设置，并且对参数不敏感,(3)在检测中允许更精确的空间定位,和(4)导致快速检测器当级联分类器时

   ### Introduction

   1. 目标检测系统的性能取决于两个关键因素:学习算法和特征表示

   2. 最近在learning[8,10,24,26]和features design[5,23,28]方面都取得了相当大的进展。

   3. 在这项工作中，我们使用标准的增强方法[11]，而不是将我们的注意力集中在特性的选择上

   4. 我们的研究基于以下架构:多个注册图像通道使用输入图像的线性和非线性变换进行计算[12,17];接下来，使用局部矩形区域上的和从每个通道提取特征。

   5. 利用积分图像有效地计算了这些局部和，以及利用哈尔小波[27]、各种泛化[7]、甚至局部直方图[20]等多个局部和计算的特征

   6. 这些local sums 和features使用多种的这样的和计算，包括Haar-like wavelets，他们的各种泛化，甚至局部直方图等可以通过integral images有效计算的。

   7. 我们将这些特征称为积分通道特征，如图1所示。

   8. Integral channel features结合了图像信道信息的丰富性和多样性，以及Viola和Jones检测框架[27]的计算效率。

   9. 多篇论文利用了Integral channel features(积分通道特征)的变体，应用包括目标识别[16,24]、行人检测[7,31]、边缘检测[6]、脑解剖结构分割[25]和局部区域匹配

   10. 在1.1节中给出了这些作品中特征表示的统一概述。

   11. 虽然积分通道特性已经被证明是有效的，但是很少有人对其本身进行分析或优化。

   12. 在上面提到的许多作品中，关注的重点都是学习方面[7,8,24]或新颖的应用[2,6,25]，很难将功能更丰富带来的性能收益与功能更强大的学习方法带来的收益分离开来。

   13. 在[16,30,31]中，作者使用积分通道特征来计算梯度方向直方图;虽然这些方法取得了良好的效果;它们没有充分挖掘这些表现的潜力

   14. 此外，文献中使用的一些积分通道特性在计算上非常昂贵，例如[6]中的通道需要30秒才能计算出640x480的图像。

   15. 在这项工作中，我们展示了如何计算有效的通道，约:05-:2s每640x480图像取决于选择的选项。

   16. 对于320x240图像，通道可以在标准PC上以每秒20-80帧的速度实时计算。

   17. INRIA行人数据集[5]是我们的主要测试平台。

   18. 行人检测在过去几年引起了人们极大的兴趣;另外，Histogram of Oriented Gradient (HOG)[5]的描述是特别针对INRIA数据集设计的

   19. HOG被成功地用于许多对象检测任务，是PASCAL对象挑战中最常用的特性之一

   20. 因此，不仅是 pedestrian detection领域对其感兴趣，HOG在其他领域的成功也为行人检测结果的有效推广提供了强有力的证据

   21. 我们对集成通道特性的详细实验探索，以及一些性能优化和互补通道类型的使用，导致了性能的巨大提高。

   22. 我们展示了显著改善的结果比起以往的应用，使用类似的特征进行行人检测

   23. 事实上，对INRIA行人数据集的全图像评估表明，使用标准增强结合优化的积分通道特征进行学习，可以匹配或优于除一种方法之外的所有方法，包括使用HOG特征通过更复杂的学习技术获得的最先进方法

   24. 在INRIA数据集中进行精确定位的任务上，该方法的性能明显优于现有的方法

   25. 最后，我们展示了在最近引入的Caltech行人数据集[9]上的结果，在每幅图像1个假阳性的情况下，检测率接近60%，相比之下，包括HOG在内的其他方法的检测率最多为50%。

   26. 本文的其余部分组织如下：我们从下面对相关工作的回顾开始。在第2节中，我们对集成通道特性进行了更详细的概述，并在第3节中讨论了实现细节。我们在第4节中进行了详细的实验评估，并在第5节中得出结论。

       #### Related Work

       1. 通道的概念可以追溯到计算机视觉的早期
       2. Roberts交叉边缘检测器[22]使用了两个表示正交空间导数算子的微小(2x2)核
       3. 这些滤波器的响应，结合非线性得到边缘强度和方向的基本测量，可以认为是ur通道。
       4. 另一项早期工作是福岛的新认知管建筑，它使用分层通道来增加鉴别能力[12]
       5. 在接下来的几十年里，出现了许多扩展。例如，Malik & Perona[17]的纹理识别方法使用了一组带通滤波器响应的非线性组合计算出的几十个信道。
       6. Malik和Perona通过高斯平滑进行空间积分;最终，统计数据使用基于直方图的表示法进行汇总[15,21]，这种表示法至今仍很流行
       7. 此后不久，Viola和Jones提出了一种增强的对象检测方法，该方法的前端避免了计算上昂贵的带通内核，而是使用积分图像实现了高效的haar类小波
       8. 然而，随着计算能力的迅速提高，计算一组带通滤波器的响应不再是一个瓶颈。
       9. 在这样的通道上使用集成图像来有效地汇集具有不同支持区域的统计信息的想法自然也随之而来，这就产生了我们称为集成通道特征的表示
       10. 我们所知的将积分图像应用于多个图像通道的第一个应用出现在Tu关于概率增强树的研究中
       11. Tu在多个尺度上计算了Gabor过滤器和Canny边缘[4]的响应，并在增强的对象检测框架中在这些通道上使用了类似haar的特性
       12. 随后Tu将该方法扩展到[25]的3D MRI脑体积分割，得到的每个通道和Haar特征都是3D的。
       13. 同样，Dollar等人[6]使用积分通道特性来训练每像素边缘检测器;使用更仔细调优的特性得到的结果与这个方法的性能匹配。
       14. 使用了大量的通道，包括不同尺度的梯度、Gabor滤波器响应、偏移高斯滤波器的差分等。
       15. 行人检测[7]和learning patch descriptors采用相似的通道
       16. 在不同的工作中，积分通道特征被用来高效地计算梯度方向的直方图
       17. 如[20]中所述，矩形直方图可以通过将图像量化为多个通道来有效计算(详细信息见第2节)。
       18. 这一关键思想在文献[16,30,31]中至少被研究过三次。
       19. Zhu等人使用积分直方图来近似HOG特征，用于级联。Laptev[16]同样使用积分图像计算梯度直方图，从而得到有效的目标检测器
       20. 在后来的工作中，[30]对cat检测使用了类似的表示，除了特征是单个直方图箱，而不是[16,19]中的整个直方图。
       21. 尽管细节各不相同，但这些方法都没有探索可能的通道类型的丰富性，以无缝集成异构信息源

       ### Channel Types

       1. 给定输入图像I，对应的通道是原始图像的注册映射，其中输出像素由输入像素的对应块计算(从而保持图像的总体布局)。

       2. 对于灰度图像，简单的通道就是C = I，对于彩色图像，每个颜色通道都可以作为一个通道。

       3. 其他通道可以用I的线性或非线性变换来计算，下面讨论各种选择(也见图1)。

       4. 我们用W来表示一个信道生成函数，并写出C = Ω(I)

       5. 为了使用滑动窗口检测器进行快速检测，通道必须是平移不变的，即给定I和I'由平移关系，C = Ω(I)和C' = Ω(I')必须由相同的平移关系

       6. 这允许Ω在整个图像上计算一次，而不是对每个重叠检测窗口单独计算。

       7. 对于每个通道使用一个积分图像[27]，f (C)可以通过三个浮点运算来计算，并且由于这种一阶特征的计算速度非常快

       8. 我们将高阶通道特性定义为任何可以使用多个一阶特性计算的特性(例如，同一通道中两个简单特性的差异)。例如通道特征如图2所示。

       9. 以上是对Viola and Jones (VJ)[27]检测框架中所使用的特征的概括

       10. 具体来说，VJ使用了具有类似于Haar基函数[18]的特征的C = I。

       11. 使用上面的术语，Haar特征是一种高阶特征，它包含2-4个矩形的和，这些矩形以不同的模式排列，计算多尺度上的一阶和二阶图像导数。

       12. 这个描述有点过于简化，因为VJ实际上使用了两个通道的表示，其中C1(x,y) = I(x,y)和C2(x,y) = I(x,y)^2。

       13. 这两个通道一起用于检测窗口的方差归一化，导致光照条件变化的部分不变性(具体见[27])。

       14. 一个示例图像的许多通道类型如图1的面板A -h所示

       15. 注意，所有显示的通道都略小于输入图像;丢弃通道边界以避免引入不需要的工件是非常重要的。

       16. 下面我们将概述文献中使用的常见通道，它们在都是平移不变的

           1. **Gray & Color**: 最简单的通道是图像的灰度版本(面板a)，也可以使用颜色通道，在面板b中我们显示三个cie -luv彩色通道

           2. **Linear Filters**: 生成捕获图像不同方面的通道的简单方法是使用线性过滤器。

           3. 面板c显示I与4个定向Gabor滤波器[17]卷积;每个通道都包含I中不同方向的边缘信息

           4. 将I与不同的高斯滤波器(DoG)进行卷积，可以捕获不同尺度下图像的“纹理”(panel d)。

           5. 与大量滤波器的卷积可能很慢，但是线性滤波器是一种简单有效的生成各种通道的方法

           6. **Nonlinear Transformations**：有无数的平移不变的非线性图像变换，这里我们提出了几个说例证。

           7. Gradient magnitude(面板e)捕捉无方向性的边缘强度，而Canny edges(面板f)更显式地计算边缘信息

           8. 两者的梯度可以在不同的尺度上通过平滑输入图像来计算;此外，对于彩色图像，一个常见的技巧是分别计算3个颜色通道上的梯度，并使用最大响应

           9. 面板h显示了对输入图像进行阈值化后得到的通道，阈值为两个不同的阈值

           10. 虽然这种特殊形式的前景分割不是鲁棒的，更复杂的算法可以使用。

           11. **Pointwise Transformations**：通道中的每个像素都可以被任意函数转换为后处理步骤

           12. 这可以用来克服特征f必须是局部和的限制。

           13. 例如，取对数，我们可以得到本地的products，
               $$
               \exp (\sum {log(x_i)}) = \prod_i x_i
               $$
               同样，每个元素的p次幂也可以用来计算广义平均:
               $$
               (1/n\sum_{i=1}^n x^p_i)^{1/p}
               $$
               将p设置为一个大的值近似于xi的最大值，这对于积累值非常有用

           14. **Integral Histogram**:Porikli[20]提出了一种利用积分图像计算直方图的有效方法

           15. 让Q作为用值{1....q}量化的版本，让
               $$
               Q_i (x,y) = l[Q(x,y)=i]  \quad for \quad each \quad i \leq q 
               $$
               l是指标函数

           16. 计算Q = i区域内的元素可以通过对同一区域内的Qi求和来计算。

           17. 因此，在给定每个通道Qi的“直方图”的积分图像的情况下，可以有效地计算矩形区域上的直方图

           18. 尽管直方图通道可以在任何输入[16]上计算，但最常用的是下面描述的一种称为梯度直方图的变体[16,30,31]。

           19. 请注意，神经科学文献中对一种称为“值编码”的相关表现形式进行了广泛的研究，如[3]。

           20. **Gradient Histogram**：梯度直方图是一种加权直方图，其中bin指数由梯度角度决定，权重由梯度大小决定

           21. 换句话说，信道是由：
               $$
               Q_{\theta}(x, y) = G(x,y)l[\Theta(x,y)=\theta]
               $$
               G(x,y)和$ \Theta (x,y)\\​$​分别为梯度幅值和量子化梯度角,在I(x,y)

           22. 面板g显示了一个量化为4个方向的示例。

           23. 通过平滑I可以再次得到不同尺度的梯度，可以使用额外的通道存储梯度幅值(panel e)对得到的直方图L1进行归一化，从而使梯度直方图近似HOG特征[31]

           24. 还要注意面板c和g中的通道之间的相似性

           25. 虽然看起来有很大的不同，但将I与定向Gabor滤波器卷积，并通过梯度角量化梯度幅值，可以得到在质量上类似的通道捕获信息

           26. 我们简要讨论了渠道规模。

           27. 我们区分**预平滑**(平滑输入图像)和**后平滑**(平滑创建的通道)。

           28. 在Garding等人的术语中。预平滑确定了表示的“局部尺度”，并用于抑制精细尺度结构和图像噪声。

           29. 预平滑可以对捕获的信息产生显著影响，例如，预平滑决定了随后计算的梯度的大小，影响了计算的Canny边缘(panel f)或梯度直方图(panel g)。

           30. 另一方面，后平滑有助于确定信息汇集的“集成规模”

           31. 然而，集成规模也取决于通过通道计算的本地和的支持，这使得后平滑变得不那么有用

           32. 通道表示具有许多吸引人的属性。

           33. 上面定义的大多数通道都可以用给定的标准图像处理工具的几行代码来计算

           34. 此外，许多通道可以非常有效地计算(我们将在第3节中讨论优化技术)。

           35. 在第4节中，我们展示了用于计算通道的大多数参数并不重要(假设它们在训练和测试之间是一致的)。

           ### Implementation Details

           1. 我们评估了三种渠道的组合:梯度直方图、颜色(包括灰度、RGB、HSV、LUV)、梯度大小
           2. 这些通道可以有效地计算并捕获各种信息
           3. 下面我们将讨论参数设置，其中的参数很少，然后简要讨论优化技术
           4. 讨论了增强框架和全图像检测
           5. **Scale**:信道的常用参数包括局部尺度(预平滑)和集成尺度(后平滑)。
           6. 为了提高计算效率，我们使用一种基于二项式系数的近似(离散化)高斯滤波器进行平滑处理
           7. 二项滤波器的宽度由半径参数r决定，r对应$\sigma = \sqrt{(2r+1)/4}  $ 的高斯滤波器
           8. 为了避免引入边界效果，必须使用至少r像素的填充
           9. 我们对每个通道使用相同的比例设置
           10. **Parameters**:除了scale之外，对于gradient histograms，必须指定orientation bins的数量。
           11. 梯度大小和颜色通道没有额外的参数
           12. **Optimization**:上面的通道可以用给定的标准图像处理工具的几行代码来计算。
           13. 然而，一些优化技术可以大大减少计算时间
           14. 对于LUV彩色通道，瓶颈是立方根计算;我们用一个粗略的近似代替
           15. 计算梯度直方图的一个常用技巧，例如在[10]中使用的方法，是通过求沿单位圆均匀间隔的向量的点积的最大值来近似二维向量的角度
           16. 这可以通过二分查找快速完成
           17. 我们将梯度角近似为方向数的10倍，并使用线性插值将每个像素放置在适当的通道中。
           18. **Computation Time**:在标准PC上测试的320x240张图像,每秒可计算出LUV通道的帧数(fps)为:135fps,gradient magnitude为140fps,gradient histograms (with 6 bins) 有 60 fps
           19. 计算所有10个通道的图像可以在40 fps下进行，如果使用r <= 8的预平滑，可以在30-34 fps下进行。
           20. 请注意，这些速率不包括分类器的计算时间(尽管这也非常快)。
           21. **Features**:我们随机生成大量候选特性，而不是通过仔细的设计。
           22. 一阶特征是给定信道中矩形区域的和;我们通过随机选择通道索引和矩形(强制最小面积为25像素)来生成候选项。
           23. 高阶特征是一阶特征的随机加权和，每个特征可以跨越多个通道。
           24. nxn区域内可能的第一存储特征个数为O(n4)，在给定高阶特征的情况下，该数迅速增长;然而，随机抽样的特征通常产生良好的结果
           25. **Boosting**:boost提供了一种方便、快速的方法来学习给定大量候选特性的[11]，并作为VJ对象检测框架的基础
           26. 这里我们使用一种称为“soft cascade”[29]的变体。
           27. 在对每个弱分类器进行评估之后，将使用阈值，而不是具有多个不同的级联层
           28. 在整个数据集上训练一个单独的boosting分类器，训练后使用一个简单的启发式来设置阈值，使得训练过程大大简化，详见[29]
           29. 我们测试了boost的三种变体:AdaBoost、RealBoost和LogitBoost [11]
           30. 采用深度两棵决策树作为弱分类器
           31. 在一个并行的四核机器上，训练一个包含1000个弱分类器的增强分类器需要5-10分钟(相比之下，原来的VJ分类器需要2周)。
           32. 关键的优化是在训练开始时对特征值进行量化并缓存，这样在训练之后每个弱分类器的速度都很快。
           33. **Full Image Detection**:我们在多个尺度上使用滑动窗口.
           34. 我们使用4像素的步长和$2^{1/10} $的缩放步长。
           35. 非极大抑制(Non-maximal suppression, NMS)用于抑制多个邻近检测。
           36. 均值漂移NMS[5]受欢迎;但是，它有多个参数设置，这些设置取决于检测器的其他方面，如步长。
           37. 相反，我们使用一个简化的NMS过程，它抑制了根据PASCAL标准充分重叠的每一对探测的不确定性
           38. 虽然在最坏的情况下，NMS程序在检测数量上是O(n2)，但在实践中，它可以很快地完成
           39. 我们的NMS只有一个参数，即重叠阈值，我们将其设置为:6。
           40. 整个系统的运行时间约为2s，用于640x480图像的多尺度检测，是[9]中所调查的所有方法中速度最快的。

           ### Experiments

           1. 大部分实验是在INRIA行人数据集[5]上进行的，我们也展示了最近引入的Caltech行人数据集的结果

           2. 在比较参数设置时，我们使用按窗口性能评估计算的ROC曲线，从而避免了NMS或其他后处理

           3. 通常，我们会在每个窗口的参考点报告10^-4个假阳性(fppw)的检出率。

           4. 然而，正如[9]中所示，每个窗口的度量是有缺陷的，在某些情况下不能预测完整的图像性能。

           5. 因此，我们也使用第4.2节中的PASCAL标准[19]来评估我们在完整图像上训练的检测器。

           6. 除明确研究的参数外，其他参数均保持不变

           7. 默认情况下，共使用了8个通道，包括梯度幅度、灰度，以及6个没有预处理或后平滑的梯度直方图通道

           8. 随机生成5000个一阶特征(默认情况下不使用高阶特征)。我们用1000个深度2决策树对AdaBoost进行了训练。

           9. 注意，无论是特征表示还是学习算法，实际上都没有其他参数。

           10. 注意，无论是特征表示还是学习算法，实际上都没有其他参数负窗口是通过使用5000个随机负窗口训练默认分类器、引导5000个硬负窗口并第二次重复整个过程而生成的。

           11. 产生的15,000个阴性结果用于后续所有实验的训练。

               #### Channels and Features

               1. **Channels**:在图4(a)和图4(b)中，我们绘制了单独使用或联合使用的各种通道类型的性能
               2. 不出意料，信息量最大的通道是梯度直方图通道(Hist)，在参考点10^-4 fppw时检测性能达到87.2%。
               3. 这与参数设置为[5]的HOG分类器所实现的89%的分类结果相似，但略低于此。
               4. 直方图的bins在至少6个方向的情况下影响不大(图4(c))。
               5. 将Hist与梯度大小(梯度)和灰度信息(灰度)结合使用可将性能提高到89.4%(默认配置)。
               6. 然而，Gray本身并不能提供足够的信息，仅实现了30.7%。
               7. LUV在色彩空间中表现突出，单独占55.8%，结合Grad和Hist占91.9%。
               8. LUV+Grad+Hist使用的特征可视化如图3所示
               9. **Scale**:使用半径为1的二项滤波器($\sigma$ = 0.87)进行预平滑，可以将性能从89:4%提高到91:1%，使用半径越大，性能明显下降(图4(d))。后平滑对性能影响不大
               10. **Features**:使用高阶(随机生成)特征对性能的影响同样很小，只提高了检出率:比一阶特征高0.6%(图f(f)),因此，为了提高效率，一阶特性是首选的.
               11. 使用大量候选特征可以显著提高性能，其中3万个特征检测量达到91.8%(图4(g))。
               12. 使用更多特性的缺点是训练时间成比例地增加
               13. **Classifier**:增加弱分类器的数量可以将性能提高到大约1000(图4(h))，尽管对于较大的值，对分类器进行评估的时间会更长。
               14. 深度2树表现最好，树桩(深度1树)仅检测到83.2%(未显示结果)。
               15. boosting算法的选择(图4(i))对性能几乎没有影响，说明了整个框架的稳定性。

               #### Full Image Results

               1. 对于所有后续的实验，我们使用一个经过重新训练的分类器。
               2. 为了最大化性能，我们从上面的默认配置中更改了4个参数。
               3. 我们使用:(1)LUVcolor通道，(2)r = 1的预平滑，(3)2000个弱分类器，(4)30000个候选特征进行训练
               4. 生成的分类器达到约93%的检出率at10^-4 fppw,而且几乎90%在10^-5 fppw。
               5. 我们将得到的方法称为ChnFtrs
               6. **INRIA results**:虽然INRIA数据集上的结果通常报告的是裁剪后的阳性结果，但数据集也包含具有相同行人的完整图像，但在原始上下文中。
               7. Dollar等[1,9]使用这些图像和PASCAL标准评估了12种算法。
               8. 许多算法报告了出色的每窗口结果(超过95%的检测)，实际上是对边界效果的过度拟合，并且每幅图像的性能相当低(见[9])。
               9. 12种算法的逐幅图像结果以及所提方法(ChnFtrs)的结果如图5(a)所示。
               10. ChnFtrs每幅图像1个假阳性检出率为86%，HOG为77%
               11. 事实上，ChnFtrs匹配或优于除另一种方法([10])之外的所有已在完整图像上评估过的方法
               12. **Localization Accuracy**:通道特性的一个优点是可以使用小的步长d进行检测，而HOG窗口必须至少间隔d >= 8像素(或者在不同的偏移量下重新计算)。
               13. 直观地说，使用较小的d应该会带来更好的本地化。
               14. 为了测试这一点，我们重复了对INRIA数据集的评估，除了我们改变了PASCAL标准中的阈值，当ground truth和detection的交集面积超过70%(而不是50%)时，将一个检测计算为正确的。
               15. d为2、4、8的ChnFtrs结果如图5(a)所示，其他方法均为d >= 8。
               16. ChnFtrs在d = 2时的检出率为79%，比最接近的检出率高出近10%。
               17. **Caltech Pedestrians**:我们通过展示加州理工行人数据集[9]上的结果来得出结论，该数据集包含近50万个带标记的边框和带注释的遮挡信息
               18. 50像素及以上、未遮挡或部分遮挡行人的结果如图5(c)所示。
               19. 几乎所有显示的分类器都是在INRIA数据集上训练的，包括我们的，因此，结果是各种方法泛化能力的一个有用的度量。
               20. ChnFtrs显著优于所有其他方法，在1 fppi下的检出率接近60%(相比之下，包括HOG在内的其他方法的检出率为50%)。

           ### Conclusion

           1. 不同的、信息丰富的通道的组合，以及用于快速特征计算的积分图像技巧，为更广泛的一类非常有效的特征打开了大门:在这项工作中仔细检查的积分通道特征
           2. 正如我们所展示的，积分通道特征加上一个标准的增强算法优于现有的特征/行人检测方法。
           3. 最后，我们希望将这些结果扩展到其他对象类(特别是PASCAL VOC挑战)。
           4. 我们还想探索更多的家庭频道。

           

           

   

   ​                                                                                                                                                                                                              

   

