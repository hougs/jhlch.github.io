---
layout: page
title: Recent Posts 
---
{% include JB/setup %}


<ul class="posts">
  {% for post in site.posts %}
    <article class="unit-article layout-post">
    <div class="unit-inner unit-article-inner">
        <div class="content">
            <div class="bd">
                <div class="entry-content">
                    {{ post.content }}
                </div><!-- entry-content -->
            </div><!-- bd -->
        </div><!-- content -->
    </div><!-- unit-inner -->
    </article>
  {% endfor %}
</ul>
