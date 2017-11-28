---
title: aaaAzure esempi di PowerShell - servizio App | Documenti Microsoft
description: Esempi di Azure PowerShell - Servizio App
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b7b4a030364f797195522c56fbae5b7f530d4d1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="0a5e8-103">Esempi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a5e8-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="0a5e8-104">Hello nella tabella seguente include gli script toobash collegamenti compilati utilizzando hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-104">hello following table includes links toobash scripts built using hello Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="0a5e8-105">**Creare un'app**</span><span class="sxs-lookup"><span data-stu-id="0a5e8-105">**Create app**</span></span>||
| [<span data-ttu-id="0a5e8-106">Creare un'App Web con la distribuzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="0a5e8-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-107">Crea un'App Web di Azure che effettua il pull del codice da GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="0a5e8-108">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="0a5e8-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-109">Crea un'App Web di Azure che distribuisce in modo continuo codice da GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="0a5e8-110">Creare un'app Web e distribuire il codice da FTP</span><span class="sxs-lookup"><span data-stu-id="0a5e8-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-111">Crea un'app Web di Azure per caricare i file da una directory locale tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="0a5e8-112">Creare un'App Web e distribuire il codice da un archivio Git locale</span><span class="sxs-lookup"><span data-stu-id="0a5e8-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-113">Crea un'App Web di Azure e configura il push del codice da un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="0a5e8-114">Creare un'app web e distribuire codice tooa ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="0a5e8-114">Create a web app and deploy code tooa staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-115">Crea un'App Web di Azure con uno slot di distribuzione per le modifiche al codice di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="0a5e8-116">**Configurare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="0a5e8-116">**Configure app**</span></span>||
| [<span data-ttu-id="0a5e8-117">Eseguire il mapping di un'app web tooa di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="0a5e8-117">Map a custom domain tooa web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-118">Crea un'app web di Azure e associa un tooit nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-118">Creates an Azure web app and maps a custom domain name tooit.</span></span> |
| [<span data-ttu-id="0a5e8-119">Associare un'app web tooa di certificati SSL personalizzata</span><span class="sxs-lookup"><span data-stu-id="0a5e8-119">Bind a custom SSL certificate tooa web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-120">Crea un'app web di Azure e associa il certificato SSL hello di un tooit nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-120">Creates an Azure web app and binds hello SSL certificate of a custom domain name tooit.</span></span> |
|<span data-ttu-id="0a5e8-121">**Ridimensionare un'app**</span><span class="sxs-lookup"><span data-stu-id="0a5e8-121">**Scale app**</span></span>||
| [<span data-ttu-id="0a5e8-122">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="0a5e8-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-123">Crea un'App Web di Azure e la ridimensiona su 2 istanze.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="0a5e8-124">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="0a5e8-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-125">Crea due App Web di Azure in due aree geografiche diverse e le rende disponibili tramite un solo endpoint usando Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="0a5e8-126">**Connettersi tooresources app**</span><span class="sxs-lookup"><span data-stu-id="0a5e8-126">**Connect app tooresources**</span></span>||
| [<span data-ttu-id="0a5e8-127">Connettersi a un tooa app web SQL Database</span><span class="sxs-lookup"><span data-stu-id="0a5e8-127">Connect a web app tooa SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-128">Crea un'app web di Azure e un database SQL, quindi aggiunge hello stringa toohello app le impostazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-128">Creates an Azure web app and a SQL database, then adds hello database connection string toohello app settings.</span></span> |
| [<span data-ttu-id="0a5e8-129">Connettersi a un account di archiviazione tooa app web</span><span class="sxs-lookup"><span data-stu-id="0a5e8-129">Connect a web app tooa storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="0a5e8-130">Crea un'applicazione web di Azure e un account di archiviazione, quindi aggiunge hello archiviazione connessione toohello app le impostazioni della stringa.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-130">Creates an Azure web app and a storage account, then adds hello storage connection string toohello app settings.</span></span> |
|<span data-ttu-id="0a5e8-131">**Monitorare un'app**</span><span class="sxs-lookup"><span data-stu-id="0a5e8-131">**Monitor app**</span></span>||
| [<span data-ttu-id="0a5e8-132">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="0a5e8-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="0a5e8-133">Crea un'app web di Azure e consente la registrazione per il computer locale di hello registri tooyour Scarica.</span><span class="sxs-lookup"><span data-stu-id="0a5e8-133">Creates an Azure web app, enables logging for it, and downloads hello logs tooyour local machine.</span></span> |
| | |
