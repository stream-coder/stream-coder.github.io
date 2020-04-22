The What, Where, When, and How of Large-Scale Data Processing

# 各章节介绍

本书分两个部分，每个部分四个章节，每部分结束后有一个独立的章节

* 第一部分：Apache Beam中的一些模型。主要介绍Apache Beam中的关于batch或streaming的high-level的模型。

  **第一章：Streaming 101**。包括stream processing的基本概念，定义一些术语，讨论了steaming system的能力，区分processing time和event time，最后审视一些通用的数据处理模式。

  **第二章：The What, Where, When, and How of Large-Scale Data Processing**。基于乱序数据，详细介绍了健壮的stream processing system的核心概念。每个场景，都使用基于具体用例的动图来强调时间维度的重要性。

  **第三章：Watermarks** 。它提供了对临时指标的进度进行深入的度量，以及它们是如何创建的、它们如何通过管道进行传播。

  **第四章：Advanced Windowing**。接着第二章，深入介绍windowing和triggering的高级概念，例如基于处理时间的窗口，会话和continuation triggers。

第五章：Exactly-Once and Side Effects。列举了实现端到端的exactly-once处理语义面临的挑战，并介绍了Apache Flink、Apache Spark及Google Cloud Dataflow在实现exactly-once的一些细节。

* 第二部分：Streams and Tables.



# 第一章 Streaming 101













