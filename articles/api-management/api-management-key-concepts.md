---
title: concetti di panoramica e la chiave di gestione API aaaAzure | Documenti Microsoft
description: Informazioni su API, prodotti, ruoli, gruppi e altri concetti chiave di Gestione API.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>Informazioni su Gestione API
Gestione API consente alle organizzazioni di pubblicare API tooexternal, partner e sviluppatori interni toounlock hello potenzialmente i dati e i servizi. Le aziende everywhere sono ricerca tooextend le relative operazioni come piattaforma digitale, creando nuovi canali, trovando nuovi clienti e stimolando un coinvolgimento maggiore con quelli esistenti. Gestione API fornisce hello core competenze tooensure un programma API di successo attraverso coinvolgimento dei sviluppatori, ottenere informazioni aziendali accurate, analitica, sicurezza e protezione.

Guardare video per una panoramica di gestione API di Azure seguenti hello e scoprire come toouse gestione API tooadd molte funzionalità tooyour API, controllo di accesso, inclusi frequenza limitazione, monitoraggio, la registrazione degli eventi e risposta la memorizzazione nella cache, con uno sforzo minimo da parte dell'utente.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse gestione API, gli amministratori creano API. Ogni API è costituita da una o più operazioni e ogni API può essere aggiunta tooone o più prodotti. toouse un'API, gli sviluppatori sottoscrivono tooa prodotto che contiene tale API, e quindi possono chiamare operazione hello dell'API, soggetto dei criteri di utilizzo tooany che possono essere attive.

In questo argomento viene fornita una panoramica sui concetti chiave di Gestione API.

