# Merkel_tree
实现merkel树
Merkle树看起来非常像二叉树，其叶子节点上的值通常为数据块的哈希值，而非叶子节点上的值，所以有时候Merkle tree也表示为Hash tree，如下图所示：



![image](https://user-images.githubusercontent.com/75195549/180139360-4bda80e1-2a58-4fe3-9689-79cd79f59e0e.png)



构造Merkle tree时：



（1）对data blocks分别计算哈希值（sha256等算法）；


（2）每层两两计算获得hash值


（3）直至计算至最上一层，得到proof。

proof可以用来检验数据的完整性和正确性，即一个data block的改动或缺失，就会导致proof的改变。




在此实现了python版本和C++版本
C++版本中，使用一维数组代表merkle树，数组元素为我们的自写结构体，其中包含左右子树以及父节点的引用标号、Hash值、节点深度等变量。我们依次按照此种顺序将Hash值写入对应数组元素，并设置其高度（根据每次轮回不同，节点高度应对应增加）、子树节点以及父节点等。倘若该层节点不足以两两分完，则将最后一个节点记录下来，并以它为头节点对应的树上的所有节点高度均加一，作为下一层节点进行，此处是为了符合RFC6962要求。
待所有节点均被设置，Merkle树创建完毕。

随后我们进行验证，证明4在树中而9.5不在树中



如图所示：



![image](https://user-images.githubusercontent.com/75195549/180652290-0917e5e1-1791-415c-9896-0e2b1c8a1170.png)



