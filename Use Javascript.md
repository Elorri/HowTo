# i'm following this class : Javascript Basics

	https://classroom.udacity.com/courses/ud804/lessons/2239648539/concepts/19260885460923
	C:\ProgrammingProjects\JavascriptProjects\frontend-nanodegree-resume

Javascript DOM
	
	JavaScript's power comes from its ability to manipulate the DOM, which is essentially a JavaScript object. 
	When JavaScript makes something interesting happen on a website, it's likely the action happened because JavaScript changed the DOM. 

Javascript jQuery

	jQuery is fast and easy to change the DOM, but it doesn't do anything you can't accomplish with vanilla (regular) JavaScript.
	jquery function documentation : http://api.jquery.com/
	
open browser console

	Chrome: go to chrome main menu > plus d'outils > Outils de développemnt > Console (here’s a guide https://developers.google.com/web/tools/chrome-devtools/console/?utm_source=dcc&utm_medium=redirect&utm_campaign=2016q3)

	FireFox: go to Tools > Web Developer > Web Console (here’s a guide https://developer.mozilla.org/en-US/docs/Tools/Browser_Console)

	IE11: go to Tools > Developer Tools > Console icon (here’s a guide https://msdn.microsoft.com/library/bg182326(v=vs.85).aspx#The_Console_tool__CTRL___2_)

	Safari: turn on the Develop menu: Preferences > Advanced > Show Develop menu in menu bar go to Develop > Show Web Inspector (here’s a guide https://developer.apple.com/library/content/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/GettingStarted/GettingStarted.html)
	
type and run

	console.log("hello world");
	THE function return 'undefined' wich mean nothingg its like a 'void' fuunction in java
	document.URL
	return the string of the url
	
note :

	most interpreteurs nowadays won't make an error if you don't finish with semicolon but it is good practice to keep adding this for now
	
jquery append and prepend

	add content after the last html tag inside of the tag specified by its id (shown by #)
	try : $("#header").append();
	you that you grab the selecror header(because that's what return the function)
	prepend add the string before the first html tag
	
to store variables

	var firstname="james";
	var age=32;
	var myArray = []
	var myFunction = function(){}
	var myObject = {}
	
note in python it would be

	firstname="james";
	age="32";
	
note about both languages

	all numbers are stored as 64bit floats which means integer are stored as float
	
now type in the resumeBuilder.js

	var firstname="james";
	var age=32;
	console.log(firstname);
	
replace function

	var email="cameron@udacity.com";
	var newEmail=email.replace("udacity","gmail");
	console.log(email);
	console.log(newEmail);
	 
now append this to the file resumeBuilder.js

	var formatedName=HTMLheaderName.replace("%data%",firstname);
	$("#header").append(formatedName);
	
note

	index.html declare helper.js function before resumeBuilder.js that's why HTMLheaderName is recognise in resumeBuilder.js because it was declared previouly in helper.js
	
slice method 

	string.slice(begin, [end]) //end is optional

	var copiedText = 'JavaScript is powerful!'.slice(0, 19);
	console.log(copiedText);
	Logs: 'JavaScript is power'
	
	var copiedText = 'audacity'.slice(2);
	console.log(copiedText);
	var udacityText = 'U' + copiedText'; //Concatenation
	console.log(udacityText);
	
	s = 'U' + s.slice(2);
	
true and false in javascript

	some values in javascript can evaluate to true or false 
	but may not equal to true or false they are instead truthy and falsy
	
truthy values are (they all evaluate to true)

	true
	non-zero number
	strings with a lenght of at least one
	objects
	arrays
	functions
	
falsy values are (they all evaluate to false)

	false
	zero
	empty strings
	undefined : variable doesn't exist and the interpreteur doesn't know what you are referring to. See below (var a; a;)
	null : variable exist but has no value
	NaN not a number. is a value that turns up when we ask Javascript to do certain impossible things in arithmetic -- like divide zero by zero.
	
True and False in JavaScript and Python

	see : https://opensourcehacker.com/2012/10/17/true-lies-and-falsy-values-in-python-and-javascript/
	
mentions that undefined means "that a variable doesn't exist and the interpreter doesn't know what you're referring to." This isn't quite true. If you try to use a var that hasn't been defined, you get a ReferenceError. You will see undefined if you declare a variable but don't assign it any values. Like so:

	var a;
	a;
	
will result in undefined. But ... will result in a ReferenceError because b hasn't been declared yet.

	b;

arrays

	works like in phyton
	have a zero index
	https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

array push and pop methods

	The pop() method removes the last element from an array and returns that element. This method changes the length of the array.
	The push() method adds one or more elements to the end of an array and returns the new length of the array.
	
array manipulation

		newArray=_array;
	or
		newArray=[];
		newArray=_array.slice(_array);
		
	followed by
	
		var last=newArray.pop();
		console.log(last);
		last=last+1;
		console.log(last);
		newArray.push(last);
		console.log(newArray);

strings manipulation : turning a string like "cAmEROn PittMAN" into "Cameron PITTMAN"

	function nameChanger(oldName) {
		var finalName = oldName;
		var names = oldName.split(" ");
		names[1] = names[1].toUpperCase();
		names[0] = names[0].slice(0,1).toUpperCase() + names[0].slice(1).toLowerCase();
		finalName = names.join(" ");
		return finalName;
	}
	
note on this example

	split method like in java
	array.join([chars]) lets us put array elements together into a single string. Each element will be separated by the optional chars. In this case, we want a space between the two names, so we made the chars a single space, " "
	
objects in javascript

	are not declared like in Phyton because
	they are no classes in javacript only objects
	there are way to mimic classes but they remain objects
	uses key:value pair notation
	
example

	var skills=["awareness","android"];
	var bio = {
		"firstname":"james",
		"age":32,
		"skills":skills
	};
	
to acces a property just use the dot

	$("#main").append(bio.name);
	
we can also use dot notation to defined its property outside of the object like that. it will add new properties to the object.

	var skills=["awareness","android"];
	var bio = {
		"firstname":"james",
		"age":32,
		"skills":skills
	};
	bio.city="Pau";
	bio.email="toto@toto.com"
	$("#main").append(bio.city);
	
another possible way is

	var skills=["awareness","android"];
	var bio = {
		"firstname":"james",
		"age":32,
		"skills":skills
	};
	bio["city"]="Pau";
	bio["email"]="toto@toto.com"
	$("#main").append(bio[city]);
	
note about adding property like this

	city and email will be the keys
	no need to use 'var' keyword
	
we can achieve the same with the skills inside

	var bio = {
		"firstname":"james",
		"age":32,
		"skills":["awareness","android"]
	};
	
when to use dot and when bracets run this program to see

	// For example, uncomment the line below to see if you can use dot notation to access `property1`.
	// console.log(weirdObject.property1);

	// I'll give you the first answer. The rest are set to false. Try out each property and
	// if you can use dot or bracket notation to access it, change the answer to true!

	// property
	var dotNotation0 = true;
	var bracketNotation0 = true;
	console.log(weirdObject.property);
	console.log(weirdObject["property"]);

	// property1
	var dotNotation1 = true;
	var bracketNotation1 = true;
	console.log(weirdObject.property1);
	console.log(weirdObject["property1"]);

	// property-2
	var dotNotation2 = false;
	var bracketNotation2 = true;
	console.log(weirdObject.property-2);
	console.log(weirdObject["property-2"]);

	// property 3
	var dotNotation3 = false;
	var bracketNotation3 = true;
	//console.log(weirdObject.property 3);
	console.log(weirdObject["property 3"]);

	// property$
	var dotNotation4 = true;
	var bracketNotation4 = true;
	console.log(weirdObject.property$);
	console.log(weirdObject["property$"]);

	// *space*property
	var dotNotation5 = false; //Space is ignore and act like console.log(weirdObject.property);
	var bracketNotation5 = true;
	console.log(weirdObject. property);
	console.log(weirdObject[" property"]);

	// property()
	var dotNotation6 = false;
	var bracketNotation6 = true;
	//console.log(weirdObject.property()); //Uncaught TypeError: weirdObject.property is not a function
	console.log(weirdObject["property()"]);

	// property[]
	var dotNotation7 = false;
	var bracketNotation7 = true;
	//console.log(weirdObject.property[]);
	console.log(weirdObject["property[]"]);

	// 8property
	var dotNotation8 = false;
	var bracketNotation8 = true;
	//console.log(weirdObject.8property);
	console.log(weirdObject["8property"]);
		
JSON

	JavaScript Object Notation. JSON is a popular and simple format for storing and transferring nested or hierarchal data. It's so popular that most other programming languages have libraries capable of parsing and writing JSON (like Python's JSON library).

	If you're generating JSON by hand, you should copy and paste your code into a JSON linter like jsonlint.com to quickly and easily find syntax errors. A linter is a piece of software that analyzes code for syntax errors. Some text editors, like Sublime Text, will automatically lint (or highlight) most syntax errors. But a JSON linter won't miss any syntax errors and you can rest assured that your JSONs will be properly formatted.
		
	For the Online Resume project you'll be using javaScript Object Literals rather than JSON to define your objects. The syntax is very similar, but javaScript Object Literals permit the inclusion of functions as properties and JSON does not. 
	
to make sure your object is well formated use this syntax 

	var education={};
	education["name"]="university";
	education["years"]="2012-2013";

use json instead

	var education={
		school:[
			{
			"name"="university1",
			"years"="2012-2013",
			"skills"=["awareness","android"]
			},
			{
			"name"="university2",
			"years"="2013-2014",
			"skills"=["awareness","android"]
			}
		]
	};

to highlight syntax errors
	
	sublime text
	jsonlint.com
	
Document Object Model
 
	As part of the process of building websites, browsers convert all of the HTML and CSS they receive into a JavaScript object called the Document Object Model (DOM).
	If you want to change html and css you need to use the DOM by calling document
	
Example

	document.getElementById("education").style.display = "none";
	document.getElementById("education").style.backgroundColor = "black";
	.style is a DOM property. It is used to change a CSS style of the selected page element. The property that follows .style is the CSS style that will be modified by this piece of code. 
	Every page element has a display CSS property, which normally controls how that page element interacts with others. If display is set to "none", however, then the element is removed entirely from the page.
	
liste of css properties that can be changed with DOM

	https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference
	
protecting from injection

	make sure the string entered by the user if it contain < and > from their HTML get turned into harmless strings.
	that means  replace all of the < and >

simpliest way 

	var charEscape = function(_html) {
    var newHTML = _html;
    newHTML = _html.replace(/</g, "&lt;");
    newHTML = newHTML.replace(/>/g, "&gt;");
    return newHTML;
	};

Alternatively, 

	you could pass an HTML string into a function like encodeURIComponent(string) to remove instances of < and >. But it isn't intended for situations like this, possibly leading to unexpected consequences.
	

equality

	Strict equality (===) vs Loose equality (==)

	When you use three equal signs, ===, no type conversion is done prior to the comparison. If the values are different types, for example, a String and a Number, they can't ever be equal. To return true, the values must be equal and the types must be the same.

	Loose equality, ==, checks to see if the two values are the same type and if not, converts to a common type before the conversion. If the types are already the same, there is no difference between the result of === and ==. When they aren't it can cause unexpected results.

	Check the link to an article on Mozilla Developer Network to see what values get converted into what.

	According to Jacques Favreau, the lead front-end engineer at Udacity, you should never use ==. It's a frequent source of bugs. In fact, if a Udacity engineer tries to commit code with ==, it automatically gets rejected.

	Though it wasn't mentioned in the video, the same conditions apply for strict inequality (!==) and loose inequality (!=). Loose inequality is more forgiving than loose equality so you might not see strict inequality as often.
 
if

    if (bio.skills.lenght>0) {
		$("#header").append(HTMLskillsStart);
	
        var formatedSkill=HTMLskills.replace("%data%",bio.skills[1]);
		$("#skills").append(formatedSkill);
		
		formatedSkill=HTMLskills.replace("%data%",bio.skills[2]);
		$("#skills").append(formatedSkill);
		
		formatedSkill=HTMLskills.replace("%data%",bio.skills[3]);
		$("#skills").append(formatedSkill);
    }

LOOPS

	for (var i ; i < 9 ; i++){
		console.log(i);
	}

will print 0 1 2 3 4 5 6 7 8

	var array=['a','b'];
	for (i in array){
		console.log(i);
	}

it is good pratice to test if key is part of an array like this

	myObj = {'country1':'Germany', 'country2':'Argentina'};
	for (key in myObj){
		if (myObj.hasOwnProperty(key)) {
			console.log(myObj[key]);
		}
	}
	
will print 0 1. its different from java i here is the index not the value.

	var work={
		jobs:[
			{
			"employer"="university1",
			"title"="2012-2013",
			},
			{
			"employer"="university2",
			"title"="2013-2014",
			}
		]
	};

	for (job in work.jobs){
		$("#workExperience").append(HTMLWorkStart);
		
        var formatedEmployer=HTMLskills.replace("%data%",work.jobs[job].employer);		
		var formatedTitle=HTMLskills.replace("%data%",work.jobs[job].title);
	    var formatedEmployerTitle=formatedEmployer+formatedTitle;
		$(".work-entry:last").append(formatedEmployerTitle);
	}
	
$(".work-entry:last")

	will select every object with the class .work-entry
	:last will appends only to the last entry
	https://www.w3schools.com/jquery/sel_last.asp
	
notes

	for-in loops are considered bad practice because it has some inconsistent behavior with arrays and objects
	http://stackoverflow.com/questions/500504/why-is-using-for-in-with-array-iteration-a-bad-idea
	http://stackoverflow.com/questions/4261051/javascript-why-for-in-is-a-bad-practice
	https://websanova.com/blog/javascript/why-javascript-for-in-loops-are-bad
	use either a standard for loop or the forEach loop instead
	
there is 2 ways to declare a function and they are equivalent (sligtly differences for the interpretor)

		var multiply = function(a, b) {
			return a  b;
		}

		function multiply(a, b) {
			return a * b;
		}
		
lets use this on our resume

		function displaywork() {
			for (job in work.jobs){
				$("#workExperience").append(HTMLWorkStart);
				
				var formatedEmployer=HTMLskills.replace("%data%",work.jobs[job].employer);		
				var formatedTitle=HTMLskills.replace("%data%",work.jobs[job].title);
				var formatedEmployerTitle=formatedEmployer+formatedTitle;
				$(".work-entry:last").append(formatedEmployerTitle);
			}
		}
		displaywork();
		
Collecting clicking locations

	$(document).click(function(loc) {
	  var x=loc.pageX;
	  var y=loc.pageY;
	  logClicks(x,y);
	});
	$(document).click() is a jQuery event handler on the page, which is a fancy way of saying that it will hold some code that runs every time a user clicks on the page. 
	The function (that doesn't have a name, making it an anonymous function) that gets passed into .click() will be run every time a user clicks on the page. 
	loc is a jQuery event object that contains information about the click event. Learn about event's properties with jQuery's documentation. http://api.jquery.com/category/events/event-object/
	the parameter of method click() is an anonymous function
	
logClicks(x,y);
	
	function logClicks(x,y) {
	  clickLocations.push(
		{
		  x: x,
		  y: y
		}
	  );
	  console.log('x location: ' + x + '; y location: ' + y);
	  
retrieve an array of locations

	var work = {
	  "jobs": [
		{
		  "employer": "Udacity",
		  "title": "Course Developer",
		  "location": "Mountain View, CA",
		  "dates": "Feb 2014 - Current",
		  "description": "Who moved my cheese cheesy feet cauliflower cheese. Queso taleggio when the cheese comes out everybody's happy airedale ricotta cheese and wine paneer camembert de normandie. Swiss mozzarella cheese slices feta fromage frais airedale swiss cheesecake. Hard cheese blue castello halloumi parmesan say cheese stinking bishop jarlsberg."
		},
		{
		  "employer": "LearnBIG",
		  "title": "Software Engineer",
		  "location": "Seattle, WA",
		  "dates": "May 2013 - Jan 2014",
		  "description": "Who moved my cheese cheesy feet cauliflower cheese. Queso taleggio when the cheese comes out everybody's happy airedale ricotta cheese and wine paneer camembert de normandie. Swiss mozzarella cheese slices feta fromage frais airedale swiss cheesecake. Hard cheese blue castello halloumi parmesan say cheese stinking bishop jarlsberg."
		},
		{
		  "employer": "LEAD Academy Charter High School",
		  "title": "Science Teacher",
		  "location": "Nashville, TN",
		  "dates": "Jul 2012 - May 2013",
		  "description": "Who moved my cheese cheesy feet cauliflower cheese. Queso taleggio when the cheese comes out everybody's happy airedale ricotta cheese and wine paneer camembert de normandie. Swiss mozzarella cheese slices feta fromage frais airedale swiss cheesecake. Hard cheese blue castello halloumi parmesan say cheese stinking bishop jarlsberg."
		},
		{
		  "employer": "Stratford High School",
		  "title": "Science Teacher",
		  "location": "Nashville, TN",
		  "dates": "Jun 2009 - Jun 2012",
		  "description": "Who moved my cheese cheesy feet cauliflower cheese. Queso taleggio when the cheese comes out everybody's happy airedale ricotta cheese and wine paneer camembert de normandie. Swiss mozzarella cheese slices feta fromage frais airedale swiss cheesecake. Hard cheese blue castello halloumi parmesan say cheese stinking bishop jarlsberg."
		}
	  ]
	};

	// Your code goes here! Let me help you get started

	function locationizer(work_obj) {
		var locationArray=[];
		
		for (job in work_obj.jobs){
			var newLocation=work_obj.jobs[job].location;
			locationArray.push(newLocation);
		}
		return locationArray;
	}

	// Did locationizer() work? This line will tell you!
	console.log(locationizer(work));
	
functions are objects

	what ?
	yes object i repeat "functions are objects"
	and i would even say "everything in javascript is an object"
	more on this here : http://helephant.com/2008/08/19/functions-are-first-class-objects-in-javascript/
	
this means that functions can encapsulate functions

	var skills=["awareness","android"];
	var bio = {
		"firstname":"james",
		"age":32,
		"skills":skills
	};
	bio.display=function(){
		//This function will be executed without having to make a specific call;
	}
	
make your resume interactive with googleMap

	$("#mapDiv").append(googleMap);
	cf helper.js for googleMap value
	
	Uncomment the last block of code in helper.js. The code you need starts with window.addEventListener('load', initializeMap); and goes until the end of the file.
	Uncomment the <script> tag for Google Maps API in the <head> of index.html.
	Google is increasingly requiring an API key to make Google Map requests. You can obtain your own Google Maps API key here.
	Once obtained, you can add the key to the Google Maps API script request in index.html: 
	<script src="http://maps.googleapis.com/maps/api/js?libraries=places&key=YOUR_API_KEY_HERE"></script> 
	
make your resume interactive with graphics

	https://d3js.org/
	https://developers.google.com/maps/documentation/javascript/tutorial
	
scope

	variables declared within a function are only available inside that function.
	Blocks, like if-statements and any of the loops you've learned about, do not create their own scope. All of the variables declared in an if statement are accessible outside it.
	
function declaration differences. As you've learned in this course, there are two syntaxes to declare functions

	var functionName = function() {}
	function functionName() {}

The JavaScript interpreter, which is responsible for taking the code you write and preparing it to become machine code, will handle the two function declarations slightly differently because of the way it handles variable declarations. All variable declarations will immediately get moved to the top of their scope. For example:

	var x = 5;
	console.log(x); // 5
	var y = 10;
	
is the same as

	var x, y; // this line simply declares x and y at the same time.
	x = 5;
	console.log(x); // 5
	y = 10;
	
Notice how the declaration of y moved to the top of the scope. And also notice how the first line doesn't set a value for neither x nor y. After var x, y; both x and y are undefined.

The same behavior holds true for other types of variables, including functions. 

	If you use the var functionName syntax, only the function's declaration (e.g. var functionName;) gets moved at the top of its scope. However, if you use function functionName() syntax, the function declaration and definition (the actual instructions inside the function) get moved to the top of the function's scope.
	
scope exercice 1 will print "First string"

	var outsideExample = "First string";
	function example() {
		var outsideExample = "Second string";
	}
	example();
	console.log(outsideExample);

scope exercice 2 will print "Second string"

	var outsideExample = "First string";
	function example() {
		outsideExample = "Second string";
	}
	example();
	console.log(outsideExample);

scope exercice 3 will print first "Second string" and then "Second string". yes both the same;

	var outsideExample = "First string";
	if (true) {
		var outsideExample = "Second string";
		console.log(outsideExample);
	}
	console.log(outsideExample);
	
scope exercice 	4 will print "Ran the example!"

	example1();
	function example1() {
		console.log("Ran the example");
	}
	
will be interpreded like that

	var example1;
	example1 = function() {
		console.log("Ran the example");
	}
	example1();
	
scope exercice 5 will not print "Ran the example!"; You should see an undefined error when this code gets run.

	example2();
	var example2 = function() {
		console.log("Ran the example");
	}
	
will be interpreded like that

	var example2;
	example2();
	example2 = function() {
		console.log("Ran the example");
	}
	
map making

	google.maps.event.addListener(marker, 'click', function() {
		// your code goes here
	});
	
if i want to update my resume properly here is the struture demanded; bio contains:

      name : string
      role : string
      contacts : an object with
            mobile: string
            email: string 
            github: string
            twitter: string 
            location: string
      welcomeMessage: string 
      skills: array of strings
      biopic: url
      display: function taking no parameters
	  
education contains:

      schools: array of objects with
           name: string
           location: string
           degree: string
           majors: array of strings
           dates: integer (graduation date)
           url: string
      onlineCourses: array with
           title: string
           school: string
           date: integer (date finished)
           url: string
      display: function taking no parameters
	  
work contains

      jobs: array of objects with
           employer: string 
           title: string 
           location: string 
           dates: string (works with a hyphen between them)
           description: string 
      display: function taking no parameters
	  
projects contains:

      projects: array of objects with
            title: string 
            dates: string (works with a hyphen between them)
            description: string
            images: array with string urls
      display: function taking no parameters
	  
# ES6

major update to javascript syntax are

	Harmony
	ES6
	ES2015
	
All 3 are refered to as

	ES6
	
Let and const

	Up until now, the only way to declare a variable in JavaScript was to use the keyword var.
	var was sometime giving unexpected results because it was scope to a function
	let and const are scoped to the block
	
	
Example with var

	function getClothing(isCold) {
	  if (isCold) {
		var freezing = 'Grab a jacket!';
	  } else {
		var hot = 'It’s a shorts kind of day.';
		console.log(freezing);
	  }
	}

This  

	will throw a undefined error
	will not throw a ReferrenceError
	this is weird but this can be explained by hoisting

Hoisting

	is a result of how JavaScript is interpreted by your browser
	means all variables are raised to the top of the function scope.
	
At runtime getClothing look like this
	
	function getClothing(isCold) {
	
	  var freezing, hot;
	  
	  if (isCold) {
		freezing = 'Grab a jacket!';
	  } else {
		hot = 'It’s a shorts kind of day.';
		console.log(freezing);
	  }
	}
		
Example with let and const

	function getClothing(isCold) {
	  if (isCold) {
		let freezing = 'Grab a jacket!';
	  } else {
		let hot = 'It’s a shorts kind of day.';
		console.log(freezing);
	  }
	}

This  

	will throw a ReferrenceError
	will not throw a undefined error	
	
let and const

	are scoped to the block
	can’t be redeclared in the same scope
	let can be reassigned
	const can’t be reassigned and must be assigned an initial value

in practice

	always start to use const and if you find you need to reasign it use const.
	throw var away never use it again, it's considered bad practice
	
Prior to ES6, the old way to concatenate strings together was by using the string concatenation operator ( + ).

	const student = {
	  name: 'Richard Kalehoff',
	  guardian: 'Mr. Kalehoff'
	};

	const teacher = {
	  name: 'Mrs. Wilson',
	  room: 'N231'
	}

	let message = student.name + ' please see ' + teacher.name + ' in ' + teacher.room + ' to pick up your report card.';
	
	Returns: Richard Kalehoff please see Mrs. Wilson in N231 to pick up your report card.
	
This works alright, but it gets more complicated when you need to build multi-line strings.

	let note = teacher.name + ',\n\n' +
	  'Please excuse ' + student.name + '.\n' +
	  'He is recovering from the flu.\n\n' +
	  'Thank you,\n' +
	  student.guardian;
	Returns:
	Mrs. Wilson,

	Please excuse Richard Kalehoff.
	He is recovering from the flu.

	Thank you,
	Mr. Kalehoff
	
NOTE: 
	
	As an alternative to using the string concatenation operator ( + ), you can use the String's concat() method, but both options are rather clunky for simulating true string interpolation.
	https://en.wikipedia.org/wiki/String_interpolation
	
Template literals

	changed the usual way of doing concatenation
	was previously referred to as "template strings" in development releases of ES6
	are string literals that include embedded expressions.
	are denoted with backticks ( `` ) instead of single quotes ( '' ) or double quotes ( "" )
	can contain placeholders which are represented using ${expression} 
	drop concatenation operator
	drop newline characters ( \n ). That's because template literals also preserve newlines as part of the string!
	
This makes it much easier to build strings

	let message = `${student.name} please see ${teacher.name} in ${teacher.room} to pick up your report card.`;
	
	
And much more readable. This 

	let note = teacher.name + ',\n\n' +
	  'Please excuse ' + student.name + '.\n' +
	  'He is recovering from the flu.\n\n' +
	  'Thank you,\n' +
	  student.guardian;

will become this

	let note = `${teacher.name},
	
	  Please excuse ${student.name}.
	  He is recovering from the flu.
	  
	  Thank you,
	  ${student.guardian}`;

and this

function createAnimalTradingCardHTML(animal) {
    const cardHTML = '<div class="card">' +
        '<h3 class="name">' + animal.name + '</h3>' +
        '<img src="' + animal.name + '.jpg" alt="' + animal.name +'" class="picture">' +
        '<div class="description">' +
            '<p class="fact">' + animal.fact + '</p>' +
            '<ul class="details">' +
                '<li><span class="bold">Scientific Name</span>: ' + animal.scientificName + '</li>' +
                '<li><span class="bold">Average Lifespan</span>: ' + animal.lifespan + '</li>' +
                '<li><span class="bold">Average Speed</span>: ' + animal.speed + '</li>' +
                '<li><span class="bold">Diet</span>: ' + animal.diet + '</li>' +
            '</ul>' +
            '<p class="brief">' + animal.summary + '</p>' +
        '</div>' +
    '</div>';

    return cardHTML;
}


will become this

	function createAnimalTradingCardHTML(animal) {
		const cardHTML = `<div class="card">
			<h3 class="name">${animal.name}</h3>
			<img src="' + animal.name + '.jpg" alt="${animal.name}" class="picture">
			<div class="description">
				<p class="fact">${animal.fact}</p>
				<ul class="details">
					<li><span class="bold">Scientific Name</span>: ${animal.scientificName}</li>
					<li><span class="bold">Average Lifespan</span>: ${animal.lifespan}</li>
					<li><span class="bold">Average Speed</span>: ${animal.speed}</li>
					<li><span class="bold">Diet</span>: ${animal.diet}</li>
				</ul>
				<p class="brief">${animal.summary}</p>
			</div>
		</div>`;

		return cardHTML;
	}


destructuring

	is a new way to extract data from array or object
	
	
old way array(this is not destructuring)

	const point = [10, 25, -34];

	const x = point[0];
	const y = point[1];
	const z = point[2];	

old way object(this is not destructuring)

	const gemstone = {
	  type: 'quartz',
	  color: 'rose',
	  karat: 21.29
	};

	const type = gemstone.type;
	const color = gemstone.color;
	const karat = gemstone.karat;
	
destructuring an array

	const point = [10, 25, -34];
	const [x, y, z] = point;
	

You can also ignore values when destructuring arrays. 
	
	For example, const [x, , z] = point; ignores the y coordinate and discards it.
	const things = ['red', 'basketball', 'paperclip', 'green', 'computer', 'earth', 'udacity', 'blue', 'dogs'];
	const [one,,,two,,,, three] = things;
	returns 1. red - 2. green - 3. blue

destructuring an object

	const gemstone = {
	  type: 'quartz',
	  color: 'rose',
	  karat: 21.29
	};

	const {type, color, karat} = gemstone;

Object literal shorthand

	used during object initialisation
	used when property names are variable names are the same
	use only one naming instead of repeating it
	can remove the function keyword by just adding ()
	
Example

	let type = 'quartz';
	let color = 'rose';
	let carat = 21.29;

	const gemstone = {
	  type: type,
	  color: color,
	  carat: carat
	  calculateWorth: function() {
		// will calculate worth of gemstone based on type, color, and carat
	  }
	};

become

	let type = 'quartz';
	let color = 'rose';
	let carat = 21.29;

	const gemstone = {type,color,carat, calculateWorth(){// will calculate worth of gemstone based on type, color, and carat}};
		
iterable protocol

	allow any object to become iterable
	by implementing the iterable protocol
	
iterable object by default

	 String
	 Array
	 Map
	 Set
	
iterator
	
	const digits=[1, 2, 3, 4, 5]

	for (let i = 0 ; i < digits.lenght ; i++){
		console.log(digits[i]);
	}
	
can be replaced by  for...in loops but this is discouraged

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

	for (const index in digits) {
	  console.log(digits[index]);
	}
	note : this is an index here, not the actual value
	
for...in loops are discouraged because see what's prints this example

	Array.prototype.decimalfy = function() {
	  for (let i = 0; i < this.length; i++) {
		this[i] = this[i].toFixed(2);
	  }
	};

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

	for (const index in digits) {
	  console.log(digits[index]);
	}
	
	Prints:

		0
		1
		2
		3
		4
		5
		6
		7
		8
		9
		function() {
		 for (let i = 0; i < this.length; i++) {
		  this[i] = this[i].toFixed(2);
		 }
		}

	Weird : its prints the function code
	
forEach loop not really better because

	forEach() is actually an array method, so it can only be used exclusively with arrays. 
	There is also no way to stop or break a forEach loop. If you need that type of behavior in your loop, you’ll have to use a basic for loop.
	
For...of loop what we want

	can be used to loop over any type of data that is iterable.
	You can stop or break a for...of loop at anytime.
	only loop over the values in the object.
	use the value not the index (like in java)
	
For...of loop example	

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

	for (const digit of digits) {
	  console.log(digit);
	}
	
You can stop or break a for...of loop at anytime.

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

	for (const digit of digits) {
	  if (digit % 2 === 0) {
		continue;
	  }
	  console.log(digit);
	}
	
only loop over the values in the object.

	Array.prototype.decimalfy = function() {
	  for (i = 0; i < this.length; i++) {
		this[i] = this[i].toFixed(2);
	  }
	};

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

	for (const digit of digits) {
	  console.log(digit);
	}
	Prints:
	0
	1
	2
	3
	4
	5
	6
	7
	8
	9

Spread operator

	gives the ability to expand, or spread, iterable objects into multiple elements.
	very useful for combining arrays
	
Examples

	const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
	console.log(...books);
	const primes = new Set([2, 3, 5, 7, 11, 13, 17, 19, 23, 29]);
	console.log(...primes);
	
will prints

	Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities
	2 3 5 7 11 13 17 19 23 29 

combining array the old way

	const fruits = ["apples", "bananas", "pears"];
	const vegetables = ["corn", "potatoes", "carrots"];
	const produce = fruits.concat(vegetables);
	console.log(produce);
	Prints: ["apples", "bananas", "pears", "corn", "potatoes", "carrots"]
	
we would like something like this to work 

	const produce = [fruits, vegetables]; //looks better
	console.log(produce);
	Prints: [Array[3], Array[3]]  //definitively not what we want
	
but it works with the spread operator

	const fruits = ["apples", "bananas", "pears"];
	const vegetables = ["corn", "potatoes", "carrots"];
	const produce = [...fruits ,...vegetables];
	console.log(produce);
	
Rest parameter

	is the contrary of spread
	allow to bundle multiple elements back into an array
	allows you to represent an indefinite number of elements as an array
	makes it easity to loop over elements
	works well with variadic functions (functions that )
	
Example

	const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
	const [total, subtotal, tax, ...items] = order;
	console.log(total, subtotal, tax, items);
	Prints: 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]
	
Note about this example

	the values of the order array are assigns to individual variables using destructuring
	total, subtotal, and tax are assigned the first three values
	items is assigned the rest of the values in the array (as an array).

example of loop

	printPackageContents('cheese', 'eggs', 'milk', 'bread');
	function printPackageContents(...items){
		for(const item of items){
			console.log(item)
		}
	}

variadic functions

	take an indefinite number of arguments
	uses the argument object : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments
	arguments object is an array-like object that is available as a local variable inside all functions. It contains a value for each argument being passed to the function starting at 0 for the first argument, 1 for the second argument, and so on.
	has down side : it is misleading because although method can have an infinite number of arguments it looks like their is no arguments
	can use rest parameter to avoid this down side
	
Example of variadic function

	function sum() {
	  let total = 0;  
	  for(const argument of arguments) {
		total += argument;
	  }
	  return total;
	}

	sum(1, 2);
	sum(10, 36, 7, 84, 90, 110);
	sum(-23, 3000, 575000);
	
works well with variadic functions : same variadic function with rest parameter

	function sum(...nums) {
	  let total = 0;  
	  for(const num of nums) {
		total += num;
	  }
	  return total;
	}

	sum(1, 2);
	sum(10, 36, 7, 84, 90, 110);
	sum(-23, 3000, 575000);
	
functions have changed a lot in ES6  here are the major changed

	arrow functions
	class keyord for creating functions
	default function parameter
	functions can connect to other functions using 'super' and 'extends' keyword
	
Arrow functions 

	are easier to read and less verbose
	
to convert a regular function into an arrow function

	remove the function keyword
	remove the parentheses
	remove the opening and closing curly braces
	remove the return keyword
	remove the semicolon
	add an arrow ( => ) between the parameter list and the function body

will change this

	const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) { 
	  return name.toUpperCase();
	});

to this

	const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
	  name => name.toUpperCase()
	);

regular functions 

	can be function declarations
	can be function expressions
	
arrow functions

	are an expression and can only be used where an expression is valid that means
	can be stored in a variable,
	can be passed as an argument to a function,
	can be stored in an object's property.
	
arrow functions can be stored in a variable

	const greet = name => `Hello ${name}!`;
	greet('Asser');
	Returns: Hello Asser!
	
arrow function parameter

	is what is before =>
	can ommit () if only one parameter
	need () if more than one or 0 parameter
	
example

	// empty parameter list requires parentheses
	const sayHi = () => console.log('Hello Udacity Student!');
	sayHi();
	Prints: Hello Udacity Student!
	
	// multiple parameters requires parentheses
	const orderIceCream = (flavor, cone) => console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
	orderIceCream('chocolate', 'waffle');
	Prints: Here's your chocolate ice cream in a waffle cone.
	
Note all those functions are correct
	
	setTimeout(() => {
		console.log('starting the test');
		test.start();
	}, 2000);
	
	setTimeout( _ => {
		console.log('starting the test');
		test.start();
	}, 2000);
	
	const vowels = 'aeiou'.split('');
	const bigVowels = vowels.map( (letter) => letter.toUpperCase() );
	
	const vowels = 'aeiou'.split('');
	const bigVowels = vowels.map( letter => letter.toUpperCase() );

Note about why

	using {} after => is correct but not a necessity
	unsing _ instead of () is correct. _ become a parameter that won't be used and will stay undefined. it's common practice so better know it
	it's correct to have () if you have one parameter but its better to omit ()
	letter => letter.toUpperCase() is correct and in good practice
	
arrow function concise body syntax

	is used when the function has a single expression as body
	has no curly braces surrounding the function body
	and automatically returns the expression. 
	
example

	const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
	  name => name.toUpperCase()
	);
	
arrow function block body syntax

	is used when the function has a several expression as body
	it uses curly braces to wrap the function body
	and a return statement needs to be used to actually return something from the function.

Example

	const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
	  name = name.toUpperCase();
	  return `${name} has ${name.length} characters in their name`;
	});
	
this keyword

	can have many different value
	is a new object if the function that call it is a regular function and this regular function is called with new keyword
	is a specified object if the function that call it is a regular function and this regular function is invoked with call/apply
	is a context object if the function that call it is a regular function and this regular function is a method of an object
	is a global object (with default undefined value if no initial value set up) if the function that call it is a regular function and this regular function is called with no context
	is an inherated context object (last value of this) if the function that call it is an arrow function and this arrow function is called with no context
	more here : https://github.com/getify/You-Dont-Know-JS/blob/master/this%20%26%20object%20prototypes/ch2.md

	has a different value depending on how the function is called. if it is a regular function
	has a different value depending on where the function is called. if it is an arrow function
	
is a new object if the function that call it is a regular function and this regular function is called with new keyword

	const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);
	In the code above, the value of this inside the Sundae constructor function is a new object because it was called with new.
	
