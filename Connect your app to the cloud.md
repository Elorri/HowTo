# I'm following this tutorial

	https://github.com/googlearchive/solutions-mobile-shopping-assistant-backend-java

# Firebase cloud messaging = Google cloud messaging

is

	send messages between servers and client apps
	could inform a client app that there is new data to be fetched from the server, as in the case of a "new email" notification
	can transfer up to 4kb of payload to the client app
	handles all aspects of queueing of messages and delivery to and from the target client app.
	
	
register you client app


make the server send a message to the app

	server send message to connection server
	connection server enqueues and stores the message if the device is offline
	When the device is online, the GCM connection server sends the message to the device.
	the client app receives the message 
	
# Ajouter un backend a une application android

une fois le backend ajouté, diverses fonctionnalités peuvent être ajoutées comme

	 un espace de stockage de données
	 Les backends exécutés sur Google App Engine évoluent automatiquement pour accommoder des millions d'utilisateurs. 
	 Vous n'avez pas besoin d'acheter ou d'exploiter vos propres serveurs.
	 
il est possible

	exécuter et tester un backend localement, puis le déboguer en même temps que l'application Android qui l'utilise.
	Lorsque la phase de développement est terminée, déployez votre backend dans  Google Cloud Source Git Repositories depuis Android Studio pour le rendre accessible à tous les utilisateurs de votre application
	debugger votre backend dans la console grace à  Google Cloud Debugger 
	
comment

	avec les plug-ins en utilisant le protocole HTTP simple, Google Cloud Endpoints et Google Cloud Messaging
	avec cadres d'applications Android Studio développés et gérés par Google
	
# Procedure

See : https://cloud.google.com/tools/android-studio/quickstart


## Select or create a Cloud Platform project.

Go to ... and create le projet. Il se voit ensuite dans les notifications (petite cloche)

	https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055
	
## Create a new Android Studio project

You know how to do that

## Add the App Engine Java Servlet module

Steps : 

	In Android Studio, select File > New > New Module.
	Select Google Cloud Module in the New Module window and click Next.
	You have 3 options here ... and a link to the documentation(as github repo) appears when selected 
	
		App Engine Java Servlet module
		App Engine Java Endpoint module
		App Engine BackEnd with GCM

		
## Which one should I use ?

App Engine Java Servlet module

	simpliest way to set up a backend
	can't generate marshalling/unmarshalling object to JSON or protect with OAuth 2.0. 
	can't push notifications
	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloWorld
	see : https://cloud.google.com/tools/android-studio/app_engine/add_module

App Engine Java Endpoint module

	define a RESTful backend API by annotating server-side Java code
	provide automated Java object marshalling/unmarshalling to JSON
	can generate libraries that can be called from your Android app
	has a built-in authentication support OAuth 2.0
	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloEndpoints
	see : https://cloud.google.com/tools/android-studio/endpoints/add_module
	
App Engine BackEnd with Firebase Cloud Messaging

	allows you to send push notifications from your server to your users' Android devices
	and also to receive messages from devices on the same connection
	handles all aspects of queueing of messages and delivery to the target Android application
	Using FCM, you can notify a client app that new email or other data is available to sync. You can send notification messages to drive user reengagement and retention. For use cases such as instant messaging, a message can transfer a payload of up to 4KB to a client app.
	usually used with "App Engine Java Endpoint" and "App Engine Java Servlet module"
		App Engine Java Endpoint is used to register Android devices with the server (App Engine Java Servlet module?)
	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/GcmEndpoints
	see : https://cloud.google.com/tools/android-studio/messaging/add_module
	
Note from the forum

	"All App Engine apps are basically Servlets. A Cloud Endpoint Module is still a servlet but the wizard adds a bunch of classes to your backend module to make it easier for you to get started creating an API, persisting data in the Cloud DataStore, enabling GCM, etc."
	For an example of unmarchmalling datato json see here http://omerio.com/2016/01/16/real-time-sensor-dashboard-using-google-app-engine-and-raspberry-pi-zero/
	
## Create a CloudAppJavaServlet

We are following the tutorial ... and github repo ...

	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloWorld
	see : https://cloud.google.com/tools/android-studio/app_engine/add_module

In android studio 

	select New > Module > Google Cloud Module > App Engine Java Servlet Module
	enter the module name
	enter the package name
	select the client you want your backend to be connected with
	
click finish

	this will set up your client module to call your backend
	a new run configuration with your backend's module name is created. You can see it under thetraditionnal run configurations
	
select Tools > Android > Sync Project with Gradle Files to sync the project. 

	This will add dependency to setting.grade
	
debbug the backend

	Run > Run... > Backend (ou clique sur la flèche verte) : this will start the local app engine
	navigate to http://localhost:8080 : you should see the name of your servlet MyServlet in the page
	navigate to http://localhost:8080/_ah/admin : you can see the task queue
	navigate to http://localhost:8080/_ah/api/explorer : you can test the functioning of the API
	try again using debugger. You should stop in the post method
	
connect your app to the remote back end

	add <uses-permission android:name="android.permission.INTERNET" /> in the manifest
	make an HTTP request that call the backend, it is a simple asynctask
	make sure the local backend is started, run it again if not
	run the app
	
how to create an AsyncTask which makes the HTTP request to the backend and prints the incoming result string to a toast ?

	class ServletPostAsyncTask extends AsyncTask<Pair<Context, String>, Void, String> {
		private Context context;

		@Override
		protected String doInBackground(Pair<Context, String>... params) {
			context = params[0].first;
			String name = params[0].second;

			try {
				// Set up the request
				URL url = new URL("http://10.0.2.2:8080/hello");
				HttpURLConnection connection = (HttpURLConnection) url.openConnection();
				connection.setRequestMethod("POST");
				connection.setDoInput(true);
				connection.setDoOutput(true);

				// Build name data request params
				Map<String, String> nameValuePairs = new HashMap<>();
				nameValuePairs.put("name", name);
				String postParams = buildPostDataString(nameValuePairs);

				// Execute HTTP Post
				OutputStream outputStream = connection.getOutputStream();
				BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(outputStream, "UTF-8"));
				writer.write(postParams);
				writer.flush();
				writer.close();
				outputStream.close();
				connection.connect();

				// Read response
				int responseCode = connection.getResponseCode();
				StringBuilder response = new StringBuilder();
				BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
				String line;
				while ((line = reader.readLine()) != null) {
					response.append(line);
				}
				reader.close();

				if (responseCode == HttpsURLConnection.HTTP_OK) {
					return response.toString();
				}
				return "Error: " + responseCode + " " + connection.getResponseMessage();

			} catch (IOException e) {
				return e.getMessage();
			}
		}

		private String buildPostDataString(Map<String, String> params) throws UnsupportedEncodingException {
			StringBuilder result = new StringBuilder();
			boolean first = true;
			for (Map.Entry<String, String> entry : params.entrySet()) {
				if (first) {
					first = false;
				} else {
					result.append("&");
				}

				result.append(URLEncoder.encode(entry.getKey(), "UTF-8"));
				result.append("=");
				result.append(URLEncoder.encode(entry.getValue(), "UTF-8"));
			}

			return result.toString();
		}

		@Override
		protected void onPostExecute(String result) {
			Toast.makeText(context, result, Toast.LENGTH_LONG).show();
		}
	}

Now add this line in MainActivity onCreate

	new ServletPostAsyncTask().execute(new Pair<Context, String>(this, "Manfred"));
	
Note : 

	if you test your app on your phone you will get error an "http://10.0.2.2:8080/" because the app will send sending requests to a computer in the local network. But the webapi service will not be available because the computer (i.e. the "server") does not exist. (Or you have to create a local serveur on your phone)
	if you test your app using the emulator, a webapi serveur is made for you, and you won't get the error.
	
