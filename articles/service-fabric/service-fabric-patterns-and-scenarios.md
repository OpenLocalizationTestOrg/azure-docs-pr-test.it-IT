---
title: aaaAzure Service Fabric modelli e gli scenari | Documenti Microsoft
description: Informazioni sulle procedure consigliate e dimostrato, toodesign modelli riutilizzabili, sviluppare e utilizzare il microservizi nell'infrastruttura del servizio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a>Modelli e scenari per Service Fabric
Se si sta consultando la creazione di microservizi su larga scala utilizzando Azure Service Fabric, imparare da hello esperti progettato e costruito questa piattaforma come servizio (PaaS). Introduzione a architettura corretta e poi Scopri come toooptimize risorse per l'applicazione. Hello [servizio Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) corso risposte hello domande spesso i clienti del mondo reale sugli scenari di Service Fabric e aree dell'applicazione.
 
Scoprire come toodesign, sviluppare e utilizzare il microservizi nell'infrastruttura del servizio utilizza le procedure consigliate e modelli e riutilizzabili. Si può iniziare da una panoramica di Service Fabric per poi procedere con vari argomenti di approfondimento come l'ottimizzazione e la sicurezza del cluster, la migrazione di applicazioni legacy, IoT su vasta scala, l'hosting di motori di gioco e altro ancora. Esaminare la distribuzione continua per diversi carichi di lavoro e anche ottenere dettagli hello sul supporto di Linux e i contenitori. 

## <a name="introduction"></a>Introduzione
Esplorare le procedure consigliate e raccogliere informazioni per la scelta di una piattaforma distribuita come servizio (PaaS, Platform as a Service) o un'infrastruttura distribuita come servizio (IaaS, Infrastructure as a Service). Recuperare i dettagli di hello sui principi di progettazione dell'applicazione si basa sulla collaudata seguenti.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduzione tooService dell'infrastruttura</a></td></tr>
</table>

## <a name="cluster-planning-and-management"></a>Pianificazione e gestione del cluster
Questa presentazione di Azure Service Fabric include informazioni sulla pianificazione della capacità, l'ottimizzazione del cluster e la sicurezza del cluster.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Pianificazione e gestione del cluster</a></td></tr>
</table>

## <a name="hyper-scale-web"></a>Web con iperscalabilità
Una presentazione dei concetti relativi al Web con iperscalabilità, incluse disponibilità e affidabilità, iperscalabilità e gestione dello stato.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Web con iperscalabilità</a></td></tr>
</table>

## <a name="iot"></a>IoT
Esplorare hello Internet delle cose (IoT) nel contesto di hello di Azure Service Fabric, tra cui hello Azure IoT pipeline, multi-tenancy e IoT su larga scala.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></td></tr>
</table>

## <a name="gaming"></a>Giochi
Informazioni sui giochi a turni, i giochi interattivi e l'hosting di motori di gioco esistenti.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Giochi</a></td></tr>
</table>

## <a name="continuous-delivery"></a>Recapito continuo
Presentazione dei concetti, tra i quali integrazione continua/recapito continuo con Visual Studio Team Services, flusso di lavoro di compilazione/creazione del pacchetto/pubblicazione, programma di installazione per più ambienti e pacchetto del servizio/condivisione.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Recapito continuo</a></td></tr>
</table>

## <a name="migration"></a>Migrazione
Informazioni sulla migrazione da un servizio cloud, inoltre toomigration delle applicazioni legacy.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migrazione</a></td></tr>
</table>

## <a name="containers-and-linux-support"></a>Contenitori e supporto di Linux
Ottenere una domanda a toohello risposta hello, "perché contenitori?" Informazioni sull'anteprima hello per i contenitori di Windows, Linux supporta e orchestrazione di contenitori di Linux. Inoltre, scoprire come toomigrate .NET Core App tooLinux.

<table><tr><th>Video</th><th>Presentazione di PowerPoint</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Contenitori e supporto Linux</a></td></tr>
</table>

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato sui modelli di Service Fabric e scenari, ulteriori informazioni su come troppo[creare e gestire cluster](service-fabric-deploy-anywhere.md), [eseguire la migrazione di servizi Cloud App tooService infrastruttura](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [impostare il recapito continuo](service-fabric-set-up-continuous-integration.md), e [distribuire contenitori](service-fabric-containers-overview.md).
