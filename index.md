---
layout: page
title: Recent trends in gender issues
subtitle: Seeking for contrasted opinions
cover-img: /assets/img/FLAG.jpeg
thumbnail-img: /assets/img/FLAG.jpeg
share-img: /assets/img/FLAG.jpeg
use-site-title: true
---

## Understanding our motivation...

Gender norms are social principles that govern the behavior of all of us in society and restrict our gender identity into what is considered to be appropriate. These are neither static nor universal and change over time, and can result in inequalities.


[LGBT](https://en.wikipedia.org/wiki/LGBT_community) issues are  extremely present in public life, with emerging pride movements and pure gender questioning. 
More and more countries have recently legalized and recognized same-sex marriage, sometimes following long legal procedures. In Switzerland, where we are based, this law was introduced in 2013, passed in 2020 by the parliament and adopted by referendum in September 2021. 
These topics have been increasingly present in the media all over the world, yet are still facing divergent opinions. In this review, we'll dive into this complex phenomenon, analyzing the different trends and opinions worldwide. 

### Available data

<img src="assets/img/wikidata_logo.png" alt="wikidata_logo" width="150" style="float:right"/>
We acquired data from [*Quotebank : A Corpus of Quotations from a Decade of News*](https://dlab.epfl.ch/people/west/pub/Vaucher-Spitz-Catasta-West_WSDM-21.pdf). It is a dataset of 178 million unique, speaker-attributed quotations that were extracted from 196 million English news articles crawled from over 377 thousand web domains between August 2008 and April 2020. However, our analysis was restricted from the start of 2015 to mid-2020. In addition, we used the free and open knowledge base *Wikidata* in order to get speaker's attributes such as nationalities, dates of births and occupations.

### Focus & Research questions 

We will focus on observing changes in the speakers’ opinions on the topics of gender equality and same-sex relationships, depending on their nationality, age, as well as occupation. It is also of interest to compare opinions within countries before and after national events, such as same-sex marriage legalization. This brings us to the following questions: 

- How legalization of same-sex marriage influenced the opinion of the authors of the quotes?
- Which features of the speakers mostly impact their sentiment regarding the LGBT community?
  * Which countries’ opinions significantly contrast with others?
  * Are artists more friendly to the LGBT community than LGBT activists?
  * Are older people really anti-LGBT ?
- Is it possible to predict speaker's attributes based on quotes ?

Before answering these questions, let's first visualize our dataset!

### First glimpse at the data

<!--- _(add bar plot)!_ -->
{% include years_distribution.html %}
Each year from 2015 to 2019 is composed of 20'000 to 50'000 quotes. The number of quotes in 2020 is below 10'000 as we only had access to a part of the year.
Most of the quotes are related to the LGBT community (~40%), whereas the feminism topic is a bit less represented (~6%). However, we had access to enough data to make a complete analysis of gender issues.

<!--- _(add bar plot)!_ -->
{% include gender_distribution2.html %}

While over 60% of the speakers are men and over 32% are women, the *Other* category represents about 6% which, in descending order of frequency, appears as: [transgender female](https://en.wikipedia.org/wiki/Trans_woman), [gender fluid](https://www.health.harvard.edu/blog/gender-fluidity-what-it-means-and-why-support-matters-2020120321544), [transgender male](https://en.wikipedia.org/wiki/Trans_man), [non binary](https://en.wikipedia.org/wiki/Non-binary_gender), [bigender](https://gender.fandom.com/wiki/Bigender), [genderqueer](https://www.webmd.com/a-to-z-guides/what-does-genderqueer-mean), [shemale](https://en.wikipedia.org/wiki/Shemale), [two-spirit](https://en.wikipedia.org/wiki/Two-spirit), [third gender](https://en.wikipedia.org/wiki/Third_gender).

The disparity between speakers can also be seen in their nationality and occupation distributions:

{% include occ_nats_dictribution.html %}

Americans and politicians are the ones talking the most about gender issues. Actors and journalists are also recurring occupations. Without surprise, LGBTIQ+ rights activists are also quite present.


Before taking a look at what our data can explain, let's get back to some programming concepts we will need in this analysis.

-----------------
## What is sentiment analysis ?

[Sentiment analysis](https://en.wikipedia.org/wiki/Sentiment_analysis), also referred to as opinion mining, is a classification technique which aims to analyze sentences to extract the expressed sentiment from them, and capture how positive or negative this statement is. In our analysis, the VADER library from [NLTK - Natural Language Toolkit](https://www.nltk.org) library was used and allowed to compute sentiment scores ranging from -1 to +1, corresponding to negative and positive extrema, respectively. In fact, the *compound* score was the one we selected and is the sum of positive, negative & neutral scores which is then normalized between -1 (most extreme negative) and +1 (most extreme positive). 
Sentiment analysis is thus a useful way to quantify a feeling from a text, but it is based on emotions rather than opinions.
Let's dive into research questions ! 

-----------------
## How legalization of same-sex marriage influenced the opinion of the authors of the quotes?

The first purpose of our analysis is to focus on a political aspect of same-sex relations, and in particular marriage legalization. We indeed believe that this legal process became popular in countries following people's agreement to integrate it into their public life. In this way, an increasing popularity of the same-sex mariage topic could correlate with legal outcomes.

To compare the average sentiment on same-sex marriage before and after its legalization, we picked countries where the number of quotes could allow basic statistical assessments, by picking only those with at least 100 quotes related to this topic.

The following table summarizes the data we used for our analysis:

| Country | Number of quotes | Legalization date |
|:-------:|:--------:|:---------:|
| United States of America (USA) | 4'173 | [07/2015](https://en.wikipedia.org/wiki/Same-sex_marriage_in_the_United_States) |
| Australia (AUS) | 1'869 | [12/2017](https://en.wikipedia.org/wiki/Same-sex_marriage_in_Australia) |
| United Kingdom (UK) | 797 | [03/2014](https://en.wikipedia.org/wiki/Same-sex_marriage_in_the_United_Kingdom) |
| Ireland (IRE) | 277 | [11/2015](https://en.wikipedia.org/wiki/Same-sex_marriage_in_the_Republic_of_Ireland) |
| Canada (CAN) | 259 | [07/2005](https://en.wikipedia.org/wiki/Same-sex_marriage_in_Canada) |

We plotted their respective sentiment score evolution versus time:

{% include interactive_legend.html %}

This figure alone does not allow to infer anything, apart from relative countries'means, if comparing a specific time point. Thus, for each of these countries, we separated the quotes in two splits: before and after legalization. Given United Kingdom and Canada did undergo legal procedures before 2015 the oldest datapoint we had accessed to - we could not assess anything regarding the trends in sentiment before and after the legalization in these two countries.

We could therefore compute the following statistics in order to answer our question: 

| Country | Average sentiment <br> (-1 to +1) | Sentiment progress following legalization | Significance |
|:-------:|:---------:|:---------:|:---------:|
| United States of America | +0.19 | -0.04 | 96% |
| United Kingdom | +0.22 | - | - |
| Australia | +0.24 | -0.05 | 92% |
| Ireland | +0.26 | +0.23 | 99% |
| Canada | +0.26 | - | - | 

Irish speakers are the ones showing the most positive sentiments about same-sex marriage. There are also the ones that progress (positively) the most in their sentiments after the legalization (with a significance of 99%). They are followed by Australians, who, on the contrary, show a slight reluctance after legalization (with a significance of 92%). Finally, Americans are also less positive about this new event (slight decrease in sentiment). Overall, it is interesting to note that between 2015 and 2020, all three countries'average are positive. However, it does not mean that all speakers have positive opinions on this topic, it might actually differ across years.

<img src="assets/img/Q1_merged_plot_with_density.png" class = "center">

The upper series of plots allows observing changes in sentiment scores when comparing the periods before and after same-sex marriage legalization. Contrasts are not always crystal clear. One should pay attention to the fact that these average curves reflect averages by quote rather than averages by month, which explains why these average lines do not always seem to be the mean of the corresponding sentiment curve. 

The lower series of plots shows the number of quotes per month, which can be interpreted as a popularity metric. This time, contrasts can be much more easily visualized, and a clear trend appears : the popularity of the same-sex marriage topic decreases straight after its legalization. On the other hand, conclusions regarding its effect on quotes' sentiment can hardly be assessed, as the effect of legalization at a country's scale does not seem to lead to strong opinion change. 

In this section, we focused on one specific event related to one sub-community of the LGBT community. Now, we would like to extend our analysis to the community as a whole. In this purpose, we will perform our sentiment analysis on a larger dataset, which includes all groups of LGBT community.    

-----------------

## Which features of the speakers have the most impact on their sentiment regarding the LGBT community ?  

As stated before, thanks to Wikidata, we had access to several speaker's features. These features, such as nationality, occupation and age, could cause  disparities between speaker'sentiments. Let's see what we get!


### Which countries' opinions significantly contrast with others ?

<embed type="text/html" src="assets/img/sentiment.html" width="800" height="600">
On the above map, you can interactively see how the sentiments on the LGBT community evolved in different countries within the world, year after year from 2015 to 2020. This can be done by clicking on the "Per year" button only. In 2020, it appears to be Russians, Americans, and Mexicans speakers that express the most positive sentiments (~0.3, 0.4 and 0.28 respectively). It is interesting to note that in 2015, thoses results were completely different, as these three countries expressed relatively neutral sentiments concerning LGBT community. However, it should be taken with a grain of salt as the dataset for this year was relatively lower than the previous ones. 
On the other hand, by selecting only the "mean" button, you can also display the average sentiment per country spanning across the five years.


### Are singers more friendly to the LGBT community than LGBT activists?

{% include median_mean.html %}

While the sentiments of different nationalities slightly differ, speaker occupations show major differences. This was also demonstrated through a [regression analysis](https://en.wikipedia.org/wiki/Regression_analysis), in which occupation was found to be the more important feature, before nationality and age.
On the graph, dots represent medians of sentiments for each year, lines represent the average with a 95% [confidence interval](https://en.wikipedia.org/wiki/Confidence_interval).
The politician's opinion has been the most stable in recent years. Judging by the difference between mean and median, opinions among politicians differ, while showing sharp negative statements.
The opinion of journalists did not change significantly over time, medians and averages do not differ much, which means that, on average, journalists coincide in opinion. Over time, attitudes of lawyers towards this topic have worsened, while those of film directors, on the contrary, have improved.
The wide confidence interval in 2020 demonstrates that attitudes towards this topic have become more diverse, which indicates a wide discussion in society. Singers and actors have the most positive attitude towards this topic, while lawyers speak out the most negatively.
LGBT activists, on the other hand, occupy an intermediate position. Most likely, this is due to the fact that they do not not only express words of support, but they also voice real problems in this area. These could be perceived by the algorithm as a negative statement.


Also, based on the [Kruskal-Wallis](https://en.wikipedia.org/wiki/Kruskal–Wallis_one-way_analysis_of_variance) test, it was demonstrated that the [p-value](https://en.wikipedia.org/wiki/P-value) for the distributions of sentiments depending on the occupation is extremely small, and therefore the medians of these samples differ significantly.

### Are older people really anti-LGBT? 

<center>
{% include gender_age.html %}
</center>
There is a stereotype that older people have a negative attitude towards the LGBT community. In addition, it is believed that men are dismissive of gender-related issues. The graph above shows the distribution of sentiments by gender (male, female and others) and age (under 40 - younger, from 40 to 60 years - boomers and over 60 years - older. However, having analyzed the distribution of sentiments in relation to age and gender, we can conclude that there is a significant similarity in the form of distribution of sentiments for people of different ages and genders. Taking into account the ideas already expressed about the characteristics of the speakers, we can come to the conclusion that neither gender, nor age, nor country of origin affects a person's opinion about gender issues (and possibly others) in the modern world, but the type of activity that the person chooses himself. Once again, this confirms the importance of eliminating discrimination based on age, gender and nationality.

-----------------
## Conclusion

Our data story tried to highlight the evolution of gender norms over time and how populations have accepted or not this new uderstanding of individual's identities. We started with a relatively gender-balanced database. However, in terms of country of origin and author's occupation, the United States and the politicians are highly represented. Our main tool for understanding the evolution of mentalities was sentiment analysis. This allowed us evaluating the evolution of feelings about same-sex marriage and seeing that the legalization of same-sex marriage has different impacts in different countries. These differences could be potentially due to cultural differences. On the other hand, we have studied the differences in feelings about the LGBT cause according to the occupation. Clear differences appeared between certain occupations such as actors being more positive than lawyers.
Thanks to these results, we can make a first panorama of the evolution of mentalities according to time, country and age of the people quoted.


-----------------
## Attempting a further step: could we predict an author's nationality based on a quote ?
#### WARNING: This section contains advanced programming content - read at your own risk.

Gender equality being an emerging and modern topic, more and more people discuss it, but not all of them are *famous*. 
In our dataset, 30% of speakers are not referenced in Wikidata, so we actually lost 30% of potentially meaningful and interesting data points given we were not able to relate such quotes with the parameters we were interested in. 
In order not to lose this part of the data, we desire to add synthetic features to these, by training a classification model. 
We expect to obtain such feature variables (nationality, age...) by using a neural network approach, trained with a set of quotes, where these feature labels were obtained from Wikidata, and which could eventually predict these from a further set of input quotes.

Firstly, we started by combining the [LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory) approach with a simple linear model to predict nationality and age of the quote’s author. 
We implemented it with a [PyTorch](https://github.com/pytorch/pytorch) framework, specified dataset’s classes, trained, and then extracted the model. 
For embedding, we used the [Twitter-roBERTa-base](https://pytorch.org/hub/pytorch_fairseq_roberta/) pretrained tokenizer. 
This model seemed too simple compared to real-life parameters, which let to only ~30% [F1](https://en.wikipedia.org/wiki/F-score) metric (harmonic mean of the precision and recall, that is positive predicted value and sensitivity)...

Hence, we decided to implement a more complex model: [GPT2](https://en.wikipedia.org/wiki/GPT-2), in order to predict the nationality of the speaker from its quote. 
At first sight, we got better results: ~70% on the validation set, as can be seen below.

{% include imbalanced.html %}

However, after checking the related [confusion matrix](https://en.wikipedia.org/wiki/Confusion_matrix), we found out that the model simply returns the most frequent value in nearly all cases. To counter this effect, we restricted our dataset to a “balanced” one, where all countries were represented by the same number of quotes in the training set, leading to the results below.

{% include conf.html %}

These results being actually worse and not improving, as we see by the validation loss plot below, we deduced this model is not sufficient to solve our concerns.

{% include balanced.html %}

It finally seems obvious that people’s minds are not only determined by their nationality, and neither is the reciprocal. 
Globalization being a key issue nowadays, which allows worldwide information flow and knowledge share, a single quote related to gender issues cannot be straight attributed to a nationality.
