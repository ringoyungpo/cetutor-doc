# 基于 Android 的英语学习 APP 的开发 {ignore=true}

**[摘要]** 全国大学英语考试，即 College English Test 是大学生在校期间才能参加的考试，主要分为 CET-4 和 CET-6 两种。通过这个考试的证书在大学生不论是找工作，还是考研，都有一定的帮助，并且可以使英语水平得到一定层次的进步。为了能够更好地准备这个考试，于是开发了一个基于 Android 的英语考试和练习 APP，能够方便用户随时随地做题和考试。并且为了使这个 Android APP 能够更好地运行，还开发了网页端用于题库管理。

**[关键字]** CET-4 CET-6 考试 练习 Android

>

# The Application of English Learning Based on Android {ignore=true}

**[Abstract]** College English Test is only accept college student to take, which mainly include CET-4 and CET-6 levels.With passing this test, students will get more advance in getting a job or being Admitted for a graduate degree, furthermore, will make their english into the next level. For better preparing the College Englis Test, This Android based English learning App is developed, with this app, users can practice and test any time and any where. To make this app function, a website for exam management is developed.

**[Key Word]** CET-4 CET-6 Test Practice Android

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [目录](#目录)
* [第一章 引言](#第一章-引言)
	* [1.1 论文研究背景与意义](#11-论文研究背景与意义)
	* [1.2 本课题研究内容与目标](#12-本课题研究内容与目标)
* [第二章 相关技术介绍](#第二章-相关技术介绍)
	* [2.1 React Native 简介](#21-react-native-简介)
	* [2.2 React 简介](#22-react-简介)
	* [2.3 Node.js 简介](#23-nodejs-简介)
	* [2.4 MongoDB 简介](#24-mongodb-简介)
* [第三章 系统分析](#第三章-系统分析)
	* [3.1 应用场景](#31-应用场景)
	* [3.2 系统需求分析](#32-系统需求分析)
		* [3.2.1 系统用例](#321-系统用例)
		* [3.2.2 用例规约](#322-用例规约)
* [第四章 系统设计](#第四章-系统设计)
	* [4.1 概述](#41-概述)
	* [4.2 静态模型](#42-静态模型)
	* [4.3 动态模型](#43-动态模型)
		* [4.3.1 时序图](#431-时序图)
		* [4.3.2 活动图](#432-活动图)
* [第五章 系统实现](#第五章-系统实现)
	* [5.1 概述](#51-概述)
	* [5.2 开发及运行环境](#52-开发及运行环境)
	* [5.3 服务端搭建](#53-服务端搭建)
	* [5.4 注册模块](#54-注册模块)
	* [5.5 登录模块](#55-登录模块)
	* [5.6 试卷管理台模块](#56-试卷管理台模块)
	* [5.7 试卷编辑模块](#57-试卷编辑模块)
	* [5.8 练习考试管理台模块](#58-练习考试管理台模块)
	* [5.9 做题模块](#59-做题模块)
* [结论](#结论)
* [致谢语](#致谢语)
* [参考文献](#参考文献)

<!-- /code_chunk_output -->

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

现在比较新的技术栈就是使用 React 开发网页端，使用 React Native 开发移动端，使用 Node.js 作为后端提供 API 服务，本课题系统通过这样的技术栈来开发一个英语学习 App 来实现对四六级英语实现练习和考试的功能。为了实现这个四六级练习和考试 app，还要实现题库管理功能，考试结果保存功能，评分系统，来及时反馈练习结果以及记录考试成绩和答题信息。

# 第二章 相关技术介绍

## 2.1 React Native 简介

React Native 是 Facebook 开发的用于开发移动端的一个框架 js 类库，使得 Android 能够通过 javascript 开发移动端的应用，也就是说不仅可以开发 Android，还可以开发 ios。主要是通过把将 javascript 代码转码成对应平台的代码来实现的，也就是说在通过编写 javascript 代码然后转码成 java 代码来运行 Android 程序，这样的一个好处就是能够使用 javascript 的库，而 javascript 的库的数量在近些年来远远超过了其他平台的数量。在 javascript 和 java 之间在开发效率上可以说 javascript 远胜 java，在 javascript 经常见的 map、filter、reduce 等函数在用 java 开发 Android 的时候是不能用的。

>

React Native 除了在开发效率上能够大大地提高外，还能够实现多平台开发，在有 Mac OS 的环境下也可以把 React Native 项目编译成 ios 的 app，轻松实现多平台。

## 2.2 React 简介

React 是前端的一个类库，能够使用 jsx 来写页面，与状态管理工具 Redux 或 Mobx 能够实现 MVVM 的方式来开发前端页面，这个前端页面包括网页端也包括移动端，而 React 通过构建一个个组件来开发页面，这种组件化的开发方式在代码不断重构出一套套组件后可以调用组件，实现快速开发。

## 2.3 Node.js 简介

Node.js 通过使用 express 这样的后端框架，可以很快速地开发出想要的 API，并且通过与 mongoose 这样的工具在建立模型可以实现对于数据的基本验证，对于较为复杂的验证也可以自己写逻辑来实现，这样就能够实现对用户传送过来的数据进行校验和对应的反馈。

## 2.4 MongoDB 简介

MongoDB 是非关系型的数据库，这样就能够直接将较为复杂数据结构存进去，大大提高了开发效率，而不像关系型数据库那样需要建立多张表来实现一个较为复杂的数据模型。

# 第三章 系统分析

## 3.1 应用场景

要实现英语四六级练习与考试系统，就要实现试卷的制作，而很明显移动端并不适合试卷制作这一过程，于是需要在网页端中进行试卷制作。所以网页端需要完成以下的场景：

1.  通过注册登陆来实现对于自己的试卷的管理。
2.  试卷要能够输入四六级考卷的题目和答案。

在网页端制作了考卷之后，用户在移动端要能够进行以下的操作：

1.  注册登陆以便能够保存自己的考试的答题信息和成绩。
2.  能够对考卷进行练习，并及时反馈所选选项是否正确。
3.  能够进行考试，其中听力只能听一次，考试结束后给出成绩和答题情况，并能够保存答题情况。
4.  能够对过去做过的考卷及其答题情况进行查看和删除，其中考卷被修改或删除后，不能影响与该考卷相关的答题情况。

## 3.2 系统需求分析

系统除了较为常见的登陆注册外，最关键的是试卷的编辑，以及试卷的使用。为了实现试卷的编辑，必须要根据试卷的结构来进行分析建模，并根据模型特征来进行数据的操作。通过试卷的编辑，可以获得试卷的结构，根据试卷的结构，可以将其进行展示，并新建出含有答题卡的数据模型，这样能够较好地对数据进行操作。为了能够更好地帮助到用户，需要对答题后进行保存，并且能够进行管理。

### 3.2.1 系统用例

网页端用户用例

```puml
left to right direction
skinparam packageStyle rectangle
actor 用户
rectangle 试卷管理系统 {
  用户 -- (登录)
  用户 -- (注册)
  用户 -- (增加试卷)
  用户 -- (修改试卷)
  用户 -- (删除试卷)
}
```

移动端用户用例

```puml
left to right direction
skinparam packageStyle rectangle
actor 用户
rectangle 练习考试系统 {
  用户 -- (登录)
  用户 -- (注册)
  用户 -- (练习)
  用户 -- (考试)
  用户 -- (考试记录查看)
}
```

### 3.2.2 用例规约

系统包括网页端和移动端，都具有最基本的登录和注册用例子，其中网页端多了试卷管理的用例，而移动端多了练习、考试、考试记录查看这三个用例。

>

网页端的用例规约如下：

1.  注册用例

| 元素       | 元素内容                                                              |
| ---------- | --------------------------------------------------------------------- |
| 用例名称   | 注册                                                                  |
| 用例 ID    | UC1.1                                                                 |
| 范围       | 试卷管理系统                                                          |
| 执行者     | 用户                                                                  |
| 前置条件   | 处于注册页面                                                          |
| 后置条件   | 跳转到登录页面                                                        |
| 基本事件流 | 1. 输入昵称，邮箱，密码，确认密码                                     |
| ^          | 2. 点击提交资料注册                                                   |
| 备选事件流 | a. 昵称、邮箱、密码和确认密码这四个基本信息缺少一个或者多个，重新输入 |
| ^          | b. 邮箱已经被注册，重新输入                                           |
| 业务规则   | 昵称、邮箱、密码和确认密码均不为空                                    |

2.  登录用例

| 元素       | 元素内容                                              |
| ---------- | ----------------------------------------------------- |
| 用例名称   | 登录                                                  |
| 用例 ID    | UC1.2                                                 |
| 范围       | 试卷管理系统                                          |
| 执行者     | 用户                                                  |
| 前置条件   | 处于登录页面                                          |
| 后置条件   | 跳转到试卷管理台页面                                  |
| 基本事件流 | 1. 输入邮箱，密码                                     |
| ^          | 2. 点击提交登录信息以便登录                           |
| 备选事件流 | a. 邮箱、密码这两个基本信息缺少一个或者多个，重新输入 |
| ^          | b. 邮箱未注册，重新输入                               |
| ^          | b. 密码错误，重新输入                                 |
| 业务规则   | 邮箱、密码均不为空                                    |

3.  增加试卷

| 元素       | 元素内容                                    |
| ---------- | ------------------------------------------- |
| 用例名称   | 增加试卷                                    |
| 用例 ID    | UC1.3                                       |
| 范围       | 试卷管理系统                                |
| 执行者     | 用户                                        |
| 前置条件   | 已经登录了账号，并且在试卷管理台页面            |
| 后置条件   | 跳转到试卷管理台页面                        |
| 基本事件流 | 1. 点击增加试卷按钮，跳转到空白试卷编辑界面 |
| ^          | 2. 输入试卷的内容，并提交                   |
| 备选事件流 | a. 部分信息空白，重新输入                   |
| 业务规则   | 试卷输入信息不能为空                        |

4.  修改试卷

| 元素       | 元素内容                                      |
| ---------- | --------------------------------------------- |
| 用例名称   | 修改试卷                                      |
| 用例 ID    | UC1.4                                         |
| 范围       | 试卷管理系统                                  |
| 执行者     | 用户                                          |
| 前置条件   | 已经登录了账号，并且在试卷管理台页面              |
| 后置条件   | 跳转到试卷管理台页面                          |
| 基本事件流 | 1. 点击要修改试卷按钮，跳转到所选试卷编辑界面 |
| ^          | 2. 输入试卷要修改的内容，并提交               |
| 备选事件流 | a. 部分信息空白，重新输入                     |
| 业务规则   | 试卷输入信息不能为空                          |

5.  删除试卷

| 元素       | 元素内容                                      |
| ---------- | --------------------------------------------- |
| 用例名称   | 删除试卷                                      |
| 用例 ID    | UC1.5                                         |
| 范围       | 试卷管理系统                                  |
| 执行者     | 用户                                          |
| 前置条件   | 已经登录了账号，并且在试卷管理台页面              |
| 后置条件   | 跳转到试卷管理台页面                          |
| 基本事件流 | 1. 点击要删除试卷按钮，删除后，刷新管理台界面 |
| 备选事件流 | 无                                            |
| 业务规则   | 无                                            |

网页端的用例规约如下：

1.  注册用例

| 元素       | 元素内容                                                              |
| ---------- | --------------------------------------------------------------------- |
| 用例名称   | 注册                                                                  |
| 用例 ID    | UC2.1                                                                 |
| 范围       | 练习考试系统                                                          |
| 执行者     | 用户                                                                  |
| 前置条件   | 处于注册页面                                                          |
| 后置条件   | 跳转到登录页面                                                        |
| 基本事件流 | 1. 输入昵称，邮箱，密码，确认密码                                     |
| ^          | 2. 点击提交资料注册                                                   |
| 备选事件流 | a. 昵称、邮箱、密码和确认密码这四个基本信息缺少一个或者多个，重新输入 |
| ^          | b. 邮箱已经被注册，重新输入                                           |
| 业务规则   | 昵称、邮箱、密码和确认密码均不为空                                    |

2.  登录用例

| 元素       | 元素内容                                              |
| ---------- | ----------------------------------------------------- |
| 用例名称   | 登录                                                  |
| 用例 ID    | UC2.2                                                 |
| 范围       | 练习考试系统                                          |
| 执行者     | 用户                                                  |
| 前置条件   | 处于登录页面                                          |
| 后置条件   | 跳转到练习考试管理台页面                                  |
| 基本事件流 | 1. 输入邮箱，密码                                     |
| ^          | 2. 点击提交登录信息以便登录                           |
| 备选事件流 | a. 邮箱、密码这两个基本信息缺少一个或者多个，重新输入 |
| ^          | b. 邮箱未注册，重新输入                               |
| ^          | b. 密码错误，重新输入                                 |
| 业务规则   | 邮箱、密码均不为空                                    |

3.  练习

| 元素       | 元素内容                                    |
| ---------- | ------------------------------------------- |
| 用例名称   | 练习                                    |
| 用例 ID    | UC2.3                                       |
| 范围       | 练习考试系统                                |
| 执行者     | 用户                                        |
| 前置条件   | 已经登录了账号，并且在练习考试管理台页面            |
| 后置条件   | 无                        |
| 基本事件流 | 1. 点击所要练习的试卷，跳转到该试卷的练习界面 |
| ^          | 2. 输入试卷的内容，及时反馈答题是否正确以及分数                   |
| 备选事件流 | 无                   |
| 业务规则   | 无                        |

4.  考试

| 元素       | 元素内容                                    |
| ---------- | ------------------------------------------- |
| 用例名称   | 考试                                    |
| 用例 ID    | UC2.4                                       |
| 范围       | 练习考试系统                                |
| 执行者     | 用户                                        |
| 前置条件   | 已经登录了账号，并且在练习考试管理台页面            |
| 后置条件   | 跳转到练习考试管理台页面                        |
| 基本事件流 | 1. 点击所要练习的试卷，跳转到该试卷的练习界面，倒计时开始 |
| ^          | 2. 输入试卷的内容                   |
| ^          | 3. 点击完成答题动作，确认答题卡，根据需要点击提交，上传答题信息                   |
| 备选事件流 | a. 倒计时时间到，自动完成答题动作，根据需要点击提交，上传答题信息              |
| 业务规则   | 无                        |

5.  考试记录查看

| 元素       | 元素内容                                    |
| ---------- | ------------------------------------------- |
| 用例名称   | 考试记录查看                                    |
| 用例 ID    | UC2.5                                       |
| 范围       | 练习考试系统                                |
| 执行者     | 用户                                        |
| 前置条件   | 已经登录了账号，并且在练习考试管理台页面，有上传答题记录         |
| 后置条件   | 无                        |
| 基本事件流 | 1. 点击所要查看的答题记录，跳转到该试卷的答题记录界面 |
| 备选事件流 | 无                   |
| 业务规则   | 无                        |

# 第四章 系统设计

## 4.1 概述
基于MongoDB的项目最开始要定义的就是数据模型，只要将数据的模型建立起来，就可以根据数据的结构特征来进行操作，由于试卷信息是一个结构化非常复杂，有很多层次的结构，所以使用非关系型数据库可以避免过多的表关联操作。在MongoDB中确定好数据的结构后，可以直接就给项目中的变量赋值，所以项目中的变量的结构在MongoDB的模型结构确定后基本就确定了。

## 4.2 静态模型
在本项目中主要设计了3个模型，其中包括用于登录、注册的User，用于保存试卷信息的Paper和用于保存答题信息的Answer,下面用类图来表示各个模型的设计
1. User模型

```puml
class User {
	String nickname,
	String email,
	String password,
	String avatar,
	Date data
}
```

2. Paper模型

```puml
class Paper {
	String title,
	String level,
	Date data
}

class Writing {
	String directions
}

class Listening {
}

class Section {
	String sectionTitle
}

class Module {
	String moduleSound
}

class ModuleSound{
	String url
}

class Question {
	String questionSound
	Number rightAnswer
	String [] options
}

class Reading {
}

class Sections {
}

class BankedCloze {
	String passage
	String [] options
	Number [] rightOrder
}

class Locating {
	String title
	String [] paragraphs
}

class LocatingQuestion {
	String questionContent
	Number rightAnswer
}

class Selection {
}

class Passage {
	String passageContent
	String [] options
	Number [] rightOrder
}

class PassageQuestion {
	String questionContent
	String [] options
	Number rightAnswer
}

class Translation {
	String question
}

Paper "1" *-- "1" Writing
Paper "1" *-- "1" Listening
Listening "1" *-- "many" Section
Section "1" *-- "many" Module
Module "1" *-- "many" Question
Module "1" *-- "1" ModuleSound
Paper "1" *-- "1" Reading
Reading "1" *-- "many" Sections
Sections "1" *-- "1" BankedCloze
Sections "1" *-- "1" Locating
Locating "1" *-- "many" LocatingQuestion
Sections "1" *-- "1" Selection
Selection "1" *-- "many" Passage
Passage "1" *-- "many" PassageQuestion
Paper "1" *-- "1" Translation

```

3. Answer模型

```puml
class Answer {
	String title,
	String level,
	Date data
}

class Writing {
	String directions
	String essay
	Number level
}

class Listening {
}

class Section {
	String sectionTitle
}

class Module {
	String moduleSound
}

class ModuleSound{
	String url
}

class Question {
	String questionSound
	Number rightAnswer
	String [] options
	Number orderSelected
}

class Reading {
}

class Sections {
}

class BankedCloze {
	String passage
	String [] options
	Number [] rightOrder
	Number [] orderSelected
}

class Locating {
	String title
	String [] paragraphs
}

class LocatingQuestion {
	String questionContent
	Number rightAnswer
	Number optionSelected
}

class Selection {
}

class Passage {
	String passageContent
	String [] options
	Number [] rightOrder
}

class PassageQuestion {
	String questionContent
	String [] options
	Number rightAnswer
	Number optionSelected
}

class Translation {
	String question
	String answer
	Number level
}

Answer "1" *-- "1" Writing
Answer "1" *-- "1" Listening
Listening "1" *-- "many" Section
Section "1" *-- "many" Module
Module "1" *-- "many" Question
Module "1" *-- "1" ModuleSound
Answer "1" *-- "1" Reading
Reading "1" *-- "many" Sections
Sections "1" *-- "1" BankedCloze
Sections "1" *-- "1" Locating
Locating "1" *-- "many" LocatingQuestion
Sections "1" *-- "1" Selection
Selection "1" *-- "many" Passage
Passage "1" *-- "many" PassageQuestion
Answer "1" *-- "1" Translation
```

## 4.3 动态模型
接下来用时序图和活动图来描述用户在应用中的一些操作

### 4.3.1 时序图
网页端和移动端共同的时序图主要有以下两个：

1. 注册
```puml
actor 用户 as A
participant "注册页面" as B
participant "注册API" as C
participant "User Collection" as D

A -> B: 输入注册信息
B -> C: 发送注册信息
C -> C: 验证两次密码是否一致
alt 两次密码不一致
	B <[#red]-- C: 返回密码不一致错误信息
	A <[#red]-- B: 提醒用户输入一致的密码
else 两次密码一致
	C -> D: 查看邮箱是否存在
	alt 邮箱存在
	C <[#red]-- D : 返回邮箱已注册错误信息
	B <[#red]-- C : 返回错误信息
	A <[#red]-- B: 提醒用户输入正确的信息
	else 邮箱不存在
		C -> D: 存储用户注册信息
		alt 注册信息缺失或不合法
			C <[#red]-- D : 返回相关错误信息
			B <[#red]-- C : 返回错误信息
			A <[#red]-- B: 提醒用户输入正确的信息
		else 保存成功
			C <[#green]-- D: 返回保存成功信息
			B <[#green]-- C: 返回保存成功信息
			A <[#green]-- B: 注册成功，跳转到登录页面
		end
	end
end
```

2. 登录
```puml
actor 用户 as A
participant "登录页面" as B
participant "登录API" as C
participant "User Collection" as D

A -> B: 输入登录信息
B -> C: 发送登录信息
C -> D: 查看邮箱是否存在
alt 邮箱不存在
C <[#red]-- D : 返回邮箱未注册错误信息
B <[#red]-- C : 返回错误信息
A <[#red]-- B: 提醒用户输入已经注册的账号
else 邮箱存在
	C -> D: 查看密码是否正确
	alt 密码不正确
		C <[#red]-- D : 返回密码不正确错误信息
		B <[#red]-- C : 返回错误信息
		A <[#red]-- B: 提醒用户输入正确的密码
	else 密码正确
		C <[#green]-- D: 返回密码正确信息
		B <[#green]-- C: 返回对应的token
		A <[#green]-- B: 注册成功，保存和配置token，跳转到对应的管理台
	end
end
```

网页端特有的时序图主要有以下三个：

1. 增加试卷
```puml
actor 用户 as A
participant "试卷管理台页面" as B
participant "试卷编辑界面" as C
participant "新增试卷API" as D
participant "Paper Collection" as E

A -> B: 点击新增试卷按钮
B -> C: 跳转到试卷编辑界面
A <-- C: 显示空白的试卷编辑界面
A -> C: 输入试卷内容
C -> D: 发送新增试卷请求
D -> E: 保存试卷信息

alt 新增试卷信息缺失或不合法
	D <[#red]-- E : 返回相关错误信息
	C <[#red]-- D : 返回错误信息
	A <[#red]-- C: 提醒用户输入正确的信息
else 保存成功
	D <[#green]-- E: 返回保存成功信息
	C <[#green]-- D: 返回保存成功信息
	A <[#green]-- C: 保存成功，跳转到管理台页面
end
```

2. 修改试卷
```puml
actor 用户 as A
participant "试卷管理台页面" as B
participant "试卷编辑界面" as C
participant "修改试卷API" as D
participant "获取用户的所有试卷API" as E
participant "Paper Collection" as F


A -> B: 进入管理台页面
B -> E: 请求用户所有试卷
E -> F: 查找该用户的所有试卷
E <-- F: 返回该用户的所有试卷
B <-- E: 返回用户所有试卷
A <-- B: 显示用户所有的试卷

A -> B: 点击所要编辑试卷
B -> C: 跳转到试卷编辑界面
A <-- C: 显示空白的试卷编辑界面
A -> C: 输入试卷内容
C -> D: 发送修改试卷请求
D -> F: 保存试卷信息

alt 修改试卷信息缺失或不合法
	D <[#red]-- F : 返回相关错误信息
	C <[#red]-- D : 返回错误信息
	A <[#red]-- C: 提醒用户输入正确的信息
else 保存成功
	D <[#green]-- F: 返回保存成功信息
	C <[#green]-- D: 返回保存成功信息
	A <[#green]-- C: 保存成功，跳转到管理台页面
end
```

3. 删除试卷
```puml
actor 用户 as A
participant "试卷管理台页面" as B
participant "获取用户的所有试卷API" as C
participant "删除试卷API" as D
participant "Paper Collection" as E

A -> B: 进入管理台页面
B -> C: 请求用户所有试卷
C -> E: 查找该用户的所有试卷
C <-- E: 返回该用户的所有试卷
B <-- C: 返回用户所有试卷
A <-- B: 显示用户所有的试卷

A -> B: 点击所要删除试卷
B -> D: 发送删除试卷请求
D -> E: 删除试卷信息
alt 所要删除试卷不存在
	D <[#red]-- E : 返回相关错误信息
	B <[#red]-- D : 返回错误信息
else 删除成功
	D <[#green]-- E: 返回保存成功信息
	B <[#green]-- D: 返回保存成功信息
end
A <-- C: 刷新管理台信息
```
移动端特有的时序图主要有以下三个：
1.练习
```puml
actor 用户 as A
participant "练习考试管理台页面" as B
participant "练习界面" as C
participant "获取试卷API" as D
participant "获取用户的所有试卷API" as E
participant "Paper Collection" as F


A -> B: 进入管理台页面
B -> E: 请求用户所有试卷
E -> F: 查找该用户的所有试卷
E <-- F: 返回该用户的所有试卷
B <-- E: 返回用户所有试卷
A <-- B: 显示用户所有的试卷

A -> B: 点击所要练习试卷
B -> C: 跳转到练习界面
C -> D: 发送获取试卷请求
D -> F: 获取试卷信息
D <-- F: 返回试卷信息
C <-- D: 返回试卷信息
A <-- C: 显示练习界面
loop 练习过程
	A -> C: 答题
	A <-- C: 反馈答题情况，包括分数和是否正确
end
```
2.考试

```puml
actor 用户 as A
participant "练习考试管理台页面" as B
participant "考试界面" as C
participant "提交预览界面" as G
participant "获取试卷API" as D
participant "保存答案API" as H
participant "获取用户的所有试卷API" as E
participant "Paper Collection" as F
participant "Answer Collection" as I

A -> B: 进入管理台页面
B -> E: 请求用户所有试卷
E -> F: 查找该用户的所有试卷
E <-- F: 返回该用户的所有试卷
B <-- E: 返回用户所有试卷
A <-- B: 显示用户所有的试卷

A -> B: 点击所要考试试卷
B -> C: 跳转到练习界面
C -> D: 发送获取试卷请求
D -> F: 获取试卷信息
D <-- F: 返回试卷信息
C <-- D: 返回试卷信息
C -> C: 开始倒计时
A <-- C: 显示考试界面
alt 倒计时过程且答题未完成
	loop 答题过程
		A -> C: 答题
		A <-- C: 反馈答题情况，不包括分数和是否正确
	end
else 倒计时结束或答题已经完成
C -> G: 跳传到提交预览界面
A <-- G: 显示答题情况，取消题目显示
	alt 确认提交
		A -> G: 点击提交按钮
		G -> H: 请求保存用户答案
		H -> I: 保存用户答案
		H <-- I: 返回保存用户答案成功信息
		G <-- H: 返回保存用户答案成功信息
		G -> B: 跳转到练习考试管理台页面
		A <-- B: 显示练习考试管理台页面
	else 不提交
		A -> B: 请求练习考试管理台
		A <-- B: 显示练习考试管理台
	end
end
```
3.考试记录查看
```puml
actor 用户 as A
participant "练习考试管理台页面" as B
participant "答题试卷回顾界面" as C
participant "获取答题试卷API" as D
participant "获取用户的所有答题试卷API" as J
participant "Answer Collection" as I

A -> B: 进入管理台页面
B -> J: 请求用户所有答题试卷
J -> I: 查找该用户的所有答题试卷
J <-- I: 返回该用户的所有答题试卷
B <-- J: 返回用户所有答题试卷
A <-- B: 显示用户所有的答题试卷

A -> B: 点击所要回顾的答题试卷
B -> C: 跳转到答题试卷回顾界面
C -> D: 发送获取答题试卷请求
D -> I: 获取答题试卷信息
D <-- I: 返回答题试卷信息
C <-- D: 返回答题试卷信息
A <-- C: 显示答题试卷回顾界面
loop 校正过程
	A -> C: 校正
	A <-- C: 反馈答题情况，包括分数和是否正确
end
```

### 4.3.2 活动图
网页端主要用来管理试卷，移动端主要用来练习考试。
1. 网页端试卷管理活动
```puml
start
if (已经登录) then (yes)
else (no)
	if (已经注册) then (yes)
	else (no)
		:注册账号;
	endif
	:登录;
endif
:试卷管理;
fork
 	:新增试卷;
	:输入试卷内容;
	:提交保存;
fork again
 	:修改试卷;
	:输入修改的试卷内容;
	:提交保存;
fork again
	:删除试卷;
endfork
stop
```

2. 移动端练习考试活动
```puml
start
if (已经登录) then (yes)
else (no)
	if (已经注册) then (yes)
	else (no)
		:注册账号;
	endif
	:登录;
endif
:练习考试;
fork
 	:练习;
fork again
 	:考试;
	if(是否提交答题试卷) then (yes)
		:提交答题试卷;
	else (no)
	endif
fork again
	:考试记录查看;
endfork
stop
```
# 第五章 系统实现

## 5.1 概述
由于本项目是用来准备四六级考试的项目，所以在四六级考试的基本需求要能够实现，也就是做题功能。要实现做题功能就要有试卷的管理系统，为了便于试卷管理，选择在网页端实现试卷管理功能。在实现了试卷的管理后，就有数据来实现移动端的做题功能，根据练习、考试和考试记录查看等不同需求，在做题的基础上做不同的实现。
在试卷的编辑中，需要对于试卷的基本结构进行模拟实现。四六级的试卷主要分成4个部分，也就是写作部分、听力部分、阅读部分和翻译部分，每个部分有不同的要求，比如听力要能够传入音频，阅读部分要根据不同的类型的题目进行不同的输入方式的实现，客观题要传入答案。
在做题功能中，写作部分和翻译部分这两个主观题部分采用自评的方式来实现批改和评分，而听力部分和阅读部分这两个客观题部分就可以根据在试卷管理时传入的答案进行批改和评分。

## 5.2 开发及运行环境
- 操作系统：Ubuntu GNOME 16.04.4
- 数据库代理商：mLab
- 数据库：MongoDB 3.4.14
- 服务器及域名代理商：Heroku
- 技术栈：
	* React Native 0.55.2
	* React 16.3.2
	* OpenJDK 1.8.0_171
	* Node.js 8.11.1
	* Express 4.16.3
	* Mongoose 5.0.15
- 编辑器及IDE等开发工具：
	* Visual Studio Code 1.22.2
	* Atom 1.26.1
	* Nuclide 0.302.0
	* Android Studio 3.1.1
- 运行环境：
	* 实体机：OnePlus 3T Andriod 8.0
	* 模拟器：Pixel 2 Android 8.0
	* 浏览器：Google Chrome 66.0.3359.170

## 5.3 服务端搭建
作为数据的中转站和数据的仓库，服务端除了搭建RESTful API以外，还要有一个存储数据的仓库。本项目使用Node.js搭建RESTful API，以及MongoDB来作为数据库。
本项目MnongoDB使用的是mLab的服务，通过简单的注册，就能够在免费在mLab新建自己的MongoDB数据库，避免了需要自己租服务器搭建的码法。在API在本地调试好后，将后端代码传到Heroku的云平台上，就能够免费地使用Heroku来上线自己的RESTful API服务，这样就能通过Heroku的域名来访问API。通过简单的配置，使得网页端也能通过Heroku的域名访问，避免了自己要租服务器来搭建的麻烦。Heroku在更新代码的方式的通过git上传代码到Heroku上托管就行。

## 5.4 注册模块
注册模块是网页端和移动端共有的一个模块，实现的方法上基本都差不多，主要是要把关键的信息填写进去，作为后面登录用的凭证。注册的账号除了在网页端能够对试卷进行操作并且保存试卷外，还可以在移动端保存考试的答题记录。以下是网页端和移动端的注册页面：
1. 网页端注册页面
![网页端注册页面](/img/网页端注册页面.png)
2. 移动端注册页面
![移动端注册页面](/img/移动端注册页面.jpg)
通过注册页面可以看到，通过输入昵称、邮箱、密码和确认密码就行
当输入为空时会进行非空校验，并且邮箱已经注册过的时候也会提示邮箱已经注册过了，如果两次密码不一致也会提示密码不一致，输入邮箱的不是邮箱格式也会提醒。注册成功后会跳转到登录页面
## 5.5 登录模块
登录模块是继注册模块之外，另一个网页端和移动端共有的模块，在注册完成后会自动进入。以下是网页端和移动端的登录页面：
1. 网页端登录页面
![网页端登录页面](/img/网页端登录页面.png)
2. 移动端登录页面
![移动端登录页面](/img/移动端登录页面.jpg)
通过登录页面可以看到只要输入邮箱账号和密码就能进入，其中如果邮箱没有注册会提醒，输入邮箱的不是邮箱格式也会提醒，密码错误也会提醒

## 5.6 试卷管理台模块
试卷管理台模块是登录账号后能够进入的模块，在这个模块能对试卷进行增加、修改和删除操作，如图所示为试卷管理台页面：
![试卷管理台页面](/img/试卷管理台页面.png)
如图所示点击Add Paper按钮能够能够添加试卷，点击要修改的试卷的标题能够修改试卷，点击Delete按钮能删除对应的试卷。

## 5.7 试卷编辑模块
试卷编辑模块，主要是在新增或编辑试卷的时候能够对试卷起到资料输入、修改的作用。一张四六级试卷除了基本的标题、等级信息要录入以外，还要录入四个部分的题目，分别是写作部分、听力部分、阅读部分和翻译部分。以下为基本信息以及各个部分的录入示例图。
1. 基本信息
![基本信息录入](/img/基本信息录入.png)
如图所示，主要是输入试卷的标题和试卷的等级，其中等级包括CET-4和CET-6两种。
2. 写作部分
![写作部分录入](/img/写作部分录入.png)
由于写作部分需要输入题目在Directions里面，所以需要输入Directions。
3. 听力部分
![听力部分录入](/img/听力部分录入.png)
听力部分主要分成三个Sections，每个Section包含不同类型的题目，所以在Title栏选择该Section的类型，Title包括News Report、Conversation、Passange和Record四种。每个Sction包括若干个模块和若干个题目，每个模块有一个模块听力，每个题目包括一个题目听力、四个选项和正确答案
4. 阅读部分
阅读部分包括三个Sections的题目，每个Sction类型不一样所以输入不能像听力那样动态添加。这三个Sections包括选词填空、信息匹配和单项选择三种
	- 选词填空录入
	![选词填空录入](/img/选词填空录入.png)
	选词填空主要是文章要录入，我使用了两个下划线代替了要选择的空格
	![选词填空答案录入](/img/选词填空答案录入.png)
	在后面的输入框能够输入能够选择的单词，在后面的选择框能够选择正确的答案
	- 信息匹配
	![信息匹配录入](/img/信息匹配录入.png)
	信息匹配的文章带有标题，所以就有一个文章的标题框，在后面是每一个段落的录入。
	![信息匹配答案录入](/img/信息匹配答案录入.png)
	在录入完文章后要录入题目和对应题目的答案
	- 单项选择
	![单项选择录入](/img/单项选择录入.png)
	单项选择包括两篇文章和若干个问题，其中每个问题问题内容、四个选项和正确答案。
5. 翻译部分
![翻译部分录入](/img/翻译部分录入.png)
翻译部分的Directions不包括题目，题目是录入在另一个部分。

## 5.8 练习考试管理台模块
考试练习管理台有三个页面，其中包括练习考试列表、考试记录列表和基本信息
1. 练习考试列表
![练习考试列表](/img/练习考试列表.jpg)
其中点击除了蓝色箭头按钮以外的部分能够进入练习页面，点击蓝色箭头按钮能够进入考试页面
2. 考试记录列表
![考试记录列表](/img/考试记录列表.jpg)
如果有考试记录的情况下会显示考试记录，在点击红色交叉按钮以外的部分可以对考试记录进行查看，点击红色交叉按钮删除该考试记录。
3. 基本信息
![基本信息](/img/基本信息.jpg)
在基本信息页面显示用户的基本信息，可以点击蓝色LOGOUT按钮退出到登录界面。

## 5.9 做题模块
做题模块主要分成3个部分，即试卷部分，倒计时部分，答题卡部分，按钮部分
如图所示为一个基本的做题模块示例：
![做题模块](/img/做题模块.jpg)
以下是将其分成主要的四个模块

1. 试卷部分
![做题模块试卷部分](/img/做题模块试卷部分.jpg)
如图所示的每一个部分都是可以点击的，点击后能够进入对应部分的题目
其中做题部分分为写作部分、听力部分、阅读部分、翻译部分
	- 写作部分
	![做题写作部分](/img/做题写作部分.jpg)
	根据Directions的指示把作文写在答题框里，并在写完后给自己评个等级，能够计算分数。
	- 听力部分
	![做题听力部分考试](/img/做题听力部分考试.jpg)
	在考试的情况下，听力听过一次就会消失。
	![做题听力部分考试](/img/做题听力部分练习.jpg)
	不在练习或者查看考试记录的情况下，听力不会消失，并且会及时反馈是否做对题目

	- 阅读部分
	阅读部分包括了选词填空、信息匹配和单项选择三种题型
		* 选词填空
		![做题阅读选词填空部分考试](/img/做题阅读选词填空部分考试.jpg)
		在点击填写空格的序号后，会展开所有的单词选项，选择后绿色为正确，红色为错误，在考试模式时为黑色。
		* 信息匹配
		![做题阅读信息匹配部分考试](/img/做题阅读信息匹配部分考试.jpg)
		点开单选框后可以选择匹配的段落，选对显示绿色，选错显示红色，考试时显示黑色
		* 单项选择
		![做题阅读单项选择部分考试](/img/做题阅读单项选择部分考试.jpg)
		点击选项可以选择选项，正确显示绿色钩号，错误显示红色叉号，考试时显示黑色粗点
	- 翻译部分
	![做题翻译部分](/img/做题翻译部分.jpg)
	与写作部分相同，根据题目翻译后给自己评个等级，会计算分数。



2. 倒计时部分
![做题模块倒计时部分](/img/做题模块倒计时部分.jpg)
仅在考试时显示，CET-4的试卷为2小时20分钟，CET-6的试卷为2小时25分钟。进入考试界面倒计时开始。

3. 答题卡部分
![做题模块答题卡部分](/img/做题模块答题卡部分.jpg)
以上时没有答题的情况
![做题答题卡部分考试](/img/做题答题卡部分考试.jpg)
在有答题的情况下会自动填充分数和通过颜色来批改客观题。在考试的情况下颜色均为黑色，分数不会显示。

4. 按钮部分
![做题模块按钮部分](/img/做题模块按钮部分.jpg)
在考试的时候显示COMPLETE按钮，点击后进入提交模式，试卷消失，只显示答题卡部分，答题卡显示分数并显示批改结果。按钮变成SUBMIT按钮，点击提交此次考试记录。


# 结论

# 致谢语

# 参考文献
