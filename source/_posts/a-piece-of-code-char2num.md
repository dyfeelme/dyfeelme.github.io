---
title: 代码片段-字母转数字
tags:
  - java
  - utils
categories:
  - java
date: 2012-03-13 15:39:54
---

## 说明 ##
本工具类可以匹配字符串中字母，并将其转换为数字，反之可行，适用于小范围查找替换。

## 大写字母转数字工具类 ##

```code
public static String char2num(String code){
	Pattern pat = Pattern.compile(REG_ALL_LETTERS);
	Matcher mat = pat.matcher(code);
	
	//遍历所有匹配项
	StringBuffer sb = new StringBuffer();
	while(mat.find()){
		mat.appendReplacement(sb,c2i(mat.group()));
	}
	mat.appendTail(sb);

	return sb.toString();
}

private static String c2i(){
	int i = c.charAt(0) - NUM_C2I;
	return Integer.toString(i);
}
```
