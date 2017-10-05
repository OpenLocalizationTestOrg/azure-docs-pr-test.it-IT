---
title: Processi Web nel servizio app di Azure
description: "Informazioni su come creare processi Web per eseguire test in background, interagire con servizi quali archiviazione e bus di servizio e creare attività pianificate."
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
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="268cc-103">Uso di Processi Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="268cc-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="268cc-104">Questo articolo include i collegamenti a risorse della documentazione relative all'uso di Processi Web di Azure e di Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="268cc-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="268cc-105">Processi Web di Azure costituisce una soluzione semplice e rapida per eseguire script e programmi sotto forma di processi in background in [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="268cc-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="268cc-106">È infatti possibile caricare ed eseguire un file eseguibile in formato cmd, bat, exe (.NET), ps1, sh, php, py, js e jar,</span><span class="sxs-lookup"><span data-stu-id="268cc-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="268cc-107">che verrà eseguito come processo Web in base a una pianificazione (cron) o senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="268cc-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="268cc-108">WebJobs SDK semplifica l'uso dell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="268cc-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="268cc-109">Include infatti un sistema di binding e attivazione che interagisce con BLOB, code e tabelle di archiviazione di Microsoft Azure, oltre che con le code del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="268cc-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="268cc-110">Grazie agli strumenti integrati in Visual Studio, è inoltre semplice creare, distribuire e gestire processi Web.</span><span class="sxs-lookup"><span data-stu-id="268cc-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="268cc-111">È possibile creare processi Web da modelli, nonché pubblicarli e gestirli (eseguirli/arrestarli/monitorarli/eseguirne il debug).</span><span class="sxs-lookup"><span data-stu-id="268cc-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="268cc-112">Il dashboard Processi Web nel portale di Azure include efficaci funzionalità di gestione per controllare completamente l'esecuzione di processi Web, tra cui la possibilità di richiamare singole funzioni nei processi Web.</span><span class="sxs-lookup"><span data-stu-id="268cc-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="268cc-113">Il dashboard visualizza inoltre i runtime delle funzioni e l'output delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="268cc-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

