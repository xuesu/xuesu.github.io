#Integration & System Test
##9.1 Testing Principles
1. Tspi测试的主要目标(<font color="red">掌握</font>)评估产品而非修复缺陷
##9.2 Testing Strategy(<font color="red">记住</font>)
1. Build The System
	1. 与集成测试其实是两步
2. Integration Test 
3. System Test
4. Regression Test(从第二周期开始(<font color="red">掌握</font>))
	1. 采用循环的开发策略
	2. 是否影响以前的功能
##9.3 The Build & Integration Test
1. should not test functions(<font color="red">掌握</font>)
2. 测试模块间的调用和关联是否正确.
3. 策略体现在四方面(<font color="red">掌握</font>)
	1. Big-Bang Strategy
		1. 优点:需要最少的测试开发工作
		2. 缺点:成功很难,尤其是质量低时
	2. The One-at-a-time Strategy
		1. 优点:很容易找到每次新添加的部分和其他模块间关系是否有问题
		2. 缺点:需要大量测试开发工作.
	3. The Cluster Strategy
		1. 把功能相似的分为一类
	4. The Flat-System Strategy
		1. 由高层次向低层次逐渐集成
		2. 优点:最开始就能发现大范围的问题
		3. 缺点:通常需要大量存根(stub)等处理未集成的子模块的空返回.
##9.4 系统测试策略(<font color="red">掌握,区分系统测试策略和集成测试策略</font>)
1. Function-first strategy
	1. 按照功能模块进行测试
		1. 对每个功能点在正常/非正常/重点情况下进行测试
	2. 测试性能
2. Functional-Area Strategy
	1. 从底层功能区到两个功能区之间测试
	2. 正常/非正常测试数字计算/可用性/性能/质量
3. Combining the Preceding-two Strategy
	1. 结合功能第一策略和功能区策略
	2. 首先采用功能第一测试原子功能,然后结合到一起形成功能区
4. Reversing the Preceding Strategy
	1. 与二者结合策略相反
	2. 从上往下走
##9.5 Test Planning
1. 要求了解测试计划(步骤,支撑材料,结果,测试无缺陷运行时间以及每次测试运行总时间,发现缺陷总数,计划排除的缺陷数,相应的测试支撑材料所需工作时间)(<font color="red">掌握</font>)
##9.6 Tracking and Measuring Testing
1. 填写LOGD,LOGTEST(开始时间,结束时间,哪些模块记录了什么等)
2. 为回归测试提供参考
##9.7 Documentation
1. 用户使用手册
2. 包含((<font color="green">了解,不用记住</font>))
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
##9.8 The Test Process
1. Entry Criteria(前面阶段工作/表格/数据/文档都ok)
2. 测试开发工作
3. 建立系统(Build)(开发策略第一步)
	1. 质量过程经理每个步骤都要看看是否返工
4. 集成测试
	1. 记录LOGD,LOGTEST
5. 系统测试
6. Documentation
	1. 需要复查集成
7. Exit Criteria
	1. 最终产品
	1. 用户使用手册
	2. LOGTEST
	3. 五大表格
	4. 测试实际数据
#后置处理
##Vob
- Fell short:没有完成目标
##Why
1. 通过提供标准流程来改善开发过程
2. PIP表,过程改进建议表,为下一个周期做准备
##Process
1. Entry Criteria
2. Review Process Data
	1. 对前面产生的所有数据进行分析
	2. 与SUMQ表作比较,评估哪些地方没有达到标准,可以知道哪些地方做的不够好需要改进,哪些地方较好,填入PIP表
3. Evaluate Role Performance
	1. 对于个人角色进行评估
	2. 每个角色的工作在哪些地方非常有效
	3. 在哪些地方存在提高空间
	4. 准备周期1报告
		1. 在team leader领导分工下,一起完成
		2. 包含
			1. summary:一个团队总结
			2. Roles Reports:角色报告
			3. Engineer Reports:作为软件开发工程师的报告
		3. 集成检验总结
	5. 角色评估
		1. 第三步是角色的性能评估由自己/同学评价
		2. 第五步使用PEER表格进行评价
4. 出口准则
	1. PEER,PIP,周期报告,其他表
#11 Being on a team(都要掌握)
1. 协同工作准则
	1. 负责
	2. 为自己的目标奋斗
	3. 适合的原则
		1. 尊重自己和他人
2. 有效的团队合作
	1. 内部交流沟通
2. 协同工作报告
3. 团队建设责任
	1. 尽自己所能
	2. 参与团队目标和计划的建设
	3. 建设维护高效合作团对
##期末比期中考试题目多,有论述题,主观题要尽可能多答
- 5/31 应当完成设计阶段
- 6/2 实现(不要求交源码)
- 6/3 测试
- 提交用户使用手册
- 6/16 周期一报告
- 6/17 验收,视频演示5min