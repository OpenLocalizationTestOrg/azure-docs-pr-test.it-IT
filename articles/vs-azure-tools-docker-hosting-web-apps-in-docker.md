---
title: aaaDeploy host Docker remoto un ASP.NET Core Linux Docker contenitore tooa | Documenti Microsoft
description: Informazioni su come toouse Visual Studio Tools per Docker toodeploy un Core di ASP.NET web contenitori di Docker tooa app in esecuzione in una macchina virtuale Linux di Azure Docker Host
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="cbe84-103">Distribuire un host di Docker remoto ASP.NET contenitore tooa</span><span class="sxs-lookup"><span data-stu-id="cbe84-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="cbe84-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cbe84-104">Overview</span></span>
<span data-ttu-id="cbe84-105">Docker è un motore di contenitore leggero, simile per alcuni macchina virtuale tooa modi, che è possibile utilizzare toohost applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="cbe84-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="cbe84-106">In questa esercitazione illustra utilizzando hello [Visual Studio Tools per Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy estensione un host di ASP.NET Core app tooa Docker in Azure tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbe84-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbe84-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cbe84-107">Prerequisites</span></span>
<span data-ttu-id="cbe84-108">esempio Hello è toocomplete necessari in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="cbe84-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="cbe84-109">Creare una macchina virtuale Host Docker di Azure, come descritto in [come toouse docker-computer con Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="cbe84-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="cbe84-110">Installare una versione più recente di hello di [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="cbe84-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="cbe84-111">Scaricare hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="cbe84-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="cbe84-112">Installare [Docker per Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="cbe84-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="cbe84-113">1. Creare un'app Web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cbe84-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="cbe84-114">Hello passaggi seguenti illustrano come creare un'applicazione ASP.NET Core di base che verrà utilizzata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cbe84-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="cbe84-115">2. Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="cbe84-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="cbe84-116">3. Utilizzare uno Script di PowerShell DockerTask.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="cbe84-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="cbe84-117">Aprire una directory radice toohello prompt dei comandi di PowerShell del progetto.</span><span class="sxs-lookup"><span data-stu-id="cbe84-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="cbe84-118">Convalidare host remoto hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cbe84-118">Validate hello remote host is running.</span></span> <span data-ttu-id="cbe84-119">Dovrebbe essere visualizzato lo stato = Running</span><span class="sxs-lookup"><span data-stu-id="cbe84-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="cbe84-120">Compilazione hello app usando hello - parametro di compilazione</span><span class="sxs-lookup"><span data-stu-id="cbe84-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="cbe84-121">Eseguire app hello, utilizzando hello - parametro di esecuzione</span><span class="sxs-lookup"><span data-stu-id="cbe84-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="cbe84-122">Al termine del processo di docker, verrà visualizzato risultati simili toohello segue:</span><span class="sxs-lookup"><span data-stu-id="cbe84-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Visualizzare l'app][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
