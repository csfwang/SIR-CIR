
训练方法：
1. 将SCIR_triplet_net.prototxt（或SCIR_pairwise_net.prototxt）的第10行source改为数据集图像的根目录，第11行image_files改为训练图像的列表文件
2. 将SCIR_triplet_solver.prototxt（或SCIR_pairwise_solver.prototxt）的第17行loss_file改为记录每次迭代损失函数值的文件名，第18行改为记录训练过程中间结果网络参数的文件名前缀
3. 运行SCIR_triplet_train.sh（或SCIR_pairwise_train.sh）

测试方法：
1. 首先对probe set和gallery set建立lmdb
2. SCIR_triplet_test_solver.prototxt（或SCIR_pairwise_test_solver.prototxt）的第2行改为probe image个数
3. SCIR_triplet_test_net.prototxt的第32行改为probe set的lmdb位置，第48行改为gallery set的lmdb位置，第50行改为gallery image个数
4. SCIR_triplet_test.sh（或SCIR_pairwise_test.sh）第5行改为网络参数的snapshot文件
5. 运行SCIR_triplet_test.sh（或SCIR_pairwise_test.sh）
6. 测试以后在config目录下会生成cost3.txt和cost4.txt（pairwise模型是lossSI.txt和cost4.txt），cost3.txt（或lossSI.txt）是single-image representation的distance matrix，cost4.txt是cross-image representation的loss matrix
7. 在matlab下运行testmatching(SIRfile,CIRfile,probelabel,gallerylabel,setting)得到matching accuracy，SIRfile是cost3.txt（或lossSI.txt）的路径，CIRfile是cost4.txt的路径，probelabel和gallerylabel分别是probe image和gallery image的label，setting是'singleshot'或者'multishot'