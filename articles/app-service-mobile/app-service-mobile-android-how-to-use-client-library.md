---
title: aaaHow toouse hello Azure Mobile App SDK per Android | Documenti Microsoft
description: Come toouse hello App Mobile di Azure SDK per Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Come toouse hello App Mobile di Azure SDK per Android

Questa guida viene spiegato come toouse hello client SDK per Android per scenari comuni tooimplement App per dispositivi mobili, ad esempio:

* L'esecuzione di query sui dati, come inserimento, aggiornamento ed eliminazione.
* L'autenticazione.
* La gestione degli errori.
* Personalizzazione client hello.

Questa guida è incentrata su hello sul lato client Android SDK.  toolearn hello SDK lato server per le App per dispositivi mobili, vedere altre informazioni sulle [utilizzano back-end .NET SDK] [ 10] o [come toouse hello back-end Node.js SDK] [ 11].

## <a name="reference-documentation"></a>Documentazione di riferimento

È possibile trovare hello [riferimento all'API Javadocs] [ 12] per la libreria client per Android hello su GitHub.

## <a name="supported-platforms"></a>Piattaforme supportate

le applicazioni mobili di Azure SDK per Android Hello supporta livelli API 19 e 24 (KitKat tramite Nougat) per fattori di forma tablet e telefoni.  L'autenticazione, in particolare, utilizza delle credenziali toogather approccio framework web comuni.  L'autenticazione basata sul flusso server non funziona con dispositivi con fattore di forma piccolo, ad esempio gli orologi.

## <a name="setup-and-prerequisites"></a>Installazione e prerequisiti

Hello completo [avvio rapido di applicazioni per dispositivi mobili](app-service-mobile-android-get-started.md) esercitazione.  Questa attività garantisce che vengano soddisfatti tutti i prerequisiti per lo sviluppo di App per dispositivi mobili di Azure.  Guida introduttiva Hello consente inoltre di configurare l'account e creare il prima App per dispositivi mobili di back-end.

Se si decide di non toocomplete hello conosca, completare hello seguenti attività:

* [creare un back-end dell'App Mobile] [ 13] toouse con l'app Android.
* In Android Studio [compilare i file di aggiornamento hello Gradle](#gradle-build).
* [Abilitare l'autorizzazione per Internet](#enable-internet).

### <a name="gradle-build"></a>Aggiornare i file di compilazione Gradle hello

Modificare entrambi i file **build.gradle** :

1. Aggiungere questo codice toohello *progetto* livello **gradle** file all'interno di hello *buildscript* tag:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Aggiungere questo codice toohello *modulo app* livello **gradle** file all'interno di hello *dipendenze* tag:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Attualmente la versione più recente di hello è 3.3.0. sono elencate le versioni supportata di Hello [su bintray][14].

### <a name="enable-internet"></a>Abilitare l'autorizzazione per Internet

tooaccess Azure, l'applicazione deve disporre di autorizzazioni INTERNET hello abilitato. Se non è già abilitato, aggiungere hello successiva riga di codice tooyour **AndroidManifest.xml** file:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Creare una connessione client

Azure App per dispositivi mobili sono disponibili quattro funzioni tooyour applicazioni per dispositivi mobili:

* Accesso ai dati e sincronizzazione offline con un servizio di App per dispositivi mobili di Azure.
* Chiamare le API personalizzate scritte con hello Azure Mobile App Server SDK.
* Autenticazione con autenticazione e autorizzazione nel servizio app di Azure.
* Registrazione di notifiche push con Hub di notifica.

Per ogni funzione prima di tutto è necessario creare un oggetto `MobileServiceClient`.  È consigliabile creare un solo oggetto `MobileServiceClient` nel client per dispositivi mobili, ovvero il modello deve essere singleton.  toocreate un `MobileServiceClient` oggetto:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Hello `<MobileAppUrl>` è una stringa o un oggetto di URL che punta back-end mobile tooyour.  Se si utilizza Azure App Service toohost back-end per dispositivi mobili, quindi accertarsi di utilizzare hello sicura `https://` versione di hello URL.

Hello client inoltre richiede accesso toohello attività o il contesto - hello `this` parametro nell'esempio hello.  Hello MobileServiceClient costruzione deve verificarsi all'interno di hello `onCreate()` metodo dell'attività a cui fa riferimento a hello hello `AndroidManifest.xml` file.

Come procedura consigliata, è opportuno astrarre le comunicazioni del server nella relativa classe (modello singleton).  In questo caso, è necessario passare hello attività all'interno di hello costruttore tooappropriately configurare servizio hello.  ad esempio:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

È ora possibile chiamare `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` metodo dell'attività principale.  Utilizzano altri metodi che necessitano di client di accesso toohello `AzureServiceAdapter.getInstance();` tooobtain un adattatore del servizio toohello di riferimento.

## <a name="data-operations"></a>Operazioni dati

core Hello di hello App Mobile di Azure SDK è tooprovide toodata di accesso archiviato in SQL Azure nel back-end di hello App per dispositivi mobili.  È possibile accedere a questi dati usando classi fortemente tipizzate (preferibile) o query non tipizzate (non consigliato).  bulk Hello in questa sezione riguarda l'utilizzo di classi fortemente tipizzate.

### <a name="define-client-data-classes"></a>Definire le classi di dati client

tooaccess dati dalle tabelle di SQL Azure, definire classi di dati client corrispondenti tabelle toohello nel back-end di hello App per dispositivi mobili. Negli esempi in questo argomento si presuppone una tabella denominata **MyDataTable**, che dispone di hello seguenti colonne:

* id
* text
* complete

Hello oggetto sul lato client tipizzato corrispondente si trova in un file denominato **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Aggiungere i metodi getter e setter per ogni campo aggiunto.  Se la tabella di SQL Azure contiene più colonne, è possibile aggiungere classe toothis campi corrispondenti di hello.  Ad esempio, se hello DTO (oggetto di trasferimento di dati) è una colonna di tipo integer priorità, quindi è possibile aggiungere questo campo, insieme ai relativi metodi get e set:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn toocreate tabelle aggiuntive nel back-end App per dispositivi mobili, vedere [procedura: definire un controller di tabella] [ 15] (back-end .NET) o [definire tabelle utilizzando uno Schema dinamico] [ 16] (Back-end di Node. js).

Una tabella di back-end delle App mobili di Azure definisce cinque campi speciali, quattro delle quali sono disponibili tooclients:

* `String id`: ID univoco globale per il record di hello hello.  Come procedura consigliata, assicurarsi di rappresentazione di stringa di hello hello id di un [UUID] [ 17] oggetto.
* `DateTimeOffset updatedAt`: hello data/ora dell'ultimo aggiornamento hello.  campo updatedAt Hello è impostato dal server hello e non deve essere mai impostata dal codice client.
* `DateTimeOffset createdAt`: hello data/ora è stato creato l'oggetto hello.  campo createdAt Hello è impostato dal server hello e non deve essere mai impostata dal codice client.
* `byte[] version`: In genere è rappresentato come stringa, versione di hello anche viene impostato dal server hello.
* `boolean deleted`: Indica che i record di hello è stato eliminato ma non ancora eliminati.  Non usare `deleted` come proprietà nella classe.

Hello `id` campo è obbligatorio.  Hello `updatedAt` campo e `version` campo vengono utilizzati per la sincronizzazione non in linea (per la risoluzione dei conflitti e di sincronizzazione incrementale rispettivamente).  Hello `createdAt` campo è un campo di riferimento e non viene utilizzato dal client hello.  i nomi di Hello "in transito" come nome di proprietà hello e non sono modificabili.  Tuttavia, è possibile creare un mapping tra l'oggetto e hello "in transito" nomi utilizzando hello [gson] [ 3] libreria.  ad esempio:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Creare un riferimento alla tabella

tooaccess una tabella, creare innanzitutto un [MobileServiceTable] [ 8] oggetto chiamante hello **getTable** metodo hello [MobileServiceClient][9].  Questo metodo presenta due overload:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

Nel seguente codice, hello **mClient** è un oggetto MobileServiceClient tooyour di riferimento.  Hello primo overload viene utilizzato in cui il nome di classe hello e nome della tabella hello sono hello stesso e hello uno utilizzato nella Guida introduttiva hello:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Hello secondo overload viene utilizzato il nome di tabella hello è diverso dal nome di classe hello: hello primo parametro è il nome di tabella hello.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Eseguire una query su una tabella del back-end

Ottenere prima di tutto un riferimento alla tabella.  Eseguire una query in riferimento alla tabella hello.  Una query è qualsiasi combinazione di:

* Una [clausola di filtro](#filtering) `.where()`.
* Una [clausola di ordinamento](#sorting) `.orderBy()`.
* Una [clausola di selezione campo](#selection) `.select()`.
* `.skip()` e `.top()` per i [risultati di paging](#paging).

clausole Hello devono essere presentate in hello ordine precedente.

### <a name="filter"></a> Applicazione di filtri ai risultati

Hello forma generale di una query è:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Hello esempio precedente restituisce tutti i risultati (le dimensioni massime della pagina toohello impostato dal server hello).  Hello `.execute()` metodo esegue query hello sul back-end hello.  query Hello è convertito tooan [OData v3] [ 19] query prima di back-end di trasmissione toohello App per dispositivi mobili.  Al momento della ricezione, back-end App per dispositivi mobili hello converte query hello in un'istruzione SQL prima dell'esecuzione nell'istanza di SQL Azure hello.  Poiché l'attività di rete può richiedere tempo, hello `.execute()` metodo restituisce un [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtrare i dati restituiti

Hello dopo l'esecuzione di query restituisce tutti gli elementi da hello **ToDoItem** tabella in cui **completo** è uguale a **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** hello riferimento toohello servizio mobile tabella creata in precedenza.

Definire un filtro utilizzando hello **dove** chiamata al metodo nel riferimento alla tabella hello. Hello **in** metodo è seguito da un **campo** metodo seguito da un metodo che specifica hello logico predicato. I possibili metodi di predicato includono **eq** (uguale a), **ne** (non uguale a), **gt** (maggiore di), **ge** (maggiore o uguale a), **lt** (minore di), **le** (minore o uguale a). Questi metodi consentono di confrontare numero e i valori toospecific i campi stringa.

ad esempio filtrare in base alle date. Hello metodi seguenti consentono di confrontare il campo di data completa hello o parti di data hello: **anno**, **mese**, **giorno**, **ora**, **minuto**, e **secondo**. esempio Hello aggiunge un filtro per gli elementi il cui *data di scadenza* 2013 è uguale.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Hello metodi seguenti supportano i filtri complessi nei campi stringa: **startsWith**, **endsWith**, **concat**, **sottostringa**, **indexOf**, **sostituire**, **toLower**, **toUpper**, **trim**, e  **lunghezza**. Hello seguendo i filtri di esempio per le righe della tabella in cui hello *testo* colonna inizia con "PRI0".

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

Hello metodi degli operatori seguenti è supportato nei campi numero: **aggiungere**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, e **arrotondare**. Hello seguendo i filtri di esempio per le righe della tabella in cui hello **durata** è un numero pari.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

È possibile combinare i predicati con questi metodi logici: **and**, **or** e **not**. Hello di esempio seguente unisce due precedenti esempi hello.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Raggruppare e annidare operatori logici:

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Per ulteriori informazioni ed esempi di filtro, vedere [esplorazione ricchezza hello del modello di query client Android hello][20].

### <a name="sorting"></a>Ordinare i dati restituiti

Hello codice seguente restituisce tutti gli elementi di una tabella **ToDoItems** disposti in ordine crescente da hello *testo* campo. *mToDoTable* hello riferimento toohello back-end tabella creata in precedenza è:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

primo parametro di hello Hello **orderBy** metodo è un nome di toohello uguale di stringa del campo hello nella quale toosort. secondo parametro Hello utilizza hello **QueryOrder** enumerazione toospecify se toosort crescente o decrescente.  Se si applica un filtro utilizzando hello ***in*** (metodo), hello ***in*** metodo deve essere chiamato prima di hello ***orderBy*** metodo.

### <a name="selection"></a>Selezionare colonne specifiche

Hello codice seguente viene illustrato come tooreturn tutti gli elementi di una tabella **ToDoItems**, ma visualizza solo hello **completo** e **testo** campi. **mToDoTable** hello riferimento toohello back-end tabella creata in precedenza.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

funzione di selezione di Hello parametri toohello sono nomi di stringa hello hello colonna di tabella che si desidera tooreturn.  Hello **selezionare** metodo richiede metodi toofollow come **in** e **orderBy**. Può essere seguito da metodi di paging come **skip** e **top**.

### <a name="paging"></a>Restituire i dati in pagine

I dati vengono **SEMPRE** restituiti in pagine.  numero massimo di Hello di record restituito viene impostato dal server hello.  Se il client di hello richiede più record, quindi server hello restituisce hello numero massimo di record.  Per impostazione predefinita, la dimensione massima della pagina hello sul server di hello è 50 record.

Hello primo esempio viene illustrato come tooselect hello primi cinque elementi da una tabella. query Hello restituisce gli elementi di hello da una tabella di **ToDoItems**. **mToDoTable** hello riferimento toohello back-end tabella creata in precedenza è:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Ecco una query che ignora hello primi cinque elementi e quindi restituisce hello cinque Avanti:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Se si desiderano tooget tutti i record in una tabella, è possibile implementare codice tooiterate su tutte le pagine:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Una richiesta per tutti i record con questo metodo crea un minimo di back-end di due richieste toohello App per dispositivi mobili.

> [!TIP]
> Dimensioni di pagina destra scegliendo hello sono un equilibrio tra l'utilizzo della memoria richiesta hello in corso, l'utilizzo della larghezza di banda e ritardi nella ricezione di dati hello completamente.  valore predefinito di Hello (50 record) è adatto per tutti i dispositivi.  Se si opera esclusivamente nei dispositivi più grandi di memoria, aumentare le too500.  Sono stati rilevati tali dimensioni di pagina hello crescente oltre 500 registra i risultati in ritardo accettabile e problemi di memoria di grandi dimensioni.

### <a name="chaining"></a>Procedura: Concatenare metodi di query

metodi di Hello utilizzati in una query sulle tabelle di back-end possono essere concatenati. Concatenamento di query metodi consente tooselect colonne specifiche di righe filtrate e del pool di paging. È possibile creare filtri logici complessi.  Ogni metodo di query restituisce un oggetto Query. serie di hello tooend di metodi e query effettivamente esecuzione hello, chiamata hello **eseguire** metodo. ad esempio:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Hello concatenate query metodi devono essere ordinati come segue:

1. Metodi di filtraggio (**where**).
2. Metodi di ordinamento (**orderBy**).
3. Metodi di selezione (**select**).
4. Metodi di paging (**skip** e **top**).

## <a name="binding"></a>Associare l'interfaccia utente toohello di dati

L'associazione dati riguarda tre componenti:

* origine dati Hello
* layout della schermata Hello
* scheda Hello che ties hello due insieme.

Nel codice di esempio, si restituiscono dati hello dalla tabella di SQL Azure di App mobili hello **ToDoItem** in una matrice. Si tratta di una delle attività più comuni per le applicazioni dati.  Le query di database spesso restituiscono una raccolta di righe che hello client ottiene un elenco o matrice. In questo esempio, matrice hello è l'origine dati hello.  codice Hello specifica un layout della schermata che definisce hello visualizzazione dati hello che viene visualizzato nel dispositivo hello.  Hello due sono associati insieme a un adapter, che in questo codice è un'estensione di hello **ArrayAdapter&lt;ToDoItem&gt;**  classe.

#### <a name="layout"></a>Definire hello Layout

layout di Hello è definito da diversi frammenti di codice XML. Dato un layout esistente, hello seguente di codice rappresenta hello **ListView** desideriamo toopopulate con i dati del server.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Nel codice precedente di hello, hello *listitem* attributo specifica l'id di hello del layout di hello per una singola riga nell'elenco di hello. Questo codice consente di specificare una casella di controllo e il testo associato e viene creata un'istanza di una volta per ogni elemento nell'elenco di hello. Questo layout non viene visualizzato hello **id** campo e un layout più complesso specificare campi aggiuntivi nella visualizzazione hello. Questo codice è in hello **row_list_to_do.xml** file.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Definire hello adattatore
Poiché la vista origine dati hello è una matrice di **ToDoItem**, abbiamo sottoclasse l'adapter da un **ArrayAdapter&lt;ToDoItem&gt;**  classe. Questo tipo di sottoclasse produce una visualizzazione per ogni **ToDoItem** utilizzando hello **row_list_to_do** layout.  Nel codice, è possibile definire hello seguente classe che è un'estensione di hello **ArrayAdapter&lt;E&gt;**  classe:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Eseguire l'override di schede di hello **getView** metodo. ad esempio:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Creare un'istanza della classe nell'attività nel modo seguente:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

costruttore ToDoItemAdapter toohello Hello secondo parametro è un layout di toohello di riferimento. È ora possibile creare un'istanza hello **ListView** e assegnare hello adapter toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Utilizzare hello Adapter tooBind toohello dell'interfaccia utente

Si è ora pronto toouse l'associazione dati. Hello codice seguente viene illustrato come gli elementi tooget tabella hello e riempimenti hello scheda locale con hello restituita.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Chiamare adapter hello ogni volta che si modifica hello **ToDoItem** tabella. Dal momento che le modifiche vengono fatte record per record, si gestisce una singola riga anziché una raccolta. Quando si inserisce un elemento, chiamare hello **aggiungere** metodo hello adapter; in caso di eliminazione, chiamare hello **rimuovere** metodo.

È possibile trovare un esempio completo in hello [progetto di avvio rapido Android][21].

## <a name="inserting"></a>Inserire dati back-end hello

Creare un'istanza di hello *ToDoItem* classe e impostarne le proprietà.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Utilizzare quindi **Insert ()** tooinsert oggetto:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hello dati hello inseriti nella tabella di back-end hello, ID di hello incluso e tutti gli altri valori di corrispondenze di entità restituiti (ad esempio hello `createdAt`, `updatedAt`, e `version` campi) impostato sul back-end hello.

Le tabelle di App per dispositivi mobili richiedono una colonna chiave primaria denominata **id**. Questa colonna deve essere una stringa. il valore predefinito Hello della colonna ID hello è un GUID.  È possibile specificare altri valori univoci, come gli indirizzi di posta elettronica o i nomi utente. Quando un valore di ID di stringa non viene fornito un record inserito, back-end hello genera un nuovo GUID.

I valori di ID di stringa forniscono hello seguenti vantaggi:

* ID può essere generato senza un database toohello di andata e ritorno.
* I record sono toomerge più semplice da diverse tabelle o database.
* I valori ID si integrano in modo più efficace con la logica di un'applicazione.

I valori ID di stringa sono **OBBLIGATORI** per il supporto di sincronizzazione offline.  È possibile modificare un Id di una volta che viene archiviato nel database back-end hello.

## <a name="updating"></a>Aggiornare dati in un'app per dispositivi mobili

tooupdate dati in una tabella, passare hello nuovo oggetto toohello **Update ()** metodo.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

In questo esempio, *elemento* è una riferimento tooa riga hello *ToDoItem* tabella in cui è stato tooit alcune modifiche apportate.  riga Hello con hello stesso **id** viene aggiornato.

## <a name="deleting"></a>Eliminare dati in un'app per dispositivi mobili

Hello seguente codice mostra come toodelete dati da una tabella specificando hello oggetto dati.

```java
mToDoTable
    .delete(item);
```

È anche possibile eliminare un elemento specificando hello **id** campo toodelete riga hello.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Cercare un elemento specifico per ID

Cercare un elemento con una versione specifica **id** campo hello **Lookup** metodo:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Procedura: Usare dati non tipizzati

modello di programmazione non tipizzato Hello offre il controllo completo della serializzazione JSON.  Esistono alcuni scenari comuni in cui è preferibile toouse un modello di programmazione non tipizzato. Ad esempio, se la tabella di back-end contiene molte colonne ed è necessario solo un subset di colonne hello tooreference.  modello tipizzato Hello richiede toodefine tutte le colonne di hello definite nel back-end App per dispositivi mobili hello nella classe di dati.  La maggior parte delle chiamate API per l'accesso ai dati hello sono simile toohello tipizzati chiamate di programmazione. Hello differenza principale è che nel modello non tipizzato hello per richiamare metodi su hello **MobileServiceJsonTable** oggetto, anziché hello **MobileServiceTable** oggetto.

### <a name="json_instance"></a>Creare un'istanza di una tabella non tipizzata

Toohello simile tipizzati modello, iniziare recuperando un riferimento alla tabella, ma in questo caso è un **MobileServicesJsonTable** oggetto. Ottenere riferimento hello hello chiamante **getTable** metodo in un'istanza del client hello:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Dopo aver creato un'istanza di hello **MobileServiceJsonTable**, è praticamente hello stessa API disponibile come modello di programmazione tipizzato hello. In alcuni casi, i metodi di hello accettano un parametro non tipizzato invece di un parametro tipizzato.

### <a name="json_insert"></a>Eseguire un inserimento in una tabella non tipizzata
Hello seguente codice mostra come toodo un'istruzione insert. primo passaggio Hello è toocreate un [JsonObject][1], che fa parte di hello [gson] [ 3] libreria.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Utilizzare quindi **Insert ()** tooinsert oggetto non tipizzata di hello in tabella hello.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Se è necessario tooget hello ID dell'oggetto inserito hello, utilizzare hello **getAsJsonPrimitive()** metodo.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Eliminare un'istanza da una tabella non tipizzata
Hello codice seguente viene illustrato come toodelete un'istanza, in questo caso, hello stessa istanza di un **JsonObject** creato nella prima hello *inserire* esempio. codice Hello è hello stesso di hello tipizzata case, ma il metodo hello ha una firma diversa, perché fa riferimento a un **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

È inoltre possibile eliminare un'istanza direttamente utilizzando il relativo ID:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Restituire tutte le righe di una tabella non tipizzata
Hello seguente codice mostra come tooretrieve un'intera tabella. Poiché si utilizza una tabella JSON, è possibile recuperare in modo selettivo solo alcune colonne della tabella hello.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Hello stesso set di filtri, filtro e paging metodi disponibili per il modello tipizzato hello sono disponibili per il modello non tipizzato hello.

## <a name="offline-sync"></a>Implementare la sincronizzazione offline

Hello Azure Mobile App Client SDK implementa inoltre la sincronizzazione non in linea dei dati utilizzando un toostore database SQLite una copia dei dati hello del server locale.  Operazioni eseguite su una tabella non in linea non richiedono la connettività mobile toowork.  Sincronizzazione non in linea degli strumenti per la resilienza e delle spese di hello di una logica più complessa per la risoluzione dei conflitti.  Hello Azure Mobile App Client SDK implementa hello seguenti caratteristiche:

* Sincronizzazione incrementale: vengono scaricati solo i record aggiornati e nuovi, risparmiando larghezza di banda e utilizzo della memoria.
* Concorrenza ottimistica: Le operazioni vengono considerate toosucceed.  Risoluzione dei conflitti viene posticipata fino a quando gli aggiornamenti vengono eseguiti nel server di hello.
* Risoluzione dei conflitti: hello che SDK rileva se una modifica in conflitto è stata eseguita nel server di hello e fornisce hook utente hello tooalert.
* L'eliminazione temporanea: Record eliminato è contrassegnata come eliminato, consentendo tooupdate altri dispositivi la cache offline.

### <a name="initialize-offline-sync"></a>Inizializzare la sincronizzazione offline

Ogni tabella non in linea deve essere definito nella cache offline di hello prima dell'uso.  Definizione della tabella in genere, viene eseguita subito dopo la creazione di hello del client hello:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Ottenere un toohello di riferimento non in linea la tabella della Cache

Per una tabella online, si usa `.getTable()`.  Per una tabella offline, usare `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Tutti hello metodi disponibili per le tabelle in linea (incluso il filtro, ordinamento, paging, inserimento di dati, l'aggiornamento dei dati e l'eliminazione dei dati) funzionano altrettanto bene in tabelle online e offline.

### <a name="synchronize-hello-local-offline-cache"></a>Sincronizzare hello Cache Offline locale

La sincronizzazione è all'interno di controllo di hello dell'app.  Ecco un esempio di metodo di sincronizzazione:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Se non viene fornito un nome di query toohello `.pull(query, queryname)` (metodo), la sincronizzazione incrementale è tooreturn utilizzati solo i record che sono stati creati o modificati dopo pull hello completato correttamente.

### <a name="handle-conflicts-during-offline-synchronization"></a>Gestire i conflitti durante la sincronizzazione offline

Se si verifica un conflitto durante un'operazione `.push()`, viene generata un'eccezione `MobileServiceConflictException`.   elemento rilasciato server Hello è incorporato nell'eccezione hello e possono essere recuperato tramite `.getItem()` eccezione hello.  Regolare il push di hello da parte del chiamante hello seguenti di elementi nell'oggetto MobileServiceSyncContext hello:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Dopo che tutti i conflitti sono contrassegnati come si desidera, chiamare `.push()` tooresolve nuovamente tutti i conflitti di hello.

## <a name="custom-api"></a>Chiamare un'API personalizzata

Un'API personalizzata consente toodefine endpoint personalizzati che espongono la funzionalità server che non eseguire il mapping delle insert tooan, aggiornare, eliminare o operazione di lettura. L'utilizzo di un'API personalizzata offre maggiore controllo sulla messaggistica, incluse la lettura e l'impostazione delle intestazioni del messaggio HTTP e la definizione di un formato del corpo del messaggio diverso da JSON.

Da un client Android, si chiama hello **invokeApi** endpoint API personalizzata di metodo toocall hello. Hello esempio seguente viene illustrato come toocall un endpoint API denominati **completeAll**, che restituisce una classe collection denominata **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Hello **invokeApi** metodo viene chiamato nel client hello, che invia una richiesta di un POST toohello nuova API personalizzata. risultato Hello restituito dall'API personalizzata hello viene visualizzata nella finestra di messaggio, come errori. Altre versioni di **invokeApi** consentono l'invio di un oggetto nel corpo della richiesta hello facoltativamente, specificare il metodo HTTP hello e Invia parametri di query con richiesta di hello. Vengono fornite anche versioni non tipizzate di **invokeApi** .

## <a name="authentication"></a>Aggiungere app tooyour authentication

Esercitazioni già descrivono in dettaglio come tooadd queste funzionalità.

Il servizio app supporta l'[autenticazione degli utenti di app](app-service-mobile-android-get-started-users.md) con diversi provider di identità esterni: Facebook, Google, account Microsoft, Twitter e Azure Active Directory. È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users. È inoltre possibile utilizzare identità hello gli utenti autenticati tooimplement delle regole di autorizzazione nel back-end.

Sono supportati due flussi di autenticazione, ovvero un flusso **server** e un flusso **client**. flusso di Hello server fornisce l'esperienza di autenticazione più semplice hello, come si basa sull'interfaccia web provider di identità hello.  Nessun SDK aggiuntivo è l'autenticazione del server flusso di tooimplement obbligatorio. L'autenticazione del server del flusso non fornisce un'integrazione completa in dispositivi mobili hello ed è consigliata solo per la prova di scenari.

flusso di Hello client consente una maggiore integrazione con funzionalità specifiche del dispositivo, ad esempio accesso single sign-on di si basa sul SDK, fornito dal provider di identità hello.  Ad esempio, è possibile integrare hello Facebook SDK nell'applicazione per dispositivi mobili.  client mobili Hello Scambia in app Facebook hello e conferma il sign-on prima di effettuare lo swapping tooyour indietro app per dispositivi mobili.

Quattro passaggi sono necessari tooenable autenticazione nell'app:

* Registrare l'app per l'autenticazione con un provider di identità.
* Configurare il back-end del servizio app.
* Limitare gli utenti tooauthenticated le autorizzazioni di tabella solo in hello back-end del servizio App.
* Aggiungere app tooyour codice di autenticazione.

È possibile impostare le autorizzazioni di accesso toorestrict tabelle per operazioni specifiche tooonly autenticata users. È inoltre possibile utilizzare hello SID di un utente autenticato di toomodify richieste.  Per altre informazioni, vedere [Introduzione all'autenticazione] e documentazione Server SDK HOWTO hello.

### <a name="caching"></a>Autenticazione: flusso server

Hello codice seguente avvia un processo di accesso server flusso usando il provider di Google hello.  Configurazione aggiuntiva è necessario a causa dei requisiti di sicurezza hello per provider di Google hello:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Inoltre, aggiungere hello seguente classe di attività metodo toohello principale:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

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
```

Hello `GOOGLE_LOGIN_REQUEST_CODE` definito in principale attività viene utilizzata per hello `login()` (metodo) e all'interno di hello `onActivityResult()` metodo.  È possibile scegliere qualsiasi numero univoco, purché hello stesso numero viene utilizzato all'interno di hello `login()` metodo e hello `onActivityResult()` metodo.  Se il codice client hello astratta in una scheda di servizio (come illustrato in precedenza), è necessario chiamare i metodi appropriati hello nella scheda servizio hello.

È inoltre necessario progetto hello tooconfigure per customtabs.  Specificare prima di tutto un URL di reindirizzamento.  Aggiungere hello seguente frammento di codice troppo`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Aggiungere hello **redirectUriScheme** toohello `build.gradle` file dell'applicazione:

```text
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
```

Infine, aggiungere `com.android.support:customtabs:23.0.1` toohello elenco di dipendenze in hello `build.gradle` file:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Ottenere ID hello di hello utente connesso da un **MobileServiceUser** utilizzando hello **Recuperaidutente** metodo. Per un esempio di come toouse ritardo toocall hello asincrona accesso API, vedere [Introduzione all'autenticazione].

> [!WARNING]
> lo schema dell'URL indicato Hello è tra maiuscole e minuscole.  Assicurarsi che tutte le occorrenze di `{url_scheme_of_you_app}` rispettino questa distinzione.

### <a name="caching"></a>Memorizzare nella cache i token di autenticazione

La memorizzazione nella cache i token di autenticazione richiede toostore hello ID utente e token di autenticazione in locale nel dispositivo hello. Hello prossimo avvio dell'applicazione hello, controllo della cache di hello e, se questi valori sono presenti, è possibile ignorare log hello nella procedura e riattivare i client hello con questi dati. Tuttavia questi dati sono riservati e devono essere archiviato crittografati per garantire la protezione in caso di furto di un telefono hello.  È possibile visualizzare un esempio completo di come token di autenticazione toocache in [Cache sezione token di autenticazione][7].

Quando si tenta di toouse un token scaduto, viene visualizzato un *401 non autorizzato* risposta. È possibile gestire gli errori di autenticazione tramite i filtri.  I filtri intercettano richieste toohello back-end del servizio App. il codice del filtro Hello verifica risposta hello per 401, trigger di processo di accesso hello e quindi riprende richiesta hello che ha generato hello 401.

### <a name="refresh"></a>Usare i token di aggiornamento

token di Hello restituito da Azure App Service autenticazione e autorizzazione ha una durata definita di un'ora.  Dopo questo periodo, è necessario ripetere l'autenticazione utente hello.  Se si utilizzando un token di lunga durato che si è ricevuto tramite l'autenticazione client per il flusso, quindi è possibile ripetere l'autenticazione con l'autenticazione del servizio App di Azure e le autorizzazioni mediante hello stesso token.  Viene generato un altro token del servizio app di Azure con una nuova durata.

È anche possibile registrare hello provider toouse i token di aggiornamento.  Un token di aggiornamento non è sempre disponibile.  È necessaria una configurazione aggiuntiva:

* Per **Azure Active Directory**, configurare un segreto client per hello App di Azure Active Directory.  Specificare la chiave privata client hello in hello Azure App Service quando si configura l'autenticazione di Azure Active Directory.  Quando si chiama `.login()`, passare `response_type=code id_token` come parametro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Per **Google**, passare hello `access_type=offline` come parametro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Per **Account Microsoft**selezionare hello `wl.offline_access` ambito.

toorefresh un token, chiamare `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Come procedura consigliata, creare un filtro che rileva una risposta dal server hello 401 e tenta di token dell'utente toorefresh hello.

## <a name="log-in-with-client-flow-authentication"></a>Accedere con l'autenticazione basata sul flusso client

processo generale di Hello per l'accesso con autenticazione di client per il flusso è come segue:

* Configurare l'autenticazione e l'autorizzazione del servizio app di Azure come si configura l'autenticazione basata sul flusso server.
* Integrare il provider di autenticazione hello SDK per l'autenticazione tooproduce un token di accesso.
* Chiamare hello `.login()` metodo come indicato di seguito:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Sostituire hello `onSuccess()` (metodo) con qualsiasi tipo di codice si desidera toouse un account di accesso ha esito positivo.  Hello `{provider}` stringa è un provider valido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, o **twitter**.  Se è stato implementato l'autenticazione personalizzata, è possibile utilizzare tag di provider di autenticazione personalizzata hello.

### <a name="adal"></a>Autenticare gli utenti con hello Active Directory Authentication Library (ADAL)

È possibile utilizzare gli utenti toosign di Active Directory Authentication Library (ADAL) hello in un'applicazione tramite Azure Active Directory. Utilizzando un account di accesso client del flusso è spesso preferibile toousing hello `loginAsync()` metodi che fornisce un'idea dell'esperienza utente più nativa e consente un'ulteriore personalizzazione.

1. Configurare il back-end dell'app mobile per l'accesso AAD hello seguente [come tooconfigure App del servizio per l'account di accesso Active Directory] [ 22] esercitazione. Verificare che passaggio facoltativo in hello toocomplete di registrazione di un'applicazione client nativa.
2. Installare ADAL modificando il hello tooinclude del file gradle seguenti definizioni:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Aggiungere hello seguito codice tooyour applicazione, rendendo hello seguenti sostituzioni:

* Sostituire **INSERT-autorità-qui** con nome hello del tenant di hello in cui è stato eseguito il provisioning dell'applicazione. formato di Hello deve essere https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Sostituire **INSERT-RESOURCE-ID-qui** con hello client ID per il back-end dell'app per dispositivi mobili. È possibile ottenere l'ID client hello da hello **avanzate** scheda **impostazioni di Azure Active Directory** nel portale di hello.
* Sostituire **INSERT-CLIENT-ID-qui** con ID client hello copiato dall'applicazione client nativa hello.
* Sostituire **INSERT-REDIRECT-URI-qui** con il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello. Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Regolare hello comunicazione tra Client e Server

Hello connessione Client è in genere una connessione HTTP di base utilizzando hello sottostante libreria HTTP fornita con hello Android SDK.  Esistono diversi motivi per cui si toochange che:

* Si desidera toouse un timeout di tooadjust libreria HTTP alternativo.
* Si desidera tooprovide un indicatore di stato.
* Si desidera tooadd una funzionalità di gestione API toosupport intestazione personalizzata.
* Si desidera toointercept una risposta non riuscita in modo che è possibile implementare la riautenticazione.
* Si desidera che il servizio analitica tooan di toolog back-end le richieste.

### <a name="using-an-alternate-http-library"></a>Uso di una libreria HTTP alternativa

Chiamare hello `.setAndroidHttpClientFactory()` metodo subito dopo la creazione del riferimento del client.  Ad esempio, tooset hello connection timeout too60 secondi (anziché hello impostazione predefinita 10 secondi):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Implementare un filtro per l'avanzamento

È possibile implementare un intercettazione di ogni richiesta implementando `ServiceFilter`.  Ad esempio, l'esempio hello aggiorna un indicatore di stato creato in precedenza:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

È possibile collegare questo client toohello filtro come segue:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Personalizzare le intestazioni delle richieste

Utilizzare la seguente hello `ServiceFilter` e allegare il filtro hello in hello esattamente come hello `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Configurare la serializzazione automatica

È possibile specificare una strategia di conversione che si applica a colonna tooevery utilizzando hello [gson] [ 3] API. libreria client per Android Hello Usa [gson] [ 3] background hello tooserialize Java gli oggetti dati tooJSON prima dell'invio dei dati hello tooAzure servizio App.  il codice seguente Hello Usa hello **setFieldNamingStrategy()** strategia hello tooset di metodo. In questo esempio verrà eliminato il carattere iniziale di hello (una "m") e successivo carattere minuscoli hello, per ogni nome di campo. ad esempio, trasforma "mId" in "id".  Implementare un hello tooreduce strategia di conversione necessaria per `SerializedName()` annotazioni nella maggior parte dei campi.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Questo codice deve essere eseguito prima di creare un riferimento di client per dispositivi mobili usando hello **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[Introduzione all'autenticazione]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
