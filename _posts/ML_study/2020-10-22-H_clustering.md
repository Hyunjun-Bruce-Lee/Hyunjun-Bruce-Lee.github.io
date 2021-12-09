---
layout: post
title: H-clustering
description: Hierarchical clustering
image:
use_math: true
ml: True
---

#### H-clustering

> - Machine Learning (머신러닝)
> -  Unsupervised Learning (비 지도학습)
> - Clustering (군집화)



#### H-clustering의 특성	

> - Dendrogram을 이용한 사후 군집개수 설정
> - 단계적, 병합형 군집화



### H-Clustering의 작동 방식

H-Clustering은 데이터들간의 거리를 기준으로 순차적으로 데이터를 병합하며 군집화를 진행한다. 데이터가 최종적으로 하나의 군집에 속할 때까지 군집간 병합을 진행하여 Dendrogram을 전개한 후, 전개된 Dendrogram을 보고 최종 군집이 이루어질 단계를 정하게된다.

<center><img src="{{ "/images/H-Clustering_1.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

<center><img src="{{ "/assets/images/H-Clustering_2.PNG" | absolute_url }}" width = 'auto' height = 'auto' alt="" /></center>

&nbsp;

&nbsp;

### Practice (python)

[Blobs](https://github.com/Hyunjun-Bruce-Lee/ML_study/blob/master/H_clustering/HClust(blobs).py)

