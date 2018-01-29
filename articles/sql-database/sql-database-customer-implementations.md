---
title: 'Implementazioni dei clienti del database SQL di Azure: dettagli tecnici | Microsoft Docs'
description: Dettagli tecnici sulle implementazioni dei clienti del database SQL di Azure per risolvere i problemi aziendali
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: Inactive
ms.date: 03/03/2017
ms.author: carlrab
ms.openlocfilehash: b22307ee0cade40370b096ee49bb15dcfd2f0071
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2017
---
# <a name="azure-sql-database-customer-implementation-technical-studies"></a>Studi tecnici sulle implementazioni dei clienti del database SQL di Azure

- [Daxko](sql-database-implementation-daxko.md): Daxko/CSI Software ha affrontato una sfida. La base di clienti dei centri fitness e di ricreazione ha registrato un aumento rapido grazie alla soluzione software aziendale onnicomprensiva. Il supporto delle esigenze dell'infrastruttura IT per la crescita della base di clienti metteva tuttavia a dura prova lo staff IT aziendale. La società era sempre più vincolata alle crescenti spese operative, in particolare per la gestione dei database in continua crescita. Ancor peggio, le spese operative venivano tagliate dalle risorse di sviluppo impegnate su nuove iniziative, tra cui le funzionalità di mobilità per il software aziendale.

- [GEP](sql-database-implementation-gep.md): GEP offre software e servizi che consentono ai responsabili dell'approvvigionamento in tutto il mondo di massimizzare l'impatto sulle operazioni, sulle strategie e sulle prestazioni finanziarie dell'azienda. Oltre ai servizi gestiti e di consulenza, l'azienda offre SMART by GEP®, una piattaforma software completa per l'approvvigionamento basata su cloud. GEP ha tuttavia riscontrato problemi nel tentativo di supportare soluzioni come SMART by GEP con il proprio data center locale: sono stati necessari importanti investimenti e i requisiti normativi in altri paesi hanno reso gli investimenti necessari un ostacolo in più. Con la migrazione al cloud, GEP ha liberato risorse IT che potevano trascurare le operazioni IT e concentrarsi maggiormente sullo sviluppo di nuove fonti di valore per i clienti in tutto il mondo.

- [SnelStart](sql-database-implementation-snelstart.md): SnelStart produce rinomati software di gestione aziendale e finanziaria per le piccole e medie imprese nei Paesi Bassi. I 55.000 clienti sono serviti da un organico composto da 110 dipendenti, tra cui 35 esperti del reparto IT. Grazie al passaggio dal software desktop a un'offerta Software come servizio (SaaS) compilata in Azure, SnelStart ha sfruttato al massimo i servizi incorporati, l'automazione della gestione tramite l'ambiente familiare in C# e l'ottimizzazione delle prestazioni e della scalabilità con provisioning eccessivo o insufficiente delle aziende, usando pool elastici. L'uso di Azure garantisce a SnelStart fluidità nello spostamento dei clienti tra ambiente locale e cloud.

- [Umbraco](sql-database-implementation-umbraco.md): per semplificare le distribuzioni ai clienti, Umbraco ha aggiunto Umbraco-as-a-Service (UaaS), un'offerta di Software-as-a-Service (SaaS) che esclude la necessità di distribuzioni locali, fornisce un ridimensionamento predefinito ed elimina il sovraccarico di gestione, consentendo agli sviluppatori di concentrarsi sull'innovazione dei prodotti invece che sulla gestione della soluzione. Umbraco offre tutti questi vantaggi basandosi sul modello Platform-as-a-Service (PaaS) flessibile offerto da Microsoft Azure.

- [Quorum](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database): Quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con il database SQL.

- [Quest](https://customers.microsoft.com/en-US/story/quest): Quest offre il servizio Spotlight su SQL Server Enterprise per garantire ai professionisti della gestione database i migliori strumenti disponibili per la protezione e lo spostamento dei dati e il controllo delle operazioni del database. Con Spotlight, Microsoft Azure e il database SQL di Azure, gli amministratori di database SQL Server possono monitorare, rilevare, diagnosticare e risolvere i problemi di prestazioni in SQL Server, dalla loro scrivania o dall'ufficio domestico.

- [Microsoft Dynamics](https://customers.microsoft.com/story/dynamics365operationsproductteam): questo breve case study evidenzia le procedure consigliate e le esperienze acquisite dal team di prodotto di Dynamics 365 for Operations nella migrazione al database SQL di Microsoft Azure, per offrire ai clienti una soluzione software come un servizio (SaaS) completamente gestita. Mediante Azure SQL Database il team Dynamics 365 for Operations ha gestito il servizio con meno personale grazie a una scalabilità intuitiva e a funzionalità di gestione predefinite come il backup automatico dei database, la conservazione dei backup di database, la disponibilità elevata e il ripristino di emergenza. Queste caratteristiche e la possibilità di aggiungere ai database elementi essenziali di automazione ha fatto di Azure SQL Database una piattaforma ideale per la configurazione di servizi su larga scala.

- [Microsoft OneDrive e SharePoint Online](https://customers.microsoft.com/story/microsoft-azure-sql-database-dicrete-manufacturing-united-states): questo breve case study racconta i retroscena della migrazione di Microsoft OneDrive e SharePoint Online al database SQL di Azure e descrive in che modo questa migrazione abbia consentito una gestione delle capacità elastica pressoché illimitata, riducendo inoltre in maniera significativa i costi operativi e il sovraccarico dell'infrastruttura.
