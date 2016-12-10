Single page application
madewithangular.com
Model View Controller

Benefits of AngularJS
1) Dependency Injection is the best thing of AngularJS
2) 2 way data binding : change to the view, update the model  // change to the model , updates the view
3)Testing
4) Model View Controller
5) Directive Filters etc

ng-app="myApp"
ng-controller = "myController"
{{}}
{{message}}

Module in angular js
module is a container for different parts of your Application like controller,directive etc.

var app = angular.module("myApp",[])
app.controller("myController",function($scope){   //$scope is angular object
$scope.message = "Angular Js Tutorials"
});

$scope is a object and the property which we attach to scope objects is model
$scope.message = "Angular Js Tutorials";
and  in index.html  {{message}}    //retreiving model from the scope

in script.js
------------
var employee = {firstname : "Yogendra",
				lastname : "Saxena",
				gender : "male"
				photo : "/images/dir/dir/image.jpg" };
				
$scope.employee = employee;    // attaching employee object to $scope object

in index.html
------------
{{employee.firstname}}
<img ng-src = "{{employee.photo}}" alt = "{{employee.firstname}}"  />

2 way data Binding
-------------------
<input type = "text" ng-model="message"/>  // as view updates then model updates , and vice versa
{{message}}

$scope.message = "Hello Angular"


ng-repeat
------------
script.js
 var employee = [
 			{firstname : "Yogendra",
				lastname : "Saxena",
				gender : "male"},
			{firstname : "Yogendra",
				lastname : "Saxena",
				gender : "male"},
			{firstname : "Yogendra",
				lastname : "Saxena",
				gender : "male"}];

index.html
----------
<tr ng-repeat = "emp in employee">
	<td>{{emp.firstname}}</td>
	<td>{{emp.lastname}}</td>
	<td>{{emp.gender}}</td>
 
 //get indexs by using {{$index}}
 {{$parent.$index}}    // generslly used in nested ng-repeat
	
	
functions
----------
<tr ng-repeat="tech in technology>
	<td>{{tech.name}}</td>
	<td>{{tech.likes}}</td>
	<td><input type="button" value="likes" ng-click="incrementlikes(tech)"/></td>
	
	
	
var technology = [
				{name : "macOS",
				likes : "0"},
				{name : "Windows",
				likes : "0"}
				];
$scope.technology = technology;
$scope.incrementlikes = function(tech){
	tech.likes++;
}


Filter
----------
Format
sort
filter data

{{expression | filterName:paramenter}}

lowercase
uppercase
number
date etc
limitTo : can be used to limit the number of rows or character in string
{{expression | limitTo : limit : begin}}

script.js
--------
var employee = [
		{name:"yogendra",dateofbirth: new date("june 19,1994"),salary:23233},
		{name:"yogendra",dateofbirth: new date("june 19,1994"),salary:23233},
		{name:"yogendra",dateofbirth: new date("june 19,1994"),salary:23233}
		];
		
	$scope.employee = employee;
	$scope.rowLimit = 3;
	
index.html
--------
<input type = "number" step="1" min="0" max ="10" ng-model="rowLimit"/>
<table>
<tr ng-repeat="emp in employee | limitTo:rowLimit:1">      // begining with row 2nd , as it starts with 0th index
	<td>{{emp.name | uppercase}}</td>
	<td>{{emp.dateofbirth | date : "dd/mm/yyyy" }}</td>
	<td>{{emp.salary | number:2}}</td>
</tr>
</table>


Sorting Data
-------------
ng-repeat =".... | orderBy:"salary":false"                   //false to sort in dec order and true to asc

index.html
-----------
Order By : <select ng-model="sortColumn">
				<option value="name">Name bhai</option>
				<option value="gender">Gender bhai</option>
				<option value="salary">Salary bhai</option>
			</select>
			
<tr ng-repeat="emp in employee | orderBy:sortColumn:true">
	<td></td>
	<td></td>
	<td></td>
</tr>

script.js
---------
$scope.sortColumn = "name";

Serach Filter
-----------
filter : parameter

<input type="text" ng-model="searchEmployee" />

<tr ng-repeat="emp in employee | filter:searchEmployee" >

</tr>

ng-repeat="emp in employee | filter:searchEmployee:true"         // true for exact match