is a specifyied object if the function that call it is a regular function and this regular function is invoked with call/apply

	const result = obj1.printName.call(obj2);
	first parameter of call() method is setup to explicitly set what this refers to
	therefore this inside printName() will refer to obj2
	
is a context object if the function that call it is a regular function and this regular function is a method of an object

	data.teleport();
	this inside teleport() refers to data
	
is a global object or undefined if the function that call it is a regular function and this regular function is called with no context

	teleport();
	this inside teleport() is either the global object or, if in strict mode, it's undefined.
	
try to understand this code and its results

	// constructor
	function IceCream() {
	  this.scoops = 0;
	}

	// adds scoop to ice cream
	IceCream.prototype.addScoop = function() {
	  //here this is a context object (dessert) but we don't call it in this example
	  setTimeout(function() {
		this.scoops++; //here this is a global object
		console.log('scoop added!');
	  }, 500);
	};

	const dessert = new IceCream();
	dessert.addScoop();
	console.log(dessert.scoops);
	console.log(scoops);
	
result in 

	Prints: scoop added!
	Prints: 0
	Prints: NaN
	
why

	because setTimeout() is called without new, without call(), without apply(), and without a context object
	That means the value of this inside the function is the global object and NOT the dessert object
	a new scoops variable is created (with a default value of undefined) and was then incremented (undefined + 1 results in NaN)
	
