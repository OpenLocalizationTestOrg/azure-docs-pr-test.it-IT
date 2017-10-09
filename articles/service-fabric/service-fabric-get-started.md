---
title: aaaSet un ambiente di sviluppo per Azure microservizi | Documenti Microsoft
description: "Installare il runtime di hello, SDK e strumenti e creare un cluster di sviluppo locale. Dopo aver completato il programma di installazione, sarà pronto toobuild applicazioni."
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
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="f09cf-104">Preparare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="f09cf-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f09cf-105">Windows</span><span class="sxs-lookup"><span data-stu-id="f09cf-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="f09cf-106">Linux</span><span class="sxs-lookup"><span data-stu-id="f09cf-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="f09cf-107">OSX</span><span class="sxs-lookup"><span data-stu-id="f09cf-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="f09cf-108">toobuild ed eseguire [applicazioni Azure Service Fabric] [ 1] nel computer di sviluppo, installare il runtime di hello, SDK e strumenti.</span><span class="sxs-lookup"><span data-stu-id="f09cf-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="f09cf-109">È inoltre necessario tooenable esecuzione degli script di Windows PowerShell hello incluso in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="f09cf-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f09cf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f09cf-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="f09cf-111">Versioni del sistema operativo supportate</span><span class="sxs-lookup"><span data-stu-id="f09cf-111">Supported operating system versions</span></span>
<span data-ttu-id="f09cf-112">Hello seguenti versioni del sistema operativo è supportato per lo sviluppo:</span><span class="sxs-lookup"><span data-stu-id="f09cf-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="f09cf-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="f09cf-113">Windows 7</span></span>
* <span data-ttu-id="f09cf-114">Windows 8 e Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="f09cf-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="f09cf-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f09cf-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="f09cf-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f09cf-116">Windows Server 2016</span></span>
* <span data-ttu-id="f09cf-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="f09cf-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="f09cf-118">Per impostazione predefinita, Windows 7 include solo Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="f09cf-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="f09cf-119">I cmdlet di PowerShell per Service Fabric richiedono PowerShell 3.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f09cf-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="f09cf-120">È possibile [scaricare Windows PowerShell 5.0] [ powershell5-download] da hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="f09cf-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="f09cf-121">Installare gli strumenti e SDK hello</span><span class="sxs-lookup"><span data-stu-id="f09cf-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="f09cf-122">toouse 2017 di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f09cf-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="f09cf-123">Strumenti di Service Fabric fanno parte di hello Azure sviluppo e gestione del carico di lavoro in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f09cf-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="f09cf-124">Abilitare questo carico di lavoro durante l'installazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f09cf-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="f09cf-125">Inoltre, è necessario tooinstall hello Microsoft Azure Service Fabric SDK, tramite l'installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="f09cf-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="f09cf-126">[Installare Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="f09cf-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="f09cf-127">toouse Visual Studio 2015 (richiede Visual Studio 2015 Update 2 o versioni successive)</span><span class="sxs-lookup"><span data-stu-id="f09cf-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="f09cf-128">Per Visual Studio 2015, gli strumenti di Service Fabric vengono installati insieme a SDK, tramite l'installazione guidata piattaforma Web hello hello:</span><span class="sxs-lookup"><span data-stu-id="f09cf-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="f09cf-129">[Installare Microsoft Azure Service Fabric SDK hello e strumenti][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="f09cf-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="f09cf-130">Installazione solo dell'SDK</span><span class="sxs-lookup"><span data-stu-id="f09cf-130">SDK installation only</span></span>
<span data-ttu-id="f09cf-131">Se è necessario solo hello SDK, è possibile installare questo pacchetto:</span><span class="sxs-lookup"><span data-stu-id="f09cf-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="f09cf-132">[Installare Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="f09cf-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="f09cf-133">le versioni correnti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="f09cf-133">hello current versions are:</span></span>
* <span data-ttu-id="f09cf-134">Service Fabric SDK 2.7.198</span><span class="sxs-lookup"><span data-stu-id="f09cf-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="f09cf-135">Runtime di Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="f09cf-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="f09cf-136">Strumenti di Service Fabric per Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="f09cf-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="f09cf-137">Visual Studio 2017 Update 2 include Strumenti di Service Fabric per Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="f09cf-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="f09cf-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) include Strumenti di Service Fabric per Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="f09cf-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="f09cf-139">Per un elenco delle versioni supportate, vedere [Service Fabric support](service-fabric-support.md) (Supporto di Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="f09cf-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="f09cf-140">Consentire l'esecuzione di script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f09cf-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="f09cf-141">Service Fabric usa script di Windows PowerShell per creare un cluster di sviluppo locale e per distribuire le applicazioni da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f09cf-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="f09cf-142">Per impostazione predefinita, Windows blocca l'esecuzione di questi script.</span><span class="sxs-lookup"><span data-stu-id="f09cf-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="f09cf-143">tooenable usarle, è necessario modificare i criteri di esecuzione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f09cf-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="f09cf-144">Aprire PowerShell come amministratore e immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f09cf-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="f09cf-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f09cf-145">Next steps</span></span>
<span data-ttu-id="f09cf-146">Dopo avere configurato l'ambiente di sviluppo, iniziare a compilare ed eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="f09cf-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="f09cf-147">Creare la prima applicazione Infrastruttura di servizi in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f09cf-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="f09cf-148">Informazioni su come toodeploy e gestire le applicazioni nel cluster locale</span><span class="sxs-lookup"><span data-stu-id="f09cf-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="f09cf-149">Informazioni sui modelli di programmazione hello: servizi affidabili e Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f09cf-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="f09cf-150">Vedere gli esempi di codice su GitHub hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f09cf-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="f09cf-151">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="f09cf-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="f09cf-152">Seguire hello tooget percorso di apprendimento una piattaforma toohello introduzione esaustiva di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f09cf-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="f09cf-153">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="f09cf-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Pagina della campagna di Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Collegamento WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Collegamento WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Collegamento WebPI Core SDK"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
