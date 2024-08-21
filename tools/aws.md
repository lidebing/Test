1. AWS CloudTrail: 分析api，对账户进行治理、合规性、运营审计、风险审计的服务
2. AWS SCT：不同数据库之间迁移需要转换。AWS DMS:快速安全的迁移数据库到AWS
3. AWS Snowball Edge：数十TB到PB的迁移。Snowball Edge不能用于数据库迁移
4. NET实例可以做堡垒机、支持端口转发、可以关联安全组。NET网关不能做堡垒机、不支持端口转发、不能关联安全组
5. EC2用户数据配置，默认情况下只有首次启动实例的时候运行，作为用户输入的数据默认以root权限运行。有显式配置除外
6. Aurora：多可用区部署，如果要读写分离，需要设置只读副本并且修改应用程序以使用对应的写、读端点。aurora每个集群最多有15个副本，副本主要两个作用，提高可用性(写坏了自动转移到副本)和提升读写能力
7. Amazon Cognito用户池：提供内置用户管理或与外部身份提供商集成，提供登录注册、内置用户等。创建之后必须在API gateway中创建该用户池的COGNITO_USER_POLLS授权方
8. Amazon Cognito主要组件是用户池和身份池,身份池提供aws凭证以授权你的用户对其他aws服务的访问权限
9. DocumentDB == MongoDB
10. DynamoDB：无服务器的Nosql数据库，是一种键值和文档数据库，可以在任何规模下提供毫秒级的性能。DynamoDB Accelertor(DAX)是一种与DynamoDB兼容的缓存服务
11. AWS Shield：是一种DDOS的保护服务
12. AWS Global Accelerator：可提供本地或者全球用户应用程序的可用性和性能的服务，提供静态ip，充当应用的固定入口点，适合非Http的服务：比如游戏UDP、LoT或者IP语音以及特别需要静态ip的情况
13. Amazon GuarDuty：监控任何恶意活动，提供威胁检测
14. Amazon Macie：数据安全和数据隐私服务，使用机器学习和模式匹配来发现和保护敏感数据，比如姓名、地址、信用卡等
15. AmazonRDSCustomforOracle：需要对Oracle数据库和其主机操作系统OS的专门定制，可以使用AmazonRDBCustomforOracle的多可用区配置，运行数据库管理员DBA访问和自定义数据库环境和底层操作系统
16. AmazonRDBForOracle不允许你访问和自定义数据库服务器主机和操作系统
17. 大数据公司处理流量突然激增的时候限制请求，可用API Gateway(如令牌桶)、SQS(扩展和解耦削峰)、Kinesis(完全托管、可扩展的服务，可以实时提取、缓冲和处理流数据)
18. 防止S3意外删除，执行合规性和监管准则：启用多重身份验证MFA删除、S3的bucket启用版本控制(删除的时候是虚拟删除)
19. 公司的EC2、RDS、S3运营之后成本高：优化方法为使用AWSCostExplorer获取使用率低的EC2实例报告，并用AWS Compute Optimizer查看实例类型建议(推荐最佳资源配置)
20. AWS Trusted Advisor：会检查未来30天过期或者过去30天过期的EC2预留实例，AWS Trusted Advisor没有自动续订预留实例的功能
21. 集群置放群组：是单个可用区内实例的逻辑分组，可以跨越同一个区域中对等vpc，低网络延迟、高网络吞吐量
22. Spot实例：抢占式实例，谁给的钱多谁用
23. 分散放置组：是一组实例，每一个实例都在不同的机架上，每个机架都有自己的网络和电源，可以跨越同一个区域中的多个可用区，每个组的每个可用区最多可以有7个正在运行的实例
24. 未来48小时为全球应用推出蓝(当前版本)绿(最新版本)部署，促销活动，尽可能对多用户部署：使用Global Accelerator将部分流量分配到特定部署
25. ElasticBeanstalk上运行的网站，安装时间长，包含静态和动态文件，怎么优化创建实例的时间： 使用已设置静态组建创建黄金亚马逊系统映像AMI、使用EC2用户数据在启动时自定义动态安装部分
26. AmazonRDSForMysql使用了只读副本，仍然有性能问题，不能脱离关系数据库，全球范围内运行：推荐使用Amazon Aurora Global Database在每个区域实现低延迟的快速本地读取。
27. Aurora：一个专为云构建的与mysql和postgreSql兼容的关系数据库，每个数据库可自动扩展到64TB
28. Amazon Redshift：一款PB级别的数据仓库，列式存储,专为大规模数据集存储和分析而设计，不是事务关系数据库
29. Redshift希望把超过一年的数据放入s3中，每日分析报告会使用最近一年的数据，希望保留交叉引用这些数据的能力：使用Amazon Redshift Spectrum创建指向S3中的基础历史数据的Redshift集群表。使用Redshift Spectrum可以高效的从s3中查询和检索结构化、半结构化的数据，而不需要将数据加载到Redshift中
30. Athena是一种交互式查询服务，可以使用标准sql轻松的在S3中分析数据
31. Redshift Copy可以把基于S3的历史数据加载到Redshift中
32. 如果服务器绑定了许可证：使用EC2专用主机
33. 批处理从标准SQS迁移到FIFO的队列：确保fifo队列的名称以.fifo结尾、确保fifo的吞吐量每秒不超过3000消息、删除现有的标准队列并将其重新创建为fifo队列。如果不是批处理fifo每秒不超过300条消息
34. DynamoDB使用DynamoDB Accelerator(DAX)作为缓存，S3使用CloudFront缓存静态内容
35. ElasticCache for redis：速度极快的内存数据存储，亚毫秒级延迟，是事务和分析处理的绝佳选择，比如缓存、聊天消息、游戏排行榜、地理空间、机器学习、媒体流、队列、实时分析和会话存储
36. 支持网关终端节点的两种AWS服务：S3、DynamoDB。其他服务使用VPC接口终端节点
37. 设计实时数据处理器，构建自定义应用程序来处理和分析流数据： 使用KinesisDataStreams处理数据流并解耦实时数据处理器的生产者和消费者
38. KinesisDataFirehose是把流数据加载到数据存储和分析工具中的最简单方法，可以把流数据加载到s3、redshift、es和splunk中
39. 确保ACM证书管理器到期前更新：利用AWS Config托管规则检查导入到ACM的第三方ssl/tsl证书是否在30天内过期，向团队通过sns发送通知。ACM里面提供的证书会自动更新不需要干预和监控，但是ACM不能自动续订你导入的证书
40. Direct connect数据查询返回60MB，可视化工具返回600KB，怎么优化流量：把可视化工具部署在数据仓库相同的aws区域中，在同一个区域的某个位置通过Direct Connect连接访问可视化工具
41. Amazon Neptune(海王星)：快速可靠的图形数据库服务。查用户a的朋友发布的视频的点赞数量是多少？
42. AmazonOpensearch：可执行交互式日志分析、实时应用程序监控、网站搜索等。
43. 把5PB的本地数据归档到持久的长期存储中：把本地数据数据传输到Snowball edge设备，然后把snowball edge数据复制到S3并创建生命周期策略以将数据转换到S3 Glacier。不能直接把Snowball edge数据复制到S3 Glacier中
44. S3给同一用户级别和跨账户级别通过访问权限：使用S3的存储桶策略。IAM是单个aws账户下的用户，所以这个只能给账户内的用户授予权限
45. S3中ACL可以想用户组授予对bucket或对象的读取、写入权限。通过ACL只能授予其他aws账户(而非特定用户)对你的s3资源的访问权限
46. 安全组是EC2实例的虚拟防火墙，控制流量的传入、传出
47. 天气预报机构收集多个城市关键天气指标，并以键值对的形式以一分钟的频率把这些数据发送到AWS，哪些方案可以高可用可靠的存储这些数据：lambda、DynamoDB
48. Amazon GuardDuty是一项威胁检测服务，可持续监控恶意活动和未经授权的行为：可以收集如CloudTrail事件、VPC流日志、DNS日志
49. AWS Transit Gateway中转网关，就是一个hub，可以互联虚拟私有云VPC和本地网络
50. VPC对等连接是两个VPC之间的网络连接，使你可以使用私有ip之间路由流量
51. AWS VPN CloudHub：可以是远端站点可以互相通信(分支机构可以互相之间以及和总部发送和接受消息)
52. 提高上传到S3的效率：使用分段上传、使用S3 transfer Acceleration更快的上传文件到目标bucket
53. Database Migration Service(DMS)可快速、安全的把数据库迁移到aws，源数据库在迁移期间完保持完全运行，如把Oracle数据复制到redshift
54. 从S3 standard转换到S3 One zone-IA之前，存储持续时间最短为30天
55. 分散Spread置放群组可以跨越同一个区域中的多个可用区，每个组的每个可用区最多可以有7个正在运行的实例
56. KinesisDataStream的的生产者和多个消费者数据传输速度存在性能滞后：使用KinesisDataStream的增强扇出功能，默认2mb/秒/分片输出在多个消费者共享，多个并行使用扇出功能的时候没个消费者都可以有2mb/秒，
57. 集中提供共享和集中管理的VPC：使用AWS Organizations中的同一父组织的其他AWS账户共享一个或者多个子网