To get the correct result with regular function here is the code

	// constructor
	function IceCream() {
	  this.scoops = 0;
	}

	// adds scoop to ice cream
	IceCream.prototype.addScoop = function() {
	  const cone = this; // sets `this` to the `cone` variable
	  setTimeout(function() {
		cone.scoops++; // references the `cone` variable
		console.log('scoop added!');
	  }, 500);
	};

	const dessert = new IceCream();
	dessert.addScoop();
	console.log(dessert.scoops);
	console.log(scoops);
	
result in 

	Prints: scoop added!
	Prints: 1
	Prints: 1??? 
	
is an inherated context object (last value of this) if the function that call it is an arrow function and this arrow function is called with no context

	// constructor
	function IceCream() {
	  this.scoops = 0;
	}

	// adds scoop to ice cream
	IceCream.prototype.addScoop = function() {
	  setTimeout(() => { // an arrow function is passed to setTimeout. this will refers to desert
		this.scoops++;
		console.log('scoop added!');
	  }, 500);
	};

	const dessert = new IceCream();
	dessert.addScoop();
	console.log(dessert.scoops);
	console.log(scoops);	
	
result in 

	Prints: scoop added!
	Prints: 1
	Prints: 1??? 
	
Now what happens if we use 2 arrow functions like this ?

	// constructor
	function IceCream() {
		this.scoops = 0;
	}

	// adds scoop to ice cream
	IceCream.prototype.addScoop = () => { // addScoop is now an arrow function
	  setTimeout(() => {
		this.scoops++;
		console.log('scoop added!');
	  }, 0.5);
	};

	const dessert = new IceCream();
	dessert.addScoop();
	console.log(dessert.scoops);
	console.log(scoops);		

