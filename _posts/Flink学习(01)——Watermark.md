# 什么是Watermark

Watermark是Apache Flink为了处理EventTime 窗口计算提出的一种机制,本质上也是一种时间戳，由Apache Flink Source或者自定义的Watermark生成器按照需求Punctuated或者Periodic两种方式生成的一种系统Event，与普通数据流Event一样流转到对应的下游算子，接收到Watermark Event的算子以此不断调整自己管理的EventTime clock。 Apache Flink 框架保证Watermark单调递增，算子接收到一个Watermark时候，**框架认为不会再有任何小于该Watermark的时间戳的数据元素到来了**，所以Watermark可以看做是告诉Flink框架数据流已经处理到什么位置(时间维度)的方式。

# Watermark的生成方式

Apache Flink 提供两种生成Watermark的方式，如下：

- Punctuated - 对应AssignerWithPunctuatedWatermarks接口，数据流中每一个递增的EventTime都会产生一个Watermark。
  在实际的生产中Punctuated方式在TPS很高的场景下会产生大量的Watermark在一定程度上对下游算子造成压力，所以只有在实时性要求非常高的场景才会选择Punctuated的方式进行Watermark的生成。
- Periodic - 对应AssignerWithPeriodicWatermarks接口，周期性的（一定时间间隔或者达到一定的记录条数）产生一个Watermark。在实际的生产中Periodic的方式必须结合时间和积累条数两个维度周期性产生Watermark，否则在极端情况下会有很大的延时。

所以Watermark的生成方式需要根据业务场景的不同进行不同的选择。

AssignerWithPunctuatedWatermarks接口和AssignerWithPeriodicWatermarks接口都继承了TimestampAssigner接口

```java
/**
 * A {@code TimestampAssigner} assigns event time timestamps to elements.
 * These timestamps are used by all functions that operate on event time,
 * for example event time windows.
 *
 * <p>Timestamps are represented in milliseconds since the Epoch
 * (midnight, January 1, 1970 UTC).
 *
 * @param <T> The type of the elements to which this assigner assigns timestamps.
 */
public interface TimestampAssigner<T> extends Function {

	/**
	 * Assigns a timestamp to an element, in milliseconds since the Epoch.
	 *
	 * <p>The method is passed the previously assigned timestamp of the element.
	 * That previous timestamp may have been assigned from a previous assigner,
	 * by ingestion time. If the element did not carry a timestamp before, this value is
	 * {@code Long.MIN_VALUE}.
	 *
	 * @param element The element that the timestamp will be assigned to.
	 * @param previousElementTimestamp The previous internal timestamp of the element,
	 *                                 or a negative value, if no timestamp has been assigned yet.
	 * @return The new timestamp.
	 */
	long extractTimestamp(T element, long previousElementTimestamp);
}
```



* 测试不同key，没数据进来的key，会不会输出
* 测试相同key，没数据进来时，会不会输出
* 







# 参考资料

[Apache Flink 漫谈系列(03) - Watermark](https://yq.aliyun.com/articles/666056?spm=a2c4e.11155435.0.0.6c231b10qR07RT)