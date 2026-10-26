# The App Category That Looks Profitable Because Google Owns It

Dataquest guided project, *Profitable App Profiles for the App Store and Google Play Markets*. Datasets: 10,841 Google Play apps and 7,197 App Store apps, scraped in 2018 and published on Kaggle.

## The recommendation being checked

The brief: find an app profile that would do well on both stores, for a company making free ad-supported apps. The usual conclusion is to **turn a popular book into an app**, because the books category ranks highly on average installs.

It does. Here is what that average is made of.

## Findings

### 1. The books recommendation is backwards on both platforms

| | Google Play | App Store |
|---|---|---|
| Rank by mean | 11 of 33 | 6 of 23 |
| **Rank by median** | **25 of 33** | **21 of 23** |
| Median outcome | 50,000 installs | 422 ratings |
| Biggest app's share of category | 60.0% | 45.3% |

**On Google Play the top 6 of 190 apps hold 84.6% of all installs in the category.** They are Google Play Books (preinstalled on Android), Amazon Kindle, Wattpad, the Bible, Audible and Wikipedia: the platform owner, the largest bookseller on earth, a religious text and the free encyclopedia.

A new free ad-supported book app is not competing with the median of that category. It is entering a market where nearly nine installs in ten already belong to six incumbents with content libraries it cannot match.

The App Store is starker: the Book genre has 14 free English apps and a median of **422 ratings**.

### 2. Why the mean fails on this data

Every category's mean sits far above its median. Communication averages 38.5M installs against a median of 500,000, a factor of **77**. The categories topping the mean ranking are the ones most owned by one app: News and Magazines takes 42.2% of its total from a single app, Travel and Local 34.5%.

On the App Store the same pattern appears on tiny samples: Navigation ranks first on **six apps**, 66.8% of its ratings from one; Reference second on 18 apps, 73.1% from one. Not genre findings, just large apps with a label attached.

**A mean install count answers "how big is the biggest app here?", not "how would a new app do?", which is the question the brief asks.**

### 3. Three data problems

1. **A malformed row.** Row 10472 is missing its Category, so every later field shifted left, giving an app a rating of 19 on a five-point scale.
2. **1,181 redundant rows.** 798 app names appear more than once; ROBLOX appears nine times. Deduplicated by keeping the row with the most reviews.
3. **`Installs` is not a number.** 21 distinct values across 9,659 apps, because Google publishes buckets. Reading "1,000,000+" as 1000000 takes the lower bound of a bucket running to the next one, so every figure understates by an unknown amount and medians are coarse, with many categories tied at exactly 1,000,000.

## What I would not claim

- **Installs are not revenue.** For an ad-supported app what matters is engaged sessions, retention and ad rates, none of which are here.
- **The two platforms measure different things.** Google Play gives bucketed installs, the App Store gives rating counts. Rankings are computed separately and never combined.
- **Bucketing limits precision throughout.** The median comparison is directionally sound; the exact figures should not be read closely.
- **These are 2018 scrapes,** predating substantial changes to both stores.
- **Neither file is the full catalogue,** and nothing states how the sample was selected.
- **The English filter is a heuristic** allowing up to three non-ASCII characters, so it keeps emoji titles and still misclassifies some apps.
- **Category labels are developer-assigned** and inconsistently applied.

## What I would actually recommend

Nothing in this data identifies a profitable app profile, and that is the finding rather than a failure.

It does support a negative: **avoid categories where one incumbent holds most of the installs**, because the headline average there measures someone else's moat. By that standard books is among the worst available choices, not the best.

A real version needs per-app revenue or engagement, the full catalogue, and a measure of how recently entered apps performed.

## Files

- `notebook.ipynb`: full analysis, executed, with two charts.

## Stack

Python standard library (csv, statistics, collections), NumPy, Matplotlib. No pandas.