---
layout: page
title: UB3RC0D3R
tagline: Code...Code...Code...
---
{% include JB/setup %}

## Programming Questions


<ul class="posts">
<table class="table table-striped">  
        <thead>  
          <tr>  
            <th>Problem </th>  
            <th>post Date</th>
          </tr>  
        </thead>  
        <tbody>    
  {% for post in site.posts %}

          <tr>
          	<td class="active"><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></td>
          	<td><span>{{ post.date | date_to_string }}</span></td></tr>
  {% endfor %}
  </tbody></table>
</ul>

