---
title: Esempi di Azure PowerShell - Servizio app | Microsoft Docs
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
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="2a915-103">Esempi di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a915-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="2a915-104">La tabella seguente include i collegamenti agli script Bash compilati tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a915-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="2a915-105">**Creare un'app**</span><span class="sxs-lookup"><span data-stu-id="2a915-105">**Create app**</span></span>||
| [<span data-ttu-id="2a915-106">Creare un'App Web con la distribuzione da GitHub</span><span class="sxs-lookup"><span data-stu-id="2a915-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-107">Crea un'App Web di Azure che effettua il pull del codice da GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a915-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="2a915-108">Creare un'App Web con distribuzione continua da GitHub</span><span class="sxs-lookup"><span data-stu-id="2a915-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-109">Crea un'App Web di Azure che distribuisce in modo continuo codice da GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a915-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="2a915-110">Creare un'app Web e distribuire il codice da FTP</span><span class="sxs-lookup"><span data-stu-id="2a915-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-111">Crea un'app Web di Azure per caricare i file da una directory locale tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="2a915-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="2a915-112">Creare un'App Web e distribuire il codice da un archivio Git locale</span><span class="sxs-lookup"><span data-stu-id="2a915-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-113">Crea un'App Web di Azure e configura il push del codice da un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="2a915-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="2a915-114">Creare un'App Web e distribuire il codice in un ambiente di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="2a915-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-115">Crea un'App Web di Azure con uno slot di distribuzione per le modifiche al codice di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="2a915-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="2a915-116">**Configurare l'applicazione**</span><span class="sxs-lookup"><span data-stu-id="2a915-116">**Configure app**</span></span>||
| [<span data-ttu-id="2a915-117">Eseguire il mapping di un dominio personalizzato a un'App Web</span><span class="sxs-lookup"><span data-stu-id="2a915-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-118">Crea un'App Web di Azure e ne esegue il mapping a un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2a915-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="2a915-119">Associare un certificato SSL personalizzato a un'app Web</span><span class="sxs-lookup"><span data-stu-id="2a915-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-120">Crea un'app Web di Azure e associa ad essa il certificato SSL di un nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="2a915-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="2a915-121">**Ridimensionare un'app**</span><span class="sxs-lookup"><span data-stu-id="2a915-121">**Scale app**</span></span>||
| [<span data-ttu-id="2a915-122">Ridimensionare un'App Web manualmente</span><span class="sxs-lookup"><span data-stu-id="2a915-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-123">Crea un'App Web di Azure e la ridimensiona su 2 istanze.</span><span class="sxs-lookup"><span data-stu-id="2a915-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="2a915-124">Ridimensionare un'App Web a livello globale con un'architettura a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="2a915-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-125">Crea due App Web di Azure in due aree geografiche diverse e le rende disponibili tramite un solo endpoint usando Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a915-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="2a915-126">**Collegare l'app alle risorse**</span><span class="sxs-lookup"><span data-stu-id="2a915-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="2a915-127">Collegare un'App Web a un database SQL</span><span class="sxs-lookup"><span data-stu-id="2a915-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-128">Crea un'App Web di Azure e un database SQL, quindi aggiunge la stringa di connessione del database alle impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="2a915-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="2a915-129">Connettere un'App Web a un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2a915-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="2a915-130">Crea un'App Web e un account di archiviazione di Azure, quindi aggiunge la stringa di connessione della risorsa di archiviazione alle impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="2a915-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="2a915-131">**Monitorare un'app**</span><span class="sxs-lookup"><span data-stu-id="2a915-131">**Monitor app**</span></span>||
| [<span data-ttu-id="2a915-132">Monitorare un'App Web con i log del server Web</span><span class="sxs-lookup"><span data-stu-id="2a915-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="2a915-133">Crea un'App Web di Azure, consente la creazione di log per essa e scarica i log nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="2a915-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
