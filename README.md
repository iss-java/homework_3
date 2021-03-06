# 基于Shazam算法的听歌识曲小程序

程序有两个入口，一个是MusicArchiver，一个是MusicSearcher。目前只能处理PCM WAV，16-bit，单声道，44100Hz的音频，不能访问麦克风，也不支持其他格式的音频。我有一个已经转好格式的乐库，共197首歌，百度云[训练集和测试集音乐 提取码4zk2](http://pan.baidu.com/s/1qXYTDGo#list/path=%2F%E9%9F%B3%E4%B9%90%E5%BA%93)

## 团队分数【15分】
1. 有的人并没有按照要求把团队成员信息写在项目根目录里，而是写在网页里。这种情况要扣【2分】。
2. 出现音频等大文件，扣【2分】。
3. 程序的入口不清晰，没有必要的说明【2分】
4. 没有.gitignore文件，扣【2分】
5. git根目录不是intellij/eclipse项目的根目录，扣【2分】
6. 没有效果截图，扣【5分】
7. commit记录里只能看到一个人，则其他人不给团队分。

## 音频读取 【25分】
1. 读取的波形和Matlab的波形是一致的 【10分】如果多出或者缺少一小段，扣【3分】
2. 能对不符合格式的音频进行排除【5分】比如说，读到不符要求的音频会抛exception。
3. 解析文件头的代码简洁清晰【5分】，很罗嗦的要酌情扣分。
4. 位运算【5分】

## 指纹提取 【25分】
1. 把时间序列按4096byte分成一个个帧【5分】
2. 每帧提取N个最值【10分】；如果没有舍掉低频部分（0-55hz，除以11就是傅里叶数组的下标）和高频部分（11000hz以上），要【扣3分】。对于使用N最值的同学，如果random-select实现有误，【扣3分】。
3. 实现组合哈希的生成，并用合适的数据结构存储组合哈希【5分】
4. 把f1、f2和dt压缩成一个int类型的hash_id【5分】

## 指纹存储 【25分】
1. 有sql表结构转储【10分】
2. 使用jdbc执行select now()并截图【5分】
3. 预防sql注入攻击，对单、双引号等字符进行转义【5分】
4. 把f1、f2、dt压缩成一个int类型的hash_id【5分】

## 匹配打分 【25分】
1. 调用数据库查询指纹出现在哪些歌曲【5分】
2. 在第一条中，对重复的hash_id/finger_id只查询一次【5分】
3. 用合适的数据结构存储指纹在每首歌出现的次数【5分】，太臃肿的数据结构要酌情扣分。
4. 在每首歌中，对匹配的指纹，求出时间差，对时间差做直方图【5分】，算直方图的算法如果太繁琐要酌情扣分。
5. 对每首歌的打分进行降序排序并输出排名【5分】。
