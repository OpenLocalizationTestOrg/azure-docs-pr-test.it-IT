---
title: aaaCreate un'app web in un ambiente del servizio App di v1
description: Informazioni su come toocreate App web e i piani di servizio app in un ambiente del servizio App di v1
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Creare un'app Web in un ambiente del servizio app (versione 1)

> [!NOTE]
> Questo articolo è sull'ambiente del servizio App v1 hello.  È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Panoramica
Questa esercitazione viene illustrato come le app web toocreate e piani di servizio App in un [ambiente del servizio App v1](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> Se si desidera toolearn come toocreate un'app web ma non necessario toodo in un ambiente del servizio App, vedere [creare un'app web .NET](app-service-web-get-started-dotnet.md) o uno dei hello correlati esercitazioni per altri linguaggi e altri Framework.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione presuppone che l'utente abbia creato un ambiente del servizio app. Se questa operazione non è ancora stata eseguita, vedere [Creare un ambiente del servizio app](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Creare un'app Web
1. In hello [portale Azure](https://portal.azure.com/), fare clic su **nuovo > Web e dispositivi mobili > App Web**. 
   
    ![][1]
2. Selezionare la propria sottoscrizione.  
   
    Se si dispone di più sottoscrizioni tenere presente che toocreate un'app nell'ambiente del servizio App, è necessario toouse hello stessa sottoscrizione utilizzata durante la creazione ambiente hello. 
3. Selezionare o creare un gruppo di risorse.
   
    *Gruppi di risorse* attiva è toomanage relative risorse di Azure come unità e sono utili quando si stabilisce *controllo di accesso basato sui ruoli* regole (RBAC) per le app. Per altre informazioni, vedere [Panoramica di Azure Resource Manager][ResourceGroups]. 
4. Selezionare o creare un piano di servizio app.
   
    *piani di servizio app* sono costituiti da set gestiti di app Web.  In genere quando si seleziona prezzi, prezzo hello applicato è toohello applicato il piano di servizio App anziché toohello singole app. In un ASE si paga per il calcolo hello istanze allocati ASE toohello anziché con la pagina ASP siano elencati.  tooscale numero hello di istanze di un'app web è la scalabilità verticale istanze hello del piano di servizio App e influisce su tutte le applicazioni web hello in tale piano.  Inoltre, alcune funzionalità, ad esempio gli slot del sito o l'integrazione della rete virtuale si applicano restrizioni di quantità all'interno del piano hello.  Per altre informazioni, vedere [Panoramica approfondita dei piani del servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    È possibile identificare hello che piani di servizio App nel ASE esaminando percorso hello è indicato nel nome del piano di hello.  
   
    ![][5]
   
    Se si desidera toouse un piano di servizio App che esiste già nell'ambiente del servizio App, selezionare tale piano. Se si desidera toocreate un nuovo piano di servizio App, vedere hello successiva sezione di questa esercitazione, [creare un piano di servizio App in un ambiente del servizio App](#createplan).
5. Immettere il nome di hello per le app web e quindi fare clic su **crea**. 
   
    Se il ASE utilizza un URL di hello VIP esterno di un'app in un ASE è: [*sitename*]. [ *nome dell'ambiente del servizio App*]. p.azurewebsites.net anziché [*sitename*]. azurewebsites.net
   
    Se il ASE utilizza un URL interno VIP quindi hello di un'app in ASE: [*sitename*]. [ *sottodominio specificato durante la creazione di ASE*]   
    Dopo aver selezionato la pagina ASP durante la creazione di ASE verrà visualizzato il sottodominio hello aggiornare sotto **nome**

## <a name="createplan"></a> Creare un piano di servizio app
Quando si crea un piano di servizio app in un ambiente del servizio app, le scelte relative al ruolo di lavoro sono diverse perché in un ambiente del servizio app non esistono ruoli di lavoro condivisi.  lavoratori Hello è toouse sono quelli che sono stati allocati toohello ASE dall'amministratore. hello hello  Ciò significa che toocreate un nuovo piano, è necessario toohave ulteriori processi di lavoro allocati tooyour ASE pool di lavoro rispetto al numero totale di hello di istanze in tutti i piani già in tale pool di lavoro.  Se non è sufficiente lavoratori nel toocreate di pool di lavoro ASE il piano, è necessario toowork con il tooget admin ASE che li aggiunto.

