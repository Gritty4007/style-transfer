CycleGAN：
首先你得去这个网站下载任何你想训练的数据集
https://people.eecs.berkeley.edu/~taesung_park/CycleGAN/datasets
然后你得将数据集划分成（以horse2zebra为例
/datasets/horse2zebra/trian/A
-----------------------  /train/B
-----------------------  /test/A
-----------------------  /test/B

当然你也可以更改训练目录为任何你想的目录
只需更改参数中的--dataroot

在本实验中你还可以通过添加--cuda参数来使用gpu训练
当然你如果有多块cpu线程也可以通过--n_cpu来更改
下面以使用默认数据目录以及gpu训练为例：
python train.py --cuda

当然如果你想直接使用训练好的模型训练
直接使用
python test.py
命令即可
但是你仍然需要在目录下创建/datasets/horse2zebra/test/A和/datasets/horse2zebra/test/B
当然也可以不是horse2zebra可以是vangoh2photo 但是这样你就需要更改dataroot中的路径
然后分别将output文件中的real_A.jpg和real_B.jpg分别放入A和B文件夹中。
最后你需要将你想训练的数据的output_XXXXXXX文件夹更名为output再进行训练即可。


CycleGAN-Plus:
这次的训练数据仍是在上述网站中下载，下载完成后放入目录./datasets/monet2photo
训练模型的命令：
python train.py --dataroot ./datasets/monet2photo --name monet2photo_cyclegan --model cycle_gan --netG resnet_fpn
这次你同样可以利用visdom来可视化训练过程：
运行python -m visdom.server并在浏览器中打开http://localhost:8097
而更多的训练结果也被保存在./checkpoint/monet2photo_cyclegan/web/index.html
测试数据时在https://drive.google.com/file/d/1M3uKI0PN6nelmbalgXBfoWDEV7CAnrL3/view?usp=sharing中下载模型，放入./checkpoint/monet2photo_pretrained/文件夹中
注意该预训练模型需下载monet2photo的数据
测试时使用命令
python test.py --dataroot datasets/monet2photo/testB --name monet2photo_pretrained --model test
结果会被保存在results文件夹中