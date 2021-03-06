---
copyright:
  years: 2014, 2018
lastupdated: "2018-01-26"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# MongoDB - 体系结构最佳做法

在 {{site.data.keyword.cloud}} 上的部署中运用 {{site.data.keyword.mongodb}} 时，请使用以下最佳做法。如果您选择的是工程服务器，那么最佳做法中有若干项建议已经实施了。 

## 部署策略
在规划 {{site.data.keyword.mongodb}} 的部署时，您需要考虑几个重要的方面。最重要的是当前和预期的数据集大小。这两个方面是您选择各个物理节点资源需求的主要驱动因素，同时也是制定分片计划的参考依据。此外，还需要考虑数据的重要性以及对数据丢失或滞后可能性的容忍度（特别是在复制场景中）。 

## 内存大小
数据集位于内存中时，{{site.data.keyword.mongodb}}（就像很多面向数据的应用程序一样）运行性能最佳。没有什么比得上无需磁盘 I/O 的 {{site.data.keyword.mongodb}} 实例性能。请尽可能选择可用 RAM 大于工作数据集大小的平台。如果数据集超过单个节点的可用 RAM，请考虑利用分片。分片可增加集群中可用 RAM 的数量，以容纳更大的数据集，从而最大限度地提高部署的总体性能。缺页故障可能指示即将超过部署中的可用 RAM。您需要考虑增加可用 RAM。

## 磁盘类型
如果不考虑速度，或者如果拥有的数据集大于可用内存策略可以支持的大小，那么有适合您部署的磁盘类型非常重要。IOPS 是选择磁盘类型的关键。IOPS 越高，{{site.data.keyword.mongodb}} 的性能越好。如果本地磁盘在可能的情况下需要被用作网络存储器，就会导致部署等待时间长、性能不佳。建议将 RAID 10 用作磁盘阵列。

## CPU
如果要使用 map-reduce，那么应考虑时钟速度和可用处理器数。但是，运行 {{site.data.keyword.mongodb}} 实例时，如果大部分数据位于内存中，时钟速度会影响性能。如果系统是在这些情况下运行，并且您希望尽可能使每秒操作数最高，请考虑包含具有高时钟/总线速度的 CPU 的部署策略。

## 复制
复制可以在集群中一个节点出现故障时，提供数据的高可用性。建议在任何 {{site.data.keyword.mongodb}} 部署中至少复制三个节点。复制三个节点的最常见配置是 2x1 部署，即在单个数据中心中有两个主节点，备份服务器位于辅助数据中心。


## 分片
如果预计会有大型数据集，建议您部署分片的 {{site.data.keyword.mongodb}} 部署。可以使用分片对跨多个节点的数据集分区。{{site.data.keyword.mongodb}} 可以在集群中的各节点之间自动分发数据。或者，可以定义分片键，然后为该键创建基于范围的分片。分片有利于提高写入性能，因此就算数据集很小，但如果需要大量更新或插入操作，也可以进行分片。部署分片集时，{{site.data.keyword.mongodb}} 只需要三个配置服务器实例，这些实例是专用 Mongo 运行时，可跟踪当前的分片配置。丢失其中一个节点会导致集群的配置进入只读方式（仅限配置），并要求在所有节点都恢复联机后，才能进行配置更改。

## 写安全方式
有多种写安全方式可管理 {{site.data.keyword.mongodb}} 如何处理数据到磁盘的持久性。重要的是考虑哪种策略最适合数据完整性和性能需求。下面是可用的写安全方式：

* **无** - 提供非阻塞的延迟写入策略，有助于提高性能。但是仍存在较小的可能性节点会发生故障，数据可能会丢失。还可能出现的情况是，为了实现读一致性，写入集群中一个节点的数据不会立即在该集群中的所有节点上可用。“无”方式并未针对网络故障提供任何数据保护。这种方式非常不可靠，仅当性能优先并且不需要考虑数据完整性时才可使用。
* **正常** - 这是 {{site.data.keyword.mongodb}} 的缺省值。“正常”方式也是非阻塞的延迟写入策略。  
* **安全** - 阻塞，直到 {{site.data.keyword.mongodb}} 确认其已收到写请求，但在执行写操作之前一直保持阻塞。在“安全”方式下，集群内的数据完整性和读一致性水平更高。
* **日志安全** - 为 {{site.data.keyword.mongodb}} 提供恢复选项。“日志安全”方式可确保数据得到确认，并确保先执行日志更新，然后再返回日志。
* **Fsync** - 提供最高级别的数据完整性和阻塞，直到执行数据物理写入为止。使用 Fsync 会使性能降级，因此仅当数据完整性是应用程序的主要考虑因素时才可使用。

