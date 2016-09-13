<center>
#Automatically Generating Wikipedia Articles
#A Structure-Aware Approach
</center>
##Aim
- a method to learn topic-specific extractors for content section jointly for the entire template.
	- use a global integer linear programming formulation
- create a comprehensive textual overview of a subject composed of info drawn from the Internet.
##Training Corpus
- n documents,d1,d2,dn ...
- for di,a set of doc delineated sections si1,si2...sim,and their corresponding heading,hi1,hi2...him.
##Process
1. Prepocessing
	1. Template introduction
		1. cluster all section headings hi1,...him for all di using a repeated bisectioning algorithm(Zhao et al.,2005)
			1. similarity function use cosine similarity and TFIDF
		2. eliminate any clusters with low internal similarity, and there are no yield unified topics.
		3. determine the average number of sections k over all docs, then select the k largest section clusters as topics t1...tk.
		4. order these topics t1...tk using a majority ordering algorithm(Cohen et al., 1998)
			1. consistent with a maximal number of pairwise relationshops observed in our data set.
		5. each topic tj is identified by the most frequent heading found within the cluster.
	2. Search:To retrieve relevant excerpts,query reformulation
		1. search using Yahoo! and retrieve the first ten result pages for each topic and extracts all possible texts(6 excerpts per page).
		2. for each topic tj of each document we wish to create, label the excerpts ej1...ejr.(the total number of excerpts found on the Internet may be differ)
2. Learning Content Selection
	- Model
		- Input
			1. The title of the desired doc
			2. t1...tk,topics from the content template
			3. ej1...ejr,candidate excerpts for each topic tj
		- Define
			1. <img src="http://www.forkosh.com/mathtex.cgi? \phi(e_{jl})">,feature vector for the lth candidate excerpt for topic tj.
			2. w1...wk,parameter vectors,one for each topic t1..tk
		- Process
			1. Ranking
				1. <img src="http://www.forkosh.com/mathtex.cgi? score_j(e_{jl}) = \phi(e_{jl}) \times \underset{w_j}{\rightarrow}">
				2. the position l of excerpt ejl within the <b> topic-specific candidate vector </b> is the excerpt's rank.
			2. Optimizing the Global Objective
				- Objective:<img src="http://www.forkosh.com/mathtex.cgi? min\sum^k_{j=1}\sum^r_{l=1}{l \times x_{jl}}">
				- Exclusivity Constraints:<img src="http://www.forkosh.com/mathtex.cgi? \sum^r_{l=1}{x_{jl}}=1,\forall j\in\begin{Bmatrix} 1...k\end{Bmatrix}">
				- Redundancy Constraints:
					- <img src="http://www.forkosh.com/mathtex.cgi? (x_{jl} + x_{j'l'})\times sim(e_{jl} + e_{j'l'}),\forall j,j' \in \begin{Bmatrix} 1...k\end{Bmatrix} \forall l,l' \in \begin{Bmatrix} 1...r\end{Bmatrix}">
			3. solve tool
				- lp-solve
	- Training
		1. for each section we add the <b>gold excerpts</b> sij to the corrsponding eij1...eijr for di and tj.
		2. ![](http://i.imgur.com/BqQygc6.png)
3. Application
	1. Given the title of a requested doc, we select several excerpts from the candidate vectors returned by the search procedure.
##简明流程
1. 预处理
	1. 确定新文档中出现的topic
		1. 使用Zhao的方法进行标题的聚类
		2. 消除内部距离较小的类,使训练集中没有表示相近意思的标题
			1. 是否指使用出现次数最大的标题代替其他标题?
		2. 定义k为各篇文档中heading数目的平均数,取出现次数最大的k个聚类
		3. 使用Cohen的方法将类排序,这k个类形成k个topic
		4. 使用出现最频繁的标题代表topic
			1. 这个标题之后就用于代表文章k部分之中的一部分,那么实际效果究竟如何?
	2. 搜索
		1. 搜索yahoo!搜索到的前10页中每页6段形成摘要
		2. 对摘要编号
2. 学习
	1. 初始化向量w为零向量
	2. 对每篇文章每个topic,使用Rank函数衡量其分数
		1. Rank函数的权值向量即为w,w代表着每段的权重
		2. 做一个全局整数线性规划,求解一个01矩阵x,使得Objective尽可能小
			1. 这个公式什么意思?摘要的编号不是按顺序直接排的么?<img src="http://www.forkosh.com/mathtex.cgi? min\sum^k_{j=1}\sum^r_{l=1}{l \times x_{jl}}">
	3. 计算
		1. ![](http://i.imgur.com/w45eyxf.png)
			1. 为什么要把01向量x和文字一起比较?是指要把预料库的文件拆分为段落(摘要)?还是拆分为词?为什么不是x与sij的特征向量相比较?
3. 应用
	1. 使用最终的01向量w形成一篇新文档