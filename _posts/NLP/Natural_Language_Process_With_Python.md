# PYTHON自然语言处理
---
## 软件安装需求
- python
- nltk
- nltk-data
- numpy
- matplotlib
- networkX
- prover9
## NLTK介绍
![](http://i.imgur.com/x0nL4S9.jpg)
## 第1章 语言处理与python
### 章节目的
1. 简单程序+大量文本能够实现什么?
2. 如何自动提取概括文本风格和内容的关键词和短语?
3. python编程语言为上述工作提供了哪些工具和技术?
4. 自然语言处理中有哪些有趣的挑战?
### 1.1 语言计算:文本和单词
  将选取一些语言相关的编程任务而不去解释它们是如何实现的.

- from nltk.book import *
	- 将加载几本书的内容
- (nltk.text.Text)text1.concordance(strToSearch)
	- 搜索文本
- text1.similar(strToSearch)
	- 词语索引(搜索词的上下文有哪些词)
- text1.common_contexts([word1,word2,...])
	- 研究两个词或以上共用的上下文
- text1.dispersion_plot([word1,word2...])
	- 绘制多个词的文件偏移的散点图
- len(text1)
	- 返回文本中单词数量
- text1.count(strToSearch)
	- 返回单词出现次数
### 1.2 近观python
   系统地回顾关键的编程概念
### 1.3 计算语言:简单的统计
- FreqDist
	- 初始化FreqDist(test1)
	- FreqDist.keys()
	- FreqDist.plot()
		- FreeDist.plot(50,cumulative=True)
			- 只选top50,累计频率图
	- FreqDist.hapaxes()
		- 低频词链表
	- ![](http://i.imgur.com/U4MrOUp.png)
- 词语搭配和双连词
	- bigrams(sent1)
	- text1.collocations()
### 1.5 自动理解自然语言
- 词意消歧
	- 关注上下文有助于自动消除歧义
- 检测主语和动词的宾语
	- 指代消解
		- 确定代词或名词短语指的是什么	
	- 语义角色标注
		- 确定名词短语如何与动词相关联
	- 先行词 
		- they的先行词thieves 或 paintings
- 自动生成语言
	- 自动问答
	- 机器学习
	- 弄清楚词的含义,动作的主语以及代词的先行词
- 机器翻译(MT)
	- 文本对齐
	- babelize_shell()
- 人机对话
	- nltk.chat.chatbots()
	- ![](http://i.imgur.com/A1Wrapt.png)
- 文本含义识别(Recognizing Textual Entailmant RTE)
	- 使用浅显但强大的技术代替无边无际的知识和推理能力
### 习题
- T15 sorted(w for w in set(text4) if w.startswith('b'))
- T17
    - text9[:].index('sunset')
	629
	- text9[630:].index('sunset')
	12
	...
- T20 
	'1'.islower() 
	True
# 2 获得文本语料库
## 2.1 获取文本语料库
### 古腾堡语料库
NLTK 包含古腾堡项目(Project Gutenberg)电子文本档案的经过挑选的一小部分文
本。该项目大约有 25,000(现在是 36,000 了)本免费电子图书,放在 
[http://www.gutenberg.
org/ ](http://www.gutenberg.
org/ ) 上。
```python
nltk.corpus.gutenberg.fileids()
gutenburg.words(fieild)#划分为词
gutenburg.sents(fieild)#划分为句
```
### 网络和聊天文本
NLTK 的网络文本小集合的内容包括 Firefox 交流论坛,在纽约无意听到的对话,
《加勒比海盗》的电影剧本,个人广告和葡萄酒的评论
```
nltk.corpus.webtext
```
即时消息聊天会话语料库,最初由美国海军研究生院为研究自动检测互联网幼童虐待癖而收集的。

这些帖子都已经被贴上 15种对话行为类型中的一种标签,例如:“陈述”,“情感”,“yn 问题”,“Continuer”。
```
nltk.corpus.nps_chat
```
### 布朗语料库
布朗语料库是第一个百万词级的英语电子语料库的,由布朗大学于 1961 年创建。这个
语料库包含 500 个不同来源的文本,按照文体分类,如:新闻、社论等

![image](https://github.com/xuesu/picture/blob/master/2016-08-22-192919_602x518_scrot.png?raw=true)

### 路透社语料库
路透社语料库包含 10,788 个新闻文档,共计 130 万字。这些文档分成 90 个主题,按照
“训练”和“测试”分为两组。因此,fileid 为“test/14826”的文档属于测试组。这样分割
是为了训练和测试算法的,这种算法自动检测文档的主题,

路透社语料库的类别是有互相重叠的,

语料库方法既接受单个的 fileid 也接受 fileids 列表作为参数
### 就职演说语料库
语料库实际上是 55个文本的集合,每个文本都是一个总统的演说。这个集合的一个有趣特性是它的时间维度
### 标注文本语料库
许多文本语料库都包含语言学标注,有词性标注、命名实体、句法结构、语义角色等。
NLTK 中提供了很方便的方式来访问这些语料库中的几个,还有一个包含语料库和语料样本
的数据包,用于教学和科研的话可以免费下载。表 2-2 列出了其中一些语料库。有关下载信
息请参阅 http://www.nltk.org/data。
### 其他语料库
![image](https://github.com/xuesu/picture/blob/master/2016-08-22-200746_686x254_scrot.png?raw=true)
![image](https://github.com/xuesu/picture/blob/master/2016-08-22-200756_712x589_scrot.png?raw=true)
### 载入自己的语料库
![image](https://github.com/xuesu/picture/blob/master/2016-08-22-201507_558x176_scrot.png?raw=true)
也可以使用BracketParseCorpusReader
## 2.2 条件频率分布
条件频率分布是频率分布的集合,每个频率分布有一个不同的“条件”。这个条件通常是文本的类别

ConditionalFreqDist

```
>>> cfd = nltk.ConditionalFreqDist(genre_word)
>>> cfd 
<ConditionalFreqDist with 2 conditions>
>>> cfd.conditions()
['news', 'romance'] 
让我们访问这两个条件,它们每一个都只是一个频率分布:
>>> cfd['news']
<FreqDist with 100554 outcomes>
>>> cfd['romance']
<FreqDist with 70022 outcomes>
>>> list(cfd['romance'])
[',', '.', 'the', 'and', 'to', 'a', 'of', '``', "''", 'was', 'I', 'in', 'he', 'had',
'?', 'her', 'that', 'it', 'his', 'she', 'with', 'you', 'for', 'at', 'He', 'on', 'him',
'said', '!', '--', 'be', 'as', ';', 'have', 'but', 'not', 'would', 'She', 'The', ...]
```

- 在 plot()和 tabulate()方法中,我们可以使用 conditions= parameter 来选择指定
哪些条件显示。如果我们忽略它,所有条件都会显示。
- 同样,我们可以使用 samples= parameter 来限制要显示的样本。这使得载入大量数据到一个条件频率分布,然后通过选定
条件和样品,绘图或制表的探索成为可能。这也使我们能全面控制条件和样本的显示顺序。
```
cfd.tabulate(conditions=['English', 'German_Deutsch'],
    samples=range(10), cumulative=True)
```
![image](https://github.com/xuesu/picture/blob/master/2016-08-22-203654_737x414_scrot.png?raw=true)
### 使用双连词生成随机文本
bigrams() 函数接受一个词汇链表,并建立一个连续的词对链表。

## 2.4 词典资源
**词典或者词典资源**是一个词和/或短语以及一些相关信息的集合,例如:词性和词意定义等相关信息。

一个**词项**包括**词目**(也叫**词条**)以及其他附加信息,例如:词性和词意定义。

两个不同的词拼写相同被称为**同音异义词**。
### 词汇列表语料库
词汇语料库是 Unix 中的/usr/dict/words 文件,被一些拼写检查程序使用。我们可以用它来寻找文本语料中不寻常的或拼写错误的词汇,
nltk.corpus.word
### 停用词语料库
nltk.corpus.stopwords
### CMU发音词典
音素包含数字表示主重音(1),次重音(2)和无重音(0)
```
nltk.corpus.cmudict.entries()
('fir', ['F', 'ER1'])
('fire', ['F', 'AY1', 'ER0'])
('fire', ['F', 'AY1', 'R'])
('firearm', ['F', 'AY1', 'ER
```
示例扫描了具有特定重音模式的词汇
### 比较词表
NLTK 中包含了所谓的斯瓦迪士核心词列表(Swa
desh wordlists),几种语言中约 200个常用词的列表。语言标识符使用 ISO639 双字母码。

nltk.corpus.swadesh
### Toolbox 和 ShoeBox
一个 Toolbox文件由一个大量条目的集合组成,其中每个条目由一个或多个字段组成。大多数字段都是可选的或重复的,这意味着这个词汇资源不能作为一个表格或电子表格来处理。以前叫做 Shoebox
![image](https://github.com/xuesu/picture/blob/master/2016-08-22-212743_687x305_scrot.png?raw=true)
## 2.5 WordNet
WordNet是面向语义的英语词典，与普通词典不同的是，它具有很多额外信息，比如同义词，词之间的关系，比如词的从属关系，部分与全部关系，材质关系另外，wordnet还从一般到具体关系出发建立层次结构

nltk.corpus.wordnet
### 意义与同义词
1. synset(同义词集),词条lemma
    - 示例car.n.01，中间表示名词词性
    - wn.synsets('motorcar')
    - wn.synset('car.n.01').lemma_names
        - ['car', 'auto', 'automobile', 'machine', 'motorcar']
    - wn.synset('car.n.01').definition
        - 'a motor vehicle with four wheels; usually propelled by an internal combustion engine'
    - wn.synset('car.n.01').examples
        - ['he needs a car to get to work']
    - wn.synset('car.n.01').lemmas
        - [Lemma('car.n.01.car'),Lemma('car.n.01.auto'),Lemma('car.n.01.automobile'), Lemma('car.n.01.machine'), Lemma('car.n.01.motorcar')]
    - wn.lemma('car.n.01.automobile')
        - Lemma('car.n.01.automobile')
    - wn.lemma('car.n.01.automobile').synset
        - Synset('car.n.01')
    - wn.lemma('car.n.01.automobile').name
        - 'automobile'
### 层次结构
1. 根：概念一般，独一无二的根同义词集
2. 下位词：更加具体的概念
    - types_of_motorcar = motorcar.hyponyms()
3. 上位词
    - motorcar.hypernyms()
        - [Synset('motor_vehicle.n.01')]
    - paths = motorcar.hypernym_paths()
        - len(paths)
            - 2
        - [synset.name for synset in paths[0]]
            - ['entity.n.01','physical_entity.n.01',...]
    - motorcar.root_hypernyms()
        - [Synset('entity.n.01')]
### 更多的层次关系
1. 部分到整体part_meronyms()
2. 材料substance_meronyms()
3. 集合与成员member_holonyms()
4. 动作和细节(蕴涵)entailments()
    - wn.synset('walk.v.01').entailments()
        - [Synset('step.v.01')]
### 语义相似度
- lowest_common_hypernyms
- min_depth
    - 通过查找每个同义词集深度量化一般性的概念
- path_similarity
    - 是基于上位词层次结构中相互连接的概念之间的最短路径在 0-1 范围的打分(两者之间没有路径就返回-1)
## 语料库重要来源
1. 公开发行的语料库的重要来源是语言数据联盟((LDC)和欧洲语言资源局(ELRA)
    - 使用 OLAC 元数据格式存档,可以通过 http://www.language-archives.org/上的 OLAC 主页搜索到
2. 语料库列表(见http://gandalf.aksis.uib.no/corpora/sub.html)是一个讨论语料库内容的邮件列表,你可以通过搜索列表档案来找到资源或发布资源到列表中。
3. Ethnologue是最完整的世界上的语言的清单,http://www.ethnoogue.com/。7000 种语言中只有几十中有大量适合 NLP 使用的数字资源
## 习题
23.a ![image](https://github.com/xuesu/picture/blob/master/2016-08-23-010403_556x430_scrot.png?raw=true)
```python
import nltk
import matplotlib.pyplot as plt
from nltk.corpus import gutenberg
import math
fd = nltk.FreqDist(gutenberg.words('austen-emma.txt'))
x = [e for e in fd.keys()]
y = [math.log(fd[x0]) for x0 in x ]
```
而对于y2 = [math.log(fd[fd.max()]/a) for a in range(1,len(fd) + 1)]，其曲线为

![image](https://github.com/xuesu/picture/blob/master/2016-08-23-011824_605x469_scrot.png?raw=true)

曲线基本一致，可以认为齐夫定律有可能，所绘的线末尾有很长一段为0

23.b
![image](https://github.com/xuesu/picture/blob/master/2016-08-23-014429_569x434_scrot.png?raw=true)
明显，由于各词汇几乎等概率，所以不满足，齐夫定律只能适用于有意义的自然语言

25.
```python
import nltk
from nltk.corpus import udhr
def findUdhr(x):
    return [f for f in udhr.fileids() if x in udhr.words(f)]
```

26。0.923
```
a = wn.all_synsets('n')
sum = 0
l  = 0
for aa in a:
    sum += len(aa.hyponyms())
    l += 1

print float(sum)/l
```

27.

- n 1.96887292212
- v 5.36602019322
- s 2.32325402071
- r 1.74813587407
```python
for t in ['n','v','s','r']:
    a = wn.all_synsets(t)
    sum = 0
    l  = 0
    for aa in a:
        sum += len(wn.synsets(aa.name().split('.')[0],t))
        l += 1
    print t,float(sum)/l
```

# 3 加工原料文本
## 3.1
可以在 http://www.gutenberg.org/catalog/上浏览 25,000 本免费在线书籍的目录,获得 ASCII 码文本文件的 URL

- 分词:nltk.word_tokenize(raw)
- 处理HTML字符串返回原始文本:nltk.clean_html(html)

在一个叫做 Universal Feed Parser 的第三方 Python 库(可从 http://feedparser.org/免费下载)的帮助下,我们可以访问一个博客的内容,

# 5 分类和标注词汇
POS tagging:将词汇按它们的词性(parts-of-speech,POS)分类以及相应的标注它们的过程被称为词性标注(part-of-speech tagging, POS tagging)或干脆简称标注。

标记集:词性也称为词类或词汇范畴。用于特定任务的标记的集合被称为一个标记集

## 5.1 使用词性标注器
POS tagger

nltk.pos_tag(text)

## 5.2 标注语料库
1. 从表示一个已标注的标识符的标准字符串创建一个这样的特殊元组
    ```
    tagged_token = nltk.tag.str2tuple('fly/NN')
    ```
2. 其他语料库使用各种格式存储词性标记。 NLTK 中的语料库阅读器提供了一个统一的接口,使你不必理会这些不同的文件格式。
3. 并非所有的语料库都采用同一组标记;一个内置的到一个简化的标记集的映射
    ```
    nltk.corpus.brown.tagged_words(simplify_tags=True)
    ```
    ![image](https://github.com/xuesu/picture/blob/master/2016-08-23-185740_539x785_scrot.png?raw=true)
4. 图形化的POS一致性工具nltk.app.concordance()
## 自动标注
1. 默认标注器
2. 正则表达式标注器
3. 查询标注器
    - nltk.UnigramTagger(model = likely_tags)
4. 一个模块输出中的任何错误都在下游模块大
大的放大
5. 黄金标准测试数据:一个已经手动标注并作为自动系统评估标准而被接受的语料库。
## 5.5 N-gram标注
一元标注(Unigram Tagging)

一个 n-gram 标注器是一个 unigram 标注器的一般化,它的上下文是当前词和它前面 n-1 个标识符的词性标记

混淆矩阵 nltk.ConfusionMatrix(gold,test)

## 5.6 基于转换的标注
Brill 标注是一种基于转换的学习,以它的发明者命名。一般的想法很简单:猜每个词的标记,然后返回和修复错误的。在这种方式中,Brill 标注器陆续将一个不良标注的文本转换成一个更好的。与 n-gram标注一样,这是有监督的学习方法,因为我们需要已标注的训练数据来评估标注器的猜测是否是一个错误。然而,不像 n-gram 标注,它**不计数观察结果,只编制一个转换修正规则链表**

- 在其训练阶段,T1,T2 和 C 的标注器猜测值创造出数以千计的候选规则。
- 每一条规则都根据其净收益打分:它修正的不正确标记的数目减去它错误修改的正确标记的数目。
## 如何确定词的分类
1. 形态学线索
2. 句法线索
3. 语义线索
4. 新词
    - 名词可以被认为是开放类，介词则可以被认为是封闭类
5. 构词法
## 习题
T2.使用ntlk时发现书中示例不能接受该参数
```
nltk.corpus.brown.tagged_words(simplify_tags=True)#错误
```
T7.d1.update(d2)时，d1中d2和d1的并集被更新覆盖为d2中内容

T15. 

- a:[u'cm.', u'two-thirds', u'mg.', u'data', u'means', u'mechanics', u'sec.', u'$5', u'$2', u"10''", u'ethics', u'Police', u'Headquarters', u'deer', u'lb.', u'savings', u'$3', u'Data']
- b:[u'home', u'Home', u'B']
- c:'NN'
- d:'IN'

T39. 在二元模型中，以下使用laplace平滑不如普通的二元模型好。另外尝试了HiddenMarkovTrainer+laplace,效果也远远不及
```
class LaplaceBigramTagger(nltk.BigramTagger):
    def __init__(self,train_sents):
        self.firstD = ConditionalFreqDist(
            (x,y) for sent in train_sents for (x,y) in sent
        )
        self.secondD = ConditionalFreqDist(
            ((x,z),y) for sent in train_sents for ((z,w),(x,y)) in nltk.bigrams(sent)
        )
    def tag(self,sent):
        ans = []
        for i in range(len(sent)):
            x = sent[i]
            if i == 0:
                sub = self.firstD[x].max() if x in self.firstD.conditions() and self.firstD[x].N() > 0 else u'NN'
            else:
                sub = u'NN'
                prob = 0
                for y in self.firstD[x].keys():
                    z = sent[i - 1]
                    nowprob = (self.firstD[x][y] + 1.0)/(self.firstD[x].N() + len(self.firstD[x].keys())) * ((1.0/(1 + len(self.secondD[(x,z)].keys()) + self.secondD[(x,z)].N())) if y in self.secondD[(x,z)].keys() else ((self.secondD[(x,z)][y] + 1.0)/(1 + len(self.secondD[(x,z)].keys()) + self.secondD[(x,z)].N())))
                    if nowprob > prob:
                        prob = nowprob
                        sub = y 
            ans.append((x,sub)) 
        return ans
```
