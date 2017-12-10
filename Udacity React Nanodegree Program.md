# Intro

Used by many compagnies
Build by Facebook engineer

But according to a Quora post 

	"the React framework seems pretty damn amazing, even if you have to write stuff in JavaScript… The main issue is that it includes a Patent Grant file which concerns its BSD license..."
	This essentially boils down (with some caveats) to the following. If facebook infringes any of your patents or copyright and you go against them in a lawsuit, your license to use React or React Native is revoked.
	Either leave the door open to them being able to steal your stuff or you’re not allowed to use their “open-source” stuff. It sounds a bit draconian, doesn’t it?
	More on this here : https://www.quora.com/Which-one-is-recommended-for-a-new-Android-developer-React-native-Android-Java-or-Kotlin
	
Udacity students usefuls links

	Slack : https://udacity-react.slack.com/messages
	Issue reporting board (if I see a problem on the course) : https://waffle.io/udacity/reactnd-issues
	also the Classroom Mentorship
	question about the react nanodegree react-support@udacity.com
	
Udacity github projects and ressources used
	
	Git repo ContactServer : https://github.com/udacity/reactnd-contacts-server
	Git repo ContactList : https://github.com/udacity/reactnd-contacts-complete
	RecipeApi https://developer.edamam.com/edamam-recipe-api
	Github repo Udacimeal https://github.com/udacity/reactnd-udacimeals-complete
	Github rep UdaciFitness https://github.com/udacity/reactnd-UdaciFitness-complete
	
Udacity guide lines

	http://udacity.github.io/frontend-nanodegree-styleguide/index.html
	http://udacity.github.io/frontend-nanodegree-styleguide/css.html
	http://udacity.github.io/frontend-nanodegree-styleguide/javascript.html
	https://udacity.github.io/git-styleguide/
		
What is Classroom Mentorship?

	you will be paired with a dedicated mentor to support you during the remainder of your Nanodegree program experience. You will benefit from the familiarity, experience and knowledge enabled by being matched with a single classroom mentor throughout your program. These mentors will be better aligned to your individual needs. In addition to helping answer questions about the content and projects, these classroom mentors will also help keep you motivated and engaged in the curriculum.
	you will be able to chat with your in-classroom mentor via a chat window in the bottom right-hand corner of your classroom. Your classroom mentor is a real person and you can expect a response in less than 24 hours (usually much less). You can also reach out in your student community for quick help as well.
	
# React fundamentals

## Composition

React is javascript specialize in UI. It uses functions that return UI instead of values. Here is an example of javascript functions retuning values : 

	function getProfilePic(username){
		return 'https://github.com/'+username+'.png?size=200';
	}

	function getProfileLink(username){
		return 'https://github.com/'+username;
	}

	function getProfileData(username){
		return {
			pic : getProfilePic(username);
			link: getProfileLink(username);
		}
	}

	getProfileData('tylermcginnis'); //invocation

Lets modify them to return some UI

	function ProfilePic(username){
		return (<img alt={username} src={'https://github.com/'+username+'.png?size=200'}/>)
	}

	function ProfileLink(username){
		return <a href={'https://github.com/'+username}>{username}</a>;
	}

	function Profile(username){
		return (
		<div classname='profile'>
			<ProfilePic username='username'/>
			<ProfileLink username='username'/>
		</div>
		)
	}

	 //invocation ??
	 
What we see here

	return is followed by () or not. () are not necessarly needed.
	return is followed by html tag that are not surronded by ''. This is a fundamental difference between React and the other popular javascript frameworks.
	function name is a little bit changed getProfilePic become ProfilePic, to have a profile attribute that looks more like html.<ProfilePic username='username'/>
	javascript object are replace by a div class which must have a name.
	
You may wonder, why not having one single function like that

	function getProfileData (username) {
	  return {
		pic: 'https://github.com/' + username + '.png?size=200',
		link: 'https://github.com/' + username
	  }
	}

and accessing if needed a single part of it like that

	var pic=getProfileData.pic;
	
because a good function should follow the DOT rule. Do One Thing. Here getProfileData is only aggregating data, that's it's main function. This allow to have getProfilePic more complexe in the future.

	function getProfileData(username){
		return {
			pic : getProfilePic(username);
			link: getProfileLink(username);
		}
	}

React makes use of the power of composition, heavily! React builds up pieces of a UI using components. Here is an example of component composition

	<Page>
	  <Article />
	  <Sidebar />
	</Page>
	
Now if our previous functions were components we would have
	
	<Profile>
	  <ProfilePic />
	  <ProfileLink />
	</Profile>
	
## Imperative vs Declarative

In a imperative world, you would tell them step by step how to make dinner. You have to provide theme these instructions:

	Go to kitchen
	Open fridge
	Remove chicken from fridge
	...
	Bring food to table
	
In a declarative would, you would simply describe what you want

	I want a dinner with chicken.
	
If you don't know how to make chicken you can't use a declarative style. React is able to be declarative because it "knows how to make chicken", for example. Compared to backbone, which only knows how to interface with the kitchen. Baasically what you do is 

	You declare the state that you want. We talk of the state of the DOM here.
	
And then React does the imperative work of

	performing all of the JavaScript/DOM steps to get us to our desired result.
	
Let's take an example, here is the imperative code

	const people = ['Amanda', 'Geoff', 'Michael', 'Richard', 'Ryan', 'Tyler']
	const excitedPeople = []

	for (let i = 0; i < people.length; i++) {
	  excitedPeople[i] = people[i] + '!'
	}
	
and its imperative steps description

	created an iterator object
	told the code when it should stop running
	used the iterator to access a specific item in the people array
	stored each new string in the excitedPeople array
	
Here is the declarative code

	const people = ['Amanda', 'Geoff', 'Michael', 'Richard', 'Ryan', 'Tyler']
	const excitedPeople = people.map(name => name + '!')

all of those imperatives steps are taken care of by 

	JavaScript's .map() Array method.
	
Another example ... I'm not sure of the syntax here.

	button = document.getElementById("aButton")
	button.addEventListener(){
		activateTeleporter()
	}
	
would become

	<button onClick={activateTeleporter}>Activate Teleporter</button>
	
imperative steps not need of ... it's all done for you.

	no need to give  name to the button
	no need of button.addEventListener()

Conclusion 

	React is declarative
	
## Two-way data binding vs Unidirectional dataflow

Two-way data binding

	If a model changes the data, then the data updates in the view. Alternatively, if the user changes the data in the view, then the data is updated in the model.
	but when app grow it become more and more difficult to determine where the data is actually being updated.
	Front-end frameworks like Angular and Ember make use of two-way data bindings
	
More on Angular and Ember two-way data binding
	
	https://angular.io/guide/template-syntax#!#two-way
	https://guides.emberjs.com/v2.13.0/object-model/bindings/
	
Unidirectional dataflow

	data flow down between components from parent to child.
	data lives in the parent, never in the child and never in its  gran-parents (in fact in Redux class they say its possible to pass the data from parent to parent to reach the child, but if it is the case its better to use Redux)
	parents only can change its data and the data of its childs
	child can only request a change by asking its parent to make the change. Sometime it is the child that receive the data (exple : textview that receive user input). To update it's view it must gives the receive string to its parent that will update himself and then him.
	
to make a parallel with android

	if fragmentA contains fragmentB
	and fragmentA and frangmentB display the same bitmap.
	FragmentA will load the bitmap and passes it to FragmentB.
	FragmentB won't load the bitmap and passes it to FragmentA because is just not allowed by React which is unidirectional and only accept Parent to Child transfert.
	FragmentA and FragmentB will have a bitmap attribute ? No. Because data lives in the parent, never in the child.
	Does this means MainActivity will have all attributes values of the all app ?
	
If the following sample code were a React application, which of the following components should be in charge of making updates to data? Check all that apply.

	<FlightPlanner>
	  <LocationPicker>
		<OriginPicker />
		<DestinationPicker />
	  </LocationPicker>
	  <DatePicker />
	</FlightPlanner>
	
Answer is

	<FlightPlanner>
	<LocationPicker>
	
## React is javascript

React doesn't like to recreate functionality that you could already do in Javascript. Its a use of most powerful javascript methods. Example React will choose to write this : 

	const friends = ['Michael', 'Ryan', 'Tyler'];
	<ul>
		friends.map(name => <li>{name}</li>)}
	</ul>

instead of this :  

	const friends = ['Michael', 'Ryan', 'Tyler'];
	<ul>
		<li>{friends[0]}</li>
		<li>{friends[1]}</li>
		<li>{friends[2]}</li>
	</ul>

React builds on a lot of the techniques of functional programming. JavaScript functions that are vital to functional programming are : 

	Array's .map() Method
	Array's .filter() Method

### Array's .map() Method

	const names = ['Michael', 'Ryan', 'Tyler'];
	const nameLengths = names.map( name => name.length );
	nameLengths will be a new array [7, 4, 5]
	This is important to understand; the .map() method returns a new array, it does not modify the original array.

