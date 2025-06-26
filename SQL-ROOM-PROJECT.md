# Analyze Hacker News Trends

<img width="270" alt="image" src="https://github.com/user-attachments/assets/528e7a62-602e-4c56-8aed-6220b1553c0c" />

**Hacker News** is a popular website run by Y Combinator. It’s widely known by people in the tech industry as a community site for sharing news, showing off projects, asking questions, among other things.

In this project, you will be working with a table named `hacker_news` that contains stories from Hacker News since its launch in 2007. It has the following columns:

* `title`: the title of the story
* `user`: the user who submitted the story
* `score`: the score of the story
* `timestamp`: the time of the story
* `url`: the link of the story

→ Let’s get started!

**(1.)** Start by getting a feel for the `hacker_news` table!                           
Let’s find the most popular Hacker News stories:                           
* What are the top five stories with the highest `scores`?
```sql
SELECT title, score
FROM hacker_news
ORDER BY score DESC
LIMIT 5;
```
### 🟩Output 
```sql
| title                                                                        | score |
| ---------------------------------------------------------------------------- | ----- |
| Penny Arcade – Surface Pro 3 update                                          | 517   |
| Hacking The Status Game                                                      | 309   |
| Postgres CLI with autocompletion and syntax highlighting                     | 304   |
| Stephen Fry hits out at ‘infantile’ culture of trigger words and safe spaces | 282   |
| Reversal: Australian Govt picks ODF doc standard over Microsoft              | 191   |
```

