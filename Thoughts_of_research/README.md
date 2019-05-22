# 改错本

### Video Instance Segmentation
1. 这次和fanyi试了两个idea, 一个是用bounding box去限制mask, 要求box内每一行，每一列都要有mask pixel, box外都是0, 这个constraint有很多trivial solution, converge的结果都是有格子的。
[]- 
