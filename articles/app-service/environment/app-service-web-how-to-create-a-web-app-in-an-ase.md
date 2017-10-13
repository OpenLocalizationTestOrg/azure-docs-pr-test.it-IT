---
title: Creare un'app Web in un ambiente del servizio app (versione 1)
description: Informazioni su come creare app Web e piani di servizio app in un ambiente del servizio app (versione 1)
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
ms.openlocfilehash: b031807073313e9e093dbc7576ecfd3d2a970abe
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Creare un'app Web in un ambiente del servizio app (versione 1)

> [!NOTE]
> Questo articolo fa riferimento all'ambiente del servizio app (versione 1),  Esiste una nuova versione dell'ambiente del servizio app che, oltre ad essere più facile da usare, può essere eseguita in un'infrastruttura più potente. Per altre informazioni su questa nuova versione, vedere [Introduzione ad Ambiente del servizio app](intro.md).
> 

## <a name="overview"></a>Panoramica
Questa esercitazione illustra come creare app Web e piani di servizio app in un [ambiente del servizio app (versione 1)](app-service-app-service-environment-intro.md). 

> [!NOTE]
> Se si vuole imparare a creare un'app Web ma non è necessario farlo in un ambiente del servizio app, vedere [Creare un'app Web .NET](../app-service-web-get-started-dotnet.md) o una delle esercitazioni correlate per altri linguaggi e framework.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione presuppone che l'utente abbia creato un ambiente del servizio app. Se questa operazione non è ancora stata eseguita, vedere [Creare un ambiente del servizio app](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Creare un'app Web
1. Nel [portale di Azure](https://portal.azure.com/) fare clic su **Nuovo > Web e dispositivi mobili > App Web**. 
   
    ![][1]
2. Selezionare la propria sottoscrizione.  
   
    Se sono presenti più sottoscrizioni, ricordare che per creare un'app nell'ambiente del servizio app è necessario usare la stessa sottoscrizione usata per la creazione dell'ambiente. 
3. Selezionare o creare un gruppo di risorse.
   
    I *gruppi di risorse* consentono di gestire risorse di Azure correlate come un'unità e sono utili per stabilire le regole di *controllo degli accessi in base al ruolo*  per le app. Per altre informazioni, vedere [Panoramica di Azure Resource Manager][ResourceGroups]. 
4. Selezionare o creare un piano di servizio app.
   
    *piani di servizio app* sono costituiti da set gestiti di app Web.  Quando si seleziona il prezzo, in genere l'importo addebitato viene applicato al piano di servizio app invece che alle singole app. Nell'ambiente del servizio app vengono addebitate le istanze di calcolo allocate all'ambiente e non quanto elencato nel piano di servizio app.  Per aumentare il numero di istanze di un'app Web, si aumentano le istanze del piano di servizio app e tale operazione influisce su tutte le app Web incluse nel piano.  Il piano può prevedere restrizioni relative alla quantità per alcune funzionalità, come gli slot di sito o l'integrazione della rete virtuale.  Per altre informazioni, vedere [Panoramica approfondita dei piani del servizio app di Azure](../azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    È possibile identificare i piani di servizio app nell'ambiente del servizio app osservando la località indicata sotto il nome del piano.  
   
    ![][5]
   
    Per usare un piano di servizio app che esiste già nell'ambiente del servizio app, selezionarlo. Per creare un nuovo piano di servizio app, vedere la sezione successiva di questa esercitazione [Creare un piano di servizio app in un ambiente del servizio app](#createplan).
5. Immettere il nome dell'app Web e fare clic su **Crea**. 
   
    Se l'ambiente del servizio app usa un indirizzo VIP esterno, l'URL dell'app nell'ambiente del servizio app è: [*nomesito*].[*nome dell'ambiente del servizio app*].p.azurewebsites.net e non [*nomesito*].azurewebsites.net
   
    Se l'ambiente del servizio app usa un indirizzo VIP interno, l'URL di un'app in tale ambiente del servizio app è: [*nomesito*].[*sottodominio specificato durante la creazione dell'ambiente del servizio app*]   
    Dopo la selezione di ASP durante la creazione dell'ambiente del servizio app, l'aggiornamento del sottodominio verrà visualizzato in **Nome**

## <a name="createplan"></a> Creare un piano di servizio app
Quando si crea un piano di servizio app in un ambiente del servizio app, le scelte relative al ruolo di lavoro sono diverse perché in un ambiente del servizio app non esistono ruoli di lavoro condivisi.  I ruoli di lavoro utilizzabili sono quelli allocati all'ambiente del servizio app dall'amministratore.  Questo significa che per creare un nuovo piano, è necessario allocare al pool di lavoro dell'ambiente del servizio app un numero di ruoli di lavoro maggiore del numero totale di istanze in tutti i piani già presenti in quel pool di lavoro.  Se nell'ambiente del servizio app non sono presenti pool di lavoro sufficienti per creare il piano, è necessario chiedere all'amministratore dell'ambiente di aggiungerli.

Un'altra differenza dei piani di servizio app ospitati in un ambiente del servizio app è data dall'impossibilità di scegliere il prezzo.  Con un ambiente del servizio app si paga infatti per le risorse di calcolo usate dal sistema e non viene addebito nulla per i piani di servizio app presenti in tale ambiente.  In genere, quando si crea un piano di servizio app è necessario selezionare un piano tariffario che determina la fatturazione.  Un ambiente del servizio app è essenzialmente una posizione privata in cui è possibile creare contenuti.  Si paga per l'ambiente e non per ospitare il contenuto.

Le istruzioni seguenti mostrano come creare un piano di servizio app mentre si crea un'app Web come illustrato nella sezione precedente dell'esercitazione.

1. Nell'interfaccia utente di selezione del piano fare clic su **Crea nuovo** e specificare un nome come si farebbe per un piano creato all'esterno di un ambiente del servizio app.
2. Selezionare l'ambiente del servizio app che si vuole usare nell'elenco di selezione della località.
   
    Poiché un ambiente del servizio app è essenzialmente una località di distribuzione privata, è visualizzato in Località. 
   
    ![][2]
   
    Dopo aver selezionato un ambiente nell'elenco di selezione della località, l'interfaccia utente di creazione del piano di servizio app viene aggiornata.  Nella località è ora visualizzato il nome del sistema dell'ambiente del servizio app e l'area in cui si trova e l'elenco di selezione del piano tariffario è stato sostituito dalla selezione del pool di lavoro.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Selezione di un pool di lavoro
Quando si seleziona un piano tariffario dedicato, nel servizio app di Azure e all'esterno di un ambiente del servizio app sono in genere disponibili tre dimensioni di calcolo.  Analogamente, per un ambiente del servizio app è possibile definire fino a tre pool di ruoli di lavoro e specificare le dimensioni di calcolo da usare per i pool di lavoro.  Per i tenant dell'ambiente del servizio app significa che invece di selezionare un piano tariffario con dimensioni di calcolo per il piano di servizio app, si seleziona ciò che viene definito un *pool di lavoro*.  

Nell'interfaccia utente di selezione del pool di lavoro sotto il nome del pool sono indicate le dimensioni di calcolo usate per il pool.  La quantità disponibile si riferisce al numero di istanze di calcolo disponibili per l'uso nel pool.  In totale nel pool possono esistere più istanze rispetto a tale numero, ma questo valore si riferisce semplicemente al numero di quelle non in uso.  Se è necessario adeguare l'ambiente del servizio app e aggiungere altre risorse di calcolo, vedere [Configurazione dell'ambiente del servizio app](app-service-web-configure-an-app-service-environment.md).

