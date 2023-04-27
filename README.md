# Summary4dialogue
为AI爱家用户对话生成摘要

## 1.transformers算法
这部分基于transformers来完成文本摘要任务，产生的是生成式摘要，旨在尽可能保留文本语义的情况下将长文本压缩为短文本。本文用到了两个下面的模型：
* [T5](https://github.com/google-research/text-to-text-transfer-transformer)：将各种 NLP 任务都转换到 text-to-text 框架来完成的通用 Transformer 架构，要进行摘要任务只需在输入文本前添加 summarize: 前缀；
* [mT5](https://github.com/google-research/multilingual-t5)：微调T5模型后的可应用于多语言的模型

代码如下[transformers.ipynb](transformers.ipynb)，其中有一些关键参数：
* input_ids：这是模型的输入，通常是已编码为整数序列的文本。

* max_length：生成摘要的最大长度。如果希望生成的摘要包含更多信息，可以增加这个值。

* num_return_sequences：要生成的摘要序列数量。这里设为 1，表示只生成一个摘要。如果需要多个备选摘要，可以增加这个值。

* length_penalty：长度惩罚系数。值越大，生成的摘要越短；值越小，生成的摘要越长。如果需要更多信息，可以降低这个值。

* no_repeat_ngram_size：指定不重复的 n-gram 大小。增加这个值可以减少生成摘要中的重复词语，使摘要更加连贯。

* temperature：控制生成摘要的随机性。值越大，生成的摘要越随机；值越小，生成的摘要越接近训练数据。为了让生成的摘要更加连贯，可以降低这个值，但注意过低的值可能导致摘要过于接近训练数据。

* top_k：在生成摘要的过程中，每个时间步只考虑概率最高的前 k 个词。增加这个值可以让模型更加灵活地选择词语，但过大的值可能导致生成的摘要不够连贯。可通过实验找到一个合适的值。

通过调整这些参数，可以在一定程度上提高生成摘要的信息量和语义连贯性。针对不同长度的对话，其参数的最佳组合需要多次测试。

## 2.jieba分词算法
这部分基于[jieba](https://github.com/fxsjy/jieba)中文分词组件完成文本摘要任务，产生的是抽取式摘要，旨在不改变原文的情况下，通过对原文关键词和句子的重新排序组合来生成摘要。
代码如下：[jieba.ipynb](jieba.ipynb)

## 3.textrank算法
这部分基于[textrank](https://github.com/davidadamojr/TextRank)算法来完成文本摘要任务，产生的是抽取式摘要，旨在不改变原文的情况下，抽取原文中权重更高的关键句子作为摘要。
代码如下：[textrank_zhongwen](textrank_zhongwen.ipynb)
