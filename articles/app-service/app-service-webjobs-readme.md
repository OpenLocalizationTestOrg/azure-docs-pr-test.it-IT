---
title: aaaWebJobs in Azure App Service
description: Informazioni su come toobuild background toorun processi Web verifica, interagire con i servizi come archiviazione e Bus di servizio e creare operazioni pianificate.
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="56c70-103">Uso di Processi Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="56c70-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="56c70-104">In questo articolo collega toodocumentation risorse sul toouse processi Web di Azure e hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="56c70-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="56c70-105">Processi Web di Azure forniscono gli script toorun un modo semplice o programmi come processi in background in [App del servizio Web App](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="56c70-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="56c70-106">È infatti possibile caricare ed eseguire un file eseguibile in formato cmd, bat, exe (.NET), ps1, sh, php, py, js e jar,</span><span class="sxs-lookup"><span data-stu-id="56c70-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="56c70-107">che verrà eseguito come processo Web in base a una pianificazione (cron) o senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="56c70-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="56c70-108">Hello WebJobs SDK rende più facile toouse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="56c70-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="56c70-109">Hello WebJobs SDK è un sistema di trigger che funziona con il BLOB di archiviazione di Microsoft Azure, code e tabelle, nonché le code del Bus di servizio e l'associazione.</span><span class="sxs-lookup"><span data-stu-id="56c70-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="56c70-110">Grazie agli strumenti integrati in Visual Studio, è inoltre semplice creare, distribuire e gestire processi Web.</span><span class="sxs-lookup"><span data-stu-id="56c70-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="56c70-111">È possibile creare processi Web da modelli, nonché pubblicarli e gestirli (eseguirli/arrestarli/monitorarli/eseguirne il debug).</span><span class="sxs-lookup"><span data-stu-id="56c70-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="56c70-112">dashboard di processi Web Hello in hello portale di Azure offre funzionalità di gestione potenti che consentono il controllo completo sull'esecuzione di hello di processi Web, tra cui hello possibilità tooinvoke singole funzioni all'interno di processi Web.</span><span class="sxs-lookup"><span data-stu-id="56c70-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="56c70-113">dashboard Hello Visualizza anche l'output di registrazione e di runtime di funzione.</span><span class="sxs-lookup"><span data-stu-id="56c70-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

