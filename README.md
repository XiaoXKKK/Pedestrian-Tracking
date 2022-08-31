学习MOT

- Yolov7+StrongSORT+OSnet cuda跑通
- webcam

### 实习工作总结
1. 时间安排
7.18 - 7.24 MOT相关知识学习  
7.25 - 7.31 几个小demo试验、PPT准备  
8.1  - 8.7  调研内容分享，环境准备  
8.8  - 8.17 代码实现与调试  
8.18 - 8.26 rgbd深度数据相关知识学习，代码实现（未完成）  

2. 工作总结

&emsp;&emsp;实习主要内容为行人的检测和跟踪项目研究。这是一个之前从未接触过的领域，我先对一些基础的知识进行了学习，主要参考了知乎上几位MOT研究方向大牛的调研总结。跟随发展历史将时间线上比较经典和著名的论文进行了下载阅读。  
&emsp;&emsp;在此基础上制作了调研ppt，在scrum meeting上进行了简单的分享。  
&emsp;&emsp;在实际功能实现上，最终延续调研时发现的当前主流实现方法，也就是two-stage 的 tracking-by-detection。采用由Yolov7（最新的一个Yolo原系列作者的项目,在COCO数据集上预训练的物体检测模型）产生的检测结果，将结果传递给StrongSORT，它结合了基于OSNet的运动和外观信息，来实现物体的追踪。在实现过程中遇到了许多bug，在到gpu环境的切换上也出现了一些问题，最终在查阅资料和提出issue寻求帮助解决了这些问题。最终结果在数据集上效果高于所有baseline方法，但在实际运行速度上仍较慢，实时检测可能有输出吞帧的情况。实际上整体流程不仅限于对行人的检测与跟踪，可对Yolo模型可检测出的任意物体进行跟踪。  
&emsp;&emsp;之后对加入一维深度数据进行了初步研究。对RGBD/TOF数据集上的一些项目进行了简单学习。由于时间关系未能完成最终的实现，目前处于了解数据导入和表示方式阶段。  
&emsp;&emsp;非常感谢思岚科技给予我这次宝贵的实习机会，也是我人生中第一段实习经历，了解了从面试到上岗的全流程。暑假中还有算法竞赛的训练，时间上较为紧张，没能参与和完成更多的内容。但这一段经历一定会成为我前进路上宝贵的财富。 
    
3. 代码清单及使用说明

    eval.sh 使用MOT16数据集对检测结果进行评估，直接运行使用  
    strong_sort tracking实现  
    yolov7 detection实现  
    requirements.txt 运行所需库  
    track.py 主函数，整体流程控制和命令行参数设置  
    --source 指定视频流，0为网络摄像头，或直接指定视频路径  
    --yolo-weights 改变yolo模型  
    --strong-sort-weights [改变reID模型](https://kaiyangzhou.github.io/deep-person-reid/MODEL_ZOO)  
    --classes 设置检测对象 0为行人  
    Golab.ipynb 在Golab上试验和评估代码  
