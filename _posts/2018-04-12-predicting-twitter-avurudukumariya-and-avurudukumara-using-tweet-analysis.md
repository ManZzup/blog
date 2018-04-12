---
title: 'Predicting Twitter #AvuruduKumariya and #AvuruduKumara using tweet analysis'
layout: post
subtitle: 'In order to make the official Twitter #AvuruduLK games interesting to me,
  I decided to try  predicting Twitter #AvuruduKumariya and #AvuruduKumara using tweet
  analysis'
image: http://manzzup.github.io/blog/public/images/3/kumari1.png
---

Hey,

I was bored and thought of making this #AvuruduLK thing a bit interesting for me. (Obviously the games doesn't interest me enough). What I wanted was to grab tweets that are related to the above contest, and try to predict the winners of the two. And if possible to derive further insights, or to provide explanations if the statistics are mismatching.


## TL;DR
### Avurudu Kumariya - **@WindDesika**

![Ranked using the "All Score" metric](/public/images/3/kumari1.png)

### Avurudu Kumara - **@MaaluPaan**

![Ranked using the "All Score" metric](/public/images/3/kumara1.png)


## Further analysis

Let's see how I calculated the above metrics. Simply it's the amount of influence a particular competitor have with regarding the particular hashtag.

ex: @WindDesika
The score includes original tweet count, retweet and favourite counts. Re-tweets were not counted separately as tweets. 

Next, I wanted to see a clear breakdown of the overall score, in order to derive a better one. (Hopefully a waited sum that would give lower weights to retweets and favourites but higher weights to original tweets).

#### The breakdown came as following for **Avurudu Kumariya**

![Score breakdown](/public/images/3/kumari2.png)

Once again, the winner is clear. But one interesting fact is, inclusion of *@katu_chooti* in the Top 5. From the final voters' page, it's clear that that handle is not a finalist. 

Interesting enough, the same happend at the next one.

#### The breakdown for **Avurudu Kumara**

![Score breakdown](/public/images/3/kumara3.png)

While the winner has not changed, the overall Top 05 has major changes. *@vishiru* and *@Aruna4udara* has slided into the Top 05, replacing 2 others that are mentioned as finalists in the voter page.

> One way to explain the above statistics is that the voters are not actively expressing their support. But it's also obvious that an active voter, would consider at least putting a "Favourite" to a tweet that's supporting his/her contestant.

**NOTE**  
This is done just for my own curiosity and boredom. ALL data used in this are public data and if you have any issues with this, deal with it yourself. But in case you don't want your twitter handle displayed here, let me know.