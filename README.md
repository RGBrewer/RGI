///////////////////////////////////////////////////////////////
//bootstrap css & js///////////////////////////////////
///////////////////////////////////////////////////////////////
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js">

<meta name="viewport" content="width=device-width, initial-scale=1">

///////////////////////////////////////////////////////////////
//jquery//////////////////////////////////////////////
///////////////////////////////////////////////////////////////
<script
  src="https://code.jquery.com/jquery-3.1.1.min.js"
  integrity="sha256-hVVnYaiADRTO2PzUGmuLJr8BLUSjGIZsDYGmIJLv2b8="
  crossorigin="anonymous"></script>
<script src="js/bootstrap.min.js"></script>


<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>title</title>
    <link rel="stylesheet" href="style.css">
    <script src="script.js"></script>
  </head>
  <body>
    <!-- page content -->
  </body>
</html>


/*     PHP      */ 

session_start(); //must be at top of page before headers are sent. 
remember to sanitize inputs. 
$_SESSION["favcolor"] = "green";


//connects to the database
<?php 
$connection = mysqli_connect('localhost', 'root', '','lp2');
if ($connection) {
	//echo "Connected to database";
	}else{ die("Failed to connect");}
?>

global $connection; in every function

 
//CREATE

$age = mysqli_real_escape_string($connection, $_POST['title']); //SANITIZE INPUTS!

$query = "INSERT INTO posts(title,link,category,submitter,postDate,image) WHERE id=$id "; //Crucial ending space
$query .= "VALUES ('$title','$link','$category','$submitter','$postDate','$image')";

$result = mysqli_query($connection, $query);

	if (!$result){
		die("Query failed to post..." .  mysqli_error($result));
	}else{echo "Post created.";}
}

//READ///

function displayPosts($limit){
	if($limit == 0){
		echo $limit;
	}
	global $connection; //VITAL
	$query = "SELECT * from posts order by id desc limit $limit";
	$result = mysqli_query($connection, $query);
	
		if (!$result){
		die("Query failed");
	}

	//for every row in mysql
	while ($row = mysqli_fetch_assoc($result)){
		//pull all the data
	$id = $row['id'];
	$title = $row['title'];
		//get how many comments for that id
	$commentCountQuery = "SELECT COUNT(*) as total FROM comments where id=$id ";
		$result2 = mysqli_query($connection, $commentCountQuery);
		if (!$result2){
		die("Comment Count Query failed");
		}
		$temp = mysqli_fetch_assoc($result2);
		$commentCount = $temp['total'];

	stylePosts($category, $postDate, $link, $title, $id, $submitter, $commentCount, $image);
	
	}
}

////UPDATE////

<?php 
function update(){
	global $connection; //VITAL
	$username = $_POST['username']; //get from post
	$password = $_POST['password'];
	$id = $_POST['id'];

$query = "UPDATE users SET ";
$query .= "username = '$username', ";
$query .= "password = '$password' ";
$query .= "WHERE id = $id";

$result = mysqli_query($connection, $query);
	if (!$result) {
		die("<BR>Unable to update.");
	}else{
		echo "Updated.";
	}
}



// DELETE //
function deletePosts(){
global $connection; //VITAL
	$id = $_POST['id'];
$query = "DELETE FROM posts WHERE id=$id";
$result = mysqli_query($connection, $query);
	if (!$result) {
	//////////FAIL////////
		die("<BR>Unable to delete record." . mysqli_error($connection));
	}else{
	////////SUCCESS///////
		echo "deleted.";
	}
}




/*   JQUERY   */


$("p").css("background-color", "yellow");

////////////////////////////
EVENTS
////////////////////////////
$("p").click(function(){ 
    $(this).hide();   //.show
});
.mouseenter(){}
.mouseleave(){}

$(document).ready(function(){
   // jQuery methods go here...
});

 ///////AJAX//////////
 $(document).ready(function(){
    $("button").click(function(){
        $("#div1").load("demo_test.txt");
    });
});
</script>
</head>
<body>
<div id="div1"></h2></div>
<button>Get External Content</button>






/* BOOTSTRAP */
https://v4-alpha.getbootstrap.com/components/forms/
https://www.w3schools.com/bootstrap/bootstrap_forms_inputs.asp

Add class .form-control to all textual <input>, <textarea>, and <select> elements

Input types:  text, password, datetime, datetime-local, date, month, time, week, number, email, url, search, tel, and color.




















