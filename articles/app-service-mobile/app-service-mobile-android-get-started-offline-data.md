---
title: aaaEnable sincronizzazione offline per l'App Mobile di Azure (Android)
description: Informazioni su come toouse App per dispositivi mobili del servizio App toocache e sincronizzazione dati offline nell'applicazione Android
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Abilitare la sincronizzazione offline per l'app per dispositivi mobili di Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione vengono illustrate funzionalità di sincronizzazione non in linea hello di App mobili di Azure per Android. Sincronizzazione non in linea consente toointeract gli utenti finali con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete. Le modifiche vengono archiviate in un database locale. Una volta dispositivo hello è tornata in linea, queste modifiche vengono sincronizzate con back-end remoto hello.

Se questa è la prima esperienza con App mobili di Azure, è necessario completare prima esercitazione hello [crea un'App Android]. Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario aggiungere hello dati estensione pacchetti tooyour di Microsoft Access. Per ulteriori informazioni sui pacchetti di estensione di server, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn sulle funzionalità di sincronizzazione non in linea hello, vedere l'argomento hello [sincronizzazione dati Offline nelle App mobili di Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Aggiornamento di sincronizzazione non in linea di hello app toosupport
Con la sincronizzazione offline, leggere scrittura tooand da un *tabella sincronizzazione* (utilizzando hello *IMobileServiceSyncTable* interfaccia), che fa parte di un **SQLite** database sul dispositivo.

toopush e pull delle modifiche tra il dispositivo di hello e servizi mobili di Azure, utilizzare un *contesto di sincronizzazione* (*MobileServiceClient.SyncContext*), che è inizializzare con database locali hello toostore dati in locale.

1. In `TodoActivity.java`, impostare come commento la definizione esistente di hello `mToDoTable` e rimuovere il commento di versione di hello sincronizzazione tabella:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. In hello `onCreate` (metodo), impostare come commento l'inizializzazione esistente hello di `mToDoTable` e rimuovere il commento da questa definizione:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. In `refreshItemsFromTable` commento hello definizione di `results` e rimuovere il commento da questa definizione:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Commento hello definizione di `refreshItemsFromMobileServiceTable`.
5. Rimuovere il commento definizione hello di `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Rimuovere il commento definizione hello di `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Test hello app
In questa sezione, verificare il comportamento di hello con Wi-Fi in e quindi disattivare Wi-Fi toocreate uno scenario non in linea.

Quando si aggiungono elementi di dati, vengono mantenuti nell'archivio SQLite locale hello, ma servizio mobile toohello non sincronizzato finché non si preme hello **aggiornamento** pulsante. Altre applicazioni potrebbero avere requisiti diversi riguardanti quando i dati devono toobe sincronizzato, ma per scopi dimostrativi per questa esercitazione sono utente hello richiederlo in modo esplicito.

Quando si preme il pulsante, viene avviata una nuova attività in background. Viene innanzitutto inserito tutte le modifiche apportate toohello archivio locale utilizzando il contesto di sincronizzazione, quindi modificato pull tutti i dati dalla tabella locale toohello Azure.

### <a name="offline-testing"></a>Test offline
1. Sul posto hello dispositivo o il simulatore in *modalità aereo*. in modo da creare uno scenario offline.
2. Aggiungere alcuni elementi *ToDo* o contrassegnare alcuni elementi come completati. Chiudere hello dispositivo o simulatore (o app hello chiusura forzata) e riavviare. Verificare che le modifiche sono state mantenute nel dispositivo hello momento che vengono mantenuti nell'archivio di SQLite locale hello.
3. Visualizzare il contenuto di hello di hello Azure *TodoItem* della tabella con uno strumento SQL, ad esempio *SQL Server Management Studio*, o un client REST, ad esempio *Fiddler* o  *Postman*. Verificare che dispongano di nuovi elementi hello *non* stati sincronizzati toohello server
   
       + Per un back-end di Node.js, visitare toohello [portale di Azure](https://portal.azure.com/), nell'App Mobile back-end, fare clic su **tabelle facile** > **TodoItem** contenuto hello tooview di hello `TodoItem` tabella.
       + Per un back-end .NET, tabella hello visualizzazione contenuto o con uno strumento SQL, ad esempio *SQL Server Management Studio*, o un client REST, ad esempio *Fiddler* o *Postman*.
4. Attivare Wi-Fi nel dispositivo hello o un simulatore. Premere quindi hello **aggiornamento** pulsante.
5. Visualizzare di nuovo dati TodoItem hello in hello portale di Azure. Hello che dovrebbe ora apparire TodoItems nuove e modificate.

## <a name="additional-resources"></a>Risorse aggiuntive
* [sincronizzazione dati Offline nelle App mobili di Azure]
* [Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure] \(Nota: hello video si trova in servizi mobili, ma non in linea sincronizzazione funziona in modo analogo in App mobili di Azure\)

<!-- URLs. -->

[sincronizzazione dati Offline nelle App mobili di Azure]: app-service-mobile-offline-data-sync.md

[crea un'App Android]: app-service-mobile-android-get-started.md

[Cloud Cover: La sincronizzazione non in linea in servizi mobili di Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

