---
title: Distribuzione di applicazioni nel servizio app di Azure
description: Informazioni su come distribuire le applicazioni per l'uso nel servizio app
keywords: servizio app, servizio app di azure, distribuire, distribuzione
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="3c967-104">Panoramica della distribuzione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="3c967-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="3c967-105">Il servizio app di Azure offre una funzionalità integrata e avanzata concepita per supportare la creazione di flussi di lavoro di distribuzione flessibili e potenti.</span><span class="sxs-lookup"><span data-stu-id="3c967-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="3c967-106">La distribuzione di app può sfruttare alcune opzioni, ad esempio l'integrazione continua o la pubblicazione locale del controllo del codice sorgente, WebDeploy e FTP.</span><span class="sxs-lookup"><span data-stu-id="3c967-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="3c967-107">Il metodo consigliato per la distribuzione di app di produzione è lo scambio degli slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3c967-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="3c967-108">Gli slot di distribuzione rappresentano gli ambienti di staging e integrazione associati alle app di produzione.</span><span class="sxs-lookup"><span data-stu-id="3c967-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="3c967-109">Gli slot di distribuzione possono essere configurati e impostati per ricevere traffico Web per la convalida. Il traffico può essere scambiato su richiesta per la distribuzione nell'ambiente di produzione senza tempi di inattività e con avvio automatico.</span><span class="sxs-lookup"><span data-stu-id="3c967-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="3c967-110">I passaggi di un flusso di lavoro di distribuzione possono essere facilmente automatizzati con prodotti di gestione del rilascio, ad esempio Release Management per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c967-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="3c967-111">Questo approccio è utile per il coordinamento con altre risorse della soluzione, ad esempio l'archivio dati, la ricorrenza e la replica tra più unità di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3c967-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

