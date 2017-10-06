---
title: aaaManage l'API prima in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocreate API, operazioni di aggiunta e Introduzione a gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Gestire la prima API in Gestione API di Azure
## <a name="overview"> </a>Panoramica
Questa guida Mostra come tooquickly iniziare utilizzando Gestione API di Azure e rendere la prima chiamata API.

## <a name="concepts"></a>Cos'è Gestione API di Azure?
È possibile utilizzare Gestione API di Azure tootake qualsiasi back-end e avviare un programma API flessibile basato su di esso.

Gli scenari comuni includono:

* **protezione dell'infrastruttura mobile** con la delega dell'accesso con le chiavi API, la prevenzione degli attacchi DOS con la limitazione oppure l'uso di criteri di sicurezza avanzata come la convalida dei token JWT.
* **Abilitazione ecosistemi partner ISV** tramite l'offerta di caricamento rapido partner tramite developer hello portale e compila un toodecouple facciata API da implementazioni interne che non sono particolarmente adatto per l'utilizzo di partner.
* **Esegue un programma API interno** offrendo una posizione centralizzata per hello organizzazione toocommunicate sulla disponibilità di hello e più recenti modifiche apportate tooAPIs, controllo di accesso in base agli account aziendali, tutti basati su un canale protetto tra Hello gateway API e hello back-end.

sistema Hello è costituito da hello seguenti componenti:

* Hello **gateway API** hello endpoint che:
  
  * Accetta API chiama e li indirizza tooyour ai back-end.
  * Verifica le chiavi API, i token JWT, i certificati e altre credenziali.
  * Applica le quote di utilizzo e i limiti di frequenza.
  * Trasforma l'API volo hello senza modifiche al codice.
  * Memorizza nella cache le risposte di back-end durante l'installazione.
  * Registra i metadati della chiamata a scopi di analisi.
* Hello **portale di pubblicazione** è l'interfaccia amministrativa di hello in cui impostare il programma di API. Può essere usato per:
  
  * Definire o importare lo schema API.
  * Creare pacchetti di API nei prodotti.
  * Impostare i criteri, ad esempio quote o di trasformazioni su hello API.
  * Ottenere informazioni dall'analisi.
  * Gestire gli utenti.
* Hello **portale per sviluppatori** funge da presenza di hello web principale per gli sviluppatori, in cui è possibile:
  
  * Leggere la documentazione relativa alle API.
  * Provare a utilizzare un'API tramite la console interattiva hello.
  * Creare un account e sottoscrizione chiavi tooget API.
  * Accedere all'analisi di utilizzo personalizzata.

## <a name="create-service-instance"></a>Creare un'istanza di Gestione API
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Se non si ha un account, è possibile creare un account gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][Azure Free Trial].
> 
> 

Hello primo passaggio nell'utilizzo di gestione API consiste toocreate un'istanza del servizio. Accedi toohello [portale Azure] [ Azure Portal] e fare clic su **New**, **Web e dispositivi mobili**, **gestione API**.

![API Management new instance][api-management-create-instance-menu]

Per **nome**, specificare un toouse nome di dominio secondario univoco per l'URL del servizio hello.

Scegliere hello desiderato **sottoscrizione**, **gruppo di risorse** e **percorso** per l'istanza del servizio.

Immettere **Contoso Ltd.** per hello **nome organizzazione**e immettere l'indirizzo di posta elettronica in hello **posta elettronica amministratore** campo.

