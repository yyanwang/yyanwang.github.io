---
layout: page
---

{% for post in site.posts %}
<div class = "card">
		<div  class = "date_label">
			<span class="day_month">
      			{{ post.date | date:"%m/%d" }}
      			</span>
      			<span class="year">
      			{{ post.date | date:"%Y" }}
      			</span>
      		</div> 
		{{ post.content  | | split:'<!--break-->' | first }}
	<div class = "read_more">
		<a class="fa fa-link" href="{{ BASE_PATH }}{{ post.url }}">  查看全文&hellip;</a>
	</div>
	
</div>

{% endfor %}



