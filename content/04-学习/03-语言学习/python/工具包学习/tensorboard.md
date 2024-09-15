# 一、在相应的 python 环境下载 tensorboard
```python
pip install tensorboard
```
# 二、启动tensorBoard
## 本地启动 tensorboard
其中 directory_name 替换为保存数据的目录，默认logs
```python
tensorboard --logdir=<directory_name>
```

如果使用 pytorch_lghtning 的话，记录默认保存在 lightning_logs/version_\<num\>

```python
tensorboard --logdir=lightning_logs/version_1
```

## 在 jupyter 中使用、与 google colab 使用
参考[TensorBoard最全使用教程：看这篇就够了 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/471198169)