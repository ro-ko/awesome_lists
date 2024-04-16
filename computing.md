## GPU Comparisons

### Contents
1. My lab's computing setup; [link](#computing-setup-of-my-lab)
2. Cloud GPU and whole machine price comparison and notes (Price comparison between cloud GPU and complete machine); [link](#price-comparison)
3. Free compute available from companies（Free computing resources that professors can apply for）; [link](#free-stuff)
4. Useful learning material on GPUs and setting up your clusters（How to build a computing cluster）; [link](#learning-stuff)

## Computing Setup of My Lab

In my lab, the [Precognition Lab](http://precognition.team/), using the start-up funds provided by the university, I have built 9 stand-alone machines equipped with a total of 32 RTX 3090/4090 GPUs (including 4-GPU and some 2-GPU machines). Additionally, I have established a cluster with 3 compute nodes, comprising a total of 24 RTX A6000 GPUs, and a 100TB NAS.

The rationale behind this hybrid setup is twofold: the stand-alone machines cost only 40% of what the cluster does, and they can be acquired quickly without necessitating additional machine room space.

As for the cluster, I've found that a 100 GB Ethernet suffices for the computing network, eliminating the need to invest in an Infiniband switch, which can cost two to three times more. With 3 nodes on this network, I can essentially achieve linear scaling with multi-node training (6 hours for 1-node training and 2 hours for 3-node training, etc.).


## Price Comparison

Vendors in mainland, China (Updated 07/2022):

|          | Machine          | Duration           | Price (RMB)         | Note                        |
|----------|---------------|----------------|----------------|------------------------------------------------|
| 阿里     | 8xV100 (16GB) | 一年           | 80万           | 只有CentOS                                     |
|          |               | 一个月         | 7.1万          |                                                |
|          |               | 一小时         |         248.42 |                                                |
| 华为云   | 8xV100 (32GB) | 一年           | 63万           |                                                |
|          |               | 一个月         | 6.3万          |                                                |
|          |               | 一小时         |          131.5 |                                                |
| 腾讯云   | 8xV100 (32GB) | 一年           | 45.8万(8.3折)  |  [link](https://cloud.tencent.com/document/product/560/8025) |
|          |               | 一个月         | 4.6万          |                                                |
|          |               | 一小时 (TIONE) |            147 |                                                |
|          | 8xA100 (40GB) | 一年           | 113.5万(8.3折) |                                                |
|          |               | 一个月         | 11.4万         |                                                |
| 百度云   | 8xA100 (40GB) | 一年           | 99.7万(8.3折)  | [link](https://cloud.baidu.com/product-price/gpu.html) |
|          |               | 一个月         | 10万           |                                                |
|          | 8xV100 (32GB) | 一年           | 59.3万         |                                                |
|          |               | 一个月         | 5.9万          |                                                |
|          |               | 一小时         |         124.14 |                                                |
| 矩池云   | 8xV100 (16GB) | 一小时         |             48 |                                                |
| 智星云   | 8x3090 (24GB) | 一个月         | 2.1万          |                                                |
|          |               | 一小时         |             36 |                                                |
|          | 8xA100 (40GB) | 一个月         | 4.5万          |                                                |
|          |               | 一小时         |             76 |                                                |
|          | 8xV100 (32GB) | 一个月         | 2.8万          |                                                |
|          |               | 一小时         |             48 |                                                |
| 极链AI云 |               |                |                |                                                |
| 恒源云   |               |                |                |                                                |
| AutoDL   |               |                |                |                          [link](https://www.autodl.com/) , Most Popular                      |
| OpenBayes |               |               |                 |                 [link](https://openbayes.com/)         |


Complete machine purchase (08/2022 consultation)

|               | machine   |            |
|---------------|--------|------------|
| dbcloud deep brain cloud (Taobao) | 8x3090 | Starting from around 200,000 |
|Professor Cheng Mingming’s experience|8xV100| [link](https://mmcheng.net/dlm/)|

**Junwei: GPU prices have plummeted recently (09/2022). It is obviously more cost-effective to buy a complete machine, and the computing power of 3090 is equivalent to V100, which is the most cost-effective card, so I think multiple 8x3090 complete machines + network hard disk NAS +kubeflow is the most cost-effective and scalable setting. You can refer to [below](#learning-stuff) on how to build your own computing cluster. **

Vendors in NA (Updated 07/2022):

|                          | Machine             | Duration            | Price        |
|--------------------------|------------------|-----------------|-------------|
| Google Cloud asia-Taiwan | 8xV100 (32GB)    | 1 month          | $12,837.30  |
|                          |                  | 1 hour          |        $17  |
| Google Cloud asia-Tokyo  | 8xA100 (40GB)    | 1 month          | $18,216.98  |
| vast.ai NA               | 8xV100 (16GB)    | 1 hour          |      $2.80  |
|                          | 8xA100 (40GB)    | 1 hour         |      $8.80  |
|                          | 8xA6000 (48GB)   | 1 hour         |      $4.40  |
|                          | 10x1080Ti (11GB) | 1 hour         |         $2  |
|                          | 8xA5000 (24GB)   | 1 hour          |      $2.40  |
|                          | 4x3090 (24GB)    | 1 hour          |      $1.20  |
| lambda NA                | 8xV100 (16GB)    | 1 hour         |      $4.40  |
|                          | 8xV100 (16GB)    | 1 hour (>3 months) |      $3.20  |
|                          | 8xA100 (40GB)    | 1 hour (>3 months) |      $8.00  |
|                          | 1xA100 (40GB)    | 1 hour |      $1.10 [link](https://www.youtube.com/watch?v=tWVq4GxSCps)  |

## Free Stuff


|              | note                                                                   | link                                                                                                                                                                                                                                                                                                                                                              |
|--------------|------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Magic Square AI       | Wanka’s computing power, free application, a fun summer of scientific research                                     | [link](https://mp.weixin.qq.com/s?__biz=Mzk0MjE3MzQ5Mg==&mid=2247484702&idx=1&sn=5157e2c6564c41171ad7973f861e3a12&chksm=c2c67945f5b1f053a997f8213dee6284e9c1ecedaf13fd4f6165a6aaea77eee92ed3320da163&mpshare=1&scene=1&srcid=0715juU6U4wioPfFdA6loJQX&sharer_sharetime=1660101801014&sharer_shareid=c5b6fadc801a2c4ecd6ca0096153aea4&version=4.0.9.99149&platform=mac#rd) |
| NVIDIA       | Funding projects with a free card                                                 |                                                                                                                                                                                                                                                                                                                                                                   |
| AWS          | When taking classes at CMU, professors of each course can apply for cloud credit of about $100 for each student. |                                                                                                                                                                                                                                                                                                                                                                   |
| Google Cloud | Similar to AWS                                                                |                                                                                                                                                                                                                                                                                                                                                                   |

## Learning Stuff

| note                     | link                                                |
|--------------------------|-----------------------------------------------------|
| GPU guide from Lambda    | [link](https://lambdalabs.com/blog/best-gpu-2022-sofar/)    |
| understanding GPU and DL | [link](https://horace.io/brrr_intro.html)                   |
| Tencent TEG Stars and Wit Team    | [link](https://cloud.tencent.com/developer/article/1500001) |
| MPIJob                   | [link](https://github.com/kubeflow/mpi-operator)            |
| Machine learning platform             | [link](https://aijishu.com/a/1060000000136087)              |
| Cluster hard drive，ceph cluster   | [link](https://www.45drives.com/products/cluster/)          |
| A discussion on machine price on Twitter (for NA)   | [link](https://twitter.com/WenhuChen/status/1565083349911326720)       |
| A discussion on 1xA100 vs 6x3090 Know almost   | [link](https://www.zhihu.com/question/551536415/answer/2657911978)       |
|Professor Cheng Mingming’s GPU cluster experience|[link](https://mmcheng.net/servers/)|
|Good cluster building guide from Lambda| [link](https://www.youtube.com/watch?v=rfu5FwncZ6s)|
|How to decide on cloud GPUs vs. on-perm vs. hybrid| [link](https://www.youtube.com/watch?v=3EnIW0EZkr4)|

