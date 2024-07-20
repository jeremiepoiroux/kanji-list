# A data-driven ordered list of Kanjis

When learning Japanese, kanjis are, soon after knowing Katakanas and Hiragana, one of the main time-consuming tasks. Many resources exist to learn (to write, to recognize or both) thousands of kanjis. However, as students may know and expect, the number of kanjis to learn and the order of the list is crucial. The state of the art about this topic is rather old, and many student still rely on learning the Kyoiku Kanjis (1 026 kanjis learnt in school) and the Jōyō Kanjis (1 110 kanjis learnt in high school) with a quite popular method: Remembering the Kanji (RTK), a 1977 book by James Heisig.

With this project, I would like to suggest a new list in order to mingle contemporary quantitative methods and learning goals. Note that this project will eventually fuel a scientific paper. If you are interested in publications on the topic, you may have a look at my [reading list](https://paperpile.com/shared/K-Kanji-f_misjmpWDUatUprdI4VzbQ).

## A new list: filtering the relevant kanjis

First of all, the task is to filter, from thousands of kanjis, a list with relevant (useful) kanjis. The most popular lists (from MEXT, RTK, JLPT, etc.) seem to have been filtered by popularity, although the criterias are unknown. They generally feature 2 000+ kanjis, a reliable number to read the majority of common texts (especially newspaper articles). Projects which try to objectify the filtering exist, like [Kanji Usage Frequency](https://scriptin.github.io/kanji-frequency/). Dmitry Shpika had a similar goal to us, which was providing answers to the following question: 
> "in which order should I learn Japanese kanji if I have a goal of reading some specific type of texts, e.g. news or fiction?".

For our project, we decided to analyse the Japanese Wikipedia, a large database of texts about various topics. Thus, we assume the use of a great number of kanjis. We tested our calculations on the 5 millions sentences of the [Japanese wiki dump sentence dataset](https://huggingface.co/datasets/AhmedSSabir/Japanese-wiki-dump-sentence-dataset) by Ahmed Sabir. For the project, we then used a complete dump of the Japanese Wikipedia, as of 2022.08.08. The dataset (.json), prepared by Inari Kami is available [here](https://huggingface.co/datasets/inarikami/wikipedia-japanese). For convenience, I transformed the .json into a .csv file (I will give access to it). 

Here are some basic stats about the Japanese Wikipedia dataset: 
- The total number of articles is 1 317 738;
- The number of occurences of:
  - kanjis, ie. all the 20 992 CJK Unified Ideographs (unicode `\u4E00` to `\u9FFF`), is 858 165 384 (44.68%);
  - katakana is 550 415 364 (26.35%);
  - hiragana is 505 859 344 (28.97%);
- The unique number of kanjis hits the limit of the CJK Unified Ideograph (20 992). 
Bonus: if we consider the CJK Unified Ideographs (20 992) as well as the characters in the CJK Extensions (97 870) and the CJK Compatibility Ideographs (1 054), the number of unique "kanjis" (actually, ideographs) would be 31 827.

The next step is to calculate the number of occurences of each kanji and the cumulative frequency. Here, I found the kanjis count fooled by two Wikipedia articles, which are (tadam), [Unicode一覧 6000-6FFF](https://ja.wikipedia.org/wiki/Unicode%E4%B8%80%E8%A6%A7_6000-6FFF) and [CJK統合漢字 (6300-77FF)](https://ja.wikipedia.org/wiki/CJK%E7%B5%B1%E5%90%88%E6%BC%A2%E5%AD%97_(6300-77FF)). As a result, the number of unique Kanjis used in the Japanese Wikipedia excepted in the mentioned articles is 20 001. We now have a [.csv file](https://github.com/jeremiepoiroux/kanji-list/blob/main/japanese_wikipedia_2022_kanjis_count.csv) with five columns, the kanjis, the rank (based on the number of occurences), the number of occurrences, the frequency of use and the cumulative frequency. The file is ordered by rank.

As a prelimenary interesting insight, to cover 10% of the total use of kanjis, one only need to know 7 of them. In other words, to know 7 kanjis should be enough to read 10% of the kanjis used in a text:
| Kanji | Rank | Nb. of occ.| Frequency | Cum. Freq. |
|-------|------|------------|------------|-----------|
| 年    | 1    | 27 383 261 | 0.031909   | 0.031909  |
| 日    | 2    | 16 694 015 | 0.019453   | 0.051363  |
| 月    | 3    | 13 533 379 | 0.015770   | 0.067133  |
| 大    | 4    | 9 205 888  | 0.010728   | 0.077861  |
| 学    | 5    | 7 801 260  | 0.009091   | 0.086951  |
| 本    | 6    | 7 239 535  | 0.008436   | 0.095387  |
| 人    | 7    | 5 861 052  | 0.006830   | 0.102217  |

This trend can also be verified on the following (basic) graph:

<img src="https://github.com/jeremiepoiroux/kanji-list/blob/main/kanji_trend.png" alt="Kanji Occurrences Trend" width="500">

If we have a look at the .csv, we can see that:
- 1 337 kanjis are only used once (6.7%):
- to cover 33% of the total use of kanjis, one only need to know 72 of them;
- to cover 50% of the total use of kanjis, one only need to know 165 of them;
- to cover 90% of the total use of kanjis, one only need to know 910 of them;
- Finally, to cover 99% of the total use of kanjis, one only need to know 2 172 of them.

We will use this threshold to filter our list accordingly. The filtered list may be downloaded [here](https://github.com/jeremiepoiroux/kanji-list/blob/main/japanese_wikipedia_2022_kanjis_count_99.csv).

As a second step, we may now proof-test the list with regard to Patrick Kandrac's [work](https://www.japanesestudies.org.uk/ejcjs/vol22/iss2/kandrac.html) which resulted in a [comparison](https://www.reddit.com/r/LearnJapanese/comments/rji33t/ultimate_kanji_frequency_list/) of the frequency rank of kanjis in seven databases, augmented by one average frequency and two weighted frequencies columns. I compared the rank of the frequency of kanjis in the Japanese 2022 Wikipedia with all the 10 dabasets, first with the mean of the differences of frequency of all kanjis, then with the mean of the ratio of frequency of all kanjis. Please note that form the merge of the two lists (mine with 2 172 kanjis, Patricks with 2 242), the comparison is effective on 1 977 kanjis. Although our list is only quite similar to the "Kanji Database" with the Mainich Newspaper (2000-2010) as a source, the ratios mean makes it close to Patricks calculations (AVG FREQ, FREQ (1) and FREQ BIG 5). We might suggest this speaks for the quality of the database we rely on.

|        | Google | KUF   | MCD    | 文化庁  | jisho.org | KD   | WKFR | AVG FREQ | FREQ (1) | FREQ BIG 5 |
|--------|--------|-------|--------|--------|-----------|------|------|----------|----------|------------|
| diff. mean | -15.26 | -49.18| -148.75| -21.72 | -11.21    | -2.44| -6.51| -36.44   | -34.17   | -53.07     |
| ratio mean | 1.24   | 0.96  | 0.88   | 1.14   | 1.17      | 1.17 | 1.17 | 0.97     | 0.98     | 0.97       |

Third, we add some information to the .csv and calculate some basic statistics. We use the [kanjiapi](https://kanjiapi.dev/) by Iridium Szreter to add the meaning of each kanji, as well as its Heisig keyword, readings, unicode, stoke count, JLPT level (from 5 to 1) and school grade level (from 1 to 6 for primary school and 8 for high school). For comparison with other databases, we keep Patricks measures.



## A new list: ordering the kanjis

Work In Progress
