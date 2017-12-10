In the main activity or wherever you want add

	sendNotification();
	
Now add ... This will send a notif to the phone and the wearable. When clicked the phone open the url with the adequat app.

    private void sendNotification() {
        Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://developer.android.com/reference/android/app/Notification.html"));
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
        builder
                .setSmallIcon(R.drawable.ic_plusone_small_off_client) //set the small top icon
                .setContentIntent(pendingIntent) //set the intent
                .setAutoCancel(true) //make the notification automatically disappear when it's clicked on
                .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                .setContentTitle("GoUbiquitouSample")
                .setContentText("Time to learn about notifications!")
                .setSubText("Tap to view documentation about notifications.");
        Notification notification = builder.build();
        
        //NotificationManager notificationManager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);	//for older devices	
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
        notificationManager.notify(NOTIFICATION_ID, notification);
    }
	
If you need several differents actions you can add buttons in the notification as follow. Note : the notification screen should be completely empty of others notifs to see the buttons showing up. If there are others notifs, buttons are hidden, to see them you must tap the notification with two fingers and swipe down. On a wearable, the action appears as a large button when the user swipes the notification to the left. Those next lines will show act1, act2, act3 button on phone and wearable.

  public void sendNotification(View view) {
        Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://developer.android.com/reference/android/app/Notification.html"));
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
        builder
                .setSmallIcon(R.drawable.ic_plusone_small_off_client) //set the small top icon
                .setContentIntent(pendingIntent) //set the intent
                .setAutoCancel(true) //make the notification automatically disappear when it's clicked on
                .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                .setContentTitle("GoUbiquitousSample")
                .setContentText("Time to learn about notifications!")
                .setSubText("Tap to view documentation about notifications.")
                .addAction(R.drawable.ic_plusone_small_off_client, "act1", pendingIntent)
                .addAction(R.drawable.ic_plusone_small_off_client, "act2", pendingIntent)
                .addAction(R.drawable.ic_plusone_small_off_client, "act3", pendingIntent);
        Notification notification = builder.build();

        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
        notificationManager.notify(NOTIFICATION_ID, notification);
    }
	
Note : the U8 smartwatch does not shows actions unfortunatly. See answer here.

	https://disqus.com/home/discussion/abidibo/how_to_get_the_best_of_your_u8_smartwatch/oldest/

	Xavier Groleau • 10 months ago
	Does actionnable notifications work(button in notifications to do actions) ? Can you use the mic of the watch to do voice commads? If so, or if there is any alternatives, those cheap chinese watches have an incredible potential.

	abidibo Mod  Xavier Groleau • 7 months ago
	No actionable notifications (on the watch side), and no voice command unfortunately
	
Seems we can use tasker to respond see

	http://www.abidibo.net/blog/2015/04/01/how-get-best-your-u8-smartwatch/
	
Those next lines will show act1, act2, act3 button on phone but only one act4 button on watch.

    public void sendNotification(View view) {
        Intent intent = new Intent(Intent.ACTION_VIEW,
                Uri.parse("http://developer.android.com/reference/android/app/Notification.html"));
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);

        NotificationCompat.Action action = new NotificationCompat.Action.Builder(
                R.drawable.ic_plusone_small_off_client, "act4", pendingIntent).build();

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
        builder
                .setSmallIcon(R.drawable.ic_plusone_small_off_client) //set the small top icon
                .setContentIntent(pendingIntent) //set the intent
                .setAutoCancel(true) //make the notification automatically disappear when it's clicked on
                .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                .setContentTitle("GoUbiquitousSample")
                .setContentText("Time to learn about notifications!")
                .setSubText("Tap to view documentation about notifications.")
                .addAction(R.drawable.ic_plusone_small_off_client, "act1", pendingIntent)
                .addAction(R.drawable.ic_plusone_small_off_client, "act2", pendingIntent)
                .addAction(R.drawable.ic_plusone_small_off_client, "act3", pendingIntent)
                .extend(new WearableExtender().addAction(action));
        Notification notification = builder.build();

        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
        notificationManager.notify(NOTIFICATION_ID, notification);
    }
	
Add a BigTextStyle notification to show more infos

   public void sendNotification(View view) {
        Intent intent = new Intent(Intent.ACTION_VIEW,
                Uri.parse("http://developer.android.com/reference/android/app/Notification.html"));
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);

        BigTextStyle bigTextStyle = (new NotificationCompat.BigTextStyle()).bigText("More infos");

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
        builder
                .setSmallIcon(R.drawable.ic_plusone_small_off_client) //set the small top icon
                .setContentIntent(pendingIntent) //set the intent
                .setAutoCancel(true) //make the notification automatically disappear when it's clicked on
                .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                .setContentTitle("GoUbiquitousSample")
                .setContentText("Time to learn about notifications!")
                .setSubText("Tap to view documentation about notifications.")
                .addAction(R.drawable.ic_plusone_small_off_client, "act1", pendingIntent)
                .setStyle(bigTextStyle);
        Notification notification = builder.build();

        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(getApplicationContext());
        notificationManager.notify(NOTIFICATION_ID, notification);
    }
}
	
Reply by voice to notification using phone micro

	GoUbiquitousSample master 96a55de commit
	
Reply by voice to notification using wearable micro (couldn't make it work)

	GoUbiquitousSample master 02c28cd commit
	see Android Studio > New > Import Sample > Wearable > Eliza Chat  <-- allows you to have conversation using speak recognition
	

	

	