> [!NOTE]
> Per ulteriori informazioni, vedere hello [gestione API basata su Cloud: sfruttando hello API di Power](http://j.mp/ms-apim-whitepaper) white paper PDF. Questo white paper introduttivo sulla gestione delle API redatto da CITO Research tratta gli argomenti seguenti: 
> 
> * Problematiche e requisiti comuni delle API
> * Disaccoppiamento delle API e presentazione delle facciate
> * Rendere operativi gli sviluppatori rapidamente
> * Protezione dell'accesso
> * Analisi e metrica
> * Ottenere il controllo e la conoscenza con una piattaforma di gestione API
> * Uso di soluzioni cloud e locali a confronto
> * Gestione API di Azure
> 
> 

## <a name="apis"> </a>API e operazioni
API sono foundation hello di un'istanza del servizio Gestione API. Ogni API rappresenta un set di operazioni disponibili toodevelopers. Ogni API contiene un servizio back-end toohello di riferimento che implementa l'API di hello e le operazioni di mapping tra le operazioni di toohello implementate dal servizio back-end hello. Le operazioni in Gestione API sono altamente configurabili e offrono il controllo sul mapping degli URL, sui parametri di query e percorsi, sul contenuto della richiesta e della risposta e sulla memorizzazione nella cache della risposta delle operazioni. Limite di velocità, quote e i criteri di restrizione IP possono anche essere implementati a livello di singola operazione o hello API.

Per ulteriori informazioni, vedere [come toocreate API] [ How toocreate APIs] e [come tooadd operazioni tooan API][How tooadd operations tooan API].

## <a name="products"></a> Prodotti
I prodotti sono come le API vengono toodevelopers esposto. I prodotti in Gestione API contengono una o più API e sono configurati con un titolo, una descrizione e le condizioni per l'utilizzo. I prodotti possono essere **aperti** o **protetti**. Prodotti protetti devono essere toobefore sottoscritti possono essere utilizzati, aperti prodotti possono essere utilizzati senza alcuna sottoscrizione. Quando un prodotto è pronto per essere usato dagli sviluppatori, può essere pubblicato. Una volta la pubblicazione, può essere visualizzata (e in hello case protetti prodotto sottoscritto) dagli sviluppatori. L'approvazione della sottoscrizione è configurata a livello di prodotto hello e può essere richiedono l'approvazione dell'amministratore o approvata automaticamente.

I gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers. Prodotti concedono toogroups visibilità e gli sviluppatori possono visualizzare e sottoscrivere i prodotti toohello toohello visibili i gruppi in cui appartengono. 

Per ulteriori informazioni, vedere [come toocreate e pubblicazione di un prodotto] [ How toocreate and publish a product] e hello seguenti video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"></a> Gruppi
I gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers. Gestione API ha hello seguenti gruppi di sistema non modificabile.

* **Amministratori** : gli amministratori delle sottoscrizioni di Azure sono membri di questo gruppo. Gli amministratori di gestire le istanze del servizio Gestione API, la creazione di hello API, operazioni e i prodotti che vengono utilizzati dagli sviluppatori.
* **Sviluppatori** : gli utenti autenticati del portale per sviluppatori rientrano in questo gruppo. Gli sviluppatori hanno clienti hello che compilano applicazioni che utilizzano l'API. Gli sviluppatori sono concesse portale per sviluppatori di accesso toohello e compilare applicazioni che chiamano le operazioni di hello di un'API.
* **Gli utenti guest** -non autenticati gli utenti del portale per sviluppatori, ad esempio clienti potenziali, visitare il portale per sviluppatori hello di un passaggio di istanza di gestione API in questo gruppo. È possibile concedere alcuni accesso di sola lettura, ad esempio hello possibilità tooview API, ma li chiama.

Nei gruppi di sistema aggiunta toothese, gli amministratori possono creare gruppi personalizzati o [sfruttare gruppi esterni nel tenant di Azure Active Directory associato](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Personalizzati e i gruppi esterni possono essere utilizzati insieme ai gruppi di sistema in fornendo agli sviluppatori di visibilità e accedere tooAPI prodotti. Ad esempio, è possibile creare un gruppo personalizzato per gli sviluppatori associati a uno specifico partner dell'organizzazione e consentono loro l'accesso toohello API da un prodotto che contiene solo le API pertinente. Un utente può essere un membro di più gruppi.

Per ulteriori informazioni, vedere [come toocreate e utilizzare gruppi][How toocreate and use groups].

## <a name="developers"></a> Sviluppatori
Gli sviluppatori rappresentano gli account utente di hello in un'istanza del servizio Gestione API. Gli sviluppatori possono essere creati o invitato toojoin dagli amministratori, o possono iscriversi da hello [portale per sviluppatori][Developer portal]. Ogni sviluppatore è un membro di uno o più gruppi e può essere prodotti toohello che concedono gruppi toothose visibilità di sottoscrizione.

Quando gli sviluppatori sottoscrivono tooa prodotto essi vengono concesse chiave primaria e secondaria di hello per prodotto hello. Questa chiave viene usata quando si effettuano chiamate nell'API del prodotto hello.

Per ulteriori informazioni, vedere [come gli sviluppatori toocreate o invito] [ How toocreate or invite developers] e [come i gruppi con gli sviluppatori tooassociate][How tooassociate groups with developers].

## <a name="policies"></a> Criteri
I criteri sono una potente funzionalità di gestione API che consentono ai server di pubblicazione hello comportamento hello toochange di hello API tramite la configurazione. I criteri sono una raccolta di istruzioni che vengono eseguite in sequenza su richiesta hello o la risposta di un'API. Le istruzioni più comuni prevedono la conversione di formato dalla frequenza tooJSON e chiamare limitare toorestrict hello quantità di chiamate in ingresso da uno sviluppatore, XML e sono disponibili molti altri criteri.

Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello. Alcuni criteri, ad esempio hello [flusso di controllo](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) e [Imposta variabile](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) criteri sono basati su espressioni di criteri. Per ulteriori informazioni, vedere [criteri avanzati](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx), e hello espressioni di controllo seguente video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Per un elenco completo dei criteri di Gestione API, vedere [Riferimenti per i criteri][Policy reference]. Per altre informazioni sull'uso e la configurazione dei criteri, vedere [Criteri di Gestione API][API Management policies]. Per un'esercitazione sulla creazione di un prodotto con criteri per la limitazione della frequenza e per le quote, vedere [Come creare e configurare impostazioni di prodotto avanzate][How create and configure advanced product settings]. Per una demo, vedere hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"></a> Portale per sviluppatori
portale per sviluppatori Hello è in cui gli sviluppatori possono apprendere le operazioni API, visualizzazione e di chiamata e la sottoscrizione tooproducts. I clienti potenziali possono visitare il portale per sviluppatori di hello, visualizzare le API e le operazioni e iscrizione. Hello URL per il portale per sviluppatori si trova in dashboard hello in hello portale classico di Azure per l'istanza del servizio Gestione API.

Aggiunta di contenuto personalizzato, personalizzare gli stili e aggiungendo la personalizzazione, è possibile personalizzare hello aspetto del portale per sviluppatori.

## <a name="api-management-and-hello-api-economy"></a>Gestione API e hello economia di API
toolearn ulteriori informazioni sulla gestione API, hello espressioni di controllo seguente presentazione conferenza hello Microsoft Ignite 2015.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