Create remote to App Engine

	go to https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055
	creer un projet 'CloudAppJavaServlet'
	once done une notification apparait, click dessus or go directly to https://console.cloud.google.com/home/dashboard?project=cloudappjavaservlet
	prendre l'id du projet ici : cloudappjavaservlet
	
Prepare for deploying using google cloud sdk

	Download the 'google cloud java standard environnement sdk for windows'
	https://cloud.google.com/appengine/downloads
	I haven't managed to make it worked henced I stopped here
	
Prepare for deploying using google cloud shell (allow you to run the Google Cloud SDK commands in a web browser)

	Go to https://cloud.google.com/shell/docs/quickstart?hl=fr
	Click the Activate Google Cloud Shell button at the top of the console window.
	run gcloud config set project cloudappjavaservlet
	run 'gcloud config list' to check what the currently set default project has been set to (here project = cloudappjavaservlet)
	run 'gcloud app create'
	choose region 'europe-west' according to this doc (le tableau à la fin) https://cloud.google.com/about/locations/
	
Deploying the backend remote to App Engine
	
	Passer dans la vue Projet d'android studio
	Aller sur backend > src/main/webapp/WEB-INF/app-engine-web.xml
	Change myApplicationId par cloudappjavaservlet (This important only if you deploy from the command line gcloud deploy.)	
	Stop the backend, if it is running locally, by selecting Run > Stop > Backend.
	Run Build > Deploy Module to App Engine > select the project id cloudappjavaservlet > Deploy
	Note : if you get an oath exception, click on create a new user (if needed to manage project user go to ... and delete recreate user https://console.cloud.google.com/iam-admin/iam/project?project=cloudappjavaservlet)
	
last step before running go to and change 

	URL url = new URL("http://10.0.2.2:8080/hello");

by

	URL url = new URL("http://cloudappjavaservlet.appspot.com/hello");
	
And you see the toast

	Hello Manfred !!! CA MARCHE
		
## Create a CloudAppEngineJavaEndpoint

We are following the tutorial ... and github repo ...

	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloEndpoints
	see : https://cloud.google.com/tools/android-studio/endpoints/add_module
	
In android studio 

	select New > Module > Google Cloud Module > App Engine Java Enpoint Module
	enter the module name
	enter the package name
	select the client you want your backend to be connected with
	
click finish

	this will set up your client module to call your backend
	a new run configuration with your backend's module name is created. You can see it under thetraditionnal run configurations
	
select Tools > Android > Sync Project with Gradle Files to sync the project. 

	This will add dependency to setting.grade
	
look at class MyEndpoint and please note

	@Named is required for all non-entity type parameters passed to server-side methods.
	@Api(name = "jokeApi",...) is requiered to give a name to the api you can usein the client
	
		
debbug the backend

	Run > Run... > Backend (ou clique sur la flèche verte) : this will start the local app engine
	navigate to http://localhost:8080 : you should see 'Google Cloud Endpoints API' in the page
	navigate to http://localhost:8080/_ah/admin : you can see the task queue
	navigate to http://localhost:8080/_ah/api/explorer : you can test the functioning of the API
	try again using debugger in the sayHi() method. You should stop in it.
	
connect your app to the remote back end

	add <uses-permission android:name="android.permission.INTERNET" /> in the manifest
	make an HTTP request that call the backend, it is a simple asynctask
	make sure the local backend is started, run it again if not
	run the app

how to create an AsyncTask which makes the HTTP request to the backend and prints the incoming result string to a toast ?

	class EndpointsAsyncTask extends AsyncTask<Pair<Context, String>, Void, String> {
		private static MyApi myApiService = null;
		private Context context;

		@Override
		protected String doInBackground(Pair<Context, String>... params) {
			if(myApiService == null) {  // Only do this once
				MyApi.Builder builder = new MyApi.Builder(AndroidHttp.newCompatibleTransport(),
						new AndroidJsonFactory(), null)
					// options for running against local devappserver
					// - 10.0.2.2 is localhost's IP address in Android emulator
					// - turn off compression when running against local devappserver
					.setRootUrl("http://10.0.2.2:8080/_ah/api/")
					.setGoogleClientRequestInitializer(new GoogleClientRequestInitializer() {
						@Override
						public void initialize(AbstractGoogleClientRequest<?> abstractGoogleClientRequest) throws IOException {
							abstractGoogleClientRequest.setDisableGZipContent(true);
						}
					});
					// end options for devappserver

				myApiService = builder.build();
			}

			context = params[0].first;
			String name = params[0].second;

			try {
				return myApiService.sayHi(name).execute().getData();
			} catch (IOException e) {
				return e.getMessage();
			}
		}

		@Override
		protected void onPostExecute(String result) {
			Toast.makeText(context, result, Toast.LENGTH_LONG).show();
		}
	}
	
Now add this line in MainActivity onCreate

	new EndpointsAsyncTask().execute(new Pair<Context, String>(this, "Manfred"));
	
Note about the execute() of this line 'return myApiService.sayHi(name).execute().getData()': 

	if you test your app on your phone you will get error "java.net.ConnectException: failed to connect to /10.0.2.2 (port 8080) after 20000ms: isConnected failed: EHOSTUNREACH (No route to host)" because the app will send sending requests to a computer in the local network. But the webapi service will not be available because the computer (i.e. the "server") does not exist. (Or you have to create a local serveur on your phone)
	if you test your app using the emulator, a webapi serveur is made for you, and you won't get the error.
	you can test on real device see here "Testing device registration on a physical device" https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloEndpoints 
	In case the link above does not work I add it here : 
		2.1.1. Testing device registration on a physical device

			Testing on a physical device with a local development server requires minor changes to your configuration.
			You must make your development server accessible to the network by setting it to listen to external connections. You can do this by editing the build.gradle for the backend project and setting the httpAddress.

				appengine {
				  ....
				  httpAddress = "0.0.0.0"
				  ....
				}
				
			You must also change the endpoint root url to point to your computer's ip address when creating the endpoint .
			
				Registration.Builder builder = new Registration.Builder(AndroidHttp.newCompatibleTransport(),
						new AndroidJsonFactory(), null)
						.setRootUrl("http://<my-computer-address>:8080/_ah/api/")
						....
	
Create remote to App Engine

	go to https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055
	creer un projet 'CloudAppEngineJavaEndpoint'
	once done une notification apparait, click dessus pour voir l'id ici 'sonorous-stone-170616'
	go to https://console.cloud.google.com/home/dashboard?project=sonorous-stone-170616
	prendre l'id du projet ici : sonorous-stone-170616
	
Prepare for deploying using google cloud sdk

	Download the 'google cloud java standard environnement sdk for windows'
	https://cloud.google.com/appengine/downloads
	I haven't managed to make it worked henced I stopped here
	
Prepare for deploying using google cloud shell (allow you to run the Google Cloud SDK commands in a web browser)

	Go to https://cloud.google.com/shell/docs/quickstart?hl=fr
	Click the Activate Google Cloud Shell button at the top of the console window.
	run gcloud config set project sonorous-stone-170616
	run 'gcloud config list' to check what the currently set default project has been set to (here project = CloudAppEngineJavaEndpoint)
	run 'gcloud app create'
	choose region 'europe-west' according to this doc (le tableau à la fin) https://cloud.google.com/about/locations/
	
Deploying the backend remote to App Engine
	
	Passer dans la vue Projet d'android studio
	Aller sur backend > src/main/webapp/WEB-INF/app-engine-web.xml
	Change myApplicationId par sonorous-stone-170616 (This important only if you deploy from the command line gcloud deploy.)	
	Stop the backend, if it is running locally, by selecting Run > Stop > Backend.
	Run Build > Deploy Module to App Engine > select the project id sonorous-stone-170616 > Deploy
	Note : if you get an oath exception, click on create a new user (if needed to manage project user go to ... and delete recreate user https://console.cloud.google.com/iam-admin/iam/project?project=cloudappjavaservlet)
	
get the remote url

	link Cloud Endpoints API Explorer : http://sonorous-stone-170616.appspot.com/_ah/api/explorer
	turn on OAuth 

define scope for your app
	
	depending on the user who is using the app, the api will return a different scope = access to its functionalities
	for more about scope : https://developers.google.com/identity/protocols/OAuth2?csw=1
	select "https://www.googleapis.com/auth/userinfo.email" scope and click 'Authorize'
	select your google account
	
get the remote url (suite)

	click on myApi API v1
	enter a name in name field and click execute
	note the post request
		
last step change 

	.setRootUrl("http://10.0.2.2:8080/_ah/api/")

by

	.setRootUrl("https://sonorous-stone-170616.appspot.com/_ah/api/")
	
And you see the toast

	Hello Manfred !!! CA MARCHE

## Create a CloudAppBackEndWithGCM

I think you can skip this tuto and use the FirebaseChat app notification tuto instead

We are following the tutorial ... and github repo ...
	
	see : https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/GcmEndpoints
	see : https://cloud.google.com/tools/android-studio/messaging/add_module
	
In android studio 

	select New > Module > Google Cloud Module > App Engine Bckend with Cloud Messenging
	enter the module name
	enter the package name
	select the client you want your backend to be connected with
	
click finish

	this will set up your client module to call your backend
	a new run configuration with your backend's module name is created. You can see it under thetraditionnal run configurations
	
select Tools > Android > Sync Project with Gradle Files to sync the project. 

	This will add dependency to setting.grade
		
debbug the backend

	Run > Run... > Backend (ou clique sur la flèche verte) : this will start the local app engine
	navigate to http://localhost:8080 : you should see 'Google Cloud Messaging' in the page
	navigate to http://localhost:8080/_ah/admin : you can see the task queue
	navigate to http://localhost:8080/_ah/api/explorer : you can test the functioning of the API

install Google Repositories

	Tools > Android > SDK Manager > SDK Tools tab
	Check the Google Repository checkbox, and click OK.
	
Check permissions and libraries

	Check FCM librairies : remove eny remaining "com.google.android.gms:play-services-gcm:8.4.0" et replace by "com.google.firebase:firebase-messaging:9.0.0" if not there already.
	Check FCM permissions : 
		"All the permissions required by FCM are now added automatically by library", see https://developers.google.com/cloud-messaging/android/android-migrate-fcm 
		remove <uses-permission android:name="android.permission.WAKE_LOCK" />
		remove <permission android:name="<your-package-name>.permission.C2D_MESSAGE"  android:protectionLevel="signature" />
		remove <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
	
	
open firebase assistant and connect your app
	
	Tools > Firebase to open the Assistant window.
	Click cloud messaging > Set up firebase cloud messaging
	Click 'Connect to firebase'
	Select your account
	Create a firebase project CloudAppBackEndWithGCM > Finish
	
Add FCM to your app

	open firebase assistant
	click add FCM to your app
	choose module 'app' (and not'backend')
	(This add libraries in the gradle file)
	
Get each device token 

	"Access the device registration token. "During backend module gneration a RegistrationEndpoint Cloud Endpoints API has been automatically generated for you, so that you could start calling this endpoint from your Android app to register devices with your new Google Cloud Messaging backend."

Add class MyFirebaseInstanceIDService next to the MainActivity

	public class MyFirebaseInstanceIDService extends FirebaseInstanceIdService {

		private static final String TAG = "MyFirebaseIIDService";

		/**
		 * Called if InstanceID token is updated. This may occur if the security of
		 * the previous token had been compromised. Note that this is called when the InstanceID token
		 * is initially generated so this is where you would retrieve the token.
		 */
		// [START refresh_token]
		@Override
		public void onTokenRefresh() {
			// Get updated InstanceID token.
			String refreshedToken = FirebaseInstanceId.getInstance().getToken();
			Log.d(TAG, "Refreshed token: " + refreshedToken);

			// If you want to send messages to this application instance or
			// manage this apps subscriptions on the server side, send the
			// Instance ID token to your app server.
			sendRegistrationToServer(refreshedToken);
		}
		// [END refresh_token]

		/**
		 * Persist token to third-party servers.
		 * <p>
		 * Modify this method to associate the user's FCM InstanceID token with any server-side account
		 * maintained by your application.
		 *
		 * @param token The new token.
		 */
		private void sendRegistrationToServer(String token) {
			((MyApplication)getApplication()).onTokenReceived(token);
		}
	}
		
	public class MyApplication extends Application implements FirebaseCloudServerCallbacks{

	   private MainActivity mMainActivity;

		@Override
		public void onTokenReceived(String token) {
			mMainActivity.refreshText(token);
		}

		public void setMainActivity(MainActivity mainActivity) {
			mMainActivity=mainActivity;
		}
	}

	public interface FirebaseCloudServerCallbacks {
		
		void onTokenReceived(String token);
	}

	public class MainActivity extends AppCompatActivity {

		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);

			((MyApplication)getApplication()).setMainActivity(this);
		}

		public void refreshText(final String token) {
			runOnUiThread(new Runnable() {
				@Override
				public void run() {
					((TextView)findViewById(R.id.token)).setText(token);
				}
			});
		}
	}
	
