# AICloth

《AI时代的数字衣物》

#目标

从1衣物点云，2.RGB图像（有人或无人,视频）
其他任务：4.衣物动态的快速物理仿真  5.衣物模型的快速生成

难点：衣物本身薄壳结构难以MVS重建，复杂形态，动态褶皱，样式众多

现有衣物建模流程：1.Blender 2.MarvolousDesigner

专业研究团队：
1.上科 2.港中文 3.Style3D

#算法：

0.暴力求解
  1.直接用CNN提取特征，PointNet等提取特征，通过GCN来糅合特征进行生成
  2.DeepFashion3D通过定义“特征线”来降低这个求解难度

1.衣物点云
考虑只有衣物的点云
可以用PointNet，对衣物进行参数化《NeuralTailor》

2.RGB图像
目标是代替昂贵的三维扫描仪
RGB图像进行分类：1.单纯衣物专业图片 2.包含人体的自然图片
通过隐式重建方法《PIFU》等，或是进一步结合SMPL先验《ARCH》《Icon》《PAMIR》等
先导技术是：人体姿态检测

nerf效果有很好的重建效果
《HumanNerf》 但是如何从Nerf中将3D模型提取出来？

思路：对Nerf进行模型抽取

人体扫描模型
##网格分割（Mesh Segmentation）
《ClothCap》：通过MRF方法对扫描模型进行顶点分割抽取出其中衣物模型
《IPNet》(MPI_meshRegister,RVH_MeshRegister)通过扫描模型进行SMPL配准
其他网格分割方法：CoSeg等
##

4.衣物动态的快速物理仿真
  1.对于Tshirt等简单衣物，用PCA进行降维来学习即可
  2.《TailorNet》

5.衣物模型的快速生成
  1.用GCN学习衣物网格特征

数据集:
《MGN》数据集,数量较少，有质量比较好的扫描模型，并且扫描模型经过SMPL配准，UV图也规整
《Cloth3D》大型数据集，包含大量生成衣物模型
《DeepFashion3D》大型数据集，包含大量衣物扫描模型
