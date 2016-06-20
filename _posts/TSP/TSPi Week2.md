#Chapter 5 The Development Plan计划阶段
##Vocabulary
1. Granularity 粒度
2. Miscellaneous 混杂的
3. rough 粗略的,大致的
4. Appraisal 评价,估价
5. Pseudocode 伪代码
6. Perspective 远景
7. Assembly 组件
8. Consolidated 加固的
##做计划的好处
##5.2 Tracking Progress Against the Plan<font color='red'>必考</font>
1. PV Planned Value 计划价值,整个工作中计划占比
2. EV Earned Value 获得价值 实际占比
##5.3 PV举例
1. 左侧任务按照时间顺序列写
2. 累计小时值之前的任务时间各项相加
3. 精确到小数点后两位

##5.4
- 工程师等级的任务分解到10小时或更少的层次
##5.5
做计划的时候遇到突发情况,预留5%-10%PV作为(management and miscellaneous)管理与杂物(M&M)阶段
##5.6 计划过程
1. 把原来策略表中形成的所有产品(代码,测试计划,说明书...)列出,把策略表的功能和其他的产品的size data 放入SUMS(SUMDI)表中.
	- SUMS表填三列1. 产品名称 2. 单位 3. 只填新增加和修改的量
3. TASK表,task names: 从TSPI过程流程走包含的任务如(启动和策略,计划,需求分析,编码,测试...,按时间顺序列写),PLAN{hours:花了多少小时,PV:每个任务的PV值是计划完成任务的时间占总时间的百分比, Cumulative PV:到此为止在这个项目中计划花费的时间占总时间百分比,Week No. 在第几周做},ACTUAL{hours:实际完成花费小时,EV实际占总时间百分比,Cumulative EV:...,WeekNo....,}
4.  Schedule表:日程安排表{现加,不在讲义,week No. PLAN{HOURS,PV,Cumulative PV},Actural{HOURS,EV,Cumulative EV}}
5.  比较TASK表和SCHEDULE表,Ttotal,Stotal,若T>S,则项目太大不能完成.需要缩小任务
6.  PLANSUMMARY(SUMP)(from SUMQ & TASK)完成size(SUMS)和time(TASK)部分
7.  Quality Plan(SUMQ)
	1.  Summary rate
		1.  LOC/hour
		2.  %reuse 复用比例
		3.  %new reuse 本次的代码有%将被下一个周期/项目复用
	2.  Percent defect-free(PDF)
		1. 给定的模块中,无缺陷的模块占总数百分比 
		2. <font color='red'>system->subsystem->component->module->submodule</font>
		3. 在系统测试阶段,达到或者超过90%
	3.  Defects/Page
		1.  from HLD or SRS
	4.  defects/KLOC
		1.  编码前是没有的
		5.  重视个人代码复查
	5. Defect Radios
		1. 缺陷比率 比率尽量>2
		2. 分为两方面
			1. Code review/compile defect radio
			2. Design review/unit defect radio
	6. Development time radios
		![](http://i.imgur.com/k7pMml8.png)
	7. A/FR in PSPi A/FR > 2; in TSPi A/FR = 1
	![](http://i.imgur.com/uvL2ZUd.png)
	8. Review and inspection rates
		![](http://i.imgur.com/rRZnmSu.png)
	9. Defect-injection Rates(Defects/Hour)
	10. <font color='red'>Phase Yields(阶段效益)</font>
		1. 在一个给定的阶段里
		2. 排除缺陷的效益
		3. (defects found) / (defects in the product (former + injected))
	11. <font color='red'>Process Yields(过程效益)</font>
		1. 在一个给定阶段之前
		2. PSPi:>80% TSPi:before first compile 75%,before first unit test:85%
8. 产生个人表(如个人SCHEDULE表)
9. Balance team workload
10. 5/17交 TASK(team/engineer(dont need to submit)),SCHDULE(team/engineer(...)),SUMP,SUMQ,SUMS	
11. 每周都要收集表..见PPT
##Exit Criteria
![](http://i.imgur.com/mTsAKQa.png)
#6 需求分析
##6.1 Why we need Requirements
##6.2 The SRS
内容

1. functional requirement
2. external interface requirement
3. design constraints
4. attributes
5. other requirements

实际


1. 角色分析
2. 功能需求分析(<font color='red'>不能出现模块</font>)
3. UML用例图(Use Case)
4. 非功能需求分析
##6.3 why Requirements is important?
1. you can argue that any changes will cost time & money.
##6.4 Process(注意顺序)
1. 入口准则
	1. Need statements:说明
	2. 开发策略/计划
2. 需求分析说明(Need Statement Review)
	1. 开发经理
	2. 不明白的问题提出并记录
3. Need Statement Clarification
	1. 同甲方交流对应问题
4. Requirement Task Allocation
	1. 开发经理将SRS开发的任务分解,team leader分配
5. Requirements Documentation
	1. 提交给开发经理,开发经理形成草稿.
6. System Test Plan
	1. 开发经理领导整个团队产生并复查
	1. 对功能性能进行测试
	2. 安排测试结果
7. Requirements & System Test Plan Inspection]
	1. quality/process manager
	2. 填写INS表格(不用填了)
8. Requirements Update
	1. 由开发经理将已经修订过的SRS和System Test Plan整合为新文档
	2. Verify traceability
9. User SRS Review
10. Requirements Baseline
	- support manager:baselines an official SRS copy
	- team can now change only by CCR
11. Exit Criteria
	- completed,inspected,updated SRS and system test plan
	- LOGT,LOGD,SUMS,TASK,SCHEDULE,SUMP,SUMQ
	- INS(completed inspection form)
	- update project notebook(5/24 SRS,system test plan 不用交,SUMS,TASK,SCHEDULE,SUMP,SUMS要交)