result in 

	Prints: scoop added!
	Prints: 0
	Prints: NaN

Why 

	because last value of this before entering addScoop method was a global object undefined.
	and as said before this inherit the last value of this before entering the arrow method.
	
default function parameters

	makes it easy to setup default values to parameters if thoses parameters are not defined
	eliminated the test on 'undefined' exemple (typeof greeting !== 'undefined')
	
example this

	function greet(name, greeting) {
	  name = (typeof name !== 'undefined') ?  name : 'Student';
	  greeting = (typeof greeting !== 'undefined') ?  greeting : 'Welcome';

	  return `${greeting} ${name}!`;
	}

	greet(); // Welcome Student!
	greet('James'); // Welcome James!
	greet('Richard', 'Howdy'); // Howdy Richard!

will be replaced by this

	function greet(name = 'Student', greeting = 'Welcome') {
	  return `${greeting} ${name}!`;
	}

	greet(); // Welcome Student!
	greet('James'); // Welcome James!
	greet('Richard', 'Howdy'); // Howdy Richard!
	
default function parameters and arrays can create really powerful functions
 
	function createGrid([width = 5, height = 5]) {
	  return `Generates a ${width} x ${height} grid`;
	}

	createGrid(); // throws an error Uncaught TypeError: Cannot read property 'Symbol(Symbol.iterator)' of undefined
	createGrid([]); // Generates a 5 x 5 grid
	createGrid([2]); // Generates a 2 x 5 grid
	createGrid([2, 3]); // Generates a 2 x 3 grid
	