Exercice

	/* Using .map()
	 *
	 * Using the musicData array and .map():
	 *   - return a string for each item in the array in the following format
	 *     <album-name> by <artist> sold <sales> copies
	 *   - store the returned data in a new albumSalesStrings variable
	 *
	 * Note:
	 *   - do not delete the musicData variable
	 *   - do not alter any of the musicData content
	 *   - do not format the sales number, leave it as a long string of digits
	 */

	const musicData = [
		{ artist: 'Adele', name: '25', sales: 1731000 },
		{ artist: 'Drake', name: 'Views', sales: 1608000 },
		{ artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
		{ artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
		{ artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
		{ artist: 'Original Broadway Cast Recording', 
		  name: 'Hamilton: An American Musical', sales: 820000 },
		{ artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
		{ artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
		{ artist: 'Rihanna', name: 'Anti', sales: 603000 },
		{ artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
	];

	const albumSalesStrings = musicData.map(album => album.name+' by '+album.artist+' sold '+album.sales+' copies');

	console.log(albumSalesStrings);

	
This was my solution but their solution was a little bit different with the ${}

	const albumSalesStrings = musicData.map(album => `${album.name} by ${album.artist} sold ${album.sales} copies`);
	
### Array's .filter() Method
	
	const names = ['Michael', 'Ryan', 'Tyler'];
	const shortNames = names.filter( name => name.length < 5 );
	shortNames will be the new array ['Ryan']
	 
Exercice 

	/* Using .filter()
	 *
	 * Using the musicData array and .filter():
	 *   - return only album objects where the album's name is
	 *     10 characters long, 25 characters long, or anywhere in between
	 *   - store the returned data in a new info variable
	 *
	 * Note:
	 *   - do not delete the musicData variable
	 *   - do not alter any of the musicData content
	 */

	const musicData = [
		{ artist: 'Adele', name: '25', sales: 1731000 },
		{ artist: 'Drake', name: 'Views', sales: 1608000 },
		{ artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
		{ artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
		{ artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
		{ artist: 'Original Broadway Cast Recording', 
		  name: 'Hamilton: An American Musical', sales: 820000 },
		{ artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
		{ artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
		{ artist: 'Rihanna', name: 'Anti', sales: 603000 },
		{ artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
	];

	const results = musicData.filter(album => album.name.length <= 25 && album.name.length >= 10);

	console.log(results);
	
###  Combining .map() And .filter() Together

	const names = ['Michael', 'Ryan', 'Tyler'];
	const shortNamesLengths = names.filter( name => name.length < 5 ).map( name => name.length );
	On a side note, you'll want to run things in this order (.filter() first and then .map()). Because .map() runs the function once for each item in the array, it will be faster if the array were already filtered.
	
Exercice

	/* Combining .filter() and .map()
	 *
	 * Using the musicData array, .filter, and .map():
	 *   - filter the musicData array down to just the albums that have 
	 *     sold over 1,000,000 copies
	 *   - on the array returned from .filter(), call .map()
	 *   - use .map() to return a string for each item in the array in the
	 *     following format: "<artist> is a great performer"
	 *   - store the array returned form .map() in a new "popular" variable
	 *
	 * Note:
	 *   - do not delete the musicData variable
	 *   - do not alter any of the musicData content
	 */

	const musicData = [
		{ artist: 'Adele', name: '25', sales: 1731000 },
		{ artist: 'Drake', name: 'Views', sales: 1608000 },
		{ artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
		{ artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
		{ artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
		{ artist: 'Original Broadway Cast Recording', 
		  name: 'Hamilton: An American Musical', sales: 820000 },
		{ artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
		{ artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
		{ artist: 'Rihanna', name: 'Anti', sales: 603000 },
		{ artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
	];

	const popular = musicData.filter(album => album.sales > 1000000).map(album => `${album.artist} is a great performer`);

	console.log(popular);
	
## React is javascript but

	React is an extension of JavaScript (i.e., a JavaScript library), but it isn't built into your browser. 
	You wouldn't be able to test out React code samples in your browser console the way you would if you were learning JavaScript.
	You will need to install a React environnement
	
# Rendering UI

React elements 
	
	are not surronded by ''. This is a fundamental difference between React and the other popular javascript frameworks.
	are lightweight javascript object
	are NOT actual DOM nodes
	
Javascript will put together react elements and DOM nodes.
	
	We describe how the page should look like in the React element.
	We let React generate the DOM nodes to achieve the result.
	
Components

	are React custom elements
	are created using React.createElement() method. Tell that to render ?
	are shown inside the page using . ReactDom.render() Does the Rendering.
	encourages programmer to use composition instead of inheritance

React.createElement()

	const element = React.createElement('div', null, 'hello world') //This is a top level API call
	is different from the documents.createElement
	1st arg : tag name of the element we want to use here a div
	2nd arg : null for now. It's for property we want to give to our DOM node.
	3rd arg : the text we will put inside the div
	
1st arg : tag name of the element we want to use here a div

	a string of any existing HTML element (e.g. 'p', 'span', or 'header') 
	or a React component (we'll be creating components with JSX, in just a moment).

2nd arg : null for now. It's for property we want to give to our DOM node.

	null,
	an object :	This is an object of HTML attributes and custom data about the element.

3rd arg : the text we will put inside the div

	 null,
	 a string, 
	 a React Element, 
	 or a React Component
	 javascript code
	
React

	can render stuff on a browser : ReactDom
	can render stuff on a server
	can render on native devices
	can render on VR environments (Virtual Reality environments)
	
ReactDom

	ReactDom.render(
		element, //Render my element into
		 document.getElementById('root') //a DOM node in that case, the root element that already on the page. Where is this root see below
	)
	
Now do a 

	console.log(element)
	
And look at the Chrome Inspector

	you see it's a javascript object
	private properties are in gray. You wont access them using the element.

Where is the root of a React app ?

	in the html file called ?
	
This file in the text editor gives nothing else than this

	<div id='root'></div>
	
Let's dig deeper. Try this

	const element = React.createElement('div', {class:'welcome-message'}, 'hello world')
	you get a warning. "Unknown DOM property class. did you mean className ? in div" See note a html below
	
try that

	const element = React.createElement('div', {className:'welcome-message'}, 'hello world')
	warning is gone. 
	an Elements tab appear in the console where you see the tree of your React page
	you have <div id='root'></div> and inside he div element you added has the class you expected <div data-reactroot class='welcome-message'>hello world</div> == $0
	the div inserted is given an index here $0 that will allow us to inspect easily one particular div in a console

as you see

	you used keyword className to describe DOM node
	keyword className what transform into class because this DOM node is an HTML one and class is the name of the html attribute
	
Note about html

	html is a custom implementation of the DOM
	react is another implementation of the DOM
	browsers parses html to a DOM
	
Inspect the div in the 'console tab' and type

	div=$0
	again you see the html representation with the word 'class' <div data-reactroot class='welcome-message'> that let you know you are on the correct div
	but here the div you have is the react node
	
now type
	
	div.class
	you can't div.class is undifined in the DOM
	
now type 

	div.className
	you get the string you expect 'welcome-message'
	
What is a VirtualDom

	are NOT real Dom element
	are NOT created
	are objects that describe Real Dom elements
	React.createElement does not create anything in the dom yet. It create a VirtualDom.
	ReactDom.render create the real DOM element
	
Supported Html attributes in React

	https://facebook.github.io/react/docs/dom-elements.html#all-supported-html-attributes
	
Nesting example

	const element = React.createElement('div', null, React.createElement('strong', null, 'hello world'))
	ReactDom.render(element, document.getElementById('root'))
	
idem with a list

	const element = React.createElement('ol', null, 
		React.createElement('li', null, 'Mickael')
		React.createElement('li', null, 'Ryan')
		React.createElement('li', null, 'Tyler')
	)
	ReactDom.render(element, document.getElementById('root'))
	
better with dynamic code solution 

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = React.createElement('ol', null, 
		people.map(person => (
				React.createElement('li', null, person.name)
		))
	)
	ReactDom.render(element, document.getElementById('root'))
	
If we try this React will complains

	"Each child in an array should have an unique key property. Check the top level render call"
	That means you need to add an unique key the each React Dom element of your array.
	we add it in the dom property parameter
	
If we use the name as a key (because in our case we know it's unique)

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = React.createElement('ol', null, 
		people.map(person => (
				React.createElement('li', {key:person.name}, person.name)
		))
	)
	ReactDom.render(element, document.getElementById('root'))
	
But we could also have used the array index (and its better practice)

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = React.createElement('ol', null, 
		people.map((person, index) => (
				React.createElement('li', {key:index}, person.name)
		))
	)
	ReactDom.render(element, document.getElementById('root'))
	
About map method

	first arg of the map callback is the object
	second argument of the map callback is the index
	
	
JSX
	
	is a syntax extention of javascript that lets us write javascript code that looks more like html
	This nested description is not very intuitive
	
lets convert our pevious code with JSX

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = <ol><li>person.name[0]</li></ol>
	ReactDom.render(element, document.getElementById('root'))
	
See in chrome

	1.person.name[0]
	
Not what we want, let's add curly brackets around to tel JSX to evaluate


	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = <ol><li>{person.name[0]}</li></ol>
	ReactDom.render(element, document.getElementById('root'))
	
See in chrome

	1.Michael
	
Note you can put any javascript code inside brackets

	{1+4}
	{false ? 'hello' : 'goodbye'}
	{people.map(person => <li>{person.name}</li>}
	
Witch gives with the key props

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = <ol>
		{people.map(person => <li key={person.name}>{person.name}</li>)}
	</ol>
	ReactDom.render(element, document.getElementById('root'))
	
Now with indexes

	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
	
	const element = <ol>
		{people.map(person, index => <li key={index}>{person.name}</li>)}
	</ol>
	ReactDom.render(element, document.getElementById('root'))

Notes

	see how we alternate between JSX and java using those curly braces
	after compiling (by typing debugger and run) JSX is convert to createElement method
	When writing JSX, keep in mind that it must only return a single element. This element may have any number of descendants, but there must be a single root element wrapping your overall JSX

	
How to create React component

	create a class that extends React.Component if use "import React from 'react';"
	create a class that extends Component if use "import React, { Component } from 'react';"
	implements method render() as follow
	instead of rendering the element, render the ContactList
	
Which  gives

	class ContactList extends React.Component{
	
			render(){
			
			const people = [
				{name:'Mickael'}, 
				{name:'Ryan'},
				{name:'Tyler'}
			]
			
			return <ol>
				{people.map(person => <li key={person.name}>{person.name}</li>)}
			</ol>
		}
	}
	ReactDom.render(<ContactList/>, document.getElementById('root'))
	
Components

	should follow the single responsibility principle and just "do one thing".
	If it manages too many different tasks, it may be a good idea to decompose your component into smaller subcomponents.
	
# To run JSX code you need

	a transpiler/compiler to transform JSX into regular JavaScript that will reach the browser. We typically use Babel.
	build tool which will bundle all of our assets (JavaScript files, CSS, images, etc.) for our web projects. We typically use Webpack
	nodeJS to run npm commands
	 
## NodeJs

	permet de développer des sites web et des applications web en javascript
	urilisé par Microsoft, Google, Yahoo!, LinkedIn, Ebay
	
## Download nodeJS

	https://nodejs.org/en/download/
	Je l'ai mis dans program F:\Mes Documents\Programmes\NodeJs
	
## apres installation on a dans C:\Program Files\nodejs\

	L'exécuteur node.js : le programme permettant d'exécuter des fichiers .js (comme php.exe le ferait avec des .php).
	Le module npm (Node Package Manager) : un gestionnaire de modules qui va vous permettre simplement d'ajouter et retirer les librairies dont vous aurez besoin pour vos applications (pas de surplus, seulement le nécessaire donc).
	Un raccourci vers la documentation en ligne.
	Des variables d'environnements : Ainsi vous pourrez exécuter les commandes node et npm dans votre invité de commande.
	
# Create a React project

run this 

	npm install -g create-react-app
	
this will

	grab the create-react-app from npm registry
	-g flag will install npm globally means the create-react-app command will be available on terminal
	
now type

	cd /c/ProgrammingProjects/JavascriptProjects/
	create-react-app contacts
	
as you can see it install

	react
	react-dom
	react-scripts contains 
		Babel so we can use the latest javascript syntax and JSX
		Webpack so we can generate the build
		Webpack Web Server which give us the auto reload behavior
	
now type

	cd contacts
	npm start
	
what's happen

	a browser is opened telling
	"To get started, edit src/App.js and save to reload."
	
open src/App.js 
	
	Ctrl+O scrapp
	make sur you are openning your local scr/app.js and not the one deployed on localhost
	if you don't see it follow "Add local source files to workspace" tutorial https://developers.google.com/web/tools/setup/setup-workflow
	basically open the sources left-side panel
	right click > Add Folder to Workspace > Choose your contacts folder > Authoriser
	
change it and reload
	
	Change <h1 className="App-title">Welcome to React</h1> by <h1 className="App-title">Welcome to React - Hello World</h1>
	I've got this error "Uncaught SyntaxError: Unexpected token import"
	I've asked fo help but still no answer. Anyway if I reload the file after change it works.
	So save ctrl-S
	npm start (yes seems that I'm not able to make auto-reload behavior works)
	as you can see your change has appeared
	
Lets explore the src directory

	as you can see app.js does not import react and react dom. It is index.js that does it.
	src/index.js import our app.js and react-dom
	public/index.html contains the root element. Webpack is going to put a script tag inside this div with our javascript script and a bundle. This is done when we build.
	
To get suggestions it is recommanded to 

	install the chrome extention "React Developper Tool" and 
	to allow URL file access
	More > Plus d'outils > Extensions > React Developper Tools >  Allow URL file access
	
# Composition over inheritance

lets render our contact list open src/app.js and
	
	remove import logo from './logo.svg'; and import './App.css';
	under the import copy paste the ContactList
	remove everything inside <div className="App"> and put the </ContactList> instead.
	
format auto indent

	Shift + Tab
	but it does not work well
	
you should have a file like that 

	import React, { Component } from 'react';

		class ContactList extends React.Component{
		
				render(){
				
				const people = [
					{name:'Mickael'}, 
					{name:'Ryan'},
					{name:'Tyler'}
				]
				
				return <ol>
					{people.map(person => <li key={person.name}>{person.name}</li>)}
				</ol>
			}
		}

	class App extends Component {
	  render() {
		return (
		  <div className="App">
			<ContactList/>
		  </div>
		);
	  }
	}

	export default App;
	
Now stop hardcoded the names. Change


	const people = [
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]
				
by

	const people = this.props.contacts

and change

	<ContactList/>
	
by

	<ContactList contacts=[
		{name:'Mickael'}, 
		{name:'Ryan'},
		{name:'Tyler'}
	]/>

Lets add several contacts

	import React, { Component } from 'react';

		class ContactList extends React.Component{
		
				render(){
				
				const people = this.props.contacts
				
				return <ol>
					{people.map(person => <li key={person.name}>{person.name}</li>)}
				</ol>
			}
		}

	class App extends Component {
	  render() {
		return (
		  <div className="App">
			<ContactList contacts={[
				{name:'Mickael'}, 
				{name:'Ryan'},
				{name:'Tyler'}
			]}/>
			<ContactList contacts={[
				{name:'Amanda'}, 
				{name:'Richard'},
				{name:'Jeff'}
			]}/>

		  </div>
		);
	  }
	}

	export default App;

Favor Composition Over Inheritance

	You might have heard before that it’s better to “favor composition over inheritance.” This is a principle that I believe is difficult to learn today. Many of the most popular programming languages make extensive use of inheritance, and it has carried over into popular UI frameworks like the Android and iOS SDKs.
	In contrast, React uses composition to build user interfaces.

React concepts

	props : allow to pass data into your components
	functional components : alternative to react components (a bit more intuitive)
	controlled components : attach your application forms with your component state
	
Modify your contacts folder to make it look like in this repository

	https://github.com/udacity/reactnd-contacts-complete/blob/starter-files-added/public/index.html
	
As you can see your app.js is now displaying 

	"Hello world"
	
Now install this backend server

	https://github.com/udacity/reactnd-contacts-server
	It's a simple Node/Express app 	
	cd /c/ProgrammingProjects/JavascriptProjects/contactsBackend/
	git clone https://github.com/udacity/reactnd-contacts-server.git
	cd reactnd-contacts-server/
	npm install  //needed to install the project dependencies
	
start the server with 

	node server.js
	
At this point, you should be running two different servers on your local machine:

	Front-end development server: Accessible on port 3000 (with npm start or yarn start)
	Back-end server: Accessible on port 5001 (with node server.js)
	
With function you have 'arguments'

	function fetchUser(username){
		
	}
	fetchUser('Tyler')

With React components you have 'props'

	class User extends React.Component{
		render(){
			return <p> Username : {this.props.username}</p>
		}
	}
	<User username='Tyler'/>
	
Or

	class User extends React.Component{
		render(){
			return 
			<div>
				<p> Username : {this.props.username}</p>
				<p> Is a Friend ? : {this.props.friend}</p>				
			</div>
		}
	}
	<User username='Tyler' friend={true}/>
	
Function vs components

	in a function you have argument
	in a composant the same concept is called props
	
Now display a static contact list. Create a ListContacts.js file as follow

	import React ,{Component} from 'react'

	class ListContacts extends Component{
		render(){
			return (
				<ol className='contact-list'>
				</ol>
			)
		}
	}

	export default ListContacts
	
Some notes

	export default ListContacts is Needed to access the ListContacts in the app.js
	className='contact-list' is a class we have in the index.css
	
Now in app.js add contacts

	const contacts = [
	  {
		"id": "ryan",
		"name": "Ryan Florence",
		"email": "ryan@reacttraining.com",
		"avatarURL": "http://localhost:5001/ryan.jpg"
	  },
	  {
		"id": "michael",
		"name": "Michael Jackson",
		"email": "michael@reacttraining.com",
		"avatarURL": "http://localhost:5001/michael.jpg"
	  },
	  {
		"id": "tyler",
		"name": "Tyler McGinnis",
		"email": "tyler@reacttraining.com",
		"avatarURL": "http://localhost:5001/tyler.jpg"
	  }
	]
	
add import 

	import ListContacts from './ListContacts'
	
delete helloWord and replace by

	<ListContacts/>
	
Now you don't see anything but 

	if you right-click inspect 
	the <ol> list exist

Now complete the <ol> list

	return (
		<ol className='contact-list'>
			{this.props.contacts.map(
				(contact) =>(<li key={contact.id}>{contact.name}</li>)
				)
			}
		</ol>
	)
	
As you can see the names are displayed but not the avatar etc lets change that

	return (
		<ol className='contact-list'>
			{this.props.contacts.map(
				(contact) =>
			(<li key={contact.id} className='contact-list-item'>
				<div className='contact-avatar' style={{backgroundImage: `url(${contact.avatarURL})`}}/>
				<div className='contact-details'>
					<p>{contact.name}</p>
					<p>{contact.email}</p>						
				</div>
				<button className='contact-remove'>Remove</button>
			</li>)
			)
			}
		</ol>
	)
	
Notes

	note the template literal `
	allow for embedded expressions. Using template literals, you can interpolate expressions as normal strings through your app.
	more here : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
	https://www.udacity.com/course/es6-javascript-improved--ud356
	
Stateless Functional components

	are used when you component component does not keep track of internal state (ie has only one method, the method render)
	it's simpler to read
	this.props is replaced by props alone
	props refers to data passed from parent component
	props represent "read-only" data that are immutable.
	Both state and props will generally be in the form of an object, and changes in either will trigger a re-render of the component, but they each play very different roles in your app.
	
Example this

	class User extends React.Component{
		render(){
			return <p> Username : {this.props.username}</p>
		}
	}
	<User username='Tyler'/>
	
Can be replaced by this

	function User(props) {
			return <p> Username : {props.username}</p>
		}
	<User username='Tyler'/>
	
Or by this if using ES6 function with an implicit return

	const User = (props) => (
	  <div>
		{props.username}
	  </div>
	);
	
If we change to a Stateless Functional components here is our component

	function ListContacts(props){
        return (
            <ol className='contact-list'>
                {props.contacts.map(
                    (contact) =>
				(<li key={contact.id} className='contact-list-item'>
					<div className='contact-avatar' style={{backgroundImage: `url(${contact.avatarURL})`}}/>
					<div className='contact-details'>
						<p>{contact.name}</p>
						<p>{contact.email}</p>						
					</div>
					<button className='contact-remove'>Remove</button>
				</li>)
				)
                }
            </ol>
        )
    }
	
Component state

	A component's state, on the other hand, represents mutable data that ultimately affects what is rendered on the page. 
	is class whose value is an object
	the state object key represent a distinct state
	we access the state properties using this.state.username
	because components are managing states we must make sure that data lives inside the component
	 
Example

	class User extends React.Component{
		
		state = {
			username: 'Tyler'
		}
	
		render(){
			return <p> Username : {this.props.username}</p>
		}
	}
	<User username='Tyler'/>
	
Here is how our app.js should look like using a state

	import React, { Component } from 'react';
	import ListContacts from './ListContacts'


	class App extends Component {

	  state = {
		contacts:[
		  {
			"id": "ryan",
			"name": "Ryan Florence",
			"email": "ryan@reacttraining.com",
			"avatarURL": "http://localhost:5001/ryan.jpg"
		  },
		  {
			"id": "michael",
			"name": "Michael Jackson",
			"email": "michael@reacttraining.com",
			"avatarURL": "http://localhost:5001/michael.jpg"
		  },
		  {
			"id": "tyler",
			"name": "Tyler McGinnis",
			"email": "tyler@reacttraining.com",
			"avatarURL": "http://localhost:5001/tyler.jpg"
		  }
		]
	  }

	  render() {
		return (
		  <div>
			<ListContacts contacts={this.state.contacts}/>
		  </div>
		)
	  }
	}

	export default App;

Props in Initial State

	When defining a component's initial state, avoid initializing that state with props. This is an error-prone anti-pattern, since state will only be initialized with props when the component is first created.

	this.state = {
	  user: props.user
	}
	In the above example, if props are ever updated, the current state will not change unless the component is "refreshed." Using props to produce a component's initial state also leads to duplication of data, deviating from a dependable "source of truth."
	

Component states reconciliation

	React compares the previous output and new output, determines what has changed, and makes these decisions for us. 
	This process of determining what has changed in the previous and new outputs is called Reconciliation.
	We dont update state directly. We use the built in function setState instead. There is 2 ways to use this function.
	
setState initialized with a function

	this.setState((prevState)=>({prevState.count:1}))
	used when the new state depend on the previous state
	
setState initialized with an object

	this.setState({username:'Tyler'})
	for everything else
	
React setState()

	whenever used re-render the entiere application to update the UI
	"in React your UI is just a function of you state"
	
Component custom methods

	they update the state
	
Let's create one

	removeContact=(contact) => {
		this.setState((state)=>({contacts : state.contacts.filter((c)=>c.id !== contact.id)}))
	}
	
add the props to the Listcontact

	<ListContacts onDeleteContact={this.removeContact} contacts={this.state.contacts}/>
	
make ListContact invoke use removeContact method with the contact corresponding

	<button onClick={() => props.onDeleteContact(contact)} className='contact-remove'>Remove</button>
	
propTypes is

	is useful for debuuging
	check props datatypes
	
install propTypes

	npm install --save prop-types
	npm run start
	
see my and their commit

	"Add PropTypes package to verify ListContacts props"
	https://github.com/udacity/reactnd-contacts-complete/commit/a7f4728c61b539863b91752bfe21924eb81f3039
	C:\ProgrammingProjects\JavascriptProjects\contacts
	
Exemple of proptypes

  PropTypes.array.isRequired
  PropTypes.func.isRequired
  PropTypes.number.isRequired
  
states and webapps

	in webapps components are called forms
	form state lives inside of the DOM
	but in React state lives inside of the components
	how to solve this problems ? with Controlled components
	
Controlled components 

	are components that render a forms
	have DOM state and component state
	but the source of thruth is considered to be the one inside the component
	then React is controlling (generating) the state of the form thats why it is called Controlled components
	supports instant input validation
	allow to enable or disable conditionnally buttons
	enforce input format
	
Example

	class NameForm extends React.Component {
		
		state:{email:''}
	
		handleChange=(event) => {
			this.setState({email:event.target.value})
		}
	
		render(){
			return (
				<form>
					<input type="text" value={this.state.email} onChange={this.handleChange}/>
				</form>
			)
		}
	}
	
Now we will add the search input. There is several way to do it

	have the input field write to the DOM (not the component)
	have the input field bind its value to a component state attribute	
	
Now add the search see the comit.

	Convert ListContacts to a controlled component with a search field

it seem conter intutive because we would expect this

	User type some input
	Ui change
	State change
	
but what's hapen is

	The user enters text into the input field.
	An event listener invokes the updateQuery() function on every onChange event.
	updateQuery() then calls setState(), merging in the new state to update the component's internal state.
	Because its state has changed, the ListContacts component re-renders.

here is how is our listcontact

	import React, { Component } from 'react';
	import PropTypes from 'prop-types'

	class ListContacts extends Component {
	  static propTypes = {
		contacts: PropTypes.array.isRequired,
		onDeleteContact: PropTypes.func.isRequired
	  }

	  state = {
		query: ''
	  }

	  updateQuery = (query) => {
		this.setState({ query: query.trim() })
	  }

	  render() {
		return (
		  <div className='list-contacts'>
			{JSON.stringify(this.state)}
			<div className='list-contacts-top'>
			  <input
				className='search-contacts'
				type='text'
				placeholder='Search contacts'
				value={this.state.query}
				onChange={(event) => this.updateQuery(event.target.value)}
			  />
			</div>
			<ol className='contact-list'>
			  {this.props.contacts.map((contact) => (
				<li key={contact.id} className='contact-list-item'>
				  <div className='contact-avatar' style={{
					backgroundImage: `url(${contact.avatarURL})`
				  }}/>
				  <div className='contact-details'>
					<p>{contact.name}</p>
					<p>{contact.email}</p>
				  </div>
				  <button onClick={() => this.props.onDeleteContact(contact)} className='contact-remove'>
					Remove
				  </button>
				</li>
			  ))}
			</ol>
		  </div>
		)
	  }
	}

	export default ListContacts
	
Notes 

	the value attribute is set on the <input> element. Our displayed value will always be the value in the component's state, making our state the "single source of truth."
	it is React that ultimately controls the value of our input form element => this is component a Controlled Component.

Let's add filtering. First install needed packages regex and sortby

	npm install --save escape-string-regexp sort-by
	npm run start
	
Here is the new file. See commit.

	https://github.com/udacity/reactnd-contacts-complete/commit/abd5fccf9a69546e75d9c178379d3ef92405719e

	import React, { Component } from 'react';
	import PropTypes from 'prop-types'
	import escapeRegExp from 'escape-string-regexp'
	import sortBy from 'sort-by'

	class ListContacts extends Component {
	  static propTypes = {
		contacts: PropTypes.array.isRequired,
		onDeleteContact: PropTypes.func.isRequired
	  }

	  state = {
		query: ''
	  }

	  updateQuery = (query) => {
		this.setState({ query: query.trim() })
	  }

	  render() {
		let showingContacts
		if (this.state.query) {
		  const match = new RegExp(escapeRegExp(this.state.query), 'i')
		  showingContacts = this.props.contacts.filter((contact) => match.test(contact.name))
		} else {
		  showingContacts = this.props.contacts
		}

		showingContacts.sort(sortBy('name'))

		return (
		  <div className='list-contacts'>
			<div className='list-contacts-top'>
			  <input
				className='search-contacts'
				type='text'
				placeholder='Search contacts'
				value={this.state.query}
				onChange={(event) => this.updateQuery(event.target.value)}
			  />
			</div>
			<ol className='contact-list'>
			  {showingContacts.map((contact) => (
				<li key={contact.id} className='contact-list-item'>
				  <div className='contact-avatar' style={{
					backgroundImage: `url(${contact.avatarURL})`
				  }}/>
				  <div className='contact-details'>
					<p>{contact.name}</p>
					<p>{contact.email}</p>
				  </div>
				  <button onClick={() => this.props.onDeleteContact(contact)} className='contact-remove'>
					Remove
				  </button>
				</li>
			  ))}
			</ol>
		  </div>
		)
	  }
	}

	export default ListContacts

	
Notes

	let showingContacts : let is like var. When declaring variables, you should declare them using the keywords in the order listed above. Declare your variables with const, first. If you find that you need to reassign the variable later, use let. There isn't a good reason to use the var keyword anymore for variable declaration. see http://udacity.github.io/frontend-nanodegree-styleguide/javascript.html
	new RegExp(escapeRegExp(this.state.query), 'i')
		escapeRegExp(this.state.query) : if there is a special caracter in the user input it should be treated as normal string exple "\ . $"
		'i' ignore case
	now the list that shown is showingContacts and not directly contacts anymore
	
Improving performance by adding object destructuring

	const { contacts, onDeleteContact } = this.props
	const { query } = this.state

	this.state.query will become query
	this.props.contacts will become contacts
	this.props.onDeleteContact will become onDeleteContact

Fething data from a database. There is several possibilities

	make an AJAX request inside of the render method
	make an AJAX request inside a Lifecycle event
	
make an AJAX request inside of the render method

	render(){
		fetchUser().then(user = > this.setState({
			name: user.name,
			age: user.age
		}))
		return (
		  <div>
			<p>Name: {this.state.name}</p>
			<p>Age: {this.state.age}</p>
		  </div>
		)
	}

This is a bad idea because 

	the render method needs to be free of side effects. The render method should be a pure function.
	it shouldn't make asynchronous call beacuse You don't have complete control over when the render method will be invoked
	it should only receive props and return UI descroption

make an AJAX request inside a Lifecycle event

	this is what we should do
	here we will use componentDidMount
	note all of the methods below call setState method when they finished
	
Lifecycle events are methods existing inside components that can be called when ... for the most common

	componentWillMount : component has been created and will be but is not yet inserted into the DOM
	componentDidMount : component has been created and has just been inserted into the DOM
	componentWillUnmount : component has not been removed from the DOM but will very soon.
	componentWillReceiveProps : component just receive new props
	
recap of all lifecycle events methods (more on this here : https://reactjs.org/docs/react-component.html#the-component-lifecycle)

	Adding to the DOM : These lifecycle events are called when a component is being added to the DOM:
		constructor()
		componentWillMount()
		render()
		componentDidMount()

	Re-rendering : These lifecycle events are called when a component is re-rendered to the DOM	
		componentWillReceiveProps()
		shouldComponentUpdate()
		componentWillUpdate()
		render()
		componentDidUpdate()
		
	Removing from the DOM : This lifecycle event is called when a component is being removed from the DOM
		componentWillUnmount()
	
here is how to use it
	
	import React, { Component } from 'react';
	import fetchUser from '../utils/UserAPI';

	class User extends Component {
	  constructor(props) {
		super(props)

		this.state = {
		  name: '',
		  age: ''
		}
	  }

	  componentDidMount() {
		fetchUser().then((user) => this.setState({
		  name: user.name,
		  age: user.age
		}))
	  }

	  render() {
		return (
		  <div>
			<p>Name: {this.state.name}</p>
			<p>Age: {this.state.age}</p>
		  </div>
		)
	  }
	}

	export default User;
	
Here is how should look our componentDidMount method

  componentDidMount() {
    ContactsAPI.getAll().then((contacts) => {
      this.setState({ contacts : contacts })
    })
  }
  
Because key end value are the same we can use this notation

	this.setState({ contacts })
	
instead of 

	this.setState({ contacts : contacts })
	
## React Router

We want 

	applications that download everything the user needs at once
	applications whose URL change depending on the data displayed (means user actions/choices should be visible in the URL)
	
This is what React Router does. 

	React Router turns React projects into single-page applications.
	It does this by providing a number of specialized components that 
		manage the creation of links
		manage the app's URL
		provide transitions when navigating between different URL locations
		
Training on React Router

	https://reacttraining.com/react-router/
	
Basically what we will do is 

	add a state attribute screen
	render the correct screen according to the state attribute
	
Note about the Short-circuit Evaluation Syntax. Here we used this

    {this.state.screen ==='list' && (<ListContacts onDeleteContact={this.removeContact} contacts={this.state.contacts}/>)}
    {this.state.screen === 'create' && (<CreateContact/>)}
	this is really just the logical expression &&
		
We could have used this with the same result

	if(this.state.screen ==='list'){<ListContacts onDeleteContact={this.removeContact} contacts={this.state.contacts}/>}
	if(this.state.screen === 'create') {(<CreateContact/>)}	
	
Now add the button to add contact screen

	https://github.com/udacity/reactnd-contacts-complete/commit/23a6a4dde977d7c18a3054a7b0b65f4fb4aad2ea
	Problem is using attribute screen state we stay on the same page when we press the back button
	
Install React Router

	npm install --save react-router-dom
	note also exist npm install --save react-router-native
	
now in index.js

	import router
	wrap your entire app with the BrowserRouter component
	
this is how your file should look like

	import React from 'react';
	import ReactDOM from 'react-dom';
	import App from './App';
	import registerServiceWorker from './registerServiceWorker';
	import './index.css';
	import { BrowserRouter } from 'react-router-dom'

	ReactDOM.render(<BrowserRouter><App /></BrowserRouter>, document.getElementById('root'));
	registerServiceWorker();
	
This alone will

	listen URLs
	notify components when URL changes
	possible with the history object : https://github.com/reacttraining/history
	
Let's look at BrowserRouter

	class BrowserRouter extends React.Component {
	  static propTypes = {
		basename: PropTypes.string,
		forceRefresh: PropTypes.bool,
		getUserConfirmation: PropTypes.func,
		keyLength: PropTypes.number,
		children: PropTypes.node
	  }

	  history = createHistory(this.props)

	  render() {
		return <Router history={this.history} children={this.props.children}  />
	  }
	}
	
BrowserRouter

	create a history object and then
	render a router based on this history object
	if you navigate using keyboard it also work
	
Behavior

	user click a link
	BrowserRouter is notifified
	BrowserRouter update the URL
	

Link component : With BrowserRouter we wont use <a> but <Link> instead, Link will convert to <a> in the DOM. Lets update ContactList

	import link
	replace a by Link
	remove onClick={this.props.onNavigate} because Link take care of this
	
This how you can declare a link

	<Link to="/about">About</Link>

or ... as you see its possible to pass a state to a link in a form of an object

	<Link to={{
	  pathname: '/courses',
	  search: '?sort=name',
	  hash: '#the-hash',
	  state: { fromDashboard: true }
	}}>
	  Courses
	</Link>

Route component : here is one

	<Route 
		path="/create"
		render={ui}
	/>

How it works

	if the path match the url then route render some ui
	if the path does not match the url then route does not render some ui
	instead of checking state, route check the url

if your path is http://localhost:3000/create it will match both paths

	path="/"
	path="/create"
	
to avoid this use exact keyword

	<Route 
		exact path="/"
		render={ui}
	/>

Serialize The Form Data

	that means adding user input values as a query string to the URL
	it is done by default onSubmit with htlm
	but we want to do this with javascript we will overide default behavior because we dont want to serialise to a string we want to serialise to an object
	for this we need to install form-serialize
	
install form-serialize

	npm install --save form-serialize
	
change 

	<form className='create-contact-form'>
	
to 

	<form onSubmit={this.handleSubmit} className='create-contact-form'>
	
implement method

	handleSubmit = (e) => {
		e.preventDefault()
		const values = serializeForm(e.target, { hash: true })
		console.log(values)
		if (this.props.onCreateContact)
		  this.props.onCreateContact(values)
	  }
	  
notes 

	e.preventDefault() will prevent default html serialisation
	e.target refers to all input fied of the form tree
	hash: true  means we want serialisation in a form of n object
	console.log(values) after clicking create this allow us to see what was the result of the serializeForm function
	
in app.js

  render() {
    return (
      <div>
        <Route exact path="/" render={() => (
          <ListContacts 
            contacts={this.state.contacts}
            onDeleteContact={this.removeContact} 
            />
        )}/>
       <Route path="/create" component={CreateContact}/>
      </div>
    )
  }
  
using render or component Route props

	component does not allow us to pass CreateContact props
	render does allow to pass props to our components (here ListContacts )
	
app.js after adding contact to db

	import React, { Component } from 'react';
	import { Route } from 'react-router-dom'
	import ListContacts from './ListContacts'
	import CreateContact from './CreateContact'
	import * as ContactsAPI from './utils/ContactsAPI'

	class App extends Component {
	  state = {
		contacts: []
	  }
	  componentDidMount() {
		ContactsAPI.getAll().then((contacts) => {
		  this.setState({ contacts })
		})
	  }
	  removeContact = (contact) => {
		this.setState((state) => ({
		  contacts: state.contacts.filter((c) => c.id !== contact.id)
		}))

		ContactsAPI.remove(contact)
	  }

	  createContact(contact) {
		ContactsAPI.create(contact).then(contact => {
		  this.setState(state => ({
			contacts: state.contacts.concat([ contact ])
		  }))
		})
	  }

	  render() {
		return (
		  <div>
			<Route exact path='/' render={() => (
			  <ListContacts
				onDeleteContact={this.removeContact}
				contacts={this.state.contacts}
			  />
			)}/>
			<Route path='/create' render={({ history }) => (
			  <CreateContact
				onCreateContact={(contact) => {
				  this.createContact(contact)
				  history.push('/')
				}}
			  />
			)}/>
		  </div>
		)
	  }
	}

	export default App;
	
Notes

	history.push('/') allow us to move back to the list screen after the contact has been added
	
# React and Redux

	https://classroom.udacity.com/nanodegrees/nd019/parts/7b1b9b53-cd0c-49c9-ae6d-7d03d020d672
	
Redux 

	is also a state management system 
	Redux can (Believe it or not) be used with projects other than React!
	is a JavaScript library used to manage an application’s front-end state.
	
it complete React when

	2 components rely on the piece of state : shared state
	store data : single source of truth
	
share state

	You could hoist that state up to a nearby parent component -- but if that parent component is several components up the component tree, passing state as a prop one-by-one down the tree can become tedious pretty quickly. What’s more: components that live between the parent component and the child component may not even need access to that state!
	
	Redux does implement a single state tree. With all of the data in one location and maintained through one interface, it makes debugging and working with data more straightforward.

store data : single source of truth

	 state in a Redux app is read-only; that is, Redux state is immutable. 
	 React components cannot write directly to Redux state. 
	 React components they must request access to that data
	 React components  express intent to update the state. 
	 only pure functions called reducers have the ability to change state. 
	 you always know just where state is coming from (the store)
	 uses unidrectional data flow like in React
	 
Redux can help complex application managing

	form state (like the Contacts app from React Fundamentals)
	Server responses
	Cached data (e.g. users)
	Local data not yet persisted to a server
	Active routes
	Currently-selected tabs
	Pagination controls
	
Redux store and React component

	You should defined yourself which state should live in the react store and which in the react state. 
	There is no clear rule for that. But we can say
	
Use Redux store when 

	state matter globally or (Share states / Global states)
	state is mutated in complex ways (Caching) = the operation to get that state was expensive exemple db call
	Examples : 
		Cached users
		A draft of an email
	
Use React when (everything else)

	state does not matter globally and
	state is not mutated in complex ways
	Examples : 
		Form input
		Current tab selected
		Dropdown open/closed status
	

Redux store

	is updated using pure functions
	
Pure functions

	Return one and the same result if the same arguments are passed in
	Depend solely on the arguments passed into them (they should never depend on the db, the dom, ...)
	Do not produce side effects (do not update db, dom, ..., network request, mutating component state)
	
Impure function 

	const tipPercentage = 0.15;
	const calculateTip = cost => cost * tipPercentage;
	it relies on a variable (tipPercentage) that lives outside the function to produce that value
	 Using impure functions isn’t necessarily “bad programming.” For example, a button with an event handler that updates the DOM wouldn’t be a great use case for pure functions because the event handler is updating the DOM (i.e., producing a side effect!).
	
can be converted to a pure function

	const calculateTip = (cost, tipPercentage = 0.15) => cost * tipPercentage;
	now tipPercentage lives inside.
	
other impurefunction squareItems

	function square(n){ //This function is pure
		return n * n  
	}
	function squareItems(arr){
		for(let i=0; i<arr.lenght;i++){
			arr[i]=square(arr[i])
		}
		return arr;
	}
	
should be converted in ... and return a new array without affecting the one given in parameter

	function squareItems(arr){
		return arr.map(square)
	}
	
Side effects ewample

	Making HTTP calls
	Mutating external state
	Retrieving today’s date
	Math.random()
	Printing a message to the console
	Adding to a database
	
Reduce method

	 takes in a large amount of data but returns a single value. 
	 
Example

	const iceCreamStats = [
	  {	name: 'Amanda',	gallonsEaten: 3.8 },
	  {	name: 'Geoff',gallonsEaten: 5.2   },
	  {	name: 'Tyler', gallonsEaten: 1.9  },
	  {	name: 'Richard', gallonsEaten: 7923 }
	];

	iceCreamStats.reduce( (accumulator, currentValue) => {
	  return accumulator + currentValue.gallonsEaten;
	}, 0);

Note about this

	0 is the starting value
	(accumulatatedValue, currentValue) are the arguments of the callback function
	
arguments of the callback function will be

	(0, {name: 'Amanda', gallonsEaten: 3.8 }) for the first call
	(0+3.8, {	name: 'Geoff',gallonsEaten: 5.2   }) for the second call
	etc...
	
from the exercices I've not managed. Exercice1

/* Using .reduce()
 *
 * Using the musicData array and .reduce():
 *   - Return the total number of sales
 *   - Store the returned data in a new 'totalAlbumSales' variable
 *
 * Notes:
 *   - Do not delete the 'musicData' variable
 *   - Do not alter any of the 'musicData' content
 *   - Do not format the sales number; leave it as a long string of digits
 */

const musicData = [
    { artist: 'Adele', name: '25', sales: 1731000 },
    { artist: 'Drake', name: 'Views', sales: 1608000 },
    { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
    { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
    { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
    { artist: 'Original Broadway Cast Recording', name: 'Hamilton: An American Musical', sales: 820000 },
    { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
    { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
    { artist: 'Rihanna', name: 'Anti', sales: 603000 },
    { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
];

const totalAlbumSales=musicData.reduce((accumulator, currentValue)=>(
        return accumulator + currentValue.sales;
    ), 0);
	

Exercice2
	
/* Combining .filter() and .reduce()
 *
 * Using the musicData array, filter(), and reduce():
 *   - Filter the musicData array down to just the albums that have a
 *     combined artist + name string length of less than 25 characters
 *     (for example, looking at the first album it would be "Adele25" which 
 *     has a length of 7, so it should be included)
 *   - Then, on the array returned from filter(), call reduce()
 *   - The value returned reduce() returns the total number of sales
 *   - Store that returned number in a new totalAlbumSales variable
 *
 * Note:
 *   - You can chain the operations!
 *   - Do not delete the musicData variable
 *   - Do not alter any of the musicData content
 *   - Do not format the sales number; leave it as a long string of digits
 */

const musicData = [
    { artist: 'Adele', name: '25', sales: 1731000 },
    { artist: 'Drake', name: 'Views', sales: 1608000 },
    { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
    { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
    { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
    { artist: 'Original Broadway Cast Recording', name: 'Hamilton: An American Musical', sales: 820000 },
    { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
    { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
    { artist: 'Rihanna', name: 'Anti', sales: 603000 },
    { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
];

const totalAlbumSales = musicData
.filter(album => album.name.length + album.name.length <= 25 )
.reduce((accumulator, currentValue)=>(return accumulator + currentValue.sales), 0)

Exercice3

	/* Popular Ice Cream Totals Quiz
	 *
	 * Using the data array and .reduce():
	 *   - Return an object where each property is the name of an ice cream flavor
	 *     and each value is an integer that's the total count of that flavor
	 *   - Store the returned data in a new iceCreamTotals variable
	 *
	 * Notes:
	 *   - Do not delete the data variable
	 *   - Do not alter any of the data content
	 */

	 const data = [
		 { name: 'Tyler', favoriteIceCreams: ['Strawberry', 'Vanilla', 'Chocolate', 'Cookies & Cream'] },
		 { name: 'Richard', favoriteIceCreams: ['Cookies & Cream', 'Mint Chocolate Chip', 'Chocolate', 'Vanilla'] },
		 { name: 'Amanda', favoriteIceCreams: ['Chocolate', 'Rocky Road', 'Pistachio', 'Banana'] },
		 { name: 'Andrew', favoriteIceCreams: ['Vanilla', 'Chocolate', 'Mint Chocolate Chip'] },
		 { name: 'David', favoriteIceCreams: ['Vanilla', 'French Vanilla', 'Vanilla Bean', 'Strawberry'] },
		 { name: 'Karl', favoriteIceCreams: ['Strawberry', 'Chocolate', 'Mint Chocolate Chip'] }
	 ];


	const iceCreamTotals=something I dont know

Redux core is composed of

	actions and action creators : it is the equivalent of html events or your eventBus events
	reducers : read an action and update the store state
	store : 
		houses the application state, 
		it request its change by sending an action
		it update its state by calling a reducer using a given action
	
Redux action

	is a javascript object with
	a type property
	the value is a string in capital that must describe what took place
	and other data as you wish
	
Example

	{
		type: 'EDIT_USER'
		id: 917
	}
	
Example 2

	const LOAD_PROFILE = 'LOAD_PROFILE';

	const myAction = {
	  type: LOAD_PROFILE
	};
	
Redux action creator

	are function that return an action
	are pure functions free of side effect
	
Example

	const submitUser = user => ({
	  type: SUBMIT_USER,
	  user
	});
	
Create udacimeals project

	cd /c/ProgrammingProjects/JavascriptProjects/
	create-react-app udacimeals
	cd udacimeals/
	npm start
	
If npm start gives you a "something is already running on port 3000" error

	netstat -ano | findstr :3000
	this will gives a result that look like that :  TCP    0.0.0.0:3000           0.0.0.0:0              LISTENING       2404
	take the last number and do
	taskkill /PID 2404 /F or 
	taskkill //PID 2404 //F (if you got an error before related to git)
	
Add the starter code shown in the "Project Skeleton commit"

	https://github.com/udacity/reactnd-udacimeals-complete/commits/master
	
There is 2 way to change the React store

	Adding a new recipe
	Removing a food item from the calendar
	
what type of data must be the state ? an array, an object ? mutiple objects ???

	it can be any format but you have the think very carrefully the one that suits your needs best before writting any reducers
	
Reducers

	creates the initial state of an application
	tell  how the actual state should change
	must be a pure function.
	must return the state in the decided format
	is just a function with 2 arguments
		current state : the function take it and then must return it
		action that just happenned : the action is used to determinate what change should be made to the state
		
Reducer example (not really correct - see next example)

	function reducer (state, action) {
	  if(action.type=='ADD_FLAVOR'){
		//change app state info
	  }
	  return state;
	}

Reducer example (correct one)

	function reducer (state, action) {
	  if(action.type=='ADD_FLAVOR'){
		//copy the state
		//modify the copy of the state
		//return the copy of the state
	  }
	  return state;
	}
	
Another example of this

	function reducer (state, action) {
	  switch (action.type) {
		case 'SUBMIT_USER' :
		  return Object.assign({}, state, {
			user: action.user
		  })
	  }
	}
	
Same thing using the object spread syntax

	function reducer (state, action) {
	  switch (action.type) {
		case 'SUBMIT_USER' :
		  return { ...state, 
			user: action.user
		  })
	  }
	}

See this commit

	https://github.com/udacity/reactnd-udacimeals-complete/commit/9303a724d8fe4388b7c9c2bdbeec8dd9339ad9c1
	
Another example exercice

	/* Create A Reducer
	 *
	 * You need to create a reducer called "appReducer" that accepts two arguments:
	 * - First, an array containing information about ice cream 
	 * - Second, an object with a 'DELETE_FLAVOR' `type` key
	 * (i.e., the object contains information to delete the flavor from the state)
	 *
	 * The action your reducer will receive will look like this:
	 * { type: 'DELETE_FLAVOR', flavor: 'Vanilla' }
	 *
	 * And the initial state will look something like this (as such, refrain 
	 * from passing in default values for any parameters!):
	 * [{ flavor: 'Chocolate', count: 36 }, { flavor: 'Vanilla', count: 210 }];
	*/
	
	const reducer =(state, action) => (
	  switch (action.type) {
		case 'DELETE_FLAVOR' :
		  return 
			state.filter(obj => obj.flavor !== action.flavor);
		  default: 
			return state;
	  }
	)

	const result = appReducer (
		[{ flavor: 'Chocolate', count: 36 },
		{ flavor: 'Vanilla', count: 210 }], 
		{type:'DELETE_FLAVOR', flavor:'Vanilla'});
	
	console.log(result);
	
the reducer create the initial state of the app using the ES6’s default parameters feature.

	function myReducer (state = initialState, action) {
	  // ...
	}
	that means if the state is undefined it will use initialState otherwise it use it as it is
	
To create a store

	const immaStore = Redux.createStore(<reducer>);
	
A store have only a few methods

	immaStore.getState() return the current state that's in the store
	immaStore.dispath() takes an action object and will pass it to the reducer function
	immaStore.subscribe(<listener function>) takes a function that will be called when the state changes
	
In the terminal install redux

	npm install redux
	npm run start
	
See commit "Create your first store"

	https://github.com/udacity/reactnd-udacimeals-complete/commits/master
	
Redux DevTools

	allows you to see the current state of your store
	allows you to see how the state changes based on actions that are dispatched
	
To make it work you have to add a second arg to the createStore method

	const store = createStore(
	reducer, 
	windows.__REDUX_DEVTOOLS_EXTENSION__ && windows.__REDUX_DEVTOOLS_EXTENSION__()
	)

See commit "Redux DevTools"

	I don't manage to make redux devtoo show the inspector with the different state diff (previous difference with current state)
	I dont see tabs : action, state, diff, test
	
Here is our src/components/App.js see commit "All together+"
	
	import React, { Component } from 'react'
	import { addRecipe } from '../actions'

	class App extends Component {
	  state = {
		calendar: null
	  }
	  componentDidMount () {
		const { store } = this.props

		store.subscribe(() => {
		  this.setState(() => ({
			calendar: store.getState()
		  }))
		})
	  }
	  submitFood = () => {
		this.props.store.dispatch(addRecipe({
		  day: 'monday',
		  meal: 'breakfast',
		  recipe: {
			label: this.input.value
		  },
		}))

		this.input.value = ''
	  }
	  render() {
		return (
		  <div>
			<input
			  type='text'
			  ref={(input) => this.input = input}
			  placeholder="Monday's Breakfast"
			/>
			<button onClick={this.submitFood}>Submit</button>

			<pre>
			  Monday's Breakfast: {this.state.calendar && this.state.calendar.monday.breakfast}
			</pre>
		  </div>
		)
	  }
	}
	export default App
	
	
Notes : 

	although we are using React store, our component has its own state anyway. We update its state using the store, that's all.
	The ref attribute is a special attribute provided by React that allows you to access the DOM. More here : https://reactjs.org/docs/refs-and-the-dom.html
	redux comes with a library called React-Redux that can simplify this code by using bindings
	
## React-Redux

It is working but something is actually ugly and that is those lines

	store.subscribe(() => {
	calendar: store.getState()
	this.props.store.dispatch(addRecipe({
		
As you can see ...

	we ended up passing the store to the main component in order to get access to dispatch(), getState(), and subscribe()
	It's fine for small app but not for big ones. But for big app with nested components, each component of the tree should receive the store props from its parent (see Props threading)
	To avoid this we can use React-Redux provider
	
Props threading

	means passing to each component of the tree a props property in order to reach a specific child
	is an opening door to errors
	
React-Redux provider

	is meant to avoid Props threading
	makes it possible for Redux to pass data from the store to any React components that need it. 
	uses React’s "context" feature to make this works.
	Components that need access to the store "connect" to it using the connect() methd.
	
install React-Redux

	npm install --save react-redux
	npm run start
	
see commit 

	Using the Provider: https://github.com/udacity/reactnd-udacimeals-complete/commits/master
		
currying

	is when you call a function without all its arguments and it return 
	a function waiting for the next argument
	is a dynamic technique that let you gives some data to a function but wait until some later point to do the full call

example

	function plate(vegetables) {
	  return function fruitFunc (fruit) {
		return `I ate a plate of ${vegetables} and ${fruit}!`;
	  }
	}

	const sentence = plate('corn')('apples');
	
connect method

	utilizes a technique in functional programming called currying
	this technique is possible because of javascript ability to return a function. That means a function that is not executed yet.
	in Java to achieve the same thing we would have to create an object with a function that return another object with the second function.
	gives possibility to pass specifics parts of the app state to a component
	gives possibility to pass actions to a component
	those app state and actions will then be available inside the component as a props
	
how it is used

	connect(mapStateToProps, mapDispatchToProps)(MyComponent)
	MyComponent is the component in which you want to get the store state
	MyComponent is the component from which you want to dispatch actions
	mapStateToProps() is a function that receives the current store
	mapDispatchToProps() allows you wrap action creators inside of dispatch
	
mapStateToProps()

	mapStateToProps(state, [ownProps])
	state is the store state
	[ownProps] an optional ownprops argument. gives us access to props passed into to component. A great place to use ownProps is when filtering some data.
	The results of mapStateToProps is a plain object that will be merged into the component’s props.”
	
mapStateToProps() example

	import { connect } from 'react-redux';

	const User = ({ name, age }) => {
	  // ...
	};

	const mapStateToProps = (state, props) => ({
	  name: state.user.name,
	  age: state.user.age
	});

	export default connect(mapStateToProps)(User);
	
[ownProps] use example 

	<ConnectedComponent firstName={'Harper'} lastName={'Lee'} />
	const mapStateToProps = (state, ownProps) => ({
	  occupation: state.occupation,
	  userInfo: `${ownProps.firstName} ${ownProps.lastName}: ${state.occupation}.`
	});
	
	export default connect(mapStateToProps)(MyComponent);
	
Another example with filtering

	const mapStateToProps = (state, ownProps) => ({
	  photos: state.photos.filter(photo => photo.user === ownProps.user)
	});

	export default connect(mapStateToProps)(MyPhotos);

	Here we have a component MyPhotos that, upon login, renders an index of all the user's photos. The logged-in user is stored in another location in the application, and is passed down to the MyPhotos component as a prop. 
	
mapDispatchToProps()

	When you connect a component, that component will automatically be passed Redux's dispatch() method without having to use mapDispatchToProps.
	mapDispatchToProps allow to clean up your code by binding dispatch() to your action creators before they ever hit your component
	
without mapDispatchToProps()

	import React, { Component } from 'react';
	import { connect } from 'react-redux';
	import { updateName } from './actions';

	class User extends Component {
	  state = { name: '' }
	  handleUpdateUser = () => {
		this.props.dispatch(updateName(this.state.name))
	  }
	  render () {
		// ...
	  }
	}

	export default connect()(User);
	
with mapDispatchToProps()

	import React, { Component } from 'react';
	import { connect } from 'react-redux';
	import { updateName } from './actions';

	class User extends Component {
	  state = { name: '' }
	  handleUpdateUser = () => {
		this.props.boundUpdateName(this.state.name)
	  }
	  render () {
		// ...
	  }
	}

	const mapDispatchToProps = dispatch => ({
	  boundUpdateName: (name) => dispatch(updateName(name))
	});

	export default connect(null, mapDispatchToProps)(User);
	
Note from the course about the code just above

	"mapDispatchToProps() is completely optional and I'm not convinced it makes things that much cleaner, but it is nice to know about."
	
See commit "mapDispatchToProps" the component App will have accessible at props the following data

	day
	meals
	selectRecipe
	remove

## Redux store architecture

Reducer Composition : how can we handle the case when there is several reducer ?? The createStore() method accept only one. Example : 

	function users (state = {}, action) {
	  switch (action.type) {
		case 'ADD_USER' :
		  return {};
		case 'REMOVE_USER':
		  return {};
		default :
		  return state;
	  }
	}
	
What if we wanted to add books to our Redux store? 

	function users (state = {}, action) { 
	  // ... 
	}

	function books (state = {}, action) { 
	  // ... 
	}
	
Up until this point	state tree has been pretty simple 
	
	const initialState = {
	  data: [],
	  isFetching: false,
	  error: ''
	}

As our app scales, we'll want to create more than just one reducer, we want to go from the state shown above to something more like this:	

	{
	  users: {},
	  modal: {},
	  posts: {},
	  replies: {},
	  listeners: {}
	}
	
This is achieved using the combineReducers() method.

	is a helper function provided by Redux that turns several reduced functions into a single reducing function. 
	We then pass this single "root reducer" into createStore() to create the application's store
	takes in an object as an argument
	return a single reducer that can be used to create a store
	
This how will look our reducer

	// reducers/root_reducer.js

	import { combineReducers } from 'redux';

	function users (state = {}, action) {
	  // ...
	}

	function books (state = {}, action) {
	  // ...
	}

	export default combineReducers({
	  users,
	  books,
	});
	
This is how look our createStore method

	import rootReducer from '../reducers/root_reducer';

	const store = createStore(rootReducer)
	console.log(store.getState()) // { users: {}, books: {} }	
	
Check this commit

	combineReducers() : https://github.com/udacity/reactnd-udacimeals-complete/commits/master
	
Notes in src/reducers/index.js this line ... means ...

	const { day, recipe, meal } = action
	grab the day, meal, recipe from the action

Normalisation

	is a way to optimize your store for better performance.
	lead to more efficient and consistent queries.
	has rules
		- Do not duplicate data, use references instead. If data lives in multiple places, you have no single source of truth, and you waste resources trying to keep the data in sync with each other.
		- Keep your store as shallow as possible. Nested data makes reducer logic more complicated (trying to update deeply nested data can get slow and complex quickly).
		
Do not duplicate data, use references instead. Example of something you should do.

	const people = {
	  kassidi: {
		name: 'Kassidi Henry',
		age: 24,
		favoriteMovie: 'Remember the Titans'
	  },
	  tyler: {
		name: 'Tyler McGinnis',
		age: 25,
		favoriteMovie: 'Fatigue: A JavaScript Story'
	  },
	  jake: {
		name: 'Jake Lingwall',
		age: 26,
		favoriteMovie: 'Casablanca'
	  },
	}

	const friends = ['kassidi', 'jake'] //This is the reference
	
how to use this : if I need to create a new array which references all of my friends, the code is simply:
	
	friends.map((friend) => people[friend])
	
Keep your store as shallow as possible. Example of something you should NOT do.

	const books = {
	  fiction: {
		fantasy: {
		  0: {
			title: 'Harry Potter and the Nested Data',
			author: 'JK Rowling'
		  }
		},
		romance: {},
		scifi: {}
	  },
	  nonFiction: {}
	};

If we want to create a new object (because we never want to modify the original state), but alter the title of Harry Potter, our reducer function will have to look something like this:

	function books (state, action) {
	  const { bookType, genre, id, title } = action
	  if (action.type = CHANGE_TITLE) {
		return {
		  ...state,
		  [bookType]: {
			...state[bookType],
			[genre]: {
			  ...state[bookType][genre]: {
				[id]: {
				  ...state[bookType][genre][id],
				  title,
				}
			  }
			}
		  }
		}
	  }

	  return state
	}
	
Note about this last example : 

	Look at that nested structure -- yikes! You get the picture. Not only is this extremely inefficient because we're cloning state with every spread operator (...), it's also extremely difficult to reason about -- both as a writer or reader of that code.
	
Now finish the app

	npm install react-icons
	npm run start
	see commit "add Calendar grid"
	
Get a Edamam API Keys

	go to https://developer.edamam.com/edamam-recipe-api
	register for the free plan
	see my local file F:\Mes Documents\Contacts - Organismes\Edamam Free Recipes
	
Once you have registered, place your unique ID and API key in a .env file located in the root directory of your project. Finish the app again

	npm install react-loading react-modal
	npm run start
	
See commit "Shopping List"

	https://github.com/udacity/reactnd-udacimeals-complete/commits/master
	
Middleware

	intercept a process or request and redirect it
	produce some side effects
	lives between dispatching of actions and reducers
	is what we must use for asynchronous call
	without middleware the redux store can only support synchronous flow of data
	
Example of middleware side effects

	Logging state Console.log()
	Making an asynchronous HTTP request
	Redirecting the action (e.g., to another piece of middleware)
	Running some code during the dispatch
	Dispatching supplementary actions
	
Where does Middleware Go in a Redux App?

	in the createStore method
	store.createStore(reducer, [enhancer])
	using the Redux function applyMiddleware() as the [enhancer]
	applyMiddleware() can accept multiple arguments, so if needed, we can apply more than one middleware to an app. 

In our app we will use middleware to log the state before and after dispatching of actions

	see commit "Add middleware logger"
	C:\ProgrammingProjects\JavascriptProjects\udacimeals
	https://github.com/udacity/reactnd-udacimeals-complete/commits/master
	
This was a custom logger but redux has its own good library

	npm install --save redux-logger
	https://www.npmjs.com/package/redux-logger
	The redux-logger package comes with default options out-of-the-box, but feel free to add further customizations as needed! https://github.com/evgenyrodionov/redux-logger#options
	
Thunk

	allow to making an asynchronous HTTP request using middleware.	we want to make a request and only dispatch an action when the request is resolved finished
	allow to write action creator that return a function rather than an object
	allow middleware to intercept action creator returned function before dispatching the action
	its a wrapper for the store dispatch method
	allow to dispatch only if a certain condition is met (e.g., a request is resolved).
	
Install thunk

	npm install --save redux-thunk
	
Thunk Action Creator Example

	// store.js

	import { createStore, applyMiddleware } from 'redux';
	import thunk from 'redux-thunk';
	import rootReducer from '../reducers/root_reducer';

	const store = () => createStore(rootReducer, applyMiddleware(thunk));

	export default store;	

let's say that the HTTP request looks like the following:
 
	// util/todos_api_util.js
	export const fetchTodos = () => fetch('/api/todos');

Since thunk middleware allows us to write asynchronous action creators that return functions rather than objects, our new action creator can now look like:

	// actions/todo_actions.js

	import * as TodoAPIUtil from '../util/todo_api_util';

	export const RECEIVE_TODOS = "RECEIVE_TODOS";

	export const receiveTodos = todos => ({
	  type: RECEIVE_TODOS,
	  todos
	});

	export const fetchTodos = () => dispatch => (
	  TodoAPIUtil
		  .fetchTodos()
		  .then(todos => dispatch(receiveTodos(todos)))
	);
	
Notes about this

	receiveTodos() is an action creator that returns an object, with a type key of RECEIVE_TODOS along with the todos payload.
	fetchTodos(), on the other hand, allows us to return a function. Here, we first make the HTTP request from TodoAPIUtil. By setting up a Promise, the action to receive all to-do items is dispatched only when the original request is resolved.
	
Here is a snippet of thunk middleware's code

	function createThunkMiddleware(extraArgument) {
	  return ({ dispatch, getState }) => next => action => {
		if (typeof action === 'function') {
		  return action(dispatch, getState, extraArgument);
		}

		return next(action);
	  };
	}

	const thunk = createThunkMiddleware();
	thunk.withExtraArgument = createThunkMiddleware;

	export default thunk;
	
As you can see

	thunk middleware intercepts actions of the type function before the dispatch is generated. 
	In addition to dispatch, getState is also passed in as a second argument;
	this allows thunk action action creators to read the current state of the store.
	
App Organization by Capability ("Type")

	Frontend
	   - Components
		  - component1.js
		  - component2.js
		  - component3.js
	   - Actions
		  - action1.js
		  - action2.js
	   - Reducers
		  - reducer1.js
	   - Util
	   - Store
	if we wanted to import all actions into a component, we can get them all in a single import!
	
Organization by Feature

	- nav
	   - actions.js
	   - index.js
	   - reducer.js

	- dashboard
	   - actions.js
	   - index.js
	   - reducer.js

	All in all, there is no "right way" to split things up, though there are conventions we can practice to help manage the complexity of Redux. Considering the features, scale, and dependencies in your app, feel free to choose whichever structure makes the most sense.
	
More redux middleware here

	https://github.com/xgrommx/awesome-redux
	https://github.com/reactjs
	

# React Native Course

setState() reconcialition

	merge the object passed to setState() into the current state of the component. This is called recocialiation.
	React recocialiation construct a new tree of React elements then "diff" it against the previous element tree in order to figure out how the UI should change in response to the new state. By doing this, React will know the exact changes which occurred, and is able to minimize its footprint on the UI by only making updates where absolutely necessary.
	
how to develop for both platforms ?

	iOS uses Xcode
	Android uses Android Studio
	instead of copy pasting code in each you can use Create React Native App
	Expo together with Create React Native App is the fastest way to get up and running, but if you're looking to integrate React Native into an existing app have a look at "Building Projects with Native Code" https://facebook.github.io/react-native/docs/getting-started.html
	
Create React Native App

	pro : minimizes the amount of time it takes to create a "hello world" application
	con :  if you need to build your own bridge between React Native and some native API that Create React Native App doesn't expose (which is pretty rare), Create React Native App won't work.
	
Install Create React Native App

	npm install -g create-react-native-app
	
Expo service

	makes React Native easier by making you avoid touching native code (Swift, ObjectiveC, java)
	allow you access to native code like Geolocalisation etc
	was created by old facebook team
	Expo team created "Create React Native App"
	
Install Create React Native App and Expo

	on your computer :  npm install -g create-react-native-app
	on your device :
		Expo on Google Play (Android)
		Expo on the App Store (iOS)
		
Then create your app

	cd /c/ProgrammingProjects/JavascriptProjects/
	create-react-native-app udacifitness
	
This gave me this error

	*******************************************************************************
	ERROR: npm 5 is not supported yet
	*******************************************************************************

	It looks like you're using npm 5 which was recently released.

	Create React Native App doesn't work with npm 5 yet, unfortunately. We
	recommend using npm 4 or yarn until some bugs are resolved.

	You can follow the known issues with npm 5 at:
	https://github.com/npm/npm/issues/16991

	*******************************************************************************	
	
That's why i did 

	npm install -g npm@4.6.1
	npm install -g create-react-native-app
	create-react-native-app udacifitness	
	cd udacifitness
	subl .
	npm start
	solve any error appearing here after the QR code (that was the reason why my debbuger wasn't working, it seems)
	open expo app on your phone
	scan the QR code
	
npm start should have show me the following messages but I didn't get them

	press a to open Android device or emulator
	press i to open iOS device or emulator
	press q to display QR code
	press r to restart packager
	press R	to restart packager and clear cache
	press d to toggle developpement mode. (current mode: developpement)
	
Here is a link to the github project 

	https://github.com/udacity/reactnd-UdaciFitness-complete
	best way to follow is by cloning the repo to see easily which branch to compare
	also check my local version C:\ProgrammingProjects\JavascriptProjects\udacifitness
	
To update you phone page
	
	save your code. it should reload the page (this one did not worked for me)
	go on the Expo notification and click refresh
	shake your phone, it will open a menu, click refresh
	
Export shake menu

		refresh (this only possible because our code is javascript, with native apps the code must be compiled and that makes it impossible )
		etc..
		debug remote (that's the option we are interested in, I don't manage to have)
		toggle element inspector
			
On the phone

	select "debug remote"
	this open a tab in your browser with http://localhost:19001/debugger-ui
	you can now open the chrome dev tool(like we did before with react js)
		
If you want to debug you app

	you need to attach the debugger by using the keyword "debugger"
	once done save
	the app restart and stop on the debugger keyword (I've not managed that)
	then on the chrome dev tool source tab, open the right panel 
	you should be able the step your program
	
Here is how to do in App.js

	export default class App extends React.Component {
	  componentDidMount(){
		console.log('Before')
		debugger
		console.log('After')	
	  }

	  render() {
		return (
		  <View style={styles.container}>
			<Text>Opening up App.js to start working on your app!</Text>
			<Text>Changes you make will automatically reload.</Text>
			<Text>Shake your phone to open the developer menu.</Text>
		  </View>
		);
	  }
	}

toggle element inspector

	clic on Expo "toggle element inspector"
	then click on an element (view) of the app
	this show you style, margins etc...
	
indent/format sublime javascript

	Edit > Line > Reindent
	
If you can make emulators works use those shortcut to debug an refresh

	To Debug : All you have to do is shake your phone, or press:

		Ctrl+D in the iOS simulator
		Ctrl+M in the Android simulator

	To Refresh : To refresh the app, just:

		Double-tap “R” on your keyboard (if using the simulator)
		Shake the phone, then select “Refresh”
	
Comparaison on Web app, Android apps, iOS apps. User experience will be different because of the differents technologies used. Here are where are the differences

	animations(button effects, screen transitions, visual feedback)
	navigation(router)
	
On web

	animations are not really important
	navigation router is not a stack
	design
	only clicks

On Android

	animations are important
	navigation 
		router is a stack with screens that can be pushed and popped
		Android devices have access to a navigation bar at the bottom of the screen, which allows users to go back to the previous screen
		Android apps include tab bars at the top of the app's screen, allowing for convenient access to different portions of the app
		see ReactNative tabNavigator
	design guidelines are Google's Material Design : https://material.io/guidelines/material-design/introduction.html
	not only clicks, also gestures
	
On iOS

	animations are important
	navigation 
		router is a stack with screens that can be pushed and popped	
		iOS devices have NO access to a navigation bar. You must create one yourself
		iOS apps include tab bars at the bottom of the app's screen, allowing for convenient access to different portions of the appsee ReactNative tabNavigator
	design guidelines are  Apple's Human Interface Design : https://developer.apple.com/ios/human-interface-guidelines/overview/themes/
	not only clicks, also gestures
	
ReactJs vs ReactNative

	ReactJs
		<div> and <span> tags to define sections or to contain other elements
		text has no tag
		
	ReactNative
		<View> tags to define sections or to contain other elements
		<Text> tags to define text
		
ReactNative Vector Icons

	they are built-in if you used create-react-native-app
	you can find the full list here : https://expo.github.io/vector-icons/
	
not only clicks, also gestures = touchable. Here are a React Native overview

	TouchableHightlight : transform from its primary color to another color when you press on it
	TouchableNativeFeedback : only supported on Android not iOS. It gives the button a Ripple effect.
	TouchableOpacity : transform the background opacity to nearly transparent
	TouchableWithoutFeedback : a way to disable any feedback on a view
	
Example of TouchableHightlight use

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			TouchableHighLight, 
			TouchableNativeFeedback, 
			TouchableOpacity, 
			TouchableWithoutFeedback
		} from 'react-native'


	export default class App extends React.Component {
		handlePress=()=>{
			alert('hello')
		}

	  render() {
		return (
		  <View style={style.container}>
			<TouchableHighLight style={style.btn} onPress={this.handlePress} underlayColor='#d4271b'>
				<Text style={style.btnText}>Touchable HighLight</Text>
			</TouchableHighLight>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}

Example of TouchableOpacity use

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			TouchableHighLight, 
			TouchableNativeFeedback, 
			TouchableOpacity, 
			TouchableWithoutFeedback
		} from 'react-native'


	export default class App extends React.Component {
		handlePress=()=>{
			alert('hello')
		}

	  render() {
		return (
		  <View style={style.container}>
			<TouchableOpacity style={style.btn} onPress={this.handlePress}>
				<Text style={style.btnText}>Touchable HighLight</Text>
			</TouchableOpacity>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}
	
Example of TouchableWithoutFeedback use

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			TouchableHighLight, 
			TouchableNativeFeedback, 
			TouchableOpacity, 
			TouchableWithoutFeedback
		} from 'react-native'


	export default class App extends React.Component {
		handlePress=()=>{
			alert('hello')
		}

	  render() {
		return (
		  <View style={style.container}>
			<TouchableWithoutFeedback  onPress={this.handlePress}>
				<View style={style.btn}>
					<Text style={style.btnText}>Touchable HighLight</Text>
				<View>
			</TouchableWithoutFeedback>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}
	
Example of TouchableNativeFeedback use

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			TouchableHighLight, 
			TouchableNativeFeedback, 
			TouchableOpacity, 
			TouchableWithoutFeedback
		} from 'react-native'


	export default class App extends React.Component {
		handlePress=()=>{
			//alert('hello')
		}

	  render() {
		return (
		  <View style={style.container}>
			<TouchableNativeFeedback  
				background={TouchableNativeFeedback.SelectableBackground()}
				onPress={this.handlePress}>
					<View style={style.btn}>
						<Text style={style.btnText}>Touchable HighLight</Text>
					<View>
			</TouchableNativeFeedback>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}

Notes : 

	we use onPress instead of onClick because we are in React Native
	
See the differents commits on my local repo

	C:\ProgrammingProjects\JavascriptProjects\udacifitness
	
React Native most used components

	ScrollView 
	FlatList (FlatList doesn’t support adding section headers to a list)
	SectionList : https://facebook.github.io/react-native/docs/sectionlist.html
	TextInput
	KeyboardAvoidingView : to avoid having the keyboard hiding the textview
	Slider
	Switch
	ActivityIndicator
	Picker
	WebView
	Modal	
	
React Native complete list of components

	https://facebook.github.io/react-native/docs/components-and-apis.html#components-and-apis
	
	
Example of list (first possibility)

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			Image
		} from 'react-native'
	import getReviews from "./reviews"
	
	
	function Review({ name, text, avatar}){
		return (
			<View style={styles.review}>
				<Image source={{uri:avatar} style={styles.avatar}}/>
				<View style={{flex:1, flexWrap:'wrap'}}>
					<Text style={fontSize: 20}>{name}</Text>
					<Text>{text}</Text>
				</View>
			</View>
		)
	}

	export default class App extends React.Component {
		const reviews = getReviews()

	  render() {
		return (
		  <View style={style.container}>
			<View  
				{reviews.map((name, text, avatar)=> <Review key={name} name={name} text={text} avatar={avatar}/>)}
			</View>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}

here is the review.js

	const reviews = [
		{
		"url": "http://toto.fr"
		"text": "toto"
		"name": "toto name"
		"key": "toto name"
		"avatar": "http://twitter.com/toto/profile_image?size=normal"
		best=true,
		},
		{
		"url": "http://titi.fr"
		"text": "titi"
		"name": "titi name"
		"key": "titi name"
		"avatar": "http://twitter.com/titi/profile_image?size=normal"
		best=true,
		},
		{etc}
	]

Example of list (first possibility) notes

	this works fine but we cant scroll
	we should use a ScrollView
	
like this

	  render() {
		return (
		  <View style={style.container}>
			<ScrollView  
				{reviews.map((name, text, avatar)=> <Review key={name} name={name} text={text} avatar={avatar}/>)}
			</ScrollView>
		  </View>
		)
	  }
	  
Problem with scrolview

	it's not performant because we are charging all item event if the user can't see it
	that's why we need a flatlist
	
with a flatlist

	  renderItem = ({item}) => {
		return <Review {...item}/>
	  }

	  render() {
		return (
		  <View style={style.container}>
			<View  
			<FlatList 
				data={reviews}
				renderItem={this.renderItem}/>
			</View>
		  </View>
		)
	  }
	
TextInput component

	import React from 'react'
	import 
		{ 
			Text, 
			View, 
			StyleSheet, 
			Switch, 
			TextInput, 
			KeyboardAvoidingView,
			Image
		} from 'react-native'
	import getReviews from "./reviews"
	
	
	export default class App extends React.Component {
	   state= {
			input ='toto'
			showInput='false',
	   }

	   handleToggleSwitch = () => {
			this.setState((state)=>(
				showInput: !showInput,
			))
	   }
	   
	   handleTextChange = () => {
			this.setState((input)=>(
				input
			))
	   }
	   
	  render() {
		const {input, showinput} = this.state
	  
		return (
		  <View style={style.container}>
			<KeyboardAvoidingView behavior='padding' style='styles.container'>
				<Image 
					source={uri: 'https://toto.png'}
					style={style.img}
				/>
				<Switch
					value={showInput}
					onValueChange={this.handleToggleSwitch}
				/>
				{showInput === true && (
					<TextInput
						value={input}
						style={styles.input}
						onChangeText={this.handleTextChange}
					/>
				)}

			</KeyboardAvoidingView>
		  </View>
		)
	  }
	  
	  const style=StyleSheet.create({
		container:{
			flex:1, 
			marginLeft:10, 
			marginRight:10, 
			alignItems:'center', 
			justifyContent:'center'
		},
		btn: {
			backgroundColor: '#E53224',
			padding:10, 
			paddingLeft:50,
			paddingRight:50,
			justifyContent:'center',
			borderRadius:5		
		},
		btnText:{
			color:'#fff'
		}
	  })
	}

Notes about the last example

	we used onChangeText but onChange would have been possible too.
	onChangeText passes the actual value (text) as the argument. 
	onChange passes the entire event object as an argument. 
	more here : https://stackoverflow.com/questions/44416541/react-native-difference-between-onchange-vs-onchangetext-of-textinput
	
	<Image source={uri: 'https://toto.png'} />  // the image is on a serveur
	<Image source={require('toto.png')} />  // the image is on a serveur, and toto.png should be in the same directory of your app.js
	<View style={margin:50} /> to add some spacing
	
Web application database

	data can be store in local storage or session storage
	https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
	data is saved in the user browser
	
Saving the store to the local storage example

	// store.js

	import { createStore } from 'redux';
	import Reducer from '../reducers/reducer';

	const configureStore = () => {
	  const store = createStore(Reducer);

	  store.subscribe(() => {
		localStorage.state = JSON.stringify(store.getState());
	  });

	  return store;
	};

	export default configureStore;
	
Note about this example

	store.subscribe() is passed in a callback function
	The callback saves a JSON string of the store's state into localStorage

Asyncstorage

	is react native version of reactJs local storage
	it's the same as local storage except it's asynchronous
	it's not db but can be considered to be one. It has the same purpose.
	has 3 main methods
		setItem
		removeItem
		clearAll
	more here : https://facebook.github.io/react-native/docs/asyncstorage.html
	and here : https://facebook.github.io/react-native/docs/asyncstorage.html#methods
	
See the commit

	https://github.com/udacity/reactnd-UdaciFitness-complete/compare/AddEntry-TextButton...Api
	
Note about the commit

	this line "return AsyncStorage.mergeItem(CALENDAR_STORAGE_KEY, JSON.stringify({" 
	means we will add object JSON.stringify etc to the database AsyncStorage by merging this object into the AsyncStorage property CALENDAR_STORAGE_KEY
	
See commits

	https://github.com/udacity/reactnd-UdaciFitness-complete/compare/Api...actions
	https://github.com/udacity/reactnd-UdaciFitness-complete/compare/actions...reducers
	
Now add redux to your project

	npm install --save react-redux
	npm run start
	
Follow this commit

	https://github.com/udacity/reactnd-UdaciFitness-complete/compare/reducers...create-store
	https://github.com/udacity/reactnd-UdaciFitness-complete/compare/create-store...connect-AddEntry
	
A component has 2 duties

	manage state
	manage presentation
	
Presentation is a combination of 2 things

	JSX markup
	style
	
Style in react

	must not be hosted in a stylesheet but in a component
	is not made using CSS
	is made using javascript
	
Style in React Native

	must be manage by the component
	"is a props accepted by all React Native component "style="
	the value of style is just a plain old JavaScript object 
	
Style an js

	 There are many different styling libraries popping up and each has different tradeoffs. 
	 Two of the most popular are Glamorous and Styled Components. 
	 Glamorous : https://github.com/robinpowered/glamorous-native
	 Styled Components : https://github.com/styled-components/styled-components
	
in css we have

	<!-- index.css -->
	.avatar {
	  border-radius: 5px;
	  margin: 10px;
	  width: 48px;
	  height: 48px;
	}

	<!-- // index.html -->
	<div>
	  <img class='avatar' src='https://tylermcginnis.com/tylermcginnis_glasses-300.png' />
	</div>
	
in js we will have

	function Avatar ({ src }) {
	  return (
		<View>
		  <Image
			style={{borderRadius: 5, margin: 10, width: 48, height: 48}}
			source={{uri: 'https://tylermcginnis.com/tylermcginnis_glasses-300.png'}}
		  />
		</View>
	  );
	}
	
Or for better reusability

	const styles = {
	  image: {
		borderRadius: 5,
		margin: 10,
		width: 48,
		height: 48
	  }
	};

	function Avatar ({ src }) {
	  return (
		<View>
		  <Image
			style={styles.image}
			source={{uri: 'https://tylermcginnis.com/tylermcginnis_glasses-300.png'}}
		  />
		</View>
	  );
	}
	
Or if we use React-Native styleSheet

	import React from 'react';
	import { StyleSheet, Text, View } from 'react-native';

	export default class TextExample extends React.Component {
	  render() {
		return (
		  <View>
			<Text style={styles.greenLarge}>This is large green text!</Text>
			<Text style={styles.red}>This is smaller red text!</Text>
		  </View>
		);
	  }
	}

	const styles = StyleSheet.create({
	  greenLarge: {
		color: 'green',
		fontWeight: 'bold',
		fontSize: 40
	  },
	  red: {
		color: 'red',
		padding: 30
	  },
	});
	

	
Use stylesheet instead of object because

	it's more performant
	it make possible to refer to it by ID instead of creating a new style object every time.
	StyleSheet validates the content within the style object as well. This means that should there be any errors in any properties or values in your style objects, the console will throw an error during compilation instead of at runtime.
	
Using array instead of object
	
	it's good for averriding styles
	<Text style={[styles.red, styles.greenLarge]}>This will be red, then greenLarge</Text>
	<Text> component will render large green text, as the last style in the array will take precedence. This is a great way to inherit styles!
	
Let's have a look at the "Styled Components" library = alternative to css and js

	npm install styled-components
	it allow you to write style in css instead of javascript
	it allow to have a component with style inside it and not passed as a props
	more here : https://www.styled-components.com/

Here is an Example of use

import React from 'react'
import {Text, View, StyleSheet} from 'react-native'
import styled from 'styled-components/native'

	const CenterView=styled.View`
		flex:1;
		align-items:center;
		justify-content:center;
		background:#333
	`

	const GreenText=styled.View`
		color: 'green';
		font-size:20;
	`
	
	const GreenButton=styled.TouchableOpacity`
		width: '100px';
		height: '50px';		
		backgroud:red;
		border-radius:5px;
		jutify-content:center;
		align-items:center;
	`
	
	export default class TextExample extends React.Component {
	  render() {
		return (
		  <CenterView>
			<GreenText>This is green text!</GreenText>
			<GreenButton onPress={()=>(alert('Hello')}><Text>GreenButton</Text></GreenButton>			
		  </CenterView>
		);
	  }
	}
	
Layout on the web is built using

	block models
	floats
	
Block Model and Float css property

	specify if the element should be placed at the right or left side of its container
	specify where the text or in-line component should wrap (passer à la ligne)
	
Flexbox

	is a layout mode intended to accomodate different
		screen sizes
		display devices
	is easier than Block Model because it does not use floats
	is a replacement of Block Model
	give the parent element the ability to control the layout of all of their (immediate!) child elements
	rather than having each child element control its own layout
	the parent becomes a flex container
	the child elements become flex items
	
Flexbox Axes are 

	Main Axis : y (ordonée) :  children are laid out vertically from top to bottom in the default behavior
	Cross Axis : x (abcisse) : children are laid out horizontally from left to right in the default behavior
	
Flex Direction 

	property in ReactJS : flex-direction
	property in ReactNative : flexDirection 
	has 2 values
		row : (flexDirection: row ). The Main axis is horizontal (abcisse), while the Cross axis is vertical (ordonée)
		column : this is the default. (flexDirection: column). The Main Axis is vertical (ordonée) and its Cross Axis is horizontal (abcisse)
		
Main Axis justifyContent has 5 properties

	justifyContent: 'flex-start' align every child element at the start of the the Main Axis. Which means "the top" if we have the default  "flexDirection: column"
	justifyContent: 'center' align every child element at the center of the the Main Axis. That's nice because they are still one under the other. They don't overlap. But all childs are centered.
	justifyContent: 'flex-end' will align every child element towards the end of the the Main Axis. Which means "the bottom" if we have the default  "flexDirection: column"
	justifyContent: 'space-between' align every child so that the first and last are respectively at the top and bottom and other are in between with the same space separating them. if we have the default  "flexDirection: column".
	justifyContent: space-around same as 'space-between' but start with a top and bottom space
	
To play arount use this Example

	import React, { Component } from 'react'
	import { StyleSheet, Text, View, AppRegistry } from 'react-native'

	class FlexboxExamples extends Component {
	  render() {
		return (
		  <View style={styles.container}>
			<View style={styles.box}/>
			<View style={styles.box}/>
			<View style={styles.box}/>
		  </View>
		)
	  }
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})

	export default FlexboxExamples;
	
example of justifyContent use
	
	container: {
	  flex: 1,
	  justifyContent: 'flex-start',
	}
	
this is equivalent to because of the default column property

	container: {
	  flex: 1,
	  flexDirection: 'column',
	  justifyContent: 'flex-start',
	}
	
if you need a row

	container: {
	  flex: 1,
	  flexDirection: 'row',
	  justifyContent: 'space-around',
	}
	
Align Items (Cross Axis only) properties

	alignItems: 'flex-start' align (One child under the other.) every child element at the start of the the Cross Axis (Which the left).   
	alignItems: 'center' align (One child under the other.) every child element at the center of the Cross Axis.
	alignItems: 'flex-end' align (One child under the other.) every child element at the end of the the Cross Axis.
	alignItems: 'stretch' will stretch every child element along the Cross Axis as long as the child element does not have a specified width (flexDirection: row) or height (flexDirection: column). Genre de match parent. Item stretch as long as that child element doesn't have a width or a height.
	Looks a bit like justifyContent but it's not.
	
Example of use

	container: {
	  flex: 1,
	  alignItems: 'stretch',
	},
	box: {
	  height: 50,
	  backgroundColor: '#e76e63',
	  margin: 10,
	}

flex property

	is a little bit like the "weight" of android
	
	class FlexboxExamples extends Component {
	  render() {
		return (
		  <View style={styles.container}>
			<View style={[styles.box, {flex: 1}]}/>
			<View style={[styles.box, {flex: 2}]}/>
			<View style={[styles.box, {flex: 1}]}/>
		  </View>
		)
	  }
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
		flexDirection: 'row',
		justifyContent: 'center',
		alignItems: 'center',
	  },
	  box: {
		width: 50,
		height: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})

	export default FlexboxExamples;
	
Aligning Individual Children : alignSelf 

	if we want all the children align a certain way. We do like we did before.
	if we want a child to align differently from what specified in the parent, we need to override the parent behavior.
	you do this with alignSelf 
	it as the same properties as alignItems 
		flex-start
		flex-end
		center
		stretch
		
Here is an example

	class FlexboxExamples extends Component {
	  render() {
		return (
		  <View style={styles.container}>
			<View style={styles.box}/>
			<View style={[styles.box, {alignSelf: 'flex-end'}]}/>
			<View style={styles.box}/>
		  </View>
		)
	  }
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
		flexDirection: 'row',
		justifyContent: 'center',
		alignItems: 'center',
	  },
	  box: {
		width: 50,
		height: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})

	export default FlexboxExamples;


React Native flex is different from ReactJs on the web

on the web with ReactJs

	flex-direction:'row' by default
	containers are not flex containers by default. If you want a flex container you have to define it yourself in css (.container {display:flex;})
	flex specifies how a flex item grows or shrinks to manage the space around it (along the main axis). 

on mobile with React Native

	flex-direction:'column' by default
	containers are flex containers by default.
	flex is generally used with flex items that are on the same level, but hold different flex values.
	
css default properties that are applied to React Native components by default

	box-sizing: border-box;
	position: relative;
	align-items: stretch;
	flex-shrink: 0;
	align-content: flex-start;
	border: 0 solid black;
	margin: 0;
	padding: 0;
	min-width: 0;
	
For example:

	import React from 'react';
	import { View } from 'react-native';

	const FlexDemo = props => (
	  <View style={{flex: 1}}>
		<View style={{flex: 1, backgroundColor: 'red'}} />
		<View style={{flex: 2, backgroundColor: 'green'}} />
		<View style={{flex: 3, backgroundColor: 'blue'}} />
	  </View>
	);

	export default FlexDemo;
	
Note about the example

	FlexDemo is a stateless functional component which renders <View> components with different flex values.
	Its outermost container is set to flex: 1, which will expand the full available width along the main axis
	Its children <View> components will fill the space accordingly, rendering 
		a blue background color that takes up three times as much space as red takes, 
		and green that takes up exactly twice as much space as red takes.

Platform API

	makes it easy to write different code for Android ou iOS
	
Dimension API

	allows to select window's width and height in the user's device!
	import { Dimensions } from 'react-native';
	const { width, height } = Dimensions.get('window');
	use these measurements to, for example, plan how your <View>s will look like.
	
Add React-Native calendar

	npm install --save udacifitness-calendar
	npm start

More on Stylesheet

	they are used to avoid having too much in-line style properties
	they allow better performance : Making a stylesheet from a style object makes it possible to refer to it by ID instead of creating a new style object every render
	
Example

	<View style={{
	  borderRadius: 4,
	  borderWidth: 0.5,
	  borderColor: '#d6d7da',
	}}>
	  <Text style={[
		{fontSize: 19, fontWeight: 'bold'}, 
		props.isActive && { color: 'red' }
	  ]}>
		Welcome
	  </Text>
	</View>
	
become

	var styles = StyleSheet.create({
	  container: {
		borderRadius: 4,
		borderWidth: 0.5,
		borderColor: '#d6d7da',
	  },
	  title: {
		fontSize: 19,
		fontWeight: 'bold',
	  },
	  activeTitle: {
		color: 'red',
	  },
	});

	<View style={styles.container}>
	  <Text style={[styles.title, props.isActive && styles.activeTitle]} />
	</View>
	

Media Queries

	One thing you may have noticed is that React Native (and specifically the StyleSheet API) doesn’t support media queries. The reason for this is because, for the most part, you can design responsive grids with flexbox which will bypass the need to use media queries. In the rare case where flexbox just won’t work for your specific needs, you can use the Dimensions API which we covered earlier to get similar results.
	
React Native Routing

	There are many solution for routing they are all good but not official
	React Native Navigation is the official solution we will study this one

Routing on the web

	you map a URL to a Component
	
Routing on mobile

	you map an URI to stack of component
	
React Native Routing Components are

	TabNavigator
	StackNavigator : can add right to left transition
	DrawerNavigator
	The return value of TabNavigator and StackNavigator is a component and we can render it as such!
	
First install

	npm install --save react-navigation

Example TabNavigator

	import React, { Component } from 'react'
	import { StyleSheet, Text, View } from 'react-native'
	import {FontAwesome, Ionicons} from 'expo/vector-icons'
	import {TabNavigator, StackNavigator, DrawerNavigator} from 'react-navigation'

	function Home()
		return (
		  <View style={styles.container}>
			<Text>HOME</Text>
		  </View>
		)
	}
	
	
	function Dashboard()
		return (
		  <View style={styles.container}>
			<Text>Dashboard</Text>
		  </View>
		)
	}
	
	const Tabs=TabNavigator({
		Home : {
			screen:Home,
			navigationOptions:{
				tabBarIcon:()=><FontAwesome name='home' size='30' color='black'/>
			}
		},
		Dashboard : {
			screen:Dashboard,
			navigationOptions:{
				tabBarIcon:()=><FontAwesome name='dashboard' size='30' color='black'/>
			}			
		}
	})
	
	export default class App extends React.Component{
		render(){
			return (
			  <View style={styles.container}>
				<Tabs/>
			  </View>
			)
		}
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})

	export default FlexboxExamples;

Example StackNavigator

	import React, { Component } from 'react'
	import { StyleSheet, Text, View } from 'react-native'
	import {FontAwesome, Ionicons} from 'expo/vector-icons'
	import {TabNavigator, StackNavigator, DrawerNavigator} from 'react-navigation'

	function Home({navigation})
		return (
		  <View style={styles.container}>
			<Text>HOME</Text>
			<TouchableOpacity onPress={()=>(navigation.navigate('Dashboard')}>
				<Text>TO DASHBOARD</Text>
			</TouchableOpacity>
		  </View>
		)
	}
	
	
	function Dashboard()
		return (
		  <View style={styles.container}>
			<Text>Dashboard</Text>
		  </View>
		)
	}
	
	const Stack=StackNavigator({
		Home : {
			screen:Home,
			navigationOptions:{
				title:'Home'
			}			
		},
		Dashboard : {
			screen:Dashboard,	
			navigationOptions:{
				title:'Dashboard',
				headerTintColor: 'red',
				headerStyle: {
					backgroundColor:'green'
				}
			}
		}
	})
	
	export default class App extends React.Component{
		render(){
			return (
			  <View style={styles.container}>
				<Stack/>
			  </View>
			)
		}
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})

	export default FlexboxExamples;

Example DrawerNavigator

	import React, { Component } from 'react'
	import { StyleSheet, Text, View } from 'react-native'
	import {FontAwesome, Ionicons} from 'expo/vector-icons'
	import {TabNavigator, StackNavigator, DrawerNavigator} from 'react-navigation'

	function Home({navigation})
		return (
		  <View style={styles.container}>
			<Text>HOME</Text>
			<TouchableOpacity onPress={()=>(navigation.navigate('DrawerOpen')}>
				<Text>Open drawer</Text>
			</TouchableOpacity>
		  </View>
		)
	}
	
	
	function Dashboard()
		return (
		  <View style={styles.container}>
			<Text>Dashboard</Text>
			<TouchableOpacity onPress={()=>(navigation.navigate('DrawerOpen')}>
				<Text>Open drawer</Text>
			</TouchableOpacity>
		  </View>
		)
	}
	
	const Drawer=DrawerNavigator({
		Home : {
			screen:Home,
			navigationOptions:{
				drawerLabel:'Home'
				drawerIcon: ()=><FontAwesome name='home' size={20} color={black}/>				
			}			
		},
		Dashboard : {
			screen:Dashboard,	
			navigationOptions:{
				drawerLabel:'Dashboard',
				headerTintColor: 'red',
				drawerIcon: ()=><FontAwesome name='Dashboard' size={20} color={black}/>		
			}
		}
	})
	

	export default class App extends React.Component{
		render(){
			return (
			  <View style={styles.container}>
				<Drawer/>
			  </View>
			)
		}
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})
	
	export default FlexboxExamples;
	
Permissions : there are three scenarios to manage:

	The user gives you permission to view their location (best-case scenario).
	The user decides to neither deny nor grant you permission to their location.
	The user denies giving you access to their location.
	
Geolocalisation

	getCurrentPositionAsync gets the current location of the device, without watching for future updates. 
	watchPositionAsync will also get the current location of the device, but it will also subscribe to location updates.
	more here : https://docs.expo.io/versions/latest/sdk/location.html

Animations : they are mainly 3 types

	decay : start with initial velocity and slow down and stop
	spring : like in physics model
	timing : animated a value over time
	more here : https://facebook.github.io/react-native/docs/animated.html
	
basically

	we add a property on our state
	the animation chnage the property and update the component several times until the animation is done
	the componanet need to be mark as Animated (ex. Animated.Image)
	

Example

	import React, { Component } from 'react'
	import { StyleSheet, Text, View, Animated } from 'react-native'
	
	export default class App extends React.Component{
		
		state = {
			opacity : new Animated.Value(0)
			width : new Animated.Value(0)
			height : new Animated.Value(0)			
		}
		
		componentDidMount(){
			const {opaciy, width, height} = this.state
			
			Animated.timing(opacity, {toValue: 1, duration : 1000})
			.start()
			
			Animated.spring(width, {toValue: 300, speed : 5})
			.start()	

			Animated.spring(height, {toValue: 300, speed : 5})
			.start()			
		}
	
		render(){
			const {opaciy, width, height} = this.state
		
			return (
			  <View style={styles.container}>
				<Animated.Image
					style={[styles.img, {opacity, width, height}]}
					source={{uri:'http://toto.png'}}
				/>
			  </View>
			)
		}
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})
	
	export default AnimatedExamples;


Note about the example

	animation start at 0 finished at 1 and takes 1000 ms
	
Notifications : there are 2 types

	push notifications : require a server which handles pushing the notification to your user's devices when a certain event occurs.
	local notifications : do not use or require any external infrastructure; the device should be on.
	
	in iOS

		 notifications do not appear at the top of the screen automatically if the application is in the foreground. 
		 push notifications do not function in the iOS simulator (whether or not Expo is used).
	 
Handling Photo : ImagePicker 

	provides access to the system's UI for selecting images from the phone's photo library or taking a photo with the camera

Example

	import React, { Component } from 'react'
	import { StyleSheet, Text, View, ImageEditor, TouchableOpacity, Image } from 'react-native'
	import { ImagePicker} from 'Expo'
	
	export default class App extends React.Component{
		
			state= {
				image:null,
			}
		
			pickImage = () => {
				ImagePicker.launchImageLibraryAsync({
					allowEditing: true,
					aspect[2,1]
				}).then((result)=>{
					if(result.cancelled){
						return
					}
					
					ImageEditor.cropImage(result.uri, {
						offset:{x:0, y:0},
						size:{width:result.width, height:result.height},
						displaySize:{width:200, heigh:100}, 
						resizeMode:'contain'
					},
					(uri)=> this.setState({image : uri})),
					() => console.log('Error')
					)
				})
			}
		
		render(){
		
			const {image} = this.state
		
			return (
			  <View style={styles.container}>
				<TouchableComponent onPress=this.pickImage>
					<Text>Open Camera roll</Text>
				</TouchableComponent>
			  </View>
			  
			  {image && (<Image style={style.img} source={{uri:image}})}
			)
		}
	}

	const styles = StyleSheet.create({
	  container: {
		flex: 1,
	  },
	  box: {
		height: 50,
		width: 50,
		backgroundColor: '#e76e63',
		margin: 10,
	  }
	})
	
	export default ImagePickerExamples;
	
App stores what you need is

	an icon that's going to show up when the user is downloading the app
	an app description name
	Expo make it easy to specify these sorts of things just by editing the app.json
	the app.json should be built and pushed on the store to work
	
example of configurations we'll be adding in our UdaciFitness app:

	{
	  "expo": {
		"sdkVersion": "19.0.0",
		"orientation": "portrait",
		"name": "Udacifitness",
		"description": "The best triathlon training app in the world.",
		"slug": "udacifitness",
		"version": "1.0",
		"icon": "https://maxcdn.icons8.com/Color/PNG/512/Sports/triathlon-512.png",
		"notification": {
		  "icon": "http://www.student-scholarships.com/images/made/img/featured/nav_basketball_45_45.png"
		},
		"ios": {
		 "bundleIdentifier": "org.udacifitness.exp",
		},
		"android": {
		 "package": "org.udacifitness.exp",
		}
	  },
	}
	
App store

	The easiest way to generate both the .apk and the .ipa files is to use Expo's exp CLI
	npm install -g exp
	make sure your app.json is setup correctly
	exp build:<your-mobile-platform>
	note expo ask you to create a keystore for you say yes
	Note that these will take anywhere from 10-20 minutes to build
	To check the status of the build you can run exp build:status (during those 10-20 minutes)
	Eventually that command will give you a URL where you can go to download either your .ipa or .apk files.
	
iOS App Store 

	will ask you for a .ipa ("iOS App Store Package") file 
	exp build:ios 
	more here : https://developer.apple.com/library/content/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/UploadingBinariesforanApp.html#//apple_ref/doc/uid/TP40011225-CH38-SW1
	 
Android Google Play store 

	will ask you for a .apk ("Android Application Package") file
	exp build:android
	more here : https://support.google.com/googleplay/android-developer/answer/113469?hl=en
	
	
# How would I apply React concept in android java without using javascript ?

	il faut un store et une db (pour persister le store qu'on veut).
	comment representer le store en java ? un bundle ? un fichier json ? 
	
	
	ArrayList<JSONObject> entryCities = new ArrayList<>();
	intent.putExtra("JSONObject", entryCities.toString());
	JSONArray entries = new JSONArray(getIntent().getStringExtra("JSONObject"));
	
	reducer create a copy of a state (part of the state)
	update pieces of state : compononentdidmount call setState (when new state available)
	persistData if someDataneed to be persisted (persisted data must be a subset of state)
	refreshUI(pieceOfstate) anycomponent view of that display this piece of state if they are displayed should refresh itelf
	each component view has it's own piece of state defined in the custom view. each view compare its piece of state with the one given, if it changed it update redraw notifydatasetchange switch case views of the fragment, update corresponding data structure, nofify
	
	