# yolov3-keras-master

# 使用yolov3-keras训练voc风格的自己数据集

环境要求：
	
	 pip/conda install tensorflow/tensroflow-gpu==1.10.0 /1.12.0

	 pip/conda install keras
	 
	 pip/conda install opencv-python

1、将所有的标签数据全部放在Annotations下，图片数据集放在JPEGImages下。

2、运行test.py脚本生成ImageSets文件下Main里面四个txt文件。

3、修改voc_annotation.py第7行里面内容为自己的类别标签同时在model_data里面修改voc_classes内容为自己类别标签，
（该过程要保证两个标签的顺序和空格不然导致inference过程没法正常运行）运行voc_annotation.py生成2007_train.txt/2007_val.txt/2007_test.txt

4、运行kmeans脚本生成自己数据的预设anchor，根目标下生成自己数据的yolo_anchorers将该文件放到model_data目录下取代原有的。

5、运行train.py为迁移学习训练自己数据，运行train_my.py为初始化训练自己的数据。（如果迁移学习在train.py里面32行加载预训练权重这里我写好不要乱改）
	
6、cfg和train/train—my里面的修改：
         cfg里面修改内容
         2/3行修改：含义为batch参数除以subdivisions等于train脚本里面batchsize（这是一个非常经典的训练测试）
	 类别classes：607/693/783/行为类别数目
	 filters = 3*（5+classses）
	 
7、测试修改yolo.py的216/217行执行脚本。

8、相关参数解释:

https://github.com/Eric3911/Dakrnet-YOLOv3/blob/master/%E4%BC%98%E5%8C%96%E8%AE%AD%E7%BB%83%E5%8F%82%E6%95%B0%E8%A7%A3%E9%87%8A

模型结构图

![](https://github.com/Eric3911/yolov3-keras-master/blob/master/YOLOV3-2.png)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/yolo-v3-structure.jpg)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/figure_1_35000.png)
![](https://github.com/Eric3911/yolov3-keras-master/blob/master/yolov3-farmwork.png)
我们论文跑的结果

![](https://github.com/Eric3911/yolov3-keras-master/blob/master/beihang_airplane_PR.png)
![](https://github.com/Eric3911/image/blob/master/QQ%E6%88%AA%E5%9B%BE20190425164616.jpg)


1、 In this version
we found that the error of Val = 0 occurred in the code during our training process, which made it impossible to train.

issue: The error code fragment in the train_Mobilenet.py script is as follows：

with open(train_path) as t_f:
    	t_lines = t_f.readlines()
	np.random.seed(10101)
np.random.shuffle(t_lines)
	np.random.seed(None)
	v_lines = t_lines[700:]
	t_lines = t_lines[:700]
	num_train = len(t_lines)
Exchange: We modified the code to be trained as follows：

 with open(train_path) as t_f:
   	 	t_lines = t_f.readlines()
     random_stat = 123
     np.random.seed(random_stat)
   	 t_lines, v_lines = train_test_split(t_lines, 
 				     test_size=0.2,
				     random_state=random_stat)
     num_train = len(t_lines)
2、Practical steps of using transfer learning training model:
DataSet VOC2007
A) Put all the label XML of training data in Annotations;
B) Put all the labeled training pictures in JPEG Images;
3、creat_list.py
C) Use the creat_list.py script under VOC2007 to generate four new documents in Main under ImageSets;
train.txt
test.txt
val.txt
4、voc_annotation.py
D) Write the class parameters in the sixth line of the voc_annotation.py script under the root directory as their own class parameters in ["aircraft"];
E) Run the voc_annotation.py script code to generate three files in the root directory: 
2007_test; 
2007_train;
2007_val;
F) Modify the class label in voc_classes under model_data directory, where the order must always be and must be the same as that in classes, including the space placeholders between some label words.
5、kmeans.py
G) Run the kmeans script to generate new yolo_anchors and copy them to the model_data directory to overwrite the previous yolo_anchors;
6、yolov3.cfg
H) Modify yolov3.cfg, which is as common as other modifications.
7、training
I) Use the train_Mobilnet.py code to modify the path of its relevant parameters. Generally, at 21-24, 37, 68, 74, 75, 86, 92, 93 lines of code, the script model can be trained to execute.
8、test
python test.py
J) After the training, test.py is used to test the model and get the result.
9、Environment
Python 3.6.5
Keras 2.1.5
tensorflow 1.6.0
9、Citing
《YOLOv3-Mobilenet-update》 By Fangyu Zhou & Jungang An

10、Realtek

https://github.com/Eric3911/yolov3_darknet

https://github.com/Eric3911/yolov3_keras

https://github.com/Eric3911/YOLOv3-Mobilenet

https://github.com/dog-qiuqiu/Yolo-Fastest

https://github.com/dog-qiuqiu/MobileNet-Yolo


其他相关教程

https://blog.csdn.net/maweifei/article/details/81204702
