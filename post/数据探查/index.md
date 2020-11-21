
### 前言

最近参与了公司一个项目，前面我根据MRD将B端标签的PRD写完了。后面便给我安排了《B端标签PRD数据探查》。这是我第一次接触到 **数据探查** 概念。俗话讲，开始工作之前，一定要弄明白工作目标是什么。在做数据探查任务之前，下面总结一下自己在网上学习到有关 *数据探查* 的知识总结。

### 数据探查

实习已经有半个月了，期间一直在学习数据仓库相关的知识。首先我们根据从客户数据库拉取到的数据，来构建客户的数据仓库。在数据仓库分层模型中，ODS层也称为原始层，这里面的数据是拉取到最原始的数据表，没有经过任何的处理。ODS层完成后，便开始了真正意义上的数据开发流程。在进行数据开发之前，最重要的事情是要保证 **数据的可靠性**，它是决定最后数据正确性非常关键的一步。

经过跟同事沟通之后，我要做的事情就是保证后面根据B端标签来拉取数据时，保证我拉取到的数据是标签定义的数据结果，比如交易总金额这个标签（标签定义是：过去3年客户实际购买商品总金额）。为了保证拉取的结果，就要检查

- 需要那些表做关联（检查表是否存在）
- 需要表中那些关键字（检查关键字是否存在）
- 关键字对应的数据列是否正常（检查数据是否重复、缺失、异常等）
- 如果上面3步没问题，是否可以拉取数据成功（给出SQL语句）

完成上述过程，一定要写一个总结性文档。这个文档用来解释：

1. 业务需求是什么？
2. 拉取到的数据是什么数据？
3. 拉取到的数据生成逻辑是什么？是否正确（是否满足业务需求）
4. 拉取过程中用到了那些表，那些标签，数据结构、数据质量如何？

总的来讲，数据探查是在拿到业务需求后（根据PRD标签拉取数据），首先从数据整体上确定实现业务需求要用那些数据源，即：数据源 -- > 数据表 --> 表中结构 --> 表内数据质量；以及表与表之间的逻辑关系，都要在文档里面阐述清楚。

这样根据数据探查的文档，才能方便后期数据清洗工作。

### 参考资料

- [数据探查（一）](https://blog.csdn.net/li2008xue2008ling/article/details/8245359)
- [数据探查（二）](https://blog.csdn.net/li2008xue2008ling/article/details/8624232?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-10.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-10.channel_param)
- [数据探查（三）](https://blog.csdn.net/li2008xue2008ling/article/details/36002421?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160404075619215646530972%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160404075619215646530972&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v28-1-36002421.first_rank_ecpm_v3_pc_rank_v2&utm_term=数据探查&spm=1018.2118.3001.4449)
- [【数据治理】数据质量探查](https://blog.csdn.net/weixin_42893650/article/details/90640708?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160404075619215646530972%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160404075619215646530972&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v28-2-90640708.first_rank_ecpm_v3_pc_rank_v2&utm_term=数据探查&spm=1018.2118.3001.4449)
- [实战<1>:数据质量检查](https://blog.csdn.net/shunqixing/article/details/80045189?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)