---
layout: single
author_profile: true
---

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<body> 
<input type="button" value="Apply Filters" onclick="show_filters()">
<input type="button" value="Clear All Filters" onclick="location.href='{{ "/projects/" | prepend:site.baseurl }}';">

<div id="filters" style="display: none;"> 
	<form action="{{ "/projects/" | prepend:site.baseurl }}" style="padding:0px">
	  <table style="display:inline-table" rules="none">
	  <tr>
	  <td><input type="checkbox" name="skill" value="NLP"> NLP</td>
	  <td><input type="checkbox" name="skill" value="HTML"> HTML</td>
	  <td><input type="checkbox" name="skill" value="Python"> Python</td>
	  </tr>
	  <tr>
	  <td colspan="3" align="center"><input type="submit" value="Submit">  <input type="reset" value="Reset"></td>
	  </tr>
	  </table>
	</form>
</div> 

<table style="width:150%">
  <tbody id="1">
  <tr>
    <td rowspan="2"><img src="{{ "/assets/images/capitalbike.png" | prepend:site.baseurl }}"  onclick="location.href='https://sheldonsebastian.github.io/Capital-Bikeshare/';"/></td>
	<td style="border:none"><h2 onclick="location.href='https://sheldonsebastian.github.io/Capital-Bikeshare/';">Capital Bikeshare</h2><p> Capital Bikeshare is very popular and always in demand service.
This project predicts the number of bikes to use per hour and have contingencies to fulfill the demand. 

Various factors such as weather, temperature, working, or non-working hour, the hour of the day are factors to determine the number of bikes.</p></td>
  </tr>
  <tr>
    <td class="keywords"><i>Keywords:</i> NLP, HTML</td>
  </tr>
  </tbody>
  <tbody id="2" onclick="location.href='https://sheldonsebastian.github.io/Capital-Bikeshare/';">
  <tr>
    <td rowspan="2"><img src="{{ "/assets/images/atus.png" | prepend:site.baseurl }}" /></td>
	<td style="border:none"><h2>Capital Bikeshare</h2><p> Capital Bikeshare is very popular and always in demand service.
This project predicts the number of bikes to use per hour and have contingencies to fulfill the demand. 

Various factors such as weather, temperature, working, or non-working hour, the hour of the day are factors to determine the number of bikes.</p></td>
  </tr>
  <tr>
    <td class="keywords"><i>Keywords:</i> NLP, HTML</td>
  </tr>
  </tbody>
  <tbody id="3">
  <tr>
    <td rowspan="2">Image 2</td>
    <td>Capital Bikeshare</td>
  </tr>
  <tr>
    <td class="keywords"><i>Keywords:</i> Python, Machine Learning</td>
  </tr>
  </tbody>
  <tbody id="4">
  <tr>
    <td rowspan="2">Image 3</td>
    <td>Traffic Prediction</td>
  </tr>
  <tr>
    <td class="keywords"><i>Keywords:</i> Python, Machine Learning, Time Series</td>
  </tr>
  </tbody>
  
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
    skill_array.push(decodeURIComponent( pair[1] ).toLowerCase());
  }
  
  return skill_array;
}


$(document).ready(function() {

  // get query from form as object
  var query_object = searchToObject();
  
  // check query_object is empty or not
  if (typeof query_object  == 'undefined' || query_object.length == 0){
	// console.log("Empty, so show all")
  }
  else{
	// console.log(query_object)
	// iterate through each row and perform union and if result is not none then show, else hide row
	var keywords = document.getElementsByClassName("keywords");
	// console.log(keywords)
	for(var i=0; i<keywords.length; i++) {
		row_keywords_arr = keywords[i].innerHTML.toLowerCase().replace("<i>keywords:</i>","").split(",").map(s => s.trim())
		// console.log(row_keywords_arr )
		intersection = row_keywords_arr.filter(x => query_object.includes(x))
		
		if(intersection.length == 0){
			// hide it
			row_id_to_hide = keywords[i].closest("tbody").id
			// console.log(row_id_to_hide)
			toggler(row_id_to_hide)
		}
	}
	
  }
});
</script> 

</body>
