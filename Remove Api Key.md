# See this post.

	https://discussions.udacity.com/t/how-to-prevent-themoviedb-org-api-key-from-being-published-on-github-com/40667

# Gradle
Add the following line to [USER_HOME]/.gradle/gradle.properties

	MyTheMovieDBApiToken="XXXXX"


Add the following code to the build.gradle file

	*build.gradle*
	```gradle
	apply plugin: 'com.android.application'

	android {
		...

		defaultConfig {
			...
		}
		buildTypes {
			release {
				...
			}
			buildTypes.each {
				it.buildConfigField 'String', 'THE_MOVIE_DB_API_TOKEN', MyTheMovieDBApiToken
			}
		}
	}

# Code
Use api keys in java code

	BuildConfig.THE_MOVIE_DB_API_TOKEN


# Git
Add the following line to the .gitignore

	gradle.properties
	
Open git in command line and type : 

	git rm --cached gradle.properties
	
Push on git

	git add -A
	git commit -m 'add gradle.properties to gitignore'
	git push origin master
	
Asyou can see gradle.properties is not anymore on github but remain in your local directory.
