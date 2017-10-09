---
title: criteri di gestione API aaaAzure | Documenti Microsoft
description: Informazioni sui criteri di hello disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>Criteri in Gestione API
In questa sezione fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  
  
 I criteri sono una potente funzionalità del sistema hello che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione. I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API. Le istruzioni più comuni includono la conversione di formato da XML tooJSON e limitare toorestrict hello quantità di chiamate in ingresso da uno sviluppatore di frequenza delle chiamate. Viene fornita hello disponibili molti altri criteri.  
  
 Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello. Alcuni criteri, ad esempio hello [flusso di controllo](api-management-advanced-policies.md#choose) e [Imposta variabile](api-management-advanced-policies.md#set-variable) criteri sono basati su espressioni di criteri. Per altre informazioni, vedere [Criteri avanzati](api-management-advanced-policies.md#AdvancedPolicies) ed [Espressioni di criteri](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Criteri  
  
-   [Criteri di limitazione dell'accesso](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [check-header](api-management-access-restriction-policies.md#CheckHTTPHeader) : impone l'esistenza e/o il valore di un'intestazione HTTP.  
  
    -   [Limita frequenza delle chiamate per sottoscrizione](api-management-access-restriction-policies.md#LimitCallRate) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.  
  
    -   [Limita frequenza delle chiamate per chiave](api-management-access-restriction-policies.md#LimitCallRateByKey) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.  
  
    -   [ip-filter](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.  
  
    -   [Quota di utilizzo di set da sottoscrizione](api-management-access-restriction-policies.md#SetUsageQuota) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.  
  
    -   [Quota di utilizzo di set da chiave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.  
  
    -   [validate-JWT](api-management-access-restriction-policies.md#ValidateJWT) : impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.  
  
-   [Criteri avanzati](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Flusso di controllo](api-management-advanced-policies.md#choose) : in modo condizionale applica istruzioni dei criteri in base a hello valutazione delle espressioni booleane.  
  
    -   [Inoltro della richiesta](api-management-advanced-policies.md#ForwardRequest) -inoltra servizio back-end di hello richiesta toohello.  
  
    -   [Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -invia messaggi hello formato specificato tooa messaggio destinazione definita da un'entità del Logger.  
  
    -   [Ripetere](api-management-advanced-policies.md#Retry) -esecuzione di tentativi di hello racchiuso tra istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione hello. Esecuzione viene ripetuto in intervalli di tempo specificati hello e backup toohello specificato numero di tentativi.  
  
    -   [Restituire una risposta](api-management-advanced-policies.md#ReturnResponse) -hello di esecuzione e restituisce pipeline interruzioni specificato risposta direttamente toohello chiamante.  
  
    -   [Inviare una richiesta unidirezionale](api-management-advanced-policies.md#SendOneWayRequest) -invia una richiesta toohello URL specificato senza attendere una risposta.  
  
    -   [Invio richiesta](api-management-advanced-policies.md#SendRequest) -invia una richiesta toohello URL specificato.  
  
    -   [Imposta variabile](api-management-advanced-policies.md#set-variable): rende persistente un valore in una variabile di contesto denominata e consente di accedervi in un momento successivo.  
  
    -   [Impostare il metodo di richiesta](api-management-advanced-policies.md#SetRequestMethod) -consente di determinare il metodo HTTP hello toochange per una richiesta.  
  
    -   [Impostare il codice di stato](api-management-advanced-policies.md#SetStatus) -toohello di codice stato HTTP hello modifiche valore specificato.  
  
    -   [Traccia](api-management-advanced-policies.md#Trace) -aggiunge una stringa hello [API controllo](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.  
  
    -   [Attesa](api-management-advanced-policies.md#Wait) -attende racchiusi [richiesta di invio](api-management-advanced-policies.md#SendRequest), [ottenere valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey), o [flusso di controllo](api-management-advanced-policies.md#choose) toocomplete criteri prima di procedere.  
  
-   [Criteri di autenticazione](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [authentication-basic](api-management-authentication-policies.md#Basic) : consente di eseguire l'autenticazione con un servizio back-end tramite l'autenticazione di base.  
  
    -   [authentication-certificate](api-management-authentication-policies.md#ClientCertificate) : consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.  
  
-   [Criteri di memorizzazione nella cache](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Recupera dalla cache](api-management-caching-policies.md#GetFromCache) : esegue una ricerca nella cache e restituisce una risposta valida memorizzata nella cache, se disponibile.  
  
    -   [Archiviare toocache](api-management-caching-policies.md#StoreToCache) -risposta cache in base toohello specificato configurazione del controllo della cache.  
  
    -   [Recupera valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.  
  
    -   [Valore di memorizzare nella cache](api-management-caching-policies.md#StoreToCacheByKey) -archiviare un elemento nella cache di hello dalla chiave.  
  
    -   [Rimuovi valore dalla cache](api-management-caching-policies.md#RemoveCacheByKey) -rimuovere un elemento nella cache di hello dalla chiave.  
  
-   [Criteri tra domini](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Consentire le chiamate tra domini](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rende accessibile hello API da client Adobe Flash e Microsoft Silverlight basati su browser.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - aggiunge JSON con riempimento (JSONP) supporto tooan operazione o chiama un'API tooallow tra domini da client JavaScript basati su browser.  
  
-   [Criteri di trasformazione](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Convertire JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - richiesta converte o corpo della risposta da JSON tooXML.  
  
    -   [Convertire XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - richiesta converte o corpo della risposta da XML tooJSON.  
  
    -   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody) : trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.  
  
    -   [Maschera URL nel contenuto](api-management-transformation-policies.md#MaskURLSContent) -riscrive (maschera) i collegamenti nella risposta hello corpo in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.  
  
    -   [Impostare il servizio back-end](api-management-transformation-policies.md#SetBackendService) -Modifica servizio back-end hello per una richiesta in ingresso.  
  
    -   [Impostare corpo](api-management-transformation-policies.md#SetBody) -imposta corpo del messaggio hello per le richieste in ingresso e in uscita.  
  
    -   [Intestazione HTTP set](api-management-transformation-policies.md#SetHTTPheader) - assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta o aggiunge una nuova intestazione di risposta e/o di richiesta.  
  
    -   [Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) : aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.  
  
    -   [Riscrittura URL](api-management-transformation-policies.md#RewriteURL) -converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello.  
  
    -   [Trasformare XML utilizzando XSLT](api-management-transformation-policies.md#XSLTransform) -si applica un tooXML trasformazione XSL nel corpo della richiesta o risposta hello.  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  
