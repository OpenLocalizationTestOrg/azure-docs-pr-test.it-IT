---
title: rete CDN di Azure con CORS aaaUsing | Documenti Microsoft
description: Informazioni su come toouse hello Azure rete CDN (Content Delivery) toowith condivisione delle risorse Multiorigine (CORS).
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Uso della rete CDN di Azure con CORS
## <a name="what-is-cors"></a>Informazioni su CORS
CORS (Cross Origin Resource Sharing) è una funzionalità HTTP che consente a un'applicazione web in esecuzione risorse di tooaccess in un dominio in un altro dominio. In ordine tooreduce hello possibilità di attacchi di script, tutti i browser moderni implementano una restrizione di sicurezza nota come [criteri stessa origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Questo impedisce a una pagina Web di chiamare le API in un dominio diverso.  Condivisione CORS offre una sezione relativa al toocall dei (dominio di origine hello) di un'origine di in modo sicuro tooallow in un'altra origine API.

## <a name="how-it-works"></a>Funzionamento
Esistono due tipi di richieste CORS, le *richieste semplici* e le *richieste complesse*.

### <a name="for-simple-requests"></a>Per le richieste semplici:

1. browser Hello Invia richiesta CORS hello con un'ulteriore **origine** intestazione della richiesta HTTP. il valore di Hello di questa intestazione è origine hello resi hello padre pagina nella quale è definito come combinazione di hello di *protocollo,* *dominio* e *porta.*  Quando una pagina da https://www.contoso.com tenta tooaccess dati di un utente in origine fabrikam.com hello, hello dopo l'intestazione della richiesta verrà inviata toofabrikam.com:

   `Origin: https://www.contoso.com`

2. server Hello può rispondere con hello seguenti:

   * Un'intestazione **Access-Control-Allow-Origin** presente nella risposta, per indicare il sito di origine consentito. ad esempio:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Codice di errore HTTP, ad esempio 403 se hello server non consente la richiesta multiorigine hello dopo il controllo intestazione Origin hello

   * Un'intestazione **Access-Control-Allow-Origin** con un carattere jolly che consente tutte le origini:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Per le richieste complesse:

Una richiesta complessa è una richiesta CORS in browser hello toosend richiesto un *richiesta preliminare* (vale a dire una verifica preliminare) prima di inviare una richiesta CORS effettiva hello. Hello richiesta preliminare richiede autorizzazione server hello se richiesta CORS originale hello può proseguire e un `OPTIONS` richiesta toohello stesso URL.

> [!TIP]
> Per ulteriori informazioni su CORS flussi e i problemi comuni, visualizzare hello [tooCORS della Guida per le API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Scenari con caratteri jolly o singola origine
CORS nella rete CDN di Azure funzioneranno automaticamente senza alcuna configurazione aggiuntiva quando hello **Access-Control-Allow-Origin** intestazione è impostata toowildcard (*) o una singola origine.  Hello CDN verrà memorizzati nella cache prima risposta hello e le richieste successive utilizzeranno hello stessa intestazione.

Se le richieste sono state apportate toohello CDN tooCORS precedente viene impostata su hello all'origine, sarà necessario toopurge contenuto nel hello tooreload contenuto endpoint contenuto con hello **Access-Control-Allow-Origin** intestazione.

## <a name="multiple-origin-scenarios"></a>Scenari con più origini
Se è necessario un elenco specifico di toobe le origini consentite per CORS tooallow, operazioni get leggermente più complesse. Hello problema si verifica quando hello rete CDN memorizza nella cache di hello **Access-Control-Allow-Origin** intestazione per l'origine CORS prima hello.  Quando una diversa origine CORS effettua una richiesta successiva, hello CDN servirà memorizzati nella cache di hello **Access-Control-Allow-Origin** intestazione, che non corrisponda.  Esistono diversi modi toocorrect questo.

### <a name="azure-cdn-premium-from-verizon"></a>Rete CDN Premium di Azure fornita da Verizon
Hello tooenable modo migliore tratta toouse **Premium rete CDN di Azure da Verizon**, che espongono alcune funzionalità avanzate. 

È necessario troppo[creare una regola](cdn-rules-engine.md) toocheck hello **origine** intestazione nella richiesta di hello.  Se si tratta di un'origine valida, la regola verrà impostata hello **Access-Control-Allow-Origin** intestazione con origine hello fornito nella richiesta di hello.  Se l'origine hello specificato in hello **origine** intestazione non è consentita, la regola non deve eseguire hello **Access-Control-Allow-Origin** intestazione che può causare errori hello tooreject hello nei browser. 

Esistono due modi toodo questo con hello motore regole di business.  In entrambi i casi, hello **Access-Control-Allow-Origin** intestazione dal server di origine del file hello viene ignorato completamente, motore regole di business del hello CDN gestisce completamente hello consentito origini CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Un'espressione regolare con tutte le origini valide
In questo caso, si creerà un'espressione regolare che include tutte le origini di hello desiderato tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> La **rete CDN di Azure fornita da Verizon** usa la libreria [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) come motore per le espressioni regolari.  È possibile utilizzare uno strumento come [101 di espressioni regolari](https://regex101.com/) toovalidate l'espressione regolare.  Si noti che hello "/" caratteri nelle espressioni regolari valido e non deve necessariamente toobe caratteri di escape, tuttavia, tale carattere di escape è considerata buona norma e prevede un validator di espressione regolare.
> 
> 

Se l'espressione regolare hello corrisponde, la regola sostituirà hello **Access-Control-Allow-Origin** intestazione (se presente) dall'origine hello con origine hello che ha inviato la richiesta di hello.  È inoltre possibile aggiungere altre intestazioni CORS, ad esempio **Access-Control-Allow-Methods**.

![Esempio di regole con espressione regolare](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Regola intestazione richiesta per ciascuna origine.
Invece di espressioni regolari, è possibile creare un apposito regola per ogni origine desiderato utilizzando hello tooallow **richiesta jolly intestazione** [corrispondono alla condizione](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Come con il metodo di espressione regolare hello, hello motore regole intestazioni da solo con set hello CORS. 

![Esempio di regole senza espressione regolare](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> Nell'esempio hello sopra, hello l'utilizzo del carattere jolly hello * indica toomatch del motore regole di hello HTTP e HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Rete CDN Standard di Azure
Nei profili di rete CDN di Azure Standard, hello solo tooallow meccanismo per più origini senza utilizzare hello di origine con caratteri jolly hello è toouse [la memorizzazione nella cache di stringa di query](cdn-query-string.md).  È necessario tooenable impostazione della stringa di query per l'endpoint rete CDN hello e quindi utilizzare una stringa di query univoci per le richieste da ogni dominio consentito. Questa operazione comporterà hello CDN la memorizzazione nella cache un oggetto separato per ogni stringa di query univoco. Questo approccio non è ideale, tuttavia, in quanto comporta in più copie di hello lo stesso file hello memorizzati nella cache nella rete CDN.  

