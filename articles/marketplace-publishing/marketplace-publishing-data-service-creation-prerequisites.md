---
title: Prerequisiti tecnici per la creazione di un servizio dati per il Marketplace | Microsoft Docs
description: "Informazioni sui requisiti per la creazione di un’offerta del servizio dati da distribuire e vendere in Azure Marketplace"
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
ms.openlocfilehash: 52827723477677bc292c645e2390c435fbad3ee4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-the-azure-marketplace"></a>Prerequisiti tecnici per la creazione di un’offerta del servizio dati per Azure Marketplace
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione aziendale SaaS che si vuole pubblicare in AppSource, è possibile trovare altre informazioni [qui](https://appsource.microsoft.com/partners). Se vuole invece pubblicare un'applicazione IaaS o un servizio per gli sviluppatori in Azure Marketplace, è possibile trovare altre informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Leggere attentamente le informazioni sul processo prima di iniziare e comprendere dove e perché viene eseguito ogni passaggio. Per quanto possibile, è necessario preparare le informazioni sulla società e altri dati, scaricare gli strumenti necessari e/o creare i componenti tecnici prima di iniziare il processo di creazione dell'offerta.

È necessario disporre dei seguenti elementi prima di iniziare il processo:

## <a name="make-a-decision-on-what-technology-will-be-used-to-publish-your-data-service-offer"></a>Prendere una decisione sulla tecnologia che verrà utilizzata per pubblicare l'offerta del servizio dati
Un autore può scegliere tra più tecnologie per la pubblicazione del servizio dati in Azure Marketplace. Le principali tecnologie supportate sono descritte di seguito. Indipendentemente dalla tecnologia utilizzata per pubblicare il servizio dati, l'utente finale utilizza i dati tramite il **feed OData** esposto dal servizio di Azure Marketplace. Informazioni dettagliate sul servizio OData sono disponibili nella [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure Database
Fare in modo che i set di dati siano disponibili in SQL Azure è responsabilità dell’autore. È necessario eseguire la sottoscrizione ad Azure, effettuare il provisioning di dimensioni appropriate del database e caricare i dati nel database di SQL Azure. L’autore è inoltre responsabile del mantenimento dei dati aggiornati. Ulteriori informazioni sulla sottoscrizione ai servizi di Azure è disponibile all’indirizzo [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Quando si spostano i dati in SQL Azure, Azure Marketplace può esporre le tabelle e le viste. L’autore può specificare quali tabelle/viste e colonne vengono esposte all'utente finale. Il provider di contenuti inoltre può specificare ulteriormente per quali colonne è possibile eseguire query da parte dell'utente finale e quali vengono restituite solo nel payload. Questo offre un elevato livello di flessibilità sui dati nel database che devono essere esposti. Le colonne per cui è possibile eseguire una query devono essere supportate da uno o più indici di database.

## <a name="rest-based-web-service"></a>Servizio Web basato su REST
Protocolli supportati: **solo HTTPS**

I servizi basati su REST esistenti possono essere esposti tramite Azure Marketplace. Poiché il set di dati è sempre esposto all'utente finale come feed OData, il servizio di Azure Marketplace deve essere in grado di eseguire il mapping del servizio in un servizio basato su OData. A tale scopo gli endpoint basati su REST devono esporre tutti i parametri come parametri HTTP.

Il payload deve essere in un forma che possa essere mappata in una risposta ATOM. Pertanto la risposta dai servizi devono essere in formato XML e può contenere solo un elemento ripetuto che contiene i valori del payload (ad esempio, il set di record). Il servizio di Azure Marketplace esegue il mapping del nodo ripetuto per il nodo di ingresso in ATOM e dei valori del payload in nodi di proprietà all'interno del nodo di ingresso.

Le informazioni di autorizzazione (ad esempio API chiave, token di autenticazione, ecc.) devono essere fornite come parametro HTTP o nell'intestazione HTTP (coppia chiave-valore): è supportata anche l'autenticazione di base. È necessario specificare una chiave valida e tutte le richieste tramite Azure Marketplace vengono effettuate tramite tale chiave. Il monitoraggio degli utenti e la fatturazione avvengono a livello di Azure Marketplace.

Gli errori restituiti dal servizio devono essere mappati in codici di stato HTTP. Nel caso in cui il servizio restituisca un elemento XML che contiene l'errore, questi verranno mappati dal servizio di Azure Marketplace in codici di stato HTTP.

## <a name="soap-based-web-services"></a>Servizi Web basati su SOAP
Protocollo: **solo HTTPS**

I requisiti sono che gli stessi della sezione del servizio basata su REST. L'unica differenza è che i parametri possono essere forniti anche in un corpo XML che viene inviato al servizio dell’autore con ogni richiesta effettuata tramite Azure Marketplace. Ciò significa che i parametri HTTP forniti dall'utente al front-end sono convertiti in elementi XML di un documento XML che viene pubblicato con la richiesta al servizio Web del provider di contenuti.

## <a name="odata-based-web-services"></a>Servizi Web basati su OData
Protocollo: **solo HTTPS**

I dati possono essere esposti come servizio OData in Azure Marketplace. Il sistema passa attraverso il servizio e sostituisce la radice del servizio con la radice del servizio Azure Marketplace per garantire che tutte le chiamate successive passino attraverso Azure Marketplace.

I servizi OData non devono passare solo in un database back-end. OData supporta qualsiasi tipo di archiviazione o logica di business per supportare il servizio.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere esaminato i prerequisiti e aver completato le attività necessarie, ora è possibile procedere alla creazione dell'offerta del servizio dati, come illustrato in dettaglio nella [Guida alla pubblicazione di un servizio dati](marketplace-publishing-data-service-creation.md).

Se si desidera rivedere il processo generale e i rispettivi articoli per ognuna delle fasi di pubblicazione, consultare l'articolo [Guida introduttiva: come pubblicare un'offerta in Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
