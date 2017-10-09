---
title: hello aaaInstall CLI di controller di dominio o del sistema operativo | Documenti Microsoft
description: Installare hello CLI di controller di dominio o del sistema operativo.
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
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="fd719-104">Questa procedura è necessaria per l'uso di cluster ACS basati su controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fd719-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="fd719-105">Non è alcuna necessità toodo questo per i cluster basato su sciame ACS.</span><span class="sxs-lookup"><span data-stu-id="fd719-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="fd719-106">Prima di tutto, [connettersi cluster basato su controller di dominio/OS ACS tooyour](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="fd719-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="fd719-107">Dopo aver eseguito questo, è possibile installare hello CLI di controller di dominio o del sistema operativo del computer client con comandi hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="fd719-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="fd719-108">Se si usa una versione precedente di Python, è possibile che vengano visualizzati avvisi di tipo "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="fd719-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="fd719-109">È possibile ignorare questi avvisi.</span><span class="sxs-lookup"><span data-stu-id="fd719-109">You can safely ignore these.</span></span>

<span data-ttu-id="fd719-110">In ordine tooget avviato senza dover riavviare la shell, eseguire:</span><span class="sxs-lookup"><span data-stu-id="fd719-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="fd719-111">Questo passaggio non sarà necessario quando si avviano nuove shell.</span><span class="sxs-lookup"><span data-stu-id="fd719-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="fd719-112">È ora possibile verificare tale hello che CLI è installato:</span><span class="sxs-lookup"><span data-stu-id="fd719-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```