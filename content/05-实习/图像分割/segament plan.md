1. 把所有 patient 样本 label union 后查看范围
2. 确定 crop 的中心和范围进行 crop
3. 对样本 resize 时只对 z 方向做
4. 最后再 train 一遍