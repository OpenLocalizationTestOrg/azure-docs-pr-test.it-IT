---
title: aaaService Panoramica sul modello di programmazione dell'infrastruttura | Documenti Microsoft
description: "Service Fabric offre due Framework per la creazione di servizi: hello framework attore e framework di servizi di hello. Offrono compromessi diversi nel controllo nella semplicità e nel controllo."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Panoramica dei modelli di programmazione di Service Fabric
Infrastruttura del servizio sono disponibili più modi toowrite e gestire i servizi. Servizi possono scegliere toouse hello API dei servizi dell'infrastruttura tootake appieno le funzionalità della piattaforma hello e Framework. I servizi possono essere anche qualsiasi programma eseguibile compilato scritto in qualsiasi linguaggio o qualsiasi codice eseguito in un contenitore e ospitato in un cluster di Service Fabric.

## <a name="guest-executables"></a>Eseguibili guest
Un [eseguibile guest](service-fabric-deploy-existing-app.md) è un eseguibile arbitrario esistente, scritto in un qualsiasi linguaggio, che può essere eseguito come servizio nell'applicazione. File eseguibili guest non chiamano direttamente hello API SDK dei servizi dell'infrastruttura. Tuttavia ancora vantaggio da una piattaforma di hello funzionalità offre, ad esempio individuazione del servizio, stato personalizzato e carico reporting chiamando le API REST esposta dall'infrastruttura del servizio. Gli eseguibili guest dispongono anche di supporto completo del ciclo di vita dell'applicazione.

Introduzione agli eseguibili guest con distribuzione della prima [applicazione eseguibile guest](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Contenitori
Per impostazione predefinita, Service Fabric distribuisce e attiva i servizi come processi. Service Fabric può anche distribuire servizi in [contenitori](service-fabric-containers-overview.md). Service Fabric supporta la distribuzione di contenitori di Linux e contenitori di Windows in Windows Server 2016. Le immagini contenitore possono essere recuperate da qualsiasi repository del contenitore e distribuita toohello macchina. È possibile distribuire le applicazioni esistenti come guest exectuables, affidabili servizi di Service Fabric con stati o senza informazioni sullo stato o Reliable Actors in contenitori ed è possibile combinare servizi nei processi e servizi in contenitori hello stessa applicazione.

[Altre informazioni sull'inserimento in contenitori dei servizi in Windows o Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Servizi affidabili è un framework leggeri per la scrittura di servizi che si integrano con la piattaforma Service Fabric hello e trarre vantaggio dal set completo di hello di funzionalità della piattaforma. Servizi affidabili forniscono un set di API che consentono di hello Service Fabric runtime toomanage hello del ciclo di vita dei servizi e di toointeract i servizi con runtime hello minimo. framework applicazione Hello è minimo, offrendo completo controllare le opzioni di progettazione e implementazione e può essere utilizzato toohost altri framework di applicazione, ad esempio ASP.NET Core.

Servizi affidabili possono essere piattaforme servizio toomost senza stato, in modo analogo, ad esempio server web, in cui ogni istanza del servizio hello viene creato uguale e lo stato viene mantenuto in una soluzione esterna, ad esempio database di Azure o l'archiviazione tabelle di Azure.

Servizi affidabili possono inoltre essere tooService esclusivo, informazioni sullo stato dell'infrastruttura, in cui lo stato mantenuto direttamente nel servizio hello utilizzando raccolte affidabile. Lo stato viene reso altamente disponibile tramite la replica e distribuito tramite partizionamento, il tutto gestito automaticamente da Service Fabric.

Vedere anche [altre informazioni su Reliable Services](service-fabric-reliable-services-introduction.md) oppure iniziare a [scrivere per la prima volta Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Basato su servizi affidabili, framework Reliable Actor hello è un framework di un'applicazione che implementa il pattern Actor virtuale hello, basato sul modello di progettazione di hello attore. il framework di Reliable Actor Hello utilizza unità indipendenti di calcolo e di stato con l'esecuzione a thread singolo chiamati attori. framework Reliable Actor Hello fornisce comunicazione predefinita per gli attori e le configurazioni di stato di persistenza e la scalabilità orizzontale.

Reliable Actors stessa è un framework di applicazione basato su servizi affidabili, è completamente integrato con piattaforma Service Fabric hello e trae vantaggio da una serie completa di hello delle funzionalità offerte dalla piattaforma hello.

Vedere anche [altre informazioni su Reliable Actors](service-fabric-reliable-actors-introduction.md) oppure iniziare a [scrivere per la prima volta un servizio di tipo Reliable Actor](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric si integra con [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) per la creazione di servizi Web e API che possono essere inclusi come parte dell'applicazione. 

[Creare un servizio front-end usando ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Passaggi successivi
[Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)

[Panoramica di Reliable Services](service-fabric-reliable-services-introduction.md)

[Panoramica di Reliable Services](service-fabric-reliable-actors-introduction.md)

[Service Fabric e ASP.NET Core ](service-fabric-reliable-services-communication-aspnetcore.md)




