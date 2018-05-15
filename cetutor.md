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
participant "注册Api" as C
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
participant "登录Api" as C
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
participant "新增试卷Api" as D
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
participant "修改试卷Api" as D
participant "获取用户的所有试卷Api" as E
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
participant "获取用户的所有试卷Api" as C
participant "删除试卷Api" as D
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
participant "获取试卷Api" as D
participant "获取用户的所有试卷Api" as E
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
participant "获取试卷Api" as D
participant "保存答案Api" as H
participant "获取用户的所有试卷Api" as E
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
participant "获取答题试卷Api" as D
participant "获取用户的所有答题试卷Api" as J
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

# 结论

# 致谢语

# 参考文献
