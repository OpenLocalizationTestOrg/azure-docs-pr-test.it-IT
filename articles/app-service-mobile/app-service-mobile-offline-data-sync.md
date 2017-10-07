---
title: Sincronizzazione di dati in App mobili di Azure aaaOffline | Documenti Microsoft
description: "Panoramica della funzionalità di sincronizzazione di dati offline hello per App mobili di Azure e riferimento concettuale"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Sincronizzazione di dati offline nelle app per dispositivi mobili di Azure
## <a name="what-is-offline-data-sync"></a>Che cos'è la sincronizzazione di dati offline?
Sincronizzazione dati non in linea è un client e server SDK funzionalità delle App mobili di Azure che rende più semplice per gli sviluppatori toocreate applicazioni che funzionano senza una connessione di rete.

Quando l'app è in modalità offline, è possibile creare e modificare i dati vengono salvati tooa di archivio locale. Quando l'applicazione hello è tornata in linea, è possibile sincronizzare le modifiche locali con il back-end dell'App Mobile di Azure. Hello funzionalità include anche il supporto per il rilevamento dei conflitti quando hello stesso record viene modificato su entrambi client hello e hello back-end. I conflitti possono quindi essere gestiti nel server di hello o client hello.

La sincronizzazione offline presenta diversi vantaggi:

* Migliorare la velocità di risposta dell'applicazione memorizzando nella cache di dati del server in locale nel dispositivo hello
* Creare app affidabili che possono essere usate anche in caso di problemi di rete
* Consenti toocreate gli utenti finali e modificare i dati anche quando non si verifica alcun accesso alla rete, senza alcuna connettività con il supporto di scenari
* Sincronizzare i dati tra più dispositivi e rilevare i conflitti quando hello stesso record viene modificato da due dispositivi
* Limitare l'uso della rete in reti a latenza elevata o a consumo

Hello seguenti esercitazioni Mostra come tooadd non in linea sincronizzazione tooyour client mobili con App mobili di Azure:

