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

<br/>

## Day 2: Includes (100 points)

### Description
> Can you get the flag? Go to this website and see what you can discover.
### Hint
> Is there more code than what the inspector initially shows?

### Solution
On visiting the challenge, we see:
```
Many programming languages and other computer files have a directive, often called include (sometimes copy or import), that causes the contents of a second file to be inserted into the original file. These included files are called copybooks or header files. They are often used to define the physical layout of program data, pieces of procedural code and/or forward declarations while promoting encapsulation and the reuse of code.
```


Let's open our handy web developer tools and inspect the HTML. No parts of the flag are within this file. However, we do see that there is a stylesheet linked. Let's go to the style editor and look at `style.css`.

Inside the CSS file, we indeed do see part of the flag. 1of2 tells us there is another part of the flag left to be found.
```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```

The webpage also had scripting for the "Say hello" button so let's also check out the `script.js` file.

```js
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_b8f4b022}
```

We can combine the first part and the second part of the flag for the full flag!

<br/>

## Day 3: ...