to avoid Uncaught TypeError we can init the array to an emty array

	function createGrid([width = 5, height = 5] = []) {
	  return `Generating a grid of ${width} by ${height}`;
	}
	createGrid(); // Generates a 5 x 5 grid
	createGrid([]); // Generates a 5 x 5 grid
	createGrid([2]); // Generates a 2 x 5 grid
	createGrid([2, 3]); // Generates a 2 x 3 grid
	createGrid([undefined, 3]); // Generates a 5 x 3 grid
	
default function parameters and object initialisation

	function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
	  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
	  return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
	}

	createSundae(); // throws an error. Uncaught TypeError: Cannot match against 'undefined' or 'null'.
	createSundae({}); // Your sundae has 1 scoop with Hot Fudge toppings.
	createSundae({scoops: 2}); // Your sundae has 2 scoops with Hot Fudge toppings.
	createSundae({scoops: 2, toppings: ['Sprinkles']}); // Your sundae has 2 scoops with Sprinkles toppings.
	createSundae({toppings: ['Cookie Dough']}); // Your sundae has 1 scoop with Cookie Dough toppings.
	createSundae({scoops: 2, 'Sprinkles'}); // throw an error because method .join(' and ') cannot be applyied to a string 
	
We can prevent 'Uncaught TypeError' by providing a default object to the function:

	function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
	  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
	  return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
	}

default function parameters : what to use ? array or object ?

	function createSundae([scoops = 1, toppings = ['Hot Fudge']] = []) { … }
	createSundae([undefined, ['Hot Fudge', 'Sprinkles', 'Caramel']]);
	
	function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) { … }
	createSundae({toppings: ['Hot Fudge', 'Sprinkles', 'Caramel']});
	
	Since arrays are positionally based, we have to pass undefined to "skip" over the first argument (and accept the default) to get to the second argument.
	recommandation : use object over array.
	
classes in javascript

	can be used to create objects (like functions does that. let cookie=new Dessert())
	can be used to provide inheritance (like this is done using prototypal inheritance. IceCream.prototype.addScoop = function() {})
	should be used only for better understanding. It will anyway be converted into functions
	
classes in other languages

	are used to create object
	are used to provide inheritance
	
ES5 class example (in ES5 there was no other way than creating functions)

	function Plane(numEngines) {
	  this.numEngines = numEngines;
	  this.enginesActive = false;
	}

	// methods "inherited" by all instances
	Plane.prototype.startEngines = function () {
	  console.log('starting engines...');
	  this.enginesActive = true;
	};

	const richardsPlane = new Plane(1);
	richardsPlane.startEngines();

	const jamesPlane = new Plane(4);
	jamesPlane.startEngines();
	
	typeof Plane; // returns : function
	
note about this

	the Plane function is a constructor function
	methods that are "inherited" by each Plane object are placed on the Plane.prototype object
	the constructor function is called with the new keyword
	
same thing in ES6

	class Plane {
	  constructor(numEngines) {
		this.numEngines = numEngines;
		this.enginesActive = false;
	  }

	  startEngines() {
		console.log('starting engines…');
		this.enginesActive = true;
	  }
	}
	
	const richardsPlane = new Plane(1);
	richardsPlane.startEngines();

	const jamesPlane = new Plane(4);
	jamesPlane.startEngines();
	
	typeof Plane; // returns : function
	
note about this

	the constructor method will automatially run when a new object is constructed from this class
	we create the object the same way as before
	eventhough we have a class now the typeof still return a function. Our class is converted into a function
	
you can add static methods to a class

	class Plane {
	  constructor(numEngines) {
		this.numEngines = numEngines;
		this.enginesActive = false;
	  }

	  static badWeather(planes) {
		for (plane of planes) {
		  plane.enginesActive = false;
		}
	  }

	  startEngines() {
		console.log('starting engines…');
		this.enginesActive = true;
	  }
	}
	
	Plane.badWeather([plane1, plane2, plane3]);
	
extends and super example

	class Tree {
	  constructor(size = '10', leaves = {spring: 'green', summer: 'green', fall: 'orange', winter: null}) {
		this.size = size;
		this.leaves = leaves;
		this.leafColor = null;
	  }

	  changeSeason(season) {
		this.leafColor = this.leaves[season];
		if (season === 'spring') {
		  this.size += 1;
		}
	  }
	}

	class Maple extends Tree {
	  constructor(syrupQty = 15, size, barkColor, leaves) {
		super(size, barkColor, leaves);
		this.syrupQty = syrupQty;
	  }

	  changeSeason(season) {
		super.changeSeason(season);
		if (season === 'spring') {
		  this.syrupQty += 1;
		}
	  }

	  gatherSyrup() {
		this.syrupQty -= 3;
	  }
	}

	const myMaple = new Maple(15, 5);
	myMaple.changeSeason('fall');
	myMaple.gatherSyrup();
	myMaple.changeSeason('spring');
	
note about this

	super(), super. , extends works like in java
	
ES5 : same example without super extends
	
	function Tree() {
	  this.size = size || 10;
	  this.leaves = leaves || {spring: 'green', summer: 'green', fall: 'orange', winter: null};
	  this.leafColor;
	}

	Tree.prototype.changeSeason = function(season) {
	  this.leafColor = this.leaves[season];
	  if (season === 'spring') {
		this.size += 1;
	  }
	}

	function Maple (syrupQty, size, barkColor, leaves) { //We create another contuctor
	  Tree.call(this, size, barkColor, leaves);
	  this.syrupQty = syrupQty || 15;
	}

	Maple.prototype = Object.create(Tree.prototype); 
	Maple.prototype.constructor = Maple; 

	Maple.prototype.changeSeason = function(season) {
	  Tree.prototype.changeSeason.call(this, season);
	  if (season === 'spring') {
		this.syrupQty += 1;
	  }
	}

	Maple.prototype.gatherSyrup = function() {
	  this.syrupQty -= 3;
	}

	const myMaple = new Maple(15, 5);
	myMaple.changeSeason('fall');
	myMaple.gatherSyrup();
	myMaple.changeSeason('spring');
	
