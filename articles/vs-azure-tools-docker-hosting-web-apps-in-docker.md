---
title: Distribuire un contenitore Docker ASP.NET Core Linux in un host Docker remoto | Documentazione Microsoft
description: Informazioni su come usare Visual Studio Tools per Docker per distribuire un'app Web ASP.NET Core in un contenitore Docker in esecuzione in una macchina virtuale Linux host Docker di Azure
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
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="a47b0-103">Distribuire un contenitore ASP.NET in un host Docker remoto</span><span class="sxs-lookup"><span data-stu-id="a47b0-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="a47b0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a47b0-104">Overview</span></span>
<span data-ttu-id="a47b0-105">Docker è un motore contenitore leggero, simile in qualche modo a una macchina virtuale, che è possibile usare per ospitare applicazioni e servizi.</span><span class="sxs-lookup"><span data-stu-id="a47b0-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="a47b0-106">Questa esercitazione illustra come usare l'estensione [Visual Studio Tools per Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) per distribuire un'app ASP.NET Core in un host Docker in Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a47b0-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a47b0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a47b0-107">Prerequisites</span></span>
<span data-ttu-id="a47b0-108">Per completare l'esercitazione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a47b0-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="a47b0-109">Creare una VM host Docker in Azure, come descritto in [Come usare Docker Machine in Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a47b0-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="a47b0-110">Installare la versione più recente di [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="a47b0-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="a47b0-111">Scaricare [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="a47b0-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="a47b0-112">Installare [Docker per Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="a47b0-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="a47b0-113">1. Creare un'app Web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a47b0-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="a47b0-114">La procedura seguente illustra la creazione di un'app ASP.NET Core di base che verrà usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a47b0-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="a47b0-115">2. Aggiungere il supporto di Docker</span><span class="sxs-lookup"><span data-stu-id="a47b0-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="a47b0-116">3. Usare lo script di PowerShell DockerTask.ps1</span><span class="sxs-lookup"><span data-stu-id="a47b0-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="a47b0-117">Aprire un prompt dei comandi di PowerShell nella directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="a47b0-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="a47b0-118">La convalida dell'host remoto è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a47b0-118">Validate the remote host is running.</span></span> <span data-ttu-id="a47b0-119">Dovrebbe essere visualizzato lo stato = Running</span><span class="sxs-lookup"><span data-stu-id="a47b0-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="a47b0-120">Compilare l'app con il parametro -Build</span><span class="sxs-lookup"><span data-stu-id="a47b0-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="a47b0-121">Eseguire l'app usando il parametro -Run</span><span class="sxs-lookup"><span data-stu-id="a47b0-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="a47b0-122">Una volta completata l'esecuzione di Docker, i risultati visualizzati dovrebbero essere simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="a47b0-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![Visualizzare l'app][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
