# Trial and errors

ajout features dans assets
ajout calculatorActivity
ajout calculatorActivitySteps
ajout Instrumentation
ajout somedependency
dans le gradle : Instrumentation runner et librairie cucumber

it's impossible to run the edit configuration popup open

comme je peux le constater le nom de ma classe est erronée

cucumber.cukeulator.test.Instrumentation doit être changé par

monpackage. Instrumentation


Error:Execution failed for task ':app:transformResourcesWithMergeJavaResForDebugAndroidTest'.
> com.android.build.api.transform.TransformException: com.android.builder.packaging.DuplicateFileException: Duplicate files copied in APK META-INF/maven/com.google.guava/guava/pom.properties
	File1: C:\Program Files\Android\Android Studio\gradle\m2repository\com\google\guava\guava\17.0\guava-17.0.jar
	File2: C:\ProgrammingProjects\AndroidStudioProjects\Examples\CukeulatorCopie\app\build\intermediates\exploded-aar\com.android.support.test.espresso\espresso-core\2.2.2\jars\classes.jar
	
	
Ajout de ... en dessous defaultConfig dans le gradle


    packagingOptions {
        exclude 'LICENSE.txt'
        pickFirst('META-INF/maven/com.google.guava/guava/pom.xml')
        pickFirst('META-INF/maven/com.google.guava/guava/pom.properties')
    }
	

Run it again and le fameux empty test suite. Voilà ce que j'ai.

	Testing started at 21:14 ...

	12/08 21:14:44: Launching CalculatorActivitySt...
	$ adb push C:\ProgrammingProjects\AndroidStudioProjects\Examples\CukeulatorCopie\app\build\outputs\apk\app-debug.apk /data/local/tmp/com.elorri.android.myapplication2
	$ adb shell pm install -r "/data/local/tmp/com.elorri.android.myapplication2"
		pkg: /data/local/tmp/com.elorri.android.myapplication2
	Success


	$ adb push C:\ProgrammingProjects\AndroidStudioProjects\Examples\CukeulatorCopie\app\build\outputs\apk\app-debug-androidTest-unaligned.apk /data/local/tmp/com.elorri.android.myapplication2.test
	$ adb shell pm install -r "/data/local/tmp/com.elorri.android.myapplication2.test"
		pkg: /data/local/tmp/com.elorri.android.myapplication2.test
	Success


	Running tests

	$ adb shell am instrument -w -r   -e debug false -e class com.elorri.android.myapplication2.CalculatorActivitySteps com.elorri.android.myapplication2.test/com.elorri.android.myapplication2.Instrumentation
	Client not ready yet..Test running started
	Test running failed: Unable to find instrumentation info for: ComponentInfo{com.elorri.android.myapplication2.test/com.elorri.android.myapplication2.Instrumentation}
	Empty test suite.
	

Voilà ce que j'aurai du avoir 

	Testing started at 19:12 ...

	12/08 19:12:42: Launching CalculatorActivitySt...
	$ adb push C:\ProgrammingProjects\AndroidStudioProjects\Examples\Cukeulator\app\build\outputs\apk\app-debug.apk /data/local/tmp/cucumber.cukeulator
	$ adb shell pm install -r "/data/local/tmp/cucumber.cukeulator"
		pkg: /data/local/tmp/cucumber.cukeulator
	Success


	$ adb push C:\ProgrammingProjects\AndroidStudioProjects\Examples\Cukeulator\app\build\outputs\apk\app-debug-androidTest-unaligned.apk /data/local/tmp/cucumber.cukeulator.test
	$ adb shell pm install -r "/data/local/tmp/cucumber.cukeulator.test"
		pkg: /data/local/tmp/cucumber.cukeulator.test
	Success


	Running tests

	$ adb shell am instrument -w -r   -e debug false -e class cucumber.cukeulator.test.CalculatorActivitySteps cucumber.cukeulator.test/cucumber.cukeulator.test.Instrumentation
	Client not ready yet..Test running started

On peut voir 2 choses

	la copie de l'apk de l'appli se fait dans /data/local/tmp/com.elorri.android.myapplication2
	la copie de l'apk de test se fait dans /data/local/tmp/com.elorri.android.myapplication2.test
	le lieu de copie est définie par cucumber je suppose. 
	Or je n'ai pas de package qui s'appelle com.elorri.android.myapplication2.test
	
Let's make sure mes test se font dans un package test. Nous revoila case départ. L'edit configuration s'ouvre. il faut changer

	com.elorri.android.myapplication2.CalculatorActivitySteps
	com.elorri.android.myapplication2.Instrumentation
	
par

	com.elorri.android.myapplication2.test.CalculatorActivitySteps
	com.elorri.android.myapplication2.test.Instrumentation
	
Empty test suite again. Il n'est même pas sur que le fait d'avoir ajouté le package test ai eu un impact. On fait un diff de la version qui marche avec celle qui marche pas

	https://github.com/Elorri/CukeulatorCopie/compare/2c4585b6127a00aae336b468f1a5ed6e8c314543...4f2ccd666a1463993d56ec1aca540cc7ec5186fa
	
On remarque ... n'a pas été modifié

	testInstrumentationRunner "cucumber.cukeulator.test.Instrumentation"
	
modifions le 

	testInstrumentationRunner "com.elorri.android.myapplication2.test.Instrumentation"
	Tadam ça marche. 
	
Mais juste pour être sur que le .test package est nécessaire enlevons le.

	Empty test suite.
	Il faut bien un package .test
	
Remettons le

	Ca marche !!!
	
Updatons android studio à la version 3.1, la dialogue Edit configuration demandant ou est le androidtestRunner ne devrait pas apparaitre est-ce que pour autant ça marchera ??

	La version qui marchait marche sur la nouvelle version d'android studio
	
On enleve le package test.

	Effectivement on ne peut pas lancer l'app, mais pas de dialogue Edit configuration.
	A la place un genre de toast rouge s'affiche en bas.
	Que faire ?
	
Aller dans 

	Edit configuration > General 
	replacer com.elorri.android.myapplication2.test.CalculatorActivitySteps
	par com.elorri.android.myapplication2.CalculatorActivitySteps
	Bizarre nullpart il y a le lien vers com.elorri.android.myapplication2.test.Instrumentation il doit le reconnaitre tout seul ?
	
Lancer l'appli

	Empty test suite on s'en doutait
	
Remettre le .test

	toujours pas d'Edit Config. Allons s'y nous m^me
	remplacons par com.elorri.android.myapplication2.test.CalculatorActivitySteps
	
Try again 

	Ca marche on s'en doutait. Youhou again.
	
# En résumé




Don't forget to put the 'Cucumber extra options' in the 'Edit configatrion run properties' in android studio??
	

	
	