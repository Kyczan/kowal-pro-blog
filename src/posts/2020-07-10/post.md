# Creating your static markdown blog

![blog](./assets/2020-07-10.jpeg)

As a JS developer sometimes I need to run away from JS in my projects. In this way I created this static blog where posts are written in [markdown](https://en.wikipedia.org/wiki/Markdown) syntax.

On server there are only `.html` files (and some assets). NO JS (with little exception for tracking pixel). Thanks for this, site is extremely fast. No `xhr` requests.

Of course I could just use some online markdown converters. Write post, paste to converter, download `.html` file, upload it to server... No. I like when entire process is fully automated. This is how `kowals-static-blog-generator` was born.

## Static blog generator

There are [plenty](https://www.staticgen.com) of static blog generators. But I wanted to make my own. For fun.

`kowals-static-blog-generator` can be found on [github](https://github.com/Kyczan/kowals-static-blog-generator) and can be installed via [npm](https://www.npmjs.com/package/kowals-static-blog-generator).

## Creating new blog

tl;dr - check out working example - [this blog repo](https://github.com/Kyczan/kowal-pro-blog)

### Initial setup

First open terminal, create new blog directory, initialize npm project inside and install `kowals-static-blog-generator`:

```sh
mkdir my-blog
cd my-blog
npm init -y
npm i -S kowals-static-blog-generator
```

Next open `package.json` and add following script in script section:

```json
"scripts": {
  "build": "kowals-static-blog-generator ./src ./dist"
},
```

Now you are able to run following command from terminal

```sh
npm run build
```

Everything what it does - it takes files from `./src` directory, converts to static `.html` files and put them to `./dist` folder.

### `./src` setup

`./src` folder is a place where your blog files live. Structure of this folder should look like this:

```
src/
  |- assets/
  |    |- some-photo.png
  |    `- styles.css
  |
  |- layout/
  |    |- includes/
  |    |    |- _footer.pug
  |    |    `- _header.pug
  |    |
  |    |- layout.pug
  |    `- post.pug
  |
  |- pages/
  |    |- blog.pug
  |    `- index.pug
  |
  `- posts/
       |- 2020-07-04/
       |    |-assets/
       |    `-post.md
       |
       `- 2020-07-10/
            |-assets/
            `-post.md
```

Let's take a closer look:

- `assets/` - there live files that should be copied to `./dist` folder without modifying.
- `layout/` - contains general structure of page written with `.pug` template engine.
- `pages/` - `.pug` files that extends `layout.pug` - they will be translated to `.html` and copied to `./dist`.
- `posts/` - finally - blog posts written in markdown. Every post should be in folder describing its date of creation. Note that every post should be named `post.md`. Layout of post is extended from `post.pug`. Every image related to post can be placed into `assets/` in post directory.

### `./dist` generation

After run `npm run build` command there will be created `./dist` folder with target files:

```
dist/
  |- assets/
  |    |- some-photo.png
  |    `- styles.css
  |
  |- posts/
  |    |- assets/
  |    |- 2020-07-04-some-title.html
  |    `- 2020-07-10-another-title.html
  |
  |- blog.html
  `- index.html
```

This files can be uploaded directly to the server. You can do this manually (like caveman) or automate whole process. But this is another story.
