# Thinking-About-Work-and-Learning
1. 目前的深度学习－CV方面大多基于分类的结果进行优化的，但分类还面临着许多问题：细分类，多标签分类，等等。
2. 目前在别人的算法(Siamese with Contrast Loss or TripletLoss or Margin-based Loss using different sampling method)基础上，我已经能将Image Retrieval在DeepFashion中Inshop Top10的mAP和mRecall刷到：0.705846784490908， 0.354670454753284
    
    但其局限性还是很大，如单品搜索效果不错，但多物体就应该会出现大问题，比如一个搜索项同时有上装，下装，鞋子，怎么办？
    
    工程上当然会说让用户画框，然后进行搜索，诚然这样可以避开这个问题，但和其他备选项作对比（正好备选项也是多物体）时怎么办？ 也许会说那对备选多生成几个特征，但世界上这么多标签，我们很难完备地列出所有标签，而且标签重叠也是一个问题，此时的问题便是1中所说。
3. 目前在ImageNet, COCO, VOC等上分类刷出来的模型都是基于这几个数据集的，其分类还比较粗糙，而且Supervised Learning其假设便是训练和测试来自同一分步，所以他们也只是在这一分步上效果不错，但到细分类就得有新突破才行。

    好比：
    * 用A方法学习了一个一次function（一种分步），训练范围在[-100, 100], 那么此方法在这个function上其他区间推断应该是不会有问题的，当然Fine-Tune到其他一次func应该也可以
    * 用B方法学习了一个二次function（另一种分步），训练范围在[-100, 100], 那么此方法在这个function上其他区间推断应该是不会有问题的
    
    其实个人认为，他们都在各自的分步上做了过拟合，只能说有对应的分步上做Inference会有预期的效果，所以我觉得过拟合是相对的，世界那么多分步，我们很难穷尽，即使用GMM，也只是考虑了有限的高斯分步，这些分步可以类比刚刚说的ImageNet, COCO, VOC等。

所以出路在哪里呢？我想到的Unsupervised Learning, Reinforce Learning，以及基于非神经网络的模型。
目前神经网络后传要求可导，但很多东西不在可导范围类，如果这方面有重大突破，那么又会有一新天地。

4. 另外关于Object Detection, 我接触过的有YOLO(1,2,3)，SSD，Faster RCNN

    这类方法都有一个共同点：下采样，然后预测bbox和类别，就精度而言，粗略可排序: Faster RCNN>SSD>YOLO，速度倒过来。

    但他们都会存在一个问题：因为进行了下采样，所以对小物体检测会有不同程度损失，SSD会好一些(因其作了Multi-scale)
