## Welcome to Big-Fat-Software-Inc.GitHub.io

Recent Posts:
- [Base64 Encoding in JavaScript](http://big-fat-software-inc.github.io/Base64%20Encoding%20in%20JavaScript.html)
- [Memory Usage in WebSites](http://big-fat-software-inc.github.io/Memory%20Usage%20in%20WebSites.html)
- [All Posts](http://big-fat-software-inc.github.io/all%20posts.html)

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/big-fat-software-inc/big-fat-software-inc.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out. [Link](url) and ![Image](src). For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).


### All Posts
{% for post in site.posts %}
  <a href='{{ post.url }}'>{{ post.title }}</a>
  {% if post.path contains 'react' %}
      <a href='{{ post.url }}'>----{{ post.title }}</a>
  {% endif %}
{% endfor %}  