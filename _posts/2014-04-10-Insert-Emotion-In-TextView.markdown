---
layout: post
title: 在TextView中插入表情
tags: textview
categories: android
---

主要使用的类
---
[SpannableString](http://developer.android.com/reference/android/text/SpannableString.html)


This is the class for text whose content is immutable but to which markup objects can be attached and detached. For mutable text, see [SpannableStringBuilder](http://developer.android.com/reference/android/text/SpannableStringBuilder.html). 

SpannableString用于不可变长度的文字，但是可以改变或者替换其中文字;对于可变长度的文字请使用SpannableStringBuilder。



使用
---
        SpannableString mSpan = new SpannableString(String text);
        mSpan.setSpan(Object what, int start, int end, int flags);
        
例如替换成图片可以这样写：

Drawable drawable = getResources().getDrawable(R.drawable.icon);   
drawable.setBounds(0, 0, drawable.getIntrinsicWidth(),drawable.getIntrinsicHeight());    
msp.setSpan(new ImageSpan(drawable), 30, 30, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);  
          