note about this

	the init seems to be made using ||
	function Maple (syrupQty, size, barkColor, leaves) { //We create another contuctor
	Maple.prototype = Object.create(Tree.prototype); //We set the function prototype to the base function prototype. override is here
	Maple.prototype.constructor = Maple; //Because we just overide original proto. We need to remake the connection between constructor property and original constructor function
	Tree.call(this, size, barkColor, leaves); is the equivalent of super(size, barkColor, leaves);
	Tree.prototype.changeSeason.call(this, season); is the equivalent of super.changeSeason(season);


javascript class example

	class Dessert {
	  constructor(calories = 250) {
		this.calories = calories;
	  }
	}

	class IceCream extends Dessert {
	  constructor(flavor, calories, toppings = []) {
		super(calories);
		this.flavor = flavor;
		this.toppings = toppings;
	  }
	  addTopping(topping) {
		this.toppings.push(topping);
	  }
	}
	
primary data types in javascript are

	numbers
	strings
	boolean
	null
	undefined
	
symbols

	is a unique identifier
	is an immutable data type 
	are used to get an unique property inside an object
	is created by writing Symbol() with an optional string as its description.
	The description "apple" is just a way to describe the symbol, but it can’t be used to access the symbol itself.
	
example

	const sym1 = Symbol('apple');
	console.log(sym1);
	const sym2 = Symbol('banana');
	const sym3 = Symbol('banana');
	console.log(sym2 === sym3);
	returns : Symbol(apple)
	returns : false
	
example bowl

	const bowl = {
	  'apple': { color: 'red', weight: 136.078 },
	  'banana': { color: 'yellow', weight: 183.15 },
	  'orange': { color: 'orange', weight: 170.097 }
	};
	console.log(bowl);
	returns : Object {apple: Object, banana: Object, orange: Object}

if we add a banana to the bowl

	const bowl = {
	  'apple': { color: 'red', weight: 136.078 },
	  'banana': { color: 'yellow', weight: 183.15 },
	  'orange': { color: 'orange', weight: 170.097 },
	  'banana': { color: 'yellow', weight: 176.845 }
	};
	console.log(bowl);
	returns : Object {apple: Object, banana: Object, orange: Object}
	
Instead of adding another banana to the bowl, our previous banana is overwritten by the new banana. To fix this we will use symbols

	const bowl = {
	  [Symbol('apple')]: { color: 'red', weight: 136.078 },
	  [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
	  [Symbol('orange')]: { color: 'orange', weight: 170.097 },
	  [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
	};
	console.log(bowl);
	returns : Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}
	
The Iterable Protocol

	is built in with some objects like strings and arrays
	can be added to any object.
	the iterable object has to implement the iterable interface and fill the default iterator method
	
The iterator method

	must define how the object should be iterated.
	is available via the constant [Symbol.iterator]
	is a zero arguments function that returns an iterator object
	
The Iterator Protocol

	define a standard way that an object produces a sequence of values
	the iterator object has to implement the next() method
	
The .next() method 

	is a zero arguments function that returns an object with two properties:
		value : the data representing the next value in the sequence of values within the object
		done : a boolean representing if the iterator is done going through the sequence of values
			If done is true, then the iterator has reached the end of its sequence of values.
			If done is false, then the iterator is able to produce another value in its sequence of values.
			
Example of Iterable Protocol and Iterator Protocol used together

	const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]; //array is iterable
	const arrayIterator = digits[Symbol.iterator](); //we access the iterator methode

	console.log(arrayIterator.next()); //next() has been implemented in the built-in array methods
	console.log(arrayIterator.next());
	console.log(arrayIterator.next());
	
this returns

	Object {value: 0, done: false}
	Object {value: 1, done: false}
	Object {value: 2, done: false}
	
Sets
		
	Sets are not indexed-based - you do not refer to items in a set based on their position in the set
	items in a Set can’t be accessed individually
	can have duplicates
	
There are several way to create a set, first one is 

	const games = new Set();
	console.log(games);
	Returns : Set {}

This creates an empty Set games with no items. If you want to create a Set from a list of values, you use an array:

	const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
	console.log(games);
	returns : Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}

To add and delete from a set use add and delete methods

	const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
	games.add('Banjo-Tooie');
	games.add('Age of Empires');
	games.delete('Super Mario Bros.');
	console.log(games);
	Returns : Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}
	if you attempt to .add() a duplicate item to a Set, you won’t receive an error, but the item will not be added to the Set.
	if you try to .delete() an item that is not in a Set, you won’t receive an error, and the Set will remain unchanged.
	.add() returns the Set if an item is successfully added. 
	.delete() returns a Boolean (true or false) depending on successful deletion.
	
To delete all items

	games.clear()
	console.log(games);
	Returns : Set {}
	
Returns the number of items : .size property (note : this defers from the array property .length)

	const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
	console.log(months.size);
	Returns : 12

Check if an item exist : .has() method

	console.log(months.has('September'));
	Returns : true
	
Retrieving All Values : .values() or .keys()

	console.log(months.values());
	Returns : SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}
	.keys() method behave the exact same way as the .values() method 
	.keys() method is an alias for the .values() method for similarity with maps. 
	
Looping over Sets : use the iterator methods

	const iterator = months.values();
	iterator.next();
	iterator.next();
	...
	iterator.next();
	Returns : 
		Object {value: 'January', done: false}
		Object {value: 'February', done: false}
		...
		Object {value: 'December', done: true}

better looping : note we don't need to call .values if we use for...of

	const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
	for (const color of colors) {
	  console.log(color);
	}
	
Weaksets

	is a special sort of Set
	can only contain objects
	is not iterable which means it can’t be looped over
	does not have a .clear() method. To delete an object just set it to null and it will be garbage collected
	useful in situations where you want an efficient, lightweight solution for creating groups of objects.
	more on garbage collection here : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection
	
Weakset example

	const student1 = { name: 'James', age: 26, gender: 'male' };
	const student2 = { name: 'Julia', age: 27, gender: 'female' };
	const student3 = { name: 'Richard', age: 31, gender: 'male' };

	const roster = new WeakSet([student1, student2, student3]);
	console.log(roster);
	Returns : WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}
	
	roster.add('Amanda')
	Returns : Uncaught TypeError: Invalid value used in weak set(…). Amanda is not an object
	
	student3 = null;
	console.log(roster);
	Returns : WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}
	
Maps

	are modified using .set() method and adding key-values pairs to itself
	.set first argument is the key
	.set second argument is the value
	can remove a key-value pairs by calling its .delete() method.
	can remove all its key-value pairs by calling its .clear() method.
	can check if a key-value pair exist by using its .has() method.
	can retrieve value by using its .get() method.
	
	if you .set() a key-value pair to a Map that already uses the same key, you won’t receive an error, but the key-value pair will overwrite what currently exists in the Map. 
	if you try to .delete() a key-value that is not in a Map, you won’t receive an error, and the Map will remain unchanged.
	the .delete() method returns true if a key-value pair is successfully deleted from the Map object, and false if unsuccessful. 
	the return value of .set() is the Map object itself if successful.
	
How to Create a Map

	const employees = new Map();
	console.log(employees);
	Returns : Map {}
	
Modifying Maps : set and delete

	const employees = new Map();

	employees.set('james.parkes@udacity.com', { 
		firstName: 'James',
		lastName: 'Parkes',
		role: 'Content Developer' 
	});
	employees.set('julia@udacity.com', {
		firstName: 'Julia',
		lastName: 'Van Cleve',
		role: 'Content Developer'
	});
	employees.set('richard@udacity.com', {
		firstName: 'Richard',
		lastName: 'Kalehoff',
		role: 'Content Developer'
	});

	console.log(employees);	
	Returns : Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}
	
can remove a key-value pairs by calling its .delete() method.
	
	employees.delete('julia@udacity.com');
	employees.delete('richard@udacity.com');
	console.log(employees);
	Returns : Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}
	
can remove all its key-value pairs by calling its .clear() method.
	
	employees.clear()
	console.log(employees);
	Returns : Map {}
		
can check if a key-value pair exist by using its .has() method.
	
	const members = new Map();
	members.set('Evelyn', 75.68);
	members.set('Liam', 20.16);
	members.set('Sophia', 0);
	members.set('Marcus', 10.25);
	console.log(members.has('Xavier'));
	console.log(members.has('Marcus'));
	Returns : 
		true
		false

can retrieve value by using its .get() method.

	console.log(members.get('Evelyn'));
	Returns : 75.68

Looping Through Maps : 3 options

	Step through each key or value using the Map’s default iterator
	Loop through each key-value pair using the new for...of loop
	Loop through each key-value pair using the Map’s .forEach() method

Step through each key or value using the Map’s default iterator

	let iteratorObjForKeys = members.keys();
	iteratorObjForKeys.next();
	iteratorObjForKeys.next();
	...
	let iteratorObjForValues = members.values();
	iteratorObjForValues.next();
	iteratorObjForValues.next();
	...

	Returns : 
		Object {value: 'Evelyn', done: false}
		Object {value: 'Liam', done: false}
		...
		Object {value: 75.68, done: false}
		...
		
Loop through each key-value pair using the new for...of loop

	for (const member of members) {
	  console.log(member);
	}
	
	Returns : 
		['Evelyn', 75.68]
		['Liam', 20.16]
		['Sophia', 0]
		['Marcus', 10.25]

	Note that key-value pair here is split up into an array where the first element is the key and the second element is the value

Loop through each key-value pair using the Map’s .forEach() method

	members.forEach((key, value) => console.log(key, value));
	Returns : 
		 'Evelyn' 75.68
		 'Liam' 20.16
		 'Sophia' 0
		 'Marcus' 10.25	

Weakmaps

	is a special sort of Map
	can only contain objects as keys
	is not iterable which means it can’t be looped over
	does not have a .clear() method. To delete an object just set it to null and it will be garbage collected
	useful in situations where you want an efficient, lightweight solution for creating groups of objects.
	more on garbage collection here : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection


how to create 

	const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
	const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
	const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };
	const library = new WeakMap();
	library.set(book1, true);
	library.set(book2, false);
	library.set(book3, true);
	console.log(library);

	Returns : 
		WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}

	library.set('The Grapes of Wrath', false);
	Returns : Uncaught TypeError: Invalid value used as weak map key(…) 'The Grapes of Wrath' is not an object
	
	book1 = null;
	console.log(library);
	Returns : WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}

Promises

	is a new way to handle asynchronous requests
	is created with the new Promise constructor function - new Promise()
	code must be defined inside the constructor of the function
	can execute a resolve function after having finished executed sucessfully the constructor code
	can execute a reject function the constructor code  when the request could not be completed.
	immediately returns an object that is not result of the asynchronous request
	object have a .then() method that is able to use the results of the asynchronous call.
	.then() have 2 arguments (which are functions), first function get the resolve result, second gets the reject result	
	https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
	there is a dedicated udacity course for that : https://www.udacity.com/course/javascript-promises--ud898

