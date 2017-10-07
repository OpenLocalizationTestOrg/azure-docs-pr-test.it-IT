---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Cordova) | Documenti Microsoft
description: Informazioni su come toouse App del servizio Mobile App toocache e sincronizzazione dati offline nella propria applicazione Cordova
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Abilitare la sincronizzazione offline per l'app per dispositivi mobili Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

In questa esercitazione introduce funzionalità di sincronizzazione non in linea hello di App mobili di Azure per Cordova. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete. Le modifiche vengono archiviate in un database locale.  Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con servizio remoto hello.

In questa esercitazione si basa sull'hello Cordova delle Guide rapide soluzione per App per dispositivi mobili creati quando si completa hello esercitazione [avvio rapido di Apache Cordova]. In questa esercitazione è aggiornare hello delle Guide rapide tooadd offline caratteristiche della soluzione di App mobili di Azure.  È inoltre evidenziati codice specifico per la linea hello in app hello.

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure]. Per informazioni dettagliate sull'utilizzo di API, vedere hello [documentazione dell'API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Aggiungi soluzione di sincronizzazione non in linea toohello Guida introduttiva
aggiungere il codice di sincronizzazione non in linea Hello toohello app. Sincronizzazione non in linea richiede plug-in cordova-sqlite-archiviazione hello, che viene aggiunto automaticamente app tooyour quando plug-in App mobili di Azure hello è incluso nel progetto hello. progetto di avvio rapido Hello include entrambi questi plug-in.

1. In Esplora soluzioni di Visual Studio, aprire index.js e sostituire hello seguente di codice

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    con questo codice:

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Successivamente, sostituire hello seguente codice:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    con questo codice:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    inizializzare l'archivio locale hello Hello aggiunte di codice precedente e definire una tabella locale che corrisponde a valori di colonna hello utilizzati in di Azure back-end. (Non è necessario tooinclude tutti i valori di colonna in questo codice.)  Hello `version` campo gestito dal back-end mobile hello e viene utilizzato per la risoluzione dei conflitti.

    Ottenere un contesto di sincronizzazione toohello riferimento chiamando **getSyncContext**. Hello contesto di sincronizzazione consente di mantenere le relazioni tra tabelle e di rilevamento e il push delle modifiche in tutte le tabelle modificato quando un'app client `.push()` viene chiamato.

3. Aggiornare l'URL dell'applicazione Mobile App tooyour URL applicazione hello.

4. Quindi, sostituire il codice:

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    con questo codice:

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    Hello precedente codice inizializza il contesto di sincronizzazione hello e quindi chiama tooget getSyncTable (anziché getTable) una tabella di riferimento toohello locale.

    Il database locale di hello utilizza codice per tutti creare, leggere, aggiornare ed eliminazione (CRUD) nella tabella.

    In questo esempio si esegue una semplice gestione degli errori nei conflitti di sincronizzazione. Un'applicazione reale si gestisce hello diversi errori, ad esempio le condizioni della rete, server è in conflitto e altri. Per esempi di codice, vedere hello [esempio di sincronizzazione non in linea].

5. Successivamente, aggiungere la sincronizzazione di funzione tooperform hello effettivo.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Si decide quando toopush cambia back-end App Mobile toohello chiamando **syncContext.push()**. Ad esempio, è possibile chiamare **syncBackend** in un evento gestore tooa legati sincronizzazione pulsante.

## <a name="offline-sync-considerations"></a>Considerazioni sulla sincronizzazione offline

Nell'esempio hello hello **push** metodo **syncContext** viene chiamato solo all'avvio dell'app in funzione di callback hello per account di accesso.  In un'applicazione reale, è possibile apportare questa funzionalità di sincronizzazione attivata manualmente o quando cambia stato rete hello.

Quando viene eseguita un'operazione di pull in una tabella che è in sospeso aggiornamenti locali registrati dal contesto hello, che pull operazione automaticamente i trigger di push. Quando l'aggiornamento, l'aggiunta e il completamento di elementi in questo esempio, è possibile omettere hello esplicita **push** chiamare, perché potrebbe essere ridondante.

