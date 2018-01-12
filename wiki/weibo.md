# 微博:  
[Reference](http://qndbp.qiniudn.com/weibo.pdf)

## 接口层 ：
无状态设计
支持HTTP/1.1协议
JSON数据格式
前端（侧重CPU和内存）

## 服务层 
- 无状态设计
- 组合服务与原子服务
- RPC Server队列处理机（侧重CPU和内存）

## 资源层 
- 数据可靠性要求很高
- 容量与QPS规划
- 扩容方案
- Hbase/MySQL	
- MC/MCQ/Redis（侧重内存与硬盘)

## Feed多级分布式缓存设计
###常见的模型指标：
- 读写比
- 访问时长分布
- 访问时段分布
- 访问量分布
- 访问来源分布
### 分布特点
- 97%用户都是浏览5天内的微博 
- 支持一致性Hash、Mod、日期hash等策略
- 每一组资源最佳4-6台

## Feed存储架构-MySQL

### 一级索引
- UID Hash/分库， 按照Month分表；
- 数据冷热区分
- 每个instance冷热数据均等
### 二级索引
- offset, count
- 按照UID分库分表
- 每个用户每个月一条记录
- 每条记录表示这个用户这个月发表了多少条微博
### 内容
- 按照ID分库分表
- 每天建立一张表

在分布式服务系统中，业务架构、技术架构与技术保障三者互为补充，共同保障系统的高可用性、高可扩展性、高吞吐量。