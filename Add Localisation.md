Localisation : https://developer.android.com/distribute/tools/localization-checklist.html
Localisation : https://developer.android.com/distribute/tools/localization-checklist.html

#Choose the most suitable localisation

## Run this prog to get a full list of available locale on your devices 
	
	    public static void printAvailableDevicesLocales(){
			final Locale[] availableLocales=Locale.getAvailableLocales();
			for(final Locale locale : availableLocales)
				Log.d("Applog",":"+locale.getDisplayName()+":"+locale.getLanguage()+":"
					+locale.getCountry()+":values-"+locale.toString().replace("_","-r"));
    }
	
	
## Or choose all the Locales you want to support with this table. 

Always support the Locale.en_US as a minimum. This is the only locale Java guarantees is always available. + choose your default Locale.
	
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

# Get info about the user device

create a utility fonction to get the user most suitable Locale and Unit and store them in a preferred file. 
			
## get the most suitable user Locale : getPreferedLocale()

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
	
## get the most suitable user Units: getPreferedUnits()

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

# When data is displayed or compute

## Whenever data is taken from the server and displayed to the user without computation
(it needs to be converted correctly in something we know)

### numbers

	double serveurDouble;
	Locale serveurLocale;
	NumberFormat numberFormat = NumberFormat.getNumberInstance(serveurLocale);
	String serveurDoubleString = numberFormat.format(serveurDouble);
	Number number = format.parse(serveurDoubleString);
	serveurDouble = number.doubleValue(); //Now we are sure we have the correct number (no ',' misplaced)
	numberFormat = NumberFormat.getNumberInstance(getPreferredLocale());
	String userFriendlyDoubleString = numberFormat.format(serveurDouble);
	
### dates

	String serveurDateString;
	Locale serveurLocale;
	DateFormat dateFormat = DateFormat.getDateInstance(DateFormat.DEFAULT, serveurLocale); //DateFormat.DEFAULT should correspond to notation used by serveur or use   SimpleDateFormat dateFormat = new SimpleDateFormat("EEE MMM dd", serveurLocale);
	DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.DEFAULT, DateFormat.DEFAULT, serveurLocale);
	DateFormat dateFormat = DateFormat.getTimeInstance(DateFormat.DEFAULT, serveurLocale);
	dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
	Date serveurDate = dateFormat.parse(serveurDateString); //Now we are sure we have a correct Date
	dateFormat = new SimpleDateFormat("EEE MMM dd", getPreferredLocale()); //format to user flavor
	String serveurDateString = dateFormat.format(serveurDate);		
	
### Timestamp

	//TODO improve this part
	Libéria : Locale.vai_LATN, Locale.vai_VAII, Locale.en_LR
	df.setTimeZone(TimeZone.getTimeZone("UTC"));
	
it is when parsing that set timezone has an effet:
	
	DateFormat utcFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'");
	Date date = utcFormat.parse("2012-08-15T22:56:02.038Z");
	
equals

	DateFormat utcFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'");
	utcFormat.setTimeZone(TimeZone.getDefault());
	Date date = utcFormat.parse("2012-08-15T22:56:02.038Z");

	
This will parse the date with the user locale, wihch is wrong because the 'Z' mentionned it's in UTC
Then trying to do

        SimpleDateFormat df = new SimpleDateFormat("HH:mm", getMostSuitableLocale(context));
        df.setTimeZone(TimeZone.getDefault());
		df.format(cal.getTimeInMillis());
	
to display, will have no effect, because it has been parse anddisplayed with thesame locale ,it will display the time in UTC thinking it'is in locale timezone.

We should do : 

	DateFormat utcFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'");
	utcFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
	Date date = utcFormat.parse("2012-08-15T22:56:02.038Z");

When we take data from the serveur, and 
	SimpleDateFormat df = new SimpleDateFormat("HH:mm", getMostSuitableLocale(context));
    df.setTimeZone(TimeZone.getDefault());
	df.format(cal.getTimeInMillis());
	
when we display it. Note the setTimeZone se fait sur le df et pas sur le calendar ou la date
	
	SimpleDateFormat df = new SimpleDateFormat("HH:mm", getMostSuitableLocale(context));
    // df.setTimeZone(TimeZone.getDefault()); default will be used anyway
    return df.format(new Date(dateTime));
	
Note : Date is always UTC-based. It does not contain time zone information. You set the timezone when you display the date, hence tell it to SimpleDateFormat. if you want the local time zone of the computer that your program is running on, use:
	
	df.setTimeZone(TimeZone.getDefault());

locales are only for special caracteeres ind idfferents languages. What matter most here is timezone.
	
### currencies

	Locale serveurLocale;
	Currency c=Currency.getInstance(serveurLocale); exple $ if serveurLocale is en_US
	//Don't use : Log.d("symbol",c.getSymbol()); //Will display $ the symbol in the serveur Locale
	Log.d("symbol",c.getSymbol(getPreferredLocale())); //Will display US$ ->$ the symbol in the user Locale
### text 

	//Don't use :toLowerCase(), toUpperCase()
	toLowerCase(getPreferredLocale()) 
	toUpperCase(getPreferredLocale()) 
	
### phone numbers 

	PhoneNumberUtils
	
### Characters
	Don't : view.setText(temperacture+"°C"); because it can change from countries.
	Do : use xliff xml static decimal temperature value AND unicode caractere for the degree symbol.
		<string name="format_temperature"><xliff:g id="temp">%1.0f</xliff:g>\u00B0</string>
		String.format(context.getString(R.string.format_temperature), temperature);
	xml string format :http://developer.android.com/guide/topics/resources/string-resource.html#FormattingAndStyling		
		
## Whenever data is taken from the user or serveur and then compute or store in the db

It is best to convert the data in Locale.en_US

	idem above but with Locale.en_US
	
## Whenever data is taken from db or computation and displayed to the user

	idem above but with user Locale
	
## Whenever data is taken from the ressource directory
### for the default chosen Locale

	1- make sure layout.xml and arrays.xml contains 0 strings.
	2- make sure it is in the default "value" directory
	3- if the others locales have a start to end display
			- add the start-end tags but do not remove left/right tag (=LTR) for Android min v < 17. Add the start-end tags alone for Android v > 17.
			- add the manifest tag : <application> android:supportsRtl="true"</application>
				- if you want a RTL language device Locale to display RTL because you are not supporting this language, do this. 
				- android:supportsRtl="@string/is_hebrew"
				- values/strings.xml : <string name="is_hebrew">false</string> hebrew language will be displayed in english LTR
				- values-he/strings.xml : <string name="is_hebrew">true</string>
			-  Android 5 (lollipop) automatically mirrors everything on the widget (even images), so a text or image that is left adjusted will become right adjusted. To prevent this add to the main/outer layout of the widget the following, android:layoutDirection="ltr" and it will force the layout to be left-to-right, even in right-to-left languages.
			- Useful attributes : 
				- android:layoutDirection - attribute for setting the direction of a component's layout.
				- android:textDirection - attribute for setting the direction of a component's text.
				- android:textAlignment - attribute for setting the alignment of a component's text.
				- getLayoutDirectionFromLocale() - method for getting the Locale-specified direction
	4- make sure you have a strings.xml for each locale and the "translable" attribute is specified. 
		Purchase translation : https://developer.android.com/distribute/tools/localization-checklist.html#gp-trans
		
### for others Locale and IF the layout change from the default 

	1- add the corresponding directory ex:values-fr-rFR or values-fr
	
	
	
Nb : 
Timestamp as well as Date does not have timezone information and should always contain a GMT timestamp.
GMT  offset(=decalage horaire par rapport a greenwish = time zone)
UTC uses GMT

To be correct Timestamp should be express with GMT offset like this : 2007-02-26T21:23:14.250+01:00
If nothing is set we must assume time zone is +00:00 from GMT
If a Z like that 2016-01-13T19:45:00Z is set we must assume time zone is +00:00 from GMT


Calendar.getTimeInMillis() 

| Java format pattern          | Timestamps                     | Label          |
| ---------------------------- | :---------------------------: |:-------------: |
| yyyy-MM-dd'T'hh:mm:ss.SSSX|2007-02-26T21:23:14.250GMT+8:00   |  General time zone   |
| yyyy-MM-dd'T'hh:mm:ss.SSSX|2007-02-26T21:23:14.250GMT+20:00   |  General time zone   |
| yyyy-MM-dd'T'hh:mm:ss.SSSX|2007-02-26T21:23:14.250+08:00   |  RFC 822 time zone  |
| yyyy-MM-dd'T'hh:mm:ss.SSSX|2012-11-25T23:50:56.193+01      |OneLetterISO8601TimeZone|
| yyyy-MM-dd'T'hh:mm:ss.SSSXX|2012-11-25T23:50:56.193+0100 |TwoLetterISO8601TimeZone|
| yyyy-MM-dd'T'hh:mm:ss.SSSXXX|2012-11-25T23:50:56.193+01:00|ThreeLetterISO8601TimeZone|


#  Some good links

https://discussions.udacity.com/t/layout-mirroring-rtl-isnt-supported-correctly-for-app-bar/177336/3
