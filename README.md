# LinkBook

收录和展示你喜欢的内容链接

## 使用

### 发布链接

你可以在 `data` 目录下的`linkcard-{$date}.json`文件中写下你要展示的内容链接

`{$date}` 是内容链接要展示出来的时间，比如`linkcard-21230601.json`只会在2123年6月1号开始展示出来

因此你可以提前把你准备好的内容链接全部放在 data 文件夹下，通过设置 {$date} 来实现要在哪一天开始可见，而不用发布时才填写 `json` 文件

### linkcard-{$date}.json
```json
[
  {
    "content_title": "linkbook 收录和展示优质内容的链接",
    "content_url": "https://github.com/kaiqiangzhao/linkbook",
    "content_description": "很多的 newsletter 都是推荐自己阅读的内容，你可以通过 linkbook 来收录和展示你喜欢的优质内容链接",
    "published_date": "2023-07-10",
    "user_nickname": "linkbook",
    "user_url": "https://github.com/kaiqiangzhao"
  }
]
```
content_title: 内容标题

content_url: 内容链接

content_description: 内容描述

published_date: 内容发布时间

user_nickname: 用户昵称

user_url: 点击昵称跳转的链接

### 推荐

你也可以使用调查问卷接收用户的推荐

## 构建

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

## 技术栈

nuxt.js + tailwind css
