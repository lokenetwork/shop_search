# 电商商品搜索引擎 #

PHP+MYSQL+redis 实现的高性能电商商品搜索引擎。支持同义词搜索，支持中英文数字混合搜索。

算法层面采用双向最大词匹配算法，字典的数据结构是hashset集合，文档倒排索引也是用hashset结构实现

对传统的算法实现进行了一些改良。

传统的正向或逆向最大词匹配算法实现，拆词拆到最后一个字的时候，会默认把这个单字作为一个词拆分出去，

这对电商商品搜索领域来说很不友好，所以我把这一步去掉了。

也就是说一个词无论是由单字符组成，还是多字符组成，它必须在字典里存在，它才能被认为是一个词。

这样实现之后，字典语料库就会变得格外重要。

但值得庆幸的是，语料库的可控性相对而言是比较高的，字典里少了哪些商品词汇，把缺的词汇加上就是了，可以在产品功能层面做一些设计，尽量快地发现缺失的词汇。

只要字典有足够的词汇，分词跟搜索的效果就会相当好。

在普通PC上的压测结果,10万商品数据，正常一个搜索请求，10毫秒左右返回结果。

![image](https://github.com/lokenetwork/shop_search/blob/master/picture/brower.png)

![image](https://github.com/lokenetwork/shop_search/blob/master/picture/ab_test.png)


