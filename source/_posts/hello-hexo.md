---
title: hello-hexo
date: 2017-09-30 13:06:10
tags:
---

# 命令
```
hexo init [folder]
hexo new [layout] <title>
hexo generate hexo g
hexo publish [layout] <filename>
hexo server
hexo deploy hexo d
```


# 引用示例

- 没有提供参数，则只输出普通的 blockquote
{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

- 引用书上的句子
{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy.
{% endblockquote %}

- 引用 Twitter
{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %}

- 引用网络上的文章
{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}



# 代码块

-普通的代码块
{% codeblock %}
alert('Hello World!');
{% endcodeblock %}

- 指定语言
{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

- 附加说明
{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

- 附加说明和网址
{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]);
=> [1, 2, 3]
{% endcodeblock %}

- 反引号代码块

``` [language] [title] [url] [link text] code snippet ```

# Pull Quote
{% pullquote [class] %}
content
{% endpullquote %}

# jsFiddle

{% jsfiddle shorttag [tabs] [skin] [width] [height] %}

# Gist

{% gist gist_id [filename] %}

# iframe
{% iframe url [width] [height] %}

# Image
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

# Link
{% link text url [external] [title] %}

# Include Code
{% include_code [title] [lang:language] path/to/file %}

# Youtube
{% youtube video_id %}

# Vimeo
{% vimeo video_id %}

# 引用文章
{% post_path slug %}
{% post_link slug [title] %}

# 引用资源
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}

# Raw
{% raw %}
content
{% endraw %}


# 数据文件
<% for (var link in site.data.menu) { %>
  <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% } %>


