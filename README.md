# Daily Checkbox

2019.5.27
- [x] build visdom on maskrcnn
- [x] run evaluation on maskrcnn classification head
- [ ] migrate visdom to fanyi-dev
- [ ] think about idea and reply all the ideas for fanyi and weixin

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



# Mistakes
能不能不要再犯这种错误了，真的影响实验进度。。。。。。。。。。。

1. 不知道第几次忘记pytorch normaliza之后会把0-255直接归一化。
2. 每次写完loader一定一定要在feed进网络之前再viusalize一次！！！！！！
3. evaluation把random crop关掉。。。。。。。。。
4. 如果不是最终版本，改动一个东西的时候，要在前面加上 #XYZ TODO这样的标示，方便以后redo的时候搜索。



