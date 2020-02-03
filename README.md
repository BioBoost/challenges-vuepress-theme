# VuePress Theme Challenges

Initial test of trying to create theme for VuePress for programming challenges for some of my courses.

## Setup

Install the theme

```bash
npm install --save vuepress-theme-challenges
```

Next add theme to config:

```js
module.exports = {
  title: '...................',
  description: '...................',,
  theme: 'vuepress-theme-challenges',
  themeConfig: {
  }
}
```

## Example

Add following front-matter to your challenge README:

```md
---
name: Biggest Number
description: Biggest number out of 3.
details: ./07_making_decisions/biggest_number/README.md
difficulty: Medium
solution: false
unitTests: true
keywords: operators
solved: false
notes:
---
```
