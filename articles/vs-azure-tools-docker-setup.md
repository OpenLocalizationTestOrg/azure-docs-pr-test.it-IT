---
title: un Host Docker con VirtualBox aaaConfigure | Documenti Microsoft
description: Istruzioni dettagliate tooconfigure Docker predefinito dell'istanza tramite Docker macchina e VirtualBox
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
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="fcd1f-103">Configurare un Host Docker con VirtualBox</span><span class="sxs-lookup"><span data-stu-id="fcd1f-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="fcd1f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fcd1f-104">Overview</span></span>
<span data-ttu-id="fcd1f-105">Questo articolo consente di configurare un'istanza di Docker predefinita usando Docker Machine e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="fcd1f-106">Se si usa hello [Docker per Windows beta](http://beta.docker.com/), questa configurazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcd1f-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fcd1f-107">Prerequisites</span></span>
<span data-ttu-id="fcd1f-108">Hello seguenti strumenti necessario toobe installato.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="fcd1f-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="fcd1f-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="fcd1f-110">Configurazione del client di Docker hello con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcd1f-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="fcd1f-111">un client di Docker, tooconfigure semplicemente aprire Windows PowerShell ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="fcd1f-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="fcd1f-112">Creare un'istanza di host docker predefinita.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="fcd1f-113">Verificare l'istanza predefinita di hello è configurato e in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="fcd1f-114">Verrà visualizzata un'istanza denominata \`default' in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. <span data-ttu-id="fcd1f-116">Impostare il valore predefinito come host corrente hello e configurare la shell.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="fcd1f-117">Visualizzare i contenitori di Docker active hello.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-117">Display hello active Docker containers.</span></span> <span data-ttu-id="fcd1f-118">elenco di Hello deve essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> <span data-ttu-id="fcd1f-120">Ogni volta che si riavvia il computer di sviluppo, è necessario toorestart all'host docker locale.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="fcd1f-121">toodo hello, questo problema comando al prompt di comando seguente: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="fcd1f-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
