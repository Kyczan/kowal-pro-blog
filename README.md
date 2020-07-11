# kowal-pro-blog

Welcome to my personal blog site repo!

This is static blog. Structure of site is created with `.pug` templates. Content of blog posts is written in markdown.

To produce static `.html` files I'm using [kowals-static-blog-generator](https://github.com/Kyczan/kowals-static-blog-generator) - small utility written by [me](https://github.com/Kyczan) in JS that converts `.pug` and `.md` files to static `.html` site.

Every push to `master` triggers github action that prepares entire blog and deploys to my server. Result can be observed under [kowal.pro](https://kowal.pro) website.
