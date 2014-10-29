# [Ten Things You Didn't Know Git And GitHub Could Do][title]

### commits by range: `master@{time}..master`
You can create a compare view in GitHub by using the URL `github.com/user/repo/compare/{range}`. Range can be two SHAs like `sha1...sha2` or two branches name like `master...my-branch`. Range is also smart enough to take time into consideration. For example, you can filter a list of commits since yesterday by using format like `master@{1.day.ago}...master`.

```html
https://github.com/rails/rails/compare/master@{1.day.ago}...master
```

### commits by author: `?author=github_handle`
You can filter commits by author in the commit view by appending param `?author=github_handle`. For exmaple, the link `https://github.com/dynjs/dynjs/commits/master?author=jingweno` shows a list of my commits to the Dynjs project:

### `.diff` & `.patch`
Add `.diff` or `.patch` to the URLs of compare view, pull request or commit page to get the diff or patch in text format. For example, the link `https://github.com/rails/rails/compare/master@{1.day.ago}...master.patch`

### line linking
In any file view, when you click one line or multiple lines by pressing SHIFT, the URL will change to reflect your selections. This is very handy for sharing the link to a chunk of code with your teammates.

### autolink
In pull requests, issues or any comment, sha and issue number (#1 for example) will be automatically linked. Besides, you can link sha or issue number from another repository with the format of `user/repo@sha1` or `user/repo#1`





[title]: http://owenou.com/2012/01/13/ten-things-you-didnt-know-git-and-github-could-do.html