## 测试部署
10gen 有多种工具可帮助您对部署执行负载测试。控制台工具“benchrun”可以通过 JavaScript 测试装置运行操作。Benchrun 会返回每个操作的操作信息和等待数。如果需要有关 {{site.data.keyword.mongodb}} 实例的更多详细信息，请考虑在测试期间运行 `mongostat` 命令或 MMS 来监视部署。有关这些工具的更多信息，请参阅以下参考资料：

[MongoStat 概述 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://docs.mongodb.org/manual/reference/mongostat/){: new_window}

[10gen 的 {{site.data.keyword.mongodb}} 监视服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.10gen.com/products/mongodb-monitoring-service){: new_window}

## 安装
安装 {{site.data.keyword.mongodb}} 时，请考虑若干注意事项，以帮助创建一个以性能为导向的稳定的解决方案。10gen 建议您尽可能使用 CentOS（64 位）。避免部署在 32 位操作系统和 Windows 操作系统上。这些系统提供的部署平台不佳。32 位操作系统的文件大小限制可能会导致问题；如果 Windows 操作系统使用虚拟内存来弥补部署中的 RAM 不足，那么可能会导致性能问题。缺省情况下，{{site.data.keyword.cloud_notm}} 为所有工程服务器部署提供 CentOS 64 位操作系统。

此外，请确保对基本操作系统安装进行以下更改，以最大限度地提高性能：
* **将 SSD 预读的缺省值设置为 16 个块** - SSD 驱动器的搜寻时间非常出色，使“预读”缩小为 16 个块。旋转磁盘可能需要略微缓冲，所以这类磁盘设置为 32 个块。
* **noatime** - noatime 无需系统将正在读取的文件写入文件系统。这意味着访问文件的速度更快，磁盘磨损减少。
* **在 BIOS 中关闭 NUMA** - Linux、NUMA 和 {{site.data.keyword.mongodb}} 通常不会一起使用。如果要在 NUMA 硬件上运行 {{site.data.keyword.mongodb}}，建议将 NUMA 关闭（使用 interleave 内存策略运行）。如果不这样做，那么可能会出现速度大幅下降或系统 CPU 时间长等问题。
* **设置 ulimit** - 对于打开文件数，ulimit 设置为 64000，对于用户进程数，ulimit 设置为 32000。这些 ulimit 可防止因可用文件句柄数或用户进程数丢失而导致的故障。 
* **使用 ext4** - Ext3 分配文件（或除去文件）的速度慢。此外，ext3 的大型文件访问性能不佳。

**注：**缺省情况下，这些更改会在所有 {{site.data.keyword.cloud_notm}} 服务器上进行设置。

此外，建议日志卷和数据卷位于不同的物理卷。如果日志目录和数据目录位于一个物理卷上，那么对日志执行清空会导致 {{site.data.keyword.mongodb}} 部署中发生数据访问中断和延迟时间峰值。

## 操作
在 {{site.data.keyword.mongodb}} 部署升级到生产之后，请考虑若干项关于监视和性能优化的建议。 
* 确保在所有 {{site.data.keyword.mongodb}} 实例上运行 MMS 代理程序。这有助于监视部署的运行状况和性能。MMS 代理程序在支持交互期间会向 10gen 提供有用的调试数据。 
* `mongostat` 命令还提供有关 {{site.data.keyword.mongodb}} 节点性能的运行时信息。

如果这些工具中的任何一个工具发现性能问题，可以通过分片或索引来帮助更正这些性能问题。 

* 索引 - 如果监视工具指示基于字段的查询运行不佳，请为 {{site.data.keyword.mongodb}} 部署创建索引。为了帮助提高性能，请在查询基于不同字段的数据时始终使用索引。
* 分片 - 节点的总体性能因大型操作数据集而受到影响时，请使用分片。确保在达到阈值之前分片。仅对于插入或更新操作上的分片，系统会拆分区块。如果等待分片的时间过长，可能会出现分布不均的问题。 


