---
title: Prerequisiti per la creazione di un servizio dati per hello Marketplace aaaTechnical | Documenti Microsoft
description: Comprendere i requisiti di hello per la creazione di un servizio dati di toodeploy e vendere su hello Azure Marketplace
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>I requisiti tecnici per la creazione di un servizio dati offrono per hello Azure Marketplace
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners). Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Processo hello accuratamente prima di iniziare leggere e comprendere dove e perché viene eseguita ogni passaggio. Per quanto possibile, è necessario preparare le informazioni della società e altri dati, scaricare gli strumenti necessari, e/o creare componenti tecnici prima di iniziare il processo di creazione offerta hello.

È necessario avere hello pronti prima di iniziare il processo di hello gli elementi seguenti:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Prendere una decisione su quale tecnologia verrà utilizzata toopublish l'offerta di servizio dati
Un autore può scegliere tra più tecnologie per la pubblicazione del servizio dati in Azure Marketplace. Hello principali tecnologie supportate descritte di seguito. Indipendentemente dal fatto che la tecnologia hello toopublish utilizzato il servizio dati, dell'utente finale hello utilizza i dati di hello tramite hello **feed OData** esposte dal servizio di Azure Marketplace. Informazioni dettagliate sul servizio OData sono disponibili nella [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure Database
Fare in modo che i set di dati siano disponibili in SQL Azure è responsabilità dell’autore. TooAzure toosubscribe, sarà necessario eseguire il provisioning di dimensioni appropriate del Database e caricare i dati in database SQL di Azure. Server di pubblicazione è anche responsabile tookeep suo dati sempre aggiornati. Ulteriori informazioni sulla sottoscrizione tooAzure servizi è possibile trovare nel [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Quando si spostano dati hello in SQL Azure, è possibile esporre hello Azure Marketplace tabelle e viste. Hello Publisher è possibile specificare quali tabelle e viste e colonne vengono esposti toohello dati gestito dall'utente. Altri provider di contenuti hello è inoltre possibile specificare le colonne che possono eseguire query per l'utente finale hello e quelle che vengono restituiti solo nel payload hello. In questo modo un elevato livello di flessibilità sui dati nel database di hello devono essere esposti. Colonne che è possibile eseguire query che richiedono toobe supportato da uno o più indici di database.

## <a name="rest-based-web-service"></a>Servizio Web basato su REST
Protocolli supportati: **solo HTTPS**

Servizi basati su REST esistenti possono essere esposti attraverso hello Azure Marketplace. Poiché set di dati hello è sempre gestito dall'utente toohello esposti come feed OData, hello del servizio di Azure Marketplace deve toomap in grado di toobe hello tooa servizio OData basato su servizio. toodo endpoint basata su REST hello necessario tooexpose tutti i parametri come parametri HTTP.

payload Hello deve toobe in un formato che può essere mappato in una risposta ATOM. Di conseguenza risposta hello dai servizi di hello deve toobe in formato XML e può contenere solo un elemento ripetuto che contiene i valori di payload hello (ad esempio, il set di record). verrà eseguito il mapping hello ripetute di nodi voce toohello nei valori di payload ATOM e hello in nodi di proprietà nel nodo voce hello Hello del servizio di Azure Marketplace.

Informazioni di autorizzazione (ad esempio API chiave, l'autenticazione token, ecc.) devono toobe fornito come parametro di HTTP o nell'intestazione HTTP hello (coppia chiave-valore): l'autenticazione di base è anche supportato. Una chiave valida deve toobe fornita e tutte le richieste tramite Azure Marketplace vengono inoltrate tramite tale chiave. Utente di monitoraggio e la fatturazione avviene a livello di hello Azure Marketplace.

Gli errori restituiti dal servizio hello necessario toobe mappati in codici di stato HTTP. Nel caso in cui il servizio di hello restituisce un elemento XML che contiene l'errore hello questi sta toobe eseguito il mapping dai codici di stato tooHTTP servizio hello Azure Marketplace.

## <a name="soap-based-web-services"></a>Servizi Web basati su SOAP
Protocollo: **solo HTTPS**

requisiti di Hello sono hello stesso come nella sezione di servizio basata su REST hello. Hello unica differenza è che i parametri possono anche essere forniti in un corpo XML che viene inserito il servizio del server di pubblicazione di toohello con ogni richiesta effettuata tramite Azure Marketplace. Questo significa che utente hello di parametri HTTP garantisce al front-end hello tradotta in elementi XML di un documento XML che viene registrata con il servizio web hello richiesta toohello del provider di contenuti.

## <a name="odata-based-web-services"></a>Servizi Web basati su OData
Protocollo: **solo HTTPS**

Dati possono essere esposto come un tooAzure servizio OData Marketplace. sistema Hello è toopass continua servizio hello tramite e sostituisce radice hello servizio hello con radice del servizio Azure Marketplace hello – tooensure passano tutte le chiamate successive tramite Azure Marketplace.

Servizi OData non è sufficiente toogo in un database back-end hello. OData supporta qualsiasi tipo di archiviazione o business logica toodrive hello del servizio.

## <a name="next-steps"></a>Passaggi successivi
Ora che si verificati prerequisiti hello e completare le attività necessarie hello, è possibile spostare in avanti con la creazione dell'offerta di servizio dati come descritto in dettaglio nella hello hello [Guida alla pubblicazione di dati del servizio](marketplace-publishing-data-service-creation.md).

O, se si desidera hello tooreview processo complessivo e articoli hello per ogni pubblicazione fasi hello, visitare articolo hello [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
