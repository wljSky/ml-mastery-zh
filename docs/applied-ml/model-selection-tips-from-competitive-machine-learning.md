# 竞争机器学习的模型选择技巧

> 原文： [https://machinelearningmastery.com/model-selection-tips-from-competitive-machine-learning/](https://machinelearningmastery.com/model-selection-tips-from-competitive-machine-learning/)

在[对您的问题进行抽样检查算法](http://machinelearningmastery.com/why-you-should-be-spot-checking-algorithms-on-your-machine-learning-problems/ "Why you should be Spot-Checking Algorithms on your Machine Learning Problems")并调整好几个之后，您最终需要选择一个或两个最佳模型来继续。

这个问题被称为模型选择，可能很烦人，因为您需要在给定不完整信息的情况下做出选择。这是您创建的[测试线束](http://machinelearningmastery.com/how-to-evaluate-machine-learning-algorithms/ "How to Evaluate Machine Learning Algorithms")和您选择的[测试选项](http://machinelearningmastery.com/how-to-choose-the-right-test-options-when-evaluating-machine-learning-algorithms/ "How To Choose The Right Test Options When Evaluating Machine Learning Algorithms")的关键所在。

在这篇文章中，您将发现模型选择的灵感来自于竞争机器学习，以及如何将这些技巧提升到更高水平并像其他任何复杂系统一样研究测试工具的想法。

[![Model Selection](img/5937b602f13b3f1fabf4294f941f6d75.jpg)](https://3qeqpr26caki16dnhd19sv6by6v-wpengine.netdna-ssl.com/wp-content/uploads/2014/10/Model-Selection.jpg)

型号选择
照片由 [tami.vroma](http://www.flickr.com/photos/32314864@N02/3253876458) 拍摄，部分版权所有

## 比赛中的模型选择

在机器学习竞赛中，您将获得一些数据样本，您需要从中构建模型。

您为不可见的测试数据集提交预测，并评估这些预测的一小部分，并在公共排行榜上报告准确性。在比赛结束时，您在比赛中的排名取决于您对完整测试数据集的预测。

在某些比赛中，您必须选择一组或两组预测（以及创建它们的模型），您认为这些预测代表您与最终排名的所有其他参与者竞争的最佳努力。选择要求您根据自己的测试工具的估计精度和公共排行榜单独报告的准确度来评估模型的准确性。

这是模型选择的问题，因为您的信息不完整而具有挑战性。更糟糕的是，公共排行榜和您自己的私人测试工具报告的准确性很可能不同意。您应该选择哪种模式，如何在这种不确定性下做出正确的决策？

## 避免过度拟合训练数据集

[Log0](http://www.kaggle.com/users/55046/log0) 在他的帖子“[如何在单打比赛](http://www.chioka.in/how-to-select-your-final-models-in-a-kaggle-competitio/)中选择你的最终模特”中探讨了这个问题。

他评论说他个人在以前的比赛中遇到了过度拟合训练数据集的问题，现在努力避免这个陷阱。竞赛中的症状是你在公共排行榜上排名很好，但是当最终分数被释放时，你的排名会落在私人排行榜上，通常很长。

他提供了许多建议，他建议可以帮助克服这个问题。

### 1.始终使用交叉验证

他评论说，单个验证数据集将对模型对未见数据的准确性给出不可靠的估计。一个小的验证数据集就是公共排行榜。

他建议在选择模型时始终使用交叉验证（CV）并遵循自己的CV估计精度，即使它可以是乐观的。

### 2.不要相信公共排行榜

公共排行榜非常令人分心。它向所有参与者展示了与其他人相比你有多好。除此之外，它充满了谎言。它不是对模型准确性的有意义的估计，实际上通常是对模型准确性的可怕估计。

Log0评论公共排行榜得分不稳定，特别是与您自己的离线CV测试工具相比时。他评论说，如果您的简历看起来不稳定，您可以增加折叠数量，如果运行缓慢，您可以对数据样本进行操作。

这些是不使用交叉验证的常见异议的好方法。

### 3.选择不同的型号

多样化。 Log0建议如果您能够选择两个或更多模型，那么您应该利用这个机会选择不同的模型子集。

他建议您按类型或方法对模型进行分组，并从每个组中选择最佳模型。从这个简短的列表中，您可以选择最终的型号。

他建议选择类似的模型意味着如果策略很差，那么模型会一起失败，让你失去一点。一个反驳的观点是，多样性是一种在您无法做出明确决定时使用的策略，而且倍增可以带来最大的回报。您需要仔细考虑您对模型的信任。

Log0还提醒选择健壮的模型，即它们本身不太可能过度拟合，例如大（多参数）模型。

## 坚固的测试线束的扩展

这是一个很棒的帖子和一些很棒的提示，但我认为你可以而且应该更进一步。

您可以像研究任何系统一样研究测试安全带的稳定性。

### 研究交叉验证线束的稳定性

您可以采用标准的稳健算法并评估交叉验证配置中折叠数的稳定性。每次交叉验证（CV）折叠执行30次重复，并重复CV折叠尺寸从1到10。绘制结果并考虑给定CV折叠数的扩散和CV折叠从1（您的基线）增加的准确度变化。

您可以使用给定CV折叠数上限/下限作为准确度的粗略不确定性。您还可以使用CV fold = 1与您选择的CV折叠之间的准确度差异来纠正乐观偏差。

### 研究数据样本的稳定性

采样时可以使用类似的技巧。抽样理论是一个庞大而复杂的主题。我们可以执行如上所述的类似过程，并获取给定大小的n样本并估计准确度，然后尝试不同大小的样本。

将结果绘制为方框图或类似图可以让您了解采样大小的稳定性（以及采样方法，如果您正在对类进行分层或重新平衡 - 您可能应该尝试这样做）。

### 小心

过度拟合潜伏在各地。

对CV参数或采样方法的研究正在使用所有可用数据。您正在了解给定标准算法在数据集上的稳定性，但您也在使用比用于评估模型的给定折叠或样本更多的数据来选择配置。这可能导致过度拟合。

然而，这可能是有用的和有价值的，你需要平衡过度拟合的真正问题，提高你对问题的理解。

## 摘要

在这篇文章中，您发现了在使用机器学习时选择最终模型时可以使用的三个技巧。这些提示对于竞争机器学习非常有用，也可用于数据分析和生产系统，其中来自少数选定模型的预测是整体组合的。

您还学习了如何扩展这些技巧，以及如何针对给定的机器学习问题研究测试工具的配置，就像您使用任何机器学习算法的参数一样。

通过示例数据深入了解问题的稳定性，可以让您深入了解模型对未见数据的预期准确性。