58. 新部署AutoScaling后工作不正常：创建新的启动配置(实例配置模版)以使用正确的实例。修改AutoScaling组以使用此新的启动配置，删除旧的启动配置。启动配置一旦创建就不可以修改
59. S3自动提供写后读一致性，不需要更改性能或者可用性，不需要额外成本。写入之后就一定可以读最新的。
60. 促进对数据库的安全访问：配置RDS以使用SSL传输数据
61. 从S3流式传输到KinesisDataStreams最快的方法：使用DMS(DataMigrationService)作为s3和KinesisDataStreams的桥梁
62. EBS卷加密：从卷创建的任何快照都经过加密、卷和实例之间移动的数据已加密、卷内的静态数据已加密
63. Global Accelerator提供低延迟分发直播体育比赛，UDP
64. 从S3的一个可用区复制到另外一个可用区：使用aws S3sync命令从源复制到目标桶、设置S3的批量复制。 实时复制只会复制新对象(如果要实时复制必须联系aws support并提交支持票证)，批量都会复制
65. 可用区EC2出现故障的时实现最大可用性：使用分散安置组
66. 弹性网络接口ENI绑定到特定的可用区，不能跨区绑定到EC2
67. EC2 Hibernate休眠的条件：EC2的实例根卷必须是EBS卷
68. 根据物理核心和底层网络套接字收费的话：必须是专用主机
69. IAM安全工具： IAM凭证报告
70. IAM角色：一个IAM实体，定义一组用于向AWS服务发出请求的权限，并将由AWS服务使用
71. IAM策略由一个或者多个语句组成：包含Sid、Effect影响、Action、Resource、Condition。不包含版本
72. EBS卷是按照可用区创建的，如果要把一个挂在到另一个可用区，必须使用快照迁移
73. EC2实例启用两个EBS卷，在EC2删除时：默认情况下，EBS的根卷也会被删除(默认删除为true)，另一个EBS卷不会被删除(默认删除为false)
74. AMI是为特定区域构建的，每个区域都是唯一的。无法跨区域启动EC2，但是可以复制到目标区域，然后用它创建EC2实例
75. 创建EC2时，只能使用以下类型的EBS卷作为启动卷：gp2、gp3、io1、io2、Standard
76. NLB网络负载均衡器提供DNS名称和静态ip、ALB提供DNS名称不会提供静态ip、
77. NLB可以提供最高的性能和最低的延迟
78. ALB支持以下协议：http、https、websocket
79. 启用跨区域负载均衡之后，NLB会在所有可用区的所有注册的实例之间均匀分配流量

