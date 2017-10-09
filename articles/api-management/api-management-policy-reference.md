---
title: aaaAzure API Gestione criteri di riferimento
description: Informazioni su hello criteri disponibili tooconfigure gestione API.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a>Informazioni di riferimento per i criteri di Gestione API di Azure
In questa sezione viene fornito un indice per i criteri di hello in hello [riferimento ai criteri di gestione API][API Management policy reference]. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API][Policies in API Management].

Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello. Alcuni criteri, ad esempio hello [flusso di controllo] [ Control flow] e [Imposta variabile] [ Set variable] criteri sono basati su espressioni di criteri. Per altre informazioni, vedere [Criteri avanzati][Advanced policies] ed [Espressioni di criteri][Policy expressions]

## <a name="policy-reference-index"></a>Indice delle informazioni di riferimento per i criteri
* [Criteri per le restrizioni sull'accesso][Access restriction policies]
  * [Controlla intestazione HTTP][Check HTTP header]: impone l'esistenza e/o il valore di un'intestazione HTTP.
  * [Limita frequenza delle chiamate per sottoscrizione][Limit call rate by subscription]: impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.
  * [Limita frequenza delle chiamate per chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey): impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.
  * [Limita IP chiamanti][Restrict caller IPs]: filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.
  * [Quota di utilizzo di set da sottoscrizione] [ Set usage quota by subscription] -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.
  * [Quota di utilizzo di set da chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.
  * [Convalida JWT][Validate JWT]: impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.
* [Criteri avanzati][Advanced policies]
  * [Flusso di controllo] [ Control flow] : in modo condizionale istruzioni dei criteri in base ai risultati di hello di valutazione di hello Boolean applica [espressioni][expressions].
  * [Inoltro della richiesta] [ Forward request] -inoltra servizio back-end di hello richiesta toohello.
  * [Log tooEvent Hub] [ Log tooEvent Hub] -invia messaggi hello destinazione del messaggio tooa specificato formato definito da un [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entità.
  * [Ripetere](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -esecuzione di tentativi di hello racchiuso tra istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione hello. Esecuzione viene ripetuto in intervalli di tempo specificati hello e backup toohello specificato numero di tentativi.
  * [Restituire una risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -hello di esecuzione e restituisce pipeline interruzioni specificato risposta direttamente toohello chiamante.
  * [Inviare una richiesta unidirezionale](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -invia una richiesta toohello URL specificato senza attendere una risposta.
  * [Invio richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -invia una richiesta toohello URL specificato.
  * [Impostare il metodo di richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -consente di determinare il metodo HTTP hello toochange per una richiesta.
  * [Impostare lo stato](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello di codice stato HTTP hello modifiche valore specificato.
  * [Imposta variabile][Set variable]: rende persistente un valore in una variabile [context][context] denominata e consente di accedervi in un momento successivo.
  * [Traccia](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -aggiunge una stringa hello [API controllo](api-management-howto-api-inspector.md) output.
  * [Attesa](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : richiesta di attesa per la trasmissione tra parentesi, ottenere valore dalla cache o controllare toocomplete criteri flusso prima di procedere.
* [Criteri di autenticazione][Authentication policies]
  * [Autenticazione di base][Authenticate with Basic]: consente di eseguire l'autenticazione con un servizio di back-end tramite l'autenticazione di base.
  * [Autentica con certificato client][Authenticate with client certificate]: consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.
* [Criteri di memorizzazione nella cache][Caching policies] 
  * [Recupera dalla cache][Get from cache]: esegue una ricerca nella cache e restituisce una risposta valida memorizzata nella cache, se disponibile.
  * [Archiviare toocache] [ Store toocache] -risposta cache in base toohello specificato configurazione del controllo della cache.
  * [Recupera valore dalla cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.
  * [Valore di memorizzare nella cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -archiviare un elemento nella cache di hello dalla chiave.
  * [Rimuovi valore dalla cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -rimuovere un elemento nella cache di hello dalla chiave.
* [Criteri tra domini][Cross domain policies] 
  * [Consentire le chiamate tra domini] [ Allow cross-domain calls] -rende accessibile hello API da client Adobe Flash e Microsoft Silverlight basati su browser.
  * [CORS] [ CORS] -aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.
  * [JSONP] [ JSONP] - aggiunge JSON con riempimento (JSONP) supporto tooan operazione o chiama un'API tooallow tra domini da client JavaScript basati su browser.
* [Criteri di trasformazione][Transformation policies] 
  * [Convertire JSON tooXML] [ Convert JSON tooXML] - richiesta converte o corpo della risposta da JSON tooXML.
  * [Convertire XML tooJSON] [ Convert XML tooJSON] - richiesta converte o corpo della risposta da XML tooJSON.
  * [Trova e sostituisci stringa nel corpo][Find and replace string in body]: trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.
  * [Maschera URL nel contenuto] [ Mask URLs in content] -riscrive (maschera) i collegamenti nella risposta hello corpo in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.
  * [Impostare il servizio back-end] [ Set backend service] -Modifica servizio back-end hello per una richiesta in ingresso.
  * [Impostare corpo] [ Set body] -imposta corpo del messaggio hello per le richieste in ingresso e in uscita.
  * [Intestazione HTTP set] [ Set HTTP header] - assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta o aggiunge una nuova intestazione di risposta e/o di richiesta.
  * [Imposta parametro di stringa di query][Set query string parameter]: aggiunge, sostituisce il valore o elimina il parametro di stringa della query di richiesta.
  * [Riscrittura URL] [ Rewrite URL] -converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulle espressioni di criteri, vedere hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


