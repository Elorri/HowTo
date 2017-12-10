
# Google cloud platform services availables only in Java

If you go to 

	https://cloud.google.com/docs/
	https://cloud.google.com/storage-options/
	
And open java and node.js languages you will see

	tutorials : some will be common to boths languages and then have the same name, some won't and then will be found only for this language
	apis : idem above. Not all apis are available for all languages.
	code samples : idem
	tools : idem


The hosting plateform for java is Google App Engine


# Google cloud platform overview

## Regions and zones

	Cloud Platform consists of a set of physical assets, such as computers and hard disk drives, and virtual resources, such as virtual machines (VMs), that are contained in Google's data centers around the globe. Each data center location is in a global region. Regions include Central US, Western Europe, and East Asia. 
	Each zone is identified by a name that combines a letter identifier with the name of the region. For example, zone a in the East Asia region is named asia-east1-a
	This distribution of resources provides several benefits, including redundancy in case of failure and reduced latency by locating resources closer to clients.

## Resources

There differents ressources :

	global resources (can be accessed by any other resource, across regions and zones) : disk images, disk snapshots, and networks
	regional resources (can be accessed only by resources that are located in the same region) : static external IP addresses
	zonal resources (can be accessed only by resources that are located in the same zone) : VM instances, their types, and disks
	
Scope of operations

	depends on what kind of resources you're working with
	exple : creating a network is a global operation because a network is a global resource
	exple : reserving an IP address is a regional operation because the address is a regional resource
	ccl : Platform won't let you do that but don't attach a disk in one region to a computer in a different region because the latency you'd introduce would make for very poor performance.

## Project

Any Cloud Platform resources that you allocate and use must belong to a project. Each project has : 

	A project name, which you provide.
	A project ID, which you can provide or Cloud Platform can provide for you.
	A project number, which Cloud Platform provides.
	A billing account (if billing enabled)
	A list of services used ???
	Screenshot visible here : https://cloud.google.com/docs/overview/

Project and ressources : 

	Resources from same project can communicate, but ressources from differents projects can't.
	For example, you might start a new project if you want to make sure only certain team members can access the resources in that project, while all team members can continue to access resources in another project.
	
Project deletion

	Once you have created a project, you can delete the project but its ID can never be used again.
	
Project and billing

	A billing account can be linked to several projects.
	
