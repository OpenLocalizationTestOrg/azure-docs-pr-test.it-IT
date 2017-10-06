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
# <a name="using-webjobs-in-azure-app-service"></a>Uso di Processi Web nel servizio app di Azure
In questo articolo collega toodocumentation risorse sul toouse processi Web di Azure e hello Azure WebJobs SDK. Processi Web di Azure forniscono gli script toorun un modo semplice o programmi come processi in background in [App del servizio Web App](http://go.microsoft.com/fwlink/?LinkId=529714). È infatti possibile caricare ed eseguire un file eseguibile in formato cmd, bat, exe (.NET), ps1, sh, php, py, js e jar, che verrà eseguito come processo Web in base a una pianificazione (cron) o senza interruzioni.

Hello WebJobs SDK rende più facile toouse di archiviazione di Azure. Hello WebJobs SDK è un sistema di trigger che funziona con il BLOB di archiviazione di Microsoft Azure, code e tabelle, nonché le code del Bus di servizio e l'associazione.

Grazie agli strumenti integrati in Visual Studio, è inoltre semplice creare, distribuire e gestire processi Web. È possibile creare processi Web da modelli, nonché pubblicarli e gestirli (eseguirli/arrestarli/monitorarli/eseguirne il debug).

dashboard di processi Web Hello in hello portale di Azure offre funzionalità di gestione potenti che consentono il controllo completo sull'esecuzione di hello di processi Web, tra cui hello possibilità tooinvoke singole funzioni all'interno di processi Web. dashboard Hello Visualizza anche l'output di registrazione e di runtime di funzione.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

