---
title: Panoramica di aaaMedia servizi operazioni API REST | Documenti Microsoft
description: Informazioni generali sull'API REST di Servizi multimediali
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Informazioni generali sull'API REST di Servizi multimediali
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Hello **REST operazioni di servizi multimediali** API viene usata per la creazione di processi, asset, i criteri di accesso e altre operazioni su oggetti in un account del servizio di supporto. Per altre informazioni, vedere le [informazioni di riferimento sull'API REST di Servizi multimediali](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Servizi multimediali di Microsoft Azure è un servizio che accetta richieste HTTP basate su OData e può rispondere in formato JSON dettagliato o atom+pub. Poiché servizi multimediali è conforme tooAzure linee guida di progettazione, è un set di intestazioni HTTP obbligatorie che ogni client deve utilizzare quando ci si connette tooMedia servizi, nonché un set di intestazioni facoltative che può essere utilizzato. Hello nelle sezioni seguenti vengono descritte le intestazioni di hello e verbi HTTP, è possibile utilizzare quando le richieste di creazione e la ricezione di risposte da servizi multimediali.

In questo argomento viene fornita una panoramica di come toouse REST v2 con servizi multimediali.

## <a name="considerations"></a>Considerazioni

Hello considerazioni seguenti si applica quando si usa REST.

* Quando una query sulle entità, è previsto un limite di 1000 entità restituito in una sola volta perché v2 REST pubblici limita risultati too1000 risultati della query. È necessario toouse **Skip** e **richiedere** (.NET) / **top** (REST) come descritto in [in questo esempio .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) e [questa API REST esempio](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Quando si utilizza JSON e specificando hello toouse **Metadata** (parola chiave) nella richiesta di hello (ad esempio, un oggetto collegato tooreferences) è necessario impostare hello **Accept** intestazione troppo[formato JSON dettagliato ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (vedere il seguente esempio hello). OData non riconosce hello **Metadata** richiedere proprietà in hello, a meno che non si imposta la proprietà tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Intestazioni delle richieste HTTP standard supportate da Servizi multimediali
Per ogni chiamata in servizi multimediali, è presente un set di intestazioni obbligatorie è necessario includere nella richiesta e anche un set di intestazioni facoltative è tooinclude. Hello seguente tabella elenca hello richiesto intestazioni:

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| Authorization |Bearer |Bearer è hello accettate solo meccanismo di autorizzazione. valore di Hello deve includere anche il token di accesso hello fornito da ACS. |
| x-ms-version |Decimale |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Poiché servizi multimediali Usa OData tooexpose l'archivio di metadati di asset sottostante tramite le API REST, hello DataServiceVersion e MaxDataServiceVersion intestazioni deve essere incluse in tutte le richieste; Tuttavia, se non lo sono, quindi attualmente servizi multimediali suppone che il valore di DataServiceVersion hello in uso sia 3.0.
> 
> 

di seguito Hello è un set di intestazioni facoltative:

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| Date |Data RFC 1123 |Timestamp della richiesta di hello |
| Accept |Tipo di contenuto |Hello richiesto tipo di contenuto per la risposta hello come illustrato di seguito hello:<p> -application/json;odata=verbose<p> - application/atom+xml<p> Le risposte potrebbero essere un tipo di contenuto diversi, ad esempio un'operazione di recupero di blob, in cui una risposta corretta contiene flusso blob hello come payload di hello. |
| Accept-Encoding |Gzip, deflate |Codifica GZIP e DEFLATE, se applicabile. Nota: in caso di risorse di grandi dimensioni, Servizi multimediali può ignorare questa intestazione e restituire dati non compressi. |
| Accept-Language |"en", "es" e così via. |Specifica la lingua hello preferito per la risposta hello. |
| Accept-Charset |Tipo di set di caratteri, ad esempio "UTF-8" |L'impostazione predefinita è UTF-8. |
| X-HTTP-Method |Metodo HTTP |Consente ai client o firewall che non supportano metodi HTTP come PUT o DELETE toouse questi metodi, con tunneling tramite una chiamata GET. |
| Content-Type |Tipo di contenuto |Tipo di contenuto del corpo della richiesta hello nelle richieste PUT o POST. |
| client-request-id |String |Un valore definito dal chiamante che identifica hello richiesta specificato. Se specificato, questo valore verrà incluso nel messaggio di risposta hello come una richiesta di hello toomap modo. <p><p>**Importante**<p>Le dimensioni di questi valori dovrebbero essere limitate a 2096 b (2 k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Intestazioni delle risposte HTTP standard supportate da Servizi multimediali
di seguito Hello è un set di intestazioni che possono essere restituiti tooyou a seconda della risorsa hello che richiesta e hello azione si intendeva tooperform.

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| request-id |String |Identificatore univoco per l'operazione corrente di hello, servizio generato. |
| client-request-id |String |Un identificatore specificato dal chiamante hello nella richiesta originale hello, se presente. |
| Date |Data RFC 1123 |Data di Hello è stata elaborata la richiesta di hello. |
| Content-Type |Variabile |tipo di contenuto Hello del corpo della risposta hello. |
| Content-Encoding |Variabile |Gzip o deflate, a seconda delle esigenze. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Verbi HTTP standard supportati da Servizi multimediali
di seguito Hello è un elenco completo dei verbi HTTP che può essere usato quando creazione di richieste HTTP:

| Verbo | Descrizione |
| --- | --- |
| GET |Restituisce hello valore corrente di un oggetto. |
| POST |Crea un oggetto basato su dati hello forniti o invia un comando. |
| PUT |Sostituisce un oggetto o ne crea uno nuovo con nome, se applicabile. |
| DELETE |Elimina un oggetto. |
| MERGE |Aggiorna un oggetto esistente con le modifiche alle proprietà denominate. |
| HEAD |Restituisce i metadati di un oggetto per una risposta GET. |

## <a name="discover-media-services-model"></a>Individuare il modello di Servizi multimediali
toomake servizi multimediali le entità più facilmente individuabili, operazione hello $metadata possono essere utilizzate. Consente di tooretrieve tutti i tipi di entità valido, le proprietà delle entità, associazioni, funzioni, azioni e così via. Hello esempio seguente viene illustrato come tooconstruct hello URI: https://media.windows.net/API/$ metadata.

È consigliabile aggiungere "? api-version=2.x" toohello fine hello URI se si desidera tooview hello metadati in un browser o di non inclusa l'intestazione x-ms-version hello nella richiesta.

## <a name="connect-toomedia-services"></a>Connessione dei servizi tooMedia

Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.

## <a name="next-steps"></a>Passaggi successivi

tooaccess APIs AMS con REST, vedere [usano Azure AD authentication tooaccess hello Azure API dei servizi multimediali con REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