* [Android: Abilitare la sincronizzazione offline]
* [Apache Cordova: Abilitare la sincronizzazione offline](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: Abilitare la sincronizzazione offline]
* [Xamarin iOS: Abilitare la sincronizzazione offline]
* [Xamarin Android: Abilitare la sincronizzazione offline]
* [Xamarin.Forms: Abilitare la sincronizzazione offline](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [Abilitare la sincronizzazione offline per l'app di Windows]

## <a name="what-is-a-sync-table"></a>Informazioni sulla tabella di sincronizzazione
hello tooaccess endpoint "/ tabelle", il client di dispositivi mobili di Azure hello SDK offrono le interfacce, ad esempio `IMobileServiceTable` (client di .NET SDK) o `MSTable` (iOS client). Queste API connettono direttamente back-end App Mobile Azure toohello e non riuscire se il dispositivo di client hello è una connessione di rete.

toosupport offline, l'app deve invece usare hello *tabella sincronizzazione* API, ad esempio `IMobileServiceSyncTable` (client di .NET SDK) o `MSSyncTable` (iOS client). Hello tutte le stesse operazioni CRUD (Create, Read, Update, Delete) funzionano con sincronizzazione tabella API, tranne che ora sono leggervi o scrivere tooa *archivio locale*. Prima di possono eseguire qualsiasi operazione di tabella di sincronizzazione, è necessario inizializzare l'archivio locale hello.

## <a name="what-is-a-local-store"></a>Informazioni sull'archivio locale
Un archivio locale è a livello di persistenza dei dati nel dispositivo client hello hello. il client di App mobili di Azure Hello SDK offrono impostazioni locali predefinite memorizzare implementazione. In Windows, Xamarin e Android è basato su SQLite, mentre in iOS è basato su Core Data.

toouse hello SQLite implementazione basata su Windows Phone o Windows Store 8.1, è necessario tooinstall un'estensione di SQLite. Per altre informazioni, vedere [Abilitare la sincronizzazione offline per l'app di Windows]. Android e iOS forniti con una versione di SQLite nel dispositivo hello sistema operativo, pertanto non è necessario tooreference la propria versione di SQLite.

Gli sviluppatori possono anche implementare il proprio archivio locale. Ad esempio, se si desiderano toostore dati in un formato crittografato nel client per dispositivi mobili hello, è possibile definire un archivio locale che utilizza SQLCipher per la crittografia.

## <a name="what-is-a-sync-context"></a>Informazioni sul contesto di sincronizzazione
Un *contesto di sincronizzazione* è associato a un oggetto client mobile, ad esempio `IMobileServiceClient` o `MSClient`, e tiene traccia delle modifiche apportate con le tabelle di sincronizzazione. contesto di sincronizzazione Hello gestisce un *coda operazione*, che mantiene un elenco ordinato di operazioni CUD (Create, Update, Delete) che in seguito viene inviato toohello server.

Un archivio locale è associato il contesto di sincronizzazione hello utilizzando un metodo di inizializzazione, ad esempio `IMobileServicesSyncContext.InitializeAsync(localstore)` in hello [client .NET SDK].

## <a name="how-sync-works"></a>Funzionamento della sincronizzazione offline
Quando si usano le tabelle di sincronizzazione, il codice client controlla quando le modifiche locali vengono sincronizzate con un back-end dell'app per dispositivi mobili di Azure. Non viene inviata back-end toohello fino a quando non c'è una chiamata*push* modifiche locali. Analogamente, archivio locale hello viene popolato con i nuovi dati solo se è presente una chiamata troppo*pull* dati.

* **Push**: Push è un'operazione nel contesto di sincronizzazione hello e invia tutte le modifiche CUD dall'ultimo push di hello. Si noti che è toosend non è possibile solo le modifiche di singole della tabella, perché in caso contrario le operazioni potrebbero essere inviate senza ordine. Push esegue una serie di REST chiamate tooyour App Mobile Azure back-end, che a sua volta modifica il database del server.
* **Pull**: Pull viene eseguito su una base per ogni tabella e può essere personalizzato con una query tooretrieve solo un subset dei dati del server hello. Hello client mobili di Azure SDK, quindi inserire i dati risultanti hello nell'archivio locale hello.
* **Push implicita**: se un'operazione di pull viene eseguita su una tabella che include aggiornamenti locali in sospeso, pull hello esegue innanzitutto un `push()` nel contesto di sincronizzazione hello. Questo comando consente di ridurre al minimo i conflitti tra le modifiche che sono già in coda e i nuovi dati dal server hello.
* **Sincronizzazione incrementale**: operazione pull toohello hello primo parametro è un *nome query* che viene utilizzato solo nel client hello. Se si utilizza un nome di query non null, hello Mobile di Azure SDK consente di eseguire un *sincronizzazione incrementale*. Ogni volta che un'operazione pull restituisce un set di risultati, hello più recente `updatedAt` timestamp da tale set di risultati vengono archiviati in tabelle di sistema locale SDK hello. Le operazioni pull successive recuperano solo i record successivi a tale timestamp.

  sincronizzazione incrementale toouse, il server deve restituire significativo `updatedAt` valori e deve essere utilizzato anche per supportare l'ordinamento in base a questo campo. Tuttavia, poiché hello SDK aggiunge il proprio ordinamento nel campo updatedAt hello, è possibile utilizzare una query pull che ha il proprio `orderBy` clausola.

  nome della query Hello può essere qualsiasi stringa desiderato, ma deve essere univoco per ogni query logici nell'applicazione.
  In caso contrario, le operazioni di pull diversi poteva sovrascrivere hello stesso timestamp sincronizzazione incrementale e le query possono restituire risultati non corretti.

  Se query hello ha un parametro, un modo toocreate un nome univoco di query è tooincorporate valore del parametro hello.
  Ad esempio, se si applica un filtro in base all'ID utente, il nome della query potrebbe essere analogo al seguente (in C#):

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Se si desidera tooopt non sincronizzati incrementale, passare `null` come hello ID di query. In questo caso, vengono recuperati tutti i record in ogni chiamata troppo`PullAsync`, che è potenzialmente inefficiente.
* **Eliminazione**: È possibile cancellare il contenuto di hello dell'uso di archivio locale hello `IMobileServiceSyncTable.PurgeAsync`.
  Eliminazione potrebbe essere necessario se si dispone di dati non aggiornati nel database di hello client o se si desiderano toodiscard tutte le modifiche in sospeso.

  Cancellazione Cancella una tabella dall'archivio locale hello. Se sono presenti operazioni in attesa di sincronizzazione con i database del server di hello, hello purge genera un'eccezione a meno che non hello *forzare l'eliminazione* parametro è impostato.

  Ad esempio di dati non aggiornati sul client hello, si supponga che nell'esempio di "elenco di attività" hello, Device1 contiene solo gli elementi che non vengono completati. Un oggetto todoitem "Comprare il Pane" è contrassegnato come completato nel server di hello da un altro dispositivo. Tuttavia, Device1 dispone ancora di hello todoitem "Comprare il Pane" nell'archivio locale perché solo effettua il pull di elementi che non sono contrassegnate come completate. Questo elemento non aggiornato viene cancellato da un'operazione di ripulitura.

## <a name="next-steps"></a>Passaggi successivi
* [iOS: Abilitare la sincronizzazione offline]
* [Xamarin iOS: Abilitare la sincronizzazione offline]
* [Xamarin Android: Abilitare la sincronizzazione offline]
* [Abilitare la sincronizzazione offline per l'app di Windows]

<!-- Links -->
[client .NET SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: Abilitare la sincronizzazione offline]: app-service-mobile-android-get-started-offline-data.md
[iOS: Abilitare la sincronizzazione offline]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: Abilitare la sincronizzazione offline]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: Abilitare la sincronizzazione offline]: app-service-mobile-xamarin-android-get-started-offline-data.md
[Abilitare la sincronizzazione offline per l'app di Windows]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
