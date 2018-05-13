# 基于 Android 的英语学习 APP 的开发

**[摘要]** 全国大学英语考试，即 College English Test 是大学生在校期间才能参加的考试，主要分为 CET-4 和 CET-6 两种。通过这个考试的证书在大学生不论是找工作，还是考研，都有一定的帮助，并且可以使英语水平得到一定层次的进步。为了能够更好地准备这个考试，于是开发了一个基于 Android 的英语考试和练习 APP，能够方便用户随时随地做题和考试。并且为了使这个 Android APP 能够更好地运行，还开发了网页端用于题库管理。

**[关键字]** CET-4 CET-6 考试 练习 Android

>

# The Application of English Learning Based on Android

**[Abstract]** College English Test is only accept college student to take, which mainly include CET-4 and CET-6 levels.With passing this test, students will get more advance in getting a job or being Admitted for a graduate degree, furthermore, will make their english into the next level. For better preparing the College Englis Test, This Android based English learning App is developed, with this app, users can practice and test any time and any where. To make this app function, a website for exam management is developed.

**[Key Word]** CET-4 CET-6 Test Practice Android

# 目录

# 第一章 引言

## 1.1 论文研究背景与意义

四六级考试是在大学期间才能参与的考试，由于大学期间学业繁忙，很难对四六级考试有一个系统性的学习，于是最好的方法是进行针对性的练习，也就是多做题。传统的做题方式就是在卷子上做题，而如果能够增加在手机上做题这一方式，就增加了一种准备考四六级的方式。由于手机 app 的可编程性，能够比传统纸质试卷增加更多的可能性，比如及时反馈做题是否正确，在选词填空上也能够在选完词后看到比较完整的文章信息，并且听力部分也能够将听力按照题目切割并放置在更适合的位置，相对于传统考试时间是基于时间段的，手机端可以基于倒计时来进行。

>

为了能够跟方便地输入试卷信息，于是开发了网页端用于试卷的编辑。在试卷内容上，不仅可以自己输入试卷信息，还能够获取其他人输入的试卷，实现试卷资源的共享。

## 1.2 本课题研究内容与目标

在 Android 上开发软件主要是用 java 开发，但是考虑到如果要使用 java 开发的话，那么除了 Android 的开发方式要学习以为，在开发网页端的话还要学习一套网页端的开发方式，这样学习成本会大幅度增加，于是选用了现在比较新的 React Native 来开发 Android App，这样在开发网页端的时候使用 React 可以用比较相似的页面开发方式来开发，而不论是 React 还是 React Nativ 都是 MVVM 的开发方式，比起传统的 MVC 开发方式提高了不少效率。

>

由于 React 和 React Native 主要都是用来开发视图，所以还需要状态管理的工具来实现页面状态的管理，避免页面自己管理状态造成最后项目过于复杂难以维护，借助状态管理工具还可以较为方便地实现状态资源的共享，避免了较为复杂的页面组件之间的参数传递。常见的状态管理工具有 Redux 和 Mobx，本项目用在网页端使用 Redux，在移动端使用 Mobx，其中 Redux 主要代表着函数式地开发方式，而 Mobx 则是响应式的开发方式。

>

现在比较新的技术栈就是使用 React 开发网页端，使用 React Native 开发移动端，使用 Node.js 作为后端提供 Api 服务，本课题系统通过这样的技术栈来开发一个英语学习 App 来实现对四六级英语实现练习和考试的功能。为了实现这个四六级练习和考试 app，还要实现题库管理功能，考试结果保存功能，评分系统，来及时反馈练习结果以及记录考试成绩和答题信息。

# 第二章 相关技术介绍

## 2.1 React Native 简介

React Native 是 Facebook 开发的用于开发移动端的一个框架 js 类库，使得 Android 能够通过 javascript 开发移动端的应用，也就是说不仅可以开发 Android，还可以开发 ios。主要是通过把将 javascript 代码转码成对应平台的代码来实现的，也就是说在通过编写 javascript 代码然后转码成 java 代码来运行 Android 程序，这样的一个好处就是能够使用 javascript 的库，而 javascript 的库的数量在近些年来远远超过了其他平台的数量。在 javascript 和 java 之间在开发效率上可以说 javascript 远胜 java，在 javascript 经常见的 map、filter、reduce 等函数在用 java 开发 Android 的时候是不能用的。

>

React Native 除了在开发效率上能够大大地提高外，还能够实现多平台开发，在有 Mac OS 的环境下也可以把 React Native 项目编译成 ios 的 app，轻松实现多平台。

## 2.2 React 简介

React 是前端的一个类库，能够使用 jsx 来写页面，与状态管理工具 Redux 或 Mobx 能够实现 MVVM 的方式来开发前端页面，这个前端页面包括网页端也包括移动端，而 React 通过构建一个个组件来开发页面，这种组件化的开发方式在代码不断重构出一套套组件后可以调用组件，实现快速开发。

## 2.3 Node.js 简介

Node.js 通过使用 express 这样的后端框架，可以很快速地开发出想要的 api，并且通过与 mongoose 这样的工具在建立模型可以实现对于数据的基本验证，对于较为复杂的验证也可以自己写逻辑来实现，这样就能够实现对用户传送过来的数据进行校验和对应的反馈。

## 2.4 MongoDB 简介

MongoDB 是非关系型的数据库，这样就能够直接将较为复杂数据结构存进去，大大提高了开发效率，而不像关系型数据库那样需要建立多张表来实现一个较为复杂的数据模型。

# 第三章 系统分析

## 3.1 应用场景

要实现英语四六级练习与考试系统，就要实现试卷的制作，而很明显手机端并不适合试卷制作这一过程，于是需要在网页端中进行试卷制作。所以网页端需要完成以下的场景：

1.  通过注册登陆来实现对于自己的试卷的管理。
2.  试卷要能够输入四六级考卷的题目和答案。

在网页端制作了考卷之后，用户在手机端要能够进行以下的操作：

1.  注册登陆以便能够保存自己的考试的答题信息和成绩。
2.  能够对考卷进行练习，并及时反馈所选选项是否正确。
3.  能够进行考试，其中听力只能听一次，考试结束后给出成绩和答题情况，并能够保存答题情况。
4.  能够对过去做过的考卷及其答题情况进行查看和删除，其中考卷被修改或删除后，不能影响与该考卷相关的答题情况。

# 结论

# 致谢语

# 参考文献
