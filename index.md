---
layout: default
---



<button id="All" onclick="filterUsingCategory('All')">
  *Show All Posts*
</button>
{% assign categories = site.categories | sort %}
{% for category in categories %}
  {% assign cat = category | first %}
  <button id="{{ cat }}" onclick="filterUsingCategory(this.id)">
    {{ cat }}
  </button>
{% endfor %}

{% assign id = 0 %}
{% for post in site.posts %}
  {% assign id = id | plus:1 %}
  <div class="post" id="{{id}}">
    <p class="itemInteriorSection">
      <a href="{{post.url}}">{{ post.articletitle }}</a><br />
      <!-- more post details here -->
    </p>
  </div>
{% endfor %}

<script type="text/javascript">
  function filterUsingCategory(selectedCategory) {
    var id = 0;
    {% for post in site.posts %}
      var cats = {{ post.categories | jsonify }}

      var postDiv = document.getElementById(++id);
      postDiv.style.display =
        (selectedCategory == 'All' || cats.includes(selectedCategory)) 
          ? 'unset' 
          : 'none';
    {% endfor %}
  }
</script>
<!-- <div class="posts">
  {% for category in site.categories %}
    <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
    </article>
  {% endfor %}
</div> -->