<form>
  <div class="form-group">
    <label for="exampleInputEmail1">Email address</label>
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Password</label>
    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
  </div>
  <div class="form-group">
    <label for="exampleSelect1">Example select</label>
    <select class="form-control" id="exampleSelect1">
      <option>1</option>
      <option>2</option>
      <option>3</option>
      <option>4</option>
      <option>5</option>
    </select>
  </div>
  <div class="form-group">
    <label for="exampleSelect2">Example multiple select</label>
    <select multiple class="form-control" id="exampleSelect2">
      <option>1</option>
      <option>2</option>
      <option>3</option>
      <option>4</option>
      <option>5</option>
    </select>
  </div>
  <div class="form-group">
    <label for="exampleTextarea">Example textarea</label>
    <textarea class="form-control" id="exampleTextarea" rows="3"></textarea>
  </div>
  <div class="form-group">
    <label for="exampleInputFile">File input</label>
    <input type="file" class="form-control-file" id="exampleInputFile" aria-describedby="fileHelp">
    <small id="fileHelp" class="form-text text-muted">This is some placeholder block-level help text for the above input. It's a bit lighter and easily wraps to a new line.</small>
  </div>
  <fieldset class="form-group">
    <legend>Radio buttons</legend>
    <div class="form-check">
      <label class="form-check-label">
        <input type="radio" class="form-check-input" name="optionsRadios" id="optionsRadios1" value="option1" checked>
        Option one is this and that&mdash;be sure to include why it's great
      </label>
    </div>
    <div class="form-check">
    <label class="form-check-label">
        <input type="radio" class="form-check-input" name="optionsRadios" id="optionsRadios2" value="option2">
        Option two can be something else and selecting it will deselect option one
      </label>
    </div>
    <div class="form-check disabled">
    <label class="form-check-label">
        <input type="radio" class="form-check-input" name="optionsRadios" id="optionsRadios3" value="option3" disabled>
        Option three is disabled
      </label>
    </div>
  </fieldset>
  <div class="form-check">
    <label class="form-check-label">
      <input type="checkbox" class="form-check-input">
      Check me out
    </label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>










Getting info from the database:

controller calls model\sale\order\getOrder($order_id), which returns an array
 of all info from that order. Each array field must be hand-coded within the model. 


------------------------------------------------------------------------------------------------------
controller\sale\order.php
$order_info = $this->model_sale_order->getOrder($this->request->get['order_id']);
	returns an array with all rows from table oc_order
 
model\sale\order.php
	$order_product_query = $this->db->query("SELECT * FROM " . DB_PREFIX . "tableName WHERE order_id = '" . (int)$order_id . "'");

	return array(
	'shipping_tracking'		  => $order_query->row['shipping_tracking'],
	)
------------------------------------------------------------------------------------------------------




Adding field to database, and making it editable.

CRUD

//READ AN EXISTING VALUE///////
Create row in database.
The model queries the database for that order_id and returns an array. You need to tell the array to look for your row. 
On pageview, controller then calls the model, which returns the array of rows.  
Tell the controller to retrieve your new row too, by adding it to the $data[''] array. This makes it available to the view.
Add necessary language to your language file. (Labels and default values mostly)
Create the view to display the values from the db.

//UPDATE//
The catalog\module\checkout\order.php file controls updating orders. Its called via ajax in the admin panel from button-save 
but it does very... very.. strange things..




/////////////////////////////////////////////////////////////////
^^^ Thats the hard way. Heres a custom solution 
/////////////////////////////////////////////////////////////////


In the view, on click, ajax post to a controller or api. the api calls a model and pushes along parameters from GET and POST. the model updates the database and the ajax callback alerts success.

$('#saveTracking').on('click', function() { //note this is just the span for the on click ... 
  trackingNumber = $('.trackingNumber').val(); //... you need the actual inputBox value
      $.ajax({
      type: "POST",
      //we will use a GET request to retrieve the order_id from its input box (via its name)
      //and pass it to api/shipping.php updatetracking()
      url: '<?php echo $catalog; ?>index.php?route=api/shipping/updatetracking&token=' + token + '&order_id=' + $('input[name=\'order_id\']').val(),        
      data: { tracking_number: trackingNumber }, //key value pairs in JSON format
      crossDomain: true, //possibly not necessary
      success: function (msg) {
         alert("Tracking Number Saved"); 
      }
      });
 });

inside the controller or api, we retrieve the variables from POST and GET

	public function updatetracking(){
		$tracking_number = $_POST['tracking_number'];
		//TODO sanitize inputs... this is an admin only page, so not a huge concern
		$order_id = $_GET['order_id'];
		$this->load->model('checkout/order');
		$this->model_checkout_order->setTracking($_POST['tracking_number'], $_GET['order_id']); //calling a function within model checkout order and passing a post and a get

	}


and we are calling this function in the model, and we're done.

	public function setTracking($data,$order_id){
		$this->db->query("UPDATE " . DB_PREFIX . "order SET shipping_tracking = '" . $data . "' WHERE order_id = '" . (int)$order_id . "'");
	}

