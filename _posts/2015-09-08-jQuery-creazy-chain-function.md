---
layout: post
title: "jQuery疯狂的链式操作"
date:   2015-09-08
subtitle: ""
author: "RryLee"
tags:
    - jQuery
---

个人喜欢 `jQuery` 的原因不只是它简化了 DOM 操作，而是它提供的链式操作。

一个 demo 来体现 jQuery 的链式之类，一个简单的导航

    <style>
        #ul {
            height: 30px;
        }
        #ul>li {
            float: left;
            margin-right: 20px;
            padding: 10px 20px;
            list-style: none;
            background: #e84545;
            color: white;
        }
        #ul .current {
            background: #8e2222;
        }
        #div>p {
            display: none;
        }
        #div .show {
            display: block;
        }
    </style>

    <ul id="ul">
        <li class="current">PHP</li>
        <li>RUBY</li>
        <li>PYTHON</li>
    </ul>

    <div id="div">
        <p class="show">The standard PHP interpreter, powered by the Zend Engine, is free software released under the PHP License.</p>
        <p>For other uses, see Ruby (disambiguation). "Ruby red" redirects here.</p>
        <p>A python is a constricting snake belonging to the Python (genus), or, more generally, any snake in the family Pythonidae (containing the Python genus).</p>
    </div>

    <script src="http://cdn.bootcss.com/jquery/3.0.0-alpha1/jquery.min.js"></script>
    <script>
        (function() {
            $('#ul>li').click(function() {
                $(this).addClass('current')
                    .siblings().removeClass('current').parent().next().children()
                    .eq($(this).index()).addClass('show')
                    .siblings().removeClass('show');
            });
        })(jQuery);
    </script>

一行代码解决，这种体验是原生JS不能带来的。

最后，推荐一篇博客，[隐居大理钻研技术的 hacker](http://teahour.fm/) 可以在里面找到，关于 web 的从古至今两位大牛聊了很多。