test the app (no need to start the back end for that)

	run the app
	the text no_token should be replaced after a few seconds.
	Note : you should uninstall the app manually and reinstall it to see the token change. 
	
send notifications via FCM, first this is an oveview of whats possible

	send notifications on apps in the background
	send message that update apps in the foreground
	send data payload (=small messages)
	
	

go to 

	https://console.firebase.google.com/
	
you see a list of all your projects that have been configured to use Firebase


	click on  CloudAppBackEndWithGCM
	click sur notification
	click sur envoyer votre premier message


	
	https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055

démarrer l'essaie gratuit




-------------------------------- To remove once tidied titles ## Create a CloudAppBackEndWithGCM and # Firebase


	
connect your app to the remote back end

	add <uses-permission android:name="android.permission.INTERNET" /> in the manifest
	make an HTTP request that call the backend, it is a simple asynctask
	make sure the local backend is started, run it again if not
	run the app

how to create an AsyncTask which makes the HTTP request to the backend and prints the incoming result string to a toast ?

	
Now add this line in MainActivity onCreate

	new EndpointsAsyncTask().execute(new Pair<Context, String>(this, "Manfred"));
	
Note about the execute() of this line 'return myApiService.sayHi(name).execute().getData()': 

	if you test your app on your phone you will get error "java.net.ConnectException: failed to connect to /10.0.2.2 (port 8080) after 20000ms: isConnected failed: EHOSTUNREACH (No route to host)" because the app will send sending requests to a computer in the local network. But the webapi service will not be available because the computer (i.e. the "server") does not exist. (Or you have to create a local serveur on your phone)
	if you test your app using the emulator, a webapi serveur is made for you, and you won't get the error.
	you can test on real device see here "Testing device registration on a physical device" https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/master/HelloEndpoints
	
Create remote to App Engine

	go to https://console.cloud.google.com/cloud-resource-manager?_ga=1.68758038.620680443.1496501055
	creer un projet 'CloudAppEngineJavaEndpoint'
	once done une notification apparait, click dessus pour voir l'id ici 'sonorous-stone-170616'
	go to https://console.cloud.google.com/home/dashboard?project=sonorous-stone-170616
	prendre l'id du projet ici : sonorous-stone-170616
	
Prepare for deploying using google cloud sdk

	Download the 'google cloud java standard environnement sdk for windows'
	https://cloud.google.com/appengine/downloads
	I haven't managed to make it worked henced I stopped here
	
