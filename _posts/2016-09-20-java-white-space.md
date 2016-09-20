---
layout: post
category: "java"
title: "关于Java空格的那些事"
tags: "Java"
---

摘要---使用Character.isWhitespace(char ch)来判断任意编码的空格字符。  

最近公司要求前台输入框要校验中文空格，无意间发现StringUtils.isNotBlank(String str)这个方法校验时会校验到中文空格，用起来很方便。  

出于好奇，就看了看源码，发现有这么一段：  

    if (Character.isWhitespace(str.charAt(i)) == false)

于是打开Java API文档，看看Character.isWhitespace(char ch)这个方法的说明。  

果然找到了如下这么一段：  

    public static boolean isWhitespace(char ch)
    Determines if the specified character is white space according to Java. A character is a Java whitespace character if and only if it satisfies one of the following criteria:
    It is a Unicode space character (SPACE_SEPARATOR, LINE_SEPARATOR, or PARAGRAPH_SEPARATOR) but is not also a non-breaking space ('\u00A0', '\u2007', '\u202F').
    It is '\t', U+0009 HORIZONTAL TABULATION.
    It is '\n', U+000A LINE FEED.
    It is '\u000B', U+000B VERTICAL TABULATION.
    It is '\f', U+000C FORM FEED.
    It is '\r', U+000D CARRIAGE RETURN.
    It is '\u001C', U+001C FILE SEPARATOR.
    It is '\u001D', U+001D GROUP SEPARATOR.
    It is '\u001E', U+001E RECORD SEPARATOR.
    It is '\u001F', U+001F UNIT SEPARATOR.
    Note: This method cannot handle supplementary characters. To support all Unicode characters, including supplementary characters, use the isWhitespace(int) method.
    
    Parameters:
    ch - the character to be tested.
    Returns:
    true if the character is a Java whitespace character; false otherwise.
    Since:
    1.1
    See Also:
    isSpaceChar(char)

也就是说，只要是空格，不管是什么编码的，这个方法都可以进行判断。  

