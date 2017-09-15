---
title: Installare l'interfaccia della riga di comando del controller di dominio/sistema operativo | Documentazione Microsoft
description: Installare l'interfaccia della riga di comando del controller di dominio/sistema operativo.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="97430-104">Questa procedura è necessaria per l'uso di cluster ACS basati su controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="97430-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="97430-105">Non è necessario eseguirla per i cluster ACS basati su Swarm.</span><span class="sxs-lookup"><span data-stu-id="97430-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="97430-106">È prima di tutto necessario [connettersi ai cluster ACS basati su controller di dominio/sistema operativo](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="97430-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="97430-107">Dopo la connessione, è possibile installare l'interfaccia della riga di comando del controller di dominio/sistema operativo nel computer client con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="97430-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="97430-108">Se si usa una versione precedente di Python, è possibile che vengano visualizzati avvisi di tipo "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="97430-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="97430-109">È possibile ignorare questi avvisi.</span><span class="sxs-lookup"><span data-stu-id="97430-109">You can safely ignore these.</span></span>

<span data-ttu-id="97430-110">Per iniziare senza riavviare la shell, eseguire:</span><span class="sxs-lookup"><span data-stu-id="97430-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="97430-111">Questo passaggio non sarà necessario quando si avviano nuove shell.</span><span class="sxs-lookup"><span data-stu-id="97430-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="97430-112">È ora possibile verificare che l'interfaccia della riga di comando sia stata installata:</span><span class="sxs-lookup"><span data-stu-id="97430-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```