80. 服务器名称指示SNI：允许在同一个侦听器上公开多个https应用，每个应用都有自己的ssl证书
81. NLB支持http、https、tcp允许健康检查
82. ALB：应用负载均衡器、NLB网络负载均衡、ELB弹性负载均衡器
83. RDS 支持 MySQL、PostgreSQL、MariaDB、Oracle、MS SQL Server 和 Amazon Aurora。
84. Aurora Global Database全球数据库允许您在另一个 AWS 区域拥有 Aurora 副本，最多可有 5 个次要区域。
85. RDS只读副本使用异步复制，多可用区使用同步复制
86. RDS最多只有15个可读副本
87. Oracle不支持IAM数据库身份认证
88. 您无法从未加密的 RDS 数据库实例创建加密的只读副本
89. Aurora支持mysql和postgreSql
90. Aurora自动备份保存时间最长35天，所以要长期保存只能按需备份
91. Aurora的克隆比从快照恢复快很多

92. EBS一次只能挂载在一个EC2上
93. 黄金 Gold AMI 是一个映像，其中包含安装和配置的所有软件，以便未来的 EC2 实例可以从该 AMI 快速启动
94. S3想要公布数据，但是不想要Bucket策略和公开，且使用FTP访问：可以使用AWS Transfer
95. 想给3个不同的应用的不同的sql发消息：使用sns + sqs 扇出
96. Kinesis数据流的容量限制由数据流中的分片数量决定.
97. KinesisDataFirehose支持Lambda进行自定义数据转换
98. SNS不支持Kinesis Sream作为订阅者
99. Amazon MQ支持行业标准API(JMS、NMS)以及消息传递协议(AMQP、STOMP、MQTT、websocket)

