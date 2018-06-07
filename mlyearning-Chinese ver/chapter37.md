## 37. 如何决定是否使用所有数据

假设你的猫咪检测器的训练集包含了 1 万张用户上传的图像。这些数据都是来自于和独立的开发/测试集相同的分布，同时代表的是你的算法想要表现良好的那种分布。你还有额外的 2 万张取自互联网的猫咪图片。你是否应该将 2万 + 1万 = 3万 这所有的图片作为你的训练集的数据？或者是放弃那 2 万张图片以防止你的学习算法出现偏差？

当使用早期的学习算法（比如手工设计计算机视觉特征，然后使用一个简单的线性分类器）时，合并这两种类型的数据导致性能更差的风险是存在的。因此，一些工程师会警告你不要把这来自网络的 2 万张图片包括进来。

但在当今这个强大、灵活的学习算法时代——比如大型神经网络——这种风险已经大大降低。如果你能负担得起用足够多的隐藏单元/层来构建一个神经网络，你就可以安全地将 2 万张图片添加到你的训练集中。

这种观察依赖于这样一个事实：存在 $x \rightarrow  y$ 的映射，对于来自不同分布的两种类型的数据都适用。换句话说，存在这样的一个系统，无论是输入来自互联网的图片还是输入用户上传的图片，它都能准确的预测出正确的标签来，即使不知道图像的来源。

添加额外的 2 万张图像会产生以下效果：

1. 它能为你的神经网络提供更多的例子说明猫是什么样子的。这很有帮助，因为互联网图片和用户上传的移动应用图片确实有一些相似之处。你的神经网络可以将从互联网图像中获得的一些知识应用到处理移动应用程序图像中来；
2. 它迫使神经网络分出一部分能力来学习特定于互联网图像的属性（例如分辨率较高，图像帧的不同分布等）。如果这些属性和移动应用程序中的图像差别很大的话，它将“消耗”掉一部分神经网络的性能。因此，从移动应用程序图像的分布中识别数据的能力就会降低——这是你真正关心的。理论上，这可能会影响算法的性能。

为了使用不同的术语来描述第二种效应，我们求助于虚拟人物夏洛克·福尔摩斯，他说你的大脑就像一个阁楼：它只有有限的空间。“每增加一点知识，你就会忘记一些你以前知道的东西。”因此，最重要的是，不要让无用的事实把有用的事实挤掉 [2]。

[2]：阿瑟·柯南·道尔的《血字的研究》

幸运的是，如果你有足够的计算能力来构建一个足够大的神经网络——即足够大的阁楼——那么这不是一个严重的问题。你有足够的能力同时从互联网和移动应用图片中学习，而不需要担心两种类型的数据争夺你的阁楼容量。你的算法的“大脑”足够大，就不必担心阁楼空间用完。

但是如果你没有足够大的神经网络（或者其他高度灵活的学习算法），那么你应该更加注意你的训练集和你的开发/测试集的分布问题。

如果你认为你所拥有的数据对提升算法表现没有任何好处，那么，你应该出于计算原因而忽略这些数据。例如，假设你的开发/测试集主要包含了人物、地点、地标和动物的随机图片，可能你还有大量扫描的历史文档。

这些图片不包含任何类似于猫的元素。它们看起来完全不同于你的开发/测试集。没有必要将这些图片归类到反例中，因为这些样本对于算法来说并不能体现出前边提到的第一个效果——几乎没有哪一个神经网络能够从这些样本中学习出用于你的开发/测试集分布的知识。同时它们还会浪费神经网络的计算资源和表示能力。