#TSP表
##未开始
###INFO表
- filled by student
- teacher use this form to make the team and role assignments
##全周期
###个人WEEK表,SCHEDULE表,TASK表
- filled by each member
- planning manager use those form to generate weekly status report,then team leader report it to instructor
###小组SCHEDULE表,TASK表
- filled by planning manager
- team leader use those form and report it to instructor
##Plan阶段开始

###SUMS,TASK,SCHEDULE,SUMP,SUMQ

##Design阶段开始
###LOGT,LOGD,
##strategy
###STRAT表
- 时间/规模估计由Planning Manager进行
- filled by Quality/Process Manager
- 三件策略周期主要做的事 
	1. conceptual design(做什么,什么周期做) 
	2. preliminary size estimation 
	3. preliminary time estimation
###ITL表
1. 记录risk
2. 将risk每周分配到组员身上进行跟踪
###SCM
1. CIP Configuration Identification Plan
	1. 规定产品命名
	2. 标识纳入产品基线变更管理的时间点
	3. 标识属主,属主将对是否同意变更做决策
2. CCP Configuration Control Plan
	1. 保证更改不冲突
3. CCB Configuration Control Board
	1. 由支持经理负责
	2. 必须加入开发经理
##Plan阶段


###个人/团队TASK表
1. 每个任务的粗略估计
2. 任务的粗略顺序
3. PV
###个人/团队SCHEDULE表
1. 每周的工作计划时间
2. 每周PV

###SUMS表
1. 扩展STRAT表的内容
2. 加入其它产品的估计
3. SUMS表填三列1. 产品名称 2. 单位 3. 只填新增加和修改的量


###SUMP表
1. from SUMQ & TASK表
2. 在Plan阶段完成Size 和Time 的计算

###SUMQ表
1. 内容
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
			2. Code review/unit defect radio
	6. Development time radios
		1. 具体见PPT
	7. A/FR in PSPi A/FR > 2; in TSPi A/FR = 1
	8. Review and inspection rates
		1. ...
	9. Defect-injection Rates(Defects/Hour)
	10. Phase Yields(阶段效益)
		1. 在一个给定的阶段里
		2. 排除缺陷的效益
		3. (defects found) / (defects in the product (former + injected))
	11. Process Yields(过程效益)
		1. 在一个给定阶段之前
		2. PSPi:>80% TSPi:before first compile 75%,before first unit test:85%

##Requirement
###completed,inspected,updated SRS and system test plan
1. SRS内容
	1. 角色分析
	2. 功能需求分析(<font color='red'>不能出现模块</font>)
	3. UML用例图(Use Case)
	4. 非功能需求分析
2. 由开发经理划分工作,由组长分配工作
3. 由开发经理形成草稿并加入基线控制
4. 过程/控制经理检查
1. System test plan 开发经理领导
2. 过程/控制经理检查

###INS(completed inspection form)
1. filled by PROCESS/QUALITY MANAGER
2. 写出test plan后(system 或 integration)
3. 最终在design阶段完成

##Design 阶段
###Design Standard
1. filled by quality/process manager
###Name glossary
###SDS
1. 内容
	1. 软件总体架构
	2. 分配用例给components
		1. 相当于功能模块图
	3. 模块/部件的外部说明(功能,使用方法,返回值)
	4. 确定每个开发周期开发哪些功能模块
	5. (实际上)界面设计,数据库设计
2. 只需要部分人做
3. 基本流程
	1. 开发经理和team leader分配任务
	2. 写SDS
	3. 写test plan
	4. SDS 和Test plan inspection
	5. SDS 和Test plan Update
	6. final SDS放入基线下
###integration Test Plan
###INS form
##Implementation
1. components
2. unit test plan and support material
	1. implementation planning 开发经理分任务
	2. task allocation: team leader分配任务
	3. Detailed Design & Design Review
	4. Unit Test Plan
	5. Detailed-Design Review
	6. Coding,code review & compile
	7. code inspection
		1. 互相代码检查
	7. unit test
	8. component quality review
	9. component release

##Test
###最终产品
###用户手册
1. 内容
	1. 文档包含
	2. 功能
	3. 想查的东西
3. 书写原则(<font color="red">记住</font>)
	1. 短句,简单句
	2. 简单的词和短语
	3. 使用标准条款
4. Review(<font color="red">掌握</font>)
	1. 组织架构是否合理
	2. Terminology
		1. 可能涉及专业知识,需要进行解释
	3. Content
		1. 内容是否正确,完整(根据架构)
	4. 准确性
	5. 可读性
	6. 易懂性
###LOGTEST
![](http://i.imgur.com/3c68Kl6.png)
##Postmortem
###周期一报告
- 队长分任务分配任务
###PIP
- 与SUMP等计划比较
###PEER
