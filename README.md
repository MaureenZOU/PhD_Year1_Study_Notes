# 要养成的习惯
目前监测的事情：
- 在一个checkpoint结束之前不能玩手机（当你意识到这个事情的时候立刻放下）
- 在每次跑程序之前，double check parameter are all correct, 开始跑程序之后每几个小时check一次程序是否断掉了
- 吃饭控制食量，差不多饱了，放下筷子，扔掉


# Daily Checkbox
2019.6.23
- [ ] run masktrackrcnn
- [ ] implement share weight colorization videon-inst-seg
- [ ] 有时间读今年cvpr的paper，看oral的video

2019.6.11
- [ ] 把soft-encoding加到classification上，Finish implement shared weight colorization framework
- [ ] 把labelme挂到server上
- [ ] 把vision6装好
- [ ] 把老板的idea想清楚，交代清楚，并且和老板道歉，在implementation这件事情上并没有完全讲实话

2019.5.27
- [x] build visdom on maskrcnn
- [x] run evaluation on maskrcnn classification head
- [x] migrate visdom to fanyi-dev

2019.5.23
- [x] Build classification branch on mask head
- [ ] Build visdom on maskrcnn

2019.5.22
- [x] Set up a more convient IDE
- [ ] Going back to maskrcnn code to go through every detail
0. - [x] Pytorch Distributed
1. what configuration does it take
2. train/test entry, engine, dataloader, main framework, loss
3. for each detail, try to understand why maskrcnn use that.

# Sui Sui Nian
0. 没有做soft-encoding的classification没有mse结果好 （为什么？）
1. Gray scale Augmentation, 对实验结果没有影响

# Mistakes
能不能不要再犯这种错误了，真的影响实验进度。。。。。。。。。。。

1. 不知道第几次忘记pytorch normaliza之后会把0-255直接归一化。
2. 每次写完loader一定一定要在feed进网络之前再viusalize一次！！！！！！
3. evaluation把random crop关掉。。。。。。。。。
4. 如果不是最终版本，改动一个东西的时候，要在前面加上 #XYZ TODO这样的标示，方便以后redo的时候搜索。
5. 每次实验之后一定要养成良好的记录习惯，不要怕浪费时间。（开一个google sheet记录实验结果）



