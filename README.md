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
| Kanji | Rank | Nb. of occ.| Frequency | Cum. Freq. |
|-------|------|------------|------------|-----------|
| 年    | 1    | 27 383 261 | 0.031909   | 0.031909  |
| 日    | 2    | 16 694 015 | 0.019453   | 0.051363  |
| 月    | 3    | 13 533 379 | 0.015770   | 0.067133  |
| 大    | 4    | 9 205 888  | 0.010728   | 0.077861  |
| 学    | 5    | 7 801 260  | 0.009091   | 0.086951  |
| 本    | 6    | 7 239 535  | 0.008436   | 0.095387  |
| 人    | 7    | 5 861 052  | 0.006830   | 0.102217  |

This trend can also be verified on the following graph (TREND GRAPH). If we have a look at the .csv, we can see that:
- 1 337 kanjis are only used once (6.7%):
- to cover \frac{1}{3} of the total use of kanjis, one only need to know 72 of them;
- to cover \frac{1}{2} of the total use of kanjis, one only need to know 165 of them;
- to cover \frac{9}{10} of the total use of kanjis, one only need to know 910 of them;
- Finally, to cover \frac{99}{100} of the total use of kanjis, one only need to know 2173 of them.
- 
\(\frac{1337}{20001}\)
\frac{1337}{20001}\

We will use this mark as a threshold and filter our list accordingly. The filtered list may be downloaded HERE.

## A new list: ordering the kanjis

Work In Progress
