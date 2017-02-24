# "Region-based Convolutional Networks for Accurate Obeject Detection and Segmentation"

## *Ӧ�������嶨λ��ʶ��

## ժҪ
---
������ʷԭ��Ŀǰ����ʶ���㷨��PASCAL VOC�����ϵ����ñ��־�Դ����ʹ���ɶ��ֵͼ�ͼ����������ɵĸ��Ӽ��ϵͳ��
�ڱ�ƪ�����У��������һ�ּ���ͨ�õ�ʶ���㷨�����ڸĽ�ʶ���mean average precision(mAP)��
���ǵ���������������������ɣ�

1. ����ʹ�þ���������Ե����ϵؽ���������������Ŀ��Ķ�λ�ͷָ��
(one can apply high-capacity convolutional networks(CNN) to bottom-up region proposals in order to localize and segment obejcts)

2. **��ʹ���ض���ѵ����ѵ����������ʶ������������Ծ���ķָλ�������fine-tune, ���Ի��������Ч������(when labeled training data are scarce,supervised pre-training for an auxilliary task, followed by domain-specific fine-tune,boosts performance significantly)**
---

## 1.���ĵ���Ҫ���ף�
---
- ��ͼ����಻ͬ�������Ҫ����Ķ�λ��Ϣ��һ����Ч�������ǰ�ͼ���⵱��һ���ع�����(regression problem)�����ǣ������ķ���������Ч�ؼ�⵽�������壬����ʶ��������ʱ����Ҫ���ӵĶ��ⶨλ����������һ�������ǽ������������(sliding-window detector)������������ڽ���ʮ���ڶ��Ǳ���������������������������֡����˼�⣬���ַ�������Ч�ʽϸߣ���������Ҫ���Ŀ�������ͬ�ĳ����(aspect ratio)��������������ʹ�û��ģ��(mixture model)�����������

- ����ʹ�á�����ʶ�𡱷���(recognition using regions)�������λ���⡣��ʶ������У�����������2000���໥�����Ŀ�������(region proposals),Ȼ��ʹ������SVMs���з��ࡣ����ʹ��ͼ�����ż���(anisotropic image scaling)�������뵽CNN�е�ͼ��̶�����ͬ�ߴ硣

- ���Ľ���ĵڶ�������������fine_tune���ж�λЧ����������һ���̵Ľ���
![rcnn_algorithm](../images/rcnn.jpg)

## 2.��ع���
---
- Deep CNNs for object detection.
- Scalbility and speed.
- Localization methods.
- Transfer learning.
- R-CNN extensions.

## 3.ģ�����

---
### 3.1 Module design

- Ϊ�˼��������������������Ҫ����CNN����ݷ������������������ʹ�þ��ο�Ŀ������������һ����һ���ĳ���
In order to compute features for a region proposal, we must first convert the image data in that region into a form that is compatibel with the CNN,
its architecture requires inputs of a fixed S * S pixel size, we warp all pixels in a tight bounding box around it to the requires size.
- 


### 3.2 Test-time detection

- ����ʹ��ǰ����������2000������������ȡ���������ÿһ����ͼ������ʹ��SVM�������������ɵ�����ѵ���б�ģ�ͣ��������ʹ�÷Ǽ���ֵ���ƻ����ѽ�������ѡ��
We warp each proposal and forward propagate it through the CNN in order to compute features.Then, for each class, we score each extracted feature vector using the SVM trained for that class.Given all scored regions in an images, we apply a greedy non-maximum suppression that rejects a region if it has an intersection-over-union overlap with a higher scoring selected region larger than a learned threshold.

- ʹ��RCNN���ж�λʶ�����������¼������� 

1. ���������������������繲��ͬһ�ײ��� all CNN parameters are shared across all categories
2. ʹ��CNN�õ�������������������õ�������Ⱦ��и��͵�ά�� Second the feature vectors computed by the CNN are low-dimensional when compared to other common approaches.
3. �ڵ�ǰϵͳ����Ҫ���ĵĲ����� SVMȨ�� �Լ� �Ǽ���ֵ����, ���� CNN���ɵ���������Ϊ 2000 * 4096 �� SVM Ȩ�ؾ���Ϊ 4096 * N��NΪ��λ����������
  ����ָ����RCNN����ʶ�����ǧ������(analysis shows that R-CNNs can scale to thousands of object classed without resorting to approximate thechniques.)


### 3.3 Trainning 
1. Supervised pre-training
- ����ʹ��ILSVRC2012������ս�����ݽ���Ԥѵ����

2. Domain-specific fine-tuning 
- Ϊ�˽�CNNCӦ�õ�detection�����У�������Ԥѵ�����������ϣ�����Ŀ���warped region proposals��ʹ������ݶ��½�������������Ĳ��������˽�ImageNet 1000�����softmax���滻�������ʼ���ģ�N+1������㣬����������Ľṹ���䡣������VOC��N=20������ILSVRC2013��N=200��
- ��ѵ�������У����ǽ���Ŀ��������0.5����IoU��������Ϊ����������������ʶΪ��������
- SGD��ѧϰ��Ϊ0.001����ÿһ��SGD���������У�����32����������96������������������128��������mini-batch���������ű�������Ϊ��Ч����������ԶС�ڱ�����������ģ������VGG���磬��������������϶࣬���û���ϴ󣬿��ʵ�����mini-batch�ĸ���

## 4.����
---

## 5.ILSVRC2013 DETECTION DATASET
---

### 5.3 ������
![rcnn_algorithm](../images/table.jpg)

## 6 SEMANTIC SEGMENTATION
- �������CPMC����ʹ�������ֲ��ԣ�
1. ��һ�ֲ��ԣ�����������״��ֱ�Ӹ����α����������CNN����������������������ڷǾ�������
2. �ڶ��ֲ��ԣ����������ǰ����Ĥ����CNN���������ǽ����������滻��Ԥ�ȼ���õľ�ֵ�������ڽ����˾�ֵ��һ���󣬱�����ֵΪ0��(background regions are zero after mean subtraction)
3. �����ֲ��ԣ�����˵�һ�ֺ͵ڶ��ֲ��ԡ�

## 7 ʵ��ϸ��
