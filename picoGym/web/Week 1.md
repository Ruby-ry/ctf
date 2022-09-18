# Week 1 of Web Challenges


## Day 1: where are the robots (100 points)

### Description
> Can you find the robots? https://jupiter.challenges.picoctf.org/problem/60915/
### Hint
> What part of the website could tell you where the creator doesn't want you to look?

### Solution
The title seems to hint at the ```robot.txt``` file, which is a file provided for web crawlers to determine what parts of the site they can access. This is usually used to prevent overwhelming your site. However, since it guides crawlers to only go to the pages you allow it to crawl to, sometimes people also put important info they do not want to be accessed by bots in this file as well!

I visited `https://jupiter.challenges.picoctf.org/problem/60915/robot.txt` and saw
```
User-agent: *
Disallow: /8028f.html
```

Given this info, `/8028f.html` is probably where the creator does not want us to look. Visiting `https://jupiter.challenges.picoctf.org/problem/60915/8028f.html` yields the flag!


For more info on robot.txt:
- https://www.robotstxt.org/robotstxt.html
- https://developers.google.com/search/docs/crawling-indexing/robots/robots-faq