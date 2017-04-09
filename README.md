# RGI

///////////////////////////////////////////////////////////////
//bootstrap css & js///////////////////////////////////
///////////////////////////////////////////////////////////////
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js">



///////////////////////////////////////////////////////////////
//jquery//////////////////////////////////////////////
///////////////////////////////////////////////////////////////
<script
  src="https://code.jquery.com/jquery-3.1.1.min.js"
  integrity="sha256-hVVnYaiADRTO2PzUGmuLJr8BLUSjGIZsDYGmIJLv2b8="
  crossorigin="anonymous"></script>
<script src="js/bootstrap.min.js"></script>





/*     PHP      */ 

//connects to the database
<?php 
$connection = mysqli_connect('localhost', 'root', '','lp2');
if ($connection) {
	//echo "Connected to database";
	}else{ die("Failed to connect");}
?>

global $connection; in every function


//CREATE
$query = "INSERT INTO posts(title,link,category,submitter,postDate,image) ";
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
