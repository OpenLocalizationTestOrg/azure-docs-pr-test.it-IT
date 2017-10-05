---
title: Eseguire il debug dell'applicazione Azure Service Fabric in Eclipse | Microsoft Docs
description: "Migliorare l'affidabilità e le prestazioni dei servizi sviluppandoli ed eseguendone il debug in Eclipse in un cluster di sviluppo locale."
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
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="08ca2-103">Eseguire il debug dell'applicazione Service Fabric di Java con Eclipse</span><span class="sxs-lookup"><span data-stu-id="08ca2-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08ca2-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="08ca2-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="08ca2-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="08ca2-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="08ca2-106">Avviare un cluster di sviluppo locale seguendo la procedura descritta nell'articolo [Configurazione dell'ambiente di sviluppo di Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="08ca2-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="08ca2-107">Aggiornare l'elemento entryPoint.sh del servizio di cui eseguire il debug in modo che avvii il processo Java con i parametri di debug remoto.</span><span class="sxs-lookup"><span data-stu-id="08ca2-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="08ca2-108">Questo file si trova nel percorso seguente: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="08ca2-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="08ca2-109">In questo esempio la porta 8001 è impostata per il debug.</span><span class="sxs-lookup"><span data-stu-id="08ca2-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="08ca2-110">Aggiornare il manifesto dell'applicazione impostando il numero di istanze o di repliche per il servizio di cui eseguire il debug su 1.</span><span class="sxs-lookup"><span data-stu-id="08ca2-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="08ca2-111">Questa impostazione evita che si verifichino conflitti per la porta usata per il debug.</span><span class="sxs-lookup"><span data-stu-id="08ca2-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="08ca2-112">Per i servizi senza stato, ad esempio, impostare ``InstanceCount="1"``, mentre per i servizi con stato impostare la destinazione e le dimensioni minime del set di repliche su 1 nel modo seguente: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="08ca2-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="08ca2-113">Distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08ca2-113">Deploy the application.</span></span>

5. <span data-ttu-id="08ca2-114">Nell'IDE di Eclipse selezionare **Run (Esegui) -> Debug Configurations (Configurazioni di debug) -> Remote Java Application (Applicazione Java remota) e le proprietà di connessione di input** e impostare le proprietà come segue:</span><span class="sxs-lookup"><span data-stu-id="08ca2-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="08ca2-115">Impostare punti di interruzione nei punti desiderati ed eseguire il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08ca2-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="08ca2-116">Se l'applicazione si arresta in modo anomalo, è possibile abilitare elementi core dump.</span><span class="sxs-lookup"><span data-stu-id="08ca2-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="08ca2-117">Eseguire ``ulimit -c`` in una shell e, se viene restituito 0, gli elementi core dump non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="08ca2-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="08ca2-118">Per abilitare elementi core dump illimitati, eseguire questo comando: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="08ca2-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="08ca2-119">È anche possibile verificare lo stato usando il comando ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="08ca2-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="08ca2-120">Se si vuole aggiornare il percorso di generazione degli elementi core dump, eseguire ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="08ca2-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="08ca2-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08ca2-121">Next steps</span></span>

* <span data-ttu-id="08ca2-122">[Raccogliere log con Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="08ca2-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="08ca2-123">[Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="08ca2-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
