#7 Designing
##7.1 Design Principles
- HLD:high level Design
	- SDS:Software Design Specification
		- 整体架构设计,功能模块设计,数据库,用户界面,接口...
- DLD:detailed Design
	- 原子模块内部的逻辑,步进条件,函数等设计
- 在TSPi中,HLD在设计阶段,DLD在实现阶段(implementation phase)
##7.2 Using the Entire Team 
- only one or two members are needed to ducument HLD
- others: 标准约定,重用...
##7.3 Design Standards(<font color = "red">掌握</font>)
- 不仅要完成SDS,还需要给出如下标准
- Naming conventions
	- 命名约定
- Interface formats
	- 接口格式,界面格式(人机接口)
- System and error messages
- Defect Standards
	- TSPi中定义的缺陷标准(10-100)
- LOC Counting
	- 代码行统计按照TSPi方式,只统计新增和修改过的代码行
- Design representation standards
	- SDS文档必须包含哪些内容
##7.4 Designing for Reuse
- 定义初始复用库的标准(<font color = 'green'>了解</font>)
	- Reuse interface standards
	- Reuse documentation standards
	- Reuse part quality
	- Application Support
		- 应用支持/技术支持
		- 谁负责维护复用模块
##7.5 SDS
- SDS内容(<font color='red'>掌握</font>)
	- 软件总体架构
	- 把系统功能分配给components(<font color='red'>掌握</font>)
		- 相当于功能模块图
	- 模块/部件的外部说明
		- 实现功能/使用方法/返回值
	- 确定在每个开发周期开发哪些功能/模块
- SDS文档应当包含所有周期
- 实验中需要包含这些内容
	- 软件层次架构设计
		- 结合自身系统说明
	- 功能模块设计(需要与分析阶段相符合)
		- 总体功能模块图
	- 数据库设计
		- ER图
		- 数据库表设计
	- 用户界面设计
		- 色彩
		- 线图(典型的功能界面)
			- 表明区域(比如功能展示区,按键区)
##7.6 Design Process(16周周二验收,需要做演示视频)
1. entry criteria
	- 做完了前面阶段的任务
2. High-Level Design
	- Develop Manager分任务,Team Leader 分配至人
	- 内容:定义软件架构,命名模块,分配用例,分配任务
3. The name glossary and Design Standard
	- Qualiy/Process Manager(<font color='red'>掌握</font>)
4. Design Task Allocation
5. The Design Specification
	- 写自己SDS部分
	- 制作并复查自己的部分
	- Develop Manager集成各部分形成草稿
6. Integration Test Plan
	- 检测模块间调用和返回等关系是否正常
	- 注意重点不在各模块功能
	- Develoment manager
7. Design & Integration Test Plan Inspection
	- INS,LOGD
	- quality/process manager
8. Design & Integration Test Plan Update
	- 重新提交给开发经理
	- 开发经理最终形成final SDS
		- 证实可追踪性
9. Design Baseline
	- support manager 放入配置管理控制之下,CCR
10. 出口准则
![](http://i.imgur.com/cqq2JXZ.png)
##8 Implementation
###8.1 Design Completion Criteria
- 划分原子对象:100-150行代码
###8.2 implementation standard(不用记)
- standard reivew(derived from design)
- naming,interface,message standards(derived from design)
- coding standards(new)
- size standards(derived from design)
	- LOC counts(Design)
- defect standards(derived from design)
- defect preventions(new)
	- 整个团队讨论
	- 出现频率最高的缺陷确定后,进行改进,看出现频率是否降低
###8.3 Implementation Strategy(<font color='red'>掌握</font>)
- 根据这三个策略完成原子对象的编码实现
	1. 复查
		- 由下往上复查
	2. 复用
		- 每日都有简短交流,看是否有复用程序段
		- 建立复用库,使用复用代码
	3. 测试
		- 按照系统测试计划,集成测试计划的顺序进行实现
###8.4 Reviews and Inspections
- 重视复查检查
- 为什么重视(见PPT 了解)
	- keystroke errors
###8.5 Design Inspection for Source Program
###8.6 Implementation Process(<font color='red'>掌握</font>)
1. Entry Criteria
2. Implementation Planing 
	- development manager 定义工作并分开
3. Task Allocation
	- team leader分配任务并得到承诺反馈
4. Detailed design and Design Review
	- 做完自己该做的详细设计(时序图/流程图)
	- 复查
	- form LOGD,LOGT
5. Unit Test Plan
6. Detailed-Design Inspection
	- LOGD,INS(INS不用交)
7. Code,Code Review and Compile
	- LOGD,LOGT	
8. Code Inspection
	- quality/support manager
	- 互相代码检查
9. Unit Test
	- LOGD,LOGT
10. Component Quality Review
	- 模块质量复查
	- SUMQ表,观察差距.
	- Quality/Process Manager
11. Component Release
	- 交给support manager,放入配置管理控制下
12. Exit Criteria
	1. components
	2. INS form
	3. Unit Test Plans and support materials
	4. LOGT,LOGD,SUMS,TASK,SCHEDULE,SUMP,SUMQ(还交五张表)
	5. updated project notebook
13. 下周一最后一次实验室讲课