![][4]

In questo esempio sono disponibili solo due pool di lavoro, in quanto l'amministratore dell'ambiente del servizio app ha allocato host solo in questi due pool di lavoro.  Allocando macchine virtuali a un terzo pool, i pool di lavoro visualizzati saranno tre.  

## <a name="after-web-app-creation"></a>Dopo la creazione dell'app Web
Per eseguire app Web e gestire piani di servizio app in un ambiente del servizio app, è opportuno tenere in considerazione alcuni aspetti.  

Come indicato in precedenza, il proprietario dell'ambiente del servizio app è responsabile delle dimensioni del sistema, di conseguenza spetta al proprietario garantire una capacità sufficiente per ospitare i piani di servizio app desiderati. Se non sono disponibili ruoli di lavoro, non sarà possibile creare il piano di servizio app.  Questa considerazione si applica anche all'aumento delle risorse per l'app Web.  Se sono necessarie altre istanze, è necessario chiedere all'amministratore dell'ambiente del servizio app di aggiungere altri processi di lavoro.

Dopo aver creato l'app Web e il piano di servizio app, è consigliabile aumentare le istanze.  Per garantire la tolleranza di errore per le app, in un ambiente del servizio app devono essere sempre presenti almeno due istanze del piano di servizio app.  La procedura per ridimensionare un piano di servizio app in un ambiente del servizio app è quella presentata dall'interfaccia utente del piano di servizio app.  Per altre informazioni sul ridimensionamento, vedere [Come ridimensionare un'app Web in un ambiente del servizio app](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: app-service-app-service-environment-intro.md
[Appserviceplans]: ../azure-web-sites-web-hosting-plans-in-depth-overview.md
[HowtoCreateASE]: app-service-web-how-to-create-an-app-service-environment.md
[HowtoScale]: app-service-web-scale-a-web-app-in-an-app-service-environment.md
[HowtoConfigureASE]: app-service-web-configure-an-app-service-environment.md
[ResourceGroups]: ../../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
