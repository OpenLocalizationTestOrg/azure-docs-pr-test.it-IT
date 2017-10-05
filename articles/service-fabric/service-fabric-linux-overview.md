---
title: Azure Service Fabric in Linux | Documentazione Microsoft
description: I cluster di Service Fabric supportano Linux e Java, per cui le applicazioni Service Fabric scritte in Java e C# possono essere distribuite e ospitate in Linux.
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
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="e5afe-103">Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="e5afe-103">Service Fabric on Linux</span></span>
<span data-ttu-id="e5afe-104">L'anteprima di Service Fabric su Linux, consente di compilare, distribuire e gestire applicazioni a disponibilità e scalabilità elevata in tale ambiente proprio come in Windows.</span><span class="sxs-lookup"><span data-stu-id="e5afe-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="e5afe-105">I framework di Service Fabric (Reliable Services e Reliable Actors) sono disponibili in Java su Linux in aggiunta a C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="e5afe-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="e5afe-106">È anche possibile compilare [servizi eseguibili guest](service-fabric-deploy-existing-app.md) con qualsiasi linguaggio o framework.</span><span class="sxs-lookup"><span data-stu-id="e5afe-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="e5afe-107">L'anteprima, inoltre, supporta contenitori Docker di orchestrazione,</span><span class="sxs-lookup"><span data-stu-id="e5afe-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="e5afe-108">che possono eseguire eseguibili guest o servizi nativi di Service Fabric, che usano i framework di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e5afe-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="e5afe-109">Concettualmente, Service Fabric in Linux è equivalente a ServiceFabric in Windows (tranne per le specifiche del sistema operativo e il supporto del linguaggio di programmazione).</span><span class="sxs-lookup"><span data-stu-id="e5afe-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="e5afe-110">Di conseguenza, la maggior parte della [documentazione esistente](http://aka.ms/servicefabricdocs) è valida e consente di acquisire familiarità con la tecnologia.</span><span class="sxs-lookup"><span data-stu-id="e5afe-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="e5afe-111">Sistemi operativi e linguaggi di programmazione supportati</span><span class="sxs-lookup"><span data-stu-id="e5afe-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="e5afe-112">L'anteprima limitata supporta la creazione di cluster di sviluppo con un solo computer, oltre ai cluster con più computer in Azure che eseguono Ubuntu Server 16.04.</span><span class="sxs-lookup"><span data-stu-id="e5afe-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="e5afe-113">L'anteprima supporta i framework Reliable Actors e Reliable Services senza stato in Java e C#, oltre a eseguibili guest e contenitori Docker di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="e5afe-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="e5afe-114">Le raccolte Reliable Collections non sono ancora supportate in Linux.</span><span class="sxs-lookup"><span data-stu-id="e5afe-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="e5afe-115">Non sono supportati anche i cluster autonomi. Nell'anteprima sono supportati solo cluster con un solo computer e più computer Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5afe-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="e5afe-116">Strumenti supportati</span><span class="sxs-lookup"><span data-stu-id="e5afe-116">Supported tooling</span></span>
<span data-ttu-id="e5afe-117">L'anteprima supporta l'interazione con il cluster tramite l'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e5afe-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="e5afe-118">Per gli sviluppatori Java viene offerta l'integrazione con Eclipse e Yeoman, con supporto di Eclipse in Linux e OSX.</span><span class="sxs-lookup"><span data-stu-id="e5afe-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="e5afe-119">Per l'integrazione in OSX viene usata in background una VM Linux tramite Vagrant.</span><span class="sxs-lookup"><span data-stu-id="e5afe-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="e5afe-120">Per gli sviluppatori C# viene offerta l'integrazione don Yeoman per la generazione di modelli di applicazione.</span><span class="sxs-lookup"><span data-stu-id="e5afe-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5afe-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5afe-121">Next steps</span></span>

* <span data-ttu-id="e5afe-122">Acquisire familiarità con i framework di programmazione [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [Reliable Services](service-fabric-reliable-services-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e5afe-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="e5afe-123">Preparare l'ambiente di sviluppo in Linux</span><span class="sxs-lookup"><span data-stu-id="e5afe-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="e5afe-124">Preparare l'ambiente di sviluppo in OSX</span><span class="sxs-lookup"><span data-stu-id="e5afe-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="e5afe-125">Creare la prima applicazione Java di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="e5afe-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="e5afe-126">Configurare l'integrazione e la distribuzione continue di Service Fabric con Jenkins e GitHub</span><span class="sxs-lookup"><span data-stu-id="e5afe-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="e5afe-127">Differenze in Service Fabric tra Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="e5afe-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
