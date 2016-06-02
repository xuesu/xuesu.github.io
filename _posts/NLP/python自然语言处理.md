#PYTHON自然语言处理
---
##软件安装需求
- python
- nltk
- nltk-data
- numpy
- matplotlib
- networkX
- prover9
##NLTK介绍
![](http://i.imgur.com/x0nL4S9.jpg)
##第1章 语言处理与python
###章节目的
1. 简单程序+大量文本能够实现什么?
2. 如何自动提取概括文本风格和内容的关键词和短语?
3. python编程语言为上述工作提供了哪些工具和技术?
4. 自然语言处理中有哪些有趣的挑战?
###1.1 语言计算:文本和单词
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
###1.2 近观python
  系统地回顾关键的编程概念
###1.3 计算语言:简单的统计
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
###自动理解自然语言
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
###习题
- 15. sorted(w for w in set(text4) if w.startswith('b'))
- 17. 
	text9[:].index('sunset')
	629
	text9[630:].index('sunset')
	12
	...
- 20. 
	'1'.islower() 
	True
