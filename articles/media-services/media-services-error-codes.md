---
title: codici di errore di servizi multimediali aaaAzure | Documenti Microsoft
description: Hello argomento viene fornita una panoramica dei codici di errore di servizi multimediali di Azure.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Codici di errore di Servizi multimediali di Azure
Quando si usa servizi multimediali di Microsoft Azure, si potrebbero ricevere i codici di errore HTTP dal servizio hello a seconda di problemi, ad esempio i token di autenticazione scade tooactions che non sono supportati in servizi multimediali. Hello seguito è riportato un elenco di **codici errore HTTP** che possono essere restituiti da servizi multimediali e le hello possibili le cause.  

## <a name="400-bad-request"></a>400 - Richiesta non valida
contiene informazioni non valide e viene rifiutato a causa di richiesta di Hello tooone di hello seguenti motivi:

* Viene specificata una versione API non supportata. Per la versione più recente di hello, vedere [il programma di installazione per lo sviluppo di API REST di servizi multimediali](media-services-rest-how-to-use.md).
* versione di Hello API di servizi multimediali non è specificato. Per informazioni su come toospecify hello versione dell'API, vedere [riferimento all'API REST di Media Services operazioni](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Se si utilizza tooMedia tooconnect .NET o Java SDK di hello servizi, hello versione API viene specificata automaticamente ogni volta che si prova e di eseguire un'azione in servizi multimediali.
  > 
  > 
* Viene specificata una proprietà non definita. nome della proprietà Hello è nel messaggio di errore hello. Solo le proprietà che fanno parte di una determinata entità possono essere specificate. Per un elenco delle entità e delle relative proprietà, vedere [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) (Informazioni di riferimento relative all'API REST di Servizi multimediali di Azure).
* Viene specificato un valore di proprietà non valido. nome della proprietà Hello è nel messaggio di errore hello. Vedere il collegamento precedente di hello per tipi di proprietà valido e i relativi valori.
* Il valore di una proprietà risulta mancante ed è obbligatorio.
* Parte dell'URL hello specificato contiene un valore non valido.
* È stato eseguito un tentativo effettuato tooupdate una proprietà WriteOnce.
* È stato eseguito un tentativo effettuato toocreate un processo che dispone di un Asset di input con un elemento AssetFile primario che non è stato specificato o non può essere determinato.
* È stato eseguito un tentativo effettuato tooupdate un localizzatore SAS. I localizzatori di firma di accesso condiviso possono solo essere creati o eliminati. I localizzatori di flusso possono essere aggiornati. Per altre informazioni, vedere [Locators](https://docs.microsoft.com/rest/api/media/operations/locator) (Localizzatori).
* È stata inviata un'operazione o una query non supportata.

## <a name="401-unauthorized"></a>401 - Non autorizzato
Hello richiesta non è stata autenticata (prima che possa essere autorizzato) scadenza tooone di hello seguenti motivi:

* L'intestazione di autenticazione risulta mancante.
* Il valore dell'intestazione di autenticazione non è valido.
  * token Hello è scaduto. 
  * token Hello contiene una firma non valida.

## <a name="403-forbidden"></a>403 - Accesso negato
Hello richiesta non è consentita scadenza tooone di hello seguenti motivi:

* Hello account di servizi multimediali non è stato trovato o è stato eliminato.
* account di servizi multimediali Hello è disabilitata e il tipo di richiesta di hello non HTTP GET. Le operazioni del servizio restituiranno una risposta 403.
* Hello token di autenticazione non contiene informazioni sulle credenziali dell'utente hello: AccountName e/o SubscriptionId. È possibile trovare queste informazioni in hello estensione dell'interfaccia utente servizi di supporto per l'account di servizi multimediali nel portale di gestione Azure hello.
* Impossibile accedere a risorse Hello.
  
  * È stato eseguito un tentativo effettuato toouse un processore di contenuti multimediali che non è disponibile per l'account di servizi multimediali.
  * Si è cercato tooupdate un'entità JobTemplate definita da servizi multimediali.
  * È stato eseguito un tentativo effettuato toooverwrite indicatore di posizione di altro account servizi multimediali.
  * È stato eseguito un tentativo effettuato toooverwrite ContentKey di altro account servizi multimediali.
* Impossibile creare la risorsa Hello a causa di quote del servizio tooa che è stato raggiunto per l'account di servizi multimediali hello. Per ulteriori informazioni sulle quote di servizio hello, vedere [quote e limitazioni](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 - Non trovato
richiesta di Hello non è consentita su una risorsa tooone a causa di hello seguenti motivi:

* È stato eseguito un tentativo effettuato tooupdate un'entità che non esiste.
* È stato eseguito un tentativo effettuato toodelete un'entità che non esiste.
* È stato eseguito un tentativo effettuato toocreate un'entità che si collega tooan entità che non esiste.
* È stato eseguito un tentativo effettuato tooGET un'entità che non esiste.
* È stato eseguito un tentativo effettuato toospecify un account di archiviazione che non è associato a hello account di servizi multimediali.  

## <a name="409-conflict"></a>409 - Conflitto
Hello richiesta non è consentita scadenza tooone di hello seguenti motivi:

* Più di un elemento AssetFile con nome specificato di hello all'interno di hello Asset.
* È stata tentata toocreate una seconda primario AssetFile all'interno di hello Asset.
* È stato effettuato un tentativo di un'entità ContentKey con hello toocreate specificato Id già in uso.
* È stato effettuato un tentativo toocreate un localizzatore con hello specificato Id già in uso.
* Più entità IngestManifestFile con nome specificato di hello all'interno di hello entità IngestManifest.
* È stato eseguito un tentativo effettuato toolink un secondo toohello ContentKey crittografia di archiviazione Asset crittografato di archiviazione.
* È stato effettuato un tentativo toolink hello toohello ContentKey stesso Asset.
* Toocreate tooan un localizzatore Asset cui contenitore di archiviazione è mancante o non è più associato hello Asset è stato effettuato un tentativo.
* È stato eseguito un tentativo effettuato toocreate tooan un localizzatore che dispone già di 5 localizzatori in uso. (Archiviazione di azure impone il limite di hello di cinque criteri di accesso condiviso in un contenitore di archiviazione).
* Il collegamento di account di archiviazione di un'entità IngestManifestAsset di tooan Asset non hello uguale all'account di archiviazione hello utilizzato dall'elemento padre di hello entità IngestManifest.  

## <a name="500-internal-server-error"></a>500 - Errore interno del server
Durante l'elaborazione di hello della richiesta di hello, servizi multimediali si verifica un errore che impedisce l'elaborazione di hello non potrà continuare. Questo potrebbe essere stato causato tooone di hello seguenti motivi:

* Creazione di un'attività o un processo ha esito negativo perché le informazioni sulla quota dell'account di servizi multimediali hello servizio è temporaneamente non disponibile.
* Creazione di un contenitore di archiviazione blob Asset o l'entità IngestManifest ha esito negativo perché informazioni sull'account di archiviazione dell'account hello è temporaneamente non disponibile.
* Un altro errore imprevisto.

## <a name="503-service-unavailable"></a>503 - Servizio non disponibile
server Hello è attualmente in grado di tooreceive richieste. Questo errore può essere causato dal servizio toohello un numero eccessivo di richieste. Meccanismo di limitazione di servizi multimediali limita l'utilizzo delle risorse di hello per le applicazioni che esegue un numero eccessivo di richieste al servizio toohello.

> [!NOTE]
> Controllo hello errore messaggio ed errore codice stringa tooget ulteriori informazioni sul motivo hello ottenuto hello errore HTTP 503. Questo errore non indica necessariamente la limitazione delle richieste.
> 
> 

Possibili descrizioni dello stato sono:

* "Il server è occupato. Esecuzioni precedenti di questo tipo di richiesta hanno impiegato più di {0} secondi."
* "Il server è occupato. Più di {0} richieste al secondo possono essere limitate."
* "Il server è occupato. Più di {0} richieste in {1} secondi possono essere limitate."

toohandle questo errore, si consiglia di utilizzare la logica di tentativi con backoff esponenziale. Ciò significa usare attese progressivamente più lunghe tra le ripetizioni dei tentativi per le risposte di errore consecutive.  Per altre informazioni, vedere [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx) (Blocco di applicazioni per la gestione degli errori temporanei).

> [!NOTE]
> Se si utilizza [Azure Media Services SDK per .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), è stata implementata la logica di riesecuzione hello per correggere l'errore 503 hello da hello SDK.  
> 
> 

## <a name="see-also"></a>Vedere anche
[Codici di errore di gestione di Servizi multimediali](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

