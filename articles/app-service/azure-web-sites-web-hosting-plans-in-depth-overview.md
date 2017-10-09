---
title: panoramica dettagliata dei piani aaaAzure servizio App | Documenti Microsoft
description: Informazioni sui piani di servizio app per Azure App Service e sui vantaggi offerti all'esperienza di gestione.
keywords: servizio app, servizio app di azure, scala, scalabile, piano di servizio app, costo del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Panoramica approfondita dei piani di servizio app di Azure

Piani di servizio App rappresentano raccolta hello di risorse fisiche utilizzate toohost app.

I piani di servizio app definiscono:

- Area (Stati Uniti occidentali, Stati Uniti orientali e così via)
- Numero di scala (una, due, tre istanze e così via)
- Dimensione dell'istanza (Small, Medium, Large)
- SKU (Gratuito, Condiviso, Basic, Standard, Premium)

Nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) le app Web, le app per dispositivi mobili, le app per le API e le app per le funzioni (o Funzioni) vengono tutte eseguite in un piano di servizio app.  App in hello stessa sottoscrizione e area possono condividere un piano di servizio App. 

Tutte le applicazioni assegnate tooan **piano di servizio App** condividere risorse hello da essa definite. in modo da consentire un risparmio sui costi quando si ospitano più app in un unico piano di servizio app.

Il **piano di servizio App** possibile scalare da **libero** e **Shared** SKU troppo**base**, **Standard**, e **Premium** SKU è accedere alle risorse di toomore e funzionalità lungo hello modo.

Se il piano di servizio App è stato impostato troppo**base** SKU o versione successiva, quindi è possibile controllare hello **dimensioni** e scala conteggio di hello macchine virtuali.

Ad esempio, se il piano è configurato toouse due istanze di "small" nel livello di servizio standard hello, eseguite tutte le applicazioni che sono associate a tale piano in entrambe le istanze. Le app prevedono inoltre le funzionalità di livello di accesso toohello servizio standard. Le istanze del piano in cui vengono eseguite le app sono completamente gestite e a disponibilità elevata.

> [!IMPORTANT]
> Hello **SKU** e **scala** di servizio App hello piano determina hello costo e hello non il numero di App ospitate in essa contenuti.

Questo articolo esamina caratteristiche principali di hello, ad esempio livello e scala, di un piano di servizio App e come essi entrano in gioco durante la gestione delle applicazioni.

## <a name="apps-and-app-service-plans"></a>App e piani di servizio app

Un'app in un servizio app può essere associata a un solo piano per volta.

App e piani sono inclusi in un **gruppo di risorse**. Un gruppo di risorse funge da limite di hello del ciclo di vita per ogni risorsa che si trova all'interno di esso. È possibile utilizzare risorse gruppi toomanage tutte le parti di hello di un'applicazione contemporaneamente.

Poiché un singolo gruppo di risorse può avere più piani di servizio App, è possibile allocare risorse fisiche toodifferent diverse app.

Si possono ad esempio separare le risorse tra ambienti di sviluppo, test e produzione. L'uso di ambienti separati per la produzione e lo sviluppo e test consente di isolare le risorse. In questo modo, test di carico rispetto a una nuova versione di App non si contendono hello stesso risorse come le applicazioni di produzione, che servono i clienti reali.

Quando in un unico gruppo di risorse sono inclusi più piani, è anche possibile definire un'applicazione che copre più aree geografiche.

Ad esempio, un'app a disponibilità elevata in esecuzione in due aree include almeno due piani, uno per ogni area, e un'app associata a ogni piano. In questo caso, tutte le copie dell'app hello hello quindi sono contenute in un singolo gruppo di risorse. Un gruppo di risorse con più piani e più App semplifica toomanage semplice, controllo e l'integrità di hello di visualizzazione di un'applicazione hello.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Creare un piano di servizio app o usare quello esistente

Quando si crea un'app, è consigliabile creare anche un gruppo di risorse. In hello altra parte, se questa applicazione è un componente per l'applicazione di grandi dimensioni, creare nel gruppo di risorse hello allocata per l'applicazione di dimensioni maggiori.

Se l'applicazione hello è un'applicazione completamente nuova o una parte di uno più grande, è possibile scegliere toouse un toohost piano esistente, o crearne uno nuovo. La decisione dipende principalmente dalla capacità e dal carico previsto.

Si consiglia di isolare l'app in un nuovo piano di servizio app nei casi seguenti:

- L'app usa molte risorse.
- App include diversi fattori di scala da hello altre App ospitate in un piano esistente.
- L'app necessita di risorse in un'area geografica diversa.

In questo modo è possibile allocare un nuovo set di risorse per l'app e ottenere un maggiore controllo delle app.

## <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

