# Sign your app

This will describe you how to sign an app with android studio, so you can put it on market with confidence.

## Create a keystore with keys with android studio

A keystore is a file that contains severals keys. Usually a developper has one keystore, and create as many key as apps he owns.
Never lose your keystore. Allways keep several copies of it.
If you publish an app to Google Play and then lose the key with which you signed your app, you will not be able to publish any updates to your app, since you must always sign all versions of your app with the same key.

For the rest of the document I will consider I'm a developper, my name is elorri, and I have created 3 apps tata, toto, tutu.

### Create a keystore

Build > Generate Sign Apk... > Keystore path > Create new
Keystore path : 'C:\Keystore\keystore.jks' 			-> if the file doesn't exist, it will be created.
password : 'elorri' 								-> select your password carefully, you will keep it for a long time, and don't want anyone to break it.

That's it, if we could enter "OK" here we would be finished in creating the keystore, but android studio doesn't allows that, it force us to add at least one key.

### Add a key to the keystore

Usuallly the key will refer to an app, so if you don't have any app ready for release yet, wait until you find the necessity to get a release apk, to continue this procedure.
In our case, we have an app called tata, created by the elorri's developper compagny.

In the 'key' part, fill the fields : 

	Alias : 'tata'
	Password : 'tata_password'
	Valididy : 25								-> Your key should be valid for at least 25 years, so you can sign app updates with the same key through the lifespan of your app.

In the certificate part (You'll also want to provide all of your company information to establish authorship in the certificate): 

	first and last name : 'Elorri E'
	organisation : 'Elorri E'
	city and locality : 'Pau'
	state and province : 'France'
	country code : '33'
	
click finish.

	Your keystore is created
	Your first key is added
	it brings you back to the 'generate apk' screen, you can cancel this screen. 
	
### Add another key to the keystore

Let say you have another app you want to claim authorship. How to sign your app using the same keystore ? Go to 

	Build > Generate sign apk >keystore path>create new
	keystore path (choose an existing one):'C:\Keystore\keystore.jks'
	password (password you gave at creation) : 'elorri'
	
Now for the key part

	Alias (choose the new one) : 'toto'
	Password : 'toto_password'
	Valididy : 25			

and for the certificate part (put the same compagny info if it is the same): 

	first and last name : 'Elorri E'
	organisation : 'Elorri E'
	city and locality : 'Pau'
	state and province : 'France'
	country code : '33'

	
## Use keystore and a key to generate a sign apk (exemple for tata app)

	Build > Generate sign apk > Choose Existing (choose an existing one 'C:\Keystore\keystore.jks')
	keystore password : 'elorri'
	key alias : 'tata'
	key alias password: 'tata_password'
	
Note : 

	use this procedure to release any app update you make.
	once the keystore password is given, you can find the different alias registered by clicking the "..." button
	
## Automate the generation of apk

	if you don't want to set up the alias and password every time you want a new release, you should automate it by adding a signingConfig in the gradle.
	procedure to do so is in 'Udacity Android developpement classes' at 'Signing an apk'. I'm not sure but I think after this is done, all you need to do is select the build variant and press the green arrow, and a new apk up to date is generated.
	the down side is that keyAlias, keyPassword, keystoreFile path, keystorePassword are visible in the build gradle. To avoid that you have to use Environment variables.
	This should be verified.

## Errors you can get

I you use an existing keystore, when building your realase apk, you must provide the correct password, or you will get an error:

	Error:Execution failed for task ':app:packageFreeRelease'.
	> com.android.ide.common.signing.KeytoolException: Failed to read key toto from store "C:\AndroidStudioProjects\TieUs\app\keystore.jks": Keystore was tampered with, or password was incorrect

You also must provide the correct alias, or you will get this error

	Error:Execution failed for task ':app:packageFreeRelease'.
	> com.android.ide.common.signing.KeytoolException: Failed to read key toto from store "C:\AndroidStudioProjects\TieUs\app\keystore.jks": No key with alias 'toto' found in keystore C:\AndroidStudioProjects\TieUs\app\keystore.jks
	
You also must provide the correct alias password, or you will get this error

	Error:Execution failed for task ':app:packageFreeRelease'.
	> com.android.ide.common.signing.KeytoolException: Failed to read key elorri from store "C:\AndroidStudioProjects\TieUs\app\keystore.jks": Cannot recover key
	elorri is the correct alias, but the password I put was incorrect


