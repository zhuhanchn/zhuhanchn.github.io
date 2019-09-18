---
title: 测试开发知识点
date: 2019-09-07 21:02:58
tags: 
	- TDE

cover: https://i.loli.net/2019/09/07/sZmvzOxABu2HyoU.png

---

# 自动化测试

## 测试工具
- 性能测试：JMeter、LoadRunner
- WebUI自动化测试：Selenium
- 接口测试：Postman
 （提供功能强大的 Web API 和 HTTP 请求的调试，它能够发送任何类型的HTTP 请求 (GET, POST, PUT, DELETE…)，并且能附带任何数量的参数和 Headers。）
- ...

## 语言
- Java
- Python
- Shell
- XML

-----------


## UI元素定位的方法

- XPath
- CSS

> Chrome浏览器F12可以看到元素的基本信息,
Selenium中，可以
1.find_element_by_id();
2.find_element_by_name():通过name查找元素, name是否唯一，name不是唯一的话会报错
3.find_element_by_class_name();
4.find_element_by_tag_name();
5.find_element_by_link_text();
6.find_element_by_xpath():通过Xpath定位元素, 使用谷歌插件XPath Helper，定位出来后自己修改也可以
7.find_element_by_css_selector():通过css定位，css_selector的语法比xpath简洁很多
8.find_element_by_partial_link_text():是一种模糊匹配，字符串可以输入其中一部分


```java
from selenium import webdriver
import time

driver = webdriver.Chrome()
driver.get("http://djuat.dtfunds.com/fund-jsqyweb/index.html")
driver.maximize_window()
time.sleep(3)

driver.find_element_by_id("mobile").send_keys("13770506773")
driver.find_element_by_name("password").send_keys("zy568521")
driver.find_element_by_class_name("s_ipt").send_keys("python")
driver.find_element_by_tag_name("input").send_keys("python")
driver.find_element_by_link_text("hao123").click()
driver.find_element_by_xpath("//input[@id='mobile']").send_keys("13770506771")
driver.find_element_by_css_selector("#password").send_keys("zy568521")

driver.quit()
```

# 集成测试
该部分原文链接：https://blog.csdn.net/tlonline/article/details/46468049

## 概述
若每个模块都经过了严格的单元测试，还需要集成测试吗？
- 回答是肯定的，确实需要集成测试。
在测试过程中经常遇到的情况是：单元测试中每个模块都能单独工作，但是将这些模块集成到一起后，某些模块就不能正常工作了。例如，接口数据丢失；模块之间的不良影响；误差积累等。因此，单元测试无法代替集成测试，每个模块的性能最优并不能保证集成之后的指标达到最优。

## 集成测试的定义
- 集成测试就是在单元测试的基础上，将所有已通过单元测试的模块按照概要设计的要求组装为子系统或系统，并进行测试的过程。
- 目的是确保各个单元模块组合在一起后能够按照既定意图协作运行，并确保增量的行为正确，需要再次强调的是，不经过单元测试的模块是不应该进行集成测试的，否则将对集成测试的效果和效率带来巨大的不利影响。

## 集成测试的内容
集成测试的内容包括模块之间接口以及集成后的功能。它主要使用**黑盒测试方法**测试集成的功能，并对以前的集成进行回归测试。具体来说，集成测试的内容包括以下方面：
(1)、将各个具有相互调用关系的模块组装起来时，检查穿越模块接口的数据是否会丢失。
(2)、判断各个子功能组合起来是否能够达到预期要求的父功能。
(3)、检查一个模块的功能是否对其他模块的功能产生不良影响。
(4)、检查全局数据结构是否正确，以及在完成模块功能的过程中是否会被异常修改。
(5)、单个模块的误差累计起来，是否会放大到不可接受的程度。

## 集成测试的评价
集成测试可基于多种测试策略站靠，可从如下4个方面对集成测试进行评价：
(1)、测试用例的规模。测试用例数量越多，设计、执行和分析这些测试用例所花费的工作量越大，因此，测试用例的规模应越小越好。
(2)、驱动模块的设计。收到模块调用关系的影响，参与某次集成测试的模块可能被不包含在本次集成中的其他模块所调用，为此需要设计驱动模块，驱动模块不含在产品代码中，因此，驱动模块的数量应越少越好。
(3)、桩模块的设计。类似地，参与某次集成测试的模块可能调用其它不包含在本次集成中的模块，为此需要设计桩模块，桩模块不应提交给用户，因此，桩模块的数量越少越好。
(4)、缺陷的定位。集成测试是主要任务是检查模块之间的接口，集成测试用例涉及的接口数量越少，越容易定位出错的接口，因此，单个集成测试设计接口的数量越少越好。