> [!TIP]
> Se si dispone di un ambiente del servizio App, è possibile esaminare hello documentazione specifici tooApp gli ambienti del servizio qui: [creare un piano di servizio App in un ambiente del servizio App](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

È possibile creare un piano di servizio App vuoto da hello esperienza di esplorazione piano di servizio App o come parte della creazione di app.

In hello [portale di Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili**, quindi selezionare **App Web** o di altro tipo di applicazione di servizio App.

![Creare un'app nel portale di Azure hello.][createWebApp]

È quindi possibile selezionare o creare il piano di servizio App per la nuova app hello hello.

 ![Creare un piano di servizio app.][createASP]

toocreate un piano di servizio App, fare clic su **[+] crea nuovi**, hello tipo **piano di servizio App** nome e quindi selezionare un'opzione appropriata **percorso**. Fare clic su **tariffario**, quindi selezionare un piano tariffario appropriato per il servizio di hello. Selezionare **visualizzare tutti** tooview più prezzi opzioni, ad esempio **libero** e **Shared**. Dopo aver selezionato hello a livello di prezzo, fare clic su hello **selezionare** pulsante.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Spostare un piano di servizio App diverso app tooa

È possibile spostare un piano di servizio App diverso app tooa hello [portale di Azure](https://portal.azure.com). È possibile spostare le applicazioni tra i piani, purché si applica ai piani hello in hello stesso gruppo di risorse e area geografica.

toomove un piano di tooanother app:

- Passare toohello app che si desidera toomove.
- In hello **Menu**, cercare hello **piano di servizio App** sezione.
- Selezionare **piano di servizio App modifica** processo hello toostart.

**Piano di servizio App modifica** apre hello **piano di servizio App** selettore. A questo punto, è possibile scegliere un toomove piano esistente in app.

> [!IMPORTANT]
> il piano di servizio App seleziona Hello dell'interfaccia utente verrà filtrato per hello seguenti criteri:
> - Esiste all'interno di hello stesso gruppo di risorse
> - Esiste in hello stessa area geografica
> - Esiste all'interno di hello stesso spazio Web
>
> Uno spazio Web è un costrutto logico all'interno del servizio app che definisce un raggruppamento di risorse del server. Un'area geografica (ad esempio Stati Uniti occidentali) contiene spazi Web molti clienti tooallocate ordine tramite il servizio App. Attualmente, le risorse del servizio App non sono in grado di toobe spostata tra gli spazi Web.
>

![Pannello di selezione Piano di servizio app.][change]

È previsto un piano tariffario diverso per ogni piano. Ad esempio, lo spostamento di un sito da un livello Standard di tooa livello gratuito, Abilita tutte le app assegnato tooit toouse hello funzionalità e risorse di livello Standard hello.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Clonare un piano di servizio App diverso app tooa

Se si desidera toomove hello app tooa altra area geografica, un'alternativa consiste app la clonazione. Con la clonazione si crea una copia dell'app in un piano di servizio app nuovo o esistente di qualsiasi area.

È possibile trovare **Clone App** in hello **gli strumenti di sviluppo** sezione del menu hello.

> [!IMPORTANT]
> La clonazione presenta alcune limitazioni, illustrate nell'articolo [Clonazione di app del servizio app di Azure con il portale di Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Scalare un piano di servizio app

Esistono tre modi tooscale un piano:

- **Livello di prezzo del piano di modifica hello**. Un piano di livello Basic hello può essere convertito tooStandard e tutte le app assegnato tooit toouse funzionalità hello del livello Standard hello.
- **Modifica delle dimensioni dell'istanza del piano di hello**. Ad esempio, un piano di livello Basic hello che utilizza le istanze di piccole dimensioni può essere modificato toouse istanze di grandi dimensioni. Tutte le app che sono associate a tale piano ora è possono utilizzare memoria aggiuntiva hello e risorse della CPU di hello offerte di dimensioni maggiori istanza.
- **Modificare il numero di istanze del piano di hello**. Ad esempio, un piano Standard che viene ridimensionato toothree istanze può essere scalato too10 istanze. È possibile aggiungere un piano Premium istanze too20 (tooavailability soggetto). Tutte le app che sono associate a tale piano ora è possono utilizzare memoria aggiuntiva hello e risorse della CPU di hello maggiore offerte di numero di istanza.

È possibile modificare i prezzi di livello e istanza dimensioni facendo hello hello **scalabilità verticale** elemento nelle impostazioni per l'applicazione hello o hello piano di servizio App. Le modifiche si applicano toohello piano di servizio App e influiscono su tutte le app che vi risiedono.

 ![Impostare i valori tooscale di un'app.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Pulizia del piano di servizio app

> [!IMPORTANT]
> **Piani di servizio app** che non dispongono di alcun toothem App associata continuerà a essere addebitato poiché continuano capacità di calcolo tooreserve hello.

tooavoid impreviste spese quando viene eliminato l'app di ultima hello ospitato in un piano di servizio App, hello vuoto risulta viene eliminato anche il piano di servizio App.

## <a name="summary"></a>Riepilogo

I piani di servizio app rappresentano un set di funzionalità e capacità che è possibile condividere tra le app. I piani di servizio App offrono si hello set tooa di flessibilità tooallocate App specifiche di risorse e ottimizza l'utilizzo di risorse di Azure. In questo modo, se si desidera toosave nell'ambiente di testing, è possibile condividere un piano tra più app. È anche possibile ottimizzare la velocità effettiva nell'ambiente di produzione scalandolo in più aree e piani.

## <a name="whats-changed"></a>Modifiche apportate

- Per una modifica di toohello della Guida da tooApp di siti Web del servizio, vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
