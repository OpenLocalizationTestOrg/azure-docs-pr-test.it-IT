---
title: aaaDebug l'applicazione dell'infrastruttura del servizio di Azure in Eclipse | Documenti Microsoft
description: "Migliorare hello affidabilità e prestazioni dei servizi, sviluppo e il debug in Eclipse in un cluster di sviluppo locale."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="76a1e-103">Eseguire il debug dell'applicazione Service Fabric di Java con Eclipse</span><span class="sxs-lookup"><span data-stu-id="76a1e-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76a1e-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="76a1e-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="76a1e-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="76a1e-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="76a1e-106">Avviare un cluster di sviluppo locale seguendo i passaggi di hello in [impostazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="76a1e-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="76a1e-107">Aggiornare entryPoint.sh del servizio hello desiderato toodebug, in modo che inizi il processo di java hello con i parametri di eseguire il debug remoto.</span><span class="sxs-lookup"><span data-stu-id="76a1e-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="76a1e-108">Questo file è reperibile in hello seguente posizione: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="76a1e-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="76a1e-109">In questo esempio la porta 8001 è impostata per il debug.</span><span class="sxs-lookup"><span data-stu-id="76a1e-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="76a1e-110">Aggiornare il manifesto dell'applicazione hello impostando il numero di istanze di hello o hello conteggio di replica per il servizio di hello che è in corso il debug too1.</span><span class="sxs-lookup"><span data-stu-id="76a1e-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="76a1e-111">Questa impostazione consente di evitare conflitti per la porta hello che viene utilizzato per il debug.</span><span class="sxs-lookup"><span data-stu-id="76a1e-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="76a1e-112">Ad esempio, per i servizi senza stati, impostare ``InstanceCount="1"`` e per i servizi con stati replica di destinazione e min hello set too1 dimensioni nel seguente modo: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="76a1e-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="76a1e-113">Distribuire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-113">Deploy hello application.</span></span>

5. <span data-ttu-id="76a1e-114">Nell'IDE di Eclipse hello, selezionare **esecuzione -> Debug Configurations -> applicazione Java remota e le proprietà di connessione di input** e impostare le proprietà di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="76a1e-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="76a1e-115">Impostare punti di interruzione in punti desiderati ed eseguire il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="76a1e-116">Se un'applicazione hello è arrestato in modo anomalo, è inoltre possibile tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="76a1e-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="76a1e-117">Eseguire ``ulimit -c`` in una shell e, se viene restituito 0, gli elementi core dump non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="76a1e-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="76a1e-118">tooenable coredumps illimitato, eseguire hello comando seguente: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="76a1e-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="76a1e-119">È inoltre possibile verificare lo stato di hello utilizzando il comando hello ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="76a1e-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="76a1e-120">Se si desidera percorso di generazione tooupdate hello coredump, eseguire ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="76a1e-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="76a1e-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76a1e-121">Next steps</span></span>

* <span data-ttu-id="76a1e-122">[Raccogliere log con Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="76a1e-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="76a1e-123">[Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="76a1e-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
