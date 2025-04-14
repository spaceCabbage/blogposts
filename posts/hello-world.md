---
title: "Hello World"
slug: "hello-world"
date: "2025-04-14"
tags: ["first post", "development", "web design"]
cover: 
---

# Doon't Freak Out
> But welcome to my new blog

this is my new space where i will document my journey as a self-taught dev and wannabe blogger

i could not find a single `cms` that i liked, i wanted something simple, free, elegant. I dont really care about `SSG` or `SSR`, i just wanted to write stuff and put it on the internet.
This is why i decided on this approach.

Im using a git repo *stored on github's servers, all for free* and im maintaining an _index_ of all my blog posts written, also saved to that repo. All i have to do is write my blog posts in markdown format, _using neovim_, include them in my `index.json` with a title and a slug and push a commit

```json
// example blog index
[
    {
        "title": "My First Blog Post",
        "slug": "my-first-blog-post"
    }
]
```

this allows me to achieve a frictionless _content management system_ without having to mess around with a clunky cloud service that i have to buy into, i can move it all to gitlab or something if i wanted to, heck its just markdown and a `fetch()` request

## Attemting to render code blocks
id like for my blog to be able to render code blocks with syntax highlighting

this will require me to pick a theme, _write some code_ and even make a git commit
```js
console.log("is this highlighted?")
```

## I will now attempt a list

1. this is
2. a numbered lis
3. it shoudl render
4. as a `<ul>`

- and this is a 
- bulleted list
- which should render
- as a `<ol>`

### This is achieved using `markdown-it`, `front-matter` and `markdow-it-prism` (for code highlighting)


# I now want to try all the styles of text in `markdown-it` to see if i styled them correctly
## bold
__Bold Text__  
## italic text
*Italic text*
## blockquotes
> here is a multi  
> line blockquote
## hr
---
## links
link are like this [Duck Duck Go](https://duckduckgo.com)

## Images
![The San Juan Mountains are beautiful!](https://mdg.imgix.net/assets/images/san-juan-mountains.jpg "San Juan Mountains")
