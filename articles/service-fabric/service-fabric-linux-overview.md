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
# <a name="service-fabric-on-linux"></a><span data-ttu-id="f5f4d-103">Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="f5f4d-103">Service Fabric on Linux</span></span>
<span data-ttu-id="f5f4d-104">Anteprima di Hello di Service Fabric in Linux consente toobuild, distribuire e gestire applicazioni a disponibilità elevata, estremamente scalabile in Linux, esattamente come in Windows.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="f5f4d-105">Framework di Service Fabric Hello (servizi affidabili e Reliable Actors) sono disponibili in Java su Linux in aggiunta tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="f5f4d-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="f5f4d-106">È anche possibile compilare [servizi eseguibili guest](service-fabric-deploy-existing-app.md) con qualsiasi linguaggio o framework.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="f5f4d-107">Inoltre, anteprima hello supporta anche l'orchestrazione contenitori Docker.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="f5f4d-108">Contenitori di docker è possono eseguire file eseguibili guest o i servizi di Service Fabric nativi, che utilizzano il framework di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="f5f4d-109">Service Fabric in Linux è concettualmente equivalente tooService Fabric in Windows (ad eccezione di specifiche del sistema operativo e il supporto del linguaggio di programmazione).</span><span class="sxs-lookup"><span data-stu-id="f5f4d-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="f5f4d-110">Di conseguenza, la maggior parte dei nostri [documentazione esistente](http://aka.ms/servicefabricdocs) si applica in che consentono acquisire familiarità con la tecnologia hello.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="f5f4d-111">Sistemi operativi e linguaggi di programmazione supportati</span><span class="sxs-lookup"><span data-stu-id="f5f4d-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="f5f4d-112">Hello limitato anteprima supporta la creazione hello di sviluppo di una casella cluster inoltre toomulti computer cluster in Azure in esecuzione Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="f5f4d-113">supporta l'anteprima Hello hello Reliable Actors e hello Framework di servizi senza stato affidabili in Java e c# in file eseguibili tooguest aggiunta e l'orchestrazione di contenitori di Docker.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5f4d-114">Le raccolte Reliable Collections non sono ancora supportate in Linux.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="f5f4d-115">Non sono supportati cluster solo stand - solo una casella o i cluster con più computer Linux di Azure sono supportati in anteprima hello.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="f5f4d-116">Strumenti supportati</span><span class="sxs-lookup"><span data-stu-id="f5f4d-116">Supported tooling</span></span>
<span data-ttu-id="f5f4d-117">Anteprima di Hello supporta l'interazione con il cluster hello tramite il servizio dell'infrastruttura CLI.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="f5f4d-118">Per gli sviluppatori Java viene offerta l'integrazione con Eclipse e Yeoman, con supporto di Eclipse in Linux e OSX.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="f5f4d-119">integrazione di OSX Hello utilizza una VM Linux quinte hello tramite vagrant.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="f5f4d-120">Per gli sviluppatori c#, integrazione con Yeoman viene realizzata toogenerate modelli di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5f4d-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f4d-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5f4d-121">Next steps</span></span>

* <span data-ttu-id="f5f4d-122">Acquisire familiarità con hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [servizi affidabili](service-fabric-reliable-services-introduction.md) Framework di programmazione</span><span class="sxs-lookup"><span data-stu-id="f5f4d-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="f5f4d-123">Preparare l'ambiente di sviluppo in Linux</span><span class="sxs-lookup"><span data-stu-id="f5f4d-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="f5f4d-124">Preparare l'ambiente di sviluppo in OSX</span><span class="sxs-lookup"><span data-stu-id="f5f4d-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="f5f4d-125">Creare la prima applicazione Java di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="f5f4d-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="f5f4d-126">Configurare l'integrazione e la distribuzione continue di Service Fabric con Jenkins e GitHub</span><span class="sxs-lookup"><span data-stu-id="f5f4d-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="f5f4d-127">Differenze in Service Fabric tra Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="f5f4d-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