Nel codice hello fornito, tutti i record nella tabella todoItem remoto hello esecuzione di query, ma è anche possibile toofilter record passando un id di query e una query troppo**push**. Per ulteriori informazioni, vedere la sezione hello *sincronizzazione incrementale* in [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="optional-disable-authentication"></a>(Facoltativo) Disabilitare l'autenticazione

Se si non desidera tooset autenticazione prima di testare la sincronizzazione non in linea, impostare come commento la funzione di callback hello per account di accesso, ma lasciare hello codice all'interno di rimuovere la funzione di callback hello.  Dopo l'impostazione come commento le righe di account di accesso hello, codice hello seguente:

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

A questo punto, hello app esegue la sincronizzazione con il back-end Azure quando si esegue l'applicazione hello hello.

## <a name="run-hello-client-app"></a>Eseguire app di hello client
Con questo punto è abilitata la sincronizzazione non in linea, è possibile eseguire un'applicazione hello client almeno una volta in ogni piattaforma per popolare il database di archivio locale hello. In un secondo momento, simulare uno scenario offline e modificare i dati di hello nell'archivio locale hello mentre l'applicazione hello è offline.

## <a name="optional-test-hello-sync-behavior"></a>(Facoltativo) Testare il comportamento di sincronizzazione hello
In questa sezione è modificare hello client progetto toosimulate uno scenario offline tramite un URL dell'applicazione non valido per il back-end. Quando si aggiunge o modifica gli elementi di dati, queste modifiche vengono mantenute nell'archivio locale, ma non sono sincronizzati toohello archivio di dati back-end fino a quando non viene ristabilita la connessione di hello.

1. Nel hello Esplora soluzioni, aprire il file di progetto index.js hello e modificare hello applicazione URL toopoint a un URL non valido, ad esempio hello seguente codice:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. In index.html, aggiornare hello CSP `<meta>` elemento con hello stesso URL non valido.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Compilare ed eseguire app client hello e si noti che un'eccezione viene registrata nella console di hello quando hello app tenta di sincronizzarsi con back-end hello dopo l'accesso. I nuovi elementi che aggiunti esistono solo nell'archivio locale di hello fino a quando queste vengono inviate back-end mobile toohello. app client Hello si comporta come se fosse connesso toohello di back-end.

4. Chiudere l'applicazione hello e riavviarlo tooverify che è stato creato in base ai nuovi elementi hello siano archivio locale toohello persistente.

5. (Facoltativo) Utilizzare Visual Studio tooview toosee di tabella del Database SQL di Azure che hello dati nel database back-end hello non vengono modificati.

    In Visual Studio aprire **Esplora server**. Esplorare database tooyour **Azure**->**database SQL**. Fare clic con il pulsante destro del mouse sul database e scegliere **Apri in Esplora oggetti di SQL Server**. È possibile cercare tooyour tabella di database SQL e il relativo contenuto.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Facoltativo) Test hello riconnessione tooyour mobile back-end

In questa sezione si riconnette hello app toohello mobile back-end, che simula l'applicazione hello proveniente da uno stato online. Quando si accede, i dati sono back-end mobile tooyour sincronizzati.

1. Riaprire index.js e ripristinare l'URL dell'applicazione hello.
2. Riaprire index.html e correggere l'URL dell'applicazione hello in hello CSP `<meta>` elemento.
3. Ricompilare ed eseguire l'applicazione client hello. app Hello tenta toosync con back-end dell'app mobile hello dopo l'accesso. Verificare che nessuna eccezione vengono registrata nella console di debug hello.
4. (Facoltativo) Hello visualizzazione aggiornata dei dati utilizzando Esplora oggetti di SQL Server o uno strumento REST come Fiddler. Si noti hello dati sono stati sincronizzati tra i database di back-end hello e archivio locale hello.

    Avviso hello dati sincronizzati tra database hello e archivio locale hello e contiene elementi hello che aggiunti mentre l'app è stata disconnessa.

## <a name="additional-resources"></a>Risorse aggiuntive
* [sincronizzazione dati Offline nelle App mobili di Azure]
* [Visual Studio Tools per Apache Cordova]

## <a name="next-steps"></a>Passaggi successivi
* Esaminare più avanzate funzionalità di sincronizzazione non in linea, ad esempio la risoluzione dei conflitti in hello [esempio di sincronizzazione non in linea]
* Esaminare la sincronizzazione non in linea hello riferimento all'API in hello [documentazione dell'API](https://azure.github.io/azure-mobile-apps-js-client).

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[avvio rapido di Apache Cordova]: app-service-mobile-cordova-get-started.md
[esempio di sincronizzazione non in linea]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools per Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
