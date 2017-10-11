---
title: keystone学习
date: 2017-10-10 17:20:04
tags:
---


## express

<!--more-->

## mongodb mongoose

### schema 的域 虚拟域 方法 静态域 前置钩子 后置钩子

- 域（理解为字段,如title就是域）
```
Post.add({
    title: { type: String, required: true },
    state: { type: Types.Select, options: 'draft, published, archived', default: 'draft' },
    author: { type: Types.Relationship, ref: 'User' },
    createdAt: { type: Date, default: Date.now },
    publishedAt: Date,
    image: { type: Types.CloudinaryImage },
    content: {
        brief: { type: Types.Html, wysiwyg: true, height: 150 },
        extended: { type: Types.Html, wysiwyg: true, height: 400 }
    }
});
```

- 虚拟域(该属性不写入数据库,用于计算属性)
```
User.schema.virtual('canAccessKeystone').get(function () {
	return this.isAdmin;
});


 PersonSchema.virtual('name.full').set(function(name){
      var split = name.split(' ');
      this.name.first = split[0];
      this.name.last = split[1];
    });
```
- 方法
```
Post.schema.methods.isPublished = function() {
    return this.state == 'published';
}
```
- 静态域
```

```
- 前置钩子
```
Post.schema.pre('save', function(next) {
    if (this.isModified('state') && this.isPublished() && !this.publishedAt) {
        this.publishedAt = new Date();
    }
    next();
});
```
- 后置钩子
```

```

### 数据类型

数据类型	域类型
String	Text
Number	Number
Date	DateTime
Boolean	Boolean


### 域参数（增加域时可以使用的参数）

label String	每个域的标签都是由域路径生成的；设置这个参数会覆盖默认值。
required Boolean	在条目保存前验证这个域是有值的(还会传给mongoose并强制使用数据库索引)。
initial Boolean	让这个域出现在管理界面中的创建条目表单中。
noedit Boolean	在管理界面中将这个域渲染为只读域。
note String	在管理界面中跟着域显示。
hidden Boolean	如果设为true，则该域在管理界面中一直是隐藏域。
collapse Boolean	该域没有值时在管理界面中显示一个+ 添加链接。当noedit也被设为true时，该域没值时则完全隐藏。
dependsOn Object	只有对象中指定的路径跟条目的当前数据匹配时才会显示 你可以在每个路径上用数组对准多个值。

## pug


