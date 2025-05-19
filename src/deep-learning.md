# 深度学习

## SPD-Conv

包含一个spd 空间到通道层 和 一个非步长卷积

## CSPNet

## VJ检测器

- 积分图像
- 特征选择
- 检测级联

## HOG算子

HOG(Histogram of oriented gradient) 方向梯度直方图

- 计算每个像素的梯度
- 同一个cell中梯度投票,得出向量-梯度直方图
- 一个block中包含2x2cell, 拼起来归一化(block滑动, 存在重叠的cell)

## R-CNN

- SS算法提取所有的object proposal,然后缩放到固定尺寸,传入一个CNN网络提取特征,再用一个线性SVM分类器判别

## SPPNet

- 提出SPP层(spatial pyramid pooling, 空间金字塔池化)
- 对不同尺寸的输入计算出固定尺寸的特征

## Fast R-CNN

- 对R-CNN和SPPNet的改进
- 同时训练检测器和边界框回归器
- 因为需要object proposal 速度慢

## Faster R-CNN

- 提出了RPN(Region Proposal Network), 加速了region proposal

## FPN

- 特征金字塔

## two-stage vs one-stage

two-stage 精度高,但是速度慢

## YOLO

## SSD

- Single Shot MultiBox Detector

## RetinaNet
