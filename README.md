# wordle-5-letter-word-stats

## Introduction
With Wordle fever everywhere, and the usual Wheel Of Fortune `RSTLNE` and `CDMA` techniques not quite working, I sought out to analyse the probability distro of letters within *exactly* 5-letter English words.

Using ~0.3333M most frequent words in English - thanks to Rachael Tatman on Kaggle, based on Norvig's Google Corpus, I made a frequency distribution to:
- find out what letters are the most frequent; and
- find out what words would help the most -- in *approximate* order of descending frequency (constrained by actual words - we can't do `AEOIS`!) when deployed on the first 2 lines in Wordle.
(and honestly, we don't need obscure words like `ZYMIC` which probably won't show up as a Wordle answer anyway).

Source: Tatman, R. (2017). Kaggle: English Word Frequency, ⅓ Million Most Frequent English Words on the Web. https://www.kaggle.com/rtatman/english-word-frequency

## Simple Python...
Here we go... with simple CSV splitting and header skipping (no point in an `import csv`), and `Counter` doing most of the hard work...

    from collections import Counter
    freq = Counter()
    with open('../input/english-word-frequency/unigram_freq.csv') as fn:
        for l in fn:
            [word, count] = l.lower().split(',')
            if count == 'count':
                continue
            if len(word) == 5:
                freq.update(word)
            
    print(freq)

## Results
    Counter({'a': 21942, 'e': 18907, 'o': 14627, 'i': 13749, 's': 13683, 'r': 12185, 'n': 11447, 'l': 10375, 't': 9856, 'c': 7422, 'd': 6970, 'm': 6957, 'u': 6806, 'h': 5633, 'g': 5584, 'p': 5511, 'b': 5003, 'k': 4966, 'y': 4617, 'f': 3208, 'v': 2597, 'w': 2391, 'z': 1868, 'j': 1485, 'x': 1456, 'q': 420})
    
Hence, fair bets for the first three entries are:
`SIREN`
`ACOLD`
`THUMP`


Good luck - feel free to reuse the code and/or analysis.

(NB: if you end up publishing or expanding on this, a citation to this MD file will be nice, thanks!).
