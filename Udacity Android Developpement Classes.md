
## 1 Android Developpement For Beginners##
        


Fond vert :https://www.youtube.com/watch?v=nrSdUNeY7AM
Hands Gestures with Chroma Key
See also : 
https://blog.udacity.com/2014/09/udacity-videos-transparent-hand.html
https://blog.udacity.com/2012/05/katy-reichelt-on-video-editing-and.html


## 2 How to use Git and GitHub##

Comparer des fichiers automatiquement : 

Windows : FC (file compare)
Linux or Mac : Diff (difference)


FC game_old.js game_new.js
diff -u game_old.js game_new.js


cd ~                          # change directories to your home directory
mkdir version-control         # make version-control directory
cd version-control            # go to version-control directory
mkdir reflections             # create reflections directory
cd reflections                # go to reflections directory
subl lesson_1_reflections.txt # launch sublime with file called lesson_1_reflections.txt (you can replace subl with another editor here if you prefer a different one)
pwd # print working directory shows what directory you are in
ls  # list the files in this directory


Installer Sublime
https://www.udacity.com/wiki/ud775/sublime

ls C:/Program\ Files/Sublime\ Text\ 2
echo 'alias subl="C:/Program\ Files/Sublime\ Text\ 2/sublime_text.exe"' >> ~/.bashrc
source ~/.bashrc

git log   #donne l'historique des commit, l'id, l'auteur, la date, le commentaire
git id_commit1 id_commit2 donne les différences entre les 2 commits.
  en noir les lignes qui n'ont pas changées
  en rouge les lignes supprimées
  en vert les lignes ajoutées
 
A good rule of thumb is to make one commit per logical change. 

git log --stat #cool pour voir uniquement les fichiers du repository qui ont changés.

git --version

git clone https://github.com/udacity/asteroids.git  #permet decopier tout le repository cad avec toutes les versions et les commits

git config --global color.ui auto faire en sorte que sur tous nos repository les affichage des changement se fassent avec des couleurs différentes.

git checkout pour revenir à une ancienne version qui marche.

open a file

vim game.js


ls -a pour voir les fichiers cachés


git init #cree un .git dans le repertoire ou on est
git status #shows withch files have changed since the last commit

git add #add to staging area. Put here only file that have something in common.

git commit # the editor you have chosen appears as soon as you run this command and you can write your message

or

git commit -m "Commit message"

commit message style guide :http://udacity.github.io/git-styleguide/

In vim there are 3 different modes:

Insert allows typing and editing as normal
Visual used for selecting copy/paste etc.
Normal used for commands
To get back to Normal mode, you can always press esc.

Once you are at Normal mode Press : to begin your command (you'll see it appear in the bottom left). The following commands are related to quiting vim:

:q quit if no changes were made
:q! quit and destroy any changes made
:wq write changes (save) and quit
:x similar to :wq, only write the file if changes were made, then quit


git diff with no argument, compare what you have put to thestaging area to your current directory

git diff --staged to see the differnce between the last commit and the staging area.

git reset --hard discard any change made to the staging area or the current directory. But be very careful you can lose some work.


git checkout master (if head detached)


git branch #show the current branches

git branch easy-mode #create a branch easy mode en copiant le code qu'il y a sur la branche master
git checkout easy-mode

git log --graph --oneline master easy-mode #pour avoir une visualisation graphique des branch mises en parametres.


When we are in "detached head" les commits ne sont pas accessible à moins qu'on note leur id ou qu'on crée une branche. En effet git log, list des commit qui sont sur la branche ou on est, les commit qui ne sont pas sur une branche ne sont pas listés.

git checkout -b new_branch_name # + integre le commit qui est "hors branche" et sur lequel on est

equivaut à 

git branch new_branch_name
git checkout new_branch_name


merging the "coin branch" into the master branch.
git merge master coin #+ enter a commit messge for the merge commit

cool mais ça "mixe" les commit de la branche master avec la branch coin en les rangeant par timestamp.
Le parent d'un commit n'est plus celui qui vient juste avant. On ne peut donc plus faire un git diff avec le commit precedent pour voir le changement introduit. Il faut faire à la place : 

git show <id> #montre les difference entre un commit et son parent

une fois la branch "coin" mergée on peut la supprimer (Attention: faire la commande ci-dessous avant  d'avoir mergé, peut faire perdre toutes les references au commit de la branche, seule l'etiquette est detruite, les commit ne sont pas détruit mais on a plus de moyen pour les retrouver).

git branch -d coins


online UML diagrams : 
https://www.gliffy.com/
http://yuml.me/diagram/nofunky/activity/samples

git merge master easy-mode
CONFLICT (content): Merge conflict in game.js
Automatic merge failed; fix conflicts and then commit the result.

Ce message veut dire les branches master et easy-mode ont modifié les m^me choses, et donc il ne sait pas quoi prendre

git status done : 
On branch easy-mode
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   game.js

no changes added to commit (use "git add" and/or "git commit -a")

"both modified:   game.js" veut dire une fois de plus sue les branches master et easy-mode ont modifié les m^me choses, et donc il ne sait pas quoi prendre.

Que faire : 

editer game.js
chercher 

		<<<<<<< HEAD
		something
		=======
		something else
		>>>>>>> master

modifier le code
sauvegarder le fichier

Puis : 

$ git add game.js
$ git commit -m "resolve conflict in easy-mode"
$ git merge master easy-mode


Merge: bdb89c7 98491aa
Author: Elorri <etchemendy.elorri@gmail.com>
Date:   Mon Sep 14 11:45:03 2015 +0200

    Merge branch 'master' into easy-mode

    Conflicts:
        game.js

git log -n1 #show only 1 commit



Famous opensource projects on GitHub

mathquill
ipython
bootstrap
jquery
atom text editor design for diting code and allow user to customize their experience


Git can be use without the website
GitHub can't

use git for your private copy

github free for something you want to share and that can be open source
github pay for something you want to share and that can't be open source


Pour mettre sur github un repertoire qu'on a crée : 

git remote
git remote add origin https://github.com/Elorri/reflections.git (origin is the standard name, if you have only one remote)
git remote -v #pour verbose montre 2 URL
the url where I will get data from (fetch)
the url where I will push data to (push)
in most cases it is the same url.

git push origin master #ne copie sur GitHub (the remote cad origin) que la branche master, s'il y a d'autres branches elles ne sont pas copiées.

git pull origin master #Si on ajoute un fichier sur GitHub.

ajouter un collaborateur sur un repository : 
Settings(à droite)>Collaborateurs (à gauche)

bash sarah_changes.sh https://github.com/Elorri/recipes.git

Si le m^me fichier a été modifié localement et sur GitHub la commande : 
git pull origin master fait : 
git fetch origin suivi de git merge master origin/master
cf Lesson 3: https://www.udacity.com/course/viewer#!/c-ud775/l-3105028581/e-3352618815/m-3349118635


git fetch origin #update locale copie avec ce qu'il y sur le remote cad origin cad GitHub
git diff origin/master master 

nb: origin/master is the serveur master branch

git merge master origin/master
change the conflict
git add chili-recipe.txt


git branch different-oil
git checkout different-oil
git add cake-recipe.txt
git commit
git push origin different-oil

Show changes to somebody. Pull request to somebody
go to the branch
select "Pull request"
change the "base fork" to whoever you want
click on "create pull request"

To see our pull request
go to the right of the repository
click on "Pull request"

bash sarah_changes_2.sh https://github.com/Elorri/recipes.git


Reflexions que je trouve interessante :
You just saw that the workflow when making changes in a separate branch is more complicated than working directly in master, especially when you need to stay up-to-date with changes others are making. Rather than simply pulling and pushing, you need to pull changes into your local master branch, merge the local master into your branch (different-oil, in our case), then push your branch to the remote before finally merging your branch into master, either locally or on GitHub.


origin upstream etc see last video of Lesson3 https://www.udacity.com/course/viewer#!/c-ud775/l-3105028581/e-3306849568/m-3315478816



If you want to revert changes made to your working copy, do this:

git checkout .
If you want to revert changes made to the index (i.e., that you have added), do this:

git reset
# Warning this will reset all of your unpushed commits to master!
If you want to revert a change that you have committed, do this:

git revert ...
If you want to remove untracked files (e.g., new files, generated files):

git clean -f 
Or untracked directories:

git clean -d


More on git :

git dash :if you want to move branches but don't want to commit your unfinished work
	https://git-scm.com/book/en/v1/Git-Tools-Stashing

## 3 Developping Android App##


# Lesson 1


APK = application package

le .apk est signé par jarSigner et est donné à ADB

ADB permet de communiquer avec le materiel physique.

Ctrl + un lien vers le fichier est crée sur android studio.


NB : dans Sunshine, le fait de devoir faire un fm.replace(frag) nous oblige à ne pas pouvoir déclarer lefragment dans un fichier xml et a utiliser un framelayout à la place.


# Lesson 2


http://openweathermap.org/API
meteo

Log
Verbose : should never be used except when in developement
Debug : are compiled mais sont invisible at runtime
Error : 
Warn : 
Info : 
1er parametre : en general, le nom de la classe ou le nom de l'appli
2eme parametre : le messgage

Le main thread est fait pour les choses principales : display UI, user input, output. PAS DE LONGUES OPERATIONS
Background thread for long running tasks : 
network calls
decoding bitmaps
reading and writing from the database

The result of the background thread should come back to the main thread : this is call synchronisation

Downloading an image from an URL

         Bitmap b = loadImageFromNetwork("http://example.com/image.png");
            mImageView.setImageBitmap(b);
			
Mais ceci n'est pas conforme avec le fait que seul le main thread doit manipuler l'UI.
Android propose donc plusieurs methodes pour manipuler l'UI à partir de thread speciaux : 

Activity.runOnUiThread(Runnable)
View.post(Runnable)
View.postDelayed(Runnable, long)

L'example plus haut devient donc : 
         final Bitmap bitmap =
                    loadImageFromNetwork("http://example.com/image.png");
            mImageView.post(new Runnable() {
                public void run() {
                    mImageView.setImageBitmap(bitmap);
                }
				
More details here : http://developer.android.com/guide/components/processes-and-threads.html


AsyncTasck permet de simplifier tout ça : 
public void onClick(View v) {
    new DownloadImageTask().execute("http://example.com/image.png");
}

private class DownloadImageTask extends AsyncTask<String, Void, Bitmap> {
    /** The system calls this to perform work in a worker thread and
      * delivers it the parameters given to AsyncTask.execute() */
    protected Bitmap doInBackground(String... urls) {
        return loadImageFromNetwork(urls[0]);
    }

    /** The system calls this to perform work in the UI thread and delivers
      * the result from doInBackground() */
    protected void onPostExecute(Bitmap result) {
        mImageView.setImageBitmap(result);
    }
}


AsyncTask<String, Void, Bitmap> les 3 parametres sont : 
AsyncTask<Type that will be pass to the doInBackground methode, Type of object that you get when you get progress update when the task get executed, if you don't use it put void, Type of result that we will send back to the main thread throw the onPostExcecute methode>


Important methodes de AsyncTask :   thread dans lequel il s'execute Main (M) or Background (B)
onPreExecute() :(M)
doInBackGround() obligatoire :(B)  can call publishProgress() qui donne des infos à l'UI comme le % de travail effectué. Ap publishProgress, onProgressUpdate sera toujours appelé et c'est là qu'il faut mettre à jour notre ProgressBar
onProgressUpdate() :(M)
onPostExecute() :(M) Quand toutes les actions sont effectuées, onPostExecute est appelé. 


A good app should give you what you want before you know you want it. The app should always be up to date and sync to the cloud. The user shouldn't have to press the refresh button.

Le pb avec cette facon de creer des background thread c'est qu'ils sont attaché à une activité ou à un elelement (view) de l'activité. Si l'activité se termine par exemple lors d'une screen rotation, le (B) se termine aussi.
AsyncTasck should only be used for task : 
that will terminate when activity terminate.
and excepted to run only 1 second or 2 second.

On mobile ce n'est pas sage de penser qu'un access au réseau (meme le plus simple) va se passer rapidement. Il est donc preferable d'utiliser un Service.

Service = un composant qui ne depend pas de l'UI. Il peut être scheduler (=synchroniser ou parle aussi de background data sync) :
à intervales + ou regulier avec une InexactAlarm 
ou mieux avec un SyncAdapter (specifique à Android)

SyncAdapter synchronise your background data sync as efficiently as possible. Le mieux pour lui "parler" et d'utiliser "Google Cloud Messenging"
Google Cloud Messenging ne fera la synchronisation que si quelque chose à changé, si rien n'a changé sur le serveur de données, pas la peine de perdre son temps.


<string name="refresh" translatable="false">Refresh</string>
Dans le fichier string à traduire, si translatable="false", la personne qui traduit peut ne pas traduire l'élément.
Egalement utile si le string qui est inscrit, est utilisé comme clé constante, pour retrouver un element, comme dans SharedPreferences


SecurityException : happens when internet permission denied.

Each app cad .apk is given its unique user-id
Each app run within an instance of an Android virtual machine

As a result each app is completely sandbox : it's files, precesses, and others ressources are inaccessible to other apps, they can't perform actions that will affect others app, the OS or users. As a consequence they can't : 
access internet
get user location
read or modify the context database

Rather than ascking the user each time if the app can access something sensitive you declare user permissions that the app requiere in its manifest.

Best practice isto request the absolute minimum permissions : 
is there alternative to ask a permission ? like using an intent to launch the camera rather than accessing the camera directly. And then sharing data with app sandboxes using Intent and ContentProvider to create bridges.

Actions qui necessitent a user-permission in the manifest.
taking a photo : No possible mais pas necessaire, on peut utiliser une app system comme intermediaire, cad aller voir ce que l'utilisateur a renseigner par defaut dans ses settings.
making a phone call : No possible mais pas necessaire, on peut utiliser une app system comme intermediaire
getting the user current location :  Yes
accessing user contacts details :  No possible mais pas necessaire, on peut utiliser une app system comme intermediaire


URL vs URI : https://www.udacity.com/course/viewer#!/c-ud853/l-1469948762/e-1630778633/m-1630778636

Pour visualiser mieux les données à extraire  :
https://jsonformatter.curiousconcept.com/


JSon JUnit test-case
https://www.udacity.com/course/viewer#!/c-ud853/l-1469948762/e-1630778641/m-1226659448


Ctrl-o pour avoir une liste de methodes qu'on peut "overider".
Maintenant qu'on a une liste de String provenant du serveur, grace à AsyncTask, il faut mettre à jour l'UI. Pour cela : 
adapter.clear()
adapter.add() dans une boucle for ou adapter.addAll() sera plus efficient
cf /c/ProgrammingProjects/AndroidStudio/Udacity/Sunshine commit "Add forcast data from internet (her version)"

ArrayAdapter + ListView :
Changer toute la liste d'élément de l'adapter: 
adapter.clear()
adapter.addAll() 
Ajouter/Supprimer 1 ou plusieurs element à la liste.
adapter.add()


Adapter (not Array) + ListView :
Changer toute la liste d'élément de l'adapter: 
adapter.clear()
adapter.addAll() 
Ajouter/Supprimer 1 ou plusieurs element à la liste.
adapter.add()
adapter.notifyDataSetChange()

ArrayAdapter internally call notifyDataSetChange when we add or remove an element, no need to do it.


Samsung Galaxy S5 screenshot : 
Power + Home button at the same time. On les retrouve dans les photos (Photo App) google+ ?
Passer sa main comme une photocopieuse.


Nb :MainThread = UI Thread

July 2015, 1.5 million Android devices are activated everyday

Ctrl+Q pour ouvrir la javadoc


# Lesson 3


setOnClickListener(View.OnClickListener l) sur la listView : listen for clicks on the whole list, not just one item.
setOnItemClickListener(AdapterView.OnItemClickListener l) : that's the one we want.


Explicit Intent : explicitly specify name of the recipient :cad the name of the class
Implicit Intent : no recipient specified mais an action we would like an activity to perform and on what data that action should be performed. Exple :an activity capable of viewing a website, an activity capable of making phone calls, an activity capable of choosing a contact from your adress book. NB: l'activité en question peut ne pas faire partie de notre appli, mais quand m^me répondre aux critères. 
For a list of implicit Intent go to : http://developer.android.com/guide/components/intents-common.html

Don't make everything a setting. 
It always possible to add the setting later. So start without.
UX = User Experience

Les settings contiennent
headers des titres
preferences
value of preferences = preference summary = looks like a subtitle text.

Common preference types are  : 
CheckBoxPreference
ListPreference
EditTextPreference
 When the user changes a setting, the system updates the corresponding value in the SharedPreferences file
 
 If you support Gingerbread you need a PreferenceActivity class
 If you support Honeycomb or later you need a PreferenceFragment class 
 Pour rendre le projet utiliser les ce que l'IDE genere quand on selectionne new "Settings Activity". C'est une combinaison de PreferenceActivity et PreferenceFragment.
 
 
 Dans pref_general.xml
     <EditTextPreference
        android:key="@string/pref_location_key"    //la clé de la SharedPreference. Ici un String "location"
        android:title="@string/pref_location_label" //le titre devant le texte que doit rentrer l'utilisateur ici "location"
        android:defaultValue="@string/pref_location_default" //la valeur par défaut
        android:inputType="text"
        android:singleLine="true"/>
		

Dans le onCreate du SettingsActivity extends PreferenceActivity
        // Add 'general' preferences, defined in the XML file
       addPreferencesFromResource(R.xml.pref_general);

        // For all preferences, attach an OnPreferenceChangeListener so the UI summary can be
        // updated when the preference changes.
        bindPreferenceSummaryToValue(findPreference(getString(R.string.pref_location_key)));


If we don't want to refresh our app manually, we can make a call in the onStart method of the fragment, that way the fragment will be refreshed, the content of the fragment too.
    @Override
    public void onStart() {
        super.onStart();
        updateWeather();
    }
	

Interessant : La listView qui est peuplée grace à l'ArrayAdapter, est peuplée au démarrage par un ArrayAdapter vide. Cad :
        String[] forcastsArray = {"Today Sunny 88/63", "Tomorrow Foggy 70/46", "Weds Cloudy 72/63", "Thurs Rainy 64/51", "Fri Foggy 70/46", "Sat Sunny 76/68"};
        mWeekForcast = new ArrayList<>(Arrays.asList(forcastsArray));
		
		devient : 
		
		mWeekForcast = new ArrayList<>();
		
Bref, elle est qd même initialisée avec qqc. On attends pas d'avoir des données pour l'initialiser.





Uri buildUri = Uri.parse(FORECAST_BASE_URL).buildUpon()
                        .appendQueryParameter(QUERY_PARAM, params[0])
                        .appendQueryParameter(FORMAT_PARAM, format)
                        .appendQueryParameter(UNITS_PARAM, units)
                        .appendQueryParameter(DAYS_PARAM, Integer.toString(numDays))
                        .build();
						
Implicit Intent (suite).
Comment notre activité sait que l'app google map par exemple, peut ouvrir notre location ?
Parce que Google Map contient dans son manifest ceci : 
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
				<data android:scheme="geo" />
            </intent-filter>
Cela veut dire que Google Map est capable de faire cette ACTION_VIEW sur toute data avec un "geo" scheme/type

Concusion dans le <intent-filter> mettre : 
les actions que notre app is capable of performing
le type de donnée sur lequelles elle peut agir (ceci est optionnel)

Most used Implicit Intent : the SHARED=SEND intent.
What to share ? 
Photos
Text
Videos
links
And you don't have to know what app the user will use to open those shares.


    private Intent createShareForecastIntent() {
        Intent shareIntent=new Intent(Intent.ACTION_SEND);
        shareIntent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET); 
        shareIntent.setType("text/plain");
        shareIntent.putExtra(Intent.EXTRA_TEXT, mForecastStr+" "+FORECAST_SHARE_HASHTAG);
        return shareIntent;
    }

NB : shareIntent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET); //permet d'eviter que l'activité qui va se lancer (autrement l'activité de l'appli qui correspond à l'implicit intent) soit ajoutée au backstack de notre appli actuelle. Et que donc, si l'on met en veille notre activité, et qu'on la relance, on ne tombe pas sur une appli qui n'a rien à voir.


To send a message to many apps, example, the system say "I'm in charge" or "Download completed" or "stop internet connectivity".
You use sendBroadCast method to broadcast an Intent. This broadcast message is receive by a broadcast receiver called assymply receivers. cf https://www.udacity.com/course/viewer#!/c-ud853/l-1474559101/m-1631278613.
Those apps that are broadcast receiver will set their manifest with a specifique <intent-filter>.

Exemple of receiver could be an app that will display all the newletters of the app you have that send a newsletter.

To create a receiver : 

public class MyReceiver extends BroadcastReceiver{
	@Override
	public void onReceive(Context context, Intent intent){
		//Handle received intent
	}
}

A receiver is a lightweight component that should do very simple task in a few second. Usually : 
they listen for broadcast
And then
they start a service or 
send a notification

To have your receiver listening for broadcast, you need to register it.
in the Manifest

        <receiver
            android:name=".MyReceiver">
            <intent-filter>
                <action android:name="com.myApp.NEWLIFEFORM" />
            </intent-filter>
        </receiver>
		
or in an activity with the fonction : 

IntentFilter intentFilter=new IntentFilter("com.myApp.NEWLIFEFORM");
registerReceiver(myReceiver, intentFilter);

cf Android BroadcastReceiver within Activity Stack Overflow.pdf que j'ai enregistré dans le dossier Ressources.

A dynamic (Activity) declared receiver, will only receive broadcast when it is running.
A Manifest declared receiver, will always receive broadcast, means if it is not running, it will be started.

Example : 
a music app will be better register a "runtime receiver" that will listen the system broadcast intent announcing the headphone are plugged. That way the app can switch play/pause button to pause when audio goes from headphone to speakers.
if I use Google Cloud Messaging to listen from new data from my server, better use the manifest.

For a list of broadcast action event intent see
http://developer.android.com/reference/android/content/Intent.html and search "Standard Broadcast Actions"
here are a few:
ACTION_BATTERY_CHANGED
ACTION_POWER_CONNECTED

These days, to make app available for the crowd. Speed is not the most important. It is quality.
App quality guideline : http://developer.android.com/distribute/essentials/quality/core.html



AdapterView : When the content for your layout is dynamic or not pre-determined, you can use a layout that subclasses AdapterView to populate the layout with views at runtime. 
Most famous of AdapterView : 
ListView
GridView

AdapterView should be bind to an Adapter.
Most famous Adapter are : 
ArrayAdapter  works only with textView cad String. Data : un ArrayList<String> en arguments.
SimpleCursorAdapter works if data come from the database. Data : un Cursor.




# Lesson 4.A


Your app isn't in control of its own destiny.It can be killed at any times.

onCreate ->Created
onStart  ->Visible
onResume ->Active (=have focus) receive imput from user no others activity are obscuring it
onPause  ->Inactive (= have lost focus)
onStopped ->Invisible
onDestroy ->Doesn't exist
onRestart ->Visible


The Active Lifecycle :
	oscille entre states : active|inactive	onResume|onPause|onResume

	Qd un implicit intent est appelé, l'activité est mise inactive (onPause), et un choix est demandé à l'utilisateur, l'activité est cependant toujours partiellement visible.
	Qu'est ce qu'on peut stopper ?
	tout ce qu'on veut except les processus qui dessinent l'UI.
	
The Visible Lifecycle
	oscille entre states : Visible|active|inactive|Invisible|Visible	onStart|onResume|onPause|onStop|onRestart
	qd on stopped est appelé on sait que l'utilisateur ne voit plus notre appli.


When we change the orientation of the phone what lifecycle can be called ?
	Actif|Inactif|Invisible|Doesn't Exist|Exist|Visible|Actif

When we push the "Home" button, launch a light app and onpen the app again ?
	Actif|Inactif|Invisible|Visible|Actif
	
When we push the "Home" button, launch a heavy app and onpen the app again ?
	Actif|Inactif|Invisible|Doesn't Exist|Exist|Visible|Actif

When app death can happen before HoneyComb?
	Inactif
	Invisible
	Doesn't Exist
	=> il faut se preparer à une app death aussi tot que possible cad dans le onPause 

When app death can happen after HoneyComb?
	Invisible
	Doesn't Exist
	=> il faut se preparer à une app death aussi tot que possible cad dans le onStop
	
As soon as onStop is called (or onPause for preHoneyComb) we must be aware that the app may not come back to life, hence we need to clean any heavy ressource like : 
	open connection
	open socket
	anything that uses a lot of battery
	anything that update the UI
	sensor listeners
	location updates
	dynamic broadcast receivers
	game physics angine

Any tasks that should continue to be even if the activity crash, shoudn't be call in the activity at all.


When is called onSaveInstanceState ?
	immediatly after onPause and it's the same for preHonnecomb

When is called onRestoreInstanceState ?
	immediatly after onCreate but only if the app had been terminated by the system.

Battery life : 
	using ondes radio especially cellular radio is detrimental.

A good app should
	avoid reducing battery life
	avoid network overload
	be still fonctionning when no network access
	
Tuto on SQLite
https://www.udacity.com/course/viewer#!/c-ud853-nd/l-3621368730/m-2602608541
More info on data storage : http://developer.android.com/guide/topics/data/index.html


Contract class : contains thedb description
example :http://developer.android.com/reference/android/provider/ContactsContract.ContactsColumns.html
This contract contains : 
column names
columns for flags
columns for ids (used to link to other tables)
coulmns for URI that pointed to URI associated with contacts

nb : boolean isThis isThat are called flags


SQLiteOpenHelper
permet de créer une database
permet de gerer les différentes versions de la base en nous aidant à modifier nos tables. Permettra donc de faire passer notre app d'une version A à une version B plus récente, cad d'UPGRADEr la base de données.

Each time you realease a new app apk that uses a new database schema, the DATABASE_VERSION should be manually updated.
private static final int DATABASE_VERSION = 2;
		static final String DATABASE_NAME = "weather.db"; // the name of the db file

The first time the database will be use onCreate will be called


Android has a built in testing framework that allows us to create a test .apk that execute junit test that call the classes of our main apk.

When you extends extends AndroidTestCase you can 
implement the setUp method : which will be run before we test.
implement tearDown() : which will be run after each test.

Similar to junit test, you simply add new methods in the class with the prefix "test". example : testThatDemonstratesAssertions. Si le test echoue une exception est levee.


The FullTestSuite contains code to include all the java test classes of its package that will be given to Junit to execute. It is done  thnak to the includeAllPackagesUnderHere method. As a consequence just adding java class to the test directory is enough to have those classes tested.
You can literaly copy this one class in all your projects.


onUpgrade is called when the database has already been created but version has changed.
When change the version when, the columms, or db schema has change. 
Allways change the databse version when you make changes in the database table.

Since we are going to use the db as a cache and not for user insert content, we can do "DROP TABLE IF EXISTS" in the onUpgrade, et aucun donnée ne sera perdues parce qu'elles sont TOUTES initialement prise sur le net.

Si l'utilisateur avaient ajouté des donnés entre temps, on aurait fait ici plusieurs ALTER TABLE.
https://www.sqlite.org/lang_altertable.html


in the TestDB ce qui doit etre verifié est : 
est-ce la db est bien constrite
is writting in it working ?
is reading from it working ?

1. get an instance of your SQLite object : 
	if you read and write
	SQLiteDatabase db = new WeatherDbHelper(this.mContext).getWritableDatabase();
	
	if you only read
	SQLiteDatabase db = new WeatherDbHelper(this.mContext).getReadableDatabase();
	
2. Create ContentValues objects for tables you want to test.
	to represent the row of data we want to insert into the db, we use a ContentValues object
		the key is the name of the column of you table
		the value : put what you want
		ContentValues weatherValues = new ContentValues();
        weatherValues.put(WeatherContract.WeatherEntry.COLUMN_DEGREES, 1.1);

3. Insert ContentValues objects and get the row_id. (nb -1 if pb)
	    long locationRowId;
        locationRowId = db.insert(WeatherContract.LocationEntry.TABLE_NAME, null, testValues);
		
		// Verify we got a row back.
        assertTrue(locationRowId != -1);
	
4. Query the db and receive the Cursor back

Query SQLite functions:
	Select * from weather;
		query(WeatherEntry.TABLE_NAME, null, null, null, null, null, null);
	Select short_desc from weather;
		query(WeatherEntry.TABLE_NAME, new String[]{WeatherEntry.COLUMN_SHORT_DESC}, null, null, null, null, null);
	Select short_desc from weather where date > 1419019200;
		query(WeatherEntry.TABLE_NAME, new String[]{WeatherEntry.COLUMN_SHORT_DESC}, WeatherEntry.COLUMN_DATE+">?", new String[]{"1419019200"}, null, null, null);
	Select short_desc from weather where date > 1419019200 order by date desc;
		query(WeatherEntry.TABLE_NAME, new String[]{WeatherEntry.COLUMN_SHORT_DESC}, WeatherEntry.COLUMN_DATE+">?", new String[]{"1419019200"}, null, null, WeatherEntry.COLUMN_DATE+"DESC");
		
	// Verify the cursor contains something
     assertTrue( "Error: No Records returned from location query", cursor.moveToFirst() );
		
En utlisant les "bind parameters" cad le "?", on pourra facilement changer la selection + tard. Et c'est + performant.

5. Validate the Cursor values with the original ContentValues


6. Close cursor and db when finished


# Lesson 4.B


Why use content providers ?
because it allows you to share your data safely and efficiently accross app boundaries by abstracting the underlined data source (SQLite, files, dynamic runtime data, etc...). Others apps communicate with the content provider not with the data source.
it allows to swich easily data source, from an SQLiteDB to Json or XML
allow many apps to access, use, and modify data source

ContextDB, MediaStore, Calendar, SMS, Contact API works that ways using Shared ContentProviders.

All Frameworks (Widgets, Search Widget, Google Play Store, Gmail Widget) uses ContentProviders for managing their data.

There is a bunch of API (SyncAdaptors, Loaders, CursorAdapters, ) design to optimize the process of : 
syncing data
querying data
updating UI automatically when the underlying data change

Building a content provider involve severals steps : 
1 Determines the URI your app will support
2 Update Contract
3 Fill out URIMatcher
4 Implements the 6 ContentProviders functions


URI universal ressources identifiers
content://com.example.sunshine/weather/94043

Content URI : content://user_dictionary/words
always start with a scheme that identify the protocol 'content://' content means ContentProvider
followed by the content authority (it must be an unique String typically the package name of the app): 'user_dictionary'  this is the keyword to contact the correct content provider
the location (typically the name of the database)
followed by the query witch can take the form of
	a traditional path : content://com.example.sunshine/weather/94043/1435103000
	a traditional query : content://com.example.sunshine/weather/94043?date=1435103000
	
The ContentProvider data changes (usually done in another thread that does db update routine) are observed by a ContentObserver.
mContext.getContentResolver().registerContentObserver(LocationEntry.CONTENT_URI, true, tco); pour enregistrer un observer
getContext().getContentResolver().notifyChange(uri, null); notify a change in the db to the ContentObserver;
mContext.getContentResolver().unregisterContentObserver(tco); pour le deenregistrer cf class TestProvider.

		

A ContentProvider return either
a list of items :Cursor
a simgle item

Android provide support for appending an id to the URI path.


Building a content provider involve severals steps : 
1 Determines the URI your app will support
		URI that are useful for the app when creating the db.
			content://com.example.sunshine/weather/ (directory)
			content://com.example.sunshine/location/ (directory)
		URI that will be used to display somethings
			content://com.example.sunshine/weather/94043 (directory)
			content://com.example.sunshine/weather/94043/1435103000 (item)

2 Update Contract
		Put in the URIs
3 Fill out URIMatcher
4 Implements the 6 ContentProviders functions



Cursors returned from a ContentProvider have unique type base on
their content
the base path


Android use something similar to describe the MIME type returned by an URI.
Cursor that return more than one item are prefixed by : CURSOR_DIR_
Cursor that return more than one item are prefixed by : CURSOR_ITEM_


1 Determines the URI your app will support
2 Update Contract and test WeatherContract class
3 Fill out URIMatcher and testWeatherProvider class
ContentProviders implements 4 types of URIs : each one excecute different type of operations against the SQLite database.
Each URI type is tied to an Integer constant.
"PATH" matches "PATH" exactly
"PATH/#" matches "PATH" followed by a number
"PATH/*" matches "PATH" followed by any string
"PATH/*/OTHER/#" matches "PATH" followed by a string followed by a number

    static final int WEATHER = 100;
		content://com.example.sunshine/weather/ (directory)
    static final int WEATHER_WITH_LOCATION = 101;
		content://com.example.sunshine/weather/94043 (directory)
    static final int WEATHER_WITH_LOCATION_AND_DATE = 102;
		content://com.example.sunshine/weather/94043/1435103000 (item)
		content://com.example.sunshine/weather/94043?date=1435103000
    static final int LOCATION = 300;
		content://com.example.sunshine/location/ (directory)

4 register the content provider in the manifest (also called PackageManager)
<provider
	android:authorities=[content authority]
	android:name=[content provider class]
/>
       <provider
           android:authorities="com.example.android.sunshine.app"
            android:name=".data.WeatherProvider" />

5 Implements the 6 ContentProviders functions

Now that the content provider is register, we can create a content resolver and use it (the provider).
ContentResolver fonctions are 
	onCreate
	Read from the data --> query (Uri, String[], String, String[], String)
	Add to the data --> insert (Uri, ContentValues)
	Change préexisting data --> update(Uri, ContentValues, String, String[])
	Delete from the data --> delete(Uri, String, String[])
	getType(Uri)
	bulkInsert (optional method)
	
ContentProvider founctions are the same. We have to implement them.

getType
	getType return the MIME of the Uri, meaning return if the Uri return an item or a directory, could also return "text/plain", or "image/jpeg" it all has to do with the type of data returned by the query.			
query
	The setNotificationUri() method of the query method cause the cursor return by the query to be aware of the changes that have appenned in the db.
	A noter :
	les jointures (sWeatherByLocationSettingQueryBuilder.setTable) et 
	les selections (sLocationSettingSelection et sLocationSettingWithStartDateSelection)
	sont enregistrée dans le Provider sous forme de variables statiques.
	ContentResolver.query -> ContentProvider.query -> SQLQueryBuilder.query (use of setTable fct for the join) -> SQLiteDB.query
insert
	needs only to implements the base URI, means the URI that refers to single table and not join. Means in our case : 
    static final int WEATHER = 100; content://com.example.sunshine/weather/ (directory)
    static final int LOCATION = 300; content://com.example.sunshine/location/ (directory)
	return the uri
	IMPORTANT : don't forget to call getContext().getContentResolver().notifyChange(uri, null); to notify any Observer that a change in the db has been done. NB: the uri is the one passed to the insert method, not the one that we will return (eg returnUri)
delete
	needs only to implements the base URI, means the URI that refers to single table and not join. Means idem insert.
	return 
update
	needs only to implements the base URI, means the URI that refers to single table and not join. Means idem insert.
bulkInsert
	puting a bunch of insert in a single transaction is much faster than adding them individually.
	the default implementation just call insert a bunch of time, but we can do better by overriding the method
	ici : il ne faut implementer que l'Uri qui est utilisée ds notre appli pour inserer plusieurs elements à la fois. ici c'est WEATHER. (et pas LOCATION qui insere toujours 1 à 1).
	IMPORTANT : if we don't set transaction to be successful the records will not be committed when we say endTransaction.



Changement par rapport à la lecon 3
FetchWeatherTask n'est plus une inner class
	sa methode : getWeatherDataFromJson en plus de questionner l'API va ajouter les donnée ds la db
	ajout de 2 nouvelles methodes : 
		addLocation()
		convertContentValuesToUXFormat()
	A noter les ajout ds la db se font dans l'AsyncTask cad ds un background thread et c'est ce qu'on veut.
	
	getWeatherDataFromJson grand moments: 
	1 read json String that contains and array of 14 weathers
	2 store ts les weathers dans ContentValues[] (ds ce cas precis c'est un Vector), each contentValue represent a weather
	3 ajoute tout les weathers to the db : bulkInsert(WeatherEntry.CONTENT_URI, ContentValues[]);
	4 read db and get a Cursor: query
	5 convert the Cursor data into a ContentValues[].
	6 convert the ContentValues[] into a String[] we want to display.
	
	BUT would be better to
	query the db before quering the network API (for performance)
	avoid calling queries on the UI thread by using loaders.
	
# Lesson 4.C


Loader have been introduced in HoneyComb but can be used in older platform by using support libraries.
They are : 
best practice implementation for an asynchron task in an activity or fragment.
What does Loaders do ?
1 create an async task = (B) creation = background Thread creation
2 load data on a background Thread (B)
3 synchronize (=brings ) the data to the main thread = ui Thread synchronisation = (M) sync.
And can be set up to deliver upate to the UI on a regular basis.

A Cursor Loader is design to query a ContentProvider and return a Cursor, all of that on an AsyncTask
And the Cursor can than be directly bind the UI. Means : 
Changes to the db => Changes to the ContentProvider => Changes to the ContentLoader => Changes to the UI 
All of this AUTOMATICALLY

Also, the loader know himself how to connect the activity that display the ui to the cursor. That means there is no need to requery data just because the device was rotated.

AsyncTaskLoader is a Loader that uses an AsyncTask behind the scenes to do its work.


Loaders :
are registered in an activity using 
	a LoaderManager
	an their id
can live beyond the lifecycle of the activity or fragment, becausethe LoaderManager make sure that the new activity created is connected with the same loader (grace à son id)

they load data
they bind data (means if the db change they deliver new results)


in project 1, an async task is created first, and if we turn the phone, another async task is created again.
onLoadFinish() est equivalent au onPostExcute() de l'asynctask.

AsyncTask Lifecycle

onCreate
	asyncTask.execute()
		asyncTask.doInBackground()
------------------------------------Activity Restart----------------------------
			onCreate -a new AsyncTask is created
				asyncTask.execute()
					asyncTask.doInBackground() -2 (B) are running parallel. Will take a long time for the user to see updates
--------------------------------------------------------------------------------	
						asyncTask.onPostExecute() le premier (B) a fini. UI is updated.
						

AsyncTaskLoader Lifecycle

onCreate	
	initLoader()
		onCreateLoader()
			loadInBackground()
------------------------------------Activity Restart----------------------------
				initLoader() -le LoaderManager de l'activité "crée" un nouveau Loader mais qui se connecte au trhread existant.Il lui dit donc de ne pas réappeler onCreateLoader() et loadInBackground().
					onLoadFinished() -(B) a fini. UI is updated.
					
AsyncTaskLoader Lifecycle (2) 
I don't know what's happen in this case : the ui has been updated before activity restart. I guess there is a crash or loadInBackground() is called again and we have to use CursorLoader for better performance.

onCreate	
	initLoader()
		onCreateLoader()
			loadInBackground()
				onLoadFinished()
------------------------------------Activity Restart----------------------------
				initLoader()
					loadInBackground() ???
						onLoadFinished() -(B) a fini. UI is updated.
						
						
						
AsyncTaskLoader Lifecycle (3) 
Maybe onLoadFinished() appelé 2 fois alors que ce n'est pas necessaire.

onCreate	
	initLoader()
		onCreateLoader()
			loadInBackground()
				onLoadFinished()
------------------------------------Activity Restart----------------------------
				initLoader()
						onLoadFinished() -(B) a fini. UI is updated.
					
					
CursorLoader Lifecycle --derived from AsyncTaskLoader but with some optimisation

onCreate	
	initLoader()
		onCreateLoader()
			loadInBackground()				
------------------------------------Activity Restart----------------------------
				initLoader()
					onLoadFinished() -le cursor est directement delivré à l'ui sans reloader les infos.
					

Disavantages of calling the db from the ui (M)?
framerate drop => too much time to see something apparing for the user = no interactivity

Pour le moment (les classes impliquées dans le retour sont identiques aux classes de départ ) :
Android UI demande -> ContentResolver -> ContentProvider -> SQLQueryBuilder-> SQLiteDB
Android UI recoit <ContentResolver <ContentProvider <SQLQueryBuilder <SQLiteDB

Avec un loader (le retour ajoute une classe qui va nous aider à upater l'ui : l'adapter) : 
Android UI -> CursorLoader -> ContentResolver -> ContentProvider -> SQLQueryBuilder-> SQLiteDB
Android UI recoit <CursorAdapter <CursorLoader <ContentResolver <ContentProvider <SQLQueryBuilder <SQLiteDB


Adapters : they are meant for associating data with UI components.

How to create a CursorLoader : 
1 create a loader ID
2 implements loaders callbacks
3 init the loader with the loader manager


How to create a CursorLoader : 
1 create a loader ID
	private static final int MY_LOADER_ID=[my id];
	a single activity can use multiple loaders (each loader has different id).

2 implements loaders callbacks
	onCreateLoader {return new CursorLoader} Since CursorLoader derived from AsyncTask it will be executed in a (B).
	onLoadFinished {cursorAdapter.swapCursor(cursor)} Called when the loader is complete and our data is ready.
	onLoadReset {cursorAdapter.swapCursor(null)} Only called when our loader is being destroyed. It means we need to remove all references to the loader data.

3 init the loader with the loader manager
	getLoaderManager().initLoader([loaderId, Bundle, loaderCallBack])
	when loading in a fragment you should do this in the onActivityCreated method.
	
	
the flags passed as parameter in CursorAdapter (Context context, Cursor c, int flags) can be : 
 FLAG_AUTO_REQUERY = 1 : depreciated discouraged
 FLAG_REGISTER_CONTENT_OBSERVER = 2. //if we want the adapter to requering when the data change
 0 //if we want the loader to requering when the data change???
 
 
Currently : the cursor return all the columns of the table or join, each colum has and index. To get the data we need to : 
int pressureIndex=cursor.getColumnIndex(WeatherEntry.COLUMN_PRESSURE);
double pressure=cursor.getDouble(pressureIndex);

To create a projection : 
String[] FORECAST_COLUMNS ={
	WeatherEntry.TABLE_NAME+"."+WeatherEntry._ID,
	WeatherEntry.COLUMN_PRESSURE,
	WeatherEntry.COLUMN_MAX_TEMP,
	WeatherEntry.COLUMN_MIN_TEMP,
	WeatherEntry.COLUMN_HUMIDITY
}
	we are sure the db will return the column in this order
	int COL_ID=0;
	int COL_PRESSURE_INDEX=1;
	int COL_MAX_TEMP_INDEX=2;
	int COL_MIN_TEMP_INDEX=3;
	int COL_HUMIDITY_INDEX=4;

	hence we can do : double pressure=cursor.getDouble(COL_PRESSURE_INDEX);

It is more efficient because we are only fetching the data from the db that we need to use.


General rule : don't make any asumption about the order of the lifecycle method call. If one method is suppose to create an object just check in the other if the object is null and procede.


To make a ContentProvider available to 3rd party apps do this : 
set the manifest to android:exported="true"
<application>
        <provider
            android:authorities="com.example.android.sunshine"
            android:name=".data.WeatherProvider" 
			android:enable="true"
			android:exported="true"/>
</application>

Now any app that knows the content uri can use it.

You can limit the accessto the db to read or write : 
only to the others apps you have created
to 3rd party apps that respect the permissions
<manifest>
        <permission
            android:name="com.example.android.sunshine.LICENCE_TO_KILL"
			android:protectionLevel="dangerous"
			android:label="Licensed to kill"/>
</manifest>


Then you need to publish : 
the contract "com.example.android.sunshine.LICENCE_TO_KILL"
the differents URIs


ContentProvider list : http://developer.android.com/reference/android/provider/package-summary.html
http://developer.android.com/guide/topics/providers/calendar-provider.html
http://developer.android.com/guide/topics/providers/contacts-provider.html


2009  100 000 activation of android devices a day in may to over 300 000 activations by december. 

Mr Rosier tip :make app capable of running on sd card not just sim card memory.


# Lesson 5


Users judge the quality of your app within the first 30 seconds. It may not be fair,but a disproportionate amount of that judgement will be based not on the functionality, but on the visual aesthetics.

A great app should : 

	let users touch and interact with objects directly rather than having to use buttons and menus.
	use rich imagery and pictures in place of lots of words and long sentences.
	allows users to customize their app, while providing beautiful and sensible defaults. 
	learn the user preference in the context provided by the device so it never asks users for information that they've already provided. 
	Provide simple shortcuts to complete complex tasks
	remember data settings and customizations making them available across every device.

The guidelines are starting point for your own creative vision. 
Deviation from the guidelines is encouraged, but when you do do so, deviate with purpose.

All views have a visible property, it can be : 
visible : it's visible
invisible: it's not shown but there is still a placeholder for it. On ne peut pas dessiner par dessus.
gone : c'est comme si il n'existait pas ds le xml

CursorAdapter
newView : create the view components but don't put data in it
bindView : fill the components with the data taken from the cursor

Instead of just knowing one item view types. The adapter can declare multiple view types.(cf Lesson5. Two item view types)

We don't need to modify the bindView() method because it will continue to work. That's because the view ID names are the same between the today layout and the future day layout.


ViewHolders
allows us to avoid moving into the view hierarchy in order to find the view to update. In short allow us to avoid unnecessary findviewbyid calls.
they reference each view in the layout
the view holder object is stored in the tag field of the view.
This allows us to use findviewbyid only once.
is just a  java class, is not extenting anything, and can be name anything we want, but it good practice to finish by "Holder"


nb : view.setTag(viewHolder); this function can be used with any view and allows to remember any object we want.



Performance : https://www.udacity.com/course/viewer#!/c-ud853/l-1623168625/m-1667758600
Hierarchy viewer (cf instructor notes)
	Inflating complex layouts can be expensive. the rule : 
	keep your layout shallow (peu profond) and wide rather than deep and narrow. cf videos fordrawing https://www.udacity.com/course/viewer#!/c-ud853/l-1623168625/m-1667758599
	the activity shouldn't have more than 10 nested views or 80 views in total
	to open it  go to the Android Device Monitor and then clicking the Hierarchy Viewer button.
	Don't use FrameLayout as a root for another Layout if there is only one child (in an include) : use merge tag. The merge tag will be eliminated when compilation start and replace by the child.
Lint : Analyze > Inspect Code 
	looks really great
My notes : 
        //conclusion: closing the merge cursor close the cursors it is made off. All cursors
        // should be closed except those which are part of a merge cursor.
        // Cursor used in a loader don't explicitly call close. The close method is called by the
        // loader. After that the onReset method is called and it is good practice to call 
        // swapCursor(null) to release ressources.
	
Responsive design : http://developer.android.com/guide/practices/screens_support.html
	the eye of the user shouldn't have to go left to right to much. The screen should be scanned easiliy.
	we group devices in 3 groups or buckets (=sceau) nb the number here is the size the (diagonale???) width: 
		small phones <600dp ou dip = density independent pixel
		normal 7' tablets >600dp
		large 10' tablets >720dp
		extra-large : ?
	new qualifiers :
		sw600dp or sw600dp = smallestWidth. The minimum width required for the layout regardless of orientation. Si on a 2 fragment a afficher et qu'on est en mode portrait, même si la largeur est suffisement grande, on affichera qu'un fragment.Mais à verifier. C'est un peu comme si 600dp etait la taille de la diagonale. See video tres bien expilquée https://www.udacity.com/course/viewer#!/c-ud853/l-1623168625/m-1660448857
		w720dp = width =  The minimum width required for the layout depending on the orientation. Use to determine whether to use a multi-pane layout or not. We can use this to avoid the -land qualifier.
		h1024dp = height =  The minimum height required for the layout depending on the orientation. Most app don't need it, because they allow scrolling.
		
		or (en d'autres termes)
		sw600dp = smallestWidth : look at the standard size of the device (always width in portrait mode), if > 600? sw600dp layout : default layout;
		w720dp = width =  look at the width size of the device in the actual orientation, if > 720? w720dp layout : default layout;
		h1024dp = height =  look at the height size of the device in the actual orientation, if > 1024? h1024dp layout : default layout;
		
		see : Common configurations (un peu plus bas dans ce fichier)
		
	then you also group devices by screen density (=dpi)
		ldpi = low density devices 120 dpi (dot per inch), 0.75x   <-very small screen, in most case don't implement them
		mdpi = medium density devices 160dpi, 1x
		hdpi = high density devices 240dpi, 1.5x
		xhdpi = extra high density devices 320dpi, 2x
		xxhdpi = extra extra high density devices 480dpi, 3x
		xxxhdpi = extra extra extra high density devices 640dpi, 4x    <-very big screen, in most case don't implement them
		
Android Ressources (they are all externalized) : 
		strings
		layouts
		drawables
		animations
	they are chosen by the device using the right folder based on 
		language : values-fr/
		dialect : values-fr-rCA/
		whether the devices is docked: layout-desk/
		the type of touch screen : layout-stylus/
		the pixel density of the display : drawable-xhdpi/
		orientation of the screen : layout-land
		the smallest available screen width : layout-sw720dp available since android 3.2 and really help. Make useof it.
	At runtime android check the configuration and load the right things
	Those values can change at runtime (means when the user use the app) (ex : the orientation). For this reason, whenever a configation element changes, android destroy and recreate the activity.
	Good Practices
		It is good practice to provide translated strings for all your users. This task is easier nowadays if you use Google Play Publisher site that offer you this service.
		It also good practice to provide differents drawables at differents pixels densities to get a net image
		It also good practice to use the smallest available screen width.
			

Common configurations :

	res/layout/main_activity.xml           # For handsets (smaller than 600dp available width)
	res/layout-sw600dp/main_activity.xml   # For 7” tablets (600dp wide and bigger)
	res/layout-sw720dp/main_activity.xml   # For 10” tablets (720dp wide and bigger)
	Dans ce cas chaque device will use only one layout file.
	
	res/layout/main_activity.xml         # For handsets (smaller than 600dp available width)
	res/layout-w600dp/main_activity.xml  # Multi-pane (any screen with 600dp available width or more)
	This way, one device may actually use both layouts, depending on the orientation of the screen.

			

Different between mipmap folders and drawable folders.
	when you build your apk, you can specify the target devices, when it's done (it's the aapt job android asset packaging tool), only the directory for your target devices exple hdpi will stay in the drawable directory, but in the mipmap all the directories will remain. Why ?
	because the launcher app of your android won't launch the icone at the current density of the device. It will launch the higher density device. Exple : if your device is a xhdpi it will launch the xxhdpi. That will make the icon look sharper.
	

Fragments and Activities : 
	In theory you can have an app with a single activity and multiple fragments. Because fragments can manage the backstack.
	Why not always create one activity with a lot of fragments ?
		increased complexity 
		harder intent handling
		difficult to read maintain and test
		risk of tight coupling
		security concern
	Good Practice : create a new activity whenever the context changes for example : 
		if the data type displayed change.
		or swiching from viewing to entering (edit) data.
		
How the lifecycle of activities compare to the lifecycle of fragments ?
	in most case you can move what you would put in the activity lifecycle to the fragment lifecycle.
	diferences : 
		the UI is built : in onCreate for Activities and onCreateView for fragment (with it's corresponding onDestroyView called just before onDestroy)
		cleanup of ressource related to the UI : is done in onDrestroyView for fragment when it was done on onPause or onStop for Activities.
		on createView allows the fragment to become alive again by connecting himself to the data sources cursors etc and to it's activity (with the method attach and detach).
		onAttach : allow us to get a reference to the parent activity. It happens before onCreate.
		onDetach : happened after onDestroy.
		onActivityCreated : it's called after theActivity onCreate. It tells the fragment that we can safely interact with the activity UI.
		a fragment can exist without a layout. And those fragments are not recreated if the orientation change which is cool. How to do that ? 
			by adding setRetainInstance(true) in the onCreate method of the NonUIFragment
			make the onCreateView return null;
		
Full fragments lifecycle : 
onAttach -> onCreate -> onCreateView -> onActivityCreated -> onStart -> onResume -> onPause -> onStop -> onDestroyView -> onDestroy -> onDetach.

When should we prepare for fragment death ?
onPause or onStop : "normal case" this happen when the activity onPaused is called.
onDestroy : happens only when the fragment has been placed on the backstack but the activity no longer exist.
	
Ressources related to the UI : 
	bitmaps in memory
	cursor
	
Others Ressources cleanup list : 
	open connection
	open socket
	anything that uses a lot of battery
	sensor listeners
	location updates
	dynamic broadcast receivers
	game physics engine
	

What to check on the differents devices and what layout to adopt ?
	Generally, you'll know whether you need alternative layouts for different screen sizes once you test your application on different screen configurations. For example:

	When testing on a small screen, you might discover that your layout doesn't quite fit on the screen. For example, a row of buttons might not fit within the width of the screen on a small screen device. In this case you should provide an alternative layout for small screens that adjusts the size or position of the buttons.
	When testing on an extra-large screen, you might realize that your layout doesn't make efficient use of the big screen and is obviously stretched to fill it. In this case, you should provide an alternative layout for extra-large screens that provides a redesigned UI that is optimized for bigger screens such as tablets.
	Although your application should work fine without an alternative layout on big screens, it's quite important to users that your application looks as though it's designed specifically for their devices. If the UI is obviously stretched, users are more likely to be unsatisfied with the application experience.
	And, when testing in the landscape orientation compared to the portrait orientation, you might notice that UI elements placed at the bottom of the screen for the portrait orientation should instead be on the right side of the screen in landscape orientation.
	
Exple:after you've designed the layout you want to use for tablet-style devices, you might determine that the layout stops working well when the screen is less than 600dp wide. This threshold thus becomes the minimum size that you require for your tablet layout. As such, you can now specify that these layout resources should be used only when there is at least 600dp of width available for your application's UI.
	
To summarise most of the time you will end up doing 3 differents design : 
for small screen
for large screens
for landscape mode


Pour revenir à une activité dans l'etat où elleétait en dernier il faut utiliser le flag Intent.FLAG_ACTIVITY_CLEAR_TOP
super.getParentActivityIntent().addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
this flag indicate that we should check if the activity is already running in our task and to use that one instead of creating a new one if so.


La methode getParentActivityIntent de la classe settingActivity est appelé pour revenir à l'activité precedente. Il faut l'overider pour lui demander decharger l'activité dans son dernier état.
NB: this method didn't exist prior to jelly been so we need to add @TargetApi annotation.

android versions : file:///C:/Users/Elorri/AppData/Local/Android/sdk/docs/guide/topics/manifest/uses-sdk-element.html#ApiLevels


Pour faire en sorte que la ligne selectionnee soit bleu il faut ajouter un state drawable au fichier xml.

List of possible drawable ressources.
http://developer.android.com/guide/topics/resources/drawable-resource.html




Whenever you have a public method, always think that the method could be called before or after onCreate or onCreateView. Hence it's good to check if your member variables are null or not before doing something.

I'm surprised, that means that the setUseTodayLayout can be called twice.

Sunshine Wireframe : dessins des differents écrans screen
Sunshine Visual Mocks : print ecran des ecrans finaux avec red lines given by the designer

Pour changer l'apparence de l'action bar, il faut changer le theme.
Pour changer l'action bar de la SettingActivity il ne suffit pas de mettre un theme.

In material design : 
the main activity should show a logo on the action bar
the detail should not. The arrow should replace it.


Appcompat only adds an action bar to activities that derive from ActionBarActivity and SettingsActivity does not subclass
ActionBarActivity. SettingsActivity is a subclass of PreferenceActivity.
So why are we using PreferenceActivity? It’s an easy way to get the preference UI working on Gingerbread devices.
By explicitly themeing SettingActivity with a theme derived from DarkActionBar, we are able to add back the Action Bar.


How to create a CustomView


MyView extends View{} : lightweigt approach
MyView extends SurfaceView{} : design to support UI elements that require rapid redraws and/or 3D graphics, using something like OpenGL. It's perfect for views that display video games.

The existing widget library is entierly View based.
The base view class draws an empty borderless 100 by 100 pixel box. To change that, we override 2 methods :
onMeasure 
	handler, which allows us to indicate the view size (@override protected void onMesure(int,int)).
	onMeasure is called when your view's parent is laying out it's children.
	when this method is called by its parent layout, it ask "How much space will you use ?" and pass "how much space is available" and "do I need to feel the space"
	you must call setMeasureDimension at the end of the implementation ofthis method otherwise your app will crash.
onDraw :
	the canvas 
		is used as a painting algorithm. Anything we paint will cover anything beneath it. 
		offers variety of brushes to draw lines, squares, circles, fill them, text with colors, patterns, gradients, images.
		offers the ability to move, scale the campus while we draw
		paint object are created and destroyed at an alarming frequency = this can be heavy and detroy the smoothness of the UI when the garbage collector is initiated.
	is called everytime the screen is refresh


@override 
protected void onMesure(int wMeasureSpec,int hMeasureSpec){
int hSpecMode = MesureSpec.getMode(hMeasureSpec);
int hSpecSize = MesureSpec.getSize(hMeasureSpec);
int myHeight=hSpecSize;

if(hSpecMode==MeasureSpec.EXACTLY) //match parent
	myHeight=hSpecSize; 
else if(hSpecMode==MeasureSpec.AT_MOST) //wrap_content
	myHeight=what I want

//idem for width

setMeasureDimension();
	
}


@override 
protected void onDraw(Canvas canvas){

}




see video for more infos https://www.udacity.com/course/viewer#!/c-ud853/l-1623168625/m-1667758618

Exemple of a custom view : minimum to do 

public MyView extends View{
	public MyView(Context context){
		super(context)
	}
	public MyView(Context context, AttributeSet attrs){
		super(context, attrs)
	}	
		public MyView(Context context, AttributeSet attrs, int defaultStyle){
		super(context, attrs, defaultStyle)
	}
	
	@override 
	protected void onMesure(int wMeasureSpec,int hMeasureSpec){}
	
	@override 
	protected void onDraw(Canvas canvas){}
}


Exemples taken on forums : 

https://discussions.udacity.com/t/lesson-5-rich-and-responsive-layouts-draw-your-own-view/25579/2
public class MyView extends View {
public MyView (Context context) {
super(context);
}
public MyView (Context context, AttributeSet attrs) {
super(context, attrs);
}
public MyView (Context context, AttributeSet attrs,
int DefaultStyle) {super(context, attrs, DefaultStyle);
}

private int mAngle;
private int mSpeed;

protected void setAngle(int angle) {
    mAngle = angle;
}
protected void setSpeed(int speed) {
    mSpeed = speed > 100 ? 100: speed;
}
protected void setAngleSpeed (int angle, int speed) {
    mAngle = angle;
    mSpeed = speed > 100 ? 100: speed;
}

@Override
protected void onMeasure(int wMeasureSpec,
                         int hMeasureSpec) {
    int hSpecMode = MeasureSpec.getMode(hMeasureSpec);
    int hSpecSize = MeasureSpec.getSize(hMeasureSpec);
    int myHeight = hSpecSize;

    if (hSpecMode == MeasureSpec.EXACTLY)
        myHeight = hSpecSize;
    else if (hSpecMode == MeasureSpec.AT_MOST)
        myHeight = hSpecSize; // wrap content

    int wSpecMode = MeasureSpec.getMode(wMeasureSpec);
    int wSpecSize = MeasureSpec.getSize(wMeasureSpec);
    int myWidth = wSpecSize;

    if (wSpecMode == MeasureSpec.EXACTLY)
        myWidth = wSpecSize;
    else if (wSpecMode == MeasureSpec.AT_MOST)
        myWidth = wSpecSize; // wrap content

    setMeasuredDimension(myWidth, myHeight);
}

@Override
protected void onDraw (Canvas canvas) {
    int myHeigth = canvas.getHeight();
    int myWidth = canvas.getWidth();
    int myMaxLen;
    int myLen;
    Paint myPaint = new Paint(Paint.ANTI_ALIAS_FLAG);
    myPaint.setColor(0xff101010);
    myPaint.setAntiAlias(true);
    myPaint.setStrokeWidth(1+myWidth/15);
    if (myHeigth>myWidth)
        myMaxLen=myWidth;
    else
        myMaxLen=myHeigth;
    
    myLen = myMaxLen * (mSpeed / 100);
    
    int myWCenter = myWidth/2;
    int myHCenter = myHeigth/2;

    canvas.drawLine(myWCenter,myHCenter,myWCenter-myLen,myHCenter,myPaint);
    canvas.rotate(mAngle,myWCenter,myHCenter);
}


Accessibility in Custom view
	Evaluate how accessible is your app. You can select accessibility option in your phone. Good options to implements are :
		talk back service
	is particularly important when creating yor own view
	how to implement accessibility in a custom view ?
		in the xml :
		<com.myapp.MyView
			android:heigh=""
			android:width=""
			android:contentDescription="@string/viewDescription //for accessibility (but this means the content doesn't change at runtime)"
			/>
		if the content change at runtime : 
			myView.setContentDescription();
		best solution : send an accessibilityEvent
				when the content of theview change
				if(AccessibilityManager.getInstance(mContext).isEnabled){
					sendAccessibilityEvent(accessibilityEvent.TYPE_VIEW_TEXT_CHANGED)
				}
				overide
				public boolean dispatchPopulateAccessibilityEvent(AccessibilityEvent ev){
					ev.getText().add(winSpeedDir);
					return true;
				}
				

Reactivity in CustomView
listen user input event and overide the event handler : key presses, screen touch events, 


Android Kernel on Git :https://github.com/android
AOSP android opensource project : https://source.android.com/
include 
	dialer
	app launcher,
	calendar
	email. 
And Google offers it own versions of each as well.

User and download and a contact app and use it as a default because those apps are not tied to the core android.


# Lesson 6


AsyncTask problems : 
The AsyncTask is not tied to the activity lifecycle.
The virtual machine will hold on the activity object as long as the AsyncTask is running. Even after onDestroy on the activity. Which means, when you rotate your phone, the activity is destroyed, but the AsyncTask not. Hence there is now 2 threads running trying to perform the same update, because of the naive implementation of AsyncTask. If you turn your phone again, anoteher thread 3, etc.
If you leave the app, the async task will continue to run, as long as the process is kept alive (untill the UI is updated), but will run in low priority and your process will be the first thing to be killed if the devices need more ressources.
the app has to be visible and running in the foreground in the first place to instantiate the asynctask.

AsyncTask is not a nice pattern for very long operations such as :
fetching from web services : downloading files, uploading photos, playing music


Right way to perform updates if the weather change rapdidly.
regular update in the background with minimal battery drain.

When to use services ?
when we don't want our app or backgroud process to be killed if the app is not visible in the foreground

How to start/stop a service?
startService(MyServiceIntent);
stopService(TheServiceIWantToStop)

Services : 
have no user interfaces
run at a higher priority than background activities. (Priority level 1 and 2)
an app with a running service is less likely to be killed at runtime in order to free ressources.
the system try o restart services that are terminated before the app stop them
are design for long running tasks that shouldn't be stopped.
can make the app suddently appearring in the foreground and visible (for tasks that need the users to stop them : exple music app, car navigation) by using startForeground(notification); The notification will be displayed and can't be dismissed unsless : 
	the user stop the service or
	stopForeground(notification);is called.
run on the main thread, so we need an AsyncTask or a backgroud thread to execute the long running tasks. 
Subclasses are IntentServices or SyncAdapter : they both execute task on the (B). In practice, intead of using Service directly you will use IntentService or SyncAdapter most of the time.
	SyncAdapter are perfect for background data synchronisation.
	IntentServices : With this class, you can perform task sequentially, this class create a queue of intent and execute them on a backgound thread in the onHandleIntent method. When the queue is empty, the service terminate. If a new intent is received, the service start again.

public class MyIntentService extends IntentService{
	@Override
	protected voidonHandleIntent(Intent intent){
	}
}

What is the lifecycle of a service ?
onCreate
onStartCommand
onDestroy


public class MyService extends Service{

	@Override
	onCreate(){
	}
	
	@Override
	onStartCommand(Intent intent, int flags, int startId){
		startForeground(notification); //only if necessary (see explanation above)
	
		//TODO instantiate background task
		return Service.START_NOT_STICKY;
	}

	@Override
	onDestroy(){
	}
}


Android Ressource Management : 
	levels
		priority level 1 survival chances: Critical : active activity and foreground services (notifications) nearly impossible to kill to free ressources use them if absolutly necessary.
		priority level 2 survival chances: High  : visible activity and running services
		priority level 3 survival chances: Low : background activity will be killed first (nb : oldest apps are killed first)
	the 3 laws
		1. Android always ensure a smooth UX.
		2. Android will keep alive visible activities and running services unless doing so violate law 1
		3. Android will keep alive background thread unless doing so violate law 1 or law 2
		
Priority of differents apps
	gmail sync email : running services
	google music playing a song in the background : foreground services
	camera app taking a photo : active activity
	google maps in the background : background activity
	
Reference guide for services :http://developer.android.com/guide/components/services.html


How does a service wake up himself and start running ?
use the AlarmManager : tell the system that you want to wake up a component after a period of time. And we can choose this component to run in the background or foreground, background being better. 

But what kind of component is exactly woke up ?
a BroadcastReceiver (penser à une antenne parabolique) : it is use to recive intent broadcast from other apps (or same app).
	register an intent filter (in sunshine intent that listen on alarms)

Alarms
use PendingIntent (it's an intent that be travel from one app to another)
https://developer.android.com/training/scheduling/alarms.html
2 types :
	"elapsed real time" : suited to setting an alarm based on the passage of time (for example, an alarm that fires every 30 seconds) since it isn't affected by time zone/locale
	"real time clock" :  suited for alarms that are dependent on current locale.


What is the difference between a PendingIntent and an Intent ?
PendingIntent : the app using it can send data with the permissions and app identity of the app that created it.
Intent : 

This means that android systems can call the app back in an asynchronous way without compromising the android security model.

To check the battery state

Battery drain and Transferring Data Efficiency are achieve with :
Less data
Less often
Less time transfering


Est-ce qu'on fait : 
A beaucoup de transfert avec peu d'infos ? LittleCookies
B peu de transferts avec beaucoup d'info ? BigCookie
Rep : B peu de transferts avec beaucoup d'info.


Ce qui utilise le plus la batterie est le systeme de reception des ondes radio "Donnees mobiles", quels sont ses états : 
RadioStandBy : il est libre et inocupé
RadioFullPower : emet et reçoit des ondes radio use a lot of battery
RadioLowPower : emet et reçoit des ondes radio use a little less battery

RadioCell lifecycle
RadioStandBy -> 2s -> RadioFullPower -> 5-10s -> RadioLowPower -> 30s -> RadioStandBy
RadioStandBy -> 2s -> RadioFullPower -> 5-10s -> RadioLowPower -> 1.5s -> RadioFullPower -> 5-10s -> RadioLowPower -> 30s -> RadioStandBy.
The number of seconds represent the time (=latency) of inactivity that is needed in order to go to the next state.
The RadioLowPower state exist to avoid having to switch from RadioFullPower to RadioStandBy and as consequence making a bad user experience when surfing the net.
The system is always trying to combine low latency with high battery life.

Enven in the best scenario, you will be emitting at least 5-10s+30s = 40s. That means the LittleCookies scenario will drain the battery. We can remember that a network call will make the RadioFullPower une demi-minute. It's a lot.

See the video for the graph : https://www.udacity.com/course/viewer#!/c-ud853/l-1614738811/e-1664298695/m-1664298696
the small picks correspond to the app "pinging it's analytics".

Battery : To minimize to number of radio state transition : 
use agressif prefetching that can last till 2-5min and transfert (1-5Mb) of data
batch and queue any transfers that aren't time critical
bundling thoses batches with user initiated time critical transfers
or bundling thoses batches with server initiated time critical transfers


We want to download all the data, the user will need during his "session"

Transferring Data Without Draining the Battery  :http://developer.android.com/training/efficient-downloads/index.html
DevBytes: Efficient Data Transfers : http://developer.android.com/training/efficient-downloads/index.html



SyncAdapter
implement many of the best practice to make background transactions efficients.
permet app android de tirer profit du framework utilisé par Google app, pour des synchronisations efficaces.
it is a centralize place to put all of the device data transfers in one place, so that they all be schedule intelligenty by the OS.
are meant to keep local data on the device in sync with data on the web.


http://developer.android.com/training/sync-adapters/index.html
http://developer.android.com/training/sync-adapters/running-sync-adapter.html
http://remotexpert.net/2013/10/why-implement-android-syncadapter/

"Note: Sync adapters run asynchronously, so you should use them with the expectation that they transfer data regularly and efficiently, but not instantaneously. If you need to do real-time data transfer, you should do it in an AsyncTask or an IntentService."

SyncManager
handle synchronisation request using SyncAdapter
the tranfers of your app is schedule with transfert from other apps.
depending on the device memory for data transfert, it will schedule several synchs.
check for network connectivity before initiating transfers
retry unfinished download when connectivity is dropped

SyncFramework
work with content providers for sync
work with the android account manager for sync that are tied to accounts

Many of the normal use cases for sync adapters involve syncing the app's local data with information from an online account. For example, in an email app, a sync adapter might be used to pull down a user’s emails at regular intervals. Of course to do this the email app would need to store the user’s account information, such as a username and password, so that the app could log in and grab the new messages. To manage this, sync adapters each have a concept of a user’s account, tied with the sync adapter.
Does Open Weather Map need a user account? No. But we still need to implement the classes to handle accounts.

In the contentProvider tag of the Manifest add : 
        <provider
            android:authorities="@string/content_authority"
            android:name=".data.WeatherProvider"
            android:exported="false"
            android:syncable="true" />
android:exported="false" means that only our app can see our content provider.
android:syncable="true" mean that this content provider will be synced with a server.


1. Your MainActivity is created and the sync adapter is initialized. During initialization, getSyncAccount is called.
2. getSyncAccount will create a new account if no sunshine.example.com account exists. If this is the case, onAccountCreated will be called.
3. onAccountCreated configures the periodic sync and calls for an immediate sync. At this point, Sunshine will sync with the Open Weather API either every 3 hours (if the build version is less than KitKat) or everyone 1 hour (if the build version is greater than or equal to KitKat)

Inexact repeating alarm better than exact repeting alarms but not ideal.
the frequently you poll, the morefresh data you can display : battery life surfer.
if you poll less, data may not be up to date
if you let the user update frequency themselves but they have better things to do in life, no ?

So what do you do ?
use Google Cloud Messaging


Google Cloud Messaging GCM
make the server which hold the data to notify your app that :
	there is data to be downloaded
	or if the data is small, the new data is given in the message payload itself.
even if you use someonelse server it make sense to create a GCM middle-man

https://developers.google.com/cloud-messaging/
https://classroom.udacity.com/nanodegrees/nd801/parts/8011345406/modules/430205859175460/lessons/3995738628/concepts/59769187350923


Notifications : 
http://developer.android.com/guide/topics/ui/notifiers/notifications.html
http://developer.android.com/design/patterns/notifications.html
As a standardized UI designed specifically for conveying timely infos in limited screen space. Notifications are the most used component of wearables. Means you can make your app compatible with wearable for free ifyou use them.
But : use with intelligence : by useful, not spammy.


NB : le Loader de forecastFragment, peut se permettre de mettre une projection, et la clause sortby (même si elle n'est pas utilisée dans toutes les requetes) parce que le DetailFragment affiche les m^me données (=> donc même projection).
Ce qu'on met dans le loader, s'appliquera à TOUTE les Uris du Provider. 


NB : la class FetchMoviesTask fait à la fois ce que fait le Loader + le Service
        @Override
        protected Cursor doInBackground(String... params) {
            tmdbAccess.syncMovies(params[0]);  	<-équivalent de syncDB : sera dans le service
            Cursor cur = getActivity().getContentResolver().query(
                    MovieEntry.buildMovieSortByUri(Utility.getSortOrderPreferences(getContext())),
                    MOVIE_COLUMNS,
                    null,						<-équivalent de syncUI : sera dans le loader
                    null,
                    null);
            return cur;
        }

		
		
http://developer.android.com/guide/topics/resources/drawable-resource.html
<selector> is a State List element. Each <item> uses various attributes to describe the state in which it should be used as the graphic for the drawable.
During each state change, the state list is traversed top to bottom and the first item that matches the current state is used—the selection is not based on the "best match," but simply the first item that meets the minimum criteria of the state.
Use selector for the favorite image.

Styles : 
    <GridView
        android:choiceMode="singleChoice"/>
devient si on prefere utiliser un style : 
    <GridView
		style="@style/MySingleChoiceStyle"
        android:choiceMode="singleChoice"/>
		
	styles.xml
<resources>
    <style name="MySingleChoiceStyle">
        <item name="android:choiceMode">singleChoice</item>
    </style>
</resources>



Themes Compatibility en fonction des versions :
support libraries version
https://developer.android.com/tools/support-library/features.html (nb le vX coresponds à la plus petite version d'android avec laquelle la lib est compatible, the follwing number ex 21 is the min compile version compileSdkVersion check your gradle)
Android dashbord pour le cammenber. Platform versions


v11
	None (integrated)
	Holo (lib)
	Sherlock (lib)
	AppCompat (lib)
	Material (not supported) <-another xml special this version is needed
v14
	None (integrated)
	Holo (integrated)
	Sherlock (not supported)
	AppCompat (not supported)
	Material (not supported)
v15-20
	None (integrated)
	Holo (integrated)
	Sherlock (integrated)
	AppCompat (integrated)
	Material (via lib '7 appcompat library' but incomplete)
v21
	None (integrated)
	Holo (integrated)
	Sherlock (integrated)
	AppCompat (integrated)
	Material(integrated)
	
For 'Settings' Activities : le theme AppCompat n'est pas supporté. Il faut choisir entre Holo et Material
cf commit 'Add ActionBar on Settings for pre-lolipop' of PopularMovies.
Pour Holo il faut etentre Holo action bar
Pour Material on peut etendre letheme ca suffit.

AppCompat vs Material: http://android-developers.blogspot.fr/2014/10/appcompat-v21-material-design-for-pre.html


querying google cloud https://cloud.google.com/datastore/docs/apis/v1beta2/datasets/runQuery


Questions : 

Steps to add an item menu in a fragment.
	1. create xml menu item
	2. add setHasOptionsMenu in the onCreate
	3. override onCreateOptionsMenu
	4. override onOptionsItemSelected
	
-Step to add a ShareActionProvider as an item menu
	1. create a xml menu item with a ShareActionProviderClass
	2. add setHasOptionsMenu in the onCreate
	3. override onCreateOptionsMenu but not onOptionsItemSelected and do the following
	4. inflate the menu
	5. get the menuItem from the menu
	6. get the ShareActionProvider from the menuItem
	7. set the ShareActionProvider with an Intent
	8. add FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET to the intent
	9. set type to the intent
		
		
		
In which class do you create a data base and how ? 
	1. extending the 






What is a Receiver ?

What are the advantages of using a CustomAdapter over an ArrayAdapter ?
	ArrayAdapter is only for textview, not imageView, by customizing it we can use imageViews

What are the advantages of using a CursorAdapter over an custom ArrayAdapter ?
	if the data we get is in form of a cursor this the simpleist way to do something with it
	provider and resolver can notify the cursorApater of a change in the db and this one will update the UI AUTOmatically
	

Why adding a ViewHolder ? to avoid walking the tree


Interet d'un CursorAdapter
	sync db
	display from cursor
	peut inflater different xml en fonction d'une condition
	


liste des version d'android dans l'ordre
http://developer.android.com/reference/android/os/Build.VERSION_CODES.html
https://source.android.com/source/build-numbers.html

15  Oreo   API level (26)   Version(Android 8.0)
14  Nougat   API level (24|25)   Version(Android 7.0||Android 7.1)
13  Marshmallow   API level (23)   Version(Android 6.0)
12  LOLLIPOP   API level (21|22)   Version(Android 5.0|Android 5.1)
11  KITKAT_WATCH   API level (20)   Version(Android 4.4W)
10  KITKAT   API level (19)   Version(Android 4.4)
9  JELLY_BEAN   API level (16|17|18)   Version(Android 4.1, 4.1.1|Android 4.3)
8  ICE_CREAM_SANDWICH   API level (14|15)   Version(Android 4.0|Android 4.0.4)
7  HONEYCOMB   API level (11|12|13)   Version(Android 3.0.x|Android 3.2)
6  GINGERBREAD   API level (9|10)   Version(Android 2.3|Android 2.3.4)
5  FROYO   API level (8)   Version(Android 2.2.x)
4  ECLAIR   API level (5|6|7)   Version(Android 2.0|Android 2.1.x)
3  DONUT   API level (4)   Version(Android 1.6)
2  CUPCAKE   API level (3)   Version(Android 1.5)
1  BASE   API level (1|2)   Version(Android 1.0|Android 1.1)


Name AsyncTask classes and pros and cons of each of them  : 

AsyncTask 
	Cons: 
		The virtual machine will hold on the activity object as long as the AsyncTask is running. Even after onDestroy on the activity. Which means, when you rotate your phone, the activity is destroyed, but the AsyncTask not. Hence there is now 2 threads running trying to perform the same update, because of the naive implementation of AsyncTask. If you turn your phone again, anoteher thread 3, etc.
		If you leave the app, the async task will continue to run, as long as the process is kept alive (untill the UI is updated), but will run in low priority and your process will be the first thing to be killed if the devices need more ressources.
		the app has to be visible and running in the foreground in the first place to instantiate the asynctask.
	Can query a ContentProvider and return a Cursor : No
	Can notify a CursorAdapter of a change in the db : No
	When activity is recreated : 
		create another parallel doInBackground thread that requery the data, every time => bad performances
	Best for tasks : 
		that will terminate when activity terminate.
		and excepted to run only 1 second or 2 second.
	Best place to implement : in an inner class of the fragment

AsyncTaskLoader
	Can query a ContentProvider and return a Cursor : Yes
	Can notify a CursorAdapter of a change in the db : Yes
	When activity is recreated : 
		does NOTE create another parallel loadInBackground that requery the data, the initLoader methode help the LoaderManager to connect to the existing thread.
		if onLoadFinished has already been called and UI is updated : onLoadFinished is called again => bad performances.
	Best for tasks : 
		that will terminate after the activity terminate.
		and excepted to run a long time.
	Best place to implement : ?	
		
CursorLoader
	Can query a ContentProvider and return a Cursor : Yes
	Can notify a CursorAdapter of a change in the db : Yes
	When activity is recreated : 
		does NOTE create another parallel loadInBackground that requery the data, the initLoader methode help the LoaderManager to connect to the existing thread.
		if onLoadFinished has already been called and UI is updated : onLoadFinished is NOT called again => GOOD performances.
	Best for tasks : 
		that will terminate after the activity terminate.
		and excepted to run a long time.
	Best place to implement : by making the fragment itself being the loader and implementing methods+ onActivityCreated. implements LoaderManager.LoaderCallbacks<Cursor> 	
		
		
Différences entre un Loader et un Service
Diferences : 
	Loader
		often use to retrieve data from the DB and display it, in short : syncUIfromDB -> MIEUX : syncUIfromContentProvider
	Services
		often use to retrieve data from the Internet and store it in the DB, in short : syncDBfromServor -> MIEUX : syncContentProviderfromServor
Similarities :
	they perform long tasks
	


How to write an XML formatted string and how to call it?


Pourquoi ne peut on pas utilser 2 fragment dans les layout xml, ms un frag + un FrameLayout ?


AlarmManager wake up a BroadcastReceiver that start a Service is that correct ?


What is a PendingIntent, Implicit Intent, Explicit Intent and how do you create them?

	In a ShareActionProvider -> mShareActionProvider.setShareIntent(intent)
			Intent intent = new Intent(Intent.ACTION_SEND);
			intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET);
			intent.setType("text/plain");
			intent.putExtra(Intent.EXTRA_TEXT, "will be the first video URL here");


Difference between registering an AlarmReceiver and an InternetReceiver ?
	AlarmReceiver 
		1. create an AlarmReceiver class : AlarmReceiver extends BroadcastReceiver
		2. create an Intent for the AlarmReceiver class : Intent intent = new Intent(getActivity(), AlarmReceiver.class);
		3. create a PendingIntent : PendingIntent pendingIntent = PendingIntent.getBroadcast(getActivity(), 0,intent,PendingIntent.FLAG_ONE_SHOT);
		4. Register the AlarmReceiver to wake up every (duration)
			AlarmManager alarmManager=(AlarmManager)getActivity().getSystemService(Context.ALARM_SERVICE);
			alarmManager.set(AlarmManager.RTC_WAKEUP, System.currentTimeMillis() + 5000, pendingIntent);
		5. fill onReceive method of BroadCastReceiver class.
	InternetReceiver
		1. create an InternetReceiver class : InternetReceiver extends BroadcastReceiver
		2. create an IntentFilter for the InternetReceiver class : 
			dynamically : IntentFilter intentFilter=new IntentFilter("com.myApp.NEWLIFEFORM");
			or in the manifest : <action android:name="com.myApp.NEWLIFEFORM" />
		3. Register the InternetReceiver when an intent of the type specified in the filter is received.
			registerReceiver(myReceiver, intentFilter);
		4. Unregister the receiver in the onPause method.
		5. fill onReceive method of BroadCastReceiver class.
		
AlarmManager and Notifications

	Since Api 21 lolipop : notification can set up an amount of time before the next notification start.No need for alarm manager
	Before Api 21 : you need one
	example : https://github.com/Valakias/SampleTimedNotification
	The code that creates and sets the alarmManager is in the main activity, the code that builds, sets the intents, and launches the notification, is in the alarmreceiver class. It's set to launch after a second after you open the main activity now, but you can modify the whens and hows by moving the code where you need and modifying the variables.
		

What are the major Services classes and their differences ?
Service 
	run on (M)
IntentService (commit 'using Services'&'using alarms' of Sunshine)
	run on (B)
	sync a queue of Intent
	schedule syncs (grace a Alarm)
	does NOT check for network connectivity
	good for real-time transfert
	
	1. Create a IntentService class (ex: SunshineService nb:remplace AsyncTask)
	2. @Override onHandleIntent of the IntentService class and do your network call (json) here
	3. Create a BroadCastReceiver class (usually as an inner class of the Service class) (ex: AlarmReceiver)
	4. Register the AlarmReceiver in the 'MainActivity'<it's not always the 'MainActivity' where to register ? the first time the app has all the data to make the sync. (in Sunshine : onLocationChange>updateWeather)
		5. create an Intent for the AlarmReceiver class : Intent intent = new Intent(getActivity(), AlarmReceiver.class);
		6. create a PendingIntent : PendingIntent pendingIntent = PendingIntent.getBroadcast(getActivity(), 0,intent,PendingIntent.FLAG_ONE_SHOT);
		7. Register the AlarmReceiver to wake up every (duration)
			AlarmManager alarmManager=(AlarmManager)getActivity().getSystemService(Context.ALARM_SERVICE);
			alarmManager.set(AlarmManager.RTC_WAKEUP, System.currentTimeMillis() + 5000, pendingIntent);
	8. In the BroadCastReceiver class onReceive method
		9. create an Intent for the IntentService class : Intent intent = new Intent(getActivity(), SunshineService.class); getActivity().startService(intent);
		10. start service : context.startService(intent);

SyncAdapter
	run on (B)
	sync an with other app Intents
	schedule syncs (grace au SyncManager)
	check for network connectivity (grace au SyncManager)
	good for regular not real-time transfert
	
	1. Create a User-Account : (to avoid run crash 'java.lang.SecurityException: caller uid 10349 is different than the authenticator's uid')
		1. Add Service in the Manifest 
			<intent-filter><action android:name="android.accounts.AccountAuthenticator" /></intent-filter>
			<meta-data android:name="android.accounts.AccountAuthenticator" android:resource="@xml/authenticator" />  
		2. Add authenticator.xml in the xml directory 
		3. Create a Service class for the Account (ex MoviesAuthenticatorService)
		4. Create a AbstractAccountAuthenticator class (nb: Account does not exist. ex MoviesAuthenticator)
	
	2. Create a SyncAdapter
		1. Create a AbstractThreadedSyncAdapter class (nb: SyncAdapter does not exist. ex SunshineSyncAdapter nb:remplace AsyncTask)
		2. @Override onPerformSync of the SyncAdapter class and do your network call (json) here
		3. Create static helper method initializeSyncAdapter
			4. Create static helper method getSyncAccount 
				5. Specify the sync account type in the xml string file <string name="sync_account_type">sunshine.example.com</string>
				6. Add manifest permissions 
					<uses-permission android:name="android.permission.READ_SYNC_SETTINGS"/> 	//if not set compilation error
					<uses-permission android:name="android.permission.WRITE_SYNC_SETTINGS"/> 	//if not set compilation error
					<uses-permission android:name="android.permission.AUTHENTICATE_ACCOUNTS"/>	//if not set compilation error
			7. Create static helper method onAccountCreated
			8. Create static helper method configurePeriodicSync
		9. Create static helper method syncImmediately
		10. Call the initializeSyncAdapter method (usually at the end of the onCreate of the mainActivity) : SunshineSyncAdapter.initializeSyncAdapter(this);
			Nb : now the App will sync regularly. If we need to sync on request, add another syncImmediately next point -> 11.
		11. Call the syncImmediately whenever we want to add a manual sync (in Sunshine onLocationChange>updateWeather ; in PopularMovies onSettingsChange>syncDb)
	
	3. Create a Service class (ex SunshineService) : 
		1. Override onCreate et onBind
		2. Add Service in the Manifest 
			<intent-filter><action android:name="android.content.SyncAdapter" /></intent-filter>
			<meta-data android:name="android.content.SyncAdapter" android:resource="@xml/syncadapter" />   // SyncAdapter info in an xml file 
		3. Add the syncadapter.xml file in the res directory
		
		
		
NB : le setArguments() ne peut se faire que sur un fragment crée dynamiquement avec la methode new, car sinon on ne peut qu'obtenir un 'IllegalStateException: Fragment already active'

Exple : 

        mMainFragment = (MainFragment) getSupportFragmentManager().findFragmentById(R.id.main_fragment);
        Bundle arguments = new Bundle();
        arguments.putParcelable(MAIN_URI, mMainUri);
        mMainFragment.setArguments(arguments); ---------------------> 'IllegalStateException: Fragment already active'
		
		Bundle arguments = new Bundle();
        arguments.putParcelable(DetailFragment.DETAIL_URI, getIntent().getData());
        DetailFragment fragment = new DetailFragment();
        fragment.setArguments(arguments); ---------------------> No errors

        mMainFragment = (MainFragment) getSupportFragmentManager().findFragmentById(R.id.main_fragment);
        mMainFragment.setMainUri(mMainUri); ---------------------> No errors
		
		
Where is adb ? 
C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools

Sqlite version ?


What can be a cause of unkilled threads running parallel ?
not checking onSaveInstanceState in the onCreate method ofan activity.
	exple : 
	@Override
    protected void onCreate(Bundle savedInstanceState) {
	       if (savedInstanceState == null) {
           ...
            getSupportFragmentManager().beginTransaction()
                    .add(R.id.detail_fragment_container, fragment)
                    .commit();
		   }
	}
	

Get a bitmap from a drawable : 
    Bitmap largeIcon = BitmapFactory.decodeResource(context.getResources(), R.mipmap.ic_launcher);
	
	
	
	
Good exemple of : 
RecyclerView
Flotting action button
Content Provider Generator
https://github.com/schordas/SchematicPlanets


In the xml file on met le nom complet de la classe, si il s'agit d'une librairie.

Any view can return a context. view.getContext();








Must have android libraries : 
https://github.com/codepath/android_guides/wiki/Must-Have-Libraries
http://stackoverflow.com/questions/16588064/how-do-i-add-a-library-project-to-the-android-studio

Images Icons generators
http://romannurik.github.io/AndroidAssetStudio/icons-generic.html#source.type=image&source.space.trim=1&source.space.pad=0&size=144&padding=8&color=33b5e5%2C100&name=ic_local_grocery_store_white_48dp


UTC time GMT

Alors qu’aujourd’hui est une journée qui comptera 1 seconde de plus que les autres (on passera de 23:59:59 à 23:59:60 puis à 00:00:00), il est intéressant de revoir un peu les différentes normes de nommages du temps GMT et UTC.

L’heure GMT (Greenwich Mean Time) correspond à l’heure astronomique qu’il fait à la ville de Greenwich en Angleterre. Il réfère à la position du Soleil dans le ciel. Elle dépend également indirectement de la vitesse de rotation terrestre.
Cette heure, anciennement officielle et légale dans le monde n’est plus un standard depuis 1972.

C’est le temps UTC (Universal Time Coordinate) qu’il faut utiliser.
Ce temps définit le jour comme la période moyenne de la rotation terrestre, mais elle est fixée par des horloges atomiques, non plus par la position du Soleil dans le ciel.
EDIT : comme on me le faire remarquer dans les commentaires, l’heure UTC+00 correspond historiquement au fuseau de Greenwitch. L’apport de UTC par rapport à GMT, c’est la précision (définition atomique au lieu de astronomiquement de la seconde) et la régularité.

L’ajout ou le retrait d’une seconde de temps en temps, comme ce soir, est nécessaire à cause des variations de la vitesse de rotation de la Terre (ralentissement à cause des frottements des marées par exemple). Le jour étant toujours défini comme une rotation de la Terre, il faut parfois ajouter une seconde pour éviter un décalage trop important au fil des siècles.



## 4 Webcast Project1 Creating and Using a Custom ArrayAdapter##


https://plus.google.com/u/0/events/chlh8qqr5q5grs1lajpqnvvql8k?authkey=CNXMrZuHsMWhNg

Coaches :
Marissa
Pugnima
Daniel
Jessica


AdapterView :
GridView
ListView
Spinner


    public class MovieAdapter extends ArrayAdapter<Movie> {
        private Context mContext;
        private Movie[] mThumbIds;

        public CustomAdapter(Context c, List<MovieW thumbIds) {
            //They put 0 for the ressource id for the layout file because they won't use it.
			super(c, 0, thumbIds);
        }

        public void updateResults(Movie[] results) {
            mThumbIds = results;
            //Triggers the list update
            notifyDataSetChanged();
        }

        public int getCount() {
            return mThumbIds.length;
        }

        public Movie getItem(int position) {
            return mThumbIds[position];
        }

        public long getItemId(int position) {
            return 0;
        }

        public View getView(int position, View convertView, ViewGroup parent) {
            View customView;
            if (mThumbIds[position].getPosterName() == null) { //The poster image doesn't exist. Display the movie title instead
                if ((convertView == null)||(convertView instanceof ImageView))  {
                    LayoutInflater inflater = LayoutInflater.from(getActivity());
                    customView =  inflater.inflate(R.layout.grid_item_layout_default, parent, false);
                } else {
                    customView = convertView;
                }
                ((TextView)customView).setText(mThumbIds[position].getTitle());
            } else {//The poster image exists, we can display the image
                if((convertView == null)||(convertView instanceof TextView)) {
                    LayoutInflater inflater = LayoutInflater.from(getActivity());
                    customView =  inflater.inflate(R.layout.grid_item_layout, parent, false);
                } else {
                    customView =  convertView;
                }
                URL posterURL=tmdbAccess.constructPosterImageURL(mThumbIds[position].getPosterName());
                Picasso.with(getActivity()).load(posterURL.toString()).into((ImageView)customView);
            }
            return customView;
        }




## 4 Webcast Project1 Parcelables and onSaveInstanceState##


onCreate

if(onSaveInstanceState==null)||(!onSaveInstanceState.containsKey("flavor"))
	flavorList=new ArrayList
else
	flavorList=savedinstanceState.getParcelableArrayList("flavor")
	
	
onSaveInstanceState
	outState.putParcelableArrayList("flavors","FlavorList")


## 5 How to Use a Content Provider Notes (Copie en conflit de Elorri 2015-10-05)##

ContentProviders are an important android framework feature


With ContentProvider Adapters can easily grab data from 
users contacts
users docs
users calendars

Business card reader app : 
the user take a picture of the business card
the app automatically add the contact info to the phone
How ?
use of content provider
use of OCR


Android UserDictionaryProvider is a list of our custom words.
frequency :number between 1 an 250. of use oftheword.


Famous ContentProviders class : 
	ContactContentProvider
	CalendarContentProvider
	AlarmsContentProvider
	
It is the ContentResolver that will contact the correct ContentProvider

The ContentProvider can only do 4 things : 
	Read from the data --> query
	Add to the data --> insert
	Change préexisting data --> update
	Delete from the data --> delete
	
	
URI : Uniform Ressource Identifier
URL is a subset of URI, means URI wrap URL and more infos.

URL refers to location


Content URI : content://user_dictionary/words
always start with 'content://'
followed by the content authority : 'user_dictionary'  this is the keyword to contact the correct content provider
followed by the paths : 'words' means we want a list of words.


Content providers developer guide : https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/docs//guide/topics/providers/content-provider-basics.html#ContentURIs
Reference for UserDictionary URIs:http://developer.android.com/reference/android/provider/UserDictionary.Words.html
Reference for Calendar URIs : http://developer.android.com/reference/android/provider/CalendarContract.html

A Cursor is an iterator. Famous methods are : 
getCount()
moveToNext() ofen use in the while. 


while(cursor.moveToNext()){
	cursor.getString(index);
}



## 5 How to Use a Content Provider Notes##

ContentProviders are an important android framework feature
https://www.udacity.com/course/viewer#!/c-ud258/l-3372188753/m-3428788794

With ContentProvider Adapters can easily grab data from 
users contacts
users docs
users calendars

Business card reader app : 
the user take a picture of the business card
the app automatically add the contact info to the phone
How ?
use of content provider
use of OCR


Android UserDictionaryProvider is a list of our custom words.
frequency :number between 1 an 250. of use oftheword.


Famous ContentProviders class : 
	ContactContentProvider
	CalendarContentProvider
	AlarmsContentProvider
	
It is the ContentResolver that will contact the correct ContentProvider

The ContentProvider can only do 4 things : 
	Read from the data --> query
	Add to the data --> insert
	Change préexisting data --> update
	Delete from the data --> delete
	
	
URI : Uniform Ressource Identifier
URL is a subset of URI, means URI wrap URL and more infos.

URL refers to location


Content URI : content://user_dictionary/words
always start with 'content://'
followed by the content authority : 'user_dictionary'  this is the keyword to contact the correct content provider
followed by the paths : 'words' means we want a list of words.


Content providers developer guide : https://stuff.mit.edu/afs/sipb/project/android/sdk/android-sdk-linux/docs//guide/topics/providers/content-provider-basics.html#ContentURIs
Reference for UserDictionary URIs:http://developer.android.com/reference/android/provider/UserDictionary.Words.html
Reference for Calendar URIs : http://developer.android.com/reference/android/provider/CalendarContract.html

A Cursor is an iterator. Famous methods are : 
getCount()
moveToNext() ofen use in the while. 

while(cursor.moveToNext()){
	index = cursor.getColumnIndex(UserDictionary.Words.WORD);
	cursor.getString(index);
}

don't forget cursor.close() if you don't want leaking memory. Best is to do it in a finally block.





## 6 Webcast Project2 ContentProvider##

NB : leur DBHelper ajoute une requette SQL dans le onUpgrade, I don't know why.

	// Upgrade database when version is changed.
	@Override
	public void onUpgrade(SQLiteDatabase sqLiteDatabase, int oldVersion, int newVersion) {
		Log.w(LOG_TAG, "Upgrading database from version " + oldVersion + " to " +
				newVersion + ". OLD DATA WILL BE DESTROYED");
		// Drop the table
		sqLiteDatabase.execSQL("DROP TABLE IF EXISTS " + FlavorsContract.FlavorEntry.TABLE_FLAVORS);
        sqLiteDatabase.execSQL("DELETE FROM SQLITE_SEQUENCE WHERE NAME = '" +
                FlavorsContract.FlavorEntry.TABLE_FLAVORS + "'");

		// re-create database
		onCreate(sqLiteDatabase);
	}

	
For content providers libraries :
https://android-arsenal.com/tag/20 (Useful if you need to another db that is not sqlite)
Best and easiest are : 
Android Content Provider Generator
SimpleProvider
the one use in the webcast is https://github.com/SimonVT/schematic


http://facebook.github.io/stetho/
https://www.youtube.com/watch?v=iyXpdkqBsG8
Stetho is an android debug bridge for android applications written by the facebook team and opensource.
We can use chrome connected with our device to get some info out of our android app.

We can : 
look inside a db
look inside our preference file
look at network ressources call and see their responses.

Enable Stetho : 


In chrome : 
chrome://inspect/#devices
click on on inspect link
ressources>Web SQL> show the device db
ressources>Local Storage> show the preferences file nb: we can change the value directly inside of the editor.	
can write sql, remember anciennescommande (flèches du haut)

Network : always 'Others' for android

dumbapp : allow us to update preferences from the command line


## 6 Webcast Project2 Parcelables and onSaveInstanceState Webcast##

file empty

## 6 Webcast Project2 RecyclerView##

There will be a course on advanced android app dvp

https://plus.google.com/events/cfmkh6nd11tcmc2inm3sqfm980o?authkey=CNW26Km9_arF7wE
Ce qu'il retenir : 

Une ListView ou GridView agit sur : 
Layout
Recycling
Selection
Decorating
Scrolling
Empty view

Une RecyclerView n'agit que sur 1 chose : 
Recycling
But provide differents :
animators
scrollLayout
Layout managers

Une bonne librairie developpée par qqn de chez google : 
https://github.com/chrisbanes/cheesesquare

setLayoutManager <va s'occuper de savoir si c'est une liste, une grille
setAdapter



## 7 Advanced Android App Development##

	1Error and Guidance Messages
	2Building a Total Experience
	3Design 
	4Accessibility
	5Localisation
	6Performance
	7Before publishing : qualitative feedback 
	8After publishing collect : quantitative feedback





### Error and Guidance Messages

#### Make a list of UI object

[ ] Make a list of UI object that can be empty and need user message to comfort him.
[ ] Make the corresponding list of tables
[ ] Make the corresponding list of serveur url request

#### Create network, serveur, table variables with their corresponding status.
Exple :

	statusNetwork : 
		INTERNET_OFF = 0 /* page can't be found because of user has not turn on network connectivity on it's device*/
		INTERNET_ON = 1
	statusServeur1
		SERVEUR1_DOWN = 0 /* page can't be found because serveur is down : look for an erreur 404 we should advice the user contact administrators.*/
		SERVEUR1_WRONG_URL_APP_INPUT = 1 /* page can't be found because of our app wrong parametters input : look at server's error message. The serveur has change over the time and we must release an upgraded version of our app. */
		SERVEUR1_WRONG_URL_USER_INPUT = 2 /* page can't be found because of user wrong input (ex:location) : look at server's error message */
		SERVEUR1_OK=3
		statusTable1
			TABLE1_STATUS_UNKNOWN = 0 /* page can't be found because of user has not turn on network connectivity on it's device*/
			TABLE1_SYNC_DONE = 1
		statusTable2
			TABLE2_STATUS_UNKNOWN = 0
			TABLE2_SYNC_DONE = 1
	statusServeur2
		SERVEUR2_DOWN = 0
		SERVEUR2_WRONG_URL_APP_INPUT = 1
		SERVEUR2_WRONG_URL_USER_INPUT = 2
		SERVEUR2_OK = 3
		statusTable1
			TABLE1_STATUS_UNKNOWN = 0
			TABLE1_SYNC_DONE = 1
		statusTable2
			TABLE2_STATUS_UNKNOWN = 0
			TABLE2_SYNC_DONE = 1

#### Create a sync function and save the status in order
[ ] init tables status
	[ ] serveur 1 : statusTable1 : TABLE1_STATUS_UNKNOWN
	[ ] serveur 1 : statusTable2 : TABLE1_STATUS_UNKNOWN
	[ ] serveur 2 : statusTable1 : TABLE1_STATUS_UNKNOWN
	[ ] serveur 2 : statusTable2 : TABLE1_STATUS_UNKNOWN
[ ] statusNetwork
[ ] statusServeur1
[ ] serveur 1 : statusTable1
[ ] serveur 1 : statusTable2
[ ] statusServeur2
[ ] serveur 2 : statusTable1
[ ] serveur 2 : statusTable2

#### Make each UX objects (or their parents) :
[ ] implement defaultSharedPreferences
[ ] register a listener in onResume
[ ] unregister it in onPause


#### Display appropriate message on each UI object.
Note: to have table1 display the correct rows, statusNetwork should be INTERNET_ON and statusServeur1 should be SERVEUR_OK and TABLE1_SYNC_DONE

	if(INTERNET_OFF)
		display internet off message
	else  if(INTERNET_ON)&&(statusServeur1 < SERVEUR1_OK)
		display serveur error message
	else  if(INTERNET_ON)&&(SERVEUR1_OK)&&(statusTable1 <TABLE1_SYNC_DONE)
		display db sync uncomplete please wait
	else
		display db no results found
		
#### Set up on internetcheck sync
Here we choose only to resync if the tables we judge  (only them) indispensable have their status marked as incorrect.

	if((serveur1Table1status < TABLE1_SYNC_DONE)||(serveur2Table1status < TABLE1_SYNC_DONE))
		sync();
	

#### Set up the regular sync or user requested sync


	

### Building a Total Experience
	1Does your app will benefit by add or removing a standart component functionnality ? think CustomView
	ex : in Sunshine LocationPreference is customised to take a min of 3 characters before starting the search.
	2Does your app will get benefit user experience by adding a library at small cost ?
	3Widgets
		Fixe size widget
		Resizable widget
		Collection widget
	4Wallpaper
	



	 



### Accessibility
	1content descriptions :for user interface components that do not have visible text. eg: ImageButton, Button, checkbox, ImageView
		android:contentDescription  layout attribute or
		setContentDescription(): uses setContentDescription(null) if you have decorative graphics
	2custom view control: you need to implement accessibility interfaces
	3turn on TalkBack an check : Parametres>Accessibility>Acces Direct> TalkBack + Accessibilité
	sur window ça s'appelle 'narrateur'
	sur window pour controller son ordinateur en parlant : 'reconnaissance vocale' à rechercher dans la barre démarrer.
	
### Localisation : https://developer.android.com/distribute/tools/localization-checklist.html
	1-Run this prog to get a full list of available locale on your devices 
	
	    public static void printAvailableDevicesLocales(){
			final Locale[] availableLocales=Locale.getAvailableLocales();
			for(final Locale locale : availableLocales)
				Log.d("Applog",":"+locale.getDisplayName()+":"+locale.getLanguage()+":"
					+locale.getCountry()+":values-"+locale.toString().replace("_","-r"));
    }
	
	
	2Or choose all the Locales you want to support with this table. Always support the Locale.en_US as a minimum. This is the only locale Java guarantees is always available. + choose your default Locale.
	
|	Display Name	|	language	|	Country	|	Dvp folder name	|	Unit	|	Text Direction	|
|	------------	|	:---------:	|	:-----:	|:----------------:	|	:-----:	|	:------------:	|
|	arabe (Égypte)	|	ar	|	EG	|	values-ar-rEG	|	metric	|	Right to left	|
|	arabe (Israël)	|	ar	|	IL	|	values-ar-rIL	|	metric	|	Right to left	|
|	arabe (Irak)	|	ar	|	IQ	|	values-ar-rIQ	|	metric	|	Right to left	|
|	arabe (Maroc)	|	ar	|	MA	|	values-ar-rMA	|	metric	|	Right to left	|
|	arabe (Syrie)	|	ar	|	SY	|	values-ar-rSY	|	metric	|	Right to left	|
|	arabe (Tunisie)	|	ar	|	TN	|	values-ar-rTN	|	metric	|	Right to left	|
|	bulgare (Bulgarie)	|	bg	|	BG	|	values-bg-rBG	|	metric	|	Left to Right	|
|	brx (Inde)	|	brx	|	IN	|	values-brx-rIN	|	metric	|	Left to Right	|
|	tchèque (République tchèque)	|	cs	|	CZ	|	values-cs-rCZ	|	metric	|	Left to Right	|
|	danois (Danemark)	|	da	|	DK	|	values-da-rDK	|	metric	|	Left to Right	|
|	allemand (Allemagne)	|	de	|	DE	|	values-de-rDE	|	metric	|	Left to Right	|
|	grec (Grèce)	|	el	|	GR	|	values-el-rGR	|	metric	|	Left to Right	|
|	anglais (Royaume-Uni)	|	en	|	GB	|	values-en-rGB	|	imperial	|	Left to Right	|
|	anglais (États-Unis)	|	en	|	US	|	values-en-rUS	|	imperial	|	Left to Right	|
|	anglais (États-Unis,informatique)	|	en	|	US	|	values-en-rUS-rPOSIX	|	metric	|	Left to Right	|
|	espagnol (Espagne)	|	es	|	ES	|	values-es-rES	|	metric	|	Left to Right	|
|	français (Canada)	|	fr	|	CA	|	values-fr-rCA	|	 imperial ?	|	Left to Right	|
|	français (France)	|	fr	|	FR	|	values-fr-rFR	|	metric	|	Left to Right	|
|	hongrois (Hongrie)	|	hu	|	HU	|	values-hu-rHU	|	metric	|	Left to Right	|
|	italien (Italie)	|	it	|	IT	|	values-it-rIT	|	metric	|	Left to Right	|
|	japonais (Japon)	|	ja	|	JP	|	values-ja-rJP	|	metric	|	Right to left	|
|	coréen (Corée du Nord)	|	ko	|	KP	|	values-ko-rKP	|	metric	|	Right to left	|
|	coréen (Corée du Sud)	|	ko	|	KR	|	values-ko-rKR	|	metric	|	Right to left	|
|	lituanien (Lituanie)	|	lt	|	LT	|	values-lt-rLT	|	metric	|	Left to Right	|
|	portugais (Portugal)	|	pt	|	PT	|	values-pt-rPT	|	metric	|	Left to Right	|
|	russe (Russie)	|	ru	|	RU	|	values-ru-rRU	|	metric	|	Left to Right	|
|	serbe (Serbie,RS)	|	sr	|	LATN	|	values-sr-rLATN-rRS	|	metric	|	Left to Right	|
|	suédois (Suède)	|	sv	|	SE	|	values-sv-rSE	|	metric	|	Left to Right	|
|	thaï (Thaïlande)	|	th	|	TH	|	values-th-rTH	|	metric	|	Left to Right	|
|	turc (Turquie)	|	tr	|	TR	|	values-tr-rTR	|	metric	|	Left to Right	|
|	chinois (Chine)	|	zh	|	CN	|	values-zh-rCN	|	metric	|	Right to left	|
|	chinois (Hong Kong,HK)	|	zh	|	HANS	|	values-zh-rHANS-rHK	|	metric	|	Right to left	|
|	chinois (Singapour,SG)	|	zh	|	HANS	|	values-zh-rHANS-rSG	|	metric	|	Right to left	|
|	chinois (HANT)	|	zh	|	HANT	|	values-zh-rHANT	|	metric	|	Right to left	|
|	chinois (Taïwan)	|	zh	|	TW	|	values-zh-rTW	|	metric	|	Right to left	|
|	Hebrew	|		|		|		|		|	Right to left	|
|	Persian	|		|		|		|		|	Right to left	|


	3. Get the user most suitable Locale and Unit and store them in a preferred file. 
		1. In the mainActivity onCreate
			get the most suitable user Locale : getPreferedLocale()
			
				public static Locale getMostSuitableLocale() {
					if ((Locale.getDefault().getLanguage().equals("fr"))
							&& (Locale.getDefault().getCountry().equals("FR")))
						return Locale.getDefault(); //In my list of chosen Locale
					if ((Locale.getDefault().getLanguage().equals("fr"))
							&& (Locale.getDefault().getCountry().equals("CA")))
						return new Locale("fr", "FR");
					return new Locale("en", "US"); //only locale Java guarantees is always available. In my
					// list of chosen Locale. Or chose one in its getAvailableLocales();
				}
			get the most suitable user Units: getPreferedUnits()
			
				    public static String getMostSuitableUnits(Context context) {
						Locale locale=getMostSuitableLocale();
						// if(locale.getISO3Country().equalsIgnoreCase("usa") || locale.getISO3Country()
						//      .equalsIgnoreCase("mmr")) //use Imperial unit
						// Or better :
						TelephonyManager tm = (TelephonyManager)context.getSystemService(Context.TELEPHONY_SERVICE);
						String countryCode = tm.getSimCountryIso();
						//TODO try removing sim card to see if crash(or use tablet)
						if (countryCode.equals("us")){
							// use imperial unit
							return "imperial";
						} else {
							// use metric unit
							return "metric";
						}
					}
	4. Whenever data is taken from the server and displayed to the user (it needs to be converted correctly in something we know)
				numbers
					double serveurDouble;
					Locale serveurLocale;
					NumberFormat numberFormat = NumberFormat.getNumberInstance(serveurLocale);
					String serveurDoubleString = numberFormat.format(serveurDouble);
					Number number = format.parse(serveurDoubleString);
					serveurDouble = number.doubleValue(); //Now we are sure we have the correct number (no ',' misplaced)
					numberFormat = NumberFormat.getNumberInstance(getPreferredLocale());
					String userFriendlyDoubleString = numberFormat.format(serveurDouble);
				
				dates
					String serveurDateString;
					Locale serveurLocale;
					DateFormat dateFormat = DateFormat.getDateInstance(DateFormat.DEFAULT, serveurLocale); //DateFormat.DEFAULT should correspond to notation used by serveur or use   SimpleDateFormat dateFormat = new SimpleDateFormat("EEE MMM dd", serveurLocale);
					DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.DEFAULT, DateFormat.DEFAULT, serveurLocale);
					DateFormat dateFormat = DateFormat.getTimeInstance(DateFormat.DEFAULT, serveurLocale);
					dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
					Date serveurDate = dateFormat.parse(serveurDateString); //Now we are sure we have a correct Date
					dateFormat = new SimpleDateFormat("EEE MMM dd", getPreferredLocale()); //format to user flavor
					String serveurDateString = dateFormat.format(serveurDate);
			
				currencies
					Locale serveurLocale;
					Currency c=Currency.getInstance(serveurLocale); exple $ if serveurLocale is en_US
					//Don't use : Log.d("symbol",c.getSymbol()); //Will display $ the symbol in the serveur Locale
					Log.d("symbol",c.getSymbol(getPreferredLocale())); //Will display US$ ->$ the symbol in the user Locale
					
				text 
					//Don't use :toLowerCase(), toUpperCase()
					toLowerCase(getPreferredLocale()) 
					toUpperCase(getPreferredLocale()) 
				
				phone numbers 
				PhoneNumberUtils
					
	5. Whenever data is taken from the user or serveur and then compute (it needs to be converted in Locale.en_US)
				idem above but with Locale.en_US
		
	6. Whenever data is taken from the ressource directory
		for the default chosen Locale
			1make sure layout.xml and arrays.xml contains 0 strings.
			2make sure it is in the default "value" directory
			3if the others locales have a start to end display
					add the start-end tags to remove left/right tag (=LTR) for Android min v < 17. Add the start-end tags alone for Android v > 17.
					add the manifest tag : <application> android:supportsRtl="true"</application>
						if you want a RTL language device Locale to display RTL because you are not supporting this language, do this. 
						android:supportsRtl="@string/is_hebrew"
						values/strings.xml : <string name="is_hebrew">false</string> hebrew language will be displayed in english LTR
						values-he/strings.xml : <string name="is_hebrew">true</string>
					 Android 5 (lollipop) automatically mirrors everything on the widget (even images), so a text or image that is left adjusted will become right adjusted. To prevent this add to the main/outer layout of the widget the following, android:layoutDirection="ltr" and it will force the layout to be left-to-right, even in right-to-left languages.
					Useful attributes : 
						android:layoutDirection — attribute for setting the direction of a component's layout.
						android:textDirection — attribute for setting the direction of a component's text.
						android:textAlignment — attribute for setting the alignment of a component's text.
						getLayoutDirectionFromLocale() — method for getting the Locale-specified direction
			4make sure you have a strings.xml for each locale and the "translable" attribute is specified. 
				Purchase translation : https://developer.android.com/distribute/tools/localization-checklist.html#gp-trans
		for others Locale and IF the layout change from the default 
			1add the corresponding directory ex:values-fr-rFR or values-fr

	

### Performance	
	1Test app without network
		1. Any drop frame ? (could be cause by Overdraw or leak memory)
		2. Overdraw ? 
			Tool : Enable Debug GPU Overdraw on your device Settings > Developer Options try to keep everything blue
			Tool : Hierarchy viewer
		3. Leak memory ?
			Tool : TraceView Any pink U-shape method ? if yes note : 
				exclusive CPU time
				inclusive CPU time
				nb calls
				nb recursion
			Tool : Heap Viewer  Android Device Monitor > Heap tab Any big size memory data ? if yes note :
				memory size of each data type alive
				run the allocation tracker
			Tool : Allocation tracker note
				allocation site : what function in the code allocated that memory				
		3. Fix Overdraw 
			remove unecessary background
			check out that any customView does the clipping by implementing canvas mehods
		4. Fix Leak memory
			batch and cache
			move code to background thread
			make sure the data strutures you use are correct ArrayList HashSet etc.., stringbuilder instead of concatanating yourself, use builders in general
			remove GC unseen like CustomView object created, in the onPause method
			close cursors : http://stackoverflow.com/questions/10723770/whats-the-best-way-to-iterate-an-android-cursor
	2Test app rotating the device several times in each screen
		same tests	
	3Test app without wifi
		same tests
	4Test app without Radio
		same tests
	5Make sure your app is not draining too much the battery
		Tool : Battery Historian python script
		Fix problems : use JobsShedulers




7Before publishing : qualitative feedback (grab some feedback from external people (you know too much the app, to be good yourself now))
	1why do they prefer one interface over another, why do they use this notification or not
	2directed reviews with specifics tasks or goal for the user to accomplish and chronometer
	
8After publishing collect : quantitative feedback
	1	how many ? how long ? How many users signed in, how long people stayed in your app.





### --------------------------------------------OLD NOTES ------------------------------------------------

Enchant Me
app should look and act effortlessly

Simplify my life
easy to understand
display useful info even when no network connectivity

Makes me amazing


You know the app so well that you miss some problems that a new comer might find that why we need external feedback :
when publishing
internal testing among employees(dog fooding)
teamFixIt (Enchant Me Simplify my life Makes me amazing)
when giving to testers 


How does google gives feedback for new google apps ?
with the google user experience review process, it goes in front of experienced google expert they look at :
design
interactions patterns
accessibility

Android UX legend Roman Nurik :
has given direct feedback
has built android UX tools
has contributed Dashclock and Muzei

2 style of users research : 
quantitative = with analytics tools : how many ? how long ? How many users signed in, how long people stayed in your app. It is a data about a large group of people.
qualitative = with interviews between users and dvp team : why? why do they prefer one interface over another, why do they use this notification or not. Interview undirected = UX reviews or directed with specifics tasks or goal for the user to accomplish.

Why the listview can be null ?
user put wrong json location
error on the server site
user is behind a captive web-portal
no network connectivity
Thoses states can be enumerated as follow : 

public enum LOCATION_STATUS{
	LOCATION_STATUS_OK, 
	LOCATION_STATUS_SERVER_DOWN,
	LOCATION_STATUS_SERVER_INVALID, 
	LOCATION_STATUS_UNKNOWN
}

But enum type is less efficient than static final constants.
But with static final constant you lose the type safety (I mean how can you tell that this final int can only be 1 2 or 4 ? you can't) so what to do ? use annotations;

We wan our tool to tell us when you assign wrong values to the static final int.

What are annotations ? 
@stuff
can be read during developpement
can be read at runtime

1-Add annotations dependencies	


To check if the device is connected to the internet : 
1 Manifest
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
2 Uses ConnectivityManager cf Utility.isNetworkAvailable()

In android we recommand not using enum types, which are costly, but static final integer constants.

We use @annotations to remember differents status. The IDE will then flag cases when we try to return values not in the set @NavigationMode (in our get or set methods).

@Retention(RetentionPolicy SOURCE)  //to tell the tool that we do not need to preserve this annotation at runtime in the class, this annotation (IntDef just bellow) won't have an impact on distributed version.
@IntDef({NAVIGATION_MODE_STANDARD, NAVIGATION_MODE_LIST, NAVIGATION_MODE_TABS})
	public @interface NavigationMode{}  //equivalent to the previous Enum type
	
	public static final int NAVIGATION_MODE_STANDARD=0;
	public static final int NAVIGATION_MODE_LIST=1;
	public static final int NAVIGATION_MODE_TABS=2;

	@NavigationMode public abstract int getNavigationMode(); //because of this annotation @NavigationMode the tool will check that the value returned by getNavigationMode is in the set predifined above.
	public abstract void setNavigationMode(@NavigationMode int mode)
	
	

SyncAdapters don't return status to us when they complete.


We will have foreCastFragment 
implements onSharedPreferenceChangeListener or
register this listener with defaultSharedPreferences in onResume and unregister it in onPause

The int we get from the Utility.getLocationStatus() method, can be out the range of the location_status we want??. That's why we add the  @SuppressWarnings("ResourceType") annotation.


Other location status problems : 
the user input text that doesn't resolve to a location.
the user input text that resolve to an existing wrong location.

CustomView
The default preference view doesn't allow us to accept input after 3 characters entered. We need a custom preference view.
link :
http://developer.android.com/training/custom-views/create-view.html
explain about xmlns res-autores-auto custom etc
cette ligne xmlns:custom="http://schemas.android.com/apk/res/com.example.android.sunshine" ajoute le name space de mon appli res directory au http://schemas.android.com/apk/res-auto genre de classpath par defaut (nb : res-auto can only be used with gradle).

Creating a custom preference view : 
1. add you custom view in your layout xml file with :
the complete path of the view java file : 
the android attribute
the custom attributes you want to add
    <com.example.android.sunshine.LocationEditTextPreference
        android:title="@string/pref_location_label"
        android:key="@string/pref_location_key"
        android:defaultValue="@string/pref_location_default"
        android:inputType="text"
        android:singleLine="true"
        custom:minLength="3"/>


2. create a custom attrs.xml file for yourcustom attributes

<?xml version="1.0" encoding="utf-8"?>
<ressources>
	<declare-stylable name="LocationEditTextPreference">
		<attr name="minLength" format="integer"/>
	</declare-stylable>
</ressources>

3. Dans le constructeur de la classe java
	transformer la liste d'attributs "AttributeSet attrs" en un trucs plus performant a lire cad un typed array
	lire le TypedArray : getBolean, getInteger
	eventuellement ajouter les methodes get et set des attributs exple setMinLenght();
	
	public LocationEditTextPreference(Context context, AttributeSet attrs) {
	    TypedArray a = context.getTheme().obtainStyledAttributes(attrs,R.styleable.LocationEditTextPreference,0, 0);
        mMinLength = a.getInteger(R.styleable.LocationEditTextPreference_minLength, DEFAULT_MINIMUM_LOCATION_LENGTH);
	}
	public void setMinLenght(int min) {
		mMinLength = min;
		invalidate();
		requestLayout();
	}
	
	

nb: chrome extension Android SDK Search
	
	
***********************************
Accessibility and Localisation
************************************

Accessibility

Text-to-speech
Haptic feedback
Gesture Navigation
Trackball
Directional Pad Navigation


Accessibility checklist
content descriptions :for user interface components that do not have visible text. eg: ImageButton, Button, checkbox, ImageView
	android:contentDescription  layout attribute or
	setContentDescription(): uses setContentDescription(null) if you have decorative graphics
focus-based navigation :make sure the user can navigate the screen layout by using the hardware based controls
	make use of D-pads, trackballs, keyboard, navigation gestures
	make sure every ui element is reachable, means 
		they are focusable
no audio only feedback : audio feedback must always have a non audio mechanism
	exple sound alarm combine with system notification
	exple sound alarm combine with haptic feedback
	exple sound alarm combine with visual queue
custom view control
	you need to implement accessibility interfaces
custom accessibility services : which can provide enhance accessibility features such as :
	audio prompting
	physical feedback
	alternative navigation mode

How to test the app : turn on accessibility service on the device
Parametres>Accessibility>Acces Direct> TalkBack + Accessibilité
Eyes-Free Keyboard to simulate use of a D-pad on a test device that does not have a physical D-pad.

https://developer.android.com/guide/topics/ui/accessibility/index.html



Localisation

To reach the most user the app should handle
text
audio files
numbers ( floating-point numbers some locales will use ',' as the decimal point and '.' for digit grouping)
currency
graphics

Identify the targets localisation element of your app
country
locale : use to format number formats, dates/time, currencies, rules for conversion to lowercase
language
Then focus your on theses targets.
developpement
translation
testing 
marketing

getAvailableLocales() to get a list of all the locales available on the device you're running on.
Always use : 


        NumberFormat numberFormat = NumberFormat.getNumberInstance(Locale.getDefault());
        numberFormat.format(1.278d);
		
		DateFormat dateFormat = DateFormat.getDateInstance(DateFormat.DEFAULT, Locale.getDefault()); ou DateFormat.SHORT (SHORT, MEDIUM, LONG, FULL, or DEFAULT)
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.DEFAULT, DateFormat.DEFAULT, Locale.getDefault());
		DateFormat dateFormat = DateFormat.getTimeInstance(DateFormat.DEFAULT, Locale.getDefault());
        dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
        dateFormat.format(new Date(0));
		
		        Currency c=Currency.getInstance(Locale.getDefault());
        Currency c=c.getSymbol();
                c.getSymbol(Locale.CANADA);
				
 Locale.en_US is the only locale Java guarantees is always available.

If you need to do a display, use the user chosen Locale
If you need to do some calculations : The best choice there is usually Locale.US – this locale is guaranteed to be available on all devices, and the fact that it has no surprising special cases and is frequently used (especially for computer-computer communication) means that it tends to be the most efficient choice too.

Be careful with method that don't take a Locale and convert from a String
parseDouble(String) : if your Locale use ',' floating (like us french) you will get wrong result. Change your Locale for the time of the conversion.
instead of parseDouble(String) use
   NumberFormat format = NumberFormat.getInstance(Locale.FRANCE);
    Number number = format.parse("1,234");
    double d = number.doubleValue();
	
toLowerCase(Locale.getDefault()) : in Turkey, for example, the characters 'i' and 'I' won't be converted to 'I' and 'i'. This is the correct behavior for Turkish text (such as user input), but inappropriate for, if you really want UpperCase if it's for a headerfor instance.
toUpperCase(Locale.getDefault()) 


Measuring unit are not supported by Locales : use :
 if (locale.getCountry().equals("US")){
 // use imperial unit
 } else {
 // use metric unit
 }
 better is : (locale.getISO3Country().equalsIgnoreCase("usa") || locale.getISO3Country().equalsIgnoreCase("mmr"))
 even better (but crash if no sim card) : 
 TelephonyManager tm = (TelephonyManager)getSystemService(Context.TELEPHONY_SERVICE);
String countryCode = tm.getSimCountryIso();
 if (countryCode.equals("us")){
 // use imperial unit
 } else {
 // use metric unit
 }
 Sinon demanderà l'utilisateur de choisir

Designing layout for Localisation
leave always around 30% space free on the side for the different languages to display joliment
or
use several alternative layout: harder to maintain

Android 4.2 introduced support for right to left layout. To make use of it : 
in the manifest : 
<application>
android:supportsRtl="true"
</application>

android > 17 : use only start/end
android <= 16 : use only start/end + left/right

On lolipop :it is possible to test the left to right app using the developper option
On other version : we have to change the language of the device

To see what Util functions are available for you, take a look at the documentation for DateUtils and DateFormat for dates, String.format() or DecimalFormat for numbers and currency, and PhoneNumberUtils for phone numbers.


***********************************
Libraries
***********************************


Downloading images from the internet and shows them on your phone
1 Download on the (B) thread
2 Cache : Prevent redownloading
3 Down sampling and decoding : we don't load giant images to display tiny icones, we scale them and load directly a tiny one

Avantages
they are reusable
Disadvantages
they have fonctions we don't need and that will create a load. memory consumption.
they may not age gracefully taking advantages of thenewest APIs

Picking the right library is the most important step
1 look for fonctionnality
2 is source code available?
3 ideally the readme match exactly what i need to do
4 integration, gradle easy to understand
5 screen shot, demos, ..
6 documentation :good doc is a sign that developpers care about their community
7 recent activity ? good sign


For images we will use Glide. It's used in a big community including google apps.
1 add graddle glide
2 Glide.with
3 <ImageView 
		android:adjustViewBounds="true"  <cela permet à l'image de s'ajuster à son contenant. Elle ne le fait plus automatiquement quand chargée du network.
		/>

***********************************
Google Cloud Messenging
***********************************

Properly pooling like we did in our app is good. It leads to : 
fewer syncs
longer battery life
make things easier on the server who won't have to deal with nagging devices all day long.

All of that if the sync is properly configured.


How to use GCM  for downstream communication (cad pour récuperer ce que le serveur a à nous dire)?

1https://console.cloud.google.com/project?pli=1
2go to https://console.cloud.google.com/apis/library?project=sunshine-gcm-1152 with the hamburger
3activer Google Cloud Messaging for Android https://console.cloud.google.com/apis/api/googlecloudmessaging/overview?project=sunshine-gcm-1152
4creer des identifiants : 
	1créer clé API > creer clé serveur > mettre 0.0.0.0/0 comme serveur IP adresse. (A changer si j'ai mon propre nom de domaine)
		API key serveur = AIzaSyB2qOpbTHmBFYxqCqjXQ6heXiXigh_vR2k
5In android studios, add Google play services. Go to Android SDK Manager>SDK tools and check : 
	google play services
	google repository
6in sunshine update the gradle with
	com.google.android.gms:play-services-gcm:7.0.0
7in the onCreate of the main activity
	check if gcm is registered here
8recheck in the onResume
9Manifest
	<uses-permission android:name="android.permission.INTERNET">
	<uses-permission android:name="android.permission.WAKELOCK"> optional.If we want to assure our device will be awake when we receive a GCM.
	<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"> Allow our app to receive messages from GCM
	
	Those 2 following line alows only our app the register itself as a receiver of GCM messages intended for our app
	<permission android:name="com.example.android.sunshine.app.permission.C2D_MESSAGE android:protectionLevel="signature"/> declare the message
	<uses-permission android:name="com.example.android.sunshine.app.permission.C2D_MESSAGE /> say we want to use the message
10Add GCM receiver in the manifest
<receiver android:name=".GcmBroadcastReceiver" android:permission="com.google.android.c2dm.permission.SEND">  <-anything that wants to send msg to this receiver must provide this permission.
	<intent-filter>
		<action android:name="com.google.android.c2dm.permission.RECEIVE"/>
		<category android:name="com.example.android.sunshine.app/>
	</intent-filter>
</receiver>	
11register gcm in an async task
	the register id given by gcm must be kept secret, hence use preferences.
13in sunshine we will use a broadcast receiver because our work is simple on reception. However for more complex work use a wakeful broadcast receiver.
	14in the onReceive method, we will process the message. And build an alert notif displayed to the user.
	

How to use GCM  for upstream communication (cad pour envoyer des trucs au serveur)?
https://developers.google.com/cloud-messaging/#sample-send


How to set up your server to work with GCM ?
https://developers.google.com/cloud-messaging/




***********************************
Material Design
***********************************


The detailView contains : 
a toolbar
the today view
additional weather details

today element is 1,5 height of the detail element.

The today view contains: 
2 spacer view above and bellow the content
16dp above and below title etc... @dimen/abc_list_item_padding_horizontal_material

The detail view contains: 
2 spacer view right and left of 32dp @dimen/forecast_detail_padding

The two sections are built with only one layout a GridLayout.


The MainScreen layout contains : 
a toolbar of ?attr/actionBarSize
a title Sunshine ?attr/listPreferredItemHeight
a listview 
	with 1st item includng a gridlayout
	others items ?attr/listPreferredItemHeight
	beetween 1st and 2nd item, there is a shadow
	
	 
Add the scrolling in the phone landscape view.
https://www.udacity.com/course/viewer#!/c-ud855-nd/l-3940839262/e-4328770422/m-4335948697


Animatting transitions

In our app, when clicking on an item. The bottom comes up (=slide up), the tool bar stay in place and everything else fade.




***********************************
Building a total experience
***********************************


Widgets :
it's a simple view
that is pass to the home screen launcher (le bureau du telephone)
and display along side with others widgets
They are differents types :
fixe size widget that respond to one action : taping  good for control bouton lecture d'un lecteur mp3
widget that show collection of data (listview with scroll) available since android 3
resizable widget (since android 3.1) that the user can change


If you want to link your app to a widget you need to add : 
AppWidgetProviderInfo.xml 
AppWidgetProvider.java 

1AppWidgetProviderInfo.xml here you can put : 
	size
	resizable :give flexibility to share almost all of our code, to make it resizable you need to specify : 
		minResizeHeight / minResizeWidth: min widget size
		minHeight / minWidth: default widget size
	preview image : witch gives a sense of what your widget will look like before adding it to the home screen.
	initialLayout : specify the xml layout to use
	minHeight and minWidth needs a number of cells. Because the number of cells can change between devices, keep some space in your widget. Here is the rule if n=number of cells : Size=(70dp x n) 30dp; exemple n=1 -> 40dp ; n=2 -> 110dp ; n=3 -> 180dp
	updatePeriodMillis : if 0 it's disable, otherwise it's  the widget provider update. default: Min update every half hours.
	previewImage :useful under developpement. When you are happy with your image, put it in your drawable nodpi folder and reference it in your AppWidgetProviderInfo.xml
2AppWidgetProvider.java 
	fill the widget view the correct data
	set onClickListeners
	use RemoteViews : it's a subset of normal views, those views can't be customed because they needs to go accross app and break those app's sandboxes. No customed view but all android common views can be used. 
		FrameLayout
		LinearLayout
		RelativeLayout
		GridLayout
		
		AnalogClock
		Button
		Chronometer
		ImageButton
		ImageView
		ProgressBar
		TextView
		ViewFlipper
		
		ListView
		GridView
		StackView
		AdapterViewFlipper
	the core of what AppWidgetProvider do is in onUpdate.
		we've got a list of appWidgetIds = unique identifier for each widget user has created
		we need to update all those widgets how to do that ?
			inflate the widget using the manager
			control what happen when you tap your widget : setOnclickPendingIntent methode
	AppWidgetProvider is broadcastreceiver
		broadcastreceiver
			have short life
			they receive broadcast thhrow their onReceive method
			use what's received in the onUpdate.
			thoses 2 methods are called on the UI thread
			that means we shouldn't call the contentProvider here, we will use a common pattern. The broadcastreceiver will start an IntentService to do the heavy work. 
		IntentServices
			onHandleIntent method runs on the (B)
			the service automatically stop itself when it's done
		because it's a broadcastreceiver, it makes easy the our SyncAdapter to notify the receiver that our data have change. How to do that ?
			in the syncAdapter add a constant ACTION_DATA_UPDATE="com.example.android.sunshine.ACTION_DATA_UPDATED"
			and use that constant as the action
				Intent dataUpdatedIntent =new Intent(ACTION_DATA_UPDATE);
				context.sendBroadcast(dataUpdateIntent);
			tell the manifest widget that he need to listen to this intent
			override the onReceive method and update the widget
			
3ConfigurationActivity : 
	to allow the user to create several widgets (for sunhine, one for each location he likes)
	appear only once, when the user select the wiget hewants to add.
	note : we won't allow this possibility on Sunshine.
4layout/widget.xml
	Avertissement (caveat) : with widget margin behavior change.
		before icecream sandwitch : widget needs to provide their own margins so that widget would appear huge next to the app icon already on the home screen
		since icecream sandwitch :margins are automatically applied, you shouldn't had some.
	To make the widget compatible : 
		we wrap our widget in a framelayout that include the padding foreach api level
5manifest
	to make the widget running we need an entry in the manifest
	here we link our AppWidgetProvider.java to our AppWidgetProviderInfo.xml (in the meta tag)
	we need also a APPWIDGET_UDDATE to call the onUpdate method
	as you can see the widget is defined as a broadcastreceiver because our AppWidgetProvider is broadcastreceiver in fact.
	


Resizable widget
1create as many layout as you want. note: use same ids accross all of them.
2make the user chosen size, take the most adapted layout.How to do that ?
	before android 4.0 it is always the default size.
	after 4.1 we use AppWidgetManager.getAppWidgetOptions() to know the size that gives us x and y in dp and we can deduct the layout
	add rsizable attributes
3add onAppWidgetOption changed to the provider. This will be called when the size of thewidget is changed. We will also refresh the widget here.


Collection widget
to fill a listview we need a manifest service with permission BIND_REMOTEVIEWS (remember the bindmethod of cursor adapter)
	this service will create a RemoteViewsFactory wihth is an equivalent of a CursorAdapter
	to connect our RemoteView to the RemoteViewsFactory, we will use the setRemoteViewsAdaptors method
to update ourwidget with new data instead of calling an intentService to update the whole widget we call the notifyAppWidgetViewDataChanged method.
	this will call RemoteViewsFactory.onDataChanged and requery for new data
to set click listener on the rows, use setOnClickFillInIntent


Wallpaper background
Muzei library
	extends Wallpaper Android API 
	bright or blurthe picture
	we just have to give him the picture
	when user select our app for the wallpaper
		onEnabled is called
		onSubscriberAdded is called
		on Update is called, this is where we need to give him the wallpaper
	when user unselect our app for the wallpaper
		onSubscriberRemove is called
		onDisabled is called
	we can use Musei scheduleUpdate to update wallpaper when sync happen
	

Widgets are more for fans, but a single feature make users rainbow your app to all their friends. Those ways are good to expand your app subtily. Think of them ...
Android wear, gives us opportunity to really improve our notifications.
Android watch
You can send notifications right before the user go out to tell him to take his umbrella or not
or info all the time

AndroidTV
more beautiful imagery

https://www.udacity.com/course/android-tv-and-google-cast-development--ud875B
https://www.udacity.com/course/android-wear-development--ud875A
https://www.udacity.com/course/android-auto-development--ud875C




***********************************
Performance
***********************************
You don't have to thing of performance for all of your app, just the ones you want to succeed.

If your app works great with wifi, it doesn't means perf will be good with Global Data = Radio

when choice, prefer android library over java

http://developer.android.com/training/articles/perf-tips.html

https://www.udacity.com/course/android-performance--ud825

users unhappy with performance give bad feedback

"Perf matter"

1gather information :
	run profiling tool
	run feedback tool
	evaluate application state before and after changes
2gain insight
3take actions


"tools not rules" Some thingsmay be ineficient, but if its not impacting your performance, it's not worth stressing over.

Rendering Performance: 
Just because you can overlay 90 views doesn't means you should
it's the most common performance issue
the system redraw the activity every 16 ms=60 frames/second =60hz, which means the app should compute and draw the screen in less of 16 ms. If it takes more, you got a drop frame= the system try to draw a new pictureto the screen but this one wasn't ready yet, donc il decide de ne rien rafraichir. the user end up seeing same graphic during 32ms. Any transition with show a jump in their smoothness, animation won't look smooth. 
Multiple dropped frames are responsible for laggy experience, it become even worst if user interact (ex scroll)
Android Rendering Pipeline is composed of : 
	CPU
		most problems comes from unecessary layouts and invalidations
			the display list will be rebuilt toomany times during a frame or
			you are spending too time invalidating too much of your view hierachy
	GPU: graphic processing unit
		most common problem : overdraw
			waste GPU processing time to colourate pixels that end up getting colored later by something else
to sumarrize most problems are
	ivalidation
	layout
	overdaw
	
Overdraw (GPU portion of Android Pipeline)
	rasterisation : process of taking some high level object like a string or a button and turning it into texture on your screen. it is a really time consuming process that's why there is aspecial piece of hardware dedicated to it in the GPU
	the CPU covert polygone+texture into images (long operation) and feed them (upload) to the rasterisation part of the GPU (long operation). Tis is done using OpenGL ES technology.
	OpenGL allows to upload content to the GPU and then leave it here, meansif you reference a button again in the future.
	every time you update a ressource on the gpu you loose processing time
	Rule of thumb : Get as much data onto the GPU as fast as possible and leave it there as long as possible.
	Since honeycomb every android system work with a gpu and you don't really have to think about it, but overdraw problems are still possible
	very common when we have layers, drawn one on thetop ofthe other
	to see the GPU overdraw on your phone
		1. Go to Settings > Developer Options 
		2. Turn on Debug GPU Overdraw. 
		3. In the popup, choose Show overdraw areas.
		Chez moi : Debog superposition GPU
		Si un pixel est dessiné 
			1 fois : couleur normal
			2 fois : bleu
			3 fois : vert
			4 fois : rose
			5 fois : rouge
		The rule : try to keep everything blue
	howto fix that ?
		eliminate part that will be redrawn
		remove unecessary background (You can nullify the windowBackground with the following statement: getWindow().setBackgroundDrawable(null))
		put a background only when avatar can't be found
		remove unecessary drawable
		Clipping
			avoid drawing UI widget that may be invisible in the final image
			android knows how to do that except if you create a custom view overiding the onDraw method
			the canvas class gives you a few methods to address this problem, the most useful method is canvas.clipRect where you can specify how much of your custom viewwill be invisible
			canvas.quickReject test whenever a given area is completely outsidethe cliping rectangle in witch case you can skip all that drawing work.

DisplayList (CPU portion of Android Pipeline)
	convert covert polygone+texture into images
	the 1st time a view needs to be rendered a DisplayList is created
	each time we need to render the view we execute that DisplayList
	if the view move on screen but nothing change on it, we just need to execute it again
	if some part ofthe view change, we need o recreate the DisplayList and execute it again
	remember that updating 1 view (like change the size) can cascade to other views and be costly, it is proportional to your hierachy
	
	
Hierarchy viewer
http://developer.android.com/tools/performance/hierarchy-viewer/setup.html
http://developer.android.com/tools/performance/hierarchy-viewer/index.html
http://developer.android.com/tools/performance/hierarchy-viewer/profiling.html
	Simplifying your view hierarchy to reduce overdraw, and make it easier to manage.
	Finding potential rendering performance bottlenecks related to the structure and shape of your view hierarchy.
Tools > Android > Android Device Monitor.

Each view in your subtree gets three dots, which can be green, yellow, or red.
	The left dot represents the Draw Process of the rendering pipeline.
	The middle dot represents the Layout Phase.
	The right dot represents the Execute Phase.
	
	Green means the view renders faster than at least half of the other views.
	Yellow means the view renders faster than the bottom half of the other views.
	Red means the view is among the slowest half of views. It's a potential problem in any situation where you can't afford slow performance. Like in a leaf node, or a view with only a few childrens. But keep in mind in any app something there will always be a slowest node, make sure it's in theright place.
	
	
	
Compute
	Java running on android is executing in virtual machine environnement, it complex there is a precompiler, a compiler, an optimizer.
	++i instead of i++ is called a compute performance
	code taking too long to execute ?
		primary reason : how the language and the associated software is handling the execution of the code
		if you find a slow function :cool it will be easy to fix
		if you can't find, you have leak memory. Memory lost a little bit everywhere. To fix this problem, you will use profiling.
	Profiling = time your code to figure out what portions are running slower than the others
	TraceView = profiling tool of AndroidStudio
		1 start the android device monitor
		2 select DDMS tab
		3 press the "start method profiling" button
		4 you get a popup with 2 ways of profiling your app
				record every method entry and exit : very ressources intensive
				sample base profiling: it's going to ping the app every 1ms and record what function isbeing executed : choose this one. It will start recording
		5 interact with the app
			select an item
			change the settings
		6 stop profiling by cliking the same icon again. and wait. it's long
		7 traceview has 2 panels
				timeline panel: show how your code is executing overtime. 
					Each row correspond to a thread
					each color correspond to a particular method thats running
					spickes (pics) when method start and stop (which make a U shape), if pink means something uses lot of cpu time
					you can zoom spicked to track particular methods
					the width of the U represent how much time it take for the method to be executed
				profile panel
					select a particular method in the traceview panel
					parents : we got info about what method actually call the one we have selected
					children : which method will be called within this one
					excusive CPU time = time spent in our method itself
					inclusive CPU time = time spent in our method itself + the method it calls internally
					call and recursion = how many time the method was called or how many times it was called recursively
					most ressource intensive appear on top
	Batching and Caching
		batching = try to eliminate the per execution overhead of an operation. kind of carsharing the save gas. 
			you have to prepare you data before operating on it. Exemple sort your array before search.
			if you have several value to find in a set. You sort the set only once and do a search on it several times.
		caching
			we'll use it when the result an action is always the same and we will use it several times
			example : if you do the exact same calcul in a loop. instead compute andsave the result outside of the loop
		cf Compute program
	Threads
		not executing long task on background thread can easily break the 16 ms windows
		if you end up not rendering the UI for more than 5 sec, the user receive the application not responding dialog
		every task that have noting to do with the draw should be move to the background thread.
	Performance of the primitive in the used language here java
		Are you confident that you are using the fastest container for what your code is doing ?
		Android Profilings tools can greatly help
	Systrace
			make use of android.os.Trace
			https://docs.google.com/document/d/1EKVq2FzcLVJFbwUtaC3QRddSwtzs0BSKZahkQyeGyHo/pub?embedded=true#h.zayu98yotlht
			http://developer.android.com/tools/debugging/systrace.html#app-trace
			http://developer.android.com/tools/debugging/systrace.html#analysis
			$ cd /c/Users/Elorri/AppData/Local/Android/sdk/platform-tools/systrace
			  $ python systrace.py --time=10 -o mynewtrace.html sched gfx view wm
			in the example with thedata structures set as they are duration is 23.384ms after data structure change it turns to 8 ms.	
			
			
Memory
	Garbage collector works like that
		find the objects that won't be access in the rest of the code
		reclaim ressources from them
		GC of android is more sophisticated than before.
		GC will behave differently depending on the device version of android
		GC event stop any other code executing during is process
		the rule : avoid writting code that makes your GC perform too often
		memory leaks happens when the GC fail to recognise there is that an object needs to be collected
		see :https://www.udacity.com/course/viewer#!/c-ud825/l-3846748822/m-3951919257
		to avoid memory leaks :
			track the life of your objects throughout your code
			clean up references when you no longer needs thems
			any object created by a custom view embeded in the xml should be clean up in the onStop method of the activity. 
			  When rotating the device, only the custom view is destroyed, not the object she created
		memory churns
			definition :process of allocating lots of objects in a very short amount of time
			exemple : 
				allocating a lot of object in a middle of a for loop
				anytime the screen needs to be redrawn or animation is occurring, you call onDraw every frame, and add object to your heap
				be careful with anycode that's going to be executed repeatedly
				string create by concatanating characters. to fix that use stringbuilder
			Allocation tracker tells you where in your code the data is being allocated
	Android Memory Monitor : Tools > Android > Memory Monitor
		the free memory + allocated memory represent all the memory available to your application
		if the app is doing nothing, it should be flat.
		the flat graph is an ideal scenario from a performance perspective
		if the app suddently needs more memory you will see a big difference in your app
		every time the GC pass, it make a mountain shape = healthy GC
		mountain pic = problem = means your app is spending a lot of time garbage collecting
		you can force a GC by pressing the initiateGC button
	Heap Viewer : Android Device Monitor > Heap tab
		select your app
		heap will update after GC has run so click on cause GC
		the table shows you what type of data is alive on the heap (ex: integer, object...) but it doesn't tellsyou where it is allocated (the Allocation tracker does that).
		if you click a data you get an histogram of the number of allocations + memory size of this data type
		it show the total size of a particular type. Size of all integers togethers, all objects etcs
	Allocation tracker
		https://www.udacity.com/course/viewer#!/c-ud825/l-3846748822/m-3767798724
		on the memory tab, click the button "start allocation tracking"
		then interact with your app
		on the memory tab, click the button "stop allocation tracking"
		click the ddms tab that has been created
			it list of the allocations that occured during you interactions
			the allocation order column tells you when the allocation happenned
			allocated class : show what type of data isbeing allocated
			allocation site : tells what function in the code allocated that memory
			clicking on an allocation makes you see its full call stack
			
Battery
	the more work your device does, the more battery it pulls
	turn airplane mode and do nothing your battery will live one month
	what task my application is doing that eats the most battery ?
	the only way to monitoryour battery drain is by attaching another piece of hardware to your phone specially dedicated for this task.
	
	Battery Historian
		http://developer.android.com/tools/performance/batterystats-battery-historian/index.html
		http://developer.android.com/tools/performance/batterystats-battery-historian/charts.html
		is a separate open source python script available in github
		download it https://github.com/google/battery-historian
		i paste it in C:\Users\Elorri\Dropbox\Udacity\Classes\7 Advanced Android App Development
		now do the following
			1. cd C:\Users\Elorri\Dropbox\Udacity\Classes\7 Advanced Android App Development
			2. C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools\adb kill-server
			   This is an important step because while you are developping lots of stuff can cause conflicts, and we want an adb clean
			3. C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools\adb devices
			   Our phone is attached, that's what we want
			4. C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools\adb shell dumpsys batterystats --reset
			   Reset the battery data gathering
			5. Unplug your phone. Now you are sure you don't draw any electrc current from your computer
			6. Go to youtube or google maps
			7. reconnect your phone
			8. C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools\adb shell dumpsys batterystats -> batterystats.txt
			   Look at battery statistics
			9. C:\Users\Elorri\AppData\Local\Android\sdk\platform-tools\adb shell dumpsys batterystats -> com.example.android.sunshine -> sunshine.txt
			   Create a more restrictive file
			10. C:\Python27\python historian.py sunshine.txt -> sunshine_batterystats.html			   
	Android turn off various part of the software in orderto prolong battery life
		first the screen go to sleep
		second the CPU go to sleep
		but even in this inactive state most app will try to do work and they will have to wake up the phone to do so
		to do so they use the powerManager.wakelock API
		wake up the phone is easy, but knowing when it can go back to sleep is more problematic. What if your app takes 60 min instead of 10 sec to analyses images before uploading them to the web ? What if the server crashes ? 
		To avoid that use wakelock.acquire that takes a time out parameter. But that doesn't solve the problem completely.
		the best thing to do is to do work for all app that are battery draining at the same time.
		if you hold on the wake lock for too long, you can be draining the battery => RELEASE your wakelock
		Networking is the baddest, dirtiest, battery draining stuff
		nice graph to understand https://www.udacity.com/course/viewer#!/c-ud825/l-3758168642/m-3772138712
	to usethe jobScheduler
		1. create a class JobService
		2. call onStartJob an onStopJob
		3. call the jobfinish method to release the wake lock(here in the  onPostFinishedMethod)
		4. call the jobScheduler :get a reference using getSystemService
		5. create a job info instance = encapsulation of the requierements for a particular task, by using the builder class
		6. setMinimumLatency : the system should wait at least 5 sec before running this job
		7. setOverrideDeadline(6000) = if this job haven't been executed within a min, go head and execute it
		8. sceduler.schedule(jobInfo)
	more info on job scheduler 
		https://www.youtube.com/watch?v=QdINLG5QrJc&feature=youtu.be
		https://developer.android.com/reference/android/app/job/JobInfo.Builder.html
		https://developer.android.com/reference/android/app/job/JobScheduler.html




***********************************
Publishing your App
***********************************

# Android code style guide lines : 
https://source.android.com/source/code-style.html
Every file should have a copyright statement at the top. Then a package statement and import statements should follow, each block separated by a blank line. And then there is the class or interface declaration. In the Javadoc comments, describe what the class or interface does.
Every class and nontrivial public method you write must contain a Javadoc comment with at least one sentence describing what the class or method does. This sentence should start with a 3rd person descriptive verb.
Public methods are part of an API and therefore require Javadoc.


	How do you know if your application works? 
		1. your app compiles.
		2. passes all the unit tests.
		3. successfully deployed to the production server
		4. successfully packaged into an installer
		5. your beta testers even signed off on it
	All of this is just noise.
	
	You don't know if your application truly works until you've performed usability tests on it with actual users.
		1. Can users actually understand your application?
		2. Can they get their work done in your application? 
	That is meaningful questions.
	
	What is usability test ?
		Simple : Watch some people while they try to use it and note where they run into trouble. Then fix it, and test it again.
		
		http://blog.codinghorror.com/low-fi-usability-testing/
		"In the beginning, though, usability testing was a very expensive proposition. You had to have a usability lab with an observation room behind a one-way mirror, and at least two video cameras so you could record the users' reactions and the thing they were using. You had to recruit a lot of people so you could get results that were statistically significant. It was Science. It cost $20,000 to $50,000 a shot. It didn't happen very often."
		"You didn't need a usability lab, and you could achieve the same results with a lot fewer users."
		"I'm going to try to explain how to do your own testing when you have no money and no time."
		
		In fact you only need to test with 5 users. See this graph : http://blog.codinghorror.com/low-fi-usability-testing/
		
		
### Test android app
https://www.genymotion.com/#!/
Testdroid



Basics
1 clean up your code
2 build an apk
3 Test the apk-release build on at least 1 target handset device and 1 target tablet device.
4 distribute your apk to a marketplace


Clean up your code
	1. Remove all Log statements.
	2. Remove the android:debuggable attribute from AndroidManifest.xml or set it to false
	3. Remove any log files or static test files that were created in your project.
	4. Remove all Debug tracing calls that you added to your code, such as startMethodTracing() and stopMethodTracing() method calls. 
	5. Remove unused file or methods
	6. Remove Activities, Applications used for devep
	7. Check your exception catch is not too general
	8. Check your exception catch DOES something. Empty {} is bad.
	9. Check you use fully qualify import
	10. Add copyright statement on each files
	11. Add javadoc at least on each public method
	12. Add javadoc at least on each class
	7. Provide values for both android:icon and android:label in the application element of AndroidManifest.xml. These are required.
	8. Provide values for both versionCode and versionName in the app-level build.gradle file to version your app. 
	8. Add license in all file see evaluator comments and update this list.
	9. Remove API key if you used one https://discussions.udacity.com/t/how-to-prevent-themoviedb-org-api-key-from-being-published-on-github-com/40667/2
	10. When choice prefer android library over java
	11. Readme.md

	
Build an apk
	The developper will need :
		an app certificate intented to establish authorship and trust between apps.
		a private cryptographic key to sign the certificate
		a keystore file that contains the private cryptographic key
	
	Important notes :
		Android Studio  automatically sign the apk with a debug-key if we don't create the apk by ourselves, it makes the developper life easier
		you can't publish with a debug-key, you need a realease-key. The difference between the two files is that the release .apk is signed with your certificate and optimized with the zipalign tool.
		the private cryptographic key MUST have a validity period that ends after 22 October 2033. Your key should be valid for at least 25 years, so you can sign app updates with the same key through the lifespan of your app.
		You'll also want to provide all of your company information to establish authorship in the certificate.
		The Android Studio wizard sets up your keystore and configures your build for you. However, clever students may notice that this places private information such as your key and password in your build.gradle file. You probably don’t want to do this. Instead, you should configure the build file to grab these values from environment variables. At the risk of repeating myself, you really should check out our super cool and very informative documentation (Step 4). See http://developer.android.com/tools/publishing/app-signing.html
	
	The developper should 
		keep in a safe and secure place and ensure secure backups of
			a private cryptographic key (If you publish an app to Google Play and then lose the key with which you signed your app, you will not be able to publish any updates to your app, since you must always sign all versions of your app with the same key.)
			a keystore file
		I repeat : keep in a safe and secure place and ensure secure backups of
			a private cryptographic key
			a keystore file


Distribute your apk to a marketplace
	The developper will need :
		an app icon
		a high resolution app icon (only for google play)
		an End User License Agreement (EULA) (pas oblicatoire mais recommandé)
		a good package name
		
	Important notes :
		the app icon should follow the guidelines http://www.google.com/design/spec/style/icons.html#icons-product-icons
		the high resolution app icon
			should follow the same guidelines as the app icon +
			Requirements
				32-bit PNG (with alpha)
				Dimensions: 512px by 512px
				Maximum file size: 1024KB
				see : https://support.google.com/googleplay/android-developer/answer/1078870
		the End User License Agreement (EULA)
			A EULA can help protect your person, organization, and intellectual property, and it is recommended that you provide one with your application.
		the package name
			can't be changed after the app start be distributed
			should use Internet domain ownership exple : com.google
			shouldn't use com.example
			http://developer.android.com/guide/topics/manifest/manifest-element.html#package
			
	other infos :https://developer.android.com/studio/publish/app-signing.html

	Marketplaces
		Google play store
		Emails
		on a Website
		

### Add app on Google play

	go to https://play.google.com/apps/publish/signup/
	
Notes concernant le contrat : 

	https://play.google.com/about/developer-distribution-agreement.html
	Google prend un pourcentage de ce qu'on vend : 30%
	Vous devez fournir à Google tout certificat de résidence fiscale applicable. Si ni Google, ni ses fournisseurs de services ne reçoivent ces documents, nous effectuerons une retenue au taux de retenue à la source applicable dans le pays local.
	Le Développeur doit déterminer si un Produit est imposable, ainsi que le taux d'imposition auquel il sera soumis.
	Vous pouvez également décider de distribuer des Produits gratuitement. Si le Produit est gratuit, aucuns Frais de transaction ne sont facturés. Vous ne pouvez pas facturer un Produit qui était initialement gratuit, à moins que les frais ne correspondent à une version alternative du Produit. Le Prestataire chargé du traitement des paiements doit traiter tous les frais qu'un Développeur reçoit pour toute version d'un Produit distribué via le Store.
	En ce qui concerne les Produits payants ou les transactions via l'application, vous devez répondre aux demandes d'assistance des clients dans les trois (3) jours ouvrés, et dans les 24 heures en ce qui concerne toute assistance ou tout problème relatif à un Produit déclaré comme urgent par Google. Le fait de ne pas fournir des informations adéquates ni un service d'assistance pour vos Produits peut entraîner des avis médiocres sur le Produit, une exposition du produit moins importante, de mauvaises ventes, des contestations de facturation, ou la suppression de votre produit du Store.
	Vous ne devez pas utiliser des informations obtenues sur le Store pour vendre ou distribuer des Produits en dehors du Store
	Le présent Contrat restera en vigueur jusqu'à sa résiliation par vous-même ou par Google, conformément aux conditions définies ci-dessous.
	Si vous souhaitez résilier le présent Contrat, vous devez respecter un préavis de trente (30) jours et le notifier préalablement par écrit à Google (sauf si le Contrat est résilié en vertu de la clause 14.1) et cesser d'utiliser toute information d'identification liée à votre qualité de Développeur.
	
# How do I find out which keystore was used to sign an app?

Rename the .apk file with the extension .zip (for example let the file be "demofile.apk" then after renaming it becomes "demofile.apk.zip"). Navigate to  /META-INF/ and Then issue this command:
	
	/c/Program\ Files/Java/jdk1.8.0_71/bin/keytool -printcert -file CERT.RSA
	
You will get certificate fingerprints like this:
	
	Empreintes du certificat :
	 MD5:  9F:43:2C:1D:2C:1E:47:C0:9E:0F:57:5E:75:D5:F1:5B
	 SHA1 : AE:A8:18:CB:BD:35:28:3E:66:2D:4F:6B:2F:6F:5A:83:EC:D6:F9:11
	 SHA256 : 30:00:A0:99:A5:5E:DE:2C:FF:27:B8:B9:69:84:AA:E4:E6:E3:40:B0:A6:D9:7B:99:ED:60:49:40:15:38:0E:00
	 Nom de l'algorithme de signature : SHA256withRSA
	 Version : 3

Then use the keytool again to print out all the aliases of your signing keystore:

	/c/Program\ Files/Java/jdk1.8.0_71/bin/keytool -list -keystore /c/Keystore/keystore.jks

You will get a list of aliases and their certificate fingerprint:
	
	tieus, 22 juin 2016, PrivateKeyEntry,
	Empreinte du certificat (SHA1) : AE:A8:18:CB:BD:35:28:3E:66:2D:4F:6B:2F:6F:5A:83:EC:D6:F9:11

	
Related videos : 
https://www.udacity.com/course/viewer#!/c-ud855-nd/l-4435942462/m-4464858641




***********************************
Add Android Studio Statistics
***********************************


Go to http://plugins.jetbrains.com/plugin/?idea&id=4509 and install the latest version

To install

Run Android Studio
From the menu bar, select Android Studio > Preferences
Under IDE Settings, click Plugins and then click Install plugin from disk
Navigate to the folder where you downloaded the plugin and double-click it
Restart Android Studio
To count the lines

Check the statistics option that is visible after installing the plugin
This option is near the run, debug, gradle console, bottom left corner of android studio
UPDATE: 21/05/2015

If you cannot see the Statistics options, do the following:

1.Select VIEW from the toolbar.

2.Select TOOLS WINDOWS.

3.Choose STATISTICS.

You will see the statistics of your project and at the bottom, there is TOTAL section which displays the total lines under the Column of LINES.



***********************************
Cost of developping mobile apps
***********************************

http://theninehertz.com/insight-of-mobile-app-development-process



https://www.google.fr/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=android%20programming%20challenges

	






## 8 Gradle for Android and Java##


### Gradle fundamentals

#### Basic build for java

build a java file : 
	
	javac MyClass.java		--> MyClass.class
	
copy your images and xml ressources to the .class directory
	
	cp /MyJava/img.png /MyClass/img.png
	
generate some doc some documentation

	javadoc 
	
run multiple sets of units tests

	??
	
finally and if all tests passed : create a jar and push it to the repository

	jar ...
	
To do all of that you can create a shell script

#### Basic build for android

	doesn't use the java bytecode, but the custom android bytecode
	it more complicated
	
you can build differents kind of versions :

	release-version
	debug-version
	free-version
	paid-version
	
it is complex, we can't do it by hand or with a script, we will use gradle.

#### Gradle tasks

	is a set of actions
	start others tasks
	define its input : files it read from
	define its output : files it write to
	
#### Install gradle : no need to install, all it need it's gradle wrapper

	build.gradle
	gradle				--> a directory called gradle with a tiny .jar
	gradlew				--> a shell script for mac and linux
	gradlew.bat			--> same for windows
	
run the shell script 

	./gradlew
	
if gradle is not installed, it will install it. If it is already installed it won't. Then it gives you these infos : To run a build :

	gradlew <task>
	
to see a list of available tasks

	gradlew tasks
	
to see a list of command line options

	gradlew --help
	
to see moredetail about a task

	gradlew help --task <task>
	
#### Gradle deamon

Notes

	gradle needs to create an instance of the JVM and it can be a long task.
	Gradle deamon reduce this time by running it in the backgroung, and starting the same JVM automatically.
	Android studio uses Gradle deamon automatically
	but when on the console, we have to start it ourselves.
	
Always use Gradle deamon !!

#### Exercice 1

va utilier le default gradle file : build.gradle

	gradlew hello

va utiliser le gradle specifié : solution.gradle

	./gradlew -b solution.gradle hello

#### Exercice 2 : install gradle

we will install gradle because it will be easier for us, but in real life their will be no need to go through this process, we can use the gradle file created by android studio.
First make sure you have an installation of by running.

    $ java -version

The output should be something like:

    java version "1.8.0_51"
    Java(TM) SE Runtime Environment (build 1.8.0_51-b16)
    Java HotSpot(TM) 64-Bit Server VM (build 25.51-b03, mixed mode)

Download Gradle : take the 'complete distribution'

	http://gradle.org/gradle-download/

Unzip it in the directory you want 

	C:\Gradle
	
Add environnement variable : variable d'environement > Variable Systeme > Nouvelle > 

	GRADLE_HOME   C:\Gradle\gradle-2.11
	
Edit user variable PATH : variable d'environement > Variable Utilisateur > PATH >  and add 

	;%GRADLE_HOME%\bin
	
Run `gradle --version` to ensure the installation is complete.

	gradle --version
	
It didn't worked in my case I will use this instead 

	/c/Gradle/gradle-2.11/bin/gradle --version
	
Add a properties file to tell Gradle to use the daemon by default. In this directory

	C:\Users\Elorri\.gradle

Create a file named "gradle.properties" and add this line

	org.gradle.daemon=true
	
Ensure the daemon is stopped by running
	
	/c/Gradle/gradle-2.11/bin/gradle --stop

Note how long the task helloworld takes : 13.764 secs  on their machine 4.153 (my machine is shit)

	/c/Gradle/gradle-2.11/bin/gradle helloWorld
	
Run it again and note the time again :  2.346 secs (10 times less) on their machine 1.244

	/c/Gradle/gradle-2.11/bin/gradle helloWorld
	
To run gradle in quiet mode and see only our script output
	
	/c/Gradle/gradle-2.11/bin/gradle -q helloWorld
	
	

#### Gradle script

	json syntax
	"gradle build language" is called "gradle DSL" = "gradle Domain Specific Language" and is based on language groovy
	in our case the Domain Specific Language is "android"
	the entiere script has a delegate object
	plugins can be written in any JVM language (like java, groovy or scala) and use the same gradle script
	
#### Groovy fondamentals

Gradle provide its own groovy distribution so we don't need to install it. Groovy doesn't requiere to declare types (like javascript) ex :

	def foo = 6.5
	println "foo has value $foo"
	
Executing simple groovy code inside a string with curly-braces block and $ sign

	println "let's do some maths : 5 + 6 = ${5+6}"
	
We don't declare type, but a type is asign anyway, if we want to print it 

	println "foo is of type ${foo.class} and has value $foo"
	
Once variable is declared it can be reasign to a different type (but its not a good practice)

	foo="a string"
	println "foo is now of type ${foo.class} and has value $foo"
	
To declare functions : there is no return statements

	def doubleIt(n){
		n + n
	}

If no arguments function should be called as follow

	def noargs(){
	}
	noargs()
	
But if arguments there is 2 ways

	def oneargs(x){
	}
	oneargs(100)
	oneargs 100
	
	def oneargs(x, y){
	}
	oneargs(100, 200)
	oneargs 100, 200
	
#### Advanced Groovy features

###### Closure

Its a function that can be 

		packaged
		passed around
		assigned to variables
		they see variable from their outside environment like the class attribute can be seen in functions in java
		
You declare one like that 

	def closure={
	}
	closure()	
		
You assign it like that 

	def bar=closure 		<-notice no parenthesis
	def baz=bar
	baz()					<-because closure is a function, baz will also be
	
For arguments they have a different syntax

	def doubleIt={x -> x + x}
	
Closure can be used as an argument in a function

	def applyTwice(func, arg){
		func(func(arg)
	}
	
###### Closures and Lists

declare a list

	def mylist=["gradle","groovy", "android"]
	
excute a closure for each item

	def printItem(item -> println "item $item")
	mylist.each(printItem)
	
this syntax does the same thing. Note, when the closure have only one arg, this arg is called "it" by default.

	mylist.each{println "item $it"}
	

###### Closures and Classes

	class GroovyClass{
		String groovy="greeting"
		def printGreeting(){println "greeting : $greeting"}
	}
	
	def myGroovyClass = new GroovyClass()
	myGroovyClass.printGreeting()
	
	
when you do ... groovy automatically create getters and setters

	myGroovyClass.groovy="anoteher"
	
closure all have a "delegate" attribute that we can set to a class to access its data

	def greetingClosure = {
	greeting = "Setting the greeting from a closure"
	printGreeting()
	}

	// greetingClosure() // This doesn't work, because `greeting` isn't defined
	greetingClosure.delegate = myGroovyGreeter
	greetingClosure() // This works as `greeting` is a property of the delegate
	

#### More on groovy language

	https://learnxinyminutes.com/docs/groovy/
	http://groovy-lang.org/documentation.html

#### Task configuration

Any script has a "project" object. You can use it or ommit it. All thoses lines does the same thing

	project.task("MyTask")
	task("myTask")
	task "myTask"
	task myTask			<-because of abstract syntax tree transformation
	
Once the task is declared it's good to set the description and the group

	myTask.description="this task will do this"
	myTask.group="All my tasks"
	
Add the task at the end of the task list.Most used.

	myTask.doLast{
	}

or (idem doLast)

	myTask.leftShift{
	}
	
or (idem doLast)

	myTask <<{
	}	
	
in one line and most used way

	task myTask << {println ""}
	
Add the task on to front of the task list

	myTask.doFirst{
	}
	
We can also pass the config to task in one shot

	task myTask6{
		description "hhhh"			<-note no '=' sign. because description is a setter function in fact. It's because the configuartion closure delegate to the task
		group "some group"
		doLast{
		}
	}
	
If you are asigning a collection to a property in a configuartion closure, you need the equals

	task myTask7{
		description "hhhh"		
		group="some group"
		doLast{
		}
	}
	
Some task properties can be set in the task declaration, that is the case for a typed task
	
	task myTask8(description:"kkkk")<<{}
	
	
#### Task Dependencies and Ordering
	
depends on : le resultat de l'une permet à lautre de commencer (ou pas si la premiere à echoué)

	task putOnSocks {
		doLast {
			println "Putting on Socks."
		}
	}

	task putOnShoes {
		dependsOn "putOnSocks"
		doLast {
			println "Putting on Shoes."
		}
	}

finalize by : le resultat de l'une permet aussi à lautre de commencer (ou pas si la premiere à echoué)

	task eatBreakfast {
		finalizedBy "brushYourTeeth"
		doLast{
			println "Om nom nom breakfast!"
		}
	}

	task brushYourTeeth {
		doLast {
			println "Brushie Brushie Brushie."
		}
	}


should run after : le résultat de l'une n'empeche pas l'autre de commencer ??
The use case for `mustRunAfter` is slightly less obvious. Say we have a long
running process that's unlikely to fail, like deploying some artifact to a
continuous integration server, and we also have a short running task that is
likely to fail, like running unit tests. Those two tasks don't have any
dependency relationship, but if we're running both, we would really like the
unit tests to run before the integration tests.

	task takeShower {
		doLast {
			println "Taking a shower."
		}
	}

	task putOnFragrance {
		shouldRunAfter "takeShower"
		doLast{
			println "Smellin' fresh!"
		}
	}
	
	gradle putOnFragrance takeShower

note that very powerful function matching : look at all the tasks in the project and decide which ones we want to depend on

	task getEquipped {
		dependsOn tasks.matching{ task -> task.name.startsWith("putOn")}
		doLast {
			println "All geared up!"
		}
	}

to fail a task

task failTask << { task ->
	println "Running ${task.name}"
		throw new TaskExecutionException(task, new Exception('Fail task on purpose'))
}

exemple that will fail: 

	task failTask << { task ->
		println "Running ${task.name}"
			throw new TaskExecutionException(task, new Exception('Fail task on purpose'))
	}

	task successTask << {
		println "Running ${it.name}"
	}
	
	gradle failTask successTask
	
exemple that will continue eventhough it fail: This is also useful in a multi-module project where we might want to build all projects even though some may have failing tests, so we get a complete overview of failed tests for all modules.

	gradle --continue failTask successTask


to see only that must be started manually, check the "other task" section of the command 

	/c/Gradle/gradle-2.11/bin/gradle tasks 
	
to see all the tasks and their dependencies

	/c/Gradle/gradle-2.11/bin/gradle tasks --all
	
#### Typed task

a typed task is declared as follow

	task copyFiles(type:Copy)
	
the documentation can be found here 

	https://docs.gradle.org/current/dsl/org.gradle.api.tasks.Copy.html
	
copy all images

	task copyImages(type: Copy) {
		from 'images'
		into 'build'
	}
	
copy only jpeg

	task copyJpegs(type: Copy) {
		from 'images'
		include '*.jpg'
		into 'build'
	}
	
copy jpeg and gif in subfolder of build

	task copyImageFolders(type: Copy) {
		from('images') {
			include '*.jpg'
			into 'jpeg'
		}

		from('images') {
			include '*.gif'
			into 'gif'
		}

		into 'build'
	}
	
createimages.zip in build directory

	task zipImages(type: Zip) {
		baseName = 'images'
		destinationDir = file('build')
		from 'images'
	}
	
copy jpeg and gif in subfolder of build in an archive zip

	task zipImageFolders(type: Zip) {
		baseName = 'images'
		destinationDir = file('build')

		from('images') {
			include '*.jpg'
			into 'jpeg'
		}

		from('images') {
			include '*.gif'
			into 'gif'
		}
	}
	
delete the build older

	task deleteBuild(type: Delete) {
		delete 'build'
	}
	

Note the value of the Incremental Build : gradle check every task input and out put in its propertie file. If gradle see that input has change it check the output if it has change (files are missing) it will run again. When nothing has to be do task is : 

	UP_TO_DATE
	
#### Parametize your build to avoid having to rethink your script everytime you want to change something.

for the simple task :

task myTask <<{
	println greeting
}

with command-line argument (-P stands for property)
	
	gradle -Pgreeting="Hello from command lines" 
	
with gradle.properties

	greeting="Hello from properties" myTask
	
in the build.gradle

	ext {
		greeting = "Hello from build script"
	}
	
with environement variable


if several places are specified 

	command-line win over gradle.properties 
	build.gradle win over gradle.properties and command-line
	
	
#### Create your own type task

extends the default task task

	class MyTask extends DefaultTask {}
	
define a method annotated with the `@TaskAction` annotation

	class HelloTask extends DefaultTask {
    @TaskAction
		void doAction() {
			println 'Hello World'
		}
	}

use it 

	task hello(type: HelloTask)
	
add properties if needed

	class HelloNameTask extends DefaultTask {
		String firstName

		@TaskAction
		void doAction() {
			println "Hello, $firstName"
		}
	}
	
to use it 

task helloName(type: HelloNameTask) {
    firstName = 'Jeremy'
}


#### Add log messages

debug -d : give a lot of info rarely useful. to find something specific add | grep 'Catch me if you can' for linux and  | findstr 'Catch me if you can' for windows

		gradle -b solution.gradle --debug hello | grep 'Catch me if you can'
		gradle -b solution.gradle --debug hello | findstr 'Catch me if you can'
	
info : better info like -i

	how long each task takes to complete
	when gradle connect to its deamon
	
lifecycle (pas de -l car c'est le default)
	
	total time the build took
	is build successful
	
quiet -q

	messages that should be displayed even if the user has chosen to be quiet
	will only display your println (i think)
	
error -e

	for errors
	
by default lifecycle, quiet and error messages are displayed. Running ... will display debug, info, lifecycle, quiet and error messages

	gradle -d toto 
	
Running ... will display info, lifecycle, quiet and error messages

	gradle -i toto 
	
And so on. To see the stacktrace just of your code

	gradle --stacktrace ou
	gradle -s
	
To see the entiere stacktrace including gradle core code

	gradle --full-stacktrace ou
	gradle -S
	
#### Gradle build is sudivided into 3 action

	initialization : app tree
	configuration : finding task tree
	execution : all actions areexecuted in proper order
	

### Building Java with Gradle

It's simplier to build java project than android project. The list of task is : 

	compile
	create a jar
	generate doc
	run the test
	generate report
	
#### Using java plugin

In the build.gradle add

	apply plugin : "java"
	
Run gradle tasks to see what the plugin is capable of. Most often we will use :

	assemble
	build
	clean
	test
	
Assemble

	create the app
	usually in a jar
	but could in more complex artifacts
	assume that the source isin folder  src/main/java
	
Check

	run any task we have set up
	
Build 

	depends on assemble and check
	
Clean

	delete all the buid output
	
To execute we need to create a task

	task execute(type: JavaExec) {
		main = "com.udacity.gradle.Person"
		// We'll talk about this shortly
		classpath = sourceSets.main.runtimeClasspath
	}

### To create a jar 

in build.gradle add

	apply plugin: 'java'
	
run

	gradle jar
	
this will create a jar in \build\tmp directory

### Default gradle configuration

	/src/main/java
	/src/main/ressources
	/src/test/java
	/src/test/ressources
	/build/classes/main
	/build/classes/test
	/build/libs

Configuration can bechange in the build.gradle see documentation

	https://docs.gradle.org/current/userguide/tutorial_java_projects.html
	https://docs.gradle.org/current/userguide/java_plugin.html	
	
	
### Internet repositories

most commons are 

	mavenCentral()
	jcenter()
	
gradle find an artifact by its unique set of coordinates
	example :   junit:junit:4.12

	
it download it and store in your local cache.

### Add a dependency

the most basic sort of repository, is just a folder full of jar called

	flat directory repository : flatDir
	
repositories configuration are done in repositories script bloc, if the dependency is not available from a remote repository use 

	repositories {
		flatDir {
			dirs 'libs'
		}
	}
	
if available from a remote repository but you don't know which one, put them all

	repositories {
		mavenCentral()
		mavenLocal()
		jcenter()
	}
	
if available on a maven URL

repositories {
    maven {
        url 'https://repo.foo.org/m2'
    }
}

if available on a ivy URL

repositories {
    ivy {
        url 'https://repo.foo.org/m2'
    }
}

if credentials are needed 

	repositories {
		maven {
			url 'https://repo.foo.org/ivy'
			credentials {
				username 'user'
				password 'secret'
			}
		}
	}

or 

	repositories {
		ivy {
			url 'https://repo.foo.org/ivy'
			credentials {
				username 'user'
				password 'secret'
			}
		}
	}

	
with https protocol

	repositories {
		ivy {
			url 'https://repo.foo.org/m2'
		}
	}

with http protocol

	repositories {
		ivy {
			url 'http://repo.foo.org/m2'
		}
	}
	
with sftp protocol

	repositories {
		ivy {
			url 'sftp://repo.foo.org/m2'
		}
	}

file based repository

	repositories {
		ivy {
			url 'file:///home/user/repo'
		}
	}

Once we have defined the repository, we can define artifacts adding it to the 'compile' task of the java plugin like this in gradle

	dependencies {
		compile 'com.google.guava:guava:18.0'
	}

like this with groovy (wich is undertood by graddle and is equivalent to the above)

	dependencies {
		compile group: 'com.google.guava', name: 'guava', version: '18.0'
	}

for file dependencies

	dependencies {
		compile files('libs/foo.jar', 'libs/bar.jar')
	}

or this (will take only jars from lib directory)

	dependencies {
		compile fileTree(dir: 'libs', include: '*.jar')
	}
	
to see all the dependencies that have been configured for the 'compile' configuration in your build.gradle

	apply plugin: 'java'

	task printDependencies << {
		configurations.compile.each { println it.name }
	}
	
now to download dependencies from repository not from cache use

	gradle printDependencies --refresh-dependencies
	
to use the cache

	gradle printDependencies
	
to generate a dependency report. Note : The report breaks out dependencies by each configuration.

	gradle dependencies
	
To see the dependencies for a particular configuration (config in java plugin are : compile runtime testCompile) ex :for runtime

	gradle dependencies --configuration runtime
	
To look at a particular dependency useful when 2 dependencies use the same artifact but with different version. Gradle resolve conflict version by taking the newest. and display an arrow ->

	gradle dependencyInsight --dependency commons-logging
	
logically related dependencies are grouped into configurations

	dependencies in compile are only available the main code
	dependencies in testCompile are only available the test code
	testCompile extends compile configauration which means that all compile depencies are included in testCompile depencies you see it in 'gradle dependencies'
	
to create a custom configuration

	configurations {
		custom
	}

	dependencies {
		custom 'com.google.guava:guava:18.0'
	}
	
in fact configurations are just a collection of files (jars) and can be used anywhere we use a cllection like here 

	task copyDependencies(type: Copy) {
		from configurations.custom
		into 'build/libs'
	}
	
or for zip, this will create a 'dependencyArchive-4.2-deps.zip' in build/distributions directory

	task zipDeps(type: Zip) { // 5. Add Zip task to bundle dependencies from 'deps'
		version = "4.2"
		baseName = "dependencyArchive"
		classifier = 'deps'
		from configurations.deps
	}
	
scheme for namings are 

	basename-appendix-version-classifier-extension
	
to make a config extends another config

	configurations {
		deps // 1. Create 'deps' configuration
		compile.extendsFrom deps // 2. Make 'compile' extend from 'deps'
	}
	

### Tests

Unit tests

	test classes or method in isolation
	
Integrated test

	test to code with libraries, or others environements
	
It's good practice to incorporate test execution into our build process

	means everychange in our code is tested
	
test should be in the 
	
	src/test/java folder
	
then you need to add a test dependencie like junit

	apply plugin: 'java'

	repositories {
		mavenCentral()
	}

	dependencies {
		testCompile 'junit:junit:4.12'
	}

then run ... if the build is successful that means all the test passed

	gradle test
	
note that a report is always generated and can be found in the ... directory. When something goes wrong you can see the fullstack trace

	build\reports\tests 
	
Most commonly used gradle plugins doc

	https://docs.gradle.org/current/userguide/standard_plugins.html
	Plugins written by third parties : https://plugins.gradle.org/
	
Gradle plugins categories

	Languages plugins like Java or Scala
	Integration plugins forcreating different sorts of artifacts
	Software developpement pluggins to make software dev easier
	
You use those plugins as follow

	buildscript{
		repositories{
			maven{
				url "https://pluggins.graddle.org/m2/"
			}
		}
		dependencies{
			classpath "com.toto.org:1:2:3"
		}
	}
	apply plugin : "com.toto.org"
	
or like that 

	plugins{
		id "com.toto.org" version "1:2:3"
	}
	
To make everyone building your project building it with the exact same tool (and not the gradle install on your machine) you can use the gradle wrapper, to create it type : 

	gradle wrapper
	
Now we use ... instead of gradle

	./gradlew
	
We can create a specific version of wrapper by adding ... to the build.gradle and run gradle wrapper again

	wrapper {
		gradleVersion = '2.2'
	}

To checkout the version used by the wrapper

	./gradlew --version
	
Configuration options of the wrapper is stored in the gradle\wrapper\gradle-wrapper.properties file where you can see the url to the correct version of graddle

	distributionUrl=https\://services.gradle.org/distributions/gradle-2.2-bin.zip
	
### Gradle and Android Studio

import a gradle file

	file > import project > select gradle file > use wrapper ? OK
	
to use the Android studio terminal first with windows 10 enable the Use legacy console option

	app> dos >invite de commande >click droit > properties > Use legacy console

you will need execution permission as follow (on linux)

	chmod +x gradlew
	
you will need execution permission as follow (on windows)

	right click the gradlew.bat file > properties > Advanced > sharing > check all
	note : type .\gradlew theTask instead of ./gradlew theTask because windows
	
you can also open the gradle windows 

	open gradle windows > select your build.gradle > double click the task you want to run
	
as you can see when executing task from the IDE it generate many others files what are they ?

	.gradle : keeps tracks of tasks input and output
	.idea : it store it's models of your project
	build : where you build output goes
	gradle : where wrapper jars and wrapper.gradle.properties goes
	.iml : useful for IDE 
	local.properties : with the android sdk location on your machine
	
to paste or include a .gradle into another one add this line

	apply from: "solution.gradle"
	
### to run a Java project solution 1

In the Main class 

	public class JokeTeller {

		public static void main(String[] args){
			System.out.println("Java. Write once, debug everywere.");
		}
	}

In the build gradle

	apply plugin: 'application'
	mainClassName = "com.udacity.gradle.JokeTeller"
	
Now the application plugin gives you the run task

	gradlew run
	
### to run a Java project solution 2 : create your own run method with the JavaExec task type

	task solutionExecute(type: JavaExec) {
		main = "com.udacity.gradle.JokeTeller"
		classpath = sourceSets.main.runtimeClasspath
	}

	gradlew solutionExecute
	
### Adroid plugin

	build and package your app
	provide bunch of configurations : 6 main themes
	provide bunch of customisations
	build variants
	application signing
	pro guarding
	testing
	
	
Look at the project defaut build.gradle

	it's a multiproject by default to make it easy to add libraries or other projects
	note the artifact com.android.tools.build:gradle:1.5.0 where we take our gradlescript
	and the allprojects block that adds the jcenter repository to every subproject of our build, means that every subproject only have to declare their artifact dependencies
	
Look at the module defaut build.gradle	

	first apply the android plugin
	then follow the Android Configuration Block
	then the dependencies bloc that works like Java dependencies

Android Configuration Block minimum requierement

    compileSdkVersion 23
    buildToolsVersion "23.0.1"

Android Configuration Block optional requierement

	defaultConfig
	buildType
	
More infos

	https://developer.android.com/tools/building/plugin-for-gradle.html
	http://tools.android.com/tech-docs/new-build-system/user-guide
	
### Build Variants

	product flavor free build type debug
	product flavor free build type release
	product flavor paid build type debug
	product flavor paid build type release	

buildTypes are declared in the buildType block of the Android Configuration Block. Note the debug buildType exist even you don't see it

	minifyEnabled false -> packaging optimisation is disabled
	proguardFiles getDefaultProguardFile -> tells where the proguard config is
	
In the gradle pane note the tasks

	assembleDebug
	assembleRelease
	
Or open the buildVariant pane on the bottom-right and select

	debug
	release

To configure an addition build type you need to add an android block a follow

	android {
		buildTypes {
			release {
				gameTesting
			}
		}
	}

To add a free flavor and a paid flavor place them in a `productFlavors { }` script block and assign them unique application ids. That way we can install both flavors on the same device.


	apply plugin: 'com.android.application'

	android {
		compileSdkVersion 22
		buildToolsVersion "22.0.1"

		defaultConfig {
			applicationId "com.example.udacity.declaringflavors"
			minSdkVersion 10
			targetSdkVersion 22
			versionCode 1
			versionName "1.0"
		}

		buildTypes {
			release {
				minifyEnabled false
				proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
			}
		}

		productFlavors {
			free {
				applicationId "com.example.udacity.declaringflavors.free"
			}
			paid {
				applicationId "com.example.udacity.declaringflavors.paid"
			}
		}
		
		android {
			buildTypes {
				debug {
					debuggable false
				}
			}
		}
	}
	
Sync gradle and see the 2 new directories

	src/free/java' and 'src/free/res
	src/paid/java' and 'src/paid/res
	
To add strings that are specific to the free and paid flavors. 

	Select New > Android resource file. Name file `strings`, and change the source set from `main` to `paid`, and add a string with a custom message.
	
To run a flavor, go to the the Build Variants pane at the bottom left of Android studio

	select freeDebug and hit run
	
To place flavor-specific configuration in our Gradle build file. Any configuration that we can put in `defaultConfig { }` script block can also be placed in a flavor configuration block.

	productFlavors {
		paid {
			minSdkVersion 21
		}
	}
	
### Source sets 

how does gradle create sourceSet ?

	it create the src/main
	then one for each flavor src/free and src/paid
	then one for debug src/debug
	then one for release src/release
	then one for each variant that means src/freeDebug, src/freeRelease, src/paidDebug, src/paidRelease
	then one for each variant that means src/freeMdpiDebug, src/freeMdpiRelease, src/paidMdpiDebug, src/paidMdpiRelease, src/freeHdpiDebug, src/freeHdpiRelease, src/paidHdpiDebug, src/paidHdpiRelease
	
conclusion put your source code in the correct directory. the most specific configuration overide the most specific config. BUT java class file can't be overriden.

	no multiple for identical java definition
	multiples are allowed in res, and manifest because every items are transformed by IDs and merge is possible
	
### Configurations

How does android plugin will create configuration foreach variant ?

	compile config and runtime config
	paidCompile config and paidRuntime config
	freeCompile config and freeRuntime config
	
To declare a librairie only for the free version. Here is google ads

	dependencies {
		compile fileTree(dir: 'libs', include: ['*.jar'])
		compile 'com.android.support:appcompat-v7:22.1.1'
		freeCompile 'com.google.android.gms:play-services:7.0.0'
	}
	
Depending on the type of project we need, we will choose a type variant, this is repesenting a list of tasks to perform.

	Application variant -> for apps -> ADK
	Library variant -> for libraries -> AAR
	Test variant -> for apk -> APK
	
Because we don't know the names of the variants in advance we reference them as a collection as follow

	applicationVariants.all
	libraryVariants.all
	testVariants.all
	
Exemple to add a compite argument to all of our application tasks

	applicationVariants.all{
		if(buildType == 'debug'){
			javaCompile.options.compilerArgs = ['-verbose']
		}
	}
	
### Libraries

to create a librarie we can create a java project 

	that build a jar file
	
to create a librarie we can create a android project 

	that build a aar file (android archive)
	
differences
	
	aar can include it's own ressources and manifest
	jar can be used in non android projects
	jar are easier to convert into aar if needed in the future, so make choice carefully
	if it needs a res and/or a manifest it needs to be a aar
	Android libraries are android apps that can't be run on their own
	
common hierarchy of a project

	/myProject/librairies/javaLib
	/myProject/librairies/androidLib
	/myProject/app1   <-modules also called subprojects
	/myProject/app2
	/myProject/setting.gradle  <-where this hierarchy configuration is registered, this file is generated by android studio

### Add Java/ Android library
	
libraries have a build.gradle file and can be build on their own. To use a library in our project

	1. Add the library as a module
	2. Go to settings.gradle
	
In settings.gradle the module

	include ':app', ':javaJokes'
	
To check projects subproject of your build

	gradlew projects
	
Declare a dependency between our app module and the library javaJokes this in done in the app build.graddle in block dependencies add ... Note : When we declare our dependency on the :javaJokes project, we're actually depending on the "default" configuration of :javaJokes, which contains the output JAR.
	
	compile project(':javaJokes')
	
Import our java library into our android project

	import com.udacity.gradle.jokes.Joker;
	
	
### Signing an apk

#### create a keystore and key once

create a key store 

	they create it in the project directory (surprising)
	they put password 'password'

create a key

	they put alias : Udacity
	they put password 'password'
	
#### create a key store and key with automatic signing

app > open module setting> signing tab > 

	name : config
	alias : Udacity
	key password 'password'
	store file : keystore.jks
	store password : 'password'
	
app > open module setting> build type > 

	select 'release' build type
	name : release
	signing config : config
	
look at the build.gradle, ... have beed added to the android block

    signingConfigs {
        config {
            keyAlias 'Udacity'
            keyPassword 'password'
            storeFile file('C:/AndroidStudioProjects/Examples/JavaJokesApp/keystore.jks')
            storePassword 'password'
        }
    }
	
plus the android buildTypes bloc now has a new config line

	buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
			signingConfig signingConfig.config
        }
    }

check gradle panel we now have

	an install release task
	
replace the absolute path 'C:/AndroidStudioProjects/Examples/JavaJokesApp/keystore.jks' by

	'$rootdir/keystore.jks'

### MultiDex

Solving the trouble writing output: Too many method references: 70936; max is 65536. caused by project with over 70 000 methods. The Android virtual machine doesn't actually run Java byte code, it runs Dalvik byte code, and there's a build step after Java compilation where the Java byte code is turned into Dalvik byte code. This step is called Dexing. Part of this process is compiling a
table of every method in the application, which is indexed with two bytes. That means we're limited to 65k methods. Fortunately, we can ask Gradle to simply break up this table into multiple tables simply by setting multiDexEnabled true in the app build gradle
    defaultConfig {
        applicationId "com.udacity.gradle.multidex"
        minSdkVersion 10
        targetSdkVersion 22
        versionCode 1
        versionName "1.0"
        multiDexEnabled true
    }

### Proguard (part of android plugin)

can

	reduce app size by remove unused code and ressources
	obfuscating the code : give each class and methods meaningless names
	minifyEnabled : turn on magnification
	shrinkRessources : remove unused code and ressources
	
try this config

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
        shrunk {
            minifyEnabled true
            shrinkResources true
        }
        big {
            minifyEnabled false
            shrinkResources false
        }
    }
	
And check the apk size, you see the shrunk win over others.

### Tests

there are 2 kinds

	unit test 
	connected test run on android device
	
unit tests

	run on java vm
	used for testing generic non android related java classes
	run on a mock androidsdk implementation -> means any code that call the android API will fail.
	if it's failing used mockito to mock the appropriate dependencies or use connected tests
	in src/test
	
connected tests

	in /src/androidTest
	if encounter 'Unable to find instrumentation info for: ComponentInfo' set the value of Test Instrumentation Runner to "android.test.InstrumentationTestRunner" in Project Structure > app > Flavors > defaultConfig > Test Instrumentation Runner. or in app build.gradle android default config testInstrumentationRunner 'android.test.InstrumentationTestRunner'
	
more infos
		
		https://www.udacity.com/course/viewer#!/c-ud867-nd/l-3983839023/e-4327702382/m-4362428736
		https://developer.android.com/training/activity-testing/activity-ui-testing.html
	
### List of Google play services

	https://developers.google.com/android/guides/setup
	
### How to install different app variants on one Android device

	https://blog.grandcentrix.net/how-to-install-different-app-variants-on-one-android-device/
	
	
### How to have several flavor with content provider

	see my old xyzreader in C:\Users\Elorri\Dropbox\Udacity\Projects\Project5\MyOldXyzReader
	



## 9 Material Design##


	
(I moved everything in the file Make your app Material)
	

	


## 99 Webcast KickOff App entrepreneurship##

Entrepreuneur strategies created at Google lectures and used at 
google
air bnb
nest


Yellow booklet


They use this strategie when they are creating a new feature 
6 stages :

understanding defining the pb
list of all the possible solutions even if nearly impossible
decide : all the team come together vote and talk
mock up your ideas : scketch design
go on forum show your idea, see if there is a demand, find some friends to develop them.
develop them


Build only what you need and not more and iterate as fast as you can.


## 99 Webcast KickOff Career development opportunities##

1. Google is looking for people and they want people
2. Active on forums
3. Being able to socialise



## 99 Webcast KickOff How Courses are made at Udacity##


https://plus.google.com/u/0/events/ci2k08lm0kfc6onms692rcpvqac?authkey=CMn7mOPwlPiJag

1. Request from Google : we need a course on java

2. Work on the code

3. Work on the Script

4. Work on Look and feel. 
must have headshop : when we see the instructor
tablet work : instructor is drawing
screen cast work : instructor is using android studio or google dashboard

For example Google play is a very hard course with a lot of code, look and feel was very important.

5. Choose the instructor.
Most of the instructors are not used to teach. So they give the script to several people (4 or 5) and they record them.
A jury thumb up or not. And we block the auditorium.

6. Auditorium

7. Materiel for Tablet work and Screen cast
a computer
tablet attach to the desk
a big light over the handto remove any shadows
a camera above

8. 2 record videos are made
one from the camera (where we see the hands of the instructor)
one from the tablet(screen recorded)

9. Traitement des images
les 2 videos sont supperposées (layers)
celle de la camera est mise en dessous de celle de la tablette.

10. The computer is use for the script.

11. when they start they push a button that make a noise, similar to taper dans les mains (CLAP). That helps to sync the 2 videos later. Et pour supprimer des passages qu'on a pas aimé.

12. To give an idea : 
for 15 min result video, instructor will be recording 1h-1h30
traitement team : 4 to 6 hours to edit

13. Un petit post it toujours devant pour verifier que les dernieres verifs ont étées faites :
room light is off. Seul le bureau est eclaire.
video 1 ON
video 2 ON
CLAP

14. La tablet a des lignes qui permettent de savoir qu'est-ce qui ne se vera pas sur Youtube

The android fundamental course tooks 8 weeks to do, but was exhausting, people didn't take week-end

15. Ecrire sur une vitre. La vitre est entre la camera et l'instructeur. Ensuite l'image est renversée la gauche devient ladroite de la persone, mais ca permet d'avoir l'ecritrure dans le bon sens.

16. Ils utilisent un ecran vert aussi.

17. After videos are recorded. They are watched and they have to pass the QA session.


## 99 Webcast KickOff Meet an Android Engineer##

Java books
effective java one
java consurency and practice


In team : 
we try to avoid working on the same class and doing major changing
some people for the UI
some people for the background processes
getting use to git and push issues (merging issues) and how to fix them.

Before the good libraries for images, it was very easy to get out of memories exceptions, to solve that we uses 
java heap analysis tools
you have to convert your android code into java code before using thoses tools
they are good because they let you know what is the gc_root means garbage collector root means the object that are still here
others tools androids include that are good : 
	profiling tools : 
	layout performance :
	debugging tool : are you achieving 60 frames per second ? are you overdrawing ?
small leaks may leaks in big leaks if there is a big number of transaction like 600 and those are not easy to find.

Use activities first and fragment laters if you are in trouble.
See Meet an Android Developer Webcast Suggested Resources.pdf. in C:\Users\Elorri\Dropbox\Udacity\Classes\99 Webcast KickOff


## 99 Webcast KickOff App entrepreneurship##


Entrepreuneur strategies created at Google lectures and used at 
google
air bnb
nest


Yellow booklet


They use this strategie when they are creating a new feature 
6 stages :

understanding defining the pb
list of all the possible solutions even if nearly impossible
decide : all the team come together vote and talk
mock up your ideas : scketch design
go on forum show your idea, see if there is a demand, find some friends to develop them.
develop them


Build only what you need and not more and iterate as fast as you can.


## 99 Webcast KickOff Tips Tricks and Troubleshooting in Android Studio Webcast##

1. Set Auto-import

	Android studio>Settings>Editor>General>AutoImport> put Insert imports on paste : All and check all the remaining boxes.

2. Pour chercher une action : 
	
	Ctrl+Shift+A

3. Pour ouvrir une classe

	Ctrl + n

4. Pour ouvrir une ressource ou xml file
	
	Ctrl+Shift+n

5. Pour copier une ligne et la coller juste en dessous
	
	Ctrl + d

6. Pour copier plusieurs lignes

	Alt+Up (mais ça marche pas) Selectionner les lignes ou le mot
	Ctrl + d

7. lien hypertext sur nom de classe ou methode

	Ctrl+Alt+mouse over

8. Pour revoir les paramettres qu'il faut dans la methode

	Ctrl+P

9. Afficher la liste des "Live Template"
	
	Ctrl+J

10. Afficher une live template

	[template_name]+Enter

11.

The tools context mirror all the attributes from the android namespace, it allows you to only have the value appearing in the build type.

               <TextView
                    android:id="@+id/releaseYear"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
					android:text="2015"/>
					
We don't want the 2015 to appear in realtime because it will be replaced, and it will use memory for nothing. But we want to see it in the preview to help us visualise. What we do is : 

               <TextView
                    android:id="@+id/releaseYear"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
					tools:text="2015"/>
					
12. Pour voir le menu avec l'ampoule rouge

	Alt+Enter


13. To remove unused imports

	Ctrl + Alt + O   stand for optimize



14. Wrap when typing reaches right margin

	In File | Settings, select "Editor", then "Code Style". There is an option "Wrap when typing reaches right margin".
	Edit: Just tried it, and it doesn't seem to work. Anyway, maybe the option "Use soft wrap" in the "General" group is more what you want.



## 99 Webcast KickOff Whats it like to work as an Android dev in the real world##

In an engeneering team there is 
product management team : scope the project, what features, what user exp
design team : scketch the design elements
engeneering team

role : engeneer developper that makes courses at Udacity.
20% coding
80% tasks administratives : 
	writting scripts for the courses
	stuff around supporting the code that I'm writting 
	
	
We try to spend more time on the planning phase and less on the coding, if you plan too little your code crash
The code is always the least we need to do.

The big project is divided in weeks of work every week why launch some improvements:
each week you : 
developp
test things


What the code review process at Udacity ?
on cree notre branch
on envoie une pull request sur la main branch d'udacity
you sign in to a person
that person gives feedback
when she gives thumb up
you can merge it in.


What is the optimal side project and employer should be doing ?
one is enough if it is good quality. people won't take the time to scroll all your projects.

Udacity engeneering team :50-20 people

Engeneering is a lot more social that what I had imagine.
Everyday you talk to your team about how you will design the next piece of code.


Apply to a lot of work, just to practice interview
book "Cracking to coding interview" full of questions.



# Others

to make a recycler view autofit column gridlayout 

	http://blog.sqisland.com/2014/12/recyclerview-autofit-grid.html
	
note : GridLayoutManager or StaggeredGridLayoutManager don't adjust the column width to fit the screen, they display exacty the width given in the width property


# Volley vs Retrofit and Picasso

Caching Round 4
Cache control can play a pretty important role when choosing between Retrofit and Volley.  Retrofit, unfortunately, does not offer much cache control and what is offered is managed solely through the request headers.  This isn’t a totally unreasonable, but retrieving a response from a previously completed request is not an option short of making the request again.  With Volley, you can retrieve a previous response from the RequestQueue by using the URL as the cache key.  With Volley you can also clear the cache for a specific response or the cache for the whole RequestQueue forcing the framework to retrieve a new, updated response at your discretion. Some of Volley’s caching abilities are shown below. Round 4: Volley.

 Volley comes packaged with a loader specifically designed to download images for you.  Packaged along with the loader is a custom view called the NetworkImageView in which the developer only has to hand a URL and an ImageLoader to and Volley does the rest.  This view is specifically targeted to work well with list views and allow for automatic cancellation of requests when the images parent view is destroyed.  On the contrary, Retrofit does not easily support image downloads.  To accomplish what we are able to with Volley, one would be required to download and include another library in your project such as Picasso.  Round 5: Volley.
	



# Go ubiquitous

devices with android

	wearable =watches
	living room
	car
	desk
	
infos : 

	Que peut-on vraiment faire avec une montre Android Wear ? FrAndroid
	

## Android wear

wearable app user allways known context is :

	time
	location
	physical activity
	
it is a personal assistant that ask input from the user only when necessary, most input are

	touch swipes
	voice
	no fine grain finger movements
	
3 main experience you can give to the user : 

	notifications
	watch faces
	apps
	
### notifications : 

already in traditional apps 

	any android app with notifications already work on the watch
	if the notification have an action, it's also working on the watch

what you can add

	stacks : rich inbox style notif, deliver multiple items in a single bundle
	pages : for showing multiple screen of info on the same topic
	replies : allow the user to respond directly from the wearable with their voice
	
see 

	https://www.udacity.com/course/viewer#!/c-ud875-nd/l-4582702279/m-4584569889
	
### watch faces design guidelines

create faces for 

	round watches
	squares watches
	
choose the best mode

	interactive mode : full color and motion with fluid animation -> when the user is giving attention to his watch
	ambient mode : low color state, limited color palette that's only updated once a minute. 95% of the sc
	
ambient mode take special screens into account

	low bit screens : pixel in ambient mode are either on or off. Means only use black or white with no anti aliasing
	use burn in protection techniques with OLED screens : avoid large blocks of opaque pixels
	95% of the screen in the ambient mode should be black
	
start a sample or template in android studio, it will create 

	CanvasWatchFaceService.Engine
	onCreate : load ressources, init paint objects for later use
	onSurfaceChange : where you can scale these objects, the screen size is passed as one of it's parameters, it is where to scale you bitmap background if you have one
	onDraw : draws your design to the canvas at a high enough frame rate to deliver fluid animation, it is use in interactive mode and ambient mode
	SystemUI elements : you can place them where you want
	
### more on notifications

	when an handheld device and a wearable are connected, the handheld automatically pushes notifications to it
	on the wearable each notif appear as a new card
	
### how to add a notification sample "Basic Notifications"

each notification we generate must have a unique value, 2 notif with the same ID will override the 1st one.

	    public static final int NOTIFICATION_ID = 1;
		
then we need a pendig intent

	Intent intent = new Intent(Intent.ACTION_VIEW,
			Uri.parse("http://developer.android.com/reference/android/app/Notification.html"));
	PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);
		
we need a notification builder that will allow us to call methods on this

	NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
	
set the small top icon. although you can use any drawable as the small icon, Android design guidelines state that the icon should be simple and monochrome. Full-color bitmaps or busy images don't render well on smaller screens and can end up confusing the user.

	builder.setSmallIcon(R.drawable.ic_stat_notification);
	
set the intent

	builder.setContentIntent(pendingIntent);
	
make the notification automatically disappear when it's clicked on

    builder.setAutoCancel(true);
	
set the left large icon. The app icon is a reasonable default if you don't have anything more compelling to use as an icon.

	builder.setLargeIcon(BitmapFactory.decodeResource(getResources(), R.drawable.ic_launcher));
	
add title, text, subtext

	builder.setContentTitle("BasicNotifications Sample");
	builder.setContentText("Time to learn about notifications!");
	builder.setSubText("Tap to view documentation about notifications.");
	
get a notification manager

    NotificationManager notificationManager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
	
give the notification to the notificationManager

	notificationManager.notify(NOTIFICATION_ID, builder.build());
	
to run the app make sure you are compiling against the v4 support library

	check the gradle
	
for newer appcompatibility replace NotificationManager by

	NotificationManagerCompat
	
witch make 

	NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
	
to add an action button use the builder. note : any notification that was created on the phone always cause the intent to run on the phone as well, not the wearable

	builder.addAction(R.drawable.icon, "desc string", pending intent for the action)  
	
to have different action on the wearble and the phone by using a wearable extender and instead of builder.addAction we do ...Note that by doing so, none of theregular addActions will be called on the wearable

	builder.extend(new WearableExtender().addAction(action))
	
and create a wearable specific action

	NotificationCompat.Action action = new NotificationCompat.Action.Builder(R.drawable.icon, "desc string", pending intent for the action).build();
	
### big view style notifications

when you touch those notifs, it expends to show more informations

	on phone it's like a dialog
	on wear device it filled the display
	
exemple

	BigTextStyle.bigStyle = new NotificationCompat.BigTextStyle();
	bigStyle.bigText(evenDescription);
	
	NotificationCompat.Builder notificationBuilder =new NotificationCompat.Builder(this)
			.setSmallIcon()
			.setLargeIcon()
			.setContentTitle()
			.setContentText()
			.setContentIntent()
			.addAction()
			.setStyle(bigStyle);
			
Note the largeIcon from the setLargeIcon is automatically used as a background image in the android wear with size of 64x64dp. If you want bigger use that 

	NotificationCompat.WearableExtender wearableExtender = new NotificationCompat.WearableExtender()
		.setHintHideIcon(true)
		.setBackground(mBitmap);  //can use high resolution bitmap (as a difference to set icon), 
		
	Notification notif=new NotificationCompat.Builder(mContext)
			.setContentTitle()
			.setContentText()
			.setSmallIcon()
			.extend()
			.build();
			
but if your image is too big you can overwhelm the memory that's why we recommand 

	400x400dp if you have static background
	640x400dp if you have an image parallax added where the left and right edges are used to simulate background mouvement
	both in drawable-nodpi
	
### reply by voice notifications

you will use the RemoteInput class

	//key for string that is delivered in action's intent
	private static final String EXTRA_VOICE_REPLY = "extra_voice_reply"
	
	//a string telling the user what we want to speak to us
	String replyLabel = getRessources().getString(R.string.reply_label)

	RemoteInput remoteInput = new RemoteInput.Builder(EXTRA_VOICE_REPLY)
		.setLabel(replyLabel)
		.build()
		
then add the remote input to our notification

	//create an intent for the reply action
	Intent intent = new Intent(this, ReplyActivity.class);
	PendingIntent replyIntent = PendingIntent.getActivity(this, 0, replyIntent, PendingIntent.FLAG_UPDATE_CURRENT);	
	
	//createthereply action and add a remote input
	NotificationCompat.Action action = new NotificationCompat.Action.Builder(R.drawable.reply_icon, "desc string", replyIntent)
		.addRemoteInput(remoteInput)
		.build();
		
	
	//create the notif for wearable
	NotificationCompat.Builder notificationBuilder =new NotificationCompat.Builder(this)
			.setSmallIcon()
			.setContentTitle()
			.setContentText()
			.extend(new WearableExtender().addAction(action))
			.build()
			
	//issue the notif
	NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
	notificationManager.notify();
	
to get the reply string back in the ReplyActivity onCreate  call

	getMessageText(getIntent())
	
and then implement the function
	
	private CharSequence getMessageText(Intent intent){
		Bundle remoteIntent = RemoteInput.getResultFromIntent(intent);
		if(remoteInput != null){
			return remote.getCharSequence(EXTRA_VOICE_REPLY)
		}
		return null;
	}

note there is also support for emoji in android wear.

To allow the user to choice how to reply,use theset choices method, to do so set the remoteInput as follow

	//key for string that is delivered in action's intent
	private static final String EXTRA_VOICE_REPLY = "extra_voice_reply"
	
	
	//a string telling the user what we want to speak to us
	String replyLabel = getRessources().getString(R.string.reply_label)
	
	//an array of choices
	String replyChoices = getRessources().getString(R.string.reply_choices)	

	RemoteInput remoteInput = new RemoteInput.Builder(EXTRA_VOICE_REPLY)
		.setLabel(replyLabel)
		.setChoices(replyChoices)
		.build()
		
### Pages notifications

if you need to provide more info, user get it by swiping to the left, to do this you create 2 notifications objects

	// Create builder for the main notification -> 1st page
	NotificationCompat.Builder notificationBuilder =new NotificationCompat.Builder(this)
			.setSmallIcon()
			.setContentTitle("Page 1")
			.setContentText("Short message")
			.setContentIntent(viewPendingNotification)
			.build()
			
	
	//Create a big text style for the 2nd page
	BigTextStyle secondPageStyle = new NotificationCompat.BigTextStyle();
	secondPageStyle.setBigContentTitle("page2").bigText("a lot of text");
	
	//Create the 2nd page notification
	Notification secondPageNotification =new NotificationCompat.Builder(this)
			.setStyle(secondPageStyle)
			.build();
			
	//Extend the notificationBuilder with the secondPageNotification
	Notification notification =notificationBuilder
			.extend(new NotificationCompat.WearableExtender().addPage(secondPageNotification))
			.build();

	//Issue the notification
	notificationManager = NotificationManagerCompat.from(this);
	notificationManager.notify(notificationId, notification); <-this will show both pages
	
	
Note : any extra pages added will never appear on the phone.

### Stack notification

it's a serie of notification that we decideto group (=stack) together to show to the user, one on the top of the other

create a separate notification for each email

	final static String GROUP_KEY_EMAILS = "group_key_emails"

	//Build the notification, setting the group approprietly
	Notification notif1 = new NotificationCompat.Builder(this)
				.setContentTitle("New mail from"+sender1)
				.setContentText(subject)
				.setSmallIcon()
				.setGroup(GROUP_KEY_EMAILS)
				.build()

	//Issue the notification
	NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
	notificationManager.notify(notificationId1, notif1);
	
	Notification notif2 = new NotificationCompat.Builder(this)
				.setContentTitle("New mail from"+sender2)
				.setContentText(subject)
				.setSmallIcon()
				.setGroup(GROUP_KEY_EMAILS)
				.build()

	//Issue the notification
	notificationManager = NotificationManagerCompat.from(this);
	notificationManager.notify(notificationId2, notif2);
	
	
	//etc
	
	//now for the phone we dont want those multiple notification, we only want one
	
	Bitmap largeIcon = BitmapFactory.decodeResource(getResources()),R.drawable.ic_large_icon);
	
	//Create inbox style notification
	Notification summaryNotification = new NotificationCompat.Builder(this)
			.setContentTitle("2 new Messages")
			.setSmallIcon()
			.setLargeIcon(largeIcon)
			.setStyle(new NotificationCompat.InboxStyle()
					.addLine("Alex Check this out")
					.addLine("Jeff Launch Party")
					.setBigContentTitle("2 new Messages")
					.setSummaryText("johndoe@gmail.com"))
			.setGroup(GROUP_KEY_EMAILS)  <-it is also part of thegroup
			.setGroupSummary(true)  <-but this is the summary, by default the summary is shown on the phone only
			.build();
			
	notificationManager.notify(notificationId3, summaryNotification);	
	
### notification only shown on the phone and not sync to the wearable

ex: notif showing that there is an uploading progress on the phone. You set this use 

	NotificationCompat.Builder(this).setLocalOnly(true)  <-notif will appearonly on the phone
	
### documentation is here

http://developer.android.com/training/wearables/notifications/index.html
https://www.udacity.com/course/viewer#!/c-ud875-nd/l-4613198543/e-4579030555/m-4579030557
Android Studio > New > Import Sample > Wearable > Wearable notifications
Android Studio > New > Import Sample > Wearable > Eliza Chat  <-allows you to have conversation using speak recognition

## Android Wear App

	android wear devices do not connect to the internet directly they communicate with the phone using bluetooth or wifi
	android wear apk are embedded inside the regular phone apk from google play
	the user download the phone apk, then the phone apk detect a wear device and copy its wear apk to the wear device
	whenever phone apk is updated on google play, this copy process is repeated
	a wearable app cannot exist witout a phone app.
	phone apk and wear apk must have same package name and version numbers
	the permissions requested by the wearable apk must also be requested by a phone apk as well
	phone apk and wear apk must be signed by the same developper keys.
	althouth they have to be embedded for google play, it's possibible to build application separately for testing purpose
	
create a wearable app and test it

	Android Studio > New Project > Phone & Tablet & Wearable > BlankActivity > BlankWearActivity
	select mobile and click build : it will only build the mobile app --> See hello world !
	enable developper mode on wearable : settings>about> build number 7 times >	devp mode > enable usb debuuging
	install window driver for the watch : http://www.tinmith.net/wayne/blog/2015/05/android-usb-windows.htm
	if your watch doesn't have usb cable use Bluetooth : https://developer.android.com/training/wearables/apps/bt-debugging.html
	select wear and click build : it will only build the wear app --> See hello square world ! or hello round world ! depending on your device.
	
again

	Tap the clock on your watch to bring up the Google voice search command
	Keep going to see the menu entries, and get all the way down to Settings
	Tap the Settings entry, then scroll down until you see About and tap it
	Scroll down to the build number, and tap it seven times — yes, just like on a phone
	Go back to the Settings menu and you'll see a new option for Developer Options, and tap it
	In the new list of settings, enable ADB Debugging
	
push your app on google play

	build > generatesigned apk > mobile > etc
	in the mobile modude gradle you can see : wearApp project(':wear') this will embedded the wear apk into the phone apk, this only happen in realease mode
	
if you try to debug packaging installation problems, you can use adb logcat and search for process WearablePkgInstaller on phone and wearble

	adb logcat | grep WearablePkgInstaller
	
wearable don't connect to internet it communicate with the phone with

	data items
	messages
	
### data items
	
data items are

	storage of key-value pairs automatically synchronised to others devices
	those others devices register a listener and listen to change
	provide by the data API provided by google play services
	limited to 100 KBs
	garanty of delivery
	used for settings like background color
	used to store gps tracks (while on the run the wearable might not have connectivity, it should be sync later)
	used for important task the user should do
	
to use data items, first make your activity implements ... and leave methods empty for now

	implements GoogleApiClient.ConnectionCallbacks, GoogleApiClient.OnConnectionFailedListener
	
in the activity onCreate add

	//This will allow the app to make Google play services api calls
	mGoogleApiClient = new GoogleApiClient.Builder(this)
			.addApi(Wearable.API)
			.addConnectionCallbacks(this)
			.addOnConnectionFailedListener(this)
			.build();
	mGoogleApiClient.connect();
		
now to send to the phone the number of step the user has done today add this method 

	sendStepCount(5, 3467890)

now implement it

    public void sendStepCount(int steps, long timestamp){
        //create a unique path for the data item to be stored on the wearable
        PutDataMapRequest putDataMapRequest = PutDataMapRequest.create("/step-counter");

        //add value to the data item
        putDataMapRequest.getDataMap().putInt("step-count", steps);
        putDataMapRequest.getDataMap().putLong("timestamp", timestamp);

        //store the data item in an object on the wearable on the path given above
        PutDataRequest request=putDataMapRequest.asPutDataRequest();
        Wearable.DataApi.putDataItem(mGoogleApiClient, request)
                .setResultCallback(new ResultCallback<DataApi.DataItemResult>() {
                    @Override
                    public void onResult(DataApi.DataItemResult dataItemResult) {
                        if(!dataItemResult.getStatus().isSuccess())
                            Log.e("MyFirstWearableApp", "Failed to send step data item ");
                        else
                        //data item successfully stored on the wearable. If the phone is nearby
                        // it will synchronise the data item on the phone, otherwise not.
                        // here we can't be sure that the phone has received it. Data item are
                        // promised to never be lost, and will arrive when the phone is paired up.
                            Log.d("MyFirstWearableApp", "Sucessfully sent step data item ");
                    }
                });
    }
	
if you want to send an Icon to the wearable use this.

	putDataMapRequest.getDataMap().putAsset(WEATHER_TEMP_ICON_KEY, asset);
	
and convert your bitmap into an asset with the size of your choice

	Asset asset = toAsset(Bitmap.createScaledBitmap(largeIcon, 52, 52, true));
	
	private static Asset toAsset(Bitmap bitmap) {
        ByteArrayOutputStream byteStream = null;
        try {
            byteStream = new ByteArrayOutputStream();
            bitmap.compress(Bitmap.CompressFormat.PNG, 100, byteStream);
            return Asset.createFromBytes(byteStream.toByteArray());
        } finally {
            if (null != byteStream) {
                try {
                    byteStream.close();
                } catch (IOException e) {
                    // ignore
                }
            }
        }
    }
	
now how to use this on the mobile app, create a service

	File > new > Service
	
change it to and implement onDataChangeMethod

	public class MyService extends WearableListenerService {

		@Override
		public void onDataChanged(DataEventBuffer dataEvents) {
			for(DataEvent dataEvent:dataEvents){
				if(dataEvent.getType()==dataEvent.TYPE_CHANGED){
					DataMap dataMap = DataMapItem.fromDataItem(dataEvent.getDataItem()).getDataMap();
					String path=dataEvent.getDataItem().getUri().getPath();
					if(path.equals("step-counter")){
						int steps=dataMap.getInt("step-count");
						long time=dataMap.getLong("timestamp");
					}
				}
			}
		}
	}
	
update the mobile AndroidManifest

        <service
            android:name=".MyService"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="com.google.android.gms.wearable.BIND_LISTENER"/>
            </intent-filter>
        </service>
		
to send an image from the wear to the phone, use the asset class as follow, in the sendStepCount method

	Asset asset=createAssetFromBitmap(bitmap);
	putDataMapRequest.getDataMap().putAsset("profileImage", asset);
	
and implement the method as follow

    //Convert the bitmap into a png bytestream under 100KBs
    private static Asset createAssetFromBitmap(Bitmap bitmap){
        final ByteArrayOutputStream byteStream = new ByteArrayOutputStream();
        bitmap.compress(Bitmap.CompressFormat.PNG, 100, byteStream);
        return Asset.createFromBytes(byteStream.toByteArray());
    }

	
### messages

for a good example of this see 

	import sample "data layer"

messages are

	simple byte array
	no garantee of delivery : if the device is not connected or out of range, the message will be lost
	used for messages that won't be relevant many hour later. ex: send notif about a nearby restaurant, current street info
	
	
to send a message. In the wearable mainActivity onCreate (or is it in the Mobile, I'm not sure, could be in both I think)

        //send a message (not on UI thread)
        Wearable.MessageApi.sendMessage(
                mGoogleApiClient,
                nodeId,  //the node to send to, see below
                "path/message", //the local path
                new byte[0]) //bytearray should be limited 100 KB other wise you get an error (ex
                // .  byte[1] )
                .setResultCallback(
                        new ResultCallback<MessageApi.SendMessageResult>() {
                            @Override
                            public void onResult(MessageApi.SendMessageResult sendMessageResult) {
                                if (!sendMessageResult.getStatus().isSuccess())
                                    Log.e("MyFirstWearableApp", "Failed to send message ");
                            }
                        }
                );
				
to get the node id use the await method to make the call immediately and it will block until the complete list is available

	//wait for the list of all connected nodes (not on UI thread)
	NodeApi.GetConnectedNodesResult nodes =
			Wearable.NodeApi.getConnectedNodes(mGoogleApiClient).await();
			
once await return

	//traverse le list of nodes
	for(Node node : nodes.getNodes()){
		//do something with node.getId() like send a message
		nodeId=node.getId();
	}
	
to receive the message, in the phone MyService onMessageReceive

    @Override
    public void onMessageReceived(MessageEvent messageEvent) {
        if(messageEvent.getPath().equals("path/message"))
            //do something with the bytearray messageEvent.getData()
    }
	

	
### battery life

	always do the heavy work on phone not on wearable
	instead of having the wearable wake up every 10 sec to check the any update from the phone, allow the phone to update the wearable device, and when doing so always compare with the previous info downloded earlier, if there is no need to update, don't update.
	when sending data to the wearable prefer a table of int than several int or float or whatever, because each int will have more data like packets, etc..
	don't check if data items are received, because they are for sure, only do so with messages
	
### android wear UI

involve ... and is achieve with GridViewPager

	scrollling side to side
	scrollling up and down
	
it works with ... that shows where the user is located

	DotsPageIndicator
	
look at the sample

	file > import sample > gridview pager
	
box inset layout : you can design separate design for round and square watches or you can desidn everything for a square and use a box inset layout to insure that content always fit in the screen.

	down side : waste space on the edges
	nice part : it promiss that it will never makethe square leak outside the round area

box inset layout sample

	file > import sample > DelayedConfirmation

this sample needs a coorection in the wearable manifest

        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name">
        </activity>
	
and specify the default activity to launch

	MainActivity
	
as you can see it has added padding to the top, but not anywhere else, this is due to the ... attribute. Note you can't see this on android studio preview

	app:layout_box="top"
	
to make the square completely inside the round

	app:layout_box="all"
	
if you set it to none, or forget to add this line, the box inset layout will do nothing

	app:layout_box="none"
	
you might be tempted to allways design for round shape that fit inside a square, and never put anything in the corners edges. But it's poor design.

	the unused corners on the square layout might look weird
	it's a waste of space
	don't do it
	
the best way to design for round and square is by using ... and doing independent layout for both types
	
	WatchViewStub : it will inflate either the rect layout or the round layout depending on the screen shape.
	Make sure same ids are present in both files
	
BoxInsetLayout vs WatchViewStub

	News reader or messaging : BoxInsetLayout because you want the text to be completly visible on the screen
	Alarm clock : WatchViewStub because you want different layouts
	Map navigation : WatchViewStub because you want different layouts
	List of week's weather : BoxInsetLayout because you've got a long list.
	Photo of a face : WatchViewStub because you want face to consume the entiere size of the watch
	Photo of a landscape : WatchViewStub because you want face to consume the entiere size of the watch
	
By default swiping will close your app and get the user back to the default watch face. If you dont want that you can disable the swipe. Now the swipe is used for something else drawing. If the user want to close the app he has to do a long press. What does the user ?

	Open an swiping normal behvaiour desabled app
	Use the app
	Long press to dismiss to close the app
	
See samble watch view stub

	File > Sample >  watch view stub

As you can to implement this you use a DismissOverlayView. In the activity_main layout 
	
	<FrameLayout
		xmlns:android="http://schemas.android.com/apk/res/android"
		android:layout_width="match_parent"
		android:layout_height="match_parent">

		<android.support.wearable.view.WatchViewStub
			xmlns:app="http://schemas.android.com/apk/res-auto"
			android:layout_width="match_parent"
			android:layout_height="match_parent"
			android:id="@+id/stub"
			app:rectLayout="@layout/rect_layout"			<-layout for rect
			app:roundLayout="@layout/round_layout"/>		<-layout for round

		<android.support.wearable.view.DismissOverlayView	<-layout when pressed to dismiss, it's invisible by default
			android:id="@+id/dismiss_overlay"
			android:layout_width="match_parent"
			android:layout_height="match_parent" />
	</FrameLayout>
	
in the MainActivity onCreate

        //Create a reference to the dismiss view
        mDismissOverlayView = (DismissOverlayView) findViewById(R.id.dismiss_overlay);

        //Create a gesture detector thatlisten to long press
        mGestureDetector = new GestureDetectorCompat(this, new LongPressListener());
		
in the MainActivity

    private class LongPressListener extends GestureDetector.SimpleOnGestureListener {
        @Override
        public void onLongPress(MotionEvent event) {
            //Show the dismiss view
            mDismissOverlayView.show();
        }
    }

to make the gesture detector work properly, tell the mainActivity to send its event to it by overriding it's dispatchTouchEvent method

    @Override
    public boolean dispatchTouchEvent(MotionEvent event) {
        return mGestureDetector.onTouchEvent(event) || super.dispatchTouchEvent(event);
    }
	
last thing we need to do is disable the standard swipe action by overiding the theme, by creating a values/themes.xml file

	<resources>
		<style name="CustomTheme" parent="@android:style/Theme.DeviceDefault">
			<item name="android:windowSwipeToDismiss">false</item>
		</style>
	</resources>
	
and activate the theme in the manifest by replacing

    <application
            android:allowBackup="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@android:style/Theme.DeviceDefault">
			
by ... and Now you can't swipe the app away but you can dismiss it with a long press.

    <application
            android:allowBackup="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/CustomTheme">
			
### Notification on the wearable but not on the phone

it works like before but be sure to call nofification on the wearable app and not the phone. For good example you have : 

	File > New > Import Sample > synchronised notifications

in the wearable NotificationUpdateService see the method buildWearableOnlyNotification

    /**
     * Builds a simple notification on the wearable.
     */
    private void buildWearableOnlyNotification(String title, String content,
            boolean withDismissal) {
        Notification.Builder builder = new Notification.Builder(this)
                .setSmallIcon(R.drawable.ic_launcher)
                .setContentTitle(title)
                .setContentText(content);

        if (withDismissal) {
            Intent dismissIntent = new Intent(Constants.ACTION_DISMISS);
            dismissIntent.putExtra(Constants.KEY_NOTIFICATION_ID, Constants.BOTH_ID);
            PendingIntent pendingIntent = PendingIntent
                    .getService(this, 0, dismissIntent, PendingIntent.FLAG_UPDATE_CURRENT);
            builder.setDeleteIntent(pendingIntent);
        }

        ((NotificationManager) getSystemService(NOTIFICATION_SERVICE))
                .notify(Constants.WATCH_ONLY_ID, builder.build());
    }
	
### Fitness app

uses sensors to measure

	step counts
	acceleration
	position
	
phones uses the sames sensor, so you can use the same APIs. So what are the best practice for battery life saving  ?

	unregister any listener you have on the wearable when you don't need it
	we log step only when the app is running in the foreground, but screen to sleep
	select an appropriate update rate : every minute maybe
	if both the phone and the wearable has a GPS it will use the phone GPS when device are paired up, wearable GPS if they are away

To do so use the registerListener method

public boolean registerListener(
	SensorEventListener listener, 
	Sensor sensor, 
	int samplingPeriodUs, 
	int maxReportLatencyUs
);


Let's look at : 

	step counts : File > New > Import Sample > Jumping Jack
	gps example : File > New > Import Sample > Speed Tracker
	
Step count : 

 introduced in kitkat. It's a low power sensor that you can use often on the wearable.
 TYPE_STEP_DETECTOR : can wake up your device everytimethe user does a step
 TYPE_STEP_COUNTER : gives you the number of step, when you ask him
 
### App running in the foreground

by default the app is destroyed afer a short period of time. How to you do ?

	grab a wake lock and keep the display on : NOO it will drain thebattery
	use the ALWAYS_ON mode : see https://developer.android.com/training/wearables/apps/always-on.html
	
first add a manifest dependencie in the wearable

    <!--needed for bacward comptatibility with devices that don't support WAKE_LOCK (before 22 api)-->
    <uses-feature android:name="android.hardware.type.watch"/>
    <!--to support WAKE_LOCK-->    
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
	
first add a manifest dependencie in the phone

    <!--to support WAKE_LOCK-->
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
	
change wearable build.gradle file   targetSdkVersion to  22

	  targetSdkVersion 22
	  
make sure you include the wearable support correctly

    compile 'com.google.android.support:wearable:+'		<-the '+' grab the latest version, but the can specify a specific version if you want
	provided 'com.google.android.wearable:wearable:+' 	 <-this deals with dependencies issues when you do release build with proguard.
	
now to make the activity stay always on, first make the wearable Activity extends WearableActivity and add method 

	public class MainActivity extends WearableActivity {
	    super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        final WatchViewStub stub = (WatchViewStub) findViewById(R.id.watch_view_stub);
        stub.setOnLayoutInflatedListener(new WatchViewStub.OnLayoutInflatedListener() {
            @Override
            public void onLayoutInflated(WatchViewStub stub) {
                mTextView = (TextView) stub.findViewById(R.id.text);
            }
        });
        
		// We want to run in ambient mode instead of going back to the default watch face		
		setAmbientEnabled();  
	}
	
then override onEnterAmbient which is called when the app start to switch to ambient mode, use it to present a much simpler UI here with no unecessary detail

    @Override
    public void onEnterAmbient(Bundle ambientDetails) {
        super.onEnterAmbient(ambientDetails);
        //display simpler UI here with no unecessary detail
        //reduce color used
        //keep pixel number used to a minimum
        mTextView.setText("Ambient mode");
        mTextView.setTextColor(Color.WHITE);
        mTextView.setTextSize(15.0f);
    }

then override onUpdateAmbient to receive system ticks every minutes

    @Override
    public void onUpdateAmbient() {
        super.onUpdateAmbient();
        //for any update you want to do every minutes
    }
	
then override onExitAmbient called when the user touch thewatch display and we needto restore the UI to normal mode, we need to undo anything we did in onEnterAmbient

    @Override
    public void onExitAmbient() {
        super.onExitAmbient();
        mTextView.setText("interactive mode");
        mTextView.setTextColor(Color.RED);
        mTextView.setTextSize(40.0f);
    }
	
Notes : 

	to know in witch modeyou are call isAmbient()
	the palm gesture (covering thewatch with the palm of the hand, switch the watch to ambient mode) or press the side button
	sample : File > Import Sample > Always On
	
	
## Android Wear Watch Faces

A watch face

	is visible all the time without having to touch the screen
	show the time
	can show timed events like : next coming event, weather, current stock price
	
You will have to consider

	round format
	square format
	different resolutions
	idealing the design works for round and square format
	make your square and round design similar
	great design adapte to the shape of the design
	great design gives only necessary info
	
Modes, devices an display

	interactive : full color, fluid animation, background image or gradient
	ambient : the screen is only updated once every minute
		
OLED display, low bit, currently ambient
	
	color solid with <5% pixels illuminated. unblack pixels consumes power and can burn.
	does not use anti-aliasing (blur the edge of text to make it look smooth)
	use low-bit colour : black, white, blue, red, magenta, green, cyan, yellow
	don't fill area, just fill the contour
	
OLED display, low bit, currently interactive

	full color, animations are fine and recommanded

LCD display, low bit, currently ambient
	
	can show gray scale images, or black and white design used in OLED can work here
	use low-bit colour : only gray

LCD display, low bit, currently interactive

	full color, animations are fine and recommanded
	
UI elements are

	cards : shows notifications etc..
	pick cards : card partially visible over the bottom of the watch face. They can be : hidden, small, variable(=size will expand to the content). You need to design for all possibilities and the user can choose his preference.
	indicators : tells the user the status, like "charging", airplane mode, connectivity
	hot word indicator : "Ok Google" they stay on the screen for a few seconds.
	better place indicators at the top of the screen to leave space for the picks cards, if they are place at the bottom the system will charge a small pick card by default, and reduce what's shown above. Or place them at the center of the screen, if the reste of theinfo is outside like in a watch
	
When to use 

	Notifications : when you need the user attention right now. Info will be out of date after an hour. The wearable will vibrate. When stock has reach a threshold. Incoming emails.
	Regular Activity : when you need user action right now. Send a text message to a friend. History of weather at a location.
	Always on activity : when you want the app to continue to run, like with a maps, for a run step and distance count
	Watch face : for everything else that is shown therest of thetime. they are selected by the user as the default watch face. Track step/distance each day. Track calendar items
	
Create a watch face

	File > Import sample > Watch face
	run the mobile app
	run the watch app
	
On the watch select a face by pressing and holding the screen

	sample analog : is a normal clock
	sample sweep : idem sample analog but the second hand (=petite aiguille) has a smooth sweeping motion. This refresh mush frequently than 1 per second
	sample card balance : it's meant to help us visualise the dimensions of the beat card
	sample tilt : use OpenGL and show 3D rotation
	sample calendar : look at the calendar on your phone and determine how many meeting you have coming up.
	sample digital : make you select setting like the background color
	
On the phone start the android wear compnion app

	you find the same sample but some have more option like sample digital 
	
#### How to create and render a watch face?

	https://www.udacity.com/course/viewer#!/c-ud875-nd/l-4582940111/m-4585430316
	note : watch face are Service not Activities	
	first extend CanvasWatchFaceService
	define an Engine class and override Engine onCreate
	call setWatchFaceStyle in the onCreate 
	initialize ressources like setting paint styles, loading large bitmap, resizing large bitmap should be done here (and not in the main draw code)
	
Something like this

	public class MyWatchFaceService extends CanvasWatchFaceService {

		private class Engine extends CanvasWatchFaceService.Engine {
			@Override
			public void onCreate(SurfaceHolder holder) {
				setWatchFaceStyle(new WatchFaceStyle.Builder(MyWatchFaceService.this)
						//we select peekcard with variable size
						.setCardPeekMode(WatchFaceStyle.PEEK_MODE_VARIABLE)
								//we want peekcard to show only for interruptive notifications
						.setBackgroundVisibility(WatchFaceStyle.BACKGROUND_VISIBILITY_INTERRUPTIVE)
								//we disable the system UI time because our watch face is doing its own time
								// representation
						.setShowSystemUiTime(false)
						.build());

				//initialize ressources
				Resources resources = MyWatchFaceService.this.getResources();
				mYOffset = resources.getDimension(R.dimen.digital_y_offset);
				mLineHeight = resources.getDimension(R.dimen.digital_line_height);
				mAmString = resources.getString(R.string.digital_am);
				mPmString = resources.getString(R.string.digital_pm);
				mBackgroundPaint = new Paint();
				mBackgroundPaint.setColor(mInteractiveBackgroundColor);
				Paint paint = new Paint();
				paint.setColor(resources.getColor(R.color.digital_date));
				paint.setTypeface(typeface);
				paint.setAntiAlias(true);
				mDatePaint = paint;
				mCalendar = Calendar.getInstance();
				mDate = new Date();
				mDayOfWeekFormat = new SimpleDateFormat("EEEE", Locale.getDefault());
				mDayOfWeekFormat.setCalendar(mCalendar);
				mDateFormat = DateFormat.getDateFormat(MyWatchFaceService.this);
				mDateFormat.setCalendar(mCalendar);
			}
		}
	}
	
Overide the onTimeTickof the Engine class. This method is called in ambient mode one every minutes.

        @Override
        public void onTimeTick() {
            super.onTimeTick();
            if (Log.isLoggable(TAG, Log.DEBUG)) {
                Log.d(TAG, "onTimeTick: ambient = " + isInAmbientMode());
            }
			//Always call this if you are doing an update in this onTimeTick method. This will force a call to the Engine onDraw method
            invalidate();
        }
		
The onDraw method

	should run quickly because it will be called a lot
	never init ressource here, do it in the onCreate
	
first set the calendar object to the current system time

    long now = System.currentTimeMillis();
	
fill a rectangle with solid colors and use the bound object to provide dimentions.

	// Draw the background.
	canvas.drawRect(0, 0, bounds.width(), bounds.height(), mBackgroundPaint);
	
Always use the Rect bound object to ... and it will work properly on any device

	calculate width
	calculate height
	center the display
	
Canvas object have many methods for drawing

	drawRect : draw rectangle
	drawText : draw text
	
You can control the draw with a Paint object given as an argument. Note the paint object must be initialize in the onCreate

	canvas.drawText(hourString, x, mYOffset, mHourPaint);
	
Now override onPropertiesChanged method and secify what to do when the device enter a more specific mode or state like 

	PROPERTY_BURN_IN_PROTECTION  		<-the display has burning issue, in this case you can for ex decidenot to use bold font
	PROPERTY_LOW_BIT_AMBIENT			<-the display can only render simple colors when in low power mode
	
Now override onAmbientModeChanged(), this method is called whenever a change is made between interactive and ambient mode. This is where you change the colors.

	paint.setColor(isInAmbientMode() ? ambientColor : interactiveColor);
	
if we are in low bit mode we can set the anti alias

	if (mLowBitAmbient)
		mDatePaint.setAntiAlias(antiAlias);
		
last thing to do in onAmbientModeChanged : 

	invalidate();
	updateTimer();

Still in Engine create an updateTimeHandler

	final Handler mUpdateTimeHandler = new Handler() {
		@Override
		public void handleMessage(Message message) {
			switch (message.what) {
				case MSG_UPDATE_TIME:
					if (Log.isLoggable(TAG, Log.VERBOSE)) {
						Log.v(TAG, "updating time");
					}
					invalidate();
					if (shouldTimerBeRunning()) {
						long timeMs = System.currentTimeMillis();
						long delayMs =
								mInteractiveUpdateRateMs (timeMs % mInteractiveUpdateRateMs); //update every 0.5 sec
						mUpdateTimeHandler.sendEmptyMessageDelayed(MSG_UPDATE_TIME, delayMs);
					}
					break;
			}
		}
	};
	
This example is taken from 

	Sample > watch face > DigitalWatchFaceService
	
Note the support for timezone. The watch detect timezone change when the user travel. It will be propagate to the phone

        /**
         * Handles time zone and locale changes.
         */
        final BroadcastReceiver mReceiver = new BroadcastReceiver() {
            @Override
            public void onReceive(Context context, Intent intent) {
                mCalendar.setTimeZone(TimeZone.getDefault());
                initFormats();
                invalidate();
            }
        };
		

		
#### How to configure a watch face?

create a standard wear activity. Note this activity will start when the user will press the setting icon

	public class DigitalWatchFaceWearableConfigActivity extends Activity{}

implement a listview and give a list of colors options

	public class DigitalWatchFaceWearableConfigActivity extends Activity implements WearableListView.ClickListener {}
	
in the onClickHandler update any registered listener ... a phone Activity

    updateConfigDataItem(colorItemViewHolder.mColorItem.getColor());
	
open the phone activity DigitalWatchFaceCompanionConfigActivity

	this activity can implements many more options because the size of the display is bigger
	
### We have Services, ConfigActivities now we need to tell the manifest

In the wearable and the phone

    <!-Required to act as a custom watch face. -->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="com.google.android.permission.PROVIDE_BACKGROUND" />
	
Each watch face must have a unique service entry

        <service
            android:name=".DigitalWatchFaceService"
            android:label="@string/digital_name"
            android:permission="android.permission.BIND_WALLPAPER" > //we'll have a wallpaper
            <meta-data
                android:name="android.service.wallpaper"
                android:resource="@xml/watch_face" />
            <meta-data
                android:name="com.google.android.wearable.watchface.preview"
                android:resource="@drawable/preview_digital" />  //for preview when user select what he wants
            <meta-data
                android:name="com.google.android.wearable.watchface.preview_circular"
                android:resource="@drawable/preview_digital_circular" /> //for preview when user select what he wants, if you don't provide one it will usethe square
            <meta-data
                android:name="com.google.android.wearable.watchface.companionConfigurationAction" //means we provide an activity on the phone to configure thewatch face, this enable thegear (setting)icone 
                android:value="com.example.android.wearable.watchface.CONFIG_DIGITAL" />
            <meta-data
                android:name="com.google.android.wearable.watchface.wearableConfigurationAction" //means we provide an activity on the wear to configure thewatch face, this enable thegear (setting)icone 
                android:value="com.example.android.wearable.watchface.CONFIG_DIGITAL" />

            <intent-filter>
                <action android:name="android.service.wallpaper.WallpaperService" />

                <category android:name="com.google.android.wearable.watchface.category.WATCH_FACE" />
            </intent-filter>
        </service>
	
	
## Android Living room

	chrome cast = cast device = small usb dongle (memory stick) that plugs into the HDMI port on the TV. Allow to streamer les vidéos de son tel sur la télé, streamer la musique de son tel sur ses enceintes
	google cast = simple sender receiver typology with allows developper to create multi devices experiences (include chromecast )
	android tv = allow to see android app on a TV without the need of a phone nearby
	
How to make your app visible on tthe tv

	1. add a google cast functionality
	2. extend your app with the lean back library : this will allow the user to launch and control the app from the android tv. Create BrowseFragment, DetailsFragment, SearchFragment
	3. declare the activity intented to run on the TV in the manifest
	4. add the Leanback launcher intent-filter and your app will show up in the home screen
	5. To have it show up in thegame menu, add isGame="true"
	6. To make it appear in the Recommendation see below
	7. To make it appear in the Search see below
	
How does google cast work ?

	sender : it's your app, that always look for a cast device nearby. If it find one, it show the user a cast icon (rectangle with waves) 
	receiver : could be chromecast, androidTV, audio speaker from LG and sony, any devices that supports cast protocol. They are small html5 applications that run on the cast device.
	
When sender and receiver are connected

	the cast icon change color
	the sender (ex. your phone) becomes a remote control

when we click on the sender video

	the sender send an applicationId to the cast device
	the cast device uses the applicationId to ask google service which url it correspond to
	the cast device load the receiver app (with the video embedded) from this url
	the receiver load the app with the video embeded
	then the receiver load the video from the cloud
	
the sender work as a remote control and you can

	adjust the volume
	start playing new media
	send custom messages like : thumb up or thumb down button
	
receiver applications running on a cast device are just web applications, they are written in ... Note: google provide samples for that, and they can even be use for production.

	html
	css
	javascript
	
the cast device run a special version of chrome
	
	a chrome with one single tab
	optimized for video playback
	
Sample receiver apps provided by google

	can even be use for production
	ex : Style Media Receiver
	
Sample sender apps provided by google

	https://developers.google.com/cast/docs/downloads
	see : "hello cast", "cast videos"
	
Google provide also a design checklist that is requiered if you want you app to appear at chromecast.com/apps

	https://developers.google.com/cast/docs/design_checklist
	The Design Cast Companion Library (for Android) provide a lot of cool features following the design checklist
		
show a one cast introduction screen
	
	will appear only once
	will notify the user of what he can do in case he's not aware of it.
	to implement it use this very good third party : https://github.com/googlecast/CastVideos-android
	
other design basic

	the user should always be able to control the cast device. ex:if a video is played on the tv, a play/stop button should available on the phone.
	also show play/back control when the phone is locked
	also show play/back control in a notification, when your app is out of focus (not on the foreground).
	or use a notification service (see cast compagnion library) to show the  play/back control in a notification, when your app is out of focus (not on the foreground) and even when your app is killed by the phone. 
	make sure the cast menu allow the user to disconnect from the cast device.
	if multiple users are connected only stop the cast device when the last user disconnect.
	reconnect users if the connection drops (or if your app is killed and user restart it, without stopping the cast) --> see Cast Companion Library
	the receiver UI (TV) should never appear touchable (it just reflect a state), never reuse an existing phone or tablet ui
	
connection drops happen when

	wifi goes out of range
	user battery is dead
	
user can connect to the cast in 2 ways : 

	connect and play
	play and connect : whenever the cast is done, what they play in their phone should automatically be cast to the tv
	
	
#### There are 3 types of receiver applications

	Default Media Receiver
	Style Media Receiver : requiere an applicationId
	Custom Receiver : requiere an applicationId
	
how to get an applicationId

	go to cast.google.com/publish
	register as a cast developper
	pay 5$
	register your receiver apps
	register your cast devices (you need to do so if you want to use them for debbuging)
	
Default Media Receiver

	play wide variety of simple media types
	no registration requiered
	uses default app id : 
		Android : CastMediaControlIntent.DEFAULT_MEDIA_RECEIVER_APPLICATION_ID
		Chrome : chrome.cast.media.DEFAULT_MEDIA_RECEIVER_APP_ID
		iOS : kGCKMediaDefaultReceiverApplicationID
	no styling or customisation possible
	no way to modify receivers behavior
	
Style Media Receiver

	design for streaming audio and video content
	work with all the same types supported by the default media receiver
	you can custom it by suppling a CSS file during registration in the developper console. Add your colors and branding
	best option if your app doesn't use advance capabilities like DRM
	you can customize the loading screen as well
	
	
exemple of Style Media Receiver CSS

	.background
		background:center no-repeat url(background.png);
		
	.logo
		background-image : url(logo.png);
		
	.progressBar
		background-color : rgb(238, 255, 65);
		
	.splash
		background-image : url(splash.png);
		
	.watermark
		background-image : url(watermark.png);
		background-size : 57px 57px;
		

Custom Receiver

	gives you full control of all aspects of your application
	best choice for playing DRM content with dynamic licences
	best choice if you need authentification
	best choice when building a data centric app like a game
	see "Hello Cast Text" sample on android studio : it's a very simple app (good to understand, but not to follow if building for commercialisation).One file sender app + very simple receiver
	see "Cast Video" sample (if building for commercialisation)
	
Chrome Debugging Tools (good to debug receivers)

	1. Register your app and cast device on the Cast Developper Console
	2. Start your sender app and cast to the cast device, so it's load the receiver
	3. Make sure the browser is running on a computer on the same network as the receiver device
	4. In Chrome, visit the IP address of the cast device on port 9222 : http://RECEIVER-IP-ADDRESS:9222
	
	
Hello Cast Text

	is available here : developpers.google.com/cast/docs/downloads
	it show illustrate the Sender lifecycle
		1. launch the sender
		2. init cast API
		3. discover devices
		4. connect to device
		5. launch receiver
		6. send / receive messages
		7. disconnect


	receiver.html : it is the receiver app
		it access the google cast api using <script type="tex/javascrit" src="//www.gstatic.com/cast/sdk/libs/receiver/2.0.0/cast_receiver">
		then you can get an instance of the cast receiver manager : window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance();
		then you can use : castReceiverManager.onSenderConnected and castReceiverManager.onSenderDisconnected
	AndroidManifest : 
		min sdk that support cast is 9
			<uses-sdk android:minSdkVersion=9 .../>
		application theme should correctly set based on the andrid sdk version
	MainActivity.java = the one file sender app
		init cast API in the onCreate: mMediaRouter=MediaRouter.getInstance(getApllicationContext());
		discover devices or filter the cast devices to get only those which can run our app (ex : if you are looking for video cast and stero cast is available you won't show the stereo to the user) : mMediaRouteSelector=new MediaRouteSelector.Builder().addControlCategory(CastMediaControlIntent.categoryForCast("794B7BBF")).build(); mMediaRouterCallBack=new MediaRouterCallBack(); //794B7BBF=applicationID
		add the cast button : extends ActionBarActivity and add a menu.xml with one item
		in onCreateOptionMenu : MediaRouteActionProvider mediaRouteActionProvider=(MediaRouteActionProvider)MenuItemCompat.getActionProvider(...)
		to trigger the discovery cast devices add in onStart(): mMediaRouter.addCallBack()...
		to conserve battery power we remove the callback when our activity is stopped
		get the cast device selected by the user in the onRouteSelected
		to launch the receiver : 
			get an instance of the GoogleApi client in launchReceiver(): mApiClient=new GoogleApiClient.Builder
			in the ConnectionCallbacks onConnected if connection is successfull we can launch the receiver app : Cast.CastApi.launchApplication(...)
			also note the setResultCallBack() in Cast.CastApi.launchApplication(...).setResultCallBack(), this is an imprtant task that can be simplified when we the the CastCompanionLibrary
		to send messages to the receiver, we do it throw a channel class HelloWorldChannel implements MessageReceivedCallback
			each custom channel is defined by a unique namespace
		now you can send messages using the sendMeassage() methode. Note if you have complex messages simply encode them in json and decode them on the receiver side
		to disconnect from the cast see the tearDown method
		
	menu.xml
		<item 
			android:id="@+id/media_route_item"
			android:title="Play on..."
			app:actionProviderClass="android.support.v7.app.MediaRouteActionProvider"
			app:showAsAction="always"/>	
		

Google Cast Companion Library (CCL) provides features and behaviors recommanded by Google guidelines and include : 
	
	easy device discovery
	custom notifications
	custom cast menu
	lock screen remote control
	player control activity
	mini controller : small controller that can be added to the layout.xml of thedefferents activities, it allow the user to browse throw the phone app while still being able to control the cast
	reconnection logic
	checks google plays services for compatibility
	media tracks
	data channel wrappers
	https://github.com/googlecast/CastCompanionLibrary-android
	https://github.com/googlecast/CastCompanionLibrary-android/blob/master/CastCompanionLibrary.pdf
	
to init a CCL: in the MainActivity onCreate

	APPLICATION_ID=getString(R.string.app_id); //app id of the receiver
	
	VideoCastManager
		.initialize(this, APPLICATION_ID, null, null)
		.setVolumStep(VOLUME_INCREMENT)
		.enableFeatures(
			VideoCastManager.FEATURE_NOTIFICATION | // enable custom notifications
			VideoCastManager.FEATURE_LOCKSCREEN |
			VideoCastManager.FEATURE_WIFI_RECONNECT | //showld also be indicated in the manifest <service android:name="com.google.android.libraries.cast.companionlibrary.cast.reconnection.ReconnectionService"/>
			VideoCastManager.FEATURE_CAPTIONS_PREFERENCE |
			VideoCastManager.FEATURE_DEBUGGING		
		);
		
	//Now we can use the CCL
	BaseCastManager.checkGooglePlayServices(this); //check if google play isinstall and show the user adialog to do so if not.
	mCastMgr=VideoCastManager.getInstance();
	
	//if you want control to play, pause etc add this line
	mCastMgr.startVideoCastControllerActivity(this, mSelectedMedia, position, autoPlay);
	note : mSelectedMedia is a MediaInfo  This is defined in the Cast SDK, and contains meta data like the title and studio, and also the URL pointing to the media (which you should place in contentId). See : https://developers.google.com/android/reference/com/google/android/gms/cast/MediaInfo
	
	//now your channel is created and you can easily send messages
	VideoCastManager.sendDataMessage(String message);
	
	//what to do when the message is received
	VideoCastManager.onDataMessageReceived(String message);
	
	//what to do when there was an error
	VideoCastManager.onDataMessageSendFailed(int errorCode);

	//if you use the miniController add
	mMini=(MiniController) findbyid(...);
	mCastMgr.addMiniController(mMini);//remember to unregister it in onDestroy
	
	
	// if you use FEATURE_WIFI_RECONNECT
	mCastMgr.reconnectSessionIfPossible(20);
		
		
for a data centric app

	use a DataCastManager intead of VideoCastManager
	
to inform the CCL if your app is active or not

	in the onStart
		mCastMgr.incrementUiCounter();
		
	in the onStop
		mCastMgr.decrementUiCounter();	
		
#### Add cast support to the universal media player. 

I've not followed this lesson.
see : https://www.udacity.com/course/viewer#!/c-ud875-nd/l-4582940113/e-4627728761/m-4627728762


### How to build an android TV app

Where will appear your app ?

	in the app bar
	or better in the recommandation bar

Declare a TvActivity in a manifest
	
	<activity
		android:name=".TvActivity">
		<intent-filter>
			<action android:name="android.intent.action.MAIN" />
			<category android:name="android.intent.category.LEANBACK_LAUNCHER"/>
		</intent-filter>
	</activity>

	
I have not followed this class so please refers to

	https://www.udacity.com/course/viewer#!/c-ud875-nd/l-4608539075/e-4628348551/m-4628348552

### Games : have not followed this class neither


### Android auto

USA people

	spend 1 hour/day in a car
	check his smartphone 125 times/day
	
To use android auto a user must

	go to google play and download your app (that have android auto support) on their phone
	connect his phone to the car
	
and then

	the phone will go in car mode (display a screen written "car mode")
	the phone will cast the app to the car screen
	you interact with it using vehicule controls + touch screen, microphone
	
major use of android auto

	music
	radio
	audiobook players
	messages : receive notification, reply with speech
	
android auto messaging (I've just followed the introduction)

	1. show a notification on screen "new msg from paul"
	2. user click on the notif
	3. women voice read the message. "Areyou coming ?"
	4. user touch vehicule voice control and say "reply"
	5. woman says : "what's the message"
	6. user says "yes in 5 min"
	7. woman says "I have message yes in 5 min do you want to send it"
	8. user says "yes"
	9. woman says "sending message"
	
android auto media (I've just followed the introduction)

	you can use the touch screen to select a song based on a variety of criterias
	you can touch vehicule voice control and speak the name of a song or artist or category "play music jazz"

#### Others notes
Use a Service.
It's meant for long-running tasks and is not tied to your Activity lifecycle.
It would be especially helpful for the user if you'd also associate a notification with the download, showing the progress (as 2GB can take a huge amount of time to fetch, especially on a mobile connection. Speaking of that please don't fetch 2GB of data on a mobile connection without making it really clear to the user that you're going to do that or enabling them to opt-out of this or do it only when connected over WiFi. Data-limited users will thank you ;)
	








# Google Play Services Location and Context

## Google Play Services udacity github repo

https://github.com/udacity/google-play-services

## Google Play Services List

maps
ads -> to monetize
drive -> to store files
analytics
sign in
fit
plus
wallet

## Google Play Services that needs credentials

sign in


## Location services

in the gradle add 

	compile 'com.google.android.gms:play-services:7+'
	
in the manifest.xml

	<meta-data android:name="com.google.gms.version" android:value="@integer/google_play_service_version/>  <-like this the gradle will put the correct value himself
	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
	
Now you will use an asynchronous model

	in the onCreate : new GoogleApiClient
	in the onStart : connect the GoogleApiClient to the google service api you want (in this case LocationServices) by making your activity  implementing its google service api generals methods. implements GoogleApiClient.ConnectionCallbacks, GoogleApiClient.ConnectionFailedListener
		onConnectionFailed : try to reconnect
		onConnectionSuspended : connection is not broken, and maybe you want to cache some infos
		onConnected method : when you succeed. LocationServices is connected. Your activity can now send a LocationRequest to the LocationServices by making your activity  implementing the google service api LocationServices specofique method. implements LocationListener
		onLocationChanged : that gives you the Location object (latitude, longitude, acceleration, bearing)
		
Then you need to enable access the google api service in the developpers console

	https://console.cloud.google.com/
	in Overview>GoogleAPi>choose the one you want and follow what is asked. If you did correctly
	you can now find it in EnableApi
	
Then you need to set credentials for google api service in the developpers console (note : not all google api services needs credentials)

	https://console.cloud.google.com/
	in Credentials>generate an API key for your app
	
Fused location provider

	analysis your gps, cellular connection, wifi
	
and based on the movement of you your phone, it can do

	activity recognition : driving, cycling, walking, standing, tilting
	
location densities

	fine location
	coarse location
	
fine location  

	uses analysis your gps or cellular connection, wifi
	is very accurate
	but uses battery
	gives you theexact spot
	
coarse location

	uses only cellular connection or wifi
	less acurate
	better for battery
	it is enough to know where you are, at the theater, in a sport event,etc but you won't knowtheexact spot (latitude and longitude)
	
you do this in the manifest

	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
	
or

	<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
	
in the onCreate

	mGoogleApiClient = new GoogleApiClient.Builder(this) <-We create an instance
			.addApi(LocationSevices.API)  <-we want to use a location service API
			.addConnectionCallbacks(this) <-we want the callbacks to come to this class (that's why we need the class to implements ConnectionCallbacks)
			.addOnConnectionFailedListener(this) <-we want the callbacks to come to this class (that's why we need the class to implements ConnectionFailedListener)
			.build();
			
in the onStart

	mGoogleApiClient.connect();
	
	
in the onConnected

	mLocationRequest = LocationRequest.create();
	mLocationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURANCY)
	mLocationRequest.setInterval(1000);//update location every seconds
	LocationServices.FusedLocationApi.requestLocationUpdates(mGoogleApiClient, mLocationRequest, this); //this will trigger the onLocationChange

priorities
	
	LocationRequest.PRIORITY_BALANCED_POWER_ACCURANCY : gives accurancy about 100 meters, is battery friendly
	LocationRequest.PRIORITY_HIGH_ACCURANCY : finest possible location based on phone hardware, battery unfriendly
	LocationRequest.PRIORITY_LOW_POWER : gives city level location, accurancy 10km, very battery friendly
	LocationRequest.PRIORITY_NO_POWER : best possible accurancy at no power cost, if other clients in the app have gotten the location, it will listen to them
	
note on pririties

	the	<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>of the manisefest override the priorities
	priorities end up having no effects
	
	
in the onStop

	mGoogleApiClient.disconnect();
	
	
more infos : 

	https://developer.android.com/training/location/receive-location-updates.html
	
## Google Play Services udacity github repo

	https://github.com/udacity/google-play-services	

LocationLesson1 : 
	
	display the latitude in a Textview
	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\LocationLessons_Final\LocationLesson1
	continuous update (every second) good for cycling apps, walk dogs apps
	
LocationLesson2 : 
	
	display the latitude in a Textview
	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\LocationLessons_Final\LocationLesson2_1
	location is find only once, no implementation of LocationListener
	
	
trick to find the sdk path : 

	open the sdk manager, the path is written at the top
	
	
activityrecognition : 
	
	show the activity of the user with a percentage of certainty, because hecan't be 100% sure
	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\LocationLessons_Final\activityrecognition
	<uses-permission android:name="android.permission.ACTIVITY_RECOGNITION"/>
	use an IntentService
	
geofencing : ability to draw virtual fence around a location in a real world and generate events when the device enter this location. Basically it is : 

	lattitude and longitude
	radius around this location
	time (hours) for which it is active (good for promotions in your store or your future canteen)
	
	
## Geofencing

you need a

	GoogleApiClient create as before
	
and a GeoFence created using a Builder and needs

	latitude
	longitude
	radius
	expiration : once the time expire the geofence is deleted. You can set up permanent time if you like.
	
you usually define several geofence as an

	ArrayList arrayOfGeoFence
	mGeoFencingRequest.addGeoFences(arrayOfGeoFence)
	

Geofencing LocationLesson3_1 : 
	
	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\LocationLessons_Final\LocationLesson3_1
	use an IntentService (the activity give an intent to the intentservice, if the service has not already been start by another intent it will start, otherwise it will queuethe intent)
	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454013/modules/8011345401375460/lessons/3976758718/concepts/42741786720923
	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
	
	
To get the latitude and longitude

	go to google map and look at the url or
	go to google map, pin and look at the popup that show up
	
	
# Google Analytics

	https://github.com/udacity/Analytics_and_Tag_Manager/
	
	how to add code to track usage data in google analytics
	the data send to analytics when using the app take a while to appear on analytics dashboard, if you prefer you can see the same info in android studio verbose logs
	to do so you need to get a GoogleAnalytics instance in your code
	
first create an application as follow

	public class MyApplication extends Application {
		public Tracker mTracker;

		public ContainerHolder mContainerHolder;
		public TagManager mTagManager;

		// Get the Tag Manager
		public TagManager getTagManager () {
			if (mTagManager == null) {
				// create the TagManager, save it in mTagManager
				mTagManager = TagManager.getInstance(this);
			}
			return mTagManager;
		}


		// Set the ContainerHolder
		public void setContainerHolder (ContainerHolder containerHolder) {
				mContainerHolder = containerHolder;
		}

		// Get the ContainerHolder
		public ContainerHolder getContainerHolder() {
			return mContainerHolder;
		}


			// Get the tracker associated with this app
		public void startTracking() {

			// Initialize an Analytics tracker using a Google Analytics property ID.

			// Does the Tracker already exist?
			// If not, create it

			if (mTracker == null) {
				GoogleAnalytics ga = GoogleAnalytics.getInstance(this);

				// Get the config data for the tracker
				mTracker = ga.newTracker(R.xml.track_app);

				// Enable tracking of activities
				ga.enableAutoActivityReports(this);

				// Set the log level to verbose.
				ga.getLogger().setLogLevel(Logger.LogLevel.VERBOSE);
			}
		}


		public Tracker getTracker() {
			// Make sure the tracker exists
			startTracking();

			// Then return the tracker
			return mTracker;
		}

	}

	
then select

	verbose
	no filter
	search :Sendding hit
	
then use the app and you should see the logging

	Sending hit to service   PATH: https:  PARAMS: sr=720x1280,  a=8749224,  v=1,  ht=1464293298434,  an=What's for Dinner 4?,  cd=Show recipe screen,  ul=fr-fr,  t=screenview,  _u=.nKK-AL,  tid=UA-XXXXXXXX-1,  cid=f255716a-7aa5-4f3a-b528-cfc693cd3565,  aid=com.example.android.dinnerapp,  av=1.0,
	an= aplication name: in this case "What's for Dinner 4?"
	cd= screen name = content description
	ul= language
	t= hit type, in this case a screenview
	tid= analytic account id it's taken from the config files
	aid= package name
	
to check the cummulative data in the analytics dashboard. Note you can change the range. If you are testing, making this range include today.

	analytics.google.com>login>AppOverview
	
to see what's happening at real time

	analytics.google.com>login>RealTime>Overview
	what you see in real time is not necessary added to the cumulated data,it's the case if there isvery low usage of the app. Sometimes you need to wait 20min or more.
	some part of google analytics may update before others.
	
what is a session ?

	it's a period of continuous use of your app
	if the user stop using your app for less than 30 min and goes back, it is considered to be part of the same session.
	
## how to send data to google analytics

in the manifest 

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	
in xml/track_app.xml

    <!-For Google Analytics -->
    <string name="ga_trackingId">UA-78373883-1</string>
	<bool name="ga_autoActivityTracking">true</bool>
	
in main activity on create

	// Make sure that Analytics tracking has started
    (MyApplication) getApplication()).startTracking();
	
user engagement indicate	
	
	how long the session lasted
	how many screens they visited per session
	
the data send to analytic with autotracking is : 

	screens/Activities
	geo informations / languages / locations
	device info : brand model / os
	network info
	
what is not sent

	events = buttons cliked, user pass a new level (in a game), set preferences
	goals = click "buy now button", click "ads", reach page3, upVote app, vote app, click the donate button, stay engage with the app a certain amount of time
	
Analytics is well design and can't damage user battery

	all android devices have an analytic service, that is shared by all apps
	the ServiceAnalytic collecte all apps tracks and send them every 2 minutes

With analytics we should always keep in mind that what we want is 

	to see if the user is reaching our goal (for example if user spend money)
	we always track goals
	
With analytics we can also

	send custom timing : how long it takes for things to happen in your app
	track crashes or exceptions
	track how user download your app
	
	
## Beyond autotracking

When we start using analytics, autotracking is fine, but if we start having a lot of people using the app, it can create a noise or even you can reach the quota limits.
If your app exceeds the quota, exces hits won't be counted.

It's better to track what you want rather than enabling autotracking.

To disable autotracking for all activities

	<bool name="ga_autoActivityTracking">false</bool>

Now you to track when the user is going to an activity, you can send a screen view in the onStart method. 

public void onStart(){
	super.onStart();
	
	//Get tracker
	Tracker tracker=((MyApplication)getApplication()).getTracker();
	
	//Set screen name
	tracker.setScreenName("A screen name");
	
	//Send a screen view
	tracker.send(new HitBuilders.ScreenViewBuilder().build());
}
	
Send a hit as above will always also gives you

	localisation info
	device info
	engagement details
	
	
In the Ecommerce/Product Performance

	you can see which product get purchase
	you can see the step throughout the purchase (if you added a hit on each step)
	
	
In behavior/app speed

	you can see the info about timing (how long it takes for things to happen in your app)
	you can only see that if you sent 2 hits (one for starting the clock, and the other for stoping)
	
## Send an event hit

Add this whereever useful

        Tracker tracker = ((MyApplication) getApplication()).getTracker();

        tracker.send(new HitBuilders.EventBuilder()
                .setCategory("Shopping steps")
                .setAction("View Order Dinner screen")
                .setLabel(dinner)
                .build());


check dashboard : 

	behavior>events>overview
	
## Set goals

in the dashboard

	Admin>Goals>new goal>Custom goal>
	
now specify : 

	name	ex: 5screens goal
	
and type of goal

	destination = screen you want to reach (the screen name you put in your tracker code, should the same as the one you mention here)
	duration = how long you want your user to stay engaged with your app
	page/session = how many pages you want him to visit in a session
	event = exple a button clicked
	
then it ask you more details. Note for destination, there is a "funnel option"

	enable you will be able to give the ordered list of screen that you want user to take before reaching yours
	
when the goal type is event

	you can specify category, action, label, and value
	
if autoActivityTracking is enable

	no code needed for screen related goals
	
if autoActivityTracking is disable 

	code needed
	
after you create a goal

	you can't delete it. Don't look for the delete button. There is none.
	but you can edit it and change it completely
	
	
dashboard 

	Conversion>Goals>Overview
	
## Track ecommerce

in the Admin tab of Analytics dashboard

	Admin>Ecommerce Settings>Enable Ecommerce>Next Step> Enable Enhanced Ecommerce>Submit
	
Now you add code to track how users 

	view products
	add products to the cart
	checkout
	purchase
	
You use 2 classes

	Product defines a product
	ProductAction defines what the user is doing with the product
	
Now you create a Product when you will need one

        Product product = new Product()
                .setName("dinner")
                .setPrice(5)
                .setVariant(dinner)
                .setId(dinnerId)
                .setQuantity(1);
	
        ProductAction productAction =
                new ProductAction(ProductAction.ACTION_ADD);
				
Then you can send to analytics.

        tracker.send(new HitBuilders.EventBuilder()
                .setCategory("Add to cart")
                .setAction("View Order Dinner screen")
                .setLabel(dinner)
                .addProduct(product)
                .setProductAction(productAction)
                .build());

The different productActions are : 

	String	ACTION_ADD	Action to use when a product is added to the cart.
	String	ACTION_CHECKOUT	Action to use for hits with checkout data.
	String	ACTION_CLICK	Action to use when the user clicks on a set of products.
	String	ACTION_DETAIL	Action to use when the user views detailed descriptions of products. Any time they view the product
	String	ACTION_REMOVE	Action to use when a product is removed from the cart.
	
Now in the dashboard

	Conversions>Ecommerce>Product Performance
	Conversions>Ecommerce>Shopping Analysis>Shopping Behavior
		SKU = Stock Keeping Unit = productId
		if you want to see the labels : select SecondaryDimension>Ecommerce>ProductVariant on the dropdown menu above SKU.
	Conversions>Ecommerce>Sell Performance
		here you can see all the products included in a unique transaction
	
For transactions actions are ... and you need to add a unique transactionId (oneway to do so is to concatenate the current time to the productId)
 
	String	ACTION_PURCHASE	Action that is used to report all the transaction data to GA.
	String	ACTION_REFUND	Action to use while reporting refunded transactions to GA.
	
This should look as follow

        Product product = new Product()
                .setName("dinner")
                .setPrice(5)
                .setVariant(thisDinner)
                .setId(thisDinnerId)
                .setQuantity(1);

        // Get a unique transaction ID
        String tID = Utility.getUniqueTransactionId(thisDinnerId);
        ProductAction productAction =
                new ProductAction(ProductAction.ACTION_PURCHASE)
                        .setTransactionId(tID);

        Tracker tracker = ((MyApplication) getApplication()).getTracker();

        tracker.send(new HitBuilders.EventBuilder()
                .setCategory("Shopping steps")
                .setAction("Purchase")
                .setLabel(thisDinner)
                .addProduct(product)
				[.addProduct(product1)
				.addProduct(product2)]
                .setProductAction(productAction)
                .build());
				
Note about refund

	it's just a report you make to analytics
	after six month from the transaction analystics can integrate the refund. (it doesn't meansthat you can't refund the customer)
	
About the checkout. It's complex

	get shipping address
	get payment address
	getpayment details
	confirm details
	review order
	
If you want to include checkout steps in your analytics, you need to 

	update your code with a step number
	add funnel sections in the admin console (it is optionnal, but if not set it will be step1, step2, step3...) Admin>EcommerceSettings>Add funnel steps
	
Now in you code

        ProductAction productAction =
                new ProductAction(ProductAction.ACTION_CHECKOUT_OPTION)
                        .setCheckoutStep(2); <-if step 2 is not set in thedashboard, I won't see it
						
## Reccord timing info

Can answer questions like, how long the dinner like take to show up

Usually to take a timestamp before, and a timestamp after and send the ellapsed time to analytics.

	aTimeStampBefore=System.nanotime() //reccord time in nanoseconds
	
then 

	tracker.send(new HitBuilders.TimingBuilder()
			.setCategory("Shopping steps")
			.setValue(aTimeStamp)
			.setLabel(thisDinner)
			.setVariable("duration")
			.build());
			
then 

	Dashboard>Behavior>AppSpeed
	you see the name of the screen andthe time
	
	
## Most of the download come from  which store ?

	Dashboard>Acquisition>New Users : you can see their location
	Dashboard>Acquisition>AppMarketplace : From which website they arrived to your place
		com.android.vending = google play store
	Dashboard>Acquisition>GooglePlayReferralReport : show the website that linked to google play, the number of view and the number of install in fine
	
To see those infos

	your app must be on Google play or iTunes
	you need to link your GoogleAnalytics account to Google Play
	
To do so

	Dashboard>Acquisition>Sources>GooglePlay>Setup app linking> Enter relevant data> turn on Get Google Play Developper Console Data > Save
	
No need to add code

	downloads will be tracked
	

## Crashes and exceptions

Go to 

	Dashboard>Behavior>Crashes and Exceptions.
	
Track a caught exception. Add this in the catch

	tracker.send(new HitBuilders.ExceptionBuilder()
			.setDescription(description)
			.setFatal(boolean)
			.build());
	
For uncaught exception: enable automatic tracking in xml/track_app

    <bool name="ga_reportUncaughtExceptions">true</bool>
	there is sometimes issues with that see : https://code.google.com/p/analytics-issues/issues/detail?id=443
	
### More ?

	If the data in analytics is not what you want, 
	you can add custom metadata in the dashboard, 
	configure custom metrics or dimensions, 
	attach them to the custom data, 
	and send your hit.
	see : https://developers.google.com/analytics/devguides/collection/android/v4/customdimsmets#overview
	
## Tag manager

	send dynamic configuration to your app
	receive hit data from your app and send it to GoogleAnalytics
	
Create an account and a container for your app
	
	https://tagmanager.google.com
	Next to the app name you see an accountId
	
how it works

	create a variable in tag manager
	publish the container in tag manager
	get the variable in your code
	use the variable in your code

now go to 

	Tag manager Dashboard> Container > Variables > User defined variables > new > ValueCollection> Enter variable name > put {key:'value'} >continue > Enable when always >Create

the variable is in User defined variables. But it's not enough. Now you need to 

	publish the variable (button on top)
	
more on

	https://support.google.com/tagmanager/answer/6106899?hl=en#mobile
	
now we needto add a default version of a container to the app

	DashBoard>Versions>Live,Lastest>Actions>Download
	

you get a

	GTM-WDWL6Z.json
	
rename it with lowercase and _ no .json 

	exple: gtm_default
	
paste it in res/raw/

	the app will get the data from the latest container on the web, but it is requiered that there is a default container like this even if it is an empty container
	
in the mainActivity onCreate a function that 

	Get the TagManager
	load the container passing the TagManager account id and the default container that you downloaded
	then you need a result callback setResultCallback that will be called when the loading is finished.
	in this callback we manually refresh the holder with latest version (we only need that because we want our change to be seen instantaneously when we test, but without that the change wouldhave appear at worse 12h later. According to the doc, we are supposed to wait at least 15min before calling this method again, sometimes changes can happens only after 15min)
	save the holder using setContainerHolder method
	
se bellow

	public void loadGTMContainer () {
        // TODO Get the TagManager
        mTagManager = ((MyApplication) getApplication()).getTagManager();

        // Enable verbose logging
        mTagManager.setVerboseLoggingEnabled(true);

        // Load the container
        PendingResult pending =
                mTagManager.loadContainerPreferFresh("GTM-123456",   
                        R.raw.gtm_default);

        // Define the callback to store the loaded container
        pending.setResultCallback(new ResultCallback<ContainerHolder>() {
            @Override
            public void onResult(ContainerHolder containerHolder) {

                // If unsuccessful, return
                if (!containerHolder.getStatus().isSuccess()) {
                    // Deal with failure
                    return;
                }

                // Manually refresh the container holder
                // Can only do this once every 15 minutes or so
                containerHolder.refresh();

                // Set the container holder, only want one per running app
                // We can retrieve it later as needed
                ((MyApplication) getApplication()).setContainerHolder(
                        containerHolder);

            }
        }, 2, TimeUnit.SECONDS); //timeout o 2 seconds for the container to load.
    }

Now in your app

        // Get the container holder
        ContainerHolder holder =
                ((MyApplication) getApplication()).getContainerHolder();

        // Get the daily special from the container holder
        // The keys need to match exactly the keys you set in the Tag Manager interface
        mDailySpecial = holder.getContainer().getString("daily-special");
		
	
the method loadContainerPreferFresh

	check if the container has been refresh during the last 12h
	if yes we load, if no we load a new one
	if there is a timeout or network error befoe the container has finished loading the container holder status is set to unsuccessful
	gives the freshest value
	
there other methods

	loadcontainerDefaultOnly() which only load the default container
	loadcontainerPreferNonDefault() does not use the default and does not necessarlly look for a fresh container
	
	
### built in variables

	Dashboard > Variables > Built-in variable > Device > Select Language
	
We will use this to trigger which variable value to use depending on the device language

	rename daily-special variable in daily-special-en	
	note we have also used daily-special for the key of the container, this does not change
	
now create a trigger that will be used when the user device is set to english

	Enable when > Custom > New > rename Untitle trigger to English Trigger > Choose event Custom >Fire On>	Language > equals > en >Save Trigger
	
remove the previously default trigger marked as... meaning for all languages

	always
	
last

	save the variable
	
Now

	Dashboard > Trigger > you can find English Trigger
	
create a french trigger

	Dashboard > Trigger > New > French Trigger > Choose event Custom >Fire On>	Language > equals > fr >Save Trigger
	
now 

	Dashboard > Variables > daily-special-en > Copy > rename daily-special-fr
	
Now we have

	2 variables
	2 triggers

Now you can publish. 

	Try the app with english language
	Try with french
	try with spanish (nothing displayed because there isno default)
	
If you want english to be the default language

	Add a trigger "Always" to the "English Trigger"
	Create Exception from existing trigger "French Trigger"
	Save the variable
	publish

### data layer

Your app can put data in the data layer like "vegan" or "meat" that way the tag manager can send à more appropriate result (or variable) to the user. Basically.

	The app store a food_pref in the data_layer of the tag manager
	the triggers get the food_pref and retrieve the user-defined-variable
	
	
To store a food_pref in the data_layer of the tag manager

	TagManager myGTM = ((MyApplication) getApplication()).getTagManager();
	DataLayer dataLayer = myGTM.getDataLayer();
	String selectedFoodPref = "vegan";
	dataLayer.push("food_pref", selectedFoodPref);

Create a dataLayer variable on the TagManager

	Dashboard > Variables > User defined variable > New > Data Layer Variable > name it food_pref > in configure variable, put the key here food_pref > default 'unrestricted eater' or whatever suit best
	
Create other variables 

	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454014/modules/8011345401475460/lessons/4027658558/concepts/43875502000923
	daily-special-vegan
	daily-special-meat
	daily-special-fish...
	
Create the triggers
	
	Dashboard > Trigger > New > Vegan Trigger > Choose event Custom >Fire On>	food_pref > equals > vegan >Save Trigger
	etc...
	
Publish.

Take this quizz please !!

https://classroom.udacity.com/nanodegrees/nd801/parts/80113454014/modules/8011345401475460/lessons/4027658558/concepts/43300399360923


### receive hit data from your app and send it to GoogleAnalytics

You can use tag manager to send tags to

	google analytics
	google adwords
	double clicks
	...
	
The main interest in sending data to tag manager and then from tag manager to analytics is

	the facility of renaming tags
	AND if your app is already used by many user, unless they download the latest app, you will still get your old tag label
	
How do you do that ?

	by putting an event into the data layer dataLayer.push("event", event parameter); note key should always be "event"
	
or you can use

	dataLayer.pushEvent(event parameters)
	
event parameters are : 

	eventName,
	dataLayer.mapOf(key1, value1, key2, value2, key3...)
	key1, key2 should be datalayer variables in tag manager
	
example

	DataLayer dl = mTagManager.getDataLayer();
	dl.pushEvent("openScreen", DataLayer.mapOf( "screen-name", "Show Daily Special"));
	
add the datalayer variable screen-name. 

then create triggers

Triggers > New > Name it OpenScreen > Fire On > Event > equals > openScreen (the event name given in code) >save
Triggers > New > Name it DailySpecialScreen > Fire On > screen name > equals > Show Daily Special >save

create a tag

Tags > New > Name it Send Daily Special Hits > For google analytics id, don't copy it raw, create a variable > New variable > Constant > name it AnalyticTrackingId > Set thevalue> tracktype: AppView iswhat we want > More Settings > fields to set > fied name > screenName > value > screen name > Fire On > Custom > select openscreen (when event equals openscreen) and Daily Special Screen > Save > Publish

Now in google analytics

	you see acolumn Screen Name with "Show Daily Special" event

If you want to track specifics events , create a tag

	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454014/modules/8011345401475460/lessons/4324988718/concepts/43259197190923
	
using tag manager you can also send ... to analytics

	e-commerce hits
	timing hits
	exception hits
	custom functions
	see https://developers.google.com/tag-manager/android/v4/enhanced-ecommerce
	see https://developers.google.com/tag-manager/android/v3/#function-call-tag
	
to understand everythings about analytics ... the place to be

	https://analyticsacademy.withgoogle.com/
	
	
# Google AdMobs

Monetization models

	Paid downloads (can be configured in the play store)
	Subscriptons (can be configured in the play store)
	Displaying ads
	In-App purchases : allow to advertise and sell digitals goods right in your app. Like new levels or items in a game.
	
	
Paid downloads

	easy to launch ? no
		the user must somehow really be sure of the value your app do in order to pay for it
		compare to all apps on the markets, only few famous people can afford this
	long term revenue ? no
		once the user has paid at first, he won't expect to be charged anymore
		you get revenus only when they download
	user value ? yes high user value
		afterall the user is willing to pay upfront to get this app
		
Subscriptons : the user pay an amount regularly for example monthly
	easy to launch ? no
		again you ask the user to pay upfront
		even more you ask the user to pay every months
	long term revenue ? yes
		the user will continue to pay for your app as long as it's provide value
		you will continue to get revenus from all users not only new
	user value ? yes high user value
		same here afterall the user is willing to pay upfront to get this app
		
Displaying ads
	easy to launch ? yes
		in particular if there is no charge fortheapp
	long term revenue ? yes
		as long as your app is used you will be payed for displayings adds.
	user value ? yes (I was surprised)
		yes because ads of AdMobs gives relevant adds for the user
		if user feels ads given help him in his life, he is not disturb
		
In-App purchases
	easy to launch ? yes
		very easy because the user doesn't have to pay for anything upfront.
	long term revenue ? yes
		as long as you can offer new digital goods all the time
	user value ? yes 
		since the user is engaged with the app, and you control what to advertise and sell, you can find your people, and keep adding valuein their life.
		
		
Monetization models very often combined (in order)

	Displaying ads && In-App purchases
	Subscriptons && In-App purchases
	Paid downloads && In-App purchases
	
Type of ads

	banner ads
	interstitial ads
	natives ads
	
Banner ads

	are small and can be share by content displayed by your app
	can be text or image
	
Interstitial ads

	cover the entiere screen
	it is perfect when there is a natural break in your add (example reaching a new level in a game)
	can show text, image and video
	
Natives ads

	gives you much more possibility to customise look and feel of the ad
	
This link is very good

	how to integrate the Google Mobile Ads SDK into a brand new app and use it to display an AdMob banner ad : https://developers.google.com/admob/android/quick-start
	
The banner_ad_unit_id we will choose will decide for text image or video selon ce qu'on veut.

It is good practice to add an ad listener like this 

	mAdView.setAdListener(new ToastAdListener(this));
	
and override 

	onAdLoaded
	onAdFailedToLoad(int code) //This give you the code error which refers to the AdRequest class
	onAdOpened //call when the user click on the ad
	onAdLeftApplication //called when an ad open another app like a browser
	onAdClosed // when the user is about to return to your application 
	
With interstitial ads we should

	place them when there is a natural break
	prepare loading before showing. Because loading it can be long and we don't want the user to wait for the ad to load when it's time to show it.
	
it's good pracice to 

	load the ad
	check if the ad has been loaded
	and show it
	
## Create an AdMob account

go to : 

	https://apps.admob.com/
	
once created you get an id Publisher ID: pub-3851606972906527 that identifie your account and can be use for contact support.
To monetize your app

	first put your app on google play
	look for the name
	select it 
	follow this :https://classroom.udacity.com/nanodegrees/nd801/parts/80113454015/modules/8011345401575460/lessons/4000748701/concepts/42743533330923
	
For more on Ad follow https://admob.googleblog.com/


# Google Maps

	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454016/modules/8011345401675460/lessons/4015598606/concepts/42806589290923

To access the Google Map Api you need a SHA 1 key (=fingerprint of your app= certificate given by a third party certificate supplier that can attest you deserve this certificate). Here we will get a "debug certificate"(=third party is yourself), but if you want publish to the play store you will need a "publication certificate" (=third party is google). Now, first locate your debugging keystore file by using a terminal.

	cd /c/Users/Elorri/.android
	
As you can see this directory contains a debug.keystore file. Now ask to get a certificate : 

	/c/Program\ Files/Java/jdk1.8.0_71/bin/keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
	
As you can see we have chosen an alias "androiddebugkey" to the certificate. Also when generating the debug certificate default password(=storepass) and username(=keypass) is just "android". Press Enter and you get the certificates fingerprints : 

	MD5
	SHA1
	SHA256

Just keep track of the SHA1 key. In my case SHA1 is : 

 SHA1 : 4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34

Or keep the whole certificate in a debug_certificate.txt in your app directory

	Nom d'alias : androiddebugkey
	Date de création : 22 oct. 2015
	Type d'entrée: PrivateKeyEntry
	Longueur de chaîne du certificat : 1
	Certificat[1]:
	Propriétaire : CN=Android Debug, O=Android, C=US
	Emetteur : CN=Android Debug, O=Android, C=US
	Numéro de série : 48b7e73e
	Valide du : Thu Oct 22 13:06:43 CEST 2015 au : Sat Oct 14 13:06:43 CEST 2045
	Empreintes du certificat :
			 MD5:  E1:25:98:AD:52:F5:A0:21:4B:99:6B:1A:78:E7:8B:CD
			 SHA1 : 4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34
			 SHA256 : 70:54:74:C1:45:43:7F:D9:5C:3B:26:F2:EC:02:7E:14:88:63:75:A1:90:D3:18:4E:06:48:8C:CB:36:01:41:8F
			 Nom de l'algorithme de signature : SHA256withRSA
			 Version : 3

	Extensions:

	#1: ObjectId: 2.5.29.14 Criticality=false
	SubjectKeyIdentifier [
	KeyIdentifier [
	0000: E1 44 85 35 DF D8 2C 63   15 6C 7A 9B 0A E6 88 5A  .D.5..,c.lz....Z
	0010: 57 11 0F FA                                        W...
	]
	]
Note :

	you will need your debug certificate to setup your Google credential in the android developper console
	
Now to set Maps you will need

	Set up Billing : you do this once for all applications under the same project.
	Create a Project : for each app
	Enable Maps API : for each app
	Set Up Credentials : for each app
	
Set up billing. Go to 

	https://console.developers.google.com/

Not every api services are charge but you still need to set billing before creating a project. What I know is charged is : 

	AppEngine
	CloudStorage
	
What I know is not charged 

	Maps
	
More on sign in for release app

	https://developer.android.com/studio/publish/app-signing.html

Step to set up billing

	name the account
	specify country for the account
	account type : business or individual
	payer details
	payment type (you will have to give you credit card details)
	
Create a project (if the billing is done otherwise not). Go to.

	https://console.developers.google.com/project
	
Then 

	Create Project > Project name : My First Map > Project Id (it must be unique accross all your projects, put a name that is not taken if you can or use the generator) exp udacity-firstmap-1 > Select the biling account> Create
	
Then you reach the project DashBoard. It's time to enable maps . Go to : 

	Api & auth > Apis > Google Maps Apis > Google Maps Android Apis > Enable API
	
Now I can set up the credentials

	Api & auth > Credentials > Public API Access > Create new Key > Android key >
	
Now if asking for my SHA1. Because I'm not deploing the app or doing anything that requiered my certificate to be checked by a real third party, I don't really need to put the fully qualify name of my app, I can put anything. But I prefer to put the fully qualified name.You can change the name later anyway. So in "Accept request from android ..." put

	<SHA1><;><com.google.devplat.lmoroney.maps1>
	
which become 

	4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34;com.google.devplat.lmoroney.maps1
	
then click on 

	Create
	
then you get an API key. Copy it.

	API key : AIzaSyAZRHN3qsEtG2apTeywhArWzmzkYVWeFAA

Now set your android studio project

	Create a blanck activity
	edit gradle
	edit manifest
		add meta for google services
		add meta API key
		add permissions for internet, network stateand write external storage
		add meta for OpenGL
	
edit gradle

	compile 'com.google.android.gms:play-services:6.5.+'
	
add meta for OpenGL

	<uses-feature
	android:glEsVersion="0x00020000"
	android:required="true"/>

add meta for google services

	<meta-data
		android:name="com.google.android.gms.version"
		android:value="@integer/google_play_services_version" />

add meta API key

    <meta-data android:name="com.google.android.maps.v2.API_KEY" android:value="AIzaSyAZRHN3qsEtG2apTeywhArWzmzkYVWeFAA"/>
	
add permissions for internet, network stateand write external storage

	<uses-permission android:name="android.permission.INTERNET"></uses-permission>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
	
see for more info: 

	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\MapsLessons_Final\Maps1\app\src\main\AndroidManifest.xml
	
Now you can customise your app. In the activity_main.xml layout instead of call our own fragment like we usally do we will call their fragment.

    <fragment xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:name="com.google.android.gms.maps.MapFragment"/>
		
Now run your app. You will see a world map (because we have not set up the camera). Now we can customize it and add some presisions. Add the map namespace and attributes.

    <fragment xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:map="http://schemas.android.com/apk/res-auto"
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:name="com.google.android.gms.maps.MapFragment"
        map:cameraBearing="112.5"
        map:cameraTargetLat="40.7484"
        map:cameraTargetLng="-73.9857"
        map:cameraTilt="65"
        map:cameraZoom="17"
        />
	
Latitude and Longitude

        map:cameraTargetLat="40.7484"
        map:cameraTargetLng="-73.9857"
		
Bearing = direction the camera is looking at

	0 degrees = look north
	180 degrees = look south
	90 degree = look east
	270 degree = look shouth
	
Tilt = l'angle par rapport au point regardé. 

	0° = camera est juste au dessus. look straight down. defaut tilt. perpendiculaire of the ground le sol
	67,5° = regarde vers le bas mais un peu vers le haut aussi. It'sthe max possible tilt
	
Zoom = 

	The larger the number the closer you are to the surface. 
	0 being the smallest number. Zoom out
	21 being the largest number. Zoon in
	if you are close enough you will automatically see the 3D view.
	
Zoom and Tilt

	if you zoom out really far, then the max tilt is 30°
	if you zoom in really far, then the max tilt is 67,5°

Using xml as we did is limited because the map start always in the same location. If we want to dinamically change the location then we need a google map object. See : 

	C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\MapsLessons_Final\Maps3_2
	

Create a new android studio project and associate it with the same API key. Do you remenber this line?

	4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34;com.google.devplat.lmoroney.maps1

Then add this under it 

	4A:C2:CC:37:DC:90:F5:51:BE:B0:F6:7D:73:90:9F:02:46:47:22:34;com.google.devplat.lmoroney.maps3_2
	
See it's the same SHA1. ink to theconsole.

	Api & auth > Credentials > Public API Access > Edit Allowed Android Applications

Then to get a google map object "m_map" by implementing the OnMapReadyCallback and overide ... as folow

    @Override
    public void onMapReady(GoogleMap map){
        mapReady=true;
        m_map = map;
        LatLng newYork = new LatLng(40.7484,-73.9857);
        CameraPosition target = CameraPosition.builder().target(newYork).zoom(14).build();
        m_map.moveCamera(CameraUpdateFactory.newCameraPosition(target));
    }
	
It very easy to set a view property on a Google Map Object. You see : 

	m_map.setMapType(GoogleMap.MAP_TYPE_NORMAL);
	m_map.setMapType(GoogleMap.MAP_TYPE_SATELLITE);
	m_map.setMapType(GoogleMap.MAP_TYPE_HYBRID);

Now the last thing to do is to load your fragment in an async task by calling in the onCreate.

	((MapFragment) getFragmentManager().findFragmentById(R.id.map)).getMapAsync(this);
	
	
## Set more camera stuff

The camera 
	is controlled by a CameraPosition
	has properties
		target latitude
		target longitude
		zoom 

To set a Camera

    static final CameraPosition cameraPosition = CameraPosition.builder()
            .target(new LatLng(40.784,-73.9857)) //A latlng contains its latitude and longitude
            .zoom(21)
            .bearing(0)
            .tilt(45)
            .build();
			
then to move instantaneously the camera to the position call

	m_map.moveCamera(CameraUpdateFactory.newCameraPosition(cameraPosition));
 
But if you want to animate it to the position

	m_map.animateCamera(CameraUpdateFactory.newCameraPosition(cameraPosition), 10000, null);
	take time in millis
	null = callback function.it's called when the animation is done.
	
## Putting pins on all location that you want

Note on the pins label you can put some useful info

	the name of the location of course
	the date ofthe next appointement
	the adress
	
To do so you need to define a marker

      MarkerOptions rentonPlace = new MarkerOptions()
                .position(new LatLng(47.489805, -122.120502))
                .title("Renton Place")
                .icon(BitmapDescriptorFactory.fromResource(R.drawable.ic_launcher)); //This last part is optional but really cool if you use you own graphics
				
Then you have to implement as before onMapReadyCallback and overide onMapReady.This here where you will add your markers.

    @Override
    public void onMapReady(GoogleMap map){
        m_map.addMarker(renton);
    }
	
	
## Polylines

	are made up of a number of lines segments that are drawn on a map
	the end point of those line are defined using latitude and logitude (LatLng = position)

how to add them. Note if you want to close the shape you need to start and stop with the same LatLng

    LatLng renton=new LatLng(47.489805, -122.120502);
    LatLng kirkland=new LatLng(47.7301986, -122.1768858);
    LatLng everett=new LatLng(47.978748,-122.202001);
    LatLng lynnwood=new LatLng(47.819533,-122.32288);
    LatLng montlake=new LatLng(47.7973733,-122.3281771);
    LatLng kent=new LatLng(47.385938,-122.258212);
    LatLng showare=new LatLng(47.38702,-122.23986);
	

	map.addPolyline(new PolylineOptions().geodesic(true)
			.add(renton)
			.add(kirkland)
			.add(everett)
			.add(lynnwood)
			.add(montlake)
			.add(kent)
			.add(showare)
			.add(renton));
		
## Polygone

	same as polyline except that the shape is always close. Means you don't have to start and stop with the LatLng.
	it can be filled with color.
	
	map.addPolygon(new PolygonOptions().add(
		renton,
		kirkland,
		everett,
		lynnwood)
		.fillColor(Color.GREEN));
				
## Circle. 

Note that if your camera is not oriented at 90° the circle will look oval

	map.addCircle(new CircleOptions()
			.center(renton)
			.radius(5000)
			.strokeColor(Color.GREEN) //color that draw the circle
			.fillColor(Color.argb(64, 0, 255, 0))); //nearly transparent because of the 64.
			
			
## Street View

This time you activity_main.xml is gonna use a StreetViewPanoramaFragment as follow

    <fragment
        android:name="com.google.android.gms.maps.StreetViewPanoramaFragment"
        android:id="@+id/streetviewpanorama"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
		
Now this is the step you have to take

	implements OnStreetViewPanoramaReadyCallback
	create a StreetViewPanoramaFragment object
	call streetViewPanoramaFragment.getStreetViewPanoramaAsync(this);
	override onStreetViewPanoramaReady
	
This how they did

	public class MainActivity extends FragmentActivity implements OnStreetViewPanoramaReadyCallback{

		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
			StreetViewPanoramaFragment streetViewPanoramaFragment =
					(StreetViewPanoramaFragment) getFragmentManager()
							.findFragmentById(R.id.streetviewpanorama);
			streetViewPanoramaFragment.getStreetViewPanoramaAsync(this);
		}

			@Override
					 public void onStreetViewPanoramaReady(StreetViewPanorama panorama) {
			// Set the panorama location on startup, when no
			// panoramas have been loaded.

			panorama.setPosition(new LatLng(36.0579667,-112.1430996)); //grand canyon position
			StreetViewPanoramaCamera camera = new StreetViewPanoramaCamera.Builder()
					.bearing(180)
					.build();
			panorama.animateTo(camera,10000);

		}
	}
	
If the user has move on the map and you want to get his location

	panorama.getLocation() witll give you  StreetViewPanoramaLocation
	
Default behavor you can change

	Street names
		isStreetNamesEnabled()
		setStreetNameEnabled()
	Zoom gestures
		isZoomGesturesEnabled()
		setZoomGesturesEnabled()
	UserNavigation
		isUserNavigationEnabled()
		setUserNavigationEnabled()

Respond to user interaction

	Detect camera changes : setOnStreetViewPanoramaCameraChangeListener
	Detect user touch on panorama : setOnStreetViewPanoramaClickListener
	Detect changes to the panorama : setOnStreetViewPanoramaChangeListener
	
# Google sign in

	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454016/modules/8011345401675460/lessons/4331999941/concepts/43269941550923

	Allow user to sign once and to be authenticated in all the devices you support and they use
	It allows you to integrate googleservices into your website and mobile apps
	
To use Google sign in you need 

	1. Android device with 2.3 android version or higher
	2. Android device with google play store installed
	3. Latestversion of sdk
	4. Core services sdk
	
Then you need

	a SHA-1 fingerprint for your app
	
Then you reach the project DashBoard. It's time to enable Google Sign In . Go to : 

	Api & auth > Apis > Google Plus Apis > Enable it > Enable API
	
Then go to 

	Api & auth > Consent screen > put youremail adress > put a product name exple Signin_v1 > Save
	For all projects registered under this product name, a consent screen will appear to the user
	
Then go to 

	Api & auth > Credential > Create new client Id > Installed application > Android > put a package name com.elorri.android.signin_v1 > copy paste your SHA1 > Deep linking disabled > Create new client Id
	
After all of that :

	Only applications with the correct fingerprint will be able to sign in and open the package
	
In the manifest add permissions

	INTERNET
	GET_ACCOUNTS
	USE_CREDENTIALS
	
Scopes

There is differents kind of scopes

	profile
	plus.login
	email
	plus.profiles.emails.read
	
Profile

	basic login scope
	it gives your app access to the authenticated user basic profile info
	this include : 
		ID
		display name
		image url
		profile url
	
Plus.login

	gives access to the social features from google plus
		include profile scope (ID, display name etc)
		age range
		list of circles that user has given permissions to access
		ability to read or write activities on the person google+ wall

Email

	gives access to 
		the user google account email adress
		the user google apps domain if he has one
		
Plus.profiles.emails.read

	gives access to
		email scope
		access to any other public email adresses that are in the user google+ profile
		
See demo 

	https://classroom.udacity.com/nanodegrees/nd801/parts/80113454016/modules/8011345401675460/lessons/4331999941/concepts/43287299020923
	clicling on sign in lead you to the consent screen
	because the app is using only profile scope, the consent screen only ask for profile scope
	
In activity_main.xml add 

	<com.google.android.gms.common.SignInButton
	android:id="@+id/sign_in_button"
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:layout_marginBottom="30dip"
	android:enabled="false" />
			
Create a Googel Api client

    public GoogleApiClient buildApiClient(){
        return new GoogleApiClient.Builder(this)
                .addConnectionCallbacks(this)
                .addOnConnectionFailedListener(this)
                .addApi(Plus.API, Plus.PlusOptions.builder().build())
                .addScope(new Scope(Scopes.PROFILE))
                .build();
    }

Add connection callbacks

	onConnectionSuspended
	onConnected
	onConnectionFailed
	onConnectionSuspended

onClick sign in

	mStatus.setText("Signing In");
	resolveSignInError();
					
onClick sign out

	// We clear the default account on sign out so that Google Play
	// services will not return an onConnected callback without user
	// interaction.
	Plus.AccountApi.clearDefaultAccount(mGoogleApiClient);
	mGoogleApiClient.disconnect();
	mGoogleApiClient.connect();
					
onClick revoke access button

	// After we revoke permissions for the user with a GoogleApiClient
	// instance, we must discard it and create a new one.
	Plus.AccountApi.clearDefaultAccount(mGoogleApiClient);
	// Our sample has caches no user data from Google+, however we
	// would normally register a callback on revokeAccessAndDisconnect
	// to delete user data so that we comply with Google developer
	// policies.
	Plus.AccountApi.revokeAccessAndDisconnect(mGoogleApiClient);
	mGoogleApiClient = buildApiClient();
	mGoogleApiClient.connect();
	
I've not finished this course so if needed

	checkout the code C:\Users\Elorri\Dropbox\Udacity\Classes\11 Google Play Services\Identity_Lessons_Final
	or videos https://classroom.udacity.com/nanodegrees/nd801/parts/80113454016/modules/8011345401675460/lessons/4331999941/concepts/43287299020923
	For an intro of Dagger with android https://medium.com/di-101/di-101-part-1-81896c2858a0#.1e4gd54i9
	
# Tests

dependency injections:Dagger2
	https://www.youtube.com/watch?v=oK_XtfXPkqw

Older dependency injections stuff

	Spring
	Juice
	Dagger1
	Butterknife
	
	
	
	
# Others notes 

mockup design écrans screens https://balsamiq.com/


commit guidelines, git guidelines

http://udacity.github.io/android-nanodegree-guidelines/git.html

Resume here :
feat: a new feature
fix: a bug fix
docs: changes to documentation
style: formatting, missing semi colons, etc; no code change
refactor: refactoring production code
test: adding tests, refactoring test; no production code change
chore: updating build tasks, package manager configs, etc; no production code change

My own thoughts : 

There is 2 kinds of commits :
commits for features (feat: test: docs: fix: refactor: style:)
commit for the app in general (refactor: style: chore:)

Also the commit can be : 
absolutely requiered : +
optionnal : -
requiered if necessary : o

Planning the app developpement means make the list of commits you want to see.
Example: if your app need a SyncAdapter you should see the following commits in the end : 

+ feat: Add a SyncAdapter
+ test: Add a SyncAdapter
+ docs: Add a SyncAdapter
o fix: Add a SyncAdapter X bug
o refactor: Add a SyncAdapter
o style: Add a SyncAdapter

Others thoughts: if one day I create an app that generate the planning of an app it should be like this.
(First note : a scenario of use will become a realease. Here we are talking of a release. A release is divided into big steps that will always be the same in every apps. The steps will be filled with tasks = commits.)

There should be a table feature with

	name : SyncAdapter
	Action : Add a SyncAdapter
	Examples/How to : links to github compares or udacity classes
	possibles commits with elapse time (elapse time shouldn't be higher than 2h to have 5commits/days, if higher consider dividing the task into severals commits)
		feat: Add a SyncAdapter (3h)
		test: Add a SyncAdapter (3h)
		docs: Add a SyncAdapter (3h)
		fix: Add a SyncAdapter X bug (3h)
		refactor: Add a SyncAdapter (1h)
		style: Add a SyncAdapter (10min)

There should be a table Comparable with comparable elements like 

	suitable for connect to the net ? true/false
	suitable for battery life ? true/false
	
The UX should have 2 buttons : Plan and Compare

If Plan is selected : 
first screen is the list of steps wrappings their features
user select features he is interested in and click next
the selected features appears and ask fot the selection of quantities (click several time on an item to add one) and click next.
the app asked for the names we will give to each feature (this step couldbe optional) next
the app générate the .md with 
	the list of commit as titles 
	their examples
	their average time
	
	
	
# other notes
icons open sources font awesome


App validates all input from servers and users. If data does not exist or is in the wrong format, the app logs this fact and does not crash.
App is equipped with a signing configuration, and the keystore and passwords are included in the repository. Keystore is referred to by a relative path.

If it regularly pulls or sends data to/from a web service or API, app updates data in its cache at regular intervals using a SyncAdapter.
OR
If it needs to pull or send data to/from a web service or API only once, or on a per request basis (such as a search application), app uses an IntentService to do so.
OR
If it performs short duration, on-demand requests(such as search), app uses an AsyncTask.


# Firebase

https://console.firebase.google.com/



Note 

Firebase rootRef = new Firebase("https://docs-examples.firebaseio.com/web/data");
rootRef.child("users/mchen/name");

is equivalent to 

Firebase rootRef = new Firebase("https://docs-examples.firebaseio.com/web/data/users/mchen/name");

Firebase databases have no native support for lists or arrays. If we try to store an list or an array, it really gets stored as an "object" with integers as the key names.

	// we send this
	['hello', 'world']
	// Firebase databases store this
	{0: 'hello', 1: 'world'}

To enable logging. Do it for each device : phone, tablette, emulator
/c/Users/Elorri/AppData/Local/Android/sdk/platform-tools/adb shell setprop log.tag.FA VERBOSE
/c/Users/Elorri/AppData/Local/Android/sdk/platform-tools/adb shell setprop log.tag.FA-SVC VERBOSE
/c/Users/Elorri/AppData/Local/Android/sdk/platform-tools/adb logcat -v time -s FA FA-SVC


then select

	verbose
	no filter
	search :FA
	f
or 

	verbose
	no filter
	search :Logging event

or 

	verbose
	no filter
	search :Event recorded
	
	
1.add google-service.json file to the app/ directory
2. build

The build will generate appropriate xml files see ... for a list: 

	https://developers.google.com/android/guides/google-services-plugin#processing_the_json_file
	
but if some files are missing make sure you have installed the appropriate google service plugin



#Lessons that I've not done (because they have been updated)

Connect Sunshine to the cloud
Google cloud messaging
Places
Publishing your app



# Career 

Resume review
Cover Letter review
Github Profile review
Android interview dry-run
Udacity Professionnal Profile Review


# Testing with cucumber


## Behavior driven developpement (BDD)

1describe your idea
2listen their reformulation
3have they understood? no explain better
4listen their feedback
5reformulate
6have you understood
7both parties agree

## Test driven developpement (TDD)

### Automated Acceptance Tests : build the right thing

developper and stakeholder write automated test together. They are called acceptance test. Because they express what the software needs to do in order for the stakeholder to find it acceptable.

we write them as examples and with ubiquitous language called Gherkin in a file called "feature". 
Each scenario will be a test. A scenario is composed of steps.
Each test will be one or 2 lines code not more. That delegate work to a library.
This library should have an analytics log. In the future, it will tel us, how much of all our users are performing this scenario of use.

Cucumber has more that 50 languages.
You can use tags to organize and group your scenarios.
Each feature typically has somewhere between five and twenty scenarios

#### Githup repos

for android

	https://github.com/cucumber/cucumber-jvm

for iOS

	https://github.com/unboxed/icuke
	https://blog.jayway.com/2011/02/11/cucumber-tests-on-iphoneipad/

#### Feature file example

	Feature: Sign-up

		Sign-up should be quick and friendly.
		
	Scenario: Successful sign-up

		New users should get a confirmation email and be greeted personally by the site once signed in.
		
	Given I have chosen to sign up
	When I sign up with valid details
	Then I should receive a confirmation email
	And I should see a personalized greeting message

	Scenario: Duplicate email

		Where someone tries to create an account for an email address that already exists.

	Given I have chosen to sign up
	When I sign up with an email address that has already registered
	Then I should be told that the email is already registered
	And I should be offered the option to recover my password
	
With this Cucumber generate snipset of "StepDefinitions" that we can copy paste in file with generally a name terminated withs "steps" and in a directory steps_definition

	step_definition/CheckoutSteps.java

### Unit tests : build the thing right

aimed at developers to check their software designs.

### To run cucumber you need

add cucumber, cucumber-java, cucumber-grovy plugins
add dependencies (not sure they are all useful)

    androidTestCompile 'info.cukes:cucumber-jvm:1.2.4'
    androidTestCompile 'info.cukes:cucumber-android:1.2.4'
    androidTestCompile 'info.cukes:cucumber-java8:1.2.4'
    androidTestCompile 'io.cucumber:gherkin:4.0.0'
    androidTestCompile 'info.cukes:cucumber-core:1.2.4'
    androidTestCompile 'info.cukes:cucumber-picocontainer:1.2.4' //for dependency injection
	
in Run>Edit Configuration

	Main class : cucumber.api.cli.Main (should be already set)
	Glue : add link to the step_definition directory : C:/AndroidStudioProjects/Examples/CucumberCheckout/app/src/androidTest/java/com/example/android/cucumbercheckout/test
	feature or folder path : C:/AndroidStudioProjects/Examples/CucumberCheckout/app/src/androidTest/assets/features(should be already set)


### From Acceptance criterias to Acceptance test

Stakeholders "Customers should be prevented from entering invalid credit card details".
Developper : Think it lack precision. "Lets illustrate by an example"

	If a customer enters a credit card number that isn’t exactly 16 digits long, when
	they try to submit the form, it should be redisplayed with an error message advising
	them of the correct number of digits.
	
### Gherkin language

#### keywords 

• Feature
• Background
• Scenario
• Given
• When
• Then
• And
• But
• *
• Scenario Outline
• Examples


#### template for describing a feature (called Feature Injection template):

	In order to <meet some goal>
	As a <type of stakeholder>
	I want <a feature>

#### Scenario pattern

Given, When, Then

	context : Get the system into a particular state.
	action : Poke it (or tickle it, or…).
	outcome : Examine the new state.
	
	context : Given
	action : When
	outcome : Then
	
And, But

	doesn't matter where there are.
	use for readability
	
This is 

	Scenario: Attempt withdrawal using stolen card
	Given I have $100 in my account
	But my card is invalid
	When I request $50
	Then my card should not be returned
	And I should be told to contact the bank
	
equivalent to 

	Scenario: Attempt withdrawal using stolen card
	Given I have $100 in my account
	Given my card is invalid
	When I request $50
	Then my card should not be returned
	Then I should be told to contact the bank
	
or 

	Scenario: Attempt withdrawal using stolen card
	* I have $100 in my account
	* my card is invalid
	* I request $50
	* my card should not be returned
	* I should be told to contact the bank

Steps

	all those keywords define steps : Given, When, Then, And, But, *
	note : step definitions are the function in the java file
	
Good practices

	Each scenario must be executed independently of any other scenario.	That means : When writing a scenario, always assume that it will run against the system in a default, blank state. Tell the story from the beginning, using Given steps to set up all the state you need for that particular scenario.

Good Naming practices

	Scenario name: avoid putting anything about the outcome (the Then part) of the scenario into the name and concentrate on summarizing the context and event (Given and When) of the scenario. Stakeholders often ask you for more "then". That way you name is always up to date and meaningful.
	
How to find your scenarios?

	create one then ask yourself
	what happen if I change the context
	what happen if I change the action
	ask the "then" at the stakeholder
	
	
#### Comments or description

	Description, which you can put after each keyword, is part of the structured Gherkin document and is the right place to put documentation for your stakeholders. 
	Comments, on the other hand, can be used more to leave notes for testers and programmers who are working with the features. Think of a comment as something more temporary, a bit like a sticky note. Comments starts with #

#### Languages

Put this first line feature file	

	norvegien -> # language: no 
	francais -> # language: fr ? 
	
### From business domain to programmer domain = from steps to steps definitions

#### Check false positives : 

Check you don't have a step phrase found in several annotations like this...

	Given I have $100 in my account
	But my card is invalid
	When I request $50
	Then my card should not be returned
	And I should be told to contact the bank

	Scenario: New accounts get a $1 gift
	Given I have a brand new Account
	And I deposit $99
	Then I have $100 in my Account
	
Given and Then have both : "Then I have $100 in my Account", this will cause false positives and end up calling same step_definition. To avoid this be more precise

	Given I have deposited $100 in my Account
	Then the balance of my Account should be $100
	
#### Use arguments : Cucumber will pass an argument to your method for every capture group in your regular expression, so you can grab as many details as you like from a step.

Replace this 

	@Given("I have deposited \\$100 in my Account")
	public void iHaveDeposited$100InMyAccount() {
	// TODO: code goes here
	}
	@Given("I have deposited \\$250 in my Account")
	public void iHaveDeposited$250InMyAccount() {
	// TODO: code goes here
	}

By this : 

	@Given("I have deposited \\$(100|250) in my Account")
	public void iHaveDeposited$100InMyAccount(int amount) {
	// TODO: code goes here
	}

or this 

	@Given("I have deposited \\$(...) in my Account")
	public void iHaveDeposited$100InMyAccount(int amount) {
	// TODO: code goes here
	}

but this last will only match 

	I have deposited $100 in my Account
	I have deposited $250 in my Account

not ... it only match 3 characters

	I have deposited $10 in my Account
	
to match an undefined number

	@Given("I have deposited \\$(.*) in my Account")
	public void iHaveDeposited$100InMyAccount(int amount) {
	// TODO: code goes here
	}
	
but then we will also match ... or ...

	I have deposited $1 and a cucumber in my Account
	I have deposited in my Account
	
we have to be more specific about the character type and use 

	@Given("I have deposited \\$([01234567890]*) in my Account")
	
or because it's continuous range of characters like we have, you can use a hyphen:

	@Given("I have deposited \\$([0-9]*) in my Account")
	
note in regular there are synonym

	\d is a synonym of [0-9] stand for digits.
	\w is a synonym of [A-Za-z0-9_] stand for word.
	\s is a synonym of [ \t\r\n] stand for whitespace character.
	\b is a synonym of opposite of \w stand for word boundary. Anything that is not a word is a word boundary
	
last step def become

	@Given("I have deposited \\$(\\d*) in my Account")
	
or better

	@Given("I have deposited \\$(\\d+) in my Account")

#### match plurals

use an interrogation mark

	@Given("I have (\\d+) cucumbers? in my basket")
	public void iHaveCucumbersInMyBasket(int number) {
	// TODO: code goes here
	}

#### if you don't want arguments but want to mach merge wording step in one unique java step

use ?:

	@When("I (?:visit|go to) the homepage")
	public void iVisitTheHomepage() {
	// TODO: code goes here
	}
	
this will match 

	I visit the homepage
	I go to the homepage
	
#### allways start and end your step_definition with ^ and $. 

	Otherwise you will match longer phrases.
	
### Make your feature less repetitive

#### Use a background

A background section in a feature file allows you to specify a set of steps that are common to every scenario in the file. Exemple :replace this 

	Feature: Change PIN
	Customers being issued new cards are supplied with a Personal Identification Number (PIN) that is randomly generated by the system. In order to be able to change it to something they can easily remember, customers with new bank cards need to be able to change their PIN using the ATM.

		Scenario: Change PIN successfully
		Given I have been issued a new card
		And I insert the card, entering the correct PIN
		When I choose "Change PIN" from the menu
		And I change the PIN to 9876
		Then the system should remember my PIN is now 9876
		
		Scenario: Try to change PIN to the same as before
		Given I have been issued a new card
		And I insert the card, entering the correct PIN
		When I choose "Change PIN" from the menu
		And I try to change the PIN to the original PIN number
		Then I should see a warning message
		And the system should not have changed my PIN
		
by this

	Feature: Change PIN
	Customers being issued new cards are supplied with a Personal Identification Number (PIN) that is randomly generated by the system. In order to be able to change it to something they can easily remember, customers with new bank cards need to be able to change their PIN using the ATM.

		Background:
		Given I have been issued a new card
		And I insert the card, entering the correct PIN
		And I choose "Change PIN" from the menu
	
		Scenario: Change PIN successfully
		When I change the PIN to 9876
		Then the system should remember my PIN is now 9876
		
		Scenario: Try to change PIN to the same as before
		When I try to change the PIN to the original PIN number
		Then I should see a warning message
		And the system should not have changed my PIN
		
you can also add a name and a description

	Background: Insert a newly issued card and sign in
	Whenever the bank issues new cards to customers, they are supplied with a Personal Identification Number (PIN) that is randomly generated by the system.

good practice

	If the Background is more than three or four steps long, think about splitting the feature file in two. If the new scenarios you want to add don’t fit with the existing background, consider splitting the feature.
	Avoid putting technical details such as clearing queues, starting backend services, or opening browsers in a background. StakeHolders should be able to read that. Those technical stuff goes in Tagged Hooked.
	
#### Data table

Replace if you find it too long

	Given I have a person unsatisfied, with one action registered, color blue, ... 

by 

	Given I have a person with the following description
	|satisfaction     |unsatisfied|
	|action registered|1          |
	|color            |blue       |

Now if you have several persones with many attributes Replace this

	Given a User "Michael Jackson" born on August 29, 1958
	And a User "Elvis" born on January 8, 1935
	And a User "John Lennon" born on October 9, 1940

by 

	Given these Users:
	| name | date of birth |
	| Michael Jackson | August 29, 1958 |
	| Elvis | January 8, 1935 |
	| John Lennon | October 9, 1940 |
	
Now if you have several persones with one attribute Replace this

	Given a User "Michael Jackson" 
	And a User "Elvis" 
	And a User "John Lennon"
	
by

	Given I have those users
	|Michael Jackson|
	|Elvis          |
	|John Lennon    |
	
Exemple of table diff. This test will fail if expectedTable and board are not identical and it will show you the diff.

	@Then("^the board should look like this:$")
	public void theBoardShouldLookLikeThis(DataTable expectedTable) throws Throwable {
	expectedTable.diff(board);
	}
	
you can read more on Gherkins DataTable online.

#### Outline Scenarios

if you have several scenarios that follow exactly the same pattern of steps, just with different input values or expected outcomes. Replace.

	Scenario: Withdraw fixed amount of $50
	Given I have $500 in my account
	When I choose to withdraw the fixed amount of $50
	Then I should receive $50 cash
	And the balance of my account should be $450

	Scenario: Withdraw fixed amount of $100
	Given I have $500 in my account
	When I choose to withdraw the fixed amount of $100
	Then I should receive $100 cash
	And the balance of my account should be $400

	Scenario: Withdraw fixed amount of $200
	Given I have $500 in my account
	When I choose to withdraw the fixed amount of $200
	Then I should receive $200 cash
	And the balance of my account should be $300
	
by

	Feature: Withdraw Fixed Amount
	The "Withdraw Cash" menu contains several fixed amounts to speed up transactions for users.

	Scenario Outline: Withdraw fixed amount
	Given I have <Balance> in my account
	When I choose to withdraw the fixed amount of <Withdrawal>
	Then I should receive <Received> cash
	And the balance of my account should be <Remaining>

	Examples:
	| Balance | Withdrawal | Received | Remaining |
	| $500 | $50 | $50 | $450 |
	| $500 | $100 | $100 | $400 |
	| $500 | $200 | $200 | $300 |
	
Notes : 

	this you create 3 scenario differents when we will execute it. 
	placeholders between <> correspnd to column names in order
	now we see missing edge scenarios like 	| $10 | $200 |what to do ?| what to do ? | we will ask stakesholders for that.
	
And here we are. All possible scenarios shown at once.

	Scenario Outline: Withdraw fixed amount
	Given I have <Balance> in my account
	When I choose to withdraw the fixed amount of <Withdrawal>
	Then I should <Outcome>
	And the balance of my account should be <Remaining>
	
	Examples:
	| Balance | Withdrawal | Remaining | Outcome |
	| $500 | $50 | $450 | receive $50 cash |
	| $500 | $100 | $400 | receive $100 cash |
	| $500 | $200 | $300 | receive $200 cash |
	| $100 | $200 | $100 | see an error message |
	
Good practice

	make your examples illustrative or representative than exhaustive
	long list exhausted tests are hard to read and your tests will take longer to run, slow down the feedback loop, making the whole team less productive as a result.
	if you operates in a safety-critical environment, then yes by all means put exhausted tests in.
	But remember that you’ll never be able to prove there are no bugs. As logicians say, absence of proof is not proof of absence
	If you move too much of the text of a step into the examples table, it can be very hard to read the flow of the scenario. Remember your goal is readability,
	
use several examples if that makes it more readible

	Feature: Account Creation
		Scenario Outline: Password validation
		Given I try to create an account with password "<Password>"
		Then I should see that the password is <Valid or Invalid>
		
		Examples: Too Short
		Passwords are invalid if less than 4 characters
		| Password | Valid or Invalid |
		| abc | invalid |
		| ab1 | invalid |
		
		Examples: Letters and Numbers
		Passwords need both letters and numbers to be valid
		| Password | Valid or Invalid |
		| abc1 | valid |
		| abcd | invalid |
		| abcd1 | valid |

use high-level step if that makes it more readible. Replace

	Scenario: Withdraw fixed amount of $50
	Given I have $500 in my account
	And I have pushed my card into the slot
	And I enter my PIN
	And I press "OK"
	When I choose to withdraw the fixed amount of $50
	Then I should receive $50 cash
	And the balance of my account should be $450
	
by

	Given I have authenticated with the correct PIN
	When I choose to withdraw the fixed amount of $50
	Then I should receive $50 cash
	And the balance of my account should be $450
	
	@Given("^I have authenticated with the correct PIN$")
	public void iHaveAuthenticatedWithTheCorrectPIN() throws Throwable {
	authenticateWithPIN();
	}

and authenticateWithPIN() 

	will make exactly the same call as the 3 step we removed.
	
#### Doc Strings

Doc strings allow you to specify a larger piece of text than you could fit on a single line. For example, if you need to describe the precise content of an email message, you could do it like this:

	Scenario: Ban Unscrupulous Users
	When I behave unscrupulously
	Then I should receive an email containing:
	"""
	Dear Sir,
	Your account privileges have been revoked due to your unscrupulous behavior.
	Sincerely,
	The Management
	"""
	And my account should be locked
	
#### Organise your feature with tags and subfolders

	You tag a scenario by putting a word prefixed with the @ character on the line before the Scenario keyword, like this:
		@widgets
		Scenario: Generate report
		
	If you tag a feature, all the scenarios will inherit the tag
	
	
### Keep your cucumbers sweet

Avoid Incidental details (they are just noise)

	Scenario: Check inbox
	Given a User "Dave" with password "password"
	And a User "Sue" with password "secret"
	And an email to "Dave" from "Sue"
	When I sign in as "Dave" with password "password"
	Then I should see 1 email from "Sue" in my inbox
	
use that instead

	Scenario: Check inbox
	Given a User "Dave"
	And a User "Sue"
	And an email to "Dave" from "Sue"
	When I sign in as "Dave"
	Then I should see 1 email from "Sue" in my inbox
	

Avoid Imperative style (how to) like this. It is stakeholder boring and too low level. It will cause duplications and stuff to move in background.

	Scenario: Redirect user to originally requested page after logging in
	Given a User "dave" exists with password "secret"
	And I am not logged in
	When I navigate to the home page
	Then I am redirected to the login form
	When I fill in "Username" with "dave"
	And I fill in "Password" with "secret"
	And I press "Login"
	Then I should be on the home page

Use declarative style (what it should be or do)

	Scenario: Redirect user to originally requested page after logging in
	Given I am an unauthenticated User
	When I attempt to view some restricted content
	Then I am shown a login form
	When I authenticate with valid credentials
	Then I should be shown the restricted content
	
Advice : 

	Try to avoid being guided by existing step definitions when you write your scenarios and just write down exactly what you want to happen, in plain English
	If by moving lower you get a duplication, raise your level of abstraction
	
	
Avoid leaky scenario = keep scenario independent

	if test 1 move system from state A to state B, and then test 2 start in state B. Don't call test1 to ensure test2 will start in the correct state. Because if you happen to change test1, then test2 will break. 
	Any dependency between test is bad idea. It can result in a chain depency andthen a chain fail.
	Team that does test maintenance only when it goes bad, always fails, teams that are able to give time to the important things "keep you tests healthy" + "keep your relationships healthy" always wins.
	Think of the Toyota example "Stop the Line at Toyota" p110
	
Use builder to create your initial test. (p104)

	Instead of creating all objects individually in your step definition code, for readability use builder.
	Separate the construction of a complex object from its representation so that the same construction process can create different representations. 
	
Use the correct thread to avoid flickering scenario

	A scenario pass and fail intermittently. 
	If your When step cause the system to start some work in the background, and if this background task happens to finish before Cucumber runs your Then step, then scenario will pass. But if Cucumber wins the race and the Then step executes before the background task is finished, the scenario will fail.
	To void this be aware of the threads.
	
## A working example

### The step definition should be readable

Replace this

	class Account {
		public Account(int openingBalance) {
		}
	}


by this

	class Account {
		public void deposit(int amount) {
		}
	}
	
Advices : 

	When creating test at first, dont implement your model methods. Think What it should do instead of how. 
	For implementation methods return 0 or null or the exact amount needed, that way you obtain a model skeleton, and the test pass to the next step of the scenario.
	Using assertion for steps given and when is good practice.
	Avoid instance variable to share state between steps, use a helper class or better dependy injection.
	Why do we hate instance variables ? The problem with instance variables is that if you don’t set them they just stay null. We hate nulls, because if someone were to later use the second step definition in another scenario that hadn’t already set the instance variable, a null would get passed.
	Dependency injection : shows dependence clearly by passing the object it depends on in its contructor.
	Don't create/init object in the step. Do it in the helper class.
	Move domain classes in well named package here nicebank
	KnowsTheDomain in its own class in support package
	one step definition file per entity
	but we want only one KnowsTheDomain instance. Use dependency injection Luke!
	
	
Avoid null by using helper methods

	private Account myAccount;

	public Account getMyAccount() {
	if (myAccount == null){
	myAccount = new Account();
	}
	return myAccount;
	}
	
# Make use of Hooks

Hooks are methods that run before or after each scenario. To test them, add a file src/test/java/hooks/SomeTestHooks.java that looks like this:

	public class SomeTestHooks {
		@Before
		public void beforeCallingScenario() {
			System.out.println("*********** About to start the scenario.");
		}
		@After
		public void afterRunningScenario(Scenario scenario) {
			System.out.println("*********** Just finished running scenario: "+ scenario.getStatus());
		}
	}
	
Hooks are like the SetUp and TearDown methods, meaning they run for every scenario in your features. If you want them to run for just certain scenarios, you need to tag those scenarios and then use a tagged hook. Example : replace this 

	Feature: Delete Widgets
		Background:
		Given I am logged in as an administrator

By this ... It is equivalent.

	@admin
	Feature: Delete Widgets

	@Before("@admin")
	public void logInAsAdmin() {
		// Log in as admin user
	}

or by this ... and only scenario with admin tag will start.


	Feature: Delete Widgets
	
	@admin
	Scenario : add a table
	

	@Before("@admin")
	public void logInAsAdmin() {
		// Log in as admin user
	}

Sometimes it’s important to be able to specify the exact order that your hooks run in. The @Before and @After annotations have an order parameter that you can set. The default value is 10000 for any hook that doesn’t have a specific order set.

	@Before( order=5 )
	public void oneHook() {
		// ....
	}
	@After( order = 200 )
	public void anotherHook() {
		// ...
	}

Cucumber runs @Before hooks from low to high. A @Before hook with an order of 10 will run before one with an order of 20. @After hooks run in the opposite direction—from high to low—so an @After hook with an order of 20 will run before one with an order of 10. If you need to use order on a tagged hook, you have to use the value parameter:
	@Before( value="myTag", order=5 )
	public void oneHook() {
		// ....
	}

Hook can accept a single argument that represents the scenario. For example, we can ask a scenario for its status:

	@After
	public void afterCallingScenario(Scenario scenario) {
		System.out.println("The scenario completed with a status of "+ scenario.getStatus());
	}

	
Get user interface screenshot when a scenario is failing

	public class WebdriverHooks {

		@After
		public void finish(Scenario scenario) {
			try {
				byte[] screenshot =
						helper.getWebDriver().getScreenshotAs(OutputType.BYTES);

				//embed method is a cucumber method that is able to save an image
				scenario.embed(screenshot, "image/png");
			} catch (WebDriverException somePlatformsDontSupportScreenshots) {
				System.err.println(somePlatformsDontSupportScreenshots.getMessage());
			} finally {
				helper.getWebDriver().close();
			}
		}
	}

	
Moving to asynchronous architecture. Up to now, the balance was updated during the Account method call to credit or debit, means that we can be certain the balance will have been updated by the time Cucumber checks the account balance in the final Then step of our scenario. To avoid flickering scenario, you have to wait. There is several way to do this correctly : 

	Synchronizing by Listening
	Synchronization by Sampling
	
Synchronizing by Listening: 

	Listening for events is the fastest and most reliable way to synchronize your tests with an asynchronous system. 
	For this technique to work, the system under test has to be designed to fire events when certain things happen. tests subscribe to these events and can use them to create synchronization points in the scenario.
	
Synchronization by Sampling

	When it isn’t possible to listen to events from the system, the next best option is to repeatedly poll the system for the state change you’re expecting. If it doesn’t appear within a certain timeout, you give up and fail the test.
	This approach works in most circumstances, but you need to take care, especially when the outcome you’re looking for at the end of the scenario looks just the same as at an earlier time in the scenario.

# Database

	Connect your code easily to the db using ORM like ormlite or realm
		http://ormlite.com/sqlite_java_android_orm.shtml
		https://realm.io/docs/java/latest/#queries
	Manage your database schema using Liquibase
	
Common leaky scenario and solution

	insert : first test pass, second fail
	solution :cleaning with database transactions
	solution :cleaning with database truncations
	
cleaning with database transactions

	Before the scenario starts, we start a new database transaction in a @Before hook. Then, our step definitions and application insert and modify data in the database. However, since this is happening in an uncommitted transaction, nothing gets changed in the database until the transaction is committed. Then, when the scenario is over (in an @After hook), we do the opposite. We roll the transaction back! All the data that was modified during the scenario gets lost, and the database is back in its original state. 	
	Downside : transactions is that they are isolated. This means that whatever database activity happens inside a transaction cannot be seen by any other database connections. And we have minimum 2 connections here. The first database connection is made by the process that runs Cucumber. The second database connection is made by the TransactionProcessor. since the database transaction that Cucumber started never gets committed, the TransactionProcessor can’t see the account we created in our first step.
	Ccl° : when the application has a different database connection than Cucumber, we cannot use transactions to clean the database. We have to use truncations.
	
cleaning with database truncations

	Truncating the database before each scenario is a brute-force technique, and the main drawback is that it’s generally slower than rolling back a transaction. This is why the transactional approach is typically preferable if you can get away with it.
	Truncating the database in an @After hook works but :
		if the process gets killed before it has time to clean up in the @After hook, it might cause the next test run to fail.
		when a scenario fails it might not be evident why it failed, and having the ability to peek inside the database as a postmortem often helps us understand why a scenario is failing.
		hence prefer @before
		
# Dependency injection

The two common ways that DI containers inject objects are :
	constructor injection
	field injection
	
How to use it, create the stepsdefinitions classes that needs DI by adding a constructer with the DI container as parameter 

    public AccountSteps(KnowsTheDomain helper) {
        this.helper = helper;
    }
	
Note : 

	we never call the new parameter. 
	The picocontainer call the new at the begining of each scenario, inject the created KnowsTheDomain in each steps of the scenario.
	Hence, each scenario start with a new "KnowsTheDomain"
	
Without pico container we could have achieve the same by

	creating a static instance of KnowsTheDomain, but because that instance would then be shared by all our scenarios, we would need to 
	reset our KnowsTheDomain in a @Before hook of each scenario.
	
We also need to make sure that our original, successful withdrawal scenario keeps working. We could do this by adding an extra step to it to load the ATM, but this would be an incidental detail.

	public TestCashSlot() {
		super.load(1000);
	}

	
# Keeping Your Features Fast

how ?

	run fewer scenarios. Tag your scenarios, and you can choose a subset of the scenarios to run, covering the area that you’re currently working on.
	Larger subsets might run in continuous integration (CI) server, at scheduled intervals (such as overnight or weekly)
	Possible Classifications tags p 246 (The cucumber for java book)
	
tags 

	Tags on the feature apply to every scenario and scenario outline within the feature. 
	Tags on a scenario outline apply to every example that is associated with it (in addition to any tags applied to the feature). 
	And tags on an example block apply to all examples in that block (in addition to any tags applied to the feature and the scenario outline).
	
	
	
# Tests

for each function you will create you will have to describe

	where to get the object or function
	the expected behaviors given correct data type
	the failing behaviors given correct data type
	the behavior when passing string instead of number, is it allowed ?
	what if you give float instead of integer


in javascript Jasmine they talk about

src = code sources
specs = test
specRunner = features file

in specs the keywords 
describe = feature = suite = group of related specs
it = scenario
expect = step = test = the test function has only one fonction, taken from the source

Write your tests first, this method of doing is called the red green refactor cycle. Means At first all your tests will fails and be red.
With asynchronous methods, you can put your test in the callback of the method, because this callback run within the scope of an application. There is a special method for test that can start in place of the callback. Keyword "done"

	beforeEach(function(done))
	see : https://classroom.udacity.com/courses/ud549/lessons/3773158892/concepts/38711686150923
	
	
# Tests and Espresso, offcial links

The set of tests you need to create are : 
	
	Unit test
	Integrated test
	UI Integrated test
	Instrumented unit test/Connected unit test
	Instrumented integrated test/Connected integrated test
	UI Instrumented integrated test/UI Connected integrated test
	UI Automator Instrumented test/UI Automator Connected test
	
it's is good practice to configure the gradle to run the test an the order were test that may fail quickly are on top. This order seems appropriate to me

	Unit test
	Integrated test
	UI Integrated test
	Instrumented unit test/Connected unit test
	Instrumented integrated test/Connected integrated test
	UI Instrumented integrated test/UI Connected integrated test
	UI Automator Instrumented test/UI Automator Connected test
	
Unit test

	run on java vm
	testing generic non android related java classes or method
	uses junit	

Integrated test

	run on java vm
	test to code with mock android-sdk-api implementation. 
	uses junit for asserts
	uses Mockito for mocking non ui elements Context, Activity ...

UI Integrated test

	run on java vm
	test to code with mock android-sdk-api implementation. 
	uses junit for asserts
	uses Mockito for mocking ui elements Views, Textviews...	
	
Instrumented unit test/Connected unit test

	run on device
	testing generic non android related java classes or method
	uses AndroidJUnitRunner for asserts	

Instrumented integrated test/Connected integrated test

	run on device
	use device android sdk api for non ui elements Context, Activity ...
	uses AndroidJUnitRunner for asserts
	
UI Instrumented integrated test/UI Connected integrated test

	run on device
	use device android sdk api for ui elements Views, Textviews...
	uses AndroidJUnitRunner for asserts
	
UI Automator Instrumented test/UI Automator Connected test
	
	run on device
	use device android sdk api to turn on/off device element for example turn on or off Wifi
	uses AndroidJUnitRunner for asserts

At Google I think they use a combinaison of these frameworks

	Espresso : https://google.github.io/android-testing-support-library/docs/index.html andthe very useful https://google.github.io/android-testing-support-library/downloads/espresso-cheat-sheet-2.1.0.pdf
	Mockito
	Dagger 2
	see : https://engineering.circle.com/instrumentation-testing-with-dagger-mockito-and-espresso-f07b5f62a85b#.7h6k8lgc1
	
# Others things
Things you usually need to mock

	Fragment
	FragmentManager
	Intent
	Context
	View
	Button
	Resources
	Bundle
	ViewPropertyAnimator
	Application
	Activity
	https://github.com/dpreussler/mockitoid/blob/master/lib/src/main/java/de/jodamob/mockitoid/AndroidMocks.java
	
https://github.com/dpreussler/mockitoid
difference between mock and any
	
# Other notes about test

Espresso will wait for any UI events or AsyncTasks to finish before executing any checks

	"The centerpiece of Espresso is its ability to seamlessly synchronize all test operations with the application under test. By default, Espresso waits for UI events in the current message queue to process and default AsyncTasks to complete before it moves on to the next test operation."
	
But Espresso won't wait for any Background tasks (that are not Async) to finish before executing any checks, solutions are : 

	1. In Espresso test, call Thread.sleep until the AdView.isLoaded() return true.
	2. Create a custom idling resource for the Espresso test. 
	2. see: https://google.github.io/android-testing-support-library/docs/espresso/advanced/index.html#using-registeridlingresource-to-synchronize-with-custom-resources
	2. see (from the women I like): http://blog.sqisland.com/2015/04/espresso-custom-idling-resource.html
	Note : Solution 1 is way simpler than solution 2, but you'll probably be making your tests run much longer than needed. At the end of the day, getting it to work is a higher priority.
	
Using Cucumber with Dagger

	https://groups.google.com/forum/#!topic/cukes/Y-ynraLTaTM
	
	
From youtube

see : 

	https://www.youtube.com/watch?v=ZLyJLGkcvFM
	https://www.youtube.com/watch?v=ar28jvdoTnY
	https://github.com/discospiff/PlantPlaces15s305

1. create the POJO java plain object, with getter and setter

	class Plant{
		int size;
		getSize();
		setSize(int size);
		List<Plant> plants;
	}
	
2. create the DAO interface

	interface Plantable{
		public void save(Plant plan)
		public List<Plant> (String searchTerm)
	}
	
3. prepare interface for tests (trhows Exception)

	interface Plantable{
		public void save(Plant plan) trhows Exception;
		public List<Plant> (String searchTerm)
	}
	
4. in PlantableTest

	//test saving a populated object (should pass)
    public void testSaveValidSpecimen() {
        givenPlantIsInitializedWithData();
        whenPlanIsSaved();
        thenVerifyNoException();
    }

	//test saving object populated with nothing (should throw an exception)
    public void testInvalidSpecimenThrowsExceptionOnSave () {
        givenPlantIsNotInitialized();
        whenPlantIsSaved();
        thenVerifyException();
    }
	
see github info for details of given, when, then methods

	https://github.com/discospiff/PlantPlaces15s305
	
note the plantDAO (or specimenDAO) we use when saving of searching data should be a stub (or prototype)

5. create a prototype that make unit tests pass

    @Override
    protected void setUp() throws Exception {
        super.setUp();
        specimenDAO = new PlantDAOStub();
    }
	
	PlantDAOStub extends Plantable
	


	

# Udacian repositories

From asheshb (the mentor I like)

	https://github.com/asheshb/lol
	Example of espresso waiting for async to finish before completed
	related post : 
		https://discussions.udacity.com/t/espresso-instrumentationtest-for-asynctask-with-app-having-interstitial-ad/42113
		https://discussions.udacity.com/t/testing-asynctask-with-espresso/162527
		
		
From Daniel (favorite Udacity coach)

	https://gist.github.com/danielmai/a0ff629047c47387d3a1
	Espresso for sunshine
	related post : https://discussions.udacity.com/t/android-ui-testing-webcast/41506
	

	
From 

	https://github.com/MDuRieu/GradleFinalProject
	Build it bigger with mockito to mock Context and avoid Intrstrumental tests
	related post : 
		https://discussions.udacity.com/t/async-task-test-where-to-even-begin/159593
		https://github.com/tarun0/p4
		
		
From aac9095
	
	Nice Sunshine Retrofit Call using asynchronous call
	https://github.com/aac9095/Sunshine
	Also in my directory : C:\AndroidStudioProjects\Udacians\Aac9095\Sunshine-master
	
		



07-12 18:32:01.647 3811-3990/com.example.android.sunshine.app E/FF: com.example.android.sunshine.app.sync.SunshineSyncAdapter.onPerformSync(SunshineSyncAdapter.java:153)http://api.openweathermap.org/data/2.5/forecast/daily?q=94043&mode=json&units=metric&cnt=14&APPID=f433cde01d664c71db857ef778034ecd
	

	
Marshmallow permissions

Just like the old permission model, the new permission model requires all permissions to be included in the applications manifest. This is required regardless of what OS you are targeting or running. If you forget to register the permission in your applications manifest, the application will not be able to ask for the runtime permission later.

http://www.captechconsulting.com/blogs/runtime-permissions-best-practices-and-how-to-gracefully-handle-permission-removal


### BitmapFactory

	most commonly as circle, to create one :

		RoundedBitmapDrawable drawable = RoundedBitmapDrawableFactory.create(
			context.getRessources(), 	//to determine density
			bitmap);					//image to round
		
		drawable.setCircular(true); //to makeit a perfect circle and not an oval
		
	if using glide or picasso

		take their solution instead, for better perf	
		
		
# Standard attributes

## ?attr : Android attributtes can be referenced with the ?attr. Attribute referenced taht way can be color, textSize, Style anything, size

	android:color="?attr/colorPrimary"
	android:height="?attr/actionBarSize"
	android:height="?attr/listPreferredItemHeight"
	style="?attr/buttonBarButtonStyle"
	
## Other attributes are also available in the differents sdk res folder using the @android: tag as follow
	
	android:color="@android:color/darker_gray"
	android:drawableLeft="@android:drawable/ic_menu_share"
	 
## or without android tag

	android:padding="@dimen/abc_list_item_padding_horizontal_material"
	android:textAppearance="@style/TextAppearance.AppCompat.Headline"	

	
# Testing

What is tight coupling ?

	Tight coupling is when a group of classes are highly dependent on one another.
	This scenario arises when a class assumes too many responsibilities, or when one concern is spread over many classes rather than having its own class.
	Loose coupling is achieved by means of a design that promotes single-responsibility and separation of concerns.
	A loosely-coupled class can be consumed and tested independently of other (concrete) classes.
	Interfaces are a powerful tool to use for decoupling. Classes can communicate through interfaces rather than other concrete classes, and any class can be on the other end of that communication simply by implementing the interface.
	
### Start reading about mockito. Some good def.

[Mockito] (http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html)

#### Some defs

Dummy

	objects are passed around but never actually used. Usually they are just used to fill parameter lists.
	
Fake

	objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an in memory database is a good example).
	Create fake implementation for accessing a database, replace it with in-memory collection.
	
Stubs

	provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test. Stubs may also record information about calls, such as an email gateway stub that remembers the messages it 'sent', or maybe only how many messages it 'sent'.
	For replacing a method with code that returns a specified result. override methods to return hard-coded values, also referred to as state-based.
	Example: Your test class depends on a method Calculate() taking 5 minutes to complete. Rather than wait for 5 minutes you can replace its real implementation with stub that returns hard-coded values; taking only a small fraction of the time.
		
Mocks

	are what we are talking about here: objects pre-programmed with expectations which form a specification of the calls they are expected to receive.	
	it's A stub with an assertion that the method gets called.
	very similar to Stub but interaction-based rather than state-based. This means you don't expect from Mock to return some value, but to assume that specific order of method calls are made.
	Example: You're testing a user registration class. After calling Save, it should call SendConfirmationEmail.
	
Spy

	When you use the spy then the real methods are called (unless a method was stubbed).
	
#### Mocking with mockito

	mock
	verify
	http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#verification
		
	
#### Subbing with mockito

	mock
	when...thenReturn...
	when..thenThrow...
	doThrow...when...
	http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#stubbing
	http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#stubbing_with_exceptions
	
#### Spying with mockito

	spy
	when...thenReturn...
	when..thenThrow...
	doThrow...when...
	http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#spy
	
#### verify method

	uses the java equals function by default but you can use an argument matcher (ex:anyInt() see:http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#argument_matchers)
	can check if an action has happened
		x time exactly -> times()
		at least one time ->  atLeastOnce()
		at least x time ->  atLeast(3)
		at most x time -> atMost(5))
		never ->  never() http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#never_verification
		verify(mockedList, times(2)).add("twice");
		see : http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#exact_verification
	can check if several actions happened in order
		inOrder.verify(singleMock).add("was added first");
		http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#in_order_verification
	can be used with a timeout :http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#verification_timeout
	can replace with a "then" keyword since v1.10.0 to follow BDD principles see:http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#BDD_behavior_verification and http://site.mockito.org/mockito/docs/current/org/mockito/BDDMockito.html
		then(person).should(times(2)).ride(bike);
		then(person).should(inOrder, times(2)).ride(bike);
	
#### Dependency injection with mockito
	
	http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html#automatic_instantiation
	
	
### android:textAppearance="?android:textAppearanceLarge"

<ImageView
    android:src="@drawable/cake"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:scaleType="center"/>

 android:scaleType="centerCrop" make the image fit the height and width of the view. Qd on redimentionne l'image les proportions ne sont pas modifiées. Souvent utilisé pour les photos. Pour avoir des full-bleed images

    android:textStyle="bold"
        android:textColor="@android:color/white"
        android:textSize="36sp"
        android:fontFamily="sans-serif-light"

Layouts:

LinearLayout
RelativeLayout
FrameLayout
GridLayout


Fond vert :https://www.youtube.com/watch?v=nrSdUNeY7AM
Hands Gestures with Chroma Key


why-is-the-app-waiting-for-the-debugger-when-its-not-connected-to-computer ?

	For me, the solution is to select "None" in "Developer Options"->"Debug"->"Choose debug application", though it already has "None" selected. Seems like the device put a "need to debug" label on my app sometime before which is still there when I "Run" the app on the device using my IDE (or even launch the app manually when the device is not connected to PC), and re-select "None" removes the label. Don't know whether it's the case.
	https://stackoverflow.com/questions/2031070/why-is-the-app-waiting-for-the-debugger-when-its-not-connected-to-computer
	

	



	

	
	





	

	

	
	

	
	

