---
layout: single
author_profile: true
---

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!--include the projects.yml file-->
{% assign projects = site.data.projects %}

<body> 
<input type="button" value="Apply Filters" onclick="show_filters()">
<input type="button" value="Clear All Filters" onclick="location.href='{{ "/projects/" | prepend:site.baseurl }}';">
<p style="font-size: 0.80em;" id="applied_filters"></p>
<div id="filters" style="display: none;"> 
	<form action="{{ "/projects/" | prepend:site.baseurl }}" style="padding:0px;background-color:#eef1f6">
	  <table style="display:inline-table">
	  <tr>
	  {% for item in projects.filters %}
		{% if item == "break" %}
		</tr><tr>
		{% continue %}
		{% endif %}
		  <td style="border:none"><input type="checkbox" name="skill" value="{{item}}"> {{item}}</td>
	  {% endfor %}    
	  </tr>
	  
	  <tr>
	  <td colspan="{{projects.filters_colspan}}" align="center" style="border:none"><input type="submit" value="Submit">  <input type="reset" value="Reset"></td>
	  </tr>
	  </table>
	</form>
</div> 

<table style="width:150%">
  {% for project_row in projects.project_rows %}
  <tbody id="{{project_row.id}}">
  <tr>
    <td rowspan="2"><img src="{{ project_row.image_source  | prepend:site.baseurl }}"  onclick="location.href='{{project_row.url}}';" style="cursor: pointer;"/></td>
	<td style="border:none"><h1 style="cursor: pointer;" onclick="location.href='{{project_row.url}}';">{{project_row.name}}</h1><p>{{project_row.abstract}}</p></td>
  </tr>
  <tr>
    <td class="keywords"><i>Keywords: </i>{{project_row.keywords}}</td>
  </tr>
  </tbody>
  {% endfor %}
  
</table>

<script> 
function toggler(divId) { 
	$("#" + divId).toggle(); 
} 

function show_filters() { 
	toggler('filters'); 
} 

function searchToObject() {

  var pairs = window.location.search.substring(1).split("&"),
    skill_array = [],
    pair,
    i;

  for ( i in pairs ) {
    if ( pairs[i] === "" ) continue;

    pair = pairs[i].split("=");
    skill_array.push(decodeURIComponent( pair[1] ).toString().replaceAll("+"," ").toLowerCase());
  }
  
  return skill_array;
}


$(document).ready(function() {

  // get query from form as object
  var query_object = searchToObject();
  
  // check query_object is empty or not
  if (typeof query_object  == 'undefined' || query_object.length == 0){
	// hide nothing
  }
  else{
	document.getElementById("applied_filters").innerHTML = "Applied Filters	: "+query_object
	var keywords = document.getElementsByClassName("keywords");
	for(var i=0; i<keywords.length; i++) {
		row_keywords_arr = keywords[i].innerHTML.toLowerCase().replace("<i>keywords: </i>","").split(",").map(s => s.trim())

		intersection = row_keywords_arr.filter(x => query_object.includes(x))
		
		if(intersection.length == 0){
			// hide it
			row_id_to_hide = keywords[i].closest("tbody").id

			toggler(row_id_to_hide)
		}
	}
	
  }
});
</script> 

</body>
