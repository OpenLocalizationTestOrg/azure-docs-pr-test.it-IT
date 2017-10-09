---
title: aaaDeploying applicazioni tooAzure servizio App
description: "Informazioni su modalità di funzionamento tooDeploy tooApp di applicazioni del servizio"
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="2c9cf-104">Panoramica della distribuzione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="2c9cf-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="2c9cf-105">Servizio App di Azure offre un ampio integrata set di funzionalità e toosupport la creazione di flussi di lavoro di distribuzione potente e flessibile.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="2c9cf-106">La distribuzione di app può sfruttare alcune opzioni, ad esempio l'integrazione continua o la pubblicazione locale del controllo del codice sorgente, WebDeploy e FTP.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="2c9cf-107">Hello consigliata del metodo per la distribuzione di app di produzione è scambio di slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="2c9cf-108">Gli slot di distribuzione rappresentano gli ambienti di staging e integrazione associati alle app di produzione.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="2c9cf-109">Gli slot di distribuzione possono essere configurati e di destinazione con il traffico web per la convalida e il traffico può essere scambiato su richiesta per la distribuzione tooproduction con alcun periodo di inattività e automatizzata riscaldamento.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="2c9cf-110">passaggi di Hello di un flusso di lavoro di distribuzione possono essere facilmente automatizzati tramite prodotti di release management, ad esempio Visual Studio Release Management.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="2c9cf-111">Questo approccio è utile per il coordinamento con altre risorse della soluzione, ad esempio l'archivio dati, la ricorrenza e la replica tra più unità di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2c9cf-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

