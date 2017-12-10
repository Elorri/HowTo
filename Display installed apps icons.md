In Tools.java   
	
		public static List<ResolveInfo> getInstalledApps(PackageManager packageManager) {
			final Intent intent = new Intent(Intent.ACTION_MAIN, null);
			intent.addCategory(Intent.CATEGORY_LAUNCHER);//choose here the best option
			return packageManager.queryIntentActivities(intent, 0);
		}

		public static List<PackageInfo> getInstalledPackages(PackageManager packageManager) {
			return packageManager.getInstalledPackages(0);
		}
	

In mainActivity

        for (ResolveInfo ri : Tools.getInstalledApps(getActivity().getPackageManager())) {
            Log.e("ff", Thread.currentThread().getStackTrace()[2] + ""+ri.activityInfo.toString());
			Log.e("ff", Thread.currentThread().getStackTrace()[2] + "" + ri.resolvePackageName);
			findViewById(R.id.image).setBackground(ri.loadIcon(getPackageManager()));
        }

        for (PackageInfo pi : Tools.getInstalledPackages(getActivity().getPackageManager())) {
            Log.e("ff", Thread.currentThread().getStackTrace()[2] + ""+pi.applicationInfo.toString());
            // to get drawable icon -->  ri.loadIcon(package_manager)
        }
		
		for (PackageInfo pi : getPackageManager().getInstalledPackages(0)) {
            Log.e("ff", Thread.currentThread().getStackTrace()[2] + "" + pi.applicationInfo.loadLabel(getPackageManager()));
            Log.e("ff", Thread.currentThread().getStackTrace()[2] + "" + pi.applicationInfo.labelRes);
            Log.e("ff", Thread.currentThread().getStackTrace()[2] + "" + pi.applicationInfo.packageName);
			try {
				findViewById(R.id.image).setBackground(getPackageManager().getApplicationIcon("com.facebook.katana"));
			} catch (PackageManager.NameNotFoundException e) {
				e.printStackTrace();
			}
        }


		
		