Prepare for deploying using google cloud shell (allow you to run the Google Cloud SDK commands in a web browser)

	Go to https://cloud.google.com/shell/docs/quickstart?hl=fr
	Click the Activate Google Cloud Shell button at the top of the console window.
	run gcloud config set project sonorous-stone-170616
	run 'gcloud config list' to check what the currently set default project has been set to (here project = cloudappjavaservlet)
	run 'gcloud app create'
	choose region 'europe-west' according to this doc (le tableau à la fin) https://cloud.google.com/about/locations/
	
Deploying the backend remote to App Engine
	
	Passer dans la vue Projet d'android studio
	Aller sur backend > src/main/webapp/WEB-INF/app-engine-web.xml
	Change myApplicationId par sonorous-stone-170616 (This important only if you deploy from the command line gcloud deploy.)	
	Stop the backend, if it is running locally, by selecting Run > Stop > Backend.
	Run Build > Deploy Module to App Engine > select the project id sonorous-stone-170616 > Deploy
	Note : if you get an oath exception, click on create a new user (if needed to manage project user go to ... and delete recreate user https://console.cloud.google.com/iam-admin/iam/project?project=cloudappjavaservlet)
	
get the remote url

	link Cloud Endpoints API Explorer : http://sonorous-stone-170616.appspot.com/_ah/api/explorer
	turn on OAuth 

define scope for your app
	
	depending on the user who is using the app, the api will return a different scope = access to its functionalities
	for more about scope : https://developers.google.com/identity/protocols/OAuth2?csw=1
	select "https://www.googleapis.com/auth/userinfo.email" scope and click 'Authorize'
	select your google account
	
get the remote url (suite)

	click on myApi API v1
	enter a name in name field and click execute
	note the post request
		
last step change 

	.setRootUrl("http://10.0.2.2:8080/_ah/api/")

by

	.setRootUrl("https://sonorous-stone-170616.appspot.com/_ah/api/")
	
And you see the toast

	Hello Manfred !!! CA MARCHE
	
	
-------------------------------------------------------------------------
	

	

	
# Firebase

Without firebase

There is a lot to decide to be able to store data on a serveur.

	1. We need a database. Hence we need to choose and setup a serveur that have this database installed and is accessible though the internet.
	2. We need to decide where we will store large items like photos, audio, videos, because database storage and file storage are often separated.
	3. To make those 2 communicate we will need an app serveur
	
This is how will achieve communication

	1. App will send request to app serveur
	2. App serveur route (=create copy ofthe request) request to database serveur and file serveur
	
Responsability of the app serveur

	write code to communicate with database serveur
	write code to communicate with file serveur
	write code to control and monitor who access to database and files
	write code to analyse user engagement, showing advertisements, push notifications
	
With firebase

	firebase realtime database keep data in the cloud and in sync between users
	firebase storage gives you a place to store user uploaded content (photo, audio, videos)
	firebase authentication verify user identity without having to write code
	firebase analytics make you keep tracks of how the app is used
	firebase notifications enables you to reengage part of your audience, without writing a line of code. 
		you can send notifications to all your users
		you can send notifications to just a specifics group of user
		you can send notification to a single user
	firebase remote config, you can change your app fetaures without having to update code, you can even target groups of user, and compare how they react with your offer
	
see ... and its readme.md and the Udacity class that goes with it

	C:\ProgrammingProjects\AndroidStudioProjects\Examples\FriendlyChatApp
	https://github.com/udacity/and-nd-firebase/
	https://www.udacity.com/course/firebase-in-a-weekend-by-google-android--ud0352
	
## Firebase realtime database
	
is unique because

	whenever a user or device send a change to the serveur other connected user/devices are informs with no seconds. a message send by one person in friendly chat, quickly show up in their friends app
	if the an user is offline (no network), firebase keeps the data in cache with a few lines of code, when the user is online again the app synchronise again with the serveur.
	skyscanner uses Firebase realtime database to store flights
	
structure

	all data is stored as JSON objects
	the entiere database is a single JSON object because the it's a tree of JSON. A tree starts with one single node.
	
nodes haves
	
	keys
	value-node
	
keys 

	can be customised exple : user1
	must be strings

value-node

	can have different types :strings, integer, float, boolean, nested-object
	
	
nested-object (example) ... the key here is "messages"

	"messages":
		"message1":
			"name" :"Person"
			"text" :"Hello"
		"message2":
			"name" :"Individual"
			"text" :"Hi"
			
this could be written with array and brackets according to json grammar

	"messages":[
		"message1":{
			"name" :"Person"
			"text" :"Hello"
			}
		"message2":{
			"name" :"Individual"
			"text" :"Hi"
			}
		]
		
but arrays are not recommanded in firebase and prefer use {} instead

	"messages":{
		"message1":{
			"name" :"Person"
			"text" :"Hello"
			}
		"message2":{
			"name" :"Individual"
			"text" :"Hi"
			}
		}
	
here we have chosen keys "message1" and "message2" but that potentially dangerous. Why ?

	because user1 and user2 could add "message3" at the same time

to avoid that FRDb can give unique keys

	they are unique between all users
	they are called Push-ID
	they are générated with push function
	they are ordered (a tree is kept ordered)
	
our tree become 

	"messages":
		"-KR9smkkkioufeniao":
			"name" :"Person"
			"text" :"Hello"
		"-KR9smkaoqkkocxwkm":
			"name" :"Individual"
			"text" :"Hi"
	
naming

	KR9smkkkioufeniao is the child node of messages
	messages is the parent node of KR9smkkkioufeniao
	a path refers to a specific part of a database. A full path start at the root
	the root of the database is noted /
	each path segment is a key
	example  /messages/-KR9smkkkioufeniao/
	
more about the data accessiblity : database security rules 

	there 3 types : .read, .write, .validate
	.read :whether data can be read by the user.
	.write : whether data can be written by the user.
	.validate : whether data is valid
		- whether data must have child nodes
		- whether data is correctly formated
		- whether data has correct type
		
more about the data accessiblity : database security predefined variables

	now : The current time in milliseconds since Unix epoch time (January 1, 1970)
	root : Corresponds to the current data at the root of the database. You can use this to read any data in your database in your rule expressions.
	newData : Corresponds to the data that will result if the write is allowed
	data : Corresponds to the current data in Firebase Realtime Database at the location of the currently executing rule.
	$variables : A wildcard path used to represent ids and dynamic child keys.
	auth : Contains the token payload if a user is authenticated, or null if the user isn't authenticated.
	
if you need more infos :

	now : https://firebase.google.com/docs/reference/security/database/#now
	root : https://firebase.google.com/docs/reference/security/database/#root
	newData : https://firebase.google.com/docs/reference/security/database/#newdata
	data : https://firebase.google.com/docs/reference/security/database/#data
	$variables : https://firebase.google.com/docs/reference/security/database/#location
	auth : https://firebase.google.com/docs/reference/security/database/#auth

## Firebase Authentification : more about auth

	The auth variable contains the JSON web token for the user.
	Once a user is authenticated, this token contains the provider, the uid, and the Firebase Auth ID token
		the provider is the method used by the user to authenticate like  email/password, Google Sign In, or Facebook Login, Twitter, Github.
		The uid is a unique user ID. This ID is guaranteed to be unique across all providers, so a user that authenticates with Google and a user that authenticates with email/password do not risk having the same identification.
		The Firebase Auth ID is a web token. Yes this means that there is a token inside the auth ID. 

The Firebase Auth ID  token can contain

	email : The email address associated with the account.
	email_verified : A boolean that is true if the user has verified they have access to the email address. Some providers automatically verify email addresses. You can customize authentication to include email verification for email/password on iOS.Un email est envoyé sur laboite mail et l'utilisateur doit cliquer dessus. On est donc sur que son email marche.
	name : The user’s display name, if one is set.
	sub : The user’s Firebase uID.
	firebase.identities : Dictionary of all the identities that are associated with this user's account.
	firebase.sign_in_provider : The sign-in provider used to obtain this Firebase Auth ID token.
	
Adding sign in is a lot of work  if we want

	good user experience
	keep user data secure
	
Questions that you will have to anwers are

	how do you implement each providers email/password, Google Sign In, or Facebook Login, Twitter, Github? 
	what password requierements will you implements ?
	will the user name be an email account ?
	will there be more than one way to log in ?
	how will the user choose a method for sign in ?
	how to create reset button
	
Firebase do all of that for you

	you can choose the scheme : email/password, Google Sign In, or Facebook Login, Twitter, Github
	but you still have to implement it for each provider, and create UI sign in
	if you dont want to implement UI sign in use Firebase UI
	
## Firebase UI

	is opensource library
	it handle the serie of screen (= UI flow) for authenticating 
		- choose sign in 
		- enter sign in data (email...)
		- enter passorword
		- go back to yourapp
	follow the best guidelines
	follow the best implementation up to date for each of the providers
	we can easily enable and disable providers
	but at the time it support only : email/password, Google Sign In, or Facebook Login, (no Twitter, no Github)
	
## Firebase Storage

	we don't store photo in the database because database is meant to be fast, and it wouldprolong load time. Firebase storage is where you will put those bigs items
	it's the perfect place to store files such as 'rich content document', 'images' and 'videos'
	provides a robust connection for uploading and downloading files : if you looses connection in the middle of a download, once you are connected again, the download will start where it stops. No matter your bandwidth you will manage to download your file.
	space is easily scale to suits the needs of your user base. As your app grow, your storage grow.
	is secure. Like in firebase database you can set who can read data, who can write data.
	allow to create folders
	Once a file is store in it. We can refer to the file by its url.
	has a space quota storage so its good practice to limit file size upload to avoid reaching the quota in one single download
	
Firebase Storage Security

	Users expect that you will protect their data, a photo they share on your network shouldn't be shared to the whole world.
	Storage tab > RULES

By default you got 

	service firebase.storage {
	  match /b/{bucket}/o {
		match /{allPaths=**} {
		  allow read, write: if request.auth != null;
		}
	  }
	}

That means

	users can read any part of the firebase storage as long as they are autheticated
	users can write in any part of the firebase storage as long as they are authenticated
	it's exactly like firebase database
	
Some explanations 

	service firebase.storage { //The rulesdefined bellow are for Firebase Storage
	  match /b/friendlychatapp-585e2.appspot.com/o { //We must replace {bucket} with the link to our firebase storage root of our project, if we want the rules to apply to its subdirectories. (Note : I'm not sure what bucket means maybe its pointing to the project by default - hope its not all our projects storages).
		//Next 3 line define the rule
		match /{allPaths=**} {
		  allow read, write: if request.auth != null;
		}
	  }
	}
	
The rule is made of 3 parts

	the match : match /{allPaths=**}
	the rule : allow read, write
	the context : if request.auth != null
	
match

	match a specific storage path.
	a path starts with a /and is followed by segments
	a segment can be 
		single 'single segment' : exple /toto.jpeg
		single with a wild card 'single wild card segment' : 
			/{anything}/toto.png will math 
				/a/toto.png
				/b/toto.png
			/toto/{anything} (this last means all files and directories find in toto directory)
				/toto/a.jpeg
				/toto/dir/
				but won't math /toto/dir/a.jpeg
		multi segment wild card (this means any number of path segments)
			/toto/{images=**}
rule
	
	each match can contain 1 rule or multiple rules
	always starts with keyword 'allow'
	follows one of those 3 possibilities
		read
		write
		read, write
	can be followed by a condition. if condition is true, rule will be activated.
	
context

	is found in the condition
	if condition is 'if request.auth !=null' then context is request.auth
	there is 2 types of context
		request
		ressource
		
resource

	contains infos for ressources that are already on file storage
	ressource.name
	ressource.size
	ressource.contentType (image, video, audio ...)
	
request

	deals with incoming data
	request.auth (is user authenticated)
	request.auth (if user is authentacted and has uid='whaterver suits me')
	request.ressource.name (info about a file that is currently uploading but not stored, or file currently updating)
	request.ressource.size
	request.ressource.contentType (image, video, audio ...)
	exple : allow read file only if file size < 1Mb
	request.time
	request.time.date()
	request.time.year()
	exple : allow read file only if file has been uploaded during the last 24h
	
example 

	allow you to read data if you are an authenticated user and the data is a gif
	request.auth != null && imageId.matches(".*.gif")  
	note .*.gif is a regex i think
	
more on security

	https://firebase.google.com/docs/storage/security/
	https://firebase.google.com/docs/reference/security/storage/
	
## Firebase analytics

	lets you checks
	how long a user has stay on your screen
	when a button is pressed
	time spent
	
A good video on analytics here

	https://classroom.udacity.com/courses/ud0352/lessons/fab5bf81-cfe5-4071-9afe-b6eb324a6257/concepts/4ec76161-1df7-4d8f-934b-a6f8a360d899
	https://support.google.com/firebase/answer/6317486?hl=en (all automatically collected data)
	https://firebase.google.com/docs/analytics/
	
How should I organise. 
	
	Lets say I see in my analytics that 70% of my users are under 25 years old
	I create a group for those people
	Do young people want acces to custom emojis ? use Firebase Remote Config Feature to write test and see how the use of custom emojis impact the group you have created.
	Make decision to add emoji permanently
	
	
## Firebase Notifiactions

	to send to all users, a group of users or a single user
	more on sending notifications : https://classroom.udacity.com/courses/ud0352/lessons/fab5bf81-cfe5-4071-9afe-b6eb324a6257/concepts/3949ce9a-6eb1-4f8b-bc31-42f34f25297e
	https://github.com/udacity/and-nd-firebase/compare/2.03-firebase-notifications-set-up...2.04-firebase-remote-config-default-values
	
## Firebase Remote Configuration

	use for small change, to avoid having to create a complete new update.
	exemple :texting a text size on screen, to get to know which one is prefered.
	it's made specifically for values that control the ... and ... of your app
		behaviour
		appearance
		
don't use remote config for
		
	- parameters that requiere authorization. If the user has the possibility to change the parameter you are testing, it won't make sense to test it
	- confidential info : like server keys.All parameters are publics in F Remote Config
	- ??? watch the video again it was important
	
more

	https://classroom.udacity.com/courses/ud0352/lessons/fab5bf81-cfe5-4071-9afe-b6eb324a6257/concepts/f84c2f01-fa14-4b93-b9c8-cf2f523a0c39
	https://classroom.udacity.com/courses/ud0352/lessons/fab5bf81-cfe5-4071-9afe-b6eb324a6257/concepts/d6b19f2f-c8ca-45a1-a92d-d3a2978b07ff
	https://github.com/udacity/and-nd-firebase/compare/2.04-firebase-remote-config-default-values...2.05-firebase-remote-config-fetch
	
		
## Firebase Cloud Functions and Javascript

### Basic comparison between Java and Javascript

In java
	
	declaration needs a type
	we use the word 'final' to declare a constant
	semicolon at the end of the segment is needed
	log to the console  System.out.println("Message"); or if android Log.d(TAG, "Message");
	equality == for primitives, .equals() for objects
	
	ArrayList arrayList = new ArrayList<>();
	arrayList.add(10);
	
	public int multiply(int a, int b) {
	  return a * b;
	}
	
	String name = "Firebase";
	
	String[] list = {"apple", "pear", "orange"};
	for (int i = 0; i < list.length; i++) {
		System.out.println(list[i]);
	}
	
	import java.util.ArrayList;

In Javascript

	declaration does not necessarly need a type :   var name = "Firebase"; name = 3; // OK
	we use the word 'const' to declare a constant
	semicolon at the end of the segment is optional. Usually people don't put it.
	log to the console  console.log("Message");
	equality === for strict equality
	
	var array = [];
	array.push(10);
	
		function multiply(a, b) {
			return a * b;
		}
	or
		// Variable assignment
		var multiply = function(a, b) {
			return a  b;
		}
	or
		// New in ES2016; drops "function" keyword
		var multiply = (a ,b) => {
			return a  b;
		}
		
	var str1 = "this is a valid string";
	var str2 = 'and this is too';
	var name = 'puf';
	var message = `Hello ${name}!`; // Hello puf! String interpolation with backtick quotes and ${}:
	
		var list = ['apple', 'pear', 'orange'];
		for (i = 0; i < list.length(); i++) {
			console.log(list[i]);
		}
	or
		for (var index in list) {
			console.log(list[index])
		}
		
	var child_process = require('child_process'); //To import we use require() and assign the result to a variable for later use
	
Javascript for beginners udacity course
	
	https://www.udacity.com/course/javascript-basics--ud804
	
Java lambda small review

	it's meant to replace anonymous classes that have a single method.

Example. 

	I have a method public void printPersons(List<Person>, CheckPerson checkPerson)
	CheckPerson is an interface with one method test

	printPersons(roster, new CheckPerson() {
        public boolean test(Person p) {
            return p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        }
    });
	
I can use lambda to replace that. 

	Because there is only one method in the interface it can be anonymous
	and you can also ommit the name of the interface because any functional interfaces like this will function the same way. Remove it's brackets too.
	you can also remove {return ...} and replace by a single ->
	
which gives : 

	printPersons(roster, (Person p) ->
				p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        );
		
here the interface single method (= the lambda method) take a Person as parameter and return a boolean. Java has a predicate that takes any possible object and return a boolean. It is define has below 

	interface Predicate<T> {
		boolean test(T t);
	}

If we avoid telling the type of the object the function is using and if our function return a boolean, then the Predicate will apply and we can write our function like this
	
	printPersons(roster, p ->
				p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        );

		
which would gives in Javacript. Just one change -> by =>

	printPersons(roster, (Person p) =>
				p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        );
		
and this if using the predicate (I'm not sure there is a Predicate inteface in Javacript, but there is no typing donc ça reviens au même)

	printPersons(roster, p =>
				p.getGender() == Person.Sex.MALE
                && p.getAge() >= 18
                && p.getAge() <= 25;
        );

more about lambda expressions

	https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
	
### How to use Firebase functions
	
Si j'avais voulu installé Firebase CLI (Command Line Interface)

	j'aurais suivi ce tuto https://classroom.udacity.com/courses/ud0352/lessons/9d2e8938-1714-420b-8421-03757d7d51a5/concepts/98447176-b878-437b-87ab-4c148974dc3b
	j'aurais eu besoin de 
		Node.js
		NodeJS package manager (npm)
		
Mais j'utilise Google Cloud Shell qui me permet de taper mes commandes en utilisant un browser. Pour l'ouvrir : 
	
	Go to https://cloud.google.com/shell/docs/quickstart?hl=fr
	Click the Activate Google Cloud Shell button at the top of the console window.
	
Authenticates the command line tool to your Firebase account

	firebase login --no-localhost
	answer Y to 'Allow Firebase to collect anonymous CLI usage information?'
	it gives you an url, open it in a browser. on arrive sur la page "Sélectionner un compte pour accéder à l'application Firebase CLI"
	choose an account. On arrive sur la page 'Firebase CLI souhaite...'
	clicker authoriser
	copier le code obtenu et le paster dans le CLI
	you get "Success! Logged in as etchemendy.elorri@gmail.com"

Set up our FriendlyChatApp function directory

	pwd  - you are in '/home/etchemendy_elorri'
	mkdir FriendlyChatApp
	cd FriendlyChatApp
	
Create Firebase Cloud function template in it

	firebase init functions
	Select a default Firebase project for this directory: FriendlyChatApp 
	Do you want to install dependencies with npm now? Yes
	
You now have a functions directory inside your project folder.

	FriendlyChatApp/functions
	the index.js is where we will write our cloud functions
	others files are less important but useful too
	
How to write a cloud function ?

	choose a name for the function : emojify
	choose a service that will trigger the cloud function. Could one of them and more (Notifications...)
		Firebase Realtime Database
		Firebase Authentication
		Firebase Storage
	choose trigger conditions (they are specifics to each services)
	choose and implements the event handler : emojifyHandler
	
To create and edit your functions you will need a text editor that can be start from the shell command line, here are the recommanded

	vim : but its very basic
	sublime : a little les basic
	atom : good one
	you can also use android studio but then I think you will have to do a copy paste
	but they are not installed on Firebase CLI, because there is a built-in code editor
	
To open the code editor

	click on the pencil next to the shell button
	
Open FriendlyChatApp/functions/index.js and observe

	const functions = require('firebase-functions'); //first line. We are importing the libraries that will make us able to use firebase functions.
	
Add your first function

	// replaces keywords with emoji in the "text" key of messages
	// pushed to /messages
	exports.emojify =
		functions.database.ref('/messages/{pushId}/text')
		.onWrite(event => {
			// Database write events include new, modified, or deleted
			// database nodes. All three types of events at the specific
			// database path trigger this cloud function.
			// For this function we only want to emojify new database nodes,
			// so we'll first check to exit out of the function early if
			// this isn't a new message.

			// !event.data.val() is a deleted event
			// event.data.previous.val() is a modified event
			if (!event.data.val() || event.data.previous.val()) {
				console.log("not a new write event");
				return;
			}

			// Now we begin the emoji transformation
			console.log("emojifying!");

			// Get the value from the 'text' key of the message
			const originalText = event.data.val();
			const emojifiedText = emojifyText(originalText);

			// Return a JavaScript Promise to update the database node
			return event.data.ref.set(emojifiedText);
		});

	// Returns text with keywords replaced by emoji
	// Replacing with the regular expression /.../ig does a case-insensitive
	// search (i flag) for all occurrences (g flag) in the string
	function emojifyText(text) {
		var emojifiedText = text;
		emojifiedText = emojifiedText.replace(/\blol\b/ig, "??");
		emojifiedText = emojifiedText.replace(/\bcat\b/ig, "??");
		return emojifiedText;
	}

Let's look at this closer. 1- choose a name for the function : emojify

	Writing exports is the standard way in Node.js to make a function publically visible. 
	We want a public function because our service, the Firebase database, must be able to see it.
	hence : exports.emojify (would be equivalent to java 'public void emojify()')
	We want to store the function hence exports.emojify =

2- choose a service that will trigger the cloud function.

	we want to trigger the firebase database : functions.database.ref()
	
3- choose trigger conditions

	at the root of the message tree /messages/{pushId}/text
	hence functions.database.ref('/messages/{pushId}/text')
	
4- choose and implements the event handler. We pass a function to the .onWrite() method with a single argument (event) that will represent our Realtime Database event.
	
	.onWrite(event => {})
	take sometime to read the comments of the method. It worth it.
	
More about trigger

	cloud functions will be called (triggered) whenever an event happens on the service
	for Firebase database, the events that can trigger cloud function are 'new', 'modified', and 'deleted'
	for other services check the documentation : https://firebase.google.com/docs/functions/
	
Infinite loop caution

	if your cloud function update a database node, and this update trigger cloud function call, that triger a cloud function call ...
	Infinite loops can burn through your quota for cloud functions 
	Infinite loops can cost you significant money depending on your pricing plan for Firebase.
	
To avoid infinite loop

	Write to a different database path
	Do not modify the same database path again
	
The cloud function should end either with a Promise, null, or an Object.

	 Returning null or an object ends the cloud function synchronously, as you typically expect from a return call.
	 Returning a Promise is helpful for longer running tasks and lets your cloud function continue to execute until all tasks are completed.
	 more on promises : https://firebase.googleblog.com/2016/01/keeping-our-promises-and-callbacks_76.html
	 
We dont want emojifyText to be a cloud function

	that why its not exported.
	
Deploy and test

	cd FriendlyChatApp
	firebase deploy

Look at what displayed

	functions: functions folder uploaded successfully
	functions[emojify]: Successful create operation.
	functions: all functions deployed successfully!
	
This command is packaging any functions in ... along with any dependencies declared in ... and deploying it to the cloud.

	functions/index.js
	functions/package.json
	
Now go to firebase console

	select 'function' tab
	you see your cloud function 'emojify' that will be triggered if 'write' event
	
Test your function from the console

	go to database tab
	add the message "Lol that cat is funny"
	it is nearly instantanéously changed to emojis 
	
Test it from your phone

	With your function deployed, you should be able to see your chat messages in FriendlyChat emojify too. But you currently don't see that. The emojify cloud function does trigger, and you can see the updated message in the Firebase console. But exiting out of the app and opening it afterwards does display the updated chat message.
	Remember that you have a simple implementation in the message database listener; you only implemented onChildAdded() database handler.
	Use Firebase UI https://github.com/firebase/FirebaseUI-Android/tree/master/database to implements the child event listener for List Views and Recycler Views.
	
More on cloud functions

	https://firebase.google.com/docs/functions/
	https://github.com/firebase/functions-samples
	


	
	
	
	
	
 

	
	

	
## FriendlyChatApp (learn by doing example to understand better)

Create an android studio project 

	name : FriendlyChatApp
	package : com.elorri.android.friendlychatapp

Navigating to the Firebase Console webpage.

	https://console.firebase.google.com/u/0/?pli=1
	
Create new project

	Selectionner "Créer un projet"
	Donner le nom "FriendlyChatApp"

Add firebase to android app

	click Add Firebase to your Android app
	enter your app's package name "com.elorri.android.friendlychatapp". The package name can only be set when you add an app to your Firebase project. Hence be careful to put the correct name. It must be the package name your app is using.
	
Because we are using authentification we will need a SHA1 key (only for debug). Go to a console 

	/c/Program\ Files/Java/jdk1.8.0_71/bin/keytool -exportcert -list -v \-alias androiddebugkey -keystore /c/Users/Elorri/.android/debug.keystore
	
Entrez le mode passe

	android
	
Copy SHA1

	4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34
	
Finish and then download google-services.json 

	use firefox (there is a bug with chrome)
	note you can download it at any time going to https://console.firebase.google.com/u/0/project/friendlychatapp-585e2/overview and then FriendlyChatApp>Parametres>download google-services.json 
	
Add google-services.json to app directory
	
	see commit https://github.com/udacity/and-nd-firebase/compare/1.00-starting-point...1.01-firebase-gradle-plugin
	note : they have some mave stuff in app/build.gradle and build.gradle. I don't have it and it also works.
	
More on setting up firebase

	https://firebase.google.com/docs/android/setup
	
Use firebase realtime database in your app

	add dependency com.google.firebase:firebase-database:11.0.1
	add FirebaseDatabase and DatabaseReference object
	a DatabaseReference object is a class that reference a specific class of the database
	mFirebaseDatabase=FirebaseDatabase.getInstance();
    mMessageDatabaseReference=mFirebaseDatabase.getReference().child("messages");
	Note :the root node is mFirebaseDatabase.getReference()
	
Try the app and look at "warn" messages in the log, you should see

	W/RepoOperation: setValue at /messages/-KmlPNM0jjNzdiRWxhoY failed: DatabaseError: Permission denied
		
Fix the security problem : go to https://console.firebase.google.com

	Select "Database" in the menu
	you see "null" next to friendlychatapp-585e2 that means no data
	you un message bleu "Les règles de sécurité par défaut nécessitent que les utilisateurs soient authentifiés."
	
selectionner l'onglet "règles"

	those rules make us manage whith user can access what information
	as you can see by default user can read and write to the db only if they are authenticated. no authentification, no possiblility to read or write
	{
	  "rules": {
		".read": "auth != null",
		".write": "auth != null"
	  }
	}
	
for now turn on every thing ...and press publish

	{
	  "rules": {
		".read": true,
		".write": true
	  }
	}

back to the données tab + type a message

	youhou message appears
	
to show user that data have been stored in the db we will retrieve the data stored and display it on screen

	note: in fact we won't retrieve to data, because firebase inform every devices when new data has been added (it is design for apps with a lot of traffic )
	listeners are triggerred
		- once for initialisation
		- again anytime the data change
	
change the rules back to 

	{
	  "rules": {
		".read": "auth != null",
		".write": "auth != null"
	  }
	}
		
database security advanced rules

	Sometimes, we don’t want to apply a rule to all users of an app.
	We may want to have administrative access for some users.
	We may want to unlock features stored in the database when users reach some target, like number of messages sent.
	We may want to add premium features to our app that only paying customers can access.
	
example for friendly chat :  give paying customers access to private chat rooms. first lets go back to our previous database

   "messages": {
	 "-KS3PV-iwUZp5wkNq70s": {
	   "name": "person1",
	   "text": "hey!"
	 },
	 "-KS3PXhIhs8J_inrExy4": {
	   "name": "person2",
	   "text": "what’s up?"
	 }

now add 2 nodes : "chat" and "special_chat" (= private room)

	{
	 "chat": {
	   "messages": {
		 "-KS3PV-iwUZp5wkNq70s": {
		   "name": "person1",
		   "text": "hey!"
		 },
		 "-KS3PXhIhs8J_inrExy4": {
		   "name": "person2",
		   "text": "what’s up?"
		 }
	   }
	 },
	 "special_chat": {
	   "messages": {
		 "-KR-DwqtKzlWGxSn9P0y": {
		   "name": "person1",
		   "text": "Want to go to the movies?"
		 },
		 "-KR4tIpWmNn-EYxquSrw": {
		   "name": "person3",
		   "text": "Yeah! Let’s meet at 7."
		 }
	   }
	 }
	 
If we would use a SQl database we would have ... and if we had 3 users 

	a table chat with 2 messages
	a table special_chat with 2 messages
	a table user with 3 users
	
Which give in JSON - each table become a top level node

	{
	 "chat": {
	   "messages": {
		 "-KS3PV-iwUZp5wkNq70s": {
		   "name": "person1",
		   "text": "hey!"
		 },
		 "-KS3PXhIhs8J_inrExy4": {
		   "name": "person2",
		   "text": "what’s up?"
		 }
	   }
	 },
	 "special_chat": {
	   "messages": {
		 "-KR-DwqtKzlWGxSn9P0y": {
		   "name": "person1",
		   "text": "Want to go to the movies?"
		 },
		 "-KR4tIpWmNn-EYxquSrw": {
		   "name": "person3",
		   "text": "Yeah! Let’s meet at 7."
		 }
	   }
	 },
	 "users": {
	   "uid1": {
		 "paid": true
	   },
	   "uid2": {
		 "paid": false
	   },
	   "uid3": {
		 "paid": true
	   }
	 }
	}
	
Going back to tab "RULES"

	{
	  "rules": {
		".read": "auth != null",
		".write": "auth != null"
	  }
	}
	
Let's add a few things

	{
	 "rules": {
	   "chat" : {
		 "messages" : {
		   ".read": "auth != null",
		   ".write": "auth != null"
		 }
	   },
	   "special_chat" : {
		 "messages": {
		   ".read": 
		   "root.child('users').child(auth.uid).child('paid').val() === true",
		   ".write": 
		   "root.child('users').child(auth.uid).child('paid').val() === true"
		 }
	   }
	 }
	}
	
Note this line "root.child('users').child(auth.uid).child('paid').val() === true"

	select all users who have paid

Note about cascading rules look at this example

	{
	 "chat": {
	   "messages": {
		 "-KRiMpW5bate5qV0Rt7i": {
		   "name": "person1",
		   "text": "hey!"
		 },
		 "-KQWHI_eepS4CGr8-kJd": {
		   "name": "person2",
		   "text": "what’s up?"
		 }
	   },
	   "admin_blog": {
		 "Jan 1": "Welcome to my page",
		 "Jan 2": "Enjoying the weather?"
	   },
	   "special_chat": {
	   },
	   "users": {
		 "uid1": {
		   "paid": true
		 },
		 "uid2": {
		   "paid": false
		 },
		 "uid3": {
		   "paid": true
		 }
	   }
	 }
	}

rules

	{
	 "rules": {
	   "chat" : {
		 // allows read and write to /chat/<all children>
		 // which includes /chat/messages and /chat/admin_blog
		 ".read": "true",
		 ".write": "true",


		 "admin_blog" : {
		   // will not negate the ability of the user to write to the blog
		   ".write" : "false"
		 }
	   }
	 }
	}
			
When .read and .write rule permissions are evaluate to true, this cascades to all of the rule’s children. but falseness is not cascading.

	This means any child of the node that has true .read or .write rules is also true. If a parent has .read or .write true, this access cannot be revoked by a child node

The structure of the rule is 

	chat (read and write to true)
		admin_blog (write to false)
		
and the structure of the data is

	chat
		messages
		admin_blog
		special_chat
		users
		
hence

	messages have read and write access
	admin_blog have read and write access even if it is set to false
	special_chat have read and write access
	users have read and write access
	
Now if we just do that

	{
	   "rules": {
		  "chat" : {
			 "messages" : {
				// allows read and write to /chat/messages/<all children>
				 ".read": "true",
				 ".write": "true"
			  },
			 "admin_blog" : {
				// allows read but not write to /chat/admin_blog/<all children>
				".read" : "true",
				".write" : "false"
			 }
		  }
	   }
	}
	
Now structure of the rule is

	chat (no rules set)
		messages (read and write access)
		admin_blog (read only)
		
and the structure of the data is still

	chat
		messages
		admin_blog
		special_chat
		users
		
hence

	messages have read and write access
	admin_blog have read only access
	special_chat have the access setup by default in the console (auth!=null) ??? not sure of this
	users have the access setup by default in the console (auth!=null) ??? not sure of this
		
now we will add some validations rules : rule .validate

	is useful for making sure that the structure or your JSON tree and format of your data matches what you design it to be.
	can make sure that every message object contains a "name" and a "text" object and no other data.
	can check that the "name" is a string, and no longer than 100 characters.
	".validate": "newData.isString() && newData.val().length() < 100"
	Note : the old SQL datastorage was able to perform checks by only on the type of the data inserted in the db. We had to use PL/SQL triggers to perform other checks.
	
for friendly chat here are the rules

	{
	 "rules": {
	   "messages": {
		 // only authenticated users can read and write the messages node
		 ".read": "auth != null",
		 ".write": "auth != null",
		 "$id": {
		   // the read and write rules cascade to the individual messages
		   // messages should have a 'name' and 'text' key or a 'name' and 'photoUrl' key
		   ".validate": "newData.hasChildren(['name', 'text']) && !newData.hasChildren(['photoUrl']) || newData.hasChildren(['name', 'photoUrl']) && !newData.hasChildren(['text'])"
		 }
	   }
	 }
	}
	
for more infos on rules 

	https://firebase.google.com/docs/database/security/
	
Add sign in

	go back to firebase console
	click on "authentification" menu
	you see Authentifiez et gérez les utilisateurs à partir de plusieurs fournisseurs sans code côté serveur.
	click on "configurer un mode de connexion"
	you get a list
	
for friendlychatapp enable 

	email
	google
	
now let's have a look at the documentaion

	https://firebase.google.com/docs/auth/
	code opensource of Firebase UI : https://github.com/firebase/FirebaseUI-Android
	
I use firebase 11.0.1 (cf gradle  compile 'com.google.firebase:firebase-database:11.0.1') so according to ... page I will need to install fireabase version ...

	https://github.com/firebase/FirebaseUI-Android
	2.0.1
	
now go to ... and click ...

	https://github.com/firebase/FirebaseUI-Android
	auth

and read the readme for auth and add dependencies

	Adapt this to the correct versions
	https://github.com/udacity/and-nd-firebase/compare/1.03-firebase-database-read...1.04-firebase-auth-firebaseui-signin
	https://github.com/udacity/and-nd-firebase/compare/1.04-firebase-auth-firebaseui-signin...1.07-firebase-auth-firebaseui-sign-out
	add this com.google.firebase:firebase-auth:11.0.1 (for a list of firebase libraries go to https://firebase.google.com/docs/android/setup)
	add this  compile 'com.firebaseui:firebase-ui-auth:2.0.1' from https://github.com/firebase/FirebaseUI-Android/tree/master/auth
	as said before my firebase version 11.0.1 should match firebase UI 2.0.1: Cool

add the sign in and sign out(trigger when the user authentication change state (sign in or log out))

	send unauthenticated users to sign in flow
	make UI that reflect if user is login or log out
		- if log in : 
			use their names when they are writting messages
			attache the database read liteners, because an unauthenticated user doesn't have permission to read from the database
		- if sign out 
			unsave the user name
			detached database listeners
			clear message list
			open sign in flow again
			
	see commit 'add AuthStateListener', 'finish add sign in', 'Add sign out' of my repo C:\ProgrammingProjects\AndroidStudioProjects\Examples\FriendlyChatApp

test the app when 

		user sign in
		user sign out
		attached to firebaseAuth

you should see 
		
	the first screen is now firebase UI, and it is smart enough to let you create an user.

now go to firebase console auth tab
	
	you should see all user connected 
	
now we will add Firebase storage. 

	Go to the console and select the "storage" tab. Nothing appears yet.
	Cliquer sur "premier pas". Un message de conseil sur la sécurité apparait. Cliquer OK. L'écran principal apparait.
	Cliquer sur l'icone "Créer un dossier" et créer le dossier "chat_photos"
	
in android studio

	add firebase storage dependency : com.google.firebase:firebase-storage:11.0.2 
	note to find the last dépendency of any firebase stuff, google "firebase dependencies"and take the first link it should be https://firebase.google.com/docs/android/setup
	
add security go to console>friendlychatapp poject > storage > regles

	service firebase.storage {
	  match /b/friendlychatapp-585e2.appspot.com/o {
		match /{imageId} {
		 // Only allow uploads of any image file that's less than 3MB
		  allow write: if request.resource.size < 3 * 1024 * 1024
					   && request.resource.contentType.matches('image/.*');
		}
	  }
	}
	
cliquer publier. et tester.

	l'image récupérée devrait être visible dans storage > fichier
	ce n'est pas mon cas. Il faudrais investiguer un peu plus.
	
je n'ai pas fais la suite du tuto.

	j'ai juste regardé les vidéos.
	il faudrais les reprendre à partir de Notifications et jusqu'à la fin
	https://classroom.udacity.com/courses/ud0352/lessons/fab5bf81-cfe5-4071-9afe-b6eb324a6257/concepts/3949ce9a-6eb1-4f8b-bc31-42f34f25297e
	https://github.com/udacity/and-nd-firebase/compare/2.03-firebase-notifications-set-up...2.04-firebase-remote-config-default-values

	
	
	


	
	
	

		




	
	




	


	
