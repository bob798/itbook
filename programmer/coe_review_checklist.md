                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
# 代码检查CheckList
## 数据库    
### 表结构设计
* 是否可以通过增加冗余字段，减少表之间的join                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    

### 索引  
* 合理使用索引，观察索引的命中率
* 分区索引                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     

### SQL优化   
* 减少SQL调用
* 减少join                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           

### SQL性能    
* 慢SQL抓取
* explain SQL语句                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     

### 数据管理  
* 对历史数据进行清理、减少表中的数据量                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
 
## 前台 
* javascript使用优化
* 静态缓存                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      

## 应用层   
### 业务   
* 避免在循环调用数据库、RPC
* 频繁读写同一行数据
* 避免长事务。例如在对数据库进行操作的过程中，进行多次外部接口的调用。 由于事务持续时间延长，事务对相关资源的锁定时间也相应增加，从而可能严重增加了并发冲突，影响到系统吞吐率和可伸缩性。
* 避免大量的数据导出。
* 算法优化。
* 关键业务处理失败，保存失败的数据，并自动进行补偿。
* 控制资源的使用，例如从数据库、文件中加载大量内容到内存中。
* 使用线程池，杜绝无限制的创建线程
* 确保释放使用的资源，最好在finally里面对使用资源，例如文件进行释放。
* 合理的区分主流程和辅助流程，通过后台异步的方式把例如记录日志之类的辅助流程跟主流程分离。
* 对数据库可以采取批量插入、更新的方式提高系统性能。
* 在while和for循环中，要留意调用代码是否会抛出异常，从而导致整个循环的失败。

### 远程调用优化  
* 合理设置timeout值，不要太长杜绝雪崩
* 远程调用未分页
* 减少远程调用
* 远程调用使用批量接口
* 适当进行重试，并考虑外部系统的压力，重试2-3次进行放弃                                                                                                                                                                                                                                                                                                                                                                                                                                       

### 数据库连接优化 
* 数据库连接池优化
* 事务优化                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

##  服务接口 
* 读接口未对返回的数据进行限制，例如时间范围进行控制
* 关键业务例如账户扣费是否支持幂等性。
* 服务接口是否需要支持大并发。例如写接口能异步化。                                                                                                                                                                                                                                                                                                                                                                                                                                                  

## 应用环境    
### JVM优化   
* JVM参数优化
* 系统内存资源清理                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         