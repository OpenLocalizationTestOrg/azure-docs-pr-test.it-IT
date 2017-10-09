
1. Aprire il progetto di hello in Android Studio.

2. In **Esplora progetti** in Android Studio, aprire il file di ToDoActivity.java hello e aggiungere hello seguendo le istruzioni di importazione:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Aggiungere hello seguente metodo toohello **ToDoActivity** classe:

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

    Questo codice crea un hello toohandle metodo processo di autenticazione Google. Una finestra di dialogo Visualizza hello ID dell'utente autenticato hello. È possibile procedere unicamente se l'autenticazione ha esito positivo.

    > [!NOTE]
    > Se si utilizza un provider di identità diverso da Google, modificare il valore di hello passato toohello **accesso** metodo tooone di hello seguenti valori: _MicrosoftAccount_, _Facebook_, _Twitter_, o _windowsazureactivedirectory_.

4. In hello **onCreate** metodo, aggiungere hello successiva riga di codice dopo il codice hello che crea un'istanza di hello `MobileServiceClient` oggetto.

        authenticate();

    La chiamata avvia il processo di autenticazione hello.

5. Spostare hello rimanenti codice dopo `authenticate();` in hello **onCreate** tooa metodo nuovo **createTable** metodo:

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

6. tooensure reindirizzamento funziona come previsto, aggiunta hello seguente frammento di _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Aggiungere too_build.gradle_ redirectUriScheme dell'applicazione Android.

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

8. Aggiungere il gradle com.android.support:customtabs:23.0.1 toohello dipendenze:

      dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }

9. Da hello **eseguire** menu, fare clic su **eseguire app** toostart hello app e accedere con il provider di identità selezionato.

> [!WARNING]
> lo schema dell'URL indicato Hello è tra maiuscole e minuscole.  Verificare che tutte le occorrenze di `{url_scheme_of_you_app}` utilizzare hello stesso case.

Quando si è connessi correttamente, hello app devono essere eseguite senza errori, ed è necessario essere in grado di tooquery hello back-end servizio e apportare aggiornamenti toodata.
