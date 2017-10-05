---
title: Configurare un Host Docker con VirtualBox | Documentazione Microsoft
description: Istruzioni passo a passo per configurare un'istanza di Docker predefinita usando Docker Machine e VirtualBox
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="7235c-103">Configurare un Host Docker con VirtualBox</span><span class="sxs-lookup"><span data-stu-id="7235c-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="7235c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7235c-104">Overview</span></span>
<span data-ttu-id="7235c-105">Questo articolo consente di configurare un'istanza di Docker predefinita usando Docker Machine e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="7235c-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="7235c-106">Se si utilizza il [Docker per Windows beta](http://beta.docker.com/), questa configurazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="7235c-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7235c-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7235c-107">Prerequisites</span></span>
<span data-ttu-id="7235c-108">È necessario installare gli strumenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="7235c-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="7235c-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="7235c-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="7235c-110">Configurare il client Docker con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7235c-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="7235c-111">Per configurare un client Docker, è sufficiente aprire Windows PowerShell ed eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7235c-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="7235c-112">Creare un'istanza di host docker predefinita.</span><span class="sxs-lookup"><span data-stu-id="7235c-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="7235c-113">Verificare che l'istanza predefinita sia configurata e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7235c-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="7235c-114">Verrà visualizzata un'istanza denominata \`default' in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7235c-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. <span data-ttu-id="7235c-116">Impostare l'host corrente come predefinito e configurare la shell.</span><span class="sxs-lookup"><span data-stu-id="7235c-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="7235c-117">Visualizzare i contenitori del Docker attivi.</span><span class="sxs-lookup"><span data-stu-id="7235c-117">Display the active Docker containers.</span></span> <span data-ttu-id="7235c-118">L'elenco deve essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="7235c-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> <span data-ttu-id="7235c-120">Ogni volta che si riavvia il computer di sviluppo, sarà necessario riavviare l'host Docker locale.</span><span class="sxs-lookup"><span data-stu-id="7235c-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="7235c-121">A questo scopo, al prompt dei comandi eseguire questo comando: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="7235c-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