100. Lambda的最长执行时间是15分钟
101. DynamoDB表中项目的最大大小为400KB
102. SNS不能直接和DynamoDB集成
103. DynamoDB Streams使DynamoDB可以获取更改日志并使用该日志在其他AWS区域中的副本表之间复制数据
104. DocumentDB是nosql数据库，但是没有serverless，也没有全局数据库功能

105. AQS QLDB: 金融交易安全、不可变、加密存储
106. Amazon Keyspaces --> Apache Cassandra
107. Amazon Timestream : 森林数据收集火灾，时间序列数据
108. Amazon EMR : Spark、Hive、Presto
109. Transcribe: 语音转文本
110. Polly：文本转语音
111. Translate：语言翻译
112. Personalize：个性化推荐
113. SageMaker：快速构建、训练、部署机器学习模型
114. Forecast：利用机器学习提供高度准确的预测
115. Rekognition：图像、视频中查找对象、任务、文本、场景
116. Lex：聊天机器人
117. Comprehend：自然语言NLP服务，比如按主题对文章分组，查找文本中的含义和见解
118. Kendra：高度准确且易于使用的企业搜索服务,由机器学习支持
119. Polly：发音词典：自定义单词发音；语音合成标记语言SMML：强调单词发音

120. 配置 EventBridge 的权限以将 Lambda 函数配置为目标: 基于资源的策略，使用KinesisDataStream为目标的时候：基于身份的策略
121. KMS密钥自动轮换的时间是每1年换一次
122. 使用访问策略列表KMS ACL来控制对KMS CMK的访问
123. AWS Firewall Manager 是一项安全管理服务，允许您跨 AWS Organizations 中的账户和应用程序集中配置和管理防火墙规则
124. AWS shield防止DDOS，需要7+24的话需要Shield Advanced
125. AWS WAF 防止sql注入攻击
126. Amazon Inspector可以扫描操作系统是否有漏洞
127. CIDR 不应重叠，AWS 中的最大 CIDR 大小为 /16
128. 安全组运行在EC2级别，NACL运行在子网级别
129. AWS VPN CloudHub 允许您使用 AWS VPN 与多个站点安全地通信。它采用简单的中心辐射模型运行，您可以使用或不使用 VPC
130. Network Firewall可以保护VPC中的3到7层
131. lowest RTO和RPO ： 使用Multi site多站点
132. high RTO和RPO ： Backup and Restore
133. 灾备中启动运行系统的缩小版本，灾难发生时，能迅速扩大规模：Warm Standby
134. 灾备中只运行关键设施，不介意更长的RTO： Pilot Light 指示灯
135. AWS DataSync不支持EBS
136. Elastic Fabric Adapter ： 集群中高性能计算HPC中提高EC2实例之间的网络性能
137. AWS Trusted Advisor 提供可帮助您遵循 AWS 最佳实践的建议。它通过使用支票来评估您的帐户。这些检查确定了优化 AWS 基础设施、提高安全性和性能、降低成本以及监控服务配额的方法。

138. CloudFormation: 代码化部署
139. SES：simple Email service
140. PinPoint：发送短信、邮件、app推送消息、语音营销
141. SSM：Systems Session Manager：允许在EC2或者内部服务器上安全使用shell而无需ssh访问、无需密钥等等、不开22端口
142. AppFlow：将 Salesforce 和 Slack 中的数据传输到 S3 存储桶中的 AWS
143. AWS Trusted Advisor：分析您的 AWS 账户并提供成本优化、性能、安全性、容错和服务限制方面的建议
