---
title: Informazioni generali sull'API REST di Servizi multimediali | Microsoft Docs
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
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Informazioni generali sull'API REST di Servizi multimediali
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

L'**API REST di Servizi multimediali** viene usata per la creazione di processi, asset, criteri di accesso e altre operazioni sugli oggetti in un account di Servizi multimediali. Per altre informazioni, vedere le [informazioni di riferimento sull'API REST di Servizi multimediali](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Servizi multimediali di Microsoft Azure è un servizio che accetta richieste HTTP basate su OData e può rispondere in formato JSON dettagliato o atom+pub. Poiché Servizi multimediali è conforme alle linee guida di progettazione di Azure, esiste un set di intestazioni HTTP obbligatorie che devono essere usate da ogni client per la connessione a Servizi multimediali, oltre a un set di intestazioni facoltative. Le seguenti sezioni descrivono le intestazioni e i verbi HTTP che è possibile usare quando si creano richieste e si ricevono risposte da Servizi multimediali.

Questo argomento offre una panoramica su come usare REST v2 con Servizi multimediali.

## <a name="considerations"></a>Considerazioni

Quando si usa REST, si applicano le considerazioni seguenti:

* Quando si esegue una query di entità, è previsto un limite di 1000 entità restituite in una sola volta perché la versione 2 pubblica di REST limita i risultati della query a 1000 risultati. È necessario usare **Skip** e **Take** (.NET)/**top** (REST) come descritto in [questo esempio .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) e in [questo esempio di API REST](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Se si usa JSON e si specifica di usare la parola chiave **__metadata** nella richiesta, ad esempio, per fare riferimento a un oggetto collegato, SI DEVE impostare l'intestazione **Accept** sul [formato JSON Verbose](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/). Vedere l'esempio seguente. OData non riconosce la proprietà **__metadata** nella richiesta, a meno che non venga impostata su verbose.  
  
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
Per ogni chiamata effettuata in Servizi multimediali, è necessario includere nella richiesta un set di intestazioni obbligatorie ed eventualmente un set di intestazioni facoltative. Nella seguente tabella sono elencate le intestazioni obbligatorie:

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| Authorization |Bearer |Bearer è l'unico meccanismo di autorizzazione accettato. Il valore deve includere anche il token di accesso fornito da ACS. |
| x-ms-version |Decimale |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Poiché Servizi multimediali usa OData per esporre l'archivio di metadati di asset sottostante tramite le API REST, le intestazioni DataServiceVersion e MaxDataServiceVersion devono essere incluse in tutte le richieste. Se non vengono incluse, Servizi multimediali suppone che il valore di DataServiceVersion in uso sia 3.0.
> 
> 

Nella seguente tabella è riportato un set di intestazioni facoltative:

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| Date |Data RFC 1123 |Timestamp della richiesta. |
| Accept |Tipo di contenuto |Tipo di contenuto richiesto per la risposta, ad esempio:<p> -application/json;odata=verbose<p> - application/atom+xml<p> Nelle risposte può essere presente un tipo di contenuto diverso, ad esempio di recupero BLOB. In questo caso, una risposta corretta deve contenere il flusso BLOB come payload. |
| Accept-Encoding |Gzip, deflate |Codifica GZIP e DEFLATE, se applicabile. Nota: in caso di risorse di grandi dimensioni, Servizi multimediali può ignorare questa intestazione e restituire dati non compressi. |
| Accept-Language |"en", "es" e così via. |Lingua preferita per la risposta. |
| Accept-Charset |Tipo di set di caratteri, ad esempio "UTF-8" |L'impostazione predefinita è UTF-8. |
| X-HTTP-Method |Metodo HTTP |Consente ai client o ai firewall che non supportano metodi HTTP come PUT o DELETE di usarli, con tunneling tramite una chiamata GET. |
| Content-Type |Tipo di contenuto |Tipo di contenuto del corpo delle richieste PUT o POST. |
| client-request-id |String |Valore definito dal chiamante che identifica la richiesta fornita. Se specificato, questo valore viene incluso nel messaggio di risposta per consentire il mapping della richiesta. <p><p>**Importante**<p>Le dimensioni di questi valori dovrebbero essere limitate a 2096 b (2 k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Intestazioni delle risposte HTTP standard supportate da Servizi multimediali
Nella seguente tabella è riportato un set di intestazioni che possono essere restituite a seconda della risorsa richiesta e dell'azione che si intende eseguire.

| Intestazione | Tipo | Valore |
| --- | --- | --- |
| request-id |String |Identificatore univoco per l'operazione corrente, generato dal servizio. |
| client-request-id |String |Identificatore specificato dal chiamante nella richiesta originale, se presente. |
| Date |Data RFC 1123 |Data di elaborazione della richiesta. |
| Content-Type |Variabile |Tipo di contenuto del corpo della risposta. |
| Content-Encoding |Variabile |Gzip o deflate, a seconda delle esigenze. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Verbi HTTP standard supportati da Servizi multimediali
Nella seguente tabella è riportato l'elenco completo dei verbi HTTP che è possibile usare per la creazione di richieste HTTP:

| Verbo | Descrizione |
| --- | --- |
| GET |Restituisce il valore corrente di un oggetto. |
| POST |Crea un oggetto in base ai dati forniti o invia un comando. |
| PUT |Sostituisce un oggetto o ne crea uno nuovo con nome, se applicabile. |
| DELETE |Elimina un oggetto. |
| MERGE |Aggiorna un oggetto esistente con le modifiche alle proprietà denominate. |
| HEAD |Restituisce i metadati di un oggetto per una risposta GET. |

## <a name="discover-media-services-model"></a>Individuare il modello di Servizi multimediali
Per rendere più facilmente individuabili le entità di Servizi multimediali, è possibile usare l'operazione $metadata, che consente di recuperare tutti i tipi validi di entità, le proprietà di entità, le associazioni, le funzioni, le azioni e così via. L'esempio seguente illustra come costruire l'URI: https://media.windows.net/API/$metadata.

Aggiungere "?api-version=2.x" alla fine dell'URI se si desidera visualizzare i metadati in un browser o se nella richiesta non è stata inclusa l'intestazione x-ms-version.

## <a name="connect-to-media-services"></a>Connettersi a Servizi multimediali

Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali. Le chiamate successive dovranno essere effettuate al nuovo URI.

## <a name="next-steps"></a>Passaggi successivi

Per accedere all'API di AMS con REST, vedere [Usare l'autenticazione di Azure AD per accedere all'API Servizi multimediali di Microsoft Azure con REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

