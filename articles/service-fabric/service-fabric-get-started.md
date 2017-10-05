---
title: Configurare un ambiente di sviluppo per i microservizi di Azure | Documentazione Microsoft
description: "Installare il runtime, l'SDK e gli strumenti e creare un cluster di sviluppo locale. Al termine della configurazione, sarà possibile iniziare a sviluppare applicazioni."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="afb90-104">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="afb90-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afb90-105">Windows</span><span class="sxs-lookup"><span data-stu-id="afb90-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="afb90-106">Linux</span><span class="sxs-lookup"><span data-stu-id="afb90-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="afb90-107">OSX</span><span class="sxs-lookup"><span data-stu-id="afb90-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="afb90-108">Per compilare ed eseguire [applicazioni di Service Fabric][1] nel computer di sviluppo, installare il runtime, l'SDK e gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="afb90-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="afb90-109">È anche necessario abilitare l'esecuzione di script Windows PowerShell inclusi nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="afb90-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afb90-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="afb90-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="afb90-111">Versioni del sistema operativo supportate</span><span class="sxs-lookup"><span data-stu-id="afb90-111">Supported operating system versions</span></span>
<span data-ttu-id="afb90-112">Per lo sviluppo, sono supportati i sistemi operativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="afb90-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="afb90-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="afb90-113">Windows 7</span></span>
* <span data-ttu-id="afb90-114">Windows 8 e Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="afb90-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="afb90-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="afb90-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="afb90-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="afb90-116">Windows Server 2016</span></span>
* <span data-ttu-id="afb90-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="afb90-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="afb90-118">Per impostazione predefinita, Windows 7 include solo Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="afb90-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="afb90-119">I cmdlet di PowerShell per Service Fabric richiedono PowerShell 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="afb90-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="afb90-120">È possibile [scaricare Windows PowerShell 5.0][powershell5-download] dall'Area download Microsoft.</span><span class="sxs-lookup"><span data-stu-id="afb90-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="afb90-121">Installare l'SDK e gli strumenti</span><span class="sxs-lookup"><span data-stu-id="afb90-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="afb90-122">Per usare Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="afb90-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="afb90-123">Gli strumenti di Service Fabric fanno parte del carico di lavoro di sviluppo e gestione di Azure in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="afb90-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="afb90-124">Abilitare questo carico di lavoro durante l'installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="afb90-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="afb90-125">È anche necessario installare Microsoft Azure Service Fabric SDK, usando Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="afb90-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="afb90-126">[Installare Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="afb90-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="afb90-127">Per usare Visual Studio 2015 (è necessario Visual Studio 2015 Update 2 o versioni successive)</span><span class="sxs-lookup"><span data-stu-id="afb90-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="afb90-128">Per Visual Studio 2015, gli strumenti di Service Fabric vengono installati con l'SDK, usando Installazione guidata piattaforma Web:</span><span class="sxs-lookup"><span data-stu-id="afb90-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="afb90-129">[Installare Microsoft Azure Service Fabric SDK e gli strumenti][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="afb90-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="afb90-130">Installazione solo dell'SDK</span><span class="sxs-lookup"><span data-stu-id="afb90-130">SDK installation only</span></span>
<span data-ttu-id="afb90-131">Se è necessario solo l'SDK, è possibile installare questo pacchetto:</span><span class="sxs-lookup"><span data-stu-id="afb90-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="afb90-132">[Installare Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="afb90-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="afb90-133">Le versioni correnti sono:</span><span class="sxs-lookup"><span data-stu-id="afb90-133">The current versions are:</span></span>
* <span data-ttu-id="afb90-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="afb90-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="afb90-135">Runtime di Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="afb90-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="afb90-136">Strumenti di Service Fabric per Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="afb90-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="afb90-137">Visual Studio 2017 Update 2 include Strumenti di Service Fabric per Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="afb90-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="afb90-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) include Strumenti di Service Fabric per Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="afb90-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="afb90-139">Per un elenco delle versioni supportate, vedere [Service Fabric support](service-fabric-support.md) (Supporto di Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="afb90-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="afb90-140">Consentire l'esecuzione di script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="afb90-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="afb90-141">Service Fabric usa script di Windows PowerShell per creare un cluster di sviluppo locale e per distribuire le applicazioni da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="afb90-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="afb90-142">Per impostazione predefinita, Windows blocca l'esecuzione di questi script.</span><span class="sxs-lookup"><span data-stu-id="afb90-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="afb90-143">Per abilitarli, è necessario modificare i criteri di esecuzione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afb90-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="afb90-144">A tale scopo, aprire PowerShell come amministratori e immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="afb90-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="afb90-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afb90-145">Next steps</span></span>
<span data-ttu-id="afb90-146">Dopo avere configurato l'ambiente di sviluppo, iniziare a compilare ed eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="afb90-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="afb90-147">Creare la prima applicazione Infrastruttura di servizi in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb90-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="afb90-148">Introduzione alla distribuzione e all'aggiornamento di applicazioni nel cluster locale</span><span class="sxs-lookup"><span data-stu-id="afb90-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="afb90-149">Informazioni sui modelli di programmazione Reliable Services e Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="afb90-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="afb90-150">Vedere gli esempi di codice di Service Fabric in GitHub</span><span class="sxs-lookup"><span data-stu-id="afb90-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="afb90-151">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="afb90-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="afb90-152">Seguire il percorso di apprendimento di Service Fabric per un'ampia Introduzione alla piattaforma</span><span class="sxs-lookup"><span data-stu-id="afb90-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="afb90-153">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="afb90-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="afb90-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Pagina della campagna di Service Fabric"</span><span class="sxs-lookup"><span data-stu-id="afb90-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="afb90-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="afb90-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="afb90-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Collegamento WebPI VS 2015"</span><span class="sxs-lookup"><span data-stu-id="afb90-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="afb90-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Collegamento WebPI Dev15"</span><span class="sxs-lookup"><span data-stu-id="afb90-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="afb90-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Collegamento WebPI Core SDK"</span><span class="sxs-lookup"><span data-stu-id="afb90-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
