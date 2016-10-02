---
layout: page
---
<script src="http://code.jquery.com/jquery.min.js"></script>
<script>
	$( document ).ready(function() {
		$("#formspree").hide();
		$("#instructions").hide();
		$("#expandinstructions").click(function(e){
			$("#instructions").show();
		});
		$( "#submit-button" ).click(function(e) {
			var formData = new FormData();
			var imageData = $("#img-input")[0].files[0];
			formData.append("image",imageData);
			$.ajax({
			  url: "https://api.imgur.com/3/image",
			  type: "POST",
			  datatype: "json",
			  headers: {
			    "Authorization": "Client-ID 893f12a98c220db"
			  },
			  data: formData,
			  success: function(response) {
				  $("#failureupload").hide();
				  $("#instructions").hide();
				  $("#imguploadform").hide();
				  $("#successupload").html("<img src=" + response.data.link + "></a>");
				  $("#formspree").show();
				  $("#imgurlink").val(response.data.link);
				  $("#imgurdelete").val(response.data.deletehash);
				  
			  },
			  error: function(response){
			  	  $("#failureupload").html("something went wrong...maybe you should try again?");
				  //window.location.href="upload_image.html";
			  },
			  cache: false,
			  contentType: false,
			  processData: false
			});
		});
	});
</script>

<div id="failureupload"></div>
<div id="successupload"></div>

<form id="imguploadform" method="POST" enctype="multipart/form-data">
	<input type="file" id="img-input" name="image" accept="image/*">
	<input type="button" id="submit-button" value="upload image">
</form>

<div id="formspree">
	<form action="https://formspree.io/fof.contribute@gmail.com" method="POST">
		<input type="email" name="_replyto" placeholder="Your email address">
		<input type="text" name="submittername" placeholder="Your name">
		<input type="text" name="location" placeholder="Where was the photo taken?">
	    <textarea style="width: 100%; height: 150px;" name="the story" placeholder="What's the story of this photo"></textarea>
		<input type="text" name="photo-link" type="hidden" id="imgurlink">
		<input type="text" name="imgur-delete-hash" type="hidden" id="imgurdelete">
		<input type="hidden" name="_subject" value="New FOF submission!" />
		<input type="text" name="_gotcha" style="display:none" />
		<input type="hidden" name="_next" value="thanks.html" />
	    <input type="submit" value="Tell us your story">
	</form>
</div>

What happens to my image? <i class="fa fa-plus" aria-hidden="true" id="expandinstructions"></i>
<div id="instructions">

<p> The image will automatically be hosted on <a href="https://help.imgur.com/hc/en-us/articles/201746817-Post-privacy">imgur.com</a>. The image will not be publicly searchable, rather imgur is only used to host the photo on the internet. The image is only accessible through a direct link.</p>

<p>Note: by uploading your image here you indicate that you hold the copyright to the image and that you wish to share it publicly.</p>

</div>


