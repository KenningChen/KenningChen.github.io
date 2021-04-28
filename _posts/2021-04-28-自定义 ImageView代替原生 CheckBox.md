---
layout: post
title: "自定义 ImageView 代替原生 CheckBox"
subtitle: ""
author: "kenning"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  -  Android
--- 
在开发过程中，经常会用到 checkbox，这很简单，霸特，产品要的并不是系统自带的样式。所以我们就只能自定义样式，看似没毛病了，然而限制太多了，checkbox 再怎么改样式，图片资源的尺寸大小在影响着 checkbox 的大小，也就是 checkbox 的大小不能自己随意设置大小，如果 checkbox 设置的小了，那么你设置的样式就显示不全，设置大了，又靠右显示，还无法偏移不能做到居中，真是够了。所以最后决定自定义 imageview 来代替 checkbox，话不多说，直接上代码：
<br>
首先就是设置属性（目前我这就只需要这么些）

```
<declare-styleable name="SwitchImageView">
        <attr name="checkOffBackground" format="color|reference"/>
        <attr name="checkOnBackground" format="color|reference"/>
        <attr name="checkstate" format="boolean"/>
    </declare-styleable>
```
自定义 view获取属性（我这里图片没有设置默认值）
```
        TypedArray a = getContext().obtainStyledAttributes(attrs, R.styleable.SwitchImageView);
        //选中时的图片资源
        mNormalDrawable = a.getDrawable(R.styleable.SwitchImageView_checkonBackground);
        //未选中时的图片资源
        mPressedDrawable = a.getDrawable(R.styleable.SwitchImageView_checkoffBackground);
        checked = a.getBoolean(R.styleable.SwitchImageView_checkstate, false);
        a.recycle();
```

在自定义 imageview 中，添加监听事件
```
public void setOnSwitchListener(OnSwitchListener listener) {
        this.listener = listener;
    }

    private OnSwitchListener listener;

    public interface OnSwitchListener {
        void checkedChangeListener(boolean isChecked);
    }

    public void setChecked(boolean checked) {
        this.checked = checked;
        if (checked) {
            setImageDrawable(mPressedDrawable);
        } else {
            setImageDrawable(mNormalDrawable);
        }
        if (listener!=null)
            listener.checkedChangeListener(checked);
    }
```
把上面的`setChecked`方法绑定到`OnClickListener`中，

```
setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                setChecked(!checked);
            }
        });
```

上述用到的变量`checked`在自定义 view 中定义，默认值为false（未选中状态），activity 中调用直接**`view.setOnSwitchListener`**
<br>
好了，目前这些可以应对一下就先这样把