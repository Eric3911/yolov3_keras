# yolov3-keras-master

1、将标签全部放在Annotations下，图片放在JPEGImages下

2、运行test.py脚本生成ImageSets文件下Main里面四个文件

3、修改voc_annotation.py第七行里面内容为自己的类别标签同时在model_data里面修改voc_classes为自己类
（该过程要保证两个标签的顺序和空格不然导致inference过程没法正常运行）生成2007_train.txt/2007_val.txt/2007_test.txt
4、运行kmeans脚本生成自己数据的预设anchor

5、运行train.py为迁移学习训练自己数据，运行train_my.py为初始化训练自己的数据
	（如果迁移学习在train.py里面32行加载预训练权重这里我写好不要乱改）
6、cfg和train/train—my里面的修改
         cfg里面修改内容
         2/3行修改：含义为batch参数除以subdivisions等于train脚本里面batchsize（这是一个非常经典的训练测试）
7、测试修改yolo.py的216/217行执行脚本

![](https://github.com/Eric3911/yolov3-keras-master/blob/master/YOLOV3-2.png)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/yolo-v3-structure.jpg)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/figure_1_35000.png)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/beihang_airplane_PR.png)
其他相关教程

https://blog.csdn.net/maweifei/article/details/81204702