code must be defined inside the constructor of the function
	
	new Promise(function () { //This promise constructor function
		window.setTimeout(function createSundae(flavor = 'chocolate') {
			const sundae = {};
			// request ice cream
			// get cone
			// warm up ice cream scoop
			// scoop generous portion into cone!
		}, Math.random() * 2000);
	});

can execute a resolve function after having finished executed sucessfully the constructor code

	new Promise(function (resolve, reject) {
		window.setTimeout(function createSundae(flavor = 'chocolate') {
			const sundae = {};
			// request ice cream
			// get cone
			// warm up ice cream scoop
			// scoop generous portion into cone!
			resolve(sundae);
		}, Math.random() * 2000);
	});

can execute a reject function the constructor code  when the request could not be completed.

	new Promise(function (resolve, reject) {
		window.setTimeout(function createSundae(flavor = 'chocolate') {
			const sundae = {};
			// request ice cream
			// get cone
			// warm up ice cream scoop
			// scoop generous portion into cone!
			if ( /* iceCreamConeIsEmpty(flavor) */ ) {
				reject(`Sorry, we're out of that flavor :-(`);
			}
			resolve(sundae);
		}, Math.random() * 2000);
	});
	
immediately returns an object that is not result of the asynchronous request

	const myPromiseObj = new Promise(function (resolve, reject) {
		// sundae creation code
	});
	
object have a .then() method that is able to use the results of the asynchronous call.

	mySundae.then(function(sundae) {
		console.log(`Time to eat my delicious ${sundae}`);
	}, function(msg) {
		console.log(msg);
		self.goCry(); // not a real method
	});

Proxies

	are object that takes all requests of another object 
	ask this object what he wants to do with the request he received for him
	tell the requester object what the object want
	its a sort of filter (if you replace objects by people, you will visualize easilly)
	
Proxy constructor

	new Proxy();
	takes 2 items as parametters
		the object that it will be the proxy for : the proxied object
		an object containing the list of methods it will handle for the proxied object :  the handler
		
simple proxy

	var richard = {status: 'looking for work'};
	var agent = new Proxy(richard, {});
	agent.status; // returns 'looking for work'

proxy handler methods = proxy handler traps

	most used methods are get and set
	others methods are
		the get trap - lets the proxy handle calls to property access. 
		the set trap - lets the proxy handle setting the property to a new value
		the apply trap - lets the proxy handle being invoked (the object being proxied is a function)
		the has trap - lets the proxy handle the using in operator
		the deleteProperty trap - lets the proxy handle if a property is deleted
		the ownKeys trap - lets the proxy handle when all keys are requested
		the construct trap - lets the proxy handle when the proxy is used with the new keyword as a constructor
		the defineProperty trap - lets the proxy handle when defineProperty is used to create a new property on the object
		the getOwnPropertyDescriptor trap - lets the proxy handle getting the property's descriptors
		the preventExtenions trap - lets the proxy handle calls to Object.preventExtensions() on the proxy object
		the isExtensible trap - lets the proxy handle calls to Object.isExtensible on the proxy object
		the getPrototypeOf trap - lets the proxy handle calls to Object.getPrototypeOf on the proxy object
		the setPrototypeOf trap - lets the proxy handle calls to Object.setPrototypeOf on the proxy object
	more info here : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/handler
	
get trap example

	const richard = {{status: 'looking for work'}: 'looking for work'};
	const handler = {
		get(target, propName) {
			console.log(target); 
			console.log(propName); 
		}
	};
	const agent = new Proxy(richard, handler);
	agent.status; 
	
	returns : 
		{status: 'looking for work'}
		status
		
note about the code above

	const agent = new Proxy(richard, handler); // agent is a Proxy
	agent.status; //Because agent is a Proxy. This line will do 2 things
		1. look in the object provided if there is a property call status
		2. excute all trap of the handler methods (if there are some)

get trap can have a return statement

	const richard = {status: 'looking for work'};
	const handler = {
		get(target, propName) {
			console.log(target);
			console.log(propName);
			return target[propName];
		}
	};
	const agent = new Proxy(richard, handler);
	agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
	
note about the code above

	i'm not sure how to access what's returned by get method.
	Does console.log(agent.status) will write 'looking for work' ?
	
set trap example

	const richard = {status: 'looking for work'};
	const handler = {
		set(target, propName, value) {
			if (propName === 'payRate') { // if the pay is being set, take 15% as commission
				value = value * 0.85;
			}
			target[propName] = value;
		}
	};
	const agent = new Proxy(richard, handler);
	agent.payRate = 1000; // set the actor's pay to $1,000
	agent.payRate; // $850 the actor's actual pay
	
