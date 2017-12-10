# Create a User-Account : 
		1. Add Service in the Manifest 
			<intent-filter><action android:name="android.accounts.AccountAuthenticator" /></intent-filter>
			<meta-data android:name="android.accounts.AccountAuthenticator" android:resource="@xml/authenticator" />  
		2. Add authenticator.xml in the xml directory 
		3. Create a Service class for the Account (ex MoviesAuthenticatorService)
		4. Create a AbstractAccountAuthenticator class (nb: Account does not exist. ex MoviesAuthenticator)
	
# Create a SyncAdapter
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
	
# Create a Service class (ex SunshineService) : 
		1. Override onCreate et onBind
		2. Add Service in the Manifest 
			<intent-filter><action android:name="android.content.SyncAdapter" /></intent-filter>
			<meta-data android:name="android.content.SyncAdapter" android:resource="@xml/syncadapter" />   // SyncAdapter info in an xml file 
		3. Add the syncadapter.xml file in the res directory