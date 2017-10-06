---
title: richiesta aaaAdvanced la limitazione delle richieste a gestione API di Azure
description: Informazioni su come toocreate e applicare una quota flessibile e a gestione API di Azure i criteri di limitazione della frequenza.
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Limitazione avanzata delle richieste con Gestione API di Azure
La toothrottle in grado di richieste in ingresso è un ruolo fondamentale di gestione API di Azure. Consente di gestione API tramite controllo frequenza hello di richieste o hello Totale richieste/dati trasferiti, API provider tooprotect le rispettive API da evitare eventuali abusi e creare il valore per diversi livelli di API del prodotto.

## <a name="product-based-throttling"></a>Limitazione basata sul prodotto
stato limitato toobeing con ambito tooa particolare sottoscrizione al prodotto (essenzialmente una chiave), definito in hello portale di gestione API pubblicazione toodate, frequenza di hello le funzionalità di limitazione. Ciò è utile per i limiti di hello API provider tooapply agli sviluppatori di hello che hanno effettuato l'iscrizione toouse API, tuttavia, non serve, ad esempio, in cui la limitazione delle richieste di singoli utenti finali di hello API. È possibile che per singolo utente di tooconsume di applicazione per gli sviluppatori di hello hello intera quota e quindi impedire altri clienti dello sviluppatore hello toouse in grado di un'applicazione hello. Inoltre, alcuni clienti che potrebbero generare un numero elevato di richieste possono limitare l'accesso toooccasional gli utenti.

## <a name="custom-key-based-throttling"></a>Limitazione basata su chiave personalizzata
nuovo Hello [frequenza limite dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) criteri forniscono un controllo di tootraffic soluzione notevolmente più flessibile. I nuovi criteri consentono di toodefine espressioni tooidentify hello chiavi saranno tootrack utilizzato traffico utilizzo. Hello funzionamento di questo è illustrato il modo più semplice con un esempio. 

## <a name="ip-address-throttling"></a>Limitazione dell'indirizzo IP
i criteri seguenti Hello limitare un singolo client IP indirizzo tooonly 10 chiama ogni minuto, con un totale di 1.000.000 chiamate e 10.000 kilobyte di larghezza di banda al mese. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Se tutti i client su Internet hello usato un indirizzo IP univoco, potrebbe trattarsi di un metodo efficace per limitare l'utilizzo dall'utente. Tuttavia, è molto probabile che più utenti saranno la condivisione di un singolo indirizzo IP pubblico a causa di toothem accesso hello Internet tramite un dispositivo NAT. Nonostante ciò, per le API che consentono di hello accesso non autenticato `IpAddress` potrebbe essere migliore hello.

## <a name="user-identity-throttling"></a>Limitazione dell'identità utente
Se un utente finale viene autenticato, può essere generata una chiave per la limitazione delle richieste in base alle informazioni che identificano in modo univoco l'utente.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

In questo esempio estrarre l'intestazione di autorizzazione hello, convertirlo troppo`JWT` oggetto utilizza soggetto hello dell'utente di hello tooidentify token hello e utilizzarlo come chiave di limitazione della frequenza hello. Se l'identità utente hello è archiviato in hello `JWT` come uno degli altri hello quindi attestazioni che valore può essere utilizzato al suo posto.

## <a name="combined-policies"></a>Criteri combinati
Sebbene hello limitazione nuovi criteri di fornisce un maggiore controllo rispetto hello esistente i criteri di limitazione, è la combinazione di entrambe le funzionalità di valore. La limitazione delle richieste dal codice product key di sottoscrizione ([frequenza delle chiamate limite sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [Set quota di utilizzo mediante sottoscrizione](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) è un ottimo modo tooenable monetizing di un'API tramite l'addebito in base ai livelli di utilizzo. Hello controllo con granularità maggiore di essere in grado di toothrottle dall'utente è complementare e impedisce il comportamento di un utente di compromettere l'esperienza di hello di un altro. 

## <a name="client-driven-throttling"></a>Limitazione basata su client
Quando la limitazione delle richieste chiave hello viene definita con un [espressione di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx), viene utilizzato il provider hello API che sceglie la limitazione delle richieste di hello ha come ambito. Tuttavia, è consigliabile uno sviluppatore toocontrol sono giudizio limitare i propri clienti. È possibile abilitare dal provider di API hello introducendo client applicazione toocommunicate hello chiave toohello dello sviluppatore un'intestazione personalizzata tooallow hello API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

In questo modo toochoose di applicazione client per gli sviluppatori di hello la modalità di limitazione chiave della frequenza toocreate hello. Un po' di ingegno uno sviluppatore di client di creare i propri livelli di velocità da set di chiavi toousers di allocazione e la rotazione di utilizzo della chiave di hello.

## <a name="summary"></a>Riepilogo
Gestione API di Azure fornisce frequenza offerta limitazione tooboth proteggere e aggiungere valore tooyour API servizio. Hello limitazione nuovi criteri con le regole di ambito personalizzati consentono di che è maggiore controllo sulla tooenable tali criteri con granularità le applicazioni di clienti toobuild ancora migliore. esempi di Hello in questo articolo illustrano l'utilizzo di hello di questi nuovi criteri per limitare le chiavi con indirizzi IP client, l'identità utente e valori del client generato tasso di produzione. Tuttavia, esistono molte altre parti di messaggio hello che potrebbero essere utilizzati come agente utente, i frammenti del percorso URL, dimensione del messaggio.

## <a name="next-steps"></a>Passaggi successivi
Per commenti e suggerimenti nel thread di Disqus hello per questo argomento. Sarebbe ideale toohear su altri potenziali valori di chiave che sono stati una scelta negli scenari di logica.

## <a name="watch-a-video-overview-of-these-policies"></a>Video contenente una panoramica di questi criteri
Per ulteriori informazioni su hello [frequenza limite dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [quota dalla chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) criteri descritti in questo articolo, guardare hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

