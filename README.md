数据库选型-业务场景: 
用户业务是面向2C以及2B的客户场景，期望建立基于用户之间关系的游戏或其他第三方app推荐。在数据库选型之初，首选并非是DynamoDB，因传统上DynamoDB被视为非关系型数据库的代表，在一个需要存储和处理关系的场景下，很容易被忽视，但在调研了不同数据库之后，首先对于可扩展性，当业务需要扩展到 TB 级以上的数据，DynamoDB 不会降低性能，业务方核心诉求需要低延迟小于10ms，其次，DynamoDB 完全托管，可处理升级、备份和其他管理任务。基于以上两点诉求，开始尝试使用DynamoDB 并最终应用在生产环境，本文重点在于使用DynamoDB进行建模，实现关系存储，以及访问模式的实现。
对于DynamoDB的性能，DynamoDB可以在水平扩展中实现任何规模下提供一致的性能。例如一些DynamoDB用户拥有超过100TB的表，而这些表的读写性能与它们小于1GB时相同。

ER Modeling 设计
针对业务场景，设计以下Entity Relation Diagram，其中涉及的实体包括: 用户(user_id)，关系Relevant(Relevantuser_id), Type(type_id) 以及用户等级(level_id) 。

访问模式实现设计(Access Patten Design)

1. 创建关系-createRelevant
2. 过滤查找指定用户在指定区域/指定性别的好友列表-getFilteredRelevant
3. 更新关系-updateRelevent ,基于主键更新ReleventContent内容, 关系内容备注。
4. 删除关系-deleteRelevant
