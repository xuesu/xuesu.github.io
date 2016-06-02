#第一章引言
- 决策树学习算法-NASA(用于区分天体)
- 交叉学科
	- 人工智能
	- 贝叶斯方法
	- 计算复杂度
	- 控制论
	- 信息论
	- 哲学
	- 心理学和神经生物学
	- 统计学
	- ...
##1.1 学习问题的标准描述
- 定义:对于某类任务T和性能度量P,如果一个计算机程序在T上以P衡量的性能随着经验E而自我完善,则可以称这个计算机程序在从经验E中学习
- 特征
	1. 任务种类T
	2. 性能标准P
	3. 训练经验E
##1.2 设计学习系统
###1.2.1 选择训练经验
1. 选择训练经验的类型
	- 关键属性:训练经验能否为系统的决策提供直接或间接的反馈
		- 直接
		- 间接
			- 例如:通过过去对弈序列和最终结局推测走法
			- <b>信用分配问题(credit assignment)</b>
2. 学习器可以在多大程度上控制训练样例序列
	1. 训练经验以超乎学习器控制的随机过程提供
		- 实验还未考虑过的全新棋局
	2. 学习器可以向施教者提出不同类型的查询
		- 自己提出特别困惑的棋局
		- 依赖施教者选取
	3. 学习其通过自动探索环境来搜集训练样例
		- 在目前发现的最有效的路线上采用微小变化
3. 训练样例的分布能多好的表示实力分布
	- 学习样例通常与最终系统被评估时的样例有一定差异,学习器必须能够从中进行学习
###1.2.2 选择目标函数
- 决定要学习的知识的确切类型以及执行程序怎样使用这些知识
- 例子:跳棋博弈程序. 最终程序需学会从合法的走子(定义了一个已知的巨大搜索空间)中选择最佳走子(最优化问题)
- 目标函数V:B(合法走子)->R
	- 学习任务被简化为发现一个理想目标函数V的可操作描述
	- 有时仅希望得到近似的目标函数
		- 函数逼近(function approximation) <img src="http://www.forkosh.com/mathtex.cgi?  \hat{V}">
###1.2.3 选择目标函数的表示
- 选取函数逼近的权衡
	- 选取一个非常有表征能力的描述,以最大可能的逼近理想的目标函数V
	- 表征能力的描述需要非常多训练数据,使程序能从它表示的多种假设中选择
- 将目标函数表示为一个线性函数
	- <img src="http://www.forkosh.com/mathtex.cgi? \hat{V}(b)=\sum^n w_i x_i">
###1.2.4 选择函数逼近算法
- 每一个训练样例是形式为<img src="http://www.forkosh.com/mathtex.cgi? \textless b,V_{train}(b) \textgreater">的序偶
- 样例过程
	1. 估计训练值
		- <img src="http://www.forkosh.com/mathtex.cgi? V_{train}(b) \leftarrow \hat{V}(Successor(b))">
	2. 调整权值 
		- 为学习算法选择最合适训练样例{<img src="http://www.forkosh.com/mathtex.cgi? \textless b,V_{train}(b) \textgreater">}的权wi
			1. 定义最佳拟合(best fit)训练数据的含义
				- 常用方法:定义为训练值和假设值预测出的值之间的误差平方和最小
			2. 进一步改进权值,使得它对于估计的训练数据中的差错有好的健壮性.
				- 最小均方法(least mean squares) LMS训练法则
					1. 对每个<img src="http://www.forkosh.com/mathtex.cgi? \textless b,V_{train}(b) \textgreater">使用当前的权计算<img src="http://www.forkosh.com/mathtex.cgi? \hat{V}(b)">
					2. 对每个权值wi,做如下更新
						- <img src="http://www.forkosh.com/mathtex.cgi? wi \leftarrow wi + \eta ( V_{train}(b) - \hat{V} ( b ) )">
						- 使得只有在训练样例的棋局中确实出现的特征的权值才能被更新
###1.2.5 最终设计
1. ![](http://i.imgur.com/OVAPPL5.png)

	- 执行系统(Performance System) 用学会的目标函数来解决指定任务
	- 鉴定器(Critic) 使用对弈路线作为记录,产生训练样例的序偶
	- 泛化器(Generalizer) 以训练样例为输入,产生输出假设,作为对目标函数的估计
	- 实验生成器(Experiment Generator) 以当前假设为输入,输出新的问题供执行系统探索.
2. 最近邻算法
3. 相互比赛,遗传算法
