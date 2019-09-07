---
title: 测试开发面试储备
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