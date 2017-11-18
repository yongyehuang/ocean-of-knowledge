## 1.[调参]AlexNet(等 CNN model) 调参过程中要注意什么？
> 在 github 上面有很多不同版本的 AlexNet，网络结构基本都是一样的，在官方的 tensorflow slim 框架中也提供了 alexnet-v2 版本。在我的任务中，发现 slim 版本的 alexnet 效果要比其他版本的好很多(2~4个百分点)。明明结构一样，为什么差别这么大。

A：虽然我觉得 slim 框架很不友好，但是里边的参数应该都是经过测试得到的较好的结果。很多小的细节都会影响最后的结果，具体要注意的有下面这些点：
- 初始化方式。在我的任务中，初始化方式影响很大。slim 中的每一层的初始化方式和 caffe 的版本中基本一致。包括 conv 层， fc 层的 weights, biases。我就是最后一个 fc 层改了一下初始化，loss 嗖嗖地就降了。
- 优化器。在原版中用的是 RMSProp 优化器，但坑的是用的不是默认参数，最好设置成跟 slim 一致。
- 数据预处理。我用 caffe 算出了整个数据集的均值，然后把原始图片[0.~255.]减去均值，效果还不错。
- lrn。在 slim 的 alexnet-v2 版本中去掉了局部响应层。结果没有变差，速度快了大概一倍吧。



## 2.[tensorflow]tensorflow 训练模型，报无法分配 memory，但是程序继续运行，这时运行的结果有问题吗？
>**ran out of memory trying to allocate 3.27GiB. The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory is available.** 这时候，使用 watch nvidia-smi 看显卡使用情况，就会发现使用率非常低。

A：这种情况下就应该把batch_size减小了！！！虽然程序还在运行，但是你会发现，结果根本不对，loss 根本就没降。这不是因为你的模型不好，学习率不对。把 batch_size 调小看看结果再下定论。


## 3.[github] github 怎么解决中文乱码问题？
> [git乱码解决方案汇总](https://blog.zengrong.net/post/1249.html)

- 在cygwin中，使用git add添加要提交的文件的时候，如果文件名是中文，会显示形如 274\232\350\256\256\346\200\273\347\273\223.png 的乱码。

解决方案：在 bash 提示符下输入：
```
git config --global core.quotepath false
```

- 在MsysGit中，使用git log显示提交的中文log乱码。

解决方案：
```
# 设置git gui的界面编码
git config –global gui.encoding utf-8

# 设置 commit log 提交时使用 utf-8 编码，可避免服务器上乱码，同时与linix上的提交保持一致！
git config –global i18n.commitencoding utf-8
```

- 我用 xftp 从 windows 下把文件传到 linux 后，在 linux 系统下直接显示的就是乱码，这是因为 windows 下使用的是 GBK 编码，我们需要把它转为 UTF-8 编码。可以使用 convmv 命令进行文件名的编码转换，而且可以使用 -r 直接把整个文件夹下的所有文件都改了：
```
convmv -f GBK -t UTF-8 --notest (-r) utf8编码的文件（夹）名
```

<center><img src="https://raw.githubusercontent.com/yongyehuang/ocean-of-knowledge/master/figs/convmv1.png"   width="80%"/>
fig1. 使用 convmv 转换中文文件名编码方式
</center>

## 4.tf.control_dependencies(control_inputs) 是什么用？
>control_inputs: A list of Operation or Tensor objects which must be executed or computed before running the operations defined in the context. Can also be None to clear the control dependencies. (control_inputs 是一个list，里边每个元素是一个 op。当执行定义在此 'context' 上下文 中的操作时，必须先执行 control_inputs 的所有操作。)
>以我的经验，在 batch normalization 更新 lambda 和 beta； center loss 中更新 centers 都可以使用这种操作，如下：
```python 
with tf.control_dependencies([centers_update_op]):
    train_op = optimizer.minimize(total_loss, global_step=global_step)
```




