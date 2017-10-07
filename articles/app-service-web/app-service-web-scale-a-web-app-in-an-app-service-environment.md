---
title: aaaHow tooScale un'App in un ambiente del servizio App
description: Ridimensionamento di un'app in un ambiente del servizio app
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Ridimensionamento di app in un ambiente del servizio app
In hello servizio App di Azure sono disponibili è possibile scalare in genere tre operazioni:

* piano tariffario
* dimensioni dei processi di lavoro 
* numero di istanze.

In un ASE non è presente alcun hello tooselect o modifica necessità dei prezzi di piano.  In termini di funzionalità il livello è già quello del piano tariffario Premium.  

Con le dimensioni di tooworker riguardo ASE salve possibile assegnare dimensioni hello di hello toobe di risorse di calcolo utilizzato per ogni pool di lavoro.  Questo significa che, se necessario, è possibile avere il pool di lavoro 1 con risorse di calcolo P4 e il pool di lavoro 2 con risorse di calcolo P1,  Siano privi di toobe in ordine di dimensioni.  Per informazioni dettagliate su dimensioni hello e il piano tariffario vedere qui il documento hello [dei prezzi di Azure App Service][AppServicePricing].  In questo modo hello sicure per le applicazioni web e i piani di servizio App in un ambiente del servizio App di toobe:

* selezione del pool di lavoro
* numero di istanze

La modifica degli elementi viene eseguita tramite hello appropriati dell'interfaccia utente visualizzato per il ASE ospitati piani di servizio App.  

![][1]

È possibile scalare in verticale ASP oltre il numero di hello disponibili delle risorse di calcolo nel pool di lavoro hello che la pagina ASP.  Se è necessario calcolare le risorse del pool di lavoro è necessario tooget il tooadd amministratore ASE li.  Per ulteriori informazioni intorno riconfigurazione del ASE informazioni hello qui: [come un ambiente del servizio App tooConfigure][HowtoConfigureASE].  È inoltre possibile tootake sfruttare hello capacità tooadd funzionalità scalabilità automatica di ASE basata su pianificazione o metriche.  ulteriori informazioni sulla configurazione di scalabilità automatica per l'ambiente hello ASE stesso, vedere tooget [come tooconfigure scalabilità automatica per un ambiente del servizio App][ASEAutoscale].

È possibile creare app più piani di servizio utilizzando le risorse di calcolo dal pool di lavoro diversi, oppure è possibile utilizzare hello stesso pool di lavoro.  Per esempio, se si dispone di risorse di calcolo disponibili (10) in lavoro Pool 1, è possibile scegliere toocreate piano di servizio di un'app con risorse di calcolo (6) e pianificare di un secondo servizio app che Usa risorse di calcolo (4).

### <a name="scaling-hello-number-of-instances"></a>Numero di hello di istanze di ridimensionamento
Quando si crea per la prima volta l'app Web in un ambiente del servizio app, il servizio viene avviato con una istanza.  È possibile quindi scalabilità tooadditional istanze tooprovide ulteriori risorse per l'app di calcolo.   

Se la capacità dell'ambiente del servizio app è sufficiente, questa operazione è abbastanza semplice.  Si passa tooyour piano di servizio App che contiene siti hello desiderato tooscale backup e selezionare la scala.  Si aprirà hello dell'interfaccia utente in cui è possibile manualmente impostare scala hello per la pagina ASP o configurare le regole di scalabilità automatica per la pagina ASP.  scala toomanually l'app è sufficiente imposta ***scalare*** troppo***un numero di istanze immesso manualmente***.  Da qui trascinare quantity toohello desiderato di dispositivo di scorrimento hello o immetterlo nel dispositivo di scorrimento hello casella Avanti toohello.  

![][2] 

regole di scalabilità automatica Hello per una pagina ASP in un lavoro ASE hello stesso come avviene normalmente.  È possibile selezionare ***Percentuale CPU*** in ***Ridimensiona di*** e creare regole di scalabilità automatica per il piano ASP in base alla percentuale di CPU oppure è possibile creare regole più complesse usando l'impostazione ***regole per la pianificazione e le prestazioni***.  toosee completare più dettagli sulla configurazione di scalabilità automatica utilizzare hello Guida [ridimensionare un'app in Azure App Service][AppScale]. 

### <a name="worker-pool-selection"></a>selezione del pool di lavoro
Come notato in precedenza, selezione del pool di lavoro hello è accessibile dalla hello dell'interfaccia utente di ASP.  Aprire il pannello hello per hello ASP tooscale desiderati e selezionare il pool di lavoro.  Verranno visualizzati tutti i pool di lavoro hello che è stato configurato l'ambiente del servizio App.  Se si dispone di un solo worker pool si verrà visualizzato solo un pool di hello elencato.  toochange quali lavoro pool di applicazioni ASP in, è sufficiente selezionare il pool di lavoro hello si desidera il toomove piano di servizio App per.  

![][3]

Prima di spostare la pagina ASP da un lavoratore pool tooanother è importante toomake che si avrà una capacità sufficiente per la pagina ASP.  Nell'elenco di hello del pool di lavoro, non solo è il nome del pool di lavoro hello elencato ma è inoltre possibile visualizzare il numero di thread di lavoro sono disponibili in tale pool di lavoro.  Assicurarsi che non esistono sufficienti toocontain disponibili le istanze del piano di servizio App.  Se è necessario calcolare più risorse nel pool di lavoro hello desiderato toomove per, quindi ottenere il tooadd amministratore ASE li.  

> [!NOTE]
> Lo spostamento di che una pagina ASP dal pool di uno lavoro causerà freddo avvia App hello in tale ASP.  Questo può causare richieste toorun lenta quando l'app è freddo avviato su nuove risorse di calcolo hello.  Hello avvio a freddo può essere evitata utilizzando hello [warm la funzionalità di applicazione] [ AppWarmup] nel servizio App di Azure.  modulo di inizializzazione dell'applicazione Hello descritto nell'articolo hello funziona anche per l'avvio a freddo, poiché il processo di inizializzazione hello viene richiamato anche quando le app sono fredde avviato su nuove risorse di calcolo. 
> 
> 

## <a name="getting-started"></a>introduttiva
tooget avviato con gli ambienti del servizio App, vedere [come tooCreate un ambiente del servizio App][HowtoCreateASE]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