Project and namespace

	A ressource of the project must have an unique name in the project. (you can usually reuse resource names if they are in separate projects)
	Some resource names must be globally unique (I don't know which one yet)
	
## How to use ressources ?

There is 3 possibilities : 

	Google Cloud Console
	Google Cloud Command-line interface = Google Cloud SDK
	Google Cloud Client libraries
	
Google Cloud Platform Console 
	
	web-based, graphical user interface
	used to manage projects
	used to manage ressources
	
Google Cloud SDK 

	is a command-line tool gcloud
	runs on Windows, Mac OS X, and Linux, and requires Python 2.7.x.
	used to manage projects
	used to manage ressources
	+ used for developpement access to App Engine, Compute Engine, Cloud Storage, BigQuery, Cloud SQL, and Cloud DNS.
	= autre nom pour Firebase CLI (Command Line Interface)??? en tout cas les commandes 'node --version' 'npm --version' and 'firebase --version' marchent bien dessus.
	
Google Cloud Client libraries

	used to manage ressources
	allow you to access products(=ressource ?) such as Google Maps, Google Drive, and YouTube...
	
## Pricing

	https://cloud.google.com/products/calculator/
	https://cloud.google.com/pricing/tco/
	
## Services

They are many but the most commons are : 

	Computing and hosting services
	Storage services
	Networking services
	Big Data services

### Computing and hosting services, they are several posibilities, order from the less responsability on your shoulder to the max responsabilities

	use the app engine : ressouce management is completely done by google (managed (application plateform)
	use the container engine : ressouce management is done by you and google 50% 50% (cluster managed)
	use compute engine = virtual machine : ressource management is done completely by you. (unmanaged(infrastructure))
	https://cloud.google.com/docs/choosing-a-compute-option
	strange but keyword "compute" means in fact "host"
	
#### App engine :

	is a platform as a service (PaaS)
	is not on your local machine
	if the application requires more computing resources because of traffic increases, Google automatically scales the system to provide those resources
	if the system software needs a security update, that's handled for you, too.
	for instance for java :	instead of using phone java vm, it will use app engine java vm and calculations will be quick.
	Google App Engine is a Platform as a Service (PaaS) that lets you deploy and run your applications on the Google infrastructure without having to worry about setting up your own hardware, Operating System or server. 

App engine allow you to use/choose: 	

	a standard environment that has vm supporting languages Python 2.7, Java 7, PHP, and Go.
	a flexible environment that has vm supporting more recent languages like Python 2.7/3.4, Java 8, Go, Node.js, and Ruby
	a custom runtimes (basically you own vm) to use an alternative implementation of a supported language or any other language.
	
App engine SDK

	is different from App engine
	it's a command line tool that simulate an App engine on your local machine
	there a 2 differents : one for the standard environment, the other for the flexible environment
	
standard environment

	the app instances run on google sandboxes
	languages : those specific version of Python 2.7, Java 7, PHP 5.5, Go 1.6
	has a NoSQL datastore called 'App engine datastore'
	has a SQL database called 'Google Cloud SQL' with possibility to choose 
		MySQL or PostgreSQL
		Redis, MongoDB, Cassandra, and Hadoop
		any third-party databases if hosted on a serveur
	has a library api generation tool called 'Google Cloud Endpoints' that makes a library accessible from the android phone
	has a security tool called 'Cloud Security Scanner' that identify security vulnerabilities
	network access only via app engine
	pricing : Based on instance hours. Intended to run for free or at very low cost, where you pay only for what you need and when you need it. For example, your application can scale to 0 instances when there is no traffic

flexible environment
	
	the app instances run on google vms (=docker containers)
	languages : any version of Python, Java, Node.js, Go, Ruby, PHP, or .NET
	has a NoSQL datastore called 'App engine datastore'
	has a SQL database called 'Google Cloud SQL' with possibility to choose
		MySQL or PostgreSQL
		any third-party databases if hosted on a serveur (but no preinstalled Redis, MongoDB, Cassandra, and Hadoop)
	has a library api generation tool called 'Google Cloud Endpoints' that makes a library accessible from the android phone
	has a security tool called 'Cloud Security Scanner' that identify security vulnerabilities
	network access yes every possibilities
	pricing Based on usage of vCPU, memory, and persistent disks

standard environment vs flexible environment help 
		
	https://cloud.google.com/appengine/docs/
	contains a very google table that compare everything clearly https://cloud.google.com/appengine/docs/the-appengine-environments
	
Google Cloud Endpoints

	allow easy shared backend management between users using OAuth 2.0 authentication
	free devloppers from system admin work, load balancing, scaling, and server maintenance
	
#### Container engine
	
	is built on the open source Kubernetes system
	has clusters = Compute Engine instances running Kubernetes
	a lot more but I'm not interested see https://cloud.google.com/docs/overview/cloud-platform-services
	
#### Google Compute Engine

	is an infrastructure as a service (IaaS)
	it's a robust computing infrastructure
	Google will ensure that resources are available, reliable, and ready for you to use
	but you must choose and configure the platform components that you want to use
	you have complete control of the systems and unlimited flexibility
	
	has virtual machines (VMs), called instances
	allow regions and zones choice to deploy your resources
	allow operating systems, development stacks, languages, frameworks, services, and other software technologies choice
	allow instance groups creation to more easily manage multiple instances together.
	allow Attach and detach disks as needed.
	allow SSH use to connect directly to your instances.
	
#### Example App Engine + Google Compute Engine used together

	https://cloud.google.com/solutions/reliable-task-scheduling-compute-engine

### Storage services

Have a persistent disk which can be one of those

	standard persistent disks (hard disk)
	solid-state persistent disks (SSD)
	
And a database which can be one of thoses : 

	a SQL database called 'Google Cloud SQL'
	a SQL database called 'Google Cloud Spanner' that offer synchronous replication for high availability
	a NoSQL datastore called 'Google Cloud datastore'
	a NoSQL datastore called 'Google Cloud bigtable'
	
choosing your data storage : go to console > menu; storage options are

	bigtable under storage tab
	datastore  under storage tab
	SQL  under storage tab
	storage  under storage tab
	big query  under big data tab (both a storage service and an analysis service)
	
thoses storage services can be divided into 2 categories

	structured : can be organised in a table with column and rows
	unstructured : needs a sequence of bytes, a place where you want to store it (called a bucket), a name to identify the sequence of bytes; it's for files (called objects in the google cloud platform) : zip, jpeg, csv ...
	
structured data can be stored with

	bigtable 
	datastore 
	SQL  
	big query
	
unstructured data can be stored with

	storage 
	
the primarly operational databases are

	bigtable 
	datastore 
	SQL  
	must be used as part of an application
	
the analytical database is
	
	big query
	
how to store a file

	console > menu > storage (stokage) > storage (stokage) > browser (navigateur) > new bucket (compartiments)
	choose a name; buckets names are unique accross all projects
	
choose the storage class

	regional/standard : its the one used by default. high availability more than once a month and mostly by people around the region. most expensive.	
	coldline/durable reduced availabilty : if you access it very rarely but more than once a month. Generally used for backup, archives. middle-cost.
	nearline : for data accessed less than once a month. lowest-cost. 
	
choose the location

	multi-Regional : if your objects will be acced by for worldwide regions; also to make sure your datastay in territories with the juridiction you belong to;
	regional : choose the same region here as the one chosen in compute/host services for better performance; for your objects (files) that will be accessed from the same region
	
create the bucket; now you have access to buttons like

	import folder
	import file
	create file
	
you can achieve the same usingbthe gcloud command
 
	gsutil ls //gives us the name of the bucket we just created as an uri exple: gs://sonorous-stone-170616.appspot.com
	gs: prefix specify objects stored in google cloud storage
	gsutil gs://sonorous-stone-170616.appspot.com
	
to access files in the local file system or objects stored in the amazon s3

	gsutil s3://sonorous-stone-170616.appspot.com
	ls .
	gutil -m cp * gs://sonorous-stone-170616.appspot.com  //copy all your local files to the 'gs://sonorous-stone-170616.appspot.com ' bucket
	
now that your files are in your bucket create a mysql serveur

	go to console > storage > SQL > New instance
	
now that we have a mysql serveur let connect to it using a client

	go to console > compute > compute engine > New instance
	in "access an security" tab > cloud sql > select enable
	or select "allow api access to all google cloud services"
	click create
	
finish client config

	in the shell type : app get install sql client
	create an ipv4 instance to connect to
	cloud sql > overview > ipv4 address > manage > request  ipv4 address
	see the video for more details...
	
cloud datastore

	scale very gracefully from small databases sizes to big databases sizes (from 0 to terabytes)
	allow flexible schema definition
	instead of creating tables we create entities of kind
	we can then have another entity with the same kind (but a different number of columns)
	
advantages

	no need to know in advance the perfect number of column you will need; if your system evolve just add an entity of the same kind
	this avoid those tables full of empty cells
	but still you need to deal with entity that dont have the data; what do you do with them; like in relational db;
	no need to tell the datastore how many ressources do i need (instances sizes, cluster sizes)
	
cloud bigtable

	 if your scaling needs are truly massive (more than a terabyte; very high volume of write)
	 it's a nosql like cloud datastore
	 was used by google over a decade
	 inspired opensource community : Hbase part of Hadoop
	 is compatible with Hadoop
	 is a lower level database than cloud sql and cloud datastore that's why it can scale high and provide low latency
	 see video https://cloud.google.com/storage-options/
	 you put the scale manually (number of nodes)
	 the minimum node you can put will still be too big for a small application; no matter how much you use it; you will have to pay;
	
bigquery

	can run sql queries over terabytes of data in seconds
	can query public data like wikimedia

There are many options use the table and video find here to make your choice

	https://cloud.google.com/storage-options/
	
very good chart about deciding between different data stores that Google cloud offers

	https://cloud.google.com/images/storage-options/flowchart.svg
	
### Network services

if you use

	app engine : networking is done for you by Google
	container engine : networking is done for you using Kubernetes model
	compute engine : you will have access to a set of services (accessed via your vm instances) that will allow you to 
		balance traffic load across resources
		create DNS records
		connect your existing network to Google's network (Carrier Interconnect, Peering connection, Compute Engine VPN)
		publish and maintain Domain Name System (DNS)
		
if your compute engine want to configure network

	it should create at least one vm instance and connect it to the network.
	must always have one default network chosen(in case you need severals)
	the configured network won't be available for other projects
	
traffic reaching network is managed by

	firewall rules : when a network is accepted, an instance is created.
	
instance created can send data to other network, those sends are managed by a

	route : exple of route you can create : a vpn
	
### Big data services

Big data services enable you to process and query big data in the cloud to get fast answers to complicated questions. 

#### BigQuery

BigQuery provides data analysis services. With BigQuery, you can:

	Create custom schemas that organize your data into datasets and tables.
	Load data from a variety of sources, including streaming data.
	Use SQL-like commands to query massive datasets very quickly. BigQuery is designed and optimized for speed.
	Use the web UI, command-line interface, or API.
	Load, query, export, and copy data by using jobs.
	Manage data and protect it by using permissions.

To try out BigQuery quickly

	https://cloud.google.com/bigquery/what-is-bigquery
	Web UI Quickstart to query a public dataset : https://cloud.google.com/bigquery/quickstart-web-ui
	Example of processing real-time data : https://cloud.google.com/solutions/real-time/kubernetes-redis-bigquery
	
#### Cloud Dataflow 

Dataflow works well for high-volume computation, especially when the processing tasks can clearly and easily be divided into parallel workloads. Useful for : 

	performing batch and streaming data processing tasks
	extracting-transforming-loading (ETL) tasks : transforming data into a more desirable format
	loading data onto a new storage system
	
#### Cloud Pub/Sub 

Is an asynchronous messaging service that works as follow : 

	Your application send messages as JSON data structures
	A global unit called topic receive the message. Because its global applications belonging to differents projects can see it.
	Applications subscribes to topics they want and receives http request or responses.
	
To try out Cloud Pub/Sub  quickly

	https://cloud.google.com/dataflow/docs/
	Web UI Quickstart : https://cloud.google.com/pubsub/docs/quickstart-console
	Example : https://cloud.google.com/solutions/real-time/kubernetes-pubsub-bigquery
	
Cloud Pub/Sub's usefulness isn't confined to big data, it is useful whenever you need asynchronous messaging

	Example without bigquery : https://cloud.google.com/solutions/reliable-task-scheduling-compute-engine
	
## Tools

### Development tools and environments

#### Google Cloud SDK 

(see above)

#### Google Cloud Shell

allow you to run the Google Cloud SDK commands in a web browser
no need to install the Cloud SDK to run it
https://cloud.google.com/shell/docs/features

#### Android Studio

You can add Cloud Platform as a backend to your Android app directly from the Android Studio IDE.

	see : https://cloud.google.com/android-studio/
	
Android Studio ships with out-of- the- box integration for 
	
		App Engine
		Cloud Endpoints
		Google Cloud Messaging for Android (GCM)
		
#### IntelliJ IDEA

Google-sponsored plugin that adds support for the Google Cloud Platform to IDEA. 
It enables you to debug production applications running on the Google Cloud Platform right inside of IntelliJ

#### Cloud Source Git Repositories

Each project you create in the Cloud Platform Console has an associated, fully-featured Git repository that is hosted on Cloud Platform. 

	https://cloud.google.com/source-repositories/docs/
	
#### Debugging, tracing, and analysis, logging and monitoring

	Stackdriver Debugger : https://cloud.google.com/debugger/
	Stackdriver Trace : https://cloud.google.com/trace/
	Stackdriver Logging : https://cloud.google.com/logging/docs/view/logs_viewer_v2
	Stackdriver Monitoring : https://app.google.stackdriver.com/account/login/?next=/
	more info : https://cloud.google.com/docs/overview/developer-and-admin-tools	

#### Others tools

I won't use now,because for other languages

	Cloud Tools for Visual Studio
	Cloud Tools for PowerShell
	Cloud Tools for Eclipse

#### Deploying systems automatically

	Google Cloud Launcher : https://cloud.google.com/launcher/
	Deployment Manager : https://cloud.google.com/deployment-manager/docs/
	More here : https://cloud.google.com/docs/overview/developer-and-admin-tools
	
#### Try it out

Free trial

	https://console.cloud.google.com/freetrial?_ga=1.261459722.620680443.1496501055&page=0
	https://cloud.google.com/free/docs/frequently-asked-questions
	
Library examples

	https://cloud.google.com/docs/tutorials
	https://github.com/GoogleCloudPlatform/
	http://googlecloudplatform.github.io/ if you select Solution>Mobile you get nice examples
	
My selected examples

	https://github.com/googlearchive/solutions-mobile-shopping-assistant-backend-java use this and replace theservlet with this below
	https://cloud.google.com/appengine/docs/standard/java/cloud-sql/
	
10 Minute Interactive Tutorial

	Je n'arrive pas à me connecter
	https://interactive-tutorial.appspot.com/
	
#### Other notes

In android studio you can run the backend module like any module.

There is 2 way to connect your app to the cloud : 

- make your app implements a REST api and send call to Google Cloud SQL directly.
- make your app communicate with Google App Engine and make Google App Engine communicate with  Google Cloud SQL.


Online Compiler avaible on play store

	
"AIDE" Great workaround for Android IDE on tablet

The front-end of Google cloud Platform is similar to J2EE, ASP, JSP
Google cloud Platform is a framework similarto JEE.


# GCPlatform project list

	https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055
	
	
# Load a csv file and query it using big querry

Most common firebase sdk commands

	gcloud
	bq for big query
	gsutil for cloud storage
	
first make sure you are on the project you want to enable the service you want

	gcloud auth login
	gcloud config list : to check what the currently set default project has been set to 
	gcloud config set project friendlychatapp-585e2 : to set your new project
	
create a csv file

	cd FriendlyChatApp/
	mkdir raw
	click droit on the 'raw' folder and click new>file
	name the file messages.csv
	
add this data in it (note I was not able to make it work with pipes, I used ',' instead)

	key1,user1,Hello it's me toto
	key2,user2,Hello it's me tutu
	key3,user3,Hello it's me turlututu
	key4,user4,Hello it's me titi
	
load this raw data to Firebase Storage

	gsutil cp messages.csv gs://friendlychatapp-585e2.appspot.com
	Operation completed over 1 objects/131.0 B.

created a Big table dataset and call it messages

	bq mk messages
	if not it will ask to select default project. Do so. Select FriendlyChatApp.
	if not it will tell you that billing has not been enable
	
go to ... and select ...

	https://console.cloud.google.com/billing
	Mes projets > FriendlyChatApp > Actions > Changer le compte de facturation
	now facturation is enabled
	
try again

	bq mk messages
	now we get 'friendlychatapp-585e2:messages' successfully created.'
	
check this here

	https://bigquery.cloud.google.com/
	select the project FriendlyChatApp
	yes it is youhoo
	
load the Firebase Storage dataset into a BigQuery table
	
	bq load messages.messages_table gs://friendlychatapp-585e2.appspot.com/messages.csv key,userName,Message
	check that there is no errors

this is also possible :define schema in a json file
	
	bq load messages.messages_table gs://friendlychatapp-585e2.appspot.com messages_table_schema.json
	more infos : 'bq help' and https://cloud.google.com/bigquery/docs/loading-data-cloud-storage
	
query your table

	bq query "select * from messages.messages_table"
	incredible it works !!!

gcloud commandes

	gcloud app
	gcloud auth
	gcloud components
	gcloud compute
	gcloud config
	gcloud container
	gcloud dataflow
	gcloud dataproc
	gcloud datastore
	gcloud debug
	gcloud deployment manager
	gcloud dns
	gcloud firebase
	gcloud iam
	gcloud kms
	gcloud ml-engine
	gcloud organizations
	gcloud projects
	gcloud service-mangement
	gcloud source
	gcloud spanner
	gcloud sql


For example to interact with BigQuery you use bq and for Cloud Storage you use gsutil.
	
	https://devopscloud.net/2014/11/30/a-real-quick-quick-start-with-google-cloud-platform-command-line-tools/



	gsutil cp PeriodicTableDataSet.csv gs://my-periodicatable-bucket
	bq mk elements
	bq load elements.ptable gs://my-periodictable-bucket/PeriodicTableDataSet.csv
	ptable_schema.json
	bq query "SELECT name, symbol from elements.ptable where Z >100"
	gsutil --help
	bq --help
	
# What makes Google Cloud Platform different?

here are the different comparison with amazon and microsoft

	https://cloud.google.com/free/docs/map-aws-google-cloud-platform
	https://cloud.google.com/docs/compare/aws/
	https://cloud.google.com/free/docs/map-azure-google-cloud-platform
	https://cloud.google.com/docs/compare/azure/
	
Migrate your data to google cloud platform

	https://cloud.google.com/migrate/
	https://cloud.google.com/storage/docs/migrating
	https://cloud.google.com/sql/docs/mysql/import-export/importing

Remove your data from google cloud platform

https://cloud.google.com/sql/docs/mysql/import-export/exporting

# What is machine learning?

Machine learning is functionality that helps software perform a task without explicit programming or rules. Traditionally considered a subcategory of artificial intelligence, machine learning involves statistical techniques, such as deep learning (aka neural networks), that are inspired by theories about how the human brain processes information.

is accessible in the form of open source libraries (TensorFlow), as well as managed services and cloud APIs
is for data scientists who want to build “future-proof” models
is for mainstream developers who lack adequate training data and want to bring a pre-built/pre-trained model into their app via a cloud API

# What is big data?

is an alternative to relational database
is used when storing, managing, or analyzing tasks can't be achieved with relational database
arrived with connected devices that end up adding a lot of information to analyse

relational database

	stores easily structured data but not unscructured data such as images, text, and video
	gives a not fast enough answer; if database is big can reply after a long long time; 
	does not scale easily if table start to be very big

to solve thoses problems the first alternatives were

	Apache Hadoop
	NoSQL database systems
	Cloud computing 

Apache Hadoop and NoSQL database systems (= on-premise systems) are

	complex to deploy and manage
	expensive and unsecure ?
	
Cloud computing 

	offers access to data storage, processing, and analytics
	offers a more scalable, flexible, cost-effective, and even secure experience

is available thouth

	Google BigQuery
	Google Cloud ML Engine
	in a pay-as-you-go manner
	
# What configuration to choose for an android app

	host/engine : google app engine
	container : ?
	storage (structured files) :  sql, firebase realtime database
	storage (unstructured files) :  datastore, google cloud storage for firebase
	operation : firebase cloud functions

# how to query your data

	https://firebase.google.com/docs/database/android/lists-of-data

# differences between couchdb et firebase

	firebase make it opaque the http requests no need for retrofit with firebase
	actuality its possible to use the Firebase’s REST API so it's not so opaque
	read data from json object does not use same java object; although we can use the same if we really want
	we can always export our database files into a json file if one day we want to change server; but cant export everything in one go is file too big
	writting data (pushing) to the server is made easier with firebase because it let you manage authentication easily
	i don't know how to authenticate with couchdb
	seems that it is possible to query with javascript https://howtofirebase.com/save-and-query-firebase-data-ed73fb8c6e3a
	
# BaaS

	enables you to manage a centralised database that lets your users share content via the cloud. Back in the day things were different and you’d need to develop your own backend using a server-side technology such as Ruby or PHP. 
	often comes with services like
		data storage
		file storage
		app analytics
		user authentications
		push notifications
		geolocation
		network and user management (authentification)
		facebook authentications...
		facebook open graph publishing for social engagement
		google places
		in-app purchase
	comes with libraries of sdk for
		iOS
		Android
		Javascript
		Java
		Windows
	
# Quel backend choisir quel prix ?

to get an idea of the price you need to to estimate demand prior to launch how your app will scale, because this is something challenging when you start most of the BaaS offer a freemium model and offer good value for money with pricing based on usage and increased scalability.

This enables you to manage commercial risk as you’ll only start to pay once your app becomes successful.

# Example of BaaS and pricing

Kumulos

	give you a 30 days free trial 
	It costs $50 per app, per month.
	supports ... giving some some API
		iOS, OSX, PHP, Windows, Cordova, Ionic,  Phonegap, Unity, Xamarin and Android
	
Kinvey

	is pricy
	has a free tier if you are an inde developer 
	can get expensive if you are a company with more than 20 employees. $2,000 a month to be exact. 
	gives you ... libraries 
		iOS
		Android
		Javascript
	to use them you need to download the libraries (in the gradle) or use the REST api
	

# Custom Backend

	A custom backend takes a lot of time to build, and afterwards requires regular maintenance – and for many small apps, this cost may not be worth the benefit. You also need to take the standard security precautions like getting an SSL Certificate, protecting database access, etc.

	Note a maket is the way to go


	 