Search by Multiple properties
-------------------------------
<input type="text" ng-model="searchEmployee.name" />
<input type="text" ng-model="searchEmployee.gender" />
<input type="checkbox" ng-model = "exactMatch">



<tr ng-repeat="emp in employee | filter:searchEmployee:exactMatch" >
		<td>{{emp.name}}</td>
		<td>{{emp.gender}}</td>
		<td>{{emp.salary}}</td>
</tr>


Creating a Custom Filter
--------------------------
let in table male ,female is given as 1 ,2 resp.
then convert it in male ,female resp.

<td>{{emp.gender | gender}}   // gender is a filter we are going to create  // filter is nothing but a function that returns a function// we can have filter in sepeate file as well just give the src

script.js
--------
var app = angular.module("myApp",[])
 app.filter("gender",function(){
 
 	return function(gender){
	
	switch(gender){
	case 1:
		return "male";
	case 2:
		return "female"
				}
			}
 		})
	.controller("myController",function($scope){

..... ... ...
})



ng-hide and ng-show
--------------------
ng-hide = "true"        // true or false

<input type="checkbox" ng-model="hiding"/>
<td ng-hide="hiding">{{emp.firstname}}</td>      // hiding firstname 

OR not hiding instead writing ### in that place

<input type="checkbox" ng-model="hiding"/>
<td ng-hide="hiding">{{emp.firstname}}</td>      // hiding firstname
<td ng-show="hiding">###</td>


ng-init is used to initialse thing before only , instead of doing in controller // but doing in controller is a better practise

ng-include
-----------
make employeetable.html as new file
ng-include = "'employeetable.html'"

OR, you can use it in controller as

ng-include = "employeeview"
and in script.js
 --------------
 $scope.employeeview = "employeetable.html";
 
 other example will be
 
 In Index.html
--------------
select View :
<select ng-model="employeeview">
	<option value="employeetable.html">TABLE</option>
	<option value="employeelist.html">LIST</option>
</select>
<br><br>
<div ng-include="employeeview"></div>

Service in AngularJs
--------------------
it is like an object which we create abd then we can call it any number of time in controller

example
-------
input : YogendraKumarSaxena
output : Yogendra Kumar Saxena
<process string>   // its a button  , when pressed output shud come like above

index.html
------------
INPUT : <input type="text" ng-model = "input"/>
OUTPUT : <input type = "text" ng-model = "output"/>
     <input type = "button" value = "Modify String" ng-click = "transformString()"/>
	 
	 
in script.js
------------
var app = angular
				.module("myApp",[])
				.controller("myController",function($scope,stringService)   //stringService is name of custom service we which we will make
				{
					$scope.transformString = function(input)
					{
					
						$scope.output = stringService.processString(input);
					}
				});
				
now creating service  stringService.js
----------------------------------------
app.factory("stringService", function()
						{
						return{
							processString : function(input)
							{
								if(!input)
									return;
								output+=input[0];
								
								var output = "";
								for(var i =1;i<input.length;i++)
								{
									if(Character.isUpperCase(input[i]))
										output+ = input[i]+" ";
									else
										output+ = input[i];
								}
								return output;
								
							}
						}
						
				})
				
				
Anchorscroll Service
---------------------
// it scroll the page according to the id provided

index.html
----------
<button id="top" ng-click="scrolling("bottom")"> scroll to bottom </button>
<p>.....</p>    //A big paragraph
<button id="bottom" ng-click="scrolling("top")"> scroll to top </button

script.js
------------
.controller("myController",function($scope,$location,$anchorScroll){

	$scope.scrolling = function(scrollTo){
	
		$location.hash(scrollTo);
		$anchorScroll.yOffset = 20;    // gives some scape(padding) between button and brower vendor
		$anchorscroll();
	
	}

});


UI-Routing
----------
there will be no .extension in url when changed
but you need to add the angular route file which does not come with core angular CDN/file
https://angularjs.org/
download angularjs 1 ,, browse addition module
angular-route.min.js   // for minified version

for CDN 
the below is core anguls js 
https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular.min.js
jist change it to angular-route.min.js at end of CND
https://ajax.googleapis.com/ajax/libs/angularjs/1.5.8/angular-route.min.js





JAVA BRAINS
--------------------------------------------------------------------------------------------------------------------------

ANGULARjs
---------