generators

	allow to stop the execution of the function in the middle and pick up again at some later point.
	is declared in a function using * sign. All of those 3 are valid declaration
		function* getEmployee() {
		function * getEmployee() {
		function *getEmployee() {
	create an iterator and run the code they have in the next() method of the iterator
	can be paused using 'yield' keyword
	can send data using 'yield data_to_send' 
	can receive data using the next() method and the yield keyword. It "replace" the yield keyword with the data provided by the next() method
	will be used heavily in upcoming additions to the JavaScript language. One upcoming feature that will make use of them is async functions. https://github.com/tc39/ecmascript-asyncawait
	
Example 

	function* getEmployee() {
		console.log('the function has started');

		const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

		for (const name of names) {
			console.log( name );
		}

		console.log('the function has ended');
	}
	
	getEmployee();

	// response you get in Chrome:
	getEmployee {[[GeneratorStatus]]: "suspended", [[GeneratorReceiver]]: Window}
	
Using yield

	function* getEmployee() {
		console.log('the function has started');

		const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

		for (const name of names) {
			console.log(name);
			yield;
		}

		console.log('the function has ended');
	}
	const generatorIterator = getEmployee();
	generatorIterator.next();
	
First iteration returns

	the function has started
	Amanda
	
Second... etc until the end of the function

	Diego
	
yielding data

	function* getEmployee() {
		console.log('the function has started');

		const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

		for (const name of names) {
			yield name;
		}

		console.log('the function has ended');
	}
	const generatorIterator = getEmployee();
	let result = generatorIterator.next();
	result.value // is "Amanda"

	generatorIterator.next().value // is "Diego"
	generatorIterator.next().value // is "Farrin"

can receive data using the next() method

	function* displayResponse() {
		const response = yield;
		console.log(`Your response is "${response}"!`);
	}

	const iterator = displayResponse();

	iterator.next(); // starts running the generator function
	iterator.next('Hello Udacity Student'); // send data into the generator
	// the line above logs to the console: Your response is "Hello Udacity Student"!
	
Another example

	function* createSundae() {
		const toppings = [];

		toppings.push(yield);
		toppings.push(yield);
		toppings.push(yield);

		return toppings;
	}

	var it = createSundae();
	it.next('hot fudge');
	it.next('sprinkles');
	it.next('whipped cream');
	it.next(); //topping will have undefined as its last item
	
Example using both sending and retrieving data to and from the generator

	function* getEmployee() {
		const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
		const facts = [];

		for (const name of names) {
			// yield *out* each name AND store the returned data into the facts array
			facts.push(yield name); 
		}

		return facts;
	}

	const generatorIterator = getEmployee();

	// get the first name out of the generator
	let name = generatorIterator.next().value;

	// pass data in *and* get the next name
	name = generatorIterator.next(`${name} is cool!`).value; 

	// pass data in *and* get the next name
	name = generatorIterator.next(`${name} is awesome!`).value; 

	// pass data in *and* get the next name
	name = generatorIterator.next(`${name} is stupendous!`).value; 

	// you get the idea
	name = generatorIterator.next(`${name} is rad!`).value; 
	name = generatorIterator.next(`${name} is impressive!`).value;
	name = generatorIterator.next(`${name} is stunning!`).value;
	name = generatorIterator.next(`${name} is awe-inspiring!`).value;

	// pass the last data in, generator ends and returns the array
	const positions = generatorIterator.next(`${name} is magnificent!`).value; 

	// displays each name with description on its own line
	
	positions.join('\n');
	
	
ES6 and old browsers

	Browser makers have to keep up with all HTML, CSS, and JavaScript changes
	they do this by following specifiactions
		World Wide Web Consortium (W3C) is the standards body for things like HTML, CSS, and SVG
		Ecma International is an industry association that develops and oversees standards like JavaScript(ES6) and JSON.
		
		
World Wide Web Consortium (W3C) is the standards body for things like HTML, CSS, and SVG
	
	https://www.w3.org/
	
Ecma International is an industry association that develops and oversees standards like JavaScript(ES6) and JSON.

	https://www.ecma-international.org/
	http://www.ecma-international.org/ecma-262/6.0/index.html (ES6)
	Ecma International is an important industry community and definitely worth checking out in more detail
	https://en.wikipedia.org/wiki/Ecma_International
	http://www.ecma-international.org/memento/index.html
	
How Can You Know What Features Browsers Support?

	Google Chrome - https://www.chromestatus.com/features#ES6
	Microsoft Edge - https://developer.microsoft.com/en-us/microsoft-edge/platform/status/?q=ES6
	Mozilla Firefox - https://platform-status.mozilla.org/
	
This can be a lot of information to track down. If you prefer a birdseye view of all the feature support for all JavaScript code, 

	check out the ECMAScript Compatibility Table built by @kangax:
	http://kangax.github.io/compat-table/es6/
	
Polyfill

	is a javascript file that patches a hole by replicating some native feature for browser that don't have it yet
	it's basically a plugin
	https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills
	https://en.wikipedia.org/wiki/Polyfill
	
An example polyfill

	if (!String.prototype.startsWith) { //Check if the native method exist before overridding it. We don't want to override if it exist
	  String.prototype.startsWith = function (searchString, position) {
		position = position || 0; //position is the position or 0 if position is undefined
		return this.substr(position, searchString.length) === searchString;
	  };
	}
	
	same code but more robust : https://github.com/mathiasbynens/String.prototype.startsWith/blob/master/startswith.js
	
Transpilling

	takes source code to target code	
	source code is human readable
	target code is human readable
	exple : 
		use to convert ES6 to ES5
		use to convert java to javascript		

Compilling
	
	takes source code to target machine code
	source code is human readable
	target code is not human readable
	exple : use to convert C++ to machine code 	
	
Babel

	convert ES6 to ES5
	convert JSX to JavaScript
	convert Flow to JavaScript.
	
transpiling some ES6 code into ES5 code directly on the Babel website. Copy this

	class Student {
	  constructor (name, major) {
		this.name = name;
		this.major = major;
	  }

	  displayInfo() {
		console.log(`${this.name} is a ${this.major} student.`);
	  }
	}

	const richard = new Student('Richard', 'Music');
	const james = new Student('James', 'Electrical Engineering');

And paste it here

	http://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015
	
Babel plugins

	http://babeljs.io/docs/plugins/transform-es2015-arrow-functions/
	http://babeljs.io/docs/plugins/transform-es2015-template-literals/
	http://babeljs.io/docs/plugins/
	
Babels presets (=groups of plugins bundled together)

	http://babeljs.io/docs/plugins/preset-es2015/
	
Take this repo that is all setup for compiling

	https://github.com/udacity/course-es6/tree/master/lesson-4/walk-through-transpiling
	
In .babelrc file add this

	{
		"presets" : ["es2015"]
	}
	
Make sure you have ... installed

	node
	npm

If not 

	install Node (which will automatically install NPM)
	https://nodejs.org/en/
	
package.json list all the npm packages that this project depends on. This project depends on

	babel-cli
	babel-preset-es2015
	
each npm packages 

	will check the .babelrc for which plugins and presets to use
	
now we need to tell babel to transpile the code. To do this we add this in pakage.json

"script" : {
	"build" : "babel ES6 -d ES5"
}
	
AJAX

	means asynchronous javascript and xml. But today it's more than that.
	help you requested data asynchronousy and
	notify when you it have the data
	request allow for content retrival and display without reloading web page
	request requiere an API key, or Oauth, or no authentification at all
	allow update the current page in place without fetching an entire page from the server
	is the technique of using XMLHTTPRequest to fetch data and then modify the current page.
	more : https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
	
data can be of any kind

	xml file
	javascript file
	Json from Rest api
	
there is 3 way to make request in ajax

	with the tried-and-true XHR object
	with jQuery
	with fetch (the last and best)
	
record an ajax request

	go to google.com
	open devTools
	got to network tab
	make sure button reccord is pressed (red)
	start wrtting a search keyword
	the homepage is replaced
	the network tool show a request of type XRH
	more on server request on udacity courses : https://classroom.udacity.com/courses/ud303
	
more on XMLHttpRequests (commonly abbreviated as XHR or xhr). 

	Go to https://unsplash.com/
	open devTool
	type const asyncRequestObject = new XMLHttpRequest(); on the console

we've constructed an XHR object named asyncRequestObject.  There are a number of methods that are available to us. The most important is 

	the open method
	asyncRequestObject.open();
	.open() method does not actually send the request! It sets the stage and gives the object the info it will need when the request is actually sent. 
	Passing false as the third option makes the XHR request become a synchronous one. 
	
open need 2 parameters
	
	1. the request parameter
	2. the url
	
the request parameter can be

	GET to asynchronously retrieve a page
	POST to asynchronously send data to a server
	
example of Get

	asyncRequestObject.open('GET', 'https://unsplash.com');
	
To actually send the request, we need to use the 'send' method:

	asyncRequestObject.send();
	https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send
	now request is sent but we don't see anything
	
To handle the successful response of an XHR request, we set the 'onload property' on the object to a function that will handle it:

	function handleSuccess () {
		// in the function, the `this` value is the XHR object
		// this.responseText holds the response from the server

		console.log( this.responseText ); // the HTML of https://unsplash.com/
	}
	asyncRequestObject.onload = handleSuccess;
	
	More on this here : https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequestEventTarget/onload
	
To handle the unsuccessful response of an XHR request, we set the 'onerror property' on the object to a function that will handle it:

	function handleError () {
		// in the function, the `this` value is the XHR object
		console.log( 'An error occurred ??' );
	}

	asyncRequestObject.onerror = handleError;
	
Here is the full XHR request

	function handleSuccess () { 
	  console.log( this.responseText ); 
	// the HTML of https://unsplash.com/}
	function handleError () { 
	  console.log( 'An error occurred \uD83D\uDE1E' );
	}
	const asyncRequestObject = new XMLHttpRequest();
	asyncRequestObject.open('GET', 'https://unsplash.com');
	asyncRequestObject.onload = handleSuccess;
	asyncRequestObject.onerror = handleError;
	asyncRequestObject.send();
	
Same thing but this time handling json

	function handleSuccess () {
	const data = JSON.parse( this.responseText ); // convert data from JSON to a JavaScript object
	console.log( data );
	}

	asyncRequestObject.onload = handleSuccess;
	
After this point I have just copy/pasted what's written. Didn't really want to install the starter code etc.
	https://classroom.udacity.com/nanodegrees/nd019/parts/c5795c43-ebd1-4da9-8af9-db1c95ccf9e4/modules/b19830db-a890-435a-9a2c-3f5394b0df08/lessons/46eaae46-af74-4264-9393-15fe8c3357ca/concepts/685ff9da-fbaa-400c-94ae-72ab42743137

Download or clone the Starter Code

	https://github.com/udacity/course-ajax. 

Once you've cloned the project, you'll notice that it has three separate folders:

	lesson-1-async-w-xhr
	lesson-2-async-w-jQuery
	lesson-3-async-w-fetch
	Make sure to work on the files for the correct lesson. 
	
Create Your Accounts

To complete these final steps, you'll need accounts with Unsplash and The New York Times.

	Create a developer account here - https://unsplash.com/developers
	create an application here - https://unsplash.com/oauth/applications this will give you an "Application ID" that you'll need to make requests
	Create a developer account here - https://developer.nytimes.com/
	They'll email you your api-key (you'll need this to make requests)

In app.js, the variable searchedForText contains the text we're interested in, and we'll set the onload property to a function called addImage (which is a do-nothing function that we'll flesh out in a moment). If we temporarily set searchedForText to "hippos", the code for the XHR call to Unsplash is:

	function addImage(){}
	const searchedForText = 'hippos';
	const unsplashRequest = new XMLHttpRequest();
	unsplashRequest.open('GET', `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`);
	unsplashRequest.onload = addImage;
	unsplashRequest.send()
	
...but if you try running this code, you'll get an error. The XHR method to include a header with the request is setRequestHeader. So the full code needs to be:

	const searchedForText = 'hippos';
	const unsplashRequest = new XMLHttpRequest();
	unsplashRequest.open('GET', `https://api.unsplash.com/search/photos?page=1&query=${searchedForText}`);
	unsplashRequest.onload = addImage;
	unsplashRequest.setRequestHeader('Authorization', 'Client-ID <your-client-id>');
	unsplashRequest.send();
	function addImage(){
	}

Since the New York Times doesn't require a specific header, we don't need to do anything special. We'll set its onload property to the function addArticles that we'll flesh out in a minute:

	function addArticles () {}
	const articleRequest = new XMLHttpRequest();
	articleRequest.onload = addArticles;
	articleRequest.open('GET', `http://api.nytimes.com/svc/search/v2/articlesearch.json?q=${searchedForText}&api-key=<your-API-key-goes-here>`);
	articleRequest.send();

Make sure to fill in the URL above with the API key you received in an email from the New York Times after signing up as a developer.

Quick recap 

	To Send An Async Request
		create an XHR object with the XMLHttpRequest constructor function
		use the .open() method - set the HTTP method and the URL of the resource to be fetched
		set the .onload property - set this to a function that will run upon a successful fetch
		set the .onerror property - set this to a function that will run when an error occurs
		use the .send() method - send the request
		
	To Use The Response
		use the .responseText property - holds the text of the async request's response

JQuery 

	c'est un peu comme stetho pour recuperer des données json sous android
	was created a number of years ago back when browsers hadn't joined together to standardize on functionality
	is just JavaScript
	can be download here https://code.jquery.com/
	can be added in an html file using  <script> tag
	now that browsers have pretty much aligned, jQuery's usage is not as necessary as it was several years ago but ajax() method is still used
	ajax() method is used to handle all asynchronous requests
	there is a Udacity class : https://www.udacity.com/course/intro-to-jquery--ud245
	I've not finished followed the class either : https://classroom.udacity.com/nanodegrees/nd019/parts/c5795c43-ebd1-4da9-8af9-db1c95ccf9e4/modules/b19830db-a890-435a-9a2c-3f5394b0df08/lessons/3cad9ae5-9def-458d-8c44-cc23cf7e37a3/concepts/c4bbcf73-1115-412b-8acf-3a18ed5e4794

Fetch api

	is like JQuery but its buitin inside browser, not need to load a library
	Fetch Is Promise-based
	not followed this class either https://classroom.udacity.com/nanodegrees/nd019/parts/c5795c43-ebd1-4da9-8af9-db1c95ccf9e4/modules/b19830db-a890-435a-9a2c-3f5394b0df08/lessons/7cd5017a-cdce-463f-ba13-e53603fa83eb/concepts/7cd8e213-23ac-4eeb-858f-b3b90fc8a8b6
	
	
	
