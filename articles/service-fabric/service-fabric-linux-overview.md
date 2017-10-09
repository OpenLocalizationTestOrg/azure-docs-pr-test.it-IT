---
title: aaaAzure Service Fabric in Linux | Documenti Microsoft
description: "I cluster di Service Fabric supportano Linux e Java, ovvero che sarà in grado di toodeploy e applicazioni di Service Fabric host scritte in Java e c# in Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric in Linux
Anteprima di Hello di Service Fabric in Linux consente toobuild, distribuire e gestire applicazioni a disponibilità elevata, estremamente scalabile in Linux, esattamente come in Windows. Framework di Service Fabric Hello (servizi affidabili e Reliable Actors) sono disponibili in Java su Linux in aggiunta tooC # (.NET Core).  È anche possibile compilare [servizi eseguibili guest](service-fabric-deploy-existing-app.md) con qualsiasi linguaggio o framework. Inoltre, anteprima hello supporta anche l'orchestrazione contenitori Docker. Contenitori di docker è possono eseguire file eseguibili guest o i servizi di Service Fabric nativi, che utilizzano il framework di Service Fabric hello.

Service Fabric in Linux è concettualmente equivalente tooService Fabric in Windows (ad eccezione di specifiche del sistema operativo e il supporto del linguaggio di programmazione). Di conseguenza, la maggior parte dei nostri [documentazione esistente](http://aka.ms/servicefabricdocs) si applica in che consentono acquisire familiarità con la tecnologia hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Sistemi operativi e linguaggi di programmazione supportati
Hello limitato anteprima supporta la creazione hello di sviluppo di una casella cluster inoltre toomulti computer cluster in Azure in esecuzione Ubuntu Server 16.04. supporta l'anteprima Hello hello Reliable Actors e hello Framework di servizi senza stato affidabili in Java e c# in file eseguibili tooguest aggiunta e l'orchestrazione di contenitori di Docker.  

> [!NOTE]
> Le raccolte Reliable Collections non sono ancora supportate in Linux. Non sono supportati cluster solo stand - solo una casella o i cluster con più computer Linux di Azure sono supportati in anteprima hello.
>
>


## <a name="supported-tooling"></a>Strumenti supportati
Anteprima di Hello supporta l'interazione con il cluster hello tramite il servizio dell'infrastruttura CLI. Per gli sviluppatori Java viene offerta l'integrazione con Eclipse e Yeoman, con supporto di Eclipse in Linux e OSX. integrazione di OSX Hello utilizza una VM Linux quinte hello tramite vagrant. Per gli sviluppatori c#, integrazione con Yeoman viene realizzata toogenerate modelli di applicazione.

## <a name="next-steps"></a>Passaggi successivi

* Acquisire familiarità con hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [servizi affidabili](service-fabric-reliable-services-introduction.md) Framework di programmazione
* [Preparare l'ambiente di sviluppo in Linux](service-fabric-get-started-linux.md)
* [Preparare l'ambiente di sviluppo in OSX](service-fabric-get-started-mac.md)
* [Creare la prima applicazione Java di Service Fabric in Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Configurare l'integrazione e la distribuzione continue di Service Fabric con Jenkins e GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Differenze in Service Fabric tra Windows e Linux](service-fabric-linux-windows-differences.md)
