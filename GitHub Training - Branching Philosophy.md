---
type: documentation
---

## Prerequisites
Below are the requirements that are expected to be known before we move ahead with this documentation,
- Git
- Commits
- Merging
- Rebase
-  Branching

## Basics of Branching
This was covered in [[GitHub Training - Branches]] please refer to that training.

## Different Workflows
There are mainly three different types of workflows that we will be considering and taking inspiration from,
1. Centralized Workflow
2. Feature Branch Workflow
3. Our Workflow

Let's look at them in detail.

### Centralized Workflow
In this workflow developers start by cloning the central repository. In their own local copies of the project, they edit files and commit changes as they would with their code; however, these new commits are stored locally - they're completely isolated from the central repository. This lets developers defer synchronizing upstream until they're at a convenient break point.

#### Example

1. Say we have a team of developers, and one of the developers, John is working on feature on his local codebase,

**![](https://lh7-us.googleusercontent.com/QPylk0VtERqn5MkqZf41MB-mp3f0W63wU98DuW4mNUiSR8CuE4H6WQHVqIFUGScYu8Gh3lMx6JR2qqclTB_LqmQSBZGpJ8otLk8XCj1lMyGRBgNRBeQDyD04L32cdKBnNiKaQtPGb0FE38tC2BsPrh_e0g=nw)**

2. After that say Mary, one of the other developers starts working on her own feature.

**![](https://lh7-us.googleusercontent.com/cGmQ-sSyX8m3V-mDY5chUVOyi4DRLsG8KPyC5jcBMz9KTzx9tfnApjFR1JfHPG-yZSqzTk6SjWv9hZGMC5twJT8iLiL_YppezTunrSXgXwSzgiqWuLREJmBqDFF5ISD5-UxIKmQB88xAv45mLttxXkD5YQ=nw)**

3. John is done with his feature and so he publishes his feature onto the upstream server.

**![](https://lh7-us.googleusercontent.com/r1wf0Rqq_kLaz5xkxkyBmOX4JJGWJWDtVg5TwVoRakCXN9XBOqfkcJ-R14a6u5eYLuOcIGIK0aBRMX_VzWpzqRLJ205ZB3oTaxsjNhOnQv6lHYjIYvO8doIxQewVJw6onqF5DX03nqhEsKKT51v2Kp3UOQ=nw)**

4. Everything is fine at this point, until Mary decides to also publish her feature. It fails because her local codebase and the upstream server's codebase are out of sync because of John pushing his code before Mary.

**![](https://lh7-us.googleusercontent.com/z17x0yxb5H-kGxszlAgG-7y6f-qfEMAWsaiHqaq8lIRuufY1IKfPr3kRXxIqcK-2SYi5gX2r0zljRT4VGGHjY17vySjilVU_0VOEma2AcJLU5hLOJfGYBidQfcYhG4_N-ZUQLyKPR7xiW7qS4hF5At9Vag=nw)**

5. So now marry has to rebase on top of John's Commit(s) to make sure that her local codebase is in sync.

**![](https://lh7-us.googleusercontent.com/K_56YAH_rtrh_etI9xBlp-rTXcOu7dCnZLAlC1rkCbgM7Gs9000ynf81R2W_-DhlWpfyVCUehAXwaqGS08dGdrZKvaeucg7nj1MQKsdMlgERf0U4YY8agjQ4M5puyk3sEEAPTj-0NZ-t0hNmkqsI4EU8Lw=nw)**

6. This is how it looks like,

**![](https://lh7-us.googleusercontent.com/xus3eqp11hIW6EXRc55aVwjnZ10nmOAXBC0KjMsJjAu-Wt7GCFT2z2I4DsSODEGGjR28-mEi5BDprwOaxhdBl3_Pm_ob5YAu3hyJemnASTLSO4ZKpfgrLtLEaDTFlwUZ2mN6dkr9FcVGQa8yCPGujykrAg=nw)**

7. And this will be the final result of the branching tree,

**![](https://lh7-us.googleusercontent.com/ejst5PfVqHA4pCJDsiqBl4rb6rfLuW4yRiV1N9Mvy6RiUB-8voJcHpCmjxadhoBpHSEG1LMg5aiT3kKgmk_Yq7YB7Y7S6KlmuOVSX-M79778vbBUbYCtidxkPOi5w7gQzWwV3Ifjpknffl8OH682RnLHfA=nw)**


#### Limitations
- Two people cannot work at the same time.
- This method is very prone to merge conflicts.
- Anyone can commit to any branch, which might be live into production.
- Increase dependency on other teams.

### Feature Branch Workflow
The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the main branch. This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the main branch will never contain broken code, which is a huge advantage for continuous integration environments. They give other developers the opportunity to sig off on a feature before it gets integrated into the official project.

#### Example
Here we can see that we branch off to create a new branch that we call the `feature branch` which is eventually merged back into the `prod branch`.

**![](https://lh7-us.googleusercontent.com/JHVqjfXD7tchTpp2jfGJALWQM3P6DETbzqOfr3bXwj8_wAWOWixrLzc0pdCEhjCXKu6LzU7AWDt26z0iBndzyb83t5ptvq4KRp-y4ckHkseqHmUI7xx3fOvpCYzyecFmjAgLwy7crj2OwhHcBOVtoUJwaA=nw)**

This is how a basic Feature Branch workflow works.

#### Limitations
- It does not accommodate for multiple environments.
- Higher risk of multiple/duplicated merge conflicts.
- It does not have the concept of *release* branches which means everything is pushed directly to production.