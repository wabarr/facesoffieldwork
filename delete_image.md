---
layout: page
---

<script src="http://code.jquery.com/jquery.min.js"></script>
<script>
	$( document ).ready(function() {
		$( "#delete-button" ).click(function(e) {
			e.preventDefault()
			var deletehash = $("#deletehash").val();
			var url = "https://api.imgur.com/3/image/" + deletehash;
			$.ajax({
			  url: url,
			  type: "DELETE",
			  headers: {
			    "Authorization": "Client-ID 893f12a98c220db"
			  },
			  success: function(response) {
				  $("#success").html("image successfully deleted")
				  
			  },
			  error: function(response){
			  	  $("#failure").html("deletion failed")
			  },
			});
		});
	});
</script>
	
<div id="success"></div>
<div id="failure"></div>
<div id="curlstring"></div>
<form id="deleteform">
	<input id="deletehash" placeholder="imgur delete hash">
	<input id="delete-button" type="submit">
</form>