> [!NOTE]
> Questo indirizzo di posta elettronica viene utilizzato per notifiche da hello sistema gestione API. Per ulteriori informazioni, vedere [come tooconfigure notifiche e modelli in Gestione API di Azure di posta elettronica][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![New API Management service][api-management-create-instance-step1]

Le istanze del servizio Gestione API sono disponibili in tre livelli: Developer, Standard e Premium.

> [!NOTE]
> Hello livello sviluppatore è per lo sviluppo, test e i programmi API pilota in cui la disponibilità elevata non rappresenta un problema. In hello Standard e i livelli Premium, è possibile ridimensionare il toohandle numero di unità riservata maggiore quantità di traffico. livelli Standard e Premium Hello forniscono al servizio Gestione API hello la maggior parte delle capacità di elaborazione e prestazioni. È possibile completare questa esercitazione usando qualsiasi livello. Per altre informazioni sui livelli di Gestione API, vedere [Gestione API - Prezzi][API Management pricing].
> 
> 

Fare clic su **crea** toostart provisioning all'istanza del servizio.

![New API Management service][api-management-instance-created]

Una volta creata l'istanza del servizio hello, passaggio successivo hello toocreate o importare un'API.

## <a name="create-api"></a>Importare un'API
Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client. Le operazioni dell'API sono servizi web tooexisting elaborate.

È possibile creare le API (e aggiungere operazioni) in modo manuale oppure è possibile importarle. In questa esercitazione, verranno importate hello API per un servizio web Calcolatrice di esempio forniti da Microsoft e ospitati in Azure.

> [!NOTE]
> Per informazioni sulla creazione di un'API e l'aggiunta manuale di operazioni, vedere [come toocreate API](api-management-howto-create-apis.md) e [come tooadd operazioni tooan API](api-management-howto-add-operations.md).
> 
> 

Le API vengono configurate dal portale di pubblicazione hello. tooreach, fare clic su **portale di pubblicazione** dalla barra degli strumenti del servizio di hello.

![Portale di pubblicazione][api-management-management-console]

Calcolatrice hello tooimport API, fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **importazione API**.

![Pulsante Importa API][api-management-import-api]

Eseguire hello seguendo i passaggi tooconfigure hello calcolatrice API:

1. Fare clic su **From URL**, immettere **http://calcapi.cloudapp.net/calcapi.json** in hello **URL del documento di specifica** testo, quindi scegliere hello **Swagger**  pulsante di opzione.
2. Tipo **calc** in hello **suffisso URL di Web API** casella di testo.
3. Fare clic nella hello **prodotti (facoltativi)** e scegliere **Starter**.
4. Fare clic su **salvare** tooimport hello API.

![Add new API][api-management-import-new-api]

> [!NOTE]
> **Gestione API** supporta attualmente sia la versione 1.2 che la versione 2.0 del documento Swagger per l'importazione. Anche se la [specifica Swagger 2.0](http://swagger.io/specification) dichiara che le proprietà `host`, `basePath` e `schemes` sono facoltative, il documento Swagger 2.0 **DEVE** contenere queste proprietà. In caso contrario, non verrà importato. 
> 
> 

Una volta importato, hello API hello pagina Riepilogo per l'API di hello viene visualizzato nel portale di pubblicazione hello.

![Riepilogo dell'API][api-management-imported-api-summary]

Hello sezione API è disponibili diverse schede. Hello **riepilogo** scheda vengono visualizzate le metriche di base e informazioni sulle API hello. Hello [impostazioni](api-management-howto-create-apis.md#configure-api-settings) scheda è tooview e modifica hello configurazione per un'API. Hello [operazioni](api-management-howto-add-operations.md) scheda è operazioni hello toomanage utilizzato dell'API. Hello **sicurezza** scheda può essere utilizzato tooconfigure l'autenticazione del gateway per server back-end hello utilizzando l'autenticazione di base o [autenticazione reciproca del certificato](api-management-howto-mutual-certificates.md)e tooconfigure [ l'autorizzazione dell'utente tramite OAuth 2.0](api-management-howto-oauth2.md).  Hello **problemi** scheda è tooview utilizzati problemi segnalati da sviluppatori hello che utilizzano le API. Hello **prodotti** scheda è prodotti hello tooconfigure utilizzati che contengono questa API.

Per impostazione predefinita, con ogni istanza di Gestione API vengono forniti due prodotti di esempio:

* **Starter**
* **Illimitato**

In questa esercitazione, hello base API Calcolatrice è stato aggiunto prodotto Starter toohello quando è stato importato hello API.

Nell'ordine toomake chiamate tooan API, gli sviluppatori devono prima sottoscrizione prodotto tooa che consenta l'accesso tooit. Gli sviluppatori possono eseguire la sottoscrizione nel portale per sviluppatori hello tooproducts o gli amministratori possono eseguire la sottoscrizione agli sviluppatori tooproducts nel portale di pubblicazione hello. Si è un amministratore dopo la creazione istanza di gestione API hello in hello passaggi precedenti nell'esercitazione di hello, pertanto sono già sottoscritti tooevery prodotto per impostazione predefinita.

## <a name="call-operation"></a>Chiamare un'operazione dal portale per sviluppatori hello
Operazioni possono essere chiamate direttamente dal portale per sviluppatori di hello, che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API. In questo passaggio dell'esercitazione, verrà chiamata dell'API di hello base Calcolatrice **aggiungere due numeri interi** operazione. Fare clic su **portale per sviluppatori** dal menu hello hello in alto a destra del portale di pubblicazione hello.

![Portale per sviluppatori][api-management-developer-portal-menu]

Fare clic su **API** dal menu superiore hello e quindi fare clic su **Calcolatrice di base** toosee hello operazioni disponibili.

![Portale per sviluppatori][api-management-developer-portal-calc-api]

Tenere presente le descrizioni di esempio hello e i parametri che sono stati importati insieme hello API e operazioni, fornendo la documentazione per sviluppatori di hello che utilizzerà questa operazione. È possibile aggiungere queste descrizioni anche quando le operazioni vengono aggiunte manualmente.

hello toocall **aggiungere due numeri interi** operazione, fare clic su **provarla**.

![Prova][api-management-developer-portal-calc-api-console]

È possibile immettere alcuni valori per parametri hello o mantenere i valori predefiniti di hello e quindi fare clic su **inviare**.

![HTTP Get][api-management-invoke-get]

Dopo un'operazione viene richiamata, il portale per sviluppatori di hello Visualizza hello **stato della risposta**, hello **le intestazioni di risposta**e di qualsiasi **contenuto della risposta**.

![Response][api-management-invoke-get-response]

## <a name="view-analytics"></a>Visualizzare l'analisi
tooview analitica per Calcolatrice di base, il portale di pubblicazione toohello indietro di commutatore selezionando **Gestisci** dal menu hello hello in alto a destra del portale per sviluppatori hello.

![Gestisci][api-management-manage-menu]

visualizzazione predefinita per il portale di pubblicazione hello Hello è hello **Dashboard**, che fornisce una panoramica dell'istanza di gestione API.

![Dashboard][api-management-dashboard]

Posizionare il mouse di hello su grafico hello per **Calcolatrice di base** metriche specifiche di hello toosee per l'utilizzo di hello di hello API per un determinato periodo di tempo.

> [!NOTE]
> Se tutte le righe non viene visualizzato nel grafico, passare portale per sviluppatori toohello indietro ed effettuare alcune chiamate in hello API, attendere alcuni istanti e tornare toohello dashboard.
> 
> 

Fare clic su **Visualizza dettagli** pagina di riepilogo hello tooview per hello API, inclusa una versione più grande di metriche di hello visualizzato.

![Analytics][api-management-mouse-over]

![Riepilogo][api-management-api-summary-metrics]

Per le metriche dettagliate e i report, fare clic su **Analitica** da hello **gestione API** menu di sinistra hello.

![Panoramica][api-management-analytics-overview]

Hello **Analitica** sezione ha hello seguenti quattro schede:

* **A colpo d'occhio** fornisce l'utilizzo complessivo e metriche sull'integrità, nonché hello sviluppatori superiore, prodotti, API superiore e operazioni superiore.
* **Utilizzo** : fornisce informazioni dettagliate sulle chiamate API e sulla larghezza di banda, inclusa una rappresentazione geografica.
* **Integrità** : è incentrata sui codici di stato, sulle percentuali di operazioni sulla cache completate, sui tempi di risposta, oltre che sui tempi di risposta di API e servizi.
* **Attività** fornisce i report drill-down attività specifiche di hello da sviluppatori, prodotto, API e operation.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[proteggere l'API con i limiti di velocità](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
