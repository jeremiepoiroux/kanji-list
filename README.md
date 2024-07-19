# A data-driven ordered list of Kanjis

When learning Japanese, Kanjis are, soon after knowing Katakanas and Hiragana, one of the main time-consuming tasks. Many resources exist to learn (to write, to recognize or both) thousands of Kanjis. However, as students may know and expect, the number of Kanjis to learn and the order of these Kanjis are crucial. The state of the art about this topic is rather old, and many student still rely on learning the Kyoiku Kanjis (1 026 kanjis learnt in school) and the Jōyō Kanjis (1 110 kanjis learnt in high school) with a quite popular method: Remembering the Kanji (RTK), a 1977 book by James Heisig.

With this project, I would like to suggest a new list, meeting contemporary quantitative methods and learning goals. Note that this project will eventually fuel a scientific paper. If you are interested in publications on the topic, you may have a look at my [reading list](https://paperpile.com/shared/K-Kanji-f_misjmpWDUatUprdI4VzbQ).

## A new list: filtering the relevant kanjis

First of all, the task is to filter, from ten thousands of kanjis, a list with relevant (useful) kanjis. The most popular lists (from MEXT, RTK, JLPT, etc.) seem to have been filtered by popularity, although the criterias are unknown. They generally feature 2000+ kanjis, a reliable number to read the majority of common texts (especially newspaper articles). Projects which try to objectify the filtering exist, like [Kanji Usage Frequency](https://scriptin.github.io/kanji-frequency/). Dmitry Shpika had a similar goal to us, which was providing answers to the following question: 
> "in which order should I learn Japanese kanji if I have a goal of reading some specific type of texts, e.g. news or fiction?".

For our project, we decided to analyse the Japanese Wikipedia, a large database of texts about various topics. Thus, we assume the necessity of using a great number of kanjis. We tested our calculations on the 5 millions sentences of the [Japanese wiki dump sentence dataset](https://huggingface.co/datasets/AhmedSSabir/Japanese-wiki-dump-sentence-dataset) by Ahmed Sabir. For the project, we then used a complete dump of the Japanese Wikipedia, as of 2022.08.08. The dataset (.json), prepared by Inari Kami is available [here](https://huggingface.co/datasets/inarikami/wikipedia-japanese). For convenience, I transformed the .json into a .csv file (I will give access to it). 

Here are some basic stats about the Japanese Wikipedia dataset: 
- The total number of articles is 1 317 738;
- The number of occurences of:
  - kanjis, ie. all the 20 992 CJK Unified Ideographs (unicode `\u4E00` to `\u9FFF`), is 858 165 384 (44.68%);
  - katakana is 550 415 364 (26.35%);
  - hiragana is 505 859 344 (28.97%);
- The unique number of kanjis hits the limit of the CJK Unified Ideograph (20 992). 
Bonus: if we consider the CJK Unified Ideographs (20 992) as well as the characters in the CJK Extensions (97 870) and the CJK Compatibility Ideographs (1 054), the number of unique "kanjis" (actually, ideographs) would be 31 827.

The next step is to calculate the number of occurences of each kanji and the cumulative frequency. Here, I found that the kanjis count was fooled by two Wikipedia articles, which are (tadam), [Unicode一覧 6000-6FFF](https://ja.wikipedia.org/wiki/Unicode%E4%B8%80%E8%A6%A7_6000-6FFF) and [CJK統合漢字 (6300-77FF)](https://ja.wikipedia.org/wiki/CJK%E7%B5%B1%E5%90%88%E6%BC%A2%E5%AD%97_(6300-77FF)). As a result, the number of unique Kanjis used in the Japanese Wikipedia excepted in the mentioned articles is 20 001. We now have a .csv file with five columns, the kanjis, the rank the rank (based on the number of occurences), the number of occurrences, the frequency of use and the cumulative frequency. The file is ordered by rank.

An interesting insight, to cover 10% of the total use of kanjis, one only need to know 7 of them. In other words, 7 kanjis are enough to read 10% of the kanjis used in a text:
1. 年, 1, 27383261, 0.0319094253598775, 0.0319094253598775
2. 日, 2, 16694015, 0.0194533596856552, 0.0513627850455327
3. 月, 3, 13533379, 0.0157703038753285, 0.0671330889208613
4. 大, 4, 9205888, 0.0107275242348744, 0.0778606131557357
5. 学, 5, 7801260, 0.0090907260345288, 0.0869513391902646
6. 本, 6, 7239535, 0.0084361538139201, 0.0953874930041847
7. 人, 7, 5861052, 0.0068298221064452, 0.10221731511063

## A new list: ordering the kanjis

Work In Progress
