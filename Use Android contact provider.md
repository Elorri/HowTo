"The provider accommodates a wide range of data sources and tries to manage as much data as possible for each person, with the result that its organization is complex. Because of this, the provider's API includes an extensive set of contract classes and interfaces that facilitate both data retrieval and modification."

source used for this class

	https://developer.android.com/guide/topics/providers/contacts-provider.html

The contact provider contains 3 tables

	contact
	raw contact
	data
		
Each table is defined in a contract classe

	ContactsContract.Contacts (https://developer.android.com/reference/android/provider/ContactsContract.Contacts.html)
	ContactsContract.RawContacts (https://developer.android.com/reference/android/provider/ContactsContract.RawContacts.html)
	ContactsContract.Data (https://developer.android.com/reference/android/provider/ContactsContract.Data.html)
	
Each contract classes defines

	content uris
	column names
	columns values
	
the structure is as follow

	a contact a merge of several raw contacts = a contact is a list of raw contacts. It is impossible to create a new contact here using insert() will result in UnsupportedOperationException exception.
	a raw contact is a list of data, a user account and an user type. This is where you can add contacts. If an application or sync adapter creates a new raw contact that does match an existing contact, the new raw contact is aggregated to the existing contact.
	a data can be maybe things but mainly it is : emails, adresses, phone numbers
	
ContactsContract.Contacts contains subclasses that are auxiliaries and 

	used to support specific manufacturer functions
	used to support telephony applications
	used to manage provider operations
	
ContactsContract.Contacts columns are

	Contacts._ID
	Contacts.LOOKUP_KEY //Used in coùbination with CONTENT_LOOKUP_URI to retrieve a contact. Don't use the Contacts._ID because it can change during maintenance.
	Contacts.PROFILE //I'm not sure of the name here. It is used to access device user details. Constants for accessing the user profile are available in the ContactsContract.Profile class.
	
ContactsContract.RawContacts columns are

	RawContacts._ID
	RawContacts.CONTACT_ID //Refers to Contacts._ID
	RawContacts.ACCOUNT_TYPE
	RawContacts.ACCOUNT_NAME
	RawContacts.DELETED //flag if the row has yet been deleted on serveur
		
RawContacts.ACCOUNT_TYPE 
	
	must be world wide unique and is generaly used to constitute the contentprovider uri
	to read or write any field depending on it, we must have registered the account on the device (see AccountManager : https://developer.android.com/reference/android/accounts/AccountManager.html)
	to understand this better see https://developer.android.com/guide/topics/providers/contacts-provider.html "Sources of raw contacts data"
	exple : com.google, com.samsung
	
RawContacts.ACCOUNT_NAME format

	is specific to its account type. It is not necessarily an email address.
	exple : 
		emily.dickinson@gmail.com
		emilyd@gmail.com
		belle_of_amherst (Twitter account)
		
ContactsContract.RawContacts is not really a table, it is a mix of a table and a view

	RawContacts._ID contains real data
	RawContacts.ACCOUNT_TYPE contains real data
	RawContacts.DELETED contains real data
	RawContacts.ACCOUNT_NAME does not contain real data. Points to a specific data of its data list (ContactsContract.CommonDataKinds.StructuredName)
	RawContacts.DIRTY more on https://developer.android.com/guide/topics/providers/contacts-provider.html#Groups
	RawContacts.VERSION more on https://developer.android.com/guide/topics/providers/contacts-provider.html#Groups
	RawContacts.SOURCE_ID more on https://developer.android.com/guide/topics/providers/contacts-provider.html#Groups
	
the contact data list 

	is made with a list of ContactsContract.Data with an id refering to the contact Data.RAW_CONTACT_ID
	some data element of the list can be unique within a contact list, this is the case of ContactsContract.CommonDataKinds.StructuredName (see more below)
	
ContactsContract.Data columns are

	Data.RAW_CONTACT_ID		//Refers to RawContacts._ID
	Data.MIMETYPE 			//Not store here but in its child ContactsContract.CommonDataKinds
	Data.IS_PRIMARY			//If this type of data row can occur more than once for a raw contact
	Data.DATA1				//The DATA1 column is indexed. Not others. Use this column for data that will be query often. Exple to store an email adress. Google contact provider or samsung provider may have used it correctly (let's check this if some time).
	Data.DATA2
	Data.DATA3
	Data.DATA4
	Data.DATA5
	Data.DATA6
	Data.DATA7
	Data.DATA8
	Data.DATA9
	Data.DATA10
	Data.DATA11
	Data.DATA12
	Data.DATA13
	Data.DATA14
	Data.DATA15			//By convention, the column DATA15 is reserved for storing Binary Large Object (BLOB) data such as photo thumbnails
	Data.SYNC1 		//should only be used by sync adapters
	Data.SYNC2 		//should only be used by sync adapters
	Data.SYNC3 		//should only be used by sync adapters
	Data.SYNC4 		//should only be used by sync adapters
	Data.DATA_VERSION
		
Those columns can be divided into 4 categories
 
	Descriptive column names : they have the same meaning regardless of the type of data in the row,
	Generic column names : have different meanings depending on the type of data.
	
	Type-specific column name classes
	
Descriptive column names are

	Data.RAW_CONTACT_ID		
	Data.MIMETYPE 	
	Data.IS_PRIMARY		
	
Generic column names are 

	Data.DATA1
	Data.DATA2
	Data.DATA3
	Data.DATA4
	Data.DATA5
	Data.DATA6
	Data.DATA7
	Data.DATA8
	Data.DATA9
	Data.DATA10
	Data.DATA11
	Data.DATA12
	Data.DATA13
	Data.DATA14
	Data.DATA15
	Data.SYNC1
	Data.SYNC2 
	Data.SYNC3 	
	Data.SYNC4 	

Now If I want to store the differents addresses of a contact along with a field specifying if the adresse is close to the beach or not, and a photo of the house.

	I will store in mimetype a mimetype corresponding to email
	I will store the adresse in Data1 because it is indexed
	I will store the boolean in Data2
	I will store the photo in data15
	
Example 2 : store the phone numbers along with a label

	I will store in mimetype a mimetype corresponding to phone
	phone number will be in data1
	label in data2
	
Example 3 : store a contact recipes

	I will store in mimetype a mimetype corresponding to recipe
	recipe name will be in data1
	ingredient1 in data2
	ingredient2 in data3
	if not enough field to store this data using phone contact provider + google contact serveur, I will need to create my own contact provider with more fields + system to store the data on serveur
	
Type-specific column names

	As we can see data1, data2, etc are used to store and retrieve values and those name are not really explicit. To make programming explicit 
	android provide classes that match the column datas (data1, data2..) with the type of data that fit best in them (adresse, email adress, recipe name for data1, ingredient for data2)
	Type-specific column names are specified in  ContactsContract.CommonDataKinds classes.
	
Example ContactsContract.CommonDataKinds.Email

	Mimetype = Email.CONTENT_ITEM_TYPE
	Data1 = Adress
	Data2 = Type
	Data3 = Label
	...
	calling ContactsContract.CommonDataKinds.Email.Adress will return data1
	
	
ContactsContract.Data 
	
	does not contains all the data
	is a common class to specify columns that exist withing all ContactsContract.Data 
	
ContactsContract.Data childs have

	ContactsContract.Data columns, but not necessarly with the same restrictions (unique, null, not null)
	columns of their own
	
ContactsContract.Data childs have
	
	ContactsContract.CommonDataKinds.StructuredName with an unique Data.RAW_CONTACT_ID
	ContactsContract.CommonDataKinds.MIMETYPE (Note : all mimetypes stored in this table are open source)
	ContactsContract.CommonDataKinds.Photo
	ContactsContract.CommonDataKinds.Email
	ContactsContract.CommonDataKinds.StructuredPostal
	ContactsContract.CommonDataKinds.GroupMembership
	
Others important tables

	ContactsContract.Profile //Get info about the device user
	ContactsContract.Settings //Get metadata
	ContactsContract.SyncState //Get metadata
	ContactsContract.Groups
	
Entities

	are used to query easily
	act like database joins between tables.
	can display all the information for a person, by retrieving all the ContactsContract.RawContacts rows for a single ContactsContract.
	can display all the information for a person, by retrieving all the all the ContactsContract.CommonDataKinds.Email rows for a single ContactsContract.RawContacts row
	see the example https://developer.android.com/guide/topics/providers/contacts-provider.html#Groups
	

Syncadapters, AccountTypes and Webservices

	Syncadapters needs an AccountType to push and pull data from a webservice.
	
Webservices can be

	com.samsung
	com.google
	com.facebook
	
AccountTypes can be

	Identifies a service in which the user has stored data. Most of the time, the user has to authenticate with the service. 
	com.samsung
	com.google
	com.facebook
	
One AccountTypes can have multiple names, example

	emily.dickinson@gmail.com
	emilyd@gmail.com
	
applyBatch and ContentProviderOperation

	when inserted data into a contentProvider we used to use insertInBulk. This method is efficient but not able to send data to the server.
	using applyBatch along with ContentProviderOperation will sync the data to the server
	more info here : https://developer.android.com/guide/topics/providers/contacts-provider.html#Groups
	note an example of this can be found in udacity XyzReaderBefore project or in my own xyzreader https://github.com/Elorri/XyzReader/blob/910ee4050ec1bfd7f05ba9b8d94ee2885c96e5e4/app/src/main/java/com/elorri/android/xyzreader/data/UpdaterService.java
	je ne suis pas sure de tout ce que j'ai mis au dessus. Mais en tout cas l'interet cest de pouvoir regrouper les operations (et pas que l'insert (car l'insert peut être regroupé pvia le bulkinsert mais pas les autres (il n'y a pas de bulkupdate par exemple))
	voir aussi yields.
	
old way vs applyBatch

	ContentValues groupValues;
	create group()
	{
	 ContentResolver cr = this.getContentResolver();
	 groupValues = new ContentValues();
	 groupValues.put(ContactsContract.Groups.TITLE, "MyContactGroup");
	 cr.insert(ContactsContract.Groups.CONTENT_URI, groupValues);
	}
	
best way

 private void createGroup() {
    ArrayList<ContentProviderOperation> ops = new ArrayList<ContentProviderOperation>();

    ops.add(ContentProviderOperation
            .newInsert(ContactsContract.Groups.CONTENT_URI)
            .withValue(ContactsContract.Groups.TITLE, "SRI").build());
		try {
			getContentResolver().applyBatch(ContactsContract.AUTHORITY, ops);
		} catch (Exception e) {
			Log.e("Error", e.toString());
		}
}


More on  LOOKUP_KEY and CONTENT_LOOKUP_URI

	Should be use as a permanent link to a contact
	Because the Contacts Provider maintains contacts automatically, it may change a contact row's _ID value in response to an aggregation or sync. Even If this happens, the content URI CONTENT_LOOKUP_URI combined with contact's LOOKUP_KEY will still point to the contact row
	This URI should always be followed by a "/" and the contact's LOOKUP_KEY. It can optionally also have a "/" and last known contact ID appended after that. This "complete" format is an important optimization and is highly recommended. As long as the contact's row ID remains the same, this URI is equivalent to CONTENT_URI. If the contact's row ID changes as a result of a sync or aggregation, this URI will look up the contact using indirect information (sync IDs or constituent raw contacts). Lookup key should be appended unencoded - it is stored in the encoded form, ready for use in a URI.
	exple : content://com.android.contacts/contacts/lookup/298i19.3552i2e/18
	
Notes

	To see the contact provider database it would be nice to root the device.
	This tool looks good but is only free for 30 days. 
	https://www.oneclickroot.com/end-user-license-agreement/
	https://drfone.wondershare.com/root/one-click-root.html 
	https://www.tutoriels-android.com/2015/01/rooter-son-galaxy-s5-mini-g800f-avec-cf-auto-root.html
	C'est celui que j'ai installé mais on est obligé de s'enregistrer : F:\Mes Documents\Programmes\Root your phone\OneClickRoot.exe
	
	
Accessing the content provider indireclty via intents

	The intent starts the device's contacts application UI
	no permission READ or WRITE is needed
	
intents can do the following operations
	
	Pick a contact from a list and have it returned to your app for further work.
	Edit an existing contact's data.
	Insert a new raw contact for any of their accounts.
	Insert a new raw contact for any of their accounts.
	Delete a contact or contacts data.
	
More on this here

	https://developer.android.com/guide/topics/providers/contacts-provider.html
	Retrieval and modification with intents
	
Rules to avoid problems

	always add a  ContactsContract.CommonDataKinds.StructuredName  Data in the data list of your new raw_contact
	allways gives a raw_contact_id to the data any data row you insert
	
Create your own mimetype in your own content provider

	cf : https://developer.android.com/guide/topics/providers/content-provider-creating.html
	sections "MIME types for tables" and "MIME types for files"
	
	
Another reason to use google as a backup server

	Getting a copy of everything you've saved to your Google Account is easy, thanks to Google Takeout. Takeout helps you create an archive of documents from Google Docs, pictures from Google Photos, messages from Gmail, bookmarks from Chrome, places in Maps, and more. You can download everything at once, or grab an archive of data from the apps you use most.
	Parfois on peut choisir le format exple json ou html, parfois. En fontion des app que j'ai installé je sais que la synchro va bien se faire. Exple : je devrais installle l'app qui gère les taches google.
	Parmis les app que je n'utilise pas il y a google fit, ou google note (keep note qu'il serai pas mal de synchoniser avec les notes de mon tel, mais étant donné qu'il n'y a pas de content provider android le content provider de l'appli keep note (s'il y en a un) est-il accessible ?)
	Les contacts se téléchargent au format csv ou vcard (pas de json). 
	Dommage que tout ne puisse pas se télécharger au format json. On peut télécharger ses stats youtube par exemple mais bien sur pas facebook.
	Cela dit dans le content provider android j'ai vu des champs facebook. (Oui dans la table attendees il y en a beaucoup (content://com.android.calendar/attendees) (content://com.android.calendar/event_entities) (content://com.android.calendar/events), cf C:\ProgrammingProjects\AndroidStudioProjects\Examples\QueryBuiltInContentProviders\providersOverviews)
	Je peux récuperer tous mes mails.
	Il y aura
	https://takeout.google.com/settings/takeout

Also : 
	
	Twitter Archive lets you download a zip with your Tweets in a .csv spreadsheet file, JSON archive, and an HTML file that lets you browse through your Tweets in a Twitter-like interface. It doesn't download your photos or direct messages, though—all you get are your plain text public Tweets.
	Facebook Archive gives you a bit more: your posts, private messages, photos, and videos. They come in a rather plain HTML file that lets you browse through posts and comments in your browser.
	
Google contact size

	Gmail used to have a limit of 10,000 contacts. For most of us, this was way more than enough, but we heard from some of you who use Gmail to communicate with more than 10,000 people. We want you to be able to store all of your contacts in a single place, so starting today, we’ve increased the limit for all Gmail users, including all those of you who use Google Apps, to 25,000 contacts.
	Also, previously an individual contact could be no larger than 32KB — big enough for most people, but not always sufficient for those who like to keep a lot of notes on individual contacts. Now, each contact may be up to 128KB in size, allowing you to store more information in the notes field.
	
Conclusion : 

	Veille a utiliser des apps available sur le web et sur le tel
	Veille à ce que le content provider du tel soit accessible. Exple si par exemple Google Keep note n'a pas de provider ne pas l'utiliser. De plus ne pas l'utiliser si je pense qu'ils vont arreter de la maintenir.
	C'est sur que tout stocker dans les contacts me parait être le plus safe car c'est sur qu'il n'arrateront pas de gérer l'appli et les syncho serveur/client.
	
Ceci est confirmé par ce qu'on peut lire dans ce google blog

	https://android-developers.googleblog.com/2010/05/be-careful-with-content-providers.html
	there are more Content Providers in the system than are documented in that package, and while you can use them, you probably shouldn’t. They’re there because some of the Google-provided apps use them internally to access their own data resources.
	(By the way, searching the source tree like this is an excellent idea, something that probably every serious developer does regularly. Not 100% sure of the best way to write code to display a record from the Contacts database? Go ahead, have a look at how the built-in app does it; even better, steal some code; it’s perfectly legal.)
	For example, there’s one inside the built-in Messaging (A.K.A. texting or SMS) app that it uses to display and search your history. Just because it’s there doesn’t mean you should use it. The Android team isn’t promising that it’ll be the same in the next release or even that it’ll be there in the next release.
	It’s worse than that; someone could ship an Android device based on the current SDK that follows all the rules but has its own enhanced messaging application that doesn’t happen to have such a Content Provider. Your app will break on such a device and it’ll be your fault.
	So, go ahead and look at the undocumented Content Providers; the code is full of good ideas to learn from. But don’t use them. And if you do, when bad things happen you’re pretty well on your own.
	
Ceci dit 

	je vois mal comment lire la liste de messages envoyés ou la liste de contact sans utiliser le built-in contact provider.
	
Ma conclusion

	utilise uniquement les content provider qui ont de la doc
	utilise les données des content providers qui évolueront peut etre mais seront toujours là. A ce moment tu seras peut être obligée de mettre à jour ton appli pour qu'elle récupère les données.
	

	

	 
	






	
	

		
