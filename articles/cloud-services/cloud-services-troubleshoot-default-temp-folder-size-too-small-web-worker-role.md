---
title: dimensioni della cartella TEMP aaaDefault sono troppo piccola per un ruolo | Documenti Microsoft
description: "Un ruolo del servizio cloud dispone di una quantità limitata di spazio per la cartella TEMP hello. In questo articolo vengono forniti alcuni suggerimenti su come tooavoid sta esaurendo lo spazio."
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
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="25ef2-104">Dimensioni della cartella TEMP predefinita ridotte per un ruolo di lavoro/Web del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="25ef2-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="25ef2-105">Per impostazione predefinita Hello directory temporanea di un ruolo web o di lavoro del servizio cloud ha una dimensione massima di 100 MB, che possono diventare completo a un certo punto.</span><span class="sxs-lookup"><span data-stu-id="25ef2-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="25ef2-106">Questo articolo viene descritto come tooavoid sta esaurendo lo spazio per la directory temporanea di hello.</span><span class="sxs-lookup"><span data-stu-id="25ef2-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="25ef2-107">Perché ho esaurito lo spazio?</span><span class="sxs-lookup"><span data-stu-id="25ef2-107">Why do I run out of space?</span></span>
<span data-ttu-id="25ef2-108">Hello standard Windows variabili di ambiente TEMP e TMP sono disponibili toocode che è in esecuzione nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25ef2-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="25ef2-109">Sia TEMP e TMP tooa punto singola directory con una dimensione massima di 100 MB.</span><span class="sxs-lookup"><span data-stu-id="25ef2-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="25ef2-110">Tutti i dati vengono archiviati in questa directory non sono persistente nel ciclo di vita di hello del servizio cloud hello; Se le istanze del ruolo hello in un servizio cloud vengono riciclate, directory di hello viene pulita.</span><span class="sxs-lookup"><span data-stu-id="25ef2-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="25ef2-111">Problema di hello toofix suggerimento</span><span class="sxs-lookup"><span data-stu-id="25ef2-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="25ef2-112">Implementare una delle seguenti alternative hello:</span><span class="sxs-lookup"><span data-stu-id="25ef2-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="25ef2-113">Configurare una risorsa di archiviazione locale e accedervi direttamente invece che usando TEMP o TMP.</span><span class="sxs-lookup"><span data-stu-id="25ef2-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="25ef2-114">una risorsa di archiviazione locale dal codice che è in esecuzione all'interno dell'applicazione, chiamata hello tooaccess [roleenvironment. Getlocalresource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="25ef2-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="25ef2-115">Configurare una risorsa di archiviazione locale e scegliere hello TEMP e TMP directory toopoint toohello percorso della risorsa di archiviazione locale di hello.</span><span class="sxs-lookup"><span data-stu-id="25ef2-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="25ef2-116">Questa modifica deve essere eseguita all'interno di hello [Roleentrypoint](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="25ef2-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="25ef2-117">Hello esempio di codice seguente viene illustrato come toomodify hello directory di destinazione per TEMP e TMP dal metodo OnStart hello:</span><span class="sxs-lookup"><span data-stu-id="25ef2-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
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

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="25ef2-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25ef2-118">Next steps</span></span>
<span data-ttu-id="25ef2-119">Lettura di un blog che descrive [come tooincrease hello dimensioni della cartella temporanea ASP.NET ruolo Web Azure hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="25ef2-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="25ef2-120">Altri [articoli sulla risoluzione dei problemi](/?tag=top-support-issue&product=cloud-services) per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="25ef2-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="25ef2-121">toolearn come ruolo del servizio cloud tootroubleshoot problemi utilizzando i dati di diagnostica di Azure PaaS computer, visualizzare [serie di blog di Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="25ef2-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
