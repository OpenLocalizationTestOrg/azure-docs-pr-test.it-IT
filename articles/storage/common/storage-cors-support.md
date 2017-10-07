---
title: Supporto di origine aaaCross risorsa condivisione (CORS) | Documenti Microsoft
description: Informazioni su come il supporto CORS tooenable per hello servizi di archiviazione di Microsoft Azure.
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Supporto di condivisione delle risorse Multiorigine (CORS) per servizi di archiviazione Azure hello
A partire dalla versione 2013-08-15, i servizi di archiviazione Azure hello supportano la condivisione delle risorse Multiorigine (CORS) per i servizi Blob, tabella, di accodamento e File hello. Condivisione CORS è una funzionalità HTTP che consente a un'applicazione web in esecuzione risorse di tooaccess in un dominio in un altro dominio. Browser Web implementano una restrizione di sicurezza nota come [criteri stessa origine](http://www.w3.org/Security/wiki/Same_Origin_Policy) che impedisce a una pagina web da chiamare API in un dominio diverso. Condivisione CORS offre un toocall (dominio di origine hello) di un dominio tooallow in modo sicuro le API in un altro dominio. Vedere hello [specifica CORS](http://www.w3.org/TR/cors/) per ulteriori dettagli sull'argomento.

È possibile impostare le regole CORS singolarmente per ogni hello servizi di archiviazione, mediante la chiamata [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [Set Queue Service Properties](https://msdn.microsoft.com/library/hh452232.aspx), e [impostare proprietà del servizio tabelle](https://msdn.microsoft.com/library/hh452240.aspx). Dopo aver impostato le regole CORS hello per servizio hello, una richiesta correttamente autenticata effettuata nel servizio hello da un altro dominio sarà valutata toodetermine se è consentito in base a regole toohello che è stato specificato.

> [!NOTE]
> CORS non è un meccanismo di autenticazione. Qualsiasi richiesta eseguita a una risorsa di archiviazione quando è abilitata la condivisione CORS deve disporre di una firma di autenticazione appropriata o deve essere eseguita su una risorsa pubblica.
> 
> 

## <a name="understanding-cors-requests"></a>Informazioni sulle richieste CORS
Una richiesta CORS proveniente da un dominio di origine può essere costituita da due richieste distinte:

* Una richiesta preliminare, che esegue una query sulle restrizioni di condivisione CORS hello imposte dal servizio hello. richiesta preliminare Hello è obbligatorio a meno che il metodo di richiesta di hello è un [metodo semplice](http://www.w3.org/TR/cors/), vale a dire GET, HEAD o POST.
* richiesta effettiva Hello, effettuata hello desiderato di risorse.

### <a name="preflight-request"></a>Richiesta preliminare
le query di richiesta preliminare Hello hello sulle restrizioni di condivisione CORS definite per il servizio di archiviazione hello dal proprietario dell'account hello. browser web Hello (o un altro agente utente) invia una richiesta OPTIONS che include intestazioni di richiesta hello, dominio di origine e di metodo. il servizio di archiviazione Hello valuta operazione hello previsto in base a un set preconfigurato di regole CORS per specificare i domini di origine, metodi di richiesta e intestazioni di richiesta possono essere specificate in una richiesta effettiva rispetto a una risorsa di archiviazione.

Se è abilitata la condivisione CORS per servizio hello ed è presente una regola CORS corrispondente alla richiesta preliminare hello, hello servizio risponde con il codice di stato 200 (OK) e include le intestazioni di controllo di accesso richiesto hello in risposta hello.

Se non è abilitata la condivisione CORS per servizio hello o alcuna regola CORS corrispondente richiesta preliminare hello, servizio hello risponderà con codice di stato 403 (accesso negato).

Se non contiene richiesta OPTIONS hello hello intestazioni CORS obbligatorie (hello origine e le intestazioni Access-Control-Request-Method), servizio hello risponderà con codice di stato 400 (richiesta non valida).

Si noti che una richiesta preliminare viene valutata rispetto a servizio hello (Blob, coda e tabella) e non rispetto hello la risorsa richiesta. proprietario dell'account Hello è necessario aver abilitato CORS come parte delle proprietà di hello account del servizio affinché toosucceed richiesta hello.

### <a name="actual-request"></a>Richiesta effettiva
Quando viene accettata la richiesta preliminare hello, viene restituita la risposta hello browser hello invierà richiesta effettiva di hello nei confronti di risorsa di archiviazione hello. browser Hello rifiuterà la richiesta effettiva hello immediatamente se hello richiesta preliminare viene rifiutata.

la richiesta effettiva Hello viene considerata come una normale richiesta nel servizio di archiviazione hello. presenza di Hello dell'intestazione di origine hello indica che hello tratta di una richiesta CORS e hello controllerà hello corrispondenti regole CORS. Se viene trovata una corrispondenza, le intestazioni di hello controllo di accesso vengono aggiunti toohello risposta e inviato client toohello indietro. Se non viene trovata una corrispondenza, le intestazioni Access-Control CORS hello non vengono restituite.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Abilitazione di CORS per servizi di archiviazione di Azure hello
Le regole CORS vengono impostate a livello di servizio hello, pertanto è necessario tooenable o si disabilita CORS per ogni servizio (Blob, coda e tabella) separatamente. Per impostazione predefinita, la condivisione CORS è disabilitata per ciascun servizio. tooenable CORS, è necessario tooset hello servizio appropriato le proprietà utilizzando la versione 2013-08-15 o versioni successive e aggiungere le proprietà del servizio toohello regole CORS. Per informazioni dettagliate su come tooenable o disabilita CORS per un servizio e come tooset CORS regole, fare riferimento troppo[Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [Set Queue Service Properties](https://msdn.microsoft.com/library/hh452232.aspx), e [impostata tabella Le proprietà del servizio](https://msdn.microsoft.com/library/hh452240.aspx).

Di seguito è riportato un esempio di una regola CORS singola, specificata tramite un'operazione Set Service Properties:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Ogni elemento incluso nella regola CORS hello è descritta di seguito:

* **AllowedOrigins**: i domini di origine hello consentiti toomake una richiesta nel servizio di archiviazione hello del servizio tramite CORS. dominio di origine Hello è hello dal quale hello origine della richiesta. Si noti che l'origine hello deve essere una corrispondenza esatta con origine hello che età utente hello invia toohello servizio. È inoltre possibile utilizzare caratteri jolly hello ' *' tooallow tutte le richieste origine toomake domini tramite CORS. Nell'esempio hello sopra, hello domini [http://www.contoso.com](http://www.contoso.com) e [http://www.fabrikam.com](http://www.fabrikam.com) può effettuare richieste nel servizio di hello tramite condivisione CORS.
* **AllowedMethods**: hello i metodi (verbi di richiesta HTTP) che dominio di origine hello può utilizzare per una richiesta CORS. Nell'esempio hello sopra, sono consentite solo richieste PUT e GET.
* **AllowedHeaders**: le intestazioni di richiesta hello tale dominio di origine hello può specificare nella richiesta CORS hello. Nell'esempio hello sopra, sono consentite tutte le intestazioni di metadati a partire da x-ms-meta-data, x-ms-meta-destinazione e x-ms-meta-abc. Si noti il carattere jolly hello ' *' indica che qualsiasi intestazione che inizi con hello specificato è consentito un prefisso.
* **ExposedHeaders**: hello intestazioni di risposta che possono essere inviate nella richiesta di hello risposta toohello CORS ed esposte dall'autorità di certificazione hello browser toohello richiesta. Nell'esempio riportato in precedenza, il browser hello hello è tooexpose istruzioni riportate qualsiasi intestazione che inizi con x-ms-meta.
* **MaxAgeInSeconds**: hello quantità di tempo massima che un browser deve memorizzare nella cache richiesta OPTIONS preliminare hello.

Hello servizi di archiviazione di Azure supportano la specifica di intestazioni con prefissata per entrambi hello **AllowedHeaders** e **ExposedHeaders** elementi. tooallow una categoria di intestazioni, è possibile specificare una categoria di toothat prefisso comune. Ad esempio, specificando *x-ms-meta** come intestazione con prefisso, viene impostata una regola corrispondente a tutte le intestazioni che iniziano con x-ms-meta.

Hello limitazioni seguenti si applica le regole di tooCORS:

* È possibile specificare di toofive regole CORS per il servizio di archiviazione (Blob, tabelle e code).
* dimensione massima di Hello di tutte le impostazioni delle regole CORS nella richiesta di hello, esclusi i tag XML, non deve superare 2 KB.
* lunghezza Hello di un'intestazione consentita, intestazione esposta o origine consentita non deve superare i 256 caratteri.
* Le intestazioni consentite e quelle esposte possono essere:
  * Intestazioni letterali, dove nome esatto dell'intestazione hello viene specificato, ad esempio **x-ms-meta-processed**. Un massimo di 64 intestazioni letterali può essere specificato nella richiesta di hello.
  * Intestazioni con prefisso, in cui un prefisso dell'intestazione hello viene specificato, ad esempio **x-ms-meta-data***. Specificando un prefisso in questo modo consente o espone qualsiasi intestazione che inizia con hello prefisso specificato. Un massimo di due intestazioni con prefisso può essere specificato nella richiesta di hello.
* Hello metodi (o verbi HTTP) specificati in hello **AllowedMethods** toohello metodi supportati dalle API del Servizio archiviazione di Azure devono essere conformi. I metodi supportati sono DELETE, GET, HEAD, MERGE, POST, OPTIONS e PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Informazioni sulla logica di valutazione delle regole CORS
Quando un servizio di archiviazione riceve una richiesta preliminare o effettiva, valuta quest'ultima in base alle regole CORS hello definite per il servizio di hello tramite l'operazione Set Service Properties appropriata hello. Le regole CORS vengono valutate in ordine di hello in cui sono state impostate nel corpo della richiesta hello di hello operazione Set Service Properties.

Le regole CORS vengono valutate come segue:

1. In primo luogo, il dominio di origine hello della richiesta di hello rispetto a domini hello elencati per hello **AllowedOrigins** elemento. Se il dominio di origine hello è incluso nell'elenco di hello o tutti i domini sono consentiti con carattere jolly hello ' *', valutazione delle regole prosegue. Se non è incluso il dominio di origine di hello, richiesta di hello ha esito negativo.
2. Successivamente, il metodo hello (o verbo HTTP) della richiesta di hello rispetto a metodi di hello in hello **AllowedMethods** elemento. Se il metodo hello è incluso nell'elenco di hello, valutazione delle regole prosegue; in caso contrario, la richiesta hello avrà esito negativo.
3. Se hello richiesta corrisponde a una regola nel relativo dominio di origine e il relativo metodo, tale regola è richiesta hello tooprocess selezionato e non altre regole vengono valutate. Prima di richiesta di hello può avere esito positivo, tuttavia, tutte le intestazioni specificate nella richiesta di hello vengono confrontate con intestazioni hello elencate in hello **AllowedHeaders** elemento. Se le intestazioni di hello inviate non corrispondono hello le intestazioni autorizzata, richiesta di hello ha esito negativo.

Poiché le regole di hello vengono elaborate nell'ordine di hello che sono presenti nel corpo della richiesta hello, è consigliabile specificare le regole più restrittive hello con rispettano tooorigins prima nell'elenco di hello, in modo che vengano valutate per prime. Specificare le regole meno restrittive, ad esempio, un tooallow regola tutte le origini, al fine di hello dell'elenco di hello.

### <a name="example--cors-rules-evaluation"></a>Esempio: valutazione di regole CORS
Hello esempio seguente viene illustrato un corpo della richiesta parziale per le regole CORS tooset un'operazione per i servizi di archiviazione hello. Vedere [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [Set Queue Service Properties](https://msdn.microsoft.com/library/hh452232.aspx), e [Set Table Service Properties](https://msdn.microsoft.com/library/hh452240.aspx) per informazioni dettagliate sulla costruzione richiesta hello.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Successivamente, si consideri hello seguenti richieste CORS:

| Richiesta |  |  | Response |  |
| --- | --- | --- | --- | --- |
| **Metodo** |**Origine** |**Intestazioni della richiesta** |**Corrispondenza regola** |**Risultato** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |Prima regola |Success |
| **GET** |http://www.contoso.com |x-ms-blob-content-type |Seconda regola |Success |
| **GET** |http://www.contoso.com |x-ms-client-request-id |Seconda regola |Esito negativo |

Hello prima richiesta corrisponde prima regola hello: dominio di origine di hello corrisponde hello le origini consentita, metodo hello corrisponde hello consentito metodi e intestazione hello corrisponde consentito intestazioni: hello e quindi ha esito positivo.

seconda richiesta Hello non corrisponde prima regola hello metodo hello non corrisponde a hello metodi consentito. Tuttavia, corrisponde seconda regola hello, pertanto ha esito positivo.

Hello terza richiesta corrisponde seconda regola di hello nel relativo dominio di origine e di un metodo, pertanto nessun altre regole vengono valutate. Tuttavia, hello *intestazione x-ms-client-request-id* non è consentita dalla seconda regola hello, in modo hello richiesta ha esito negativo, nonostante hello che semantica hello della terza regola hello ne avrebbe consentito toosucceed.

> [!NOTE]
> Anche se in questo esempio mostra una regola meno restrittiva prima di una più restrittiva, in genere consigliata hello è regole più restrittive di hello toolist prima.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Informazioni sulla configurazione intestazione Vary hello
Hello *Vary* intestazione è un'intestazione HTTP/1.1 standard costituito da un set di campi di intestazione di richiesta che indichino hello browser o all'agente utente sui criteri hello che sono stati selezionati dall'hello server tooprocess hello richiesta. Hello *Vary* intestazione viene utilizzata principalmente per la memorizzazione nella cache dal proxy, browser e reti CDN, che la impiegano toodetermine come hello risposta deve essere memorizzata nella cache. Per informazioni dettagliate, vedere Specifica hello hello [intestazione Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Quando il browser hello o un altro agente utente memorizza nella cache la risposta hello da una richiesta CORS, il dominio di origine hello viene memorizzato nella cache come hello origine consentita. Quando un secondo problemi dominio hello stessa richiesta per una risorsa di archiviazione mentre è attiva cache di hello, agente utente hello recupera il dominio di origine memorizzato nella cache di hello. dominio di secondo Hello corrisponde dominio memorizzate nella cache di hello, in modo richiesta hello ha esito negativo quando avrebbe potuto essere positivo. In alcuni casi, archiviazione di Azure Imposta intestazione Vary hello troppo**origine** tooinstruct hello agente toosend hello successive CORS richiesta toohello servizio utente quando la richiesta di dominio è diverso dall'hello hello memorizzato nella cache di origine.

Archiviazione di Azure imposta hello *Vary* intestazione troppo**origine** per le richieste GET/HEAD effettive in hello seguenti casi:

* Quando richiesta hello origine corrisponde esattamente hello consentito origine definito da una regola CORS. toobe una corrispondenza esatta, regola CORS hello non può includere un carattere jolly ' * ' caratteri.
* Non vi è alcuna origine della richiesta regola hello corrispondente, ma è abilitata la condivisione CORS per il servizio di archiviazione hello.

In caso di hello in cui una richiesta GET/HEAD corrisponde a una regola CORS che consente tutte le origini, risposta hello indica che sono consentite tutte le origini e cache dell'agente utente hello consentirà le richieste successive da qualsiasi dominio di origine mentre è attiva cache di hello.

Si noti che per le richieste utilizzando metodi diversi da GET/HEAD, i servizi di archiviazione hello non imposterà intestazione Vary hello, poiché i metodi toothese risposte non memorizzate nella cache per gli agenti utente.

Nella tabella seguente Hello indica come Azure storage risponderà richieste tooGET/HEAD in base hello precedentemente menzionato casi:

| Richiesta | Impostazione account e risultato della valutazione della regola |  |  | Response |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Intestazione di origine presente sulla richiesta** |**Regole CORS specificate per questo servizio** |**Presenza di una regola di corrispondenza che consente tutte le origini (*)** |**Presenza di una regola per l'esatta corrispondenza dell'origine** |**Risposta include tooOrigin set di intestazione Vary** |**Risposta che include Access-Control-Allowed-Origin: "*"** |**Risposta che include Access-Control-Exposed-Headers** |
| No |No |No |No |No |No |No |
| No |Sì |No |No |Sì |No |No |
| No |Sì |Sì |No |No |Sì |Sì |
| Sì |No |No |No |No |No |No |
| Sì |Sì |No |Sì |Sì |No |Sì |
| Sì |Sì |No |No |Sì |No |No |
| Sì |Sì |Sì |No |No |Sì |Sì |

## <a name="billing-for-cors-requests"></a>Fatturazione per le richieste CORS
Preliminari con esito positivo delle richieste vengono fatturati se è stata abilitata la condivisione CORS per hello servizi di archiviazione per l'account (chiamando [Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx), [Set Queue Service Properties](https://msdn.microsoft.com/library/hh452232.aspx), o [ Set Table Service Properties](https://msdn.microsoft.com/library/hh452240.aspx)). gli addebiti toominimize, provare a impostare hello **MaxAgeInSeconds** elemento CORS regole tooa valori di grandi dimensioni in modo che hello agente utente memorizza nella cache richiesta hello.

Le richieste preliminari con esito negativo non verranno fatturate.

## <a name="next-steps"></a>Passaggi successivi
[Set Blob Service Properties](https://msdn.microsoft.com/library/hh452235.aspx)

[Set Queue Service Properties](https://msdn.microsoft.com/library/hh452232.aspx)

[Set Table Service Properties](https://msdn.microsoft.com/library/hh452240.aspx)

[Specifica del W3C relativa alla condivisione delle risorse multiorigine (CORS)](http://www.w3.org/TR/cors/)

