---
title: Dimensioni della cartella TEMP predefinita ridotte per un ruolo | Documentazione Microsoft
description: "Un ruolo del servizio cloud dispone di una quantità limitata di spazio per la cartella TEMP. Questo articolo fornisce alcuni suggerimenti su come evitare l'esaurimento dello spazio."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="c02bd-104">Dimensioni della cartella TEMP predefinita ridotte per un ruolo di lavoro/Web del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="c02bd-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="c02bd-105">La directory temporanea predefinita di un ruolo Web o di lavoro del servizio cloud ha una dimensione massima di 100 MB, che può esaurirsi.</span><span class="sxs-lookup"><span data-stu-id="c02bd-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="c02bd-106">Questo articolo descrive come evitare l'esaurimento dello spazio della directory temporanea.</span><span class="sxs-lookup"><span data-stu-id="c02bd-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="c02bd-107">Perché ho esaurito lo spazio?</span><span class="sxs-lookup"><span data-stu-id="c02bd-107">Why do I run out of space?</span></span>
<span data-ttu-id="c02bd-108">Le variabili di ambiente Windows standard, TEMP e TMP, sono disponibili per il codice in esecuzione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c02bd-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="c02bd-109">Sia TEMP che TMP puntano a una singola directory con una dimensione massima di 100 MB.</span><span class="sxs-lookup"><span data-stu-id="c02bd-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="c02bd-110">Tutti i dati archiviati in questa directory non sono persistenti nel ciclo di vita del servizio cloud. Se le istanze del ruolo in un servizio cloud vengono riciclate, la directory viene pulita.</span><span class="sxs-lookup"><span data-stu-id="c02bd-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="c02bd-111">Suggerimento per risolvere il problema</span><span class="sxs-lookup"><span data-stu-id="c02bd-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="c02bd-112">Implementare una delle alternative seguenti:</span><span class="sxs-lookup"><span data-stu-id="c02bd-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="c02bd-113">Configurare una risorsa di archiviazione locale e accedervi direttamente invece che usando TEMP o TMP.</span><span class="sxs-lookup"><span data-stu-id="c02bd-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="c02bd-114">Per accedere a una risorsa di archiviazione locale dal codice in esecuzione nell'applicazione, chiamare il metodo [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c02bd-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="c02bd-115">Configurare una risorsa di archiviazione locale e definire le directory TEMP e TMP in modo che puntino al percorso della risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="c02bd-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="c02bd-116">Questa modifica deve essere eseguita nel metodo [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c02bd-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="c02bd-117">L'esempio di codice seguente illustra come modificare le directory di destinazione per TEMP e TMP nel metodo OnStart:</span><span class="sxs-lookup"><span data-stu-id="c02bd-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c02bd-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c02bd-118">Next steps</span></span>
<span data-ttu-id="c02bd-119">Vedere il blog [How to increase the size of the Windows Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx)(Come aumentare le dimensioni della cartella temporanea ASP.NET del ruolo Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="c02bd-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="c02bd-120">Altri [articoli sulla risoluzione dei problemi](/?tag=top-support-issue&product=cloud-services) per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="c02bd-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="c02bd-121">Per informazioni su come risolvere i problemi dei ruoli del servizio cloud usando i dati di diagnostica del computer Azure PaaS, vedere la [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="c02bd-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