ng-if="true/false"
<p ng-if="true">welcome</p>
<p ng-if="10>12">welcome</p>      //it will be hidden para coz false


Basic angularjs features
-------------------------
ng-app is a directive that comes out of the box , its a root elemetn of the application

ng-init  // controller will help us to do the requireed task

ng-if  // ig ng-if evalutes to false then that elemet will be removed from the DOM Tree


Introducing scope
---------------------
when anugalr app starts ,it crests an object called SCOPE where all variable are place

ng-bind is same as {{}} 


introduction to controller
---------------------------------

var module = angular.module("myApp",[])
module.controller("myController",Main)  // it register a controller inside myApp angular application, defining function globally is not correct to do ,
												make it a controller and then call function

function Main()
{
	console.log("main called");
}



controller summery
-----------------------
A module is a collection of directive ,  controller and othr stuffs
a controller has to be register with module


Dependecny injection and Scope
--------------------------------

var module = angular.module("myApp",[])
module.controller("myController",Main) 
function Main($scope)   // $scope as argument , so before calling this function it will go fetch the scope and pass it to method execution
{
	$scope.name = "yogendra";   
	console.log("main called");
	
}


Coding Exexrice
------------------
CLOCK APPLICATION
---------------------------------
<html ng-app="myApp">
    <head>
        <script src = "https://ajax.googleapis.com/ajax/libs/angularjs/1.6.0-rc.2/angular.min.js"></script>
    </head>
    
    <body ng-controller="myController">
    
    <h2>CLOCK APPLICATION</h2><br>
       
        The Current Time is {{currentTime}} <br>
        <button ng-click="update()">Update</button>
        
    
        
        <script>
        
        var module = angular.module("myApp",[])
        module.controller("myController", gettingCurrentTime)
        
        function gettingCurrentTime($scope)
            {
               
                var date = new Date();
                $scope.currentTime = date.toTimeString();
                $scope.update = function()
                {
                    var date = new Date();
                    $scope.currentTime = date.toTimeString();
                    
                }
            }
        </script>
    </body>
</html>
---------------------------------


ngClick and data binding
-----------------------------------
ng-click="update()"

any variale u do in html is prefix with a scope tag thatswhy do don't write scope.name to get varibalr in html , but in angular controller u have to mention


Nested controller and scope hierarchy
--------------------------------------

every controller has there own scope object 
 like
 
 app.controller("myCtrl1",main1)
 app.controller("myCtrl2",main2)
 
 function main1($scope)
 {
 	$scope.name = "yogendra1";
 }
 
 function main2($scope)
 {
 	$scope.name = "yogendra2";
 }
 
   in html
   
   <div ng-controller="myCtrl1"
   {{name}}   // prints yogendra1
   </div>
   
    <div ng-controller="myCtrl2"
   {{name}}   //prints yogendra2
   </div>
   
   
   
Nested Controller
-----------------
in html
<div ng-controller="myCtrl1"
{{name}}
	<div ng-controller="myctrl2"
		{{name}}
	</div>
</div>


if we don't have myctrl2 in controller in script app.js, then it has a parent
so output
yogendra1
yogendra1

if angular does'nt found in inner controller then it looks for its parent controller

so this type of nesting contoller is not recommended

SO we use aliasing for this  --  "as" keyword

<div ng-controller="myCtrl1 as c1"
{{c1.name}}     // alias.property
	<div ng-controller="myctrl2 as c2"
		{{c2.name}}
	</div>
</div>


but we need to make changes in contrller as well for this

function main1()
	{
	//var this = $scope;    /// assume that angular add this statement in such cases
	this.name = yogendra1;
	}
	
	
function main2()
	{
	//var this = $scope   
	this.name = yogendra2;
	}
	
	
NOTE ::: USING THIS INSTEAD OF $SCOPE WORKS ONLY WITH THE CONTROLLER-AS SYNTAX , WITHOUT CONTROLLER-AS, YOU WILL NEED
TO INJECT $SCOPE AS BEFORE



ng-show and ng-hide
-------------------

ng-if="true/false"   // it literally remove element from DOM //check using inspect element
ng-show/ng-hide   // it make display as none in css property


looping with ng-repeat
-----------------------

ng-repeat loops creates multiple copies of html elements that all need to exist concurrenty, at same time