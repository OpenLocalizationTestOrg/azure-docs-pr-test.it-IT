
1. <span data-ttu-id="8c204-101">Aprire il progetto di hello in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="8c204-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="8c204-102">In **Esplora progetti** in Android Studio, aprire il file di ToDoActivity.java hello e aggiungere hello seguendo le istruzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="8c204-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="8c204-103">Aggiungere hello seguente metodo toohello **ToDoActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="8c204-103">Add hello following method toohello **ToDoActivity** class:</span></span>

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="8c204-104">Questo codice crea un hello toohandle metodo processo di autenticazione Google.</span><span class="sxs-lookup"><span data-stu-id="8c204-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="8c204-105">Una finestra di dialogo Visualizza hello ID dell'utente autenticato hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="8c204-106">È possibile procedere unicamente se l'autenticazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="8c204-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c204-107">Se si utilizza un provider di identità diverso da Google, modificare il valore di hello passato toohello **accesso** metodo tooone di hello seguenti valori: _MicrosoftAccount_, _Facebook_, _Twitter_, o _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="8c204-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="8c204-108">In hello **onCreate** metodo, aggiungere hello successiva riga di codice dopo il codice hello che crea un'istanza di hello `MobileServiceClient` oggetto.</span><span class="sxs-lookup"><span data-stu-id="8c204-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="8c204-109">La chiamata avvia il processo di autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c204-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="8c204-110">Spostare hello rimanenti codice dopo `authenticate();` in hello **onCreate** tooa metodo nuovo **createTable** metodo:</span><span class="sxs-lookup"><span data-stu-id="8c204-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="8c204-111">tooensure reindirizzamento funziona come previsto, aggiunta hello seguente frammento di _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="8c204-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="8c204-112">Aggiungere too_build.gradle_ redirectUriScheme dell'applicazione Android.</span><span class="sxs-lookup"><span data-stu-id="8c204-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. <span data-ttu-id="8c204-113">Aggiungere il gradle com.android.support:customtabs:23.0.1 toohello dipendenze:</span><span class="sxs-lookup"><span data-stu-id="8c204-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="8c204-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="8c204-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="8c204-115">Da hello **eseguire** menu, fare clic su **eseguire app** toostart hello app e accedere con il provider di identità selezionato.</span><span class="sxs-lookup"><span data-stu-id="8c204-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="8c204-116">lo schema dell'URL indicato Hello è tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8c204-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="8c204-117">Verificare che tutte le occorrenze di `{url_scheme_of_you_app}` utilizzare hello stesso case.</span><span class="sxs-lookup"><span data-stu-id="8c204-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="8c204-118">Quando si è connessi correttamente, hello app devono essere eseguite senza errori, ed è necessario essere in grado di tooquery hello back-end servizio e apportare aggiornamenti toodata.</span><span class="sxs-lookup"><span data-stu-id="8c204-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
