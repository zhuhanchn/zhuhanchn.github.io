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
Selenium中，
可以find_element_by_id();
find_element_by_name();
find_element_by_class_name();
find_element_by_tag_name();
find_element_by_link_text();
find_element_by_xpath();
find_element_by_css_selector();
find_element_by_partial_link_text():是一种模糊匹配，字符串可以输入其中一部分


```java
from selenium import webdriver
import time

driver = webdriver.Chrome()
driver.get("http://djuat.dtfunds.com/fund-jsqyweb/index.html")
time.sleep(3)

driver.find_element_by_id("mobile").send_keys("13770506773")
time.sleep(3)

# 通过name查找元素, name是否唯一，name不是唯一的话会报错。
driver.find_element_by_name("password").send_keys("zy568521")

driver.maximize_window()
driver.find_element_by_class_name("s_ipt").send_keys("python")

# <input type="text" class="s_ipt" name="wd" id="kw" maxlength="100" autocomplete="off">
driver.find_element_by_tag_name("input").send_keys("python")

driver.find_element_by_link_text("hao123").click()
time.sleep(2)

# 通过Xpath定位元素, 使用谷歌插件XPath Helper，定位出来后自己修改也可以
driver.find_element_by_xpath("//input[@id='mobile']").send_keys("13770506771")

# 通过css定位, css_selector的语法比xpath简洁很多
driver.find_element_by_css_selector("#password").send_keys("zy568521")

driver.quit()
```