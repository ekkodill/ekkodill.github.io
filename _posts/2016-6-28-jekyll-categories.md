---
layout: post
title: How to add categories on jekyll
category: webdev
category-url: webdev
---


`1. Create "category.html" in the _layouts folder.`


```liquid
{% raw %}
---
layout: default
type: archive
---
<div class="archive-description">
  <h1 class="archive-title">{{ page.category }} Archive</h1>
  {{ content }}
</div>

<div class="wrap">
{% if site.categories[page.category] %}
  <div class="group-year">
    {% for post in site.categories[page.category] %}
      {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
      {% unless year == this_year %}
        {% assign year = this_year %}
        <p>{{ year }}</p>
      {% endunless %}
      <article>
        <h3><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h3>
        <time>
          <span class="month">{{ post.date | date: "%b" }}</span>
          <span class="day">{{ post.date | date: "%d" }}</span>
          <span class="year">{{ post.date | date: "%Y" }}</span>
        </time>
      </article>
    {% endfor %}
  </div>
{% else %}
  <p>There are no posts in this category.</p>
{% endif %}
</div>
{% endraw %}
```

`2. Create "post-categories.html" in the _inclues folder folder.`

```html
<span class="entry-categories"><a href="{{ site.url }}/{{ page.category-url }}/" rel="category">{{ page.category }}</a></span>
```


`3. Create a new folder in the root directory called "_pages"`

`4. Create a new file inside "_pages" dir called e.g "fishing.md"`

```liquid
---
layout: category
title: How to fish
description: How to's for fishing
category: fishing
permalink: /fishing/
---
Fishing category with how to's for fishing
```


`5. Create a new post and include this`

```liquid
category: fishing
category-url: fishing
```

`6. Include this in _config.yml`

```liquid
include: ["_pages"]
```

`7. url in _config.yml needs to be either proper for local dev or published`

```liquid
url: http://127.0.0.1:4000 or url: username.github.io
```