Un'altra differenza con i piani di servizio App ospitata da un ambiente del servizio App è la mancanza di hello di prezzo di selezione.  Quando si dispone di un ambiente del servizio App pagamento per le risorse di calcolo usate dal sistema hello e non ha aggiunto i costi per i piani di hello in tale ambiente.  In genere, quando si crea un piano di servizio app è necessario selezionare un piano tariffario che determina la fatturazione.  Un ambiente del servizio app è essenzialmente una posizione privata in cui è possibile creare contenuti.  Si paga per ambiente hello e non toohost il contenuto.

Hello istruzioni seguenti viene illustrato come un servizio App toocreate piano durante la creazione di un'app web, come illustrato nella sezione precedente di hello di esercitazione hello.

1. Fare clic su **Crea nuovo** in hello piano selezione dell'interfaccia utente e specificare un nome per il piano come accade in genere all'esterno di un tipo di base.
2. Selezionare ASE hello che si desidera toouse dalla selezione del percorso.
   
    Poiché un ambiente del servizio app è essenzialmente una località di distribuzione privata, è visualizzato in Località. 
   
    ![][2]
   
    Dopo la selezione di un ASE nella selezione percorso hello, hello gli aggiornamenti dell'interfaccia utente di creazione piano di servizio App.  percorso Hello ora Mostra nome hello di hello sistema ASE e area hello in e hello prezzi selezione piano viene sostituito con un pulsante di selezione del pool di lavoro.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Selezione di un pool di lavoro
In genere in Azure App Service e all'esterno di un ambiente del servizio App, sono presenti 3 dimensioni di calcolo che sono disponibili con la selezione di un piano di prezzo dedicato hello.  In questo modo, per un ASE è possibile definire i too3 pool dei thread di lavoro e specificare le dimensioni di calcolo hello che viene utilizzata il pool di lavoro.  Ciò significa che per i tenant di hello ASE è invece di selezionare un piano tariffario con dimensioni di calcolo per il piano di servizio App, selezionare quello che viene definito un *pool di lavoro*.  

selezione del pool di lavoro Hello dell'interfaccia utente Mostra dimensioni di calcolo hello utilizzata il pool di lavoro sotto il nome hello.  Hello quantità disponibile fa riferimento toohow molte istanze sono disponibili per l'utilizzo del pool di calcolo.  pool totale Hello effettivamente può avere più istanze di questo numero, ma questo valore si riferisce toosimply quanti non siano utilizzate.  Se è necessario tooadjust tooadd l'ambiente del servizio App di calcolo più risorse, vedere [sulla configurazione dell'ambiente del servizio App](app-service-web-configure-an-app-service-environment.md).

![][4]

In questo esempio sono disponibili solo due pool di lavoro, Ciò avviene perché l'amministratore di ASE hello allocate solo gli host in tali pool di lavoro di due.  Hello terzo verrà visualizzati quando sono presenti macchine virtuali allocate al suo interno.  

## <a name="after-web-app-creation"></a>Dopo la creazione dell'app Web
Esistono alcune considerazioni per le applicazioni web in esecuzione e la gestione dei piani di servizio App in un ASE necessarie toobe presi in considerazione.  

Come notato in precedenza, il proprietario di hello di hello ASE è responsabile di dimensioni hello system hello e di conseguenza sono inoltre responsabili per verificare che sia presente hello toohost di capacità sufficiente desiderato di piani di servizio App. Se sono non presenti processi di lavoro disponibili, è necessario non essere in grado di toocreate piano di servizio App.  È anche true tooscaling backup dell'app web.  Se è necessario più istanze, sarebbe necessario tooget tooadd di amministratore l'ambiente del servizio App più worker.

Dopo aver creato l'applicazione web e un piano di servizio App è tooscale una buona idea, configurarlo.  In un ASE toohave almeno 2 istanze di tolleranza di errore del servizio App piano tooprovide è sempre necessario per le app.  Il ridimensionamento di un servizio App piano in un ASE è hello stesso come di consueto tramite hello il piano di servizio App dell'interfaccia utente.  Per ulteriori informazioni sulla scalabilità, [come tooscale un'app web in un ambiente del servizio App](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
