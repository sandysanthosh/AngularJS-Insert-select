Welcome to the AngularJS-Insert-select wiki!


angularjs:
--add angularjs
--add bootstrap

 <div ng-app="myapp" ng-controller="usercontroller" ng-init="displayData()">
 <input type="text" name="firstname" ng-model="firstname" class="form-control">
 <label>firstname</label>
 <br/>
 <label>Lastname></label>
 <input type="text" name="lastname" ng-model="firstname" class="form-control">
 <br/>
 <input type="submit" name="btnInsert" class="btn btn-info" ng-click="insertData()" value="ADD"/> 
 <table class="table table-bordered">
 <tr>
   <th>Firstname</th>
   <th>Lastname</th>
</tr>
 <tr ng-repeat="x in names">
   <td> {{ x.firstname }} </td>
   <td>{{ x.Lastname }} </td>
</tr>
</div>
</div>
</body>
</html>

<script>
var app=angular.modular("myapp",[]);

app.controller("usercontroller",function($scope,$http){
$scope.insertData=function(){
$http.post(
"insert.php",
{'firstname':$scope.firstname,'lastname':$scope.lastname}
).success(function(data){
alert(data);
$scope.firstname=null;
$scope.lastname=null;
$scope.displayData();
});
}

$scope.displayData=function(){
$http.get("select.php")
.success(function(data){
$scope.names=data;
}
});



php file:


<?php

//insert.php


$connect=mysql_connect("localhost","root","testing");
$data=json_decode(file_get_contents("php://input"));
if(count($data > 0))
{
$firstname= mysqli_real_escape_string($connect,$data->firstname);
$lastname= mysqli_real_escape_string($connect,$data->lastname);
$query="INSERT INTO tbl_user(firstname,last_name) VALUES ('$firstname','$lastname');
if(mysqli_query($connect,$query))
{
echo "Data Inserted..";
}
else
{
echo "error";
}
?>

-->php file
//select.php
   
$connect = mysqli_connect("localhost","root","","testing");
$output= array();
$query="SELECT * FROM tbl_user";
$result= mysqli_query($connect,$query);
if(mysql_num_rows($result) > 0)
{
while($rows= mysqli_fecth_array($result))
{
$output[]=$row;
}
echo json_encode($output);
}



youtube  link:

https://www.youtube.com/watch?annotation_id=annotation_2583773695&feature=iv&src_vid=Y_nJIp0UqI0&v=TMkNON3aBmU
https://www.youtube.com/watch?v=Y_nJIp0UqI0


