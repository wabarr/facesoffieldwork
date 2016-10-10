---
layout: default
---
<script src="http://code.jquery.com/jquery.min.js"></script>
<script>
	$( document ).ready(function() {
		$("#expandinstructions").click(function(e){
			$("#instructions").toggleClass("visible hidden");
			$("#expandinstructions").toggleClass('fa-plus-circle fa-minus-circle')
		});
		$( "#submit-button" ).click(function(e) {
			$("#uploadprogress").toggleClass("visible hidden");
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
				  $("#uploadprogress").toggleClass("visible hidden");
				  $("#failureupload").remove();
				  $("#whathappens").remove();
				  $("#instructions").remove();
				  $("#imguploadform").remove();
				  $("#successupload").html("<img src=" + response.data.link + "></a>");
				  $("#formspree").removeClass("hidden").addClass("visible");
				  $("#imgurlink").val(response.data.link);
				  $("#imgurdelete").val(response.data.deletehash);
				  
			  },
			  error: function(response){
				  $("#uploadprogress").removeClass("visible").addClass("hidden");
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

<div class="my-text-body">
<h3>Share your story</h3>

<p>Upload your photo to share your story with Faces of Fieldwork. You can share your story after uploading the photo. The photo should be square, and the resolution should be at least 1024 x 1024. Maximum file size is 10mb.</p>



<div id="failureupload" class="error"></div>
<div id="successupload"></div>

<div class="my-text-body">
	<form id="imguploadform" method="POST" enctype="multipart/form-data">
		<div class="row">
			<input type="file" id="img-input" name="image" accept="image/*" style="padding-left:110px">
		</div>
		<div class="row">
			<input type="button" id="submit-button" value="upload image">
		</div>
		<div class="row" class="hidden" id="uploadprogress">
			<i class="fa fa-spinner fa-pulse fa-2x fa-fw"></i>
		</div>
	</form>
</div>

<div id="whathappens">
What happens to my image? <i class="fa fa-plus-circle" aria-hidden="true" id="expandinstructions"></i>
</div>

<div id="instructions" class="hidden">

 <p> The image will automatically be hosted on <a href="https://help.imgur.com/hc/en-us/articles/201746817-Post-privacy">imgur.com</a>. The site imgur.com is only used to host the photo on the internet. The image you upload is accessible through a direct link, and is hosted anonymously on the imgur site. It is not viewable in public imgur galleries or imgur searches.</p>

 <p>Note: by uploading your image here you indicate that either you took the photo personally or that you hold the copyright to the image and that you wish to share it publicly.</p>

</div>

<div id="formspree" class="hidden">
	<form action="https://formspree.io/fof.contribute@gmail.com" method="POST">
		<input type="email" name="_replyto" placeholder="Your email address">
		<input type="text" name="twitterhandle" placeholder="Your twitter handle">
		<input type="text" name="submittername" placeholder="Your name">
		<input type="text" name="location" placeholder="Where was the photo taken?">
	    <textarea style="width: 100%; height: 150px;" name="the story" placeholder="What's the story of this photo"></textarea>
		<input type="text" name="photo-link" type="hidden" id="imgurlink">
		<input type="text" name="imgur-delete-hash" type="hidden" id="imgurdelete">
		<input type="hidden" name="_subject" value="New FOF submission!" />
		<input type="text" name="_gotcha" style="display:none" />
		<input type="hidden" name="_next" value="/thanks/" />
	    <input type="submit" value="Tell us your story">
	</form>
</div>
</div>