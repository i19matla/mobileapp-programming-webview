
# Rapport

Mats Läth Webbutveckling - Programmering kursen programmering av mobila applikationer.

Den presenterade appen är i grunden en "Fork" av appen WebView vilken uppgiften bjuder genom Github.
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Appen har fått ett nytt namn vilket skapades i XML-filen strings som huserar i mappen mobileapp-programming-webview\app\src\main\res\values\strings.xml
<resources>
    <string name="app_name">Mats L WebViewApp</string>			<-- Nytt namn.
    <string name="action_external_web">External Web Page</string>
    <string name="action_internal_web">Internal Web Page</string>
</resources>
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Appen gavs internetåtkomst genom att lägga till XML-koden <uses-permission android:name="android.permission.INTERNET" />
i XML-filen mobileapp-programming-webview\app\src\main\AndroidManifest.xml
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Det användaren möttas av initialt ursprungligen i appen var en text. Texten ersattes med ett WebView element (som i detta läget inte visar något).
Det ursprungliga textelementets kod ersattes med följande kod i XML-filen mobileapp-programming-webview\app\src\main\res\layout\content_main.xml
<WebView
        android:id="@+id/my_webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
WebView elementet gavs även ett id vilket är den följande del av ovanstående kod: android:id="@+id/my_webview".
Med detta id kan webview elementet enkelt kommas åt senare i appen genom att lagra det i en variabel (vilket inte görs här).
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Det id som skapades lagras nu i en variabel för att komma åt det för att kunna visa upp "förstasidan" för appen, det första mötet till användaren.
WebView firstMeeting = (WebView) findViewById(R.id.my_webview);
Därefter används java variabeln med xml id:t lagrad för att kalla på den i Android Studio skapade filen about.html som är skapad efter att mappen assets
hade skapats för att lagra about.html
about.html är med andra ord en tom html fil vilken sedan fått tillägget genom visual studio code en text som säger "En jättebra app faktiskt." och faktiskt
så är det ju det ;-) .
firstMeeting.loadUrl("file:///android_asset/about.html");
i filen AndroidStudioProjects\mobileapp-programming-webview\app\src\main\java\com\example\webviewapp\MainActivity.java
-------------------------------------------------------------------------------------------------------------------------------------------------------------
För att göra appen mer "webbvänlig" aktiveras också javascript för appens inbyggda webbläsare. Detta sker genom följande kod i filen
AndroidStudioProjects\mobileapp-programming-webview\app\src\main\java\com\example\webviewapp\MainActivity.java

WebSettings webSettings = myWebView.getSettings();
webSettings.setJavaScriptEnabled(true);
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Slutligen lades en extern och en intern webbsida till appen, his.se agerar som extern webbsida och som intern webbsida huserar den förträffliga sajten
Akademiska Hillbillyklubben. För att komma åt dessa krävs att användaren klickar på den av punkter vertikala linjen uppe till höger och väljer intern eller extern.
Koden för att visa den externa sajten är tillagd i metoden "public void showExternalWebPage()" och koden för den interna sajten ligger i metoden
"public void showInternalWebPage()"

public void showExternalWebPage(){
        WebView myWebView = (WebView) findViewById(R.id.my_webview);
        myWebView.loadUrl("https://www.his.se");
    }

public void showInternalWebPage(){
        WebView minWebView = (WebView) findViewById(R.id.my_webview);
        minWebView.loadUrl("file:///android_asset/index.html");
        //myWebView.loadUrl("file:///android_asset/about.html");
    }

För att sedan kunna använda dessa metoder kallas dessa längre ned i den övergripande gemensamma klassen "public class MainActivity extends AppCompatActivity"
anropet ser ut som följande:
public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_external_web) {
            Log.d("==>","Will display external web page");
            showExternalWebPage();				<--- Kallar på den externa sajten.
            return true;
        }

        if (id == R.id.action_internal_web) {
            Log.d("==>","Will display internal web page");
            showInternalWebPage();				<--- Kallar på den interna sajten.
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Slutligen läggs koden för att kunna zippa filen till:
```

Bilder läggs i samma mapp som markdown-filen.

![](android.png)
