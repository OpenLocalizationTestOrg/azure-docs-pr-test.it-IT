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
# <a name="azure-app-service-deployment-overview"></a>Panoramica della distribuzione nel servizio app di Azure
Servizio App di Azure offre un ampio integrata set di funzionalità e toosupport la creazione di flussi di lavoro di distribuzione potente e flessibile. La distribuzione di app può sfruttare alcune opzioni, ad esempio l'integrazione continua o la pubblicazione locale del controllo del codice sorgente, WebDeploy e FTP. Hello consigliata del metodo per la distribuzione di app di produzione è scambio di slot di distribuzione. Gli slot di distribuzione rappresentano gli ambienti di staging e integrazione associati alle app di produzione. Gli slot di distribuzione possono essere configurati e di destinazione con il traffico web per la convalida e il traffico può essere scambiato su richiesta per la distribuzione tooproduction con alcun periodo di inattività e automatizzata riscaldamento. passaggi di Hello di un flusso di lavoro di distribuzione possono essere facilmente automatizzati tramite prodotti di release management, ad esempio Visual Studio Release Management. Questo approccio è utile per il coordinamento con altre risorse della soluzione, ad esempio l'archivio dati, la ricorrenza e la replica tra più unità di distribuzione. 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

