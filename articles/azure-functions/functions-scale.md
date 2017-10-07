---
title: i piani di utilizzo di funzioni e il servizio App aaaAzure | Documenti Microsoft
description: "Comprendere le funzioni di Azure la scalabilità di esigenze di hello toomeet i carichi di lavoro basato su eventi."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Piani a consumo e piani di servizio app di Funzioni di Azure 

## <a name="introduction"></a>Introduzione

È possibile eseguire Funzioni di Azure in due modalità diverse, ovvero con piano a consumo e piano di servizio app di Azure. piano di consumo Hello alloca automaticamente potenza di calcolo quando il codice è in esecuzione, consente una scalabilità orizzontale come carico toohandle necessarie e quindi il ridimensionamento quando codice non è in esecuzione. In tal caso, si dispone di toopay per le macchine virtuali inattive e non tooreserve capacità in anticipo. In questo articolo è incentrato sul piano il consumo di hello. Per informazioni dettagliate sul funzionamento di hello piano di servizio App, vedere hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Se non si ha familiarità con le funzioni di Azure, vedere hello [panoramica delle funzioni di Azure](functions-overview.md).

Quando si crea un'app di funzione, è necessario configurare un piano di hosting per le funzioni hello app contiene. In entrambe le modalità, un'istanza di hello *host di Azure funzioni* esegue le funzioni hello. tipo di Hello dei controlli di piano:

* Il modo in cui vengono aumentate le istanze dell'host.
* Hello risorse host disponibili tooeach.

Attualmente, è necessario scegliere il tipo di piano hello durante la creazione di app di funzione hello hello. Non è possibile modificare il piano in un secondo momento. 

È possibile applicare la scalabilità tra livelli su hello piano di servizio App. Piano di consumo hello, funzioni di Azure gestisce automaticamente tutta l'allocazione di risorse.

## <a name="consumption-plan"></a>Piano a consumo

Quando si utilizza un piano di utilizzo, le istanze dell'host di Azure funzioni hello in modo dinamico vengono aggiunti e rimossi in base al numero di hello di eventi in entrata. Questo piano offre la scalabilità automatica e sono previsti costi per le risorse di calcolo solo quando le funzioni sono in esecuzione. In un piano a consumo, una funzione può essere eseguita al massimo per 10 minuti. 

> [!NOTE]
> il timeout predefinito Hello per le funzioni in un piano di utilizzo è 5 minuti. valore di Hello può essere maggiore too10 minuti per App di funzione hello modificando proprietà hello `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

La fatturazione è basata sul tempo di esecuzione e sulla memoria usata ed è aggregata per tutte le funzioni in un'app per le funzioni. Per ulteriori informazioni, vedere hello [funzioni Azure pagina dei prezzi].

piano il consumo di Hello è hello predefinita e offre hello seguenti vantaggi:
- Addebiti solo quando le funzioni sono in esecuzione.
- Aumento automatico del numero di istanze anche in periodo di carico elevato.

## <a name="app-service-plan"></a>Piano di servizio app

Sul dedicato macchine virtuali in Basic, Standard e Premium SKU, tooWeb simile app nel servizio App hello piano, le app di funzione. Macchine virtuali dedicate sono allocati tooyour App del servizio App, ovvero host funzioni hello è sempre in esecuzione.

Si consideri un piano di servizio App di hello seguenti casi:
- Sono presenti macchine virtuali sottoutilizzate, che eseguono già altre istanze del servizio app.
- Si prevede che il toorun app di funzione in modo continuato o quasi continua.
- È necessario più opzioni di utilizzo della CPU o memoria rispetto a quello fornito nel piano di consumo hello.
- È necessario più di hello tempo di esecuzione massimo consentito per il piano di consumo hello toorun.

Una macchina virtuale separa il costo per tempo di esecuzione e dimensioni della memoria. Di conseguenza, non si evitano così costi più di costo hello dell'istanza della macchina virtuale che alloca hello. Per informazioni dettagliate sul funzionamento di hello piano di servizio App, vedere hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Con un piano di servizio app, è possibile aumentare manualmente il numero di istanze aggiungendo altre istanze di macchine virtuali oppure abilitare la scalabilità automatica. Per altre informazioni, vedere [Scalare il conteggio delle istanze manualmente o automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Per aumentare le prestazioni è anche possibile scegliere un piano di servizio App diverso. Per altre informazioni, vedere [Aumentare le prestazioni di un'app in Azure](../app-service-web/web-sites-scale.md). Se si intende toorun funzioni JavaScript in un piano di servizio App, è consigliabile scegliere un piano con un minor numero di core. Per ulteriori informazioni, vedere hello [riferimento JavaScript per le funzioni](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### AlwaysOn

Se si esegue in un piano di servizio App, è necessario abilitare hello **Always On** impostazione in modo che l'app di funzione viene eseguita correttamente. Un piano di servizio App, il runtime di funzioni hello diventerà inattivo dopo pochi minuti di inattività, in modo solo i trigger HTTP saranno "riattivazione" delle funzioni. Ciò è simile toohow che processi Web deve è sempre abilitato. 

L'opzione Sempre online è disponibile solo nel piano di servizio app. Un piano di utilizzo, piattaforma hello attiva automaticamente le app di funzione.

## <a name="storage-account-requirements"></a>Requisiti dell'account di archiviazione

In un piano a consumo o un piano di servizio app è necessario che un'app per le funzioni abbia un account di archiviazione di Azure che supporta l'archivio BLOB, code e tabelle. Funzioni di Azure usa internamente Archiviazione di Azure per operazioni come la gestione dei trigger e la registrazione dell'esecuzione delle funzioni. Alcuni account di archiviazione non supportano code e tabelle, ad esempio gli account di archiviazione solo BLOB (tra cui Archiviazione Premium) e gli account di archiviazione di uso generico con replica archiviazione con ridondanza della zona. Questi account vengono filtrati da hello **Account di archiviazione** pannello quando si crea un'app di funzione.

toolearn ulteriori informazioni sui tipi di account di archiviazione, vedere [Introduzione a servizi di archiviazione Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Funzionamento del piano di consumo hello

piano il consumo di Hello viene ridimensionato automaticamente alle risorse di CPU e memoria aggiungendo ulteriori istanze di host funzioni hello, in base al numero di hello di eventi che vengono attivate le funzioni in. Ogni istanza dell'host funzioni hello è limitato too1.5 GB di memoria.

Quando si utilizza il file di codice di funzione sono archiviato nelle condivisioni di file di Azure nell'account di archiviazione principale hello hello consumo piano di hosting. Quando si elimina l'account di archiviazione principale hello, questo contenuto viene eliminato e non può essere recuperato.

> [!NOTE]
> Quando si utilizza un trigger di blob in un piano di utilizzo, può esistere di ritardo di 10 minuti tooa durante l'elaborazione di nuovi BLOB se un'app di funzione è diventato inattiva. Dopo l'applicazione di funzione hello è in esecuzione, i BLOB vengono elaborati immediatamente. tooavoid iniziale di questo ritardo, considerare una delle seguenti opzioni hello:
> - Usare un piano di servizio app con l'opzione Always On abilitata.
> - Utilizzare un altro blob di hello tootrigger meccanismo di elaborazione, ad esempio un messaggio nella coda che contiene il nome di blob hello. Per un esempio, vedere il [Queue trigger with blob input binding](functions-bindings-storage-blob.md#input-sample) (Trigger della coda con associazione di input del BLOB).

### <a name="runtime-scaling"></a>Ridimensionamento in fase di runtime

Funzioni di Azure Usa un componente chiamato hello *controller scala* toomonitor hello frequenza degli eventi e determinare se tooscale scalare verso il basso o disattivata. controller di scala Hello utilizza regole euristiche per ogni tipo di trigger. Ad esempio, quando si utilizza un trigger di archiviazione della coda di Azure, si adatta in base alla lunghezza della coda hello ed età hello di messaggio della coda hello meno recente.

unità di scala di Hello è hello funzione app. Quando l'applicazione di funzione hello è scalare orizzontalmente, più risorse vengono allocate toorun più istanze dell'host di Azure funzioni hello. Viceversa, come calcolo richiesta è diminuita, controller scala hello rimuove le istanze dell'host (funzione). numero di istanze di Hello è alla fine progressive toozero quando nessuna funzione vengono eseguite all'interno di un'app di funzione.

![Monitoraggio degli eventi e creazione delle istanze da parte del controller di scalabilità](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modello di fatturazione

La fatturazione per il piano di consumo hello è descritte in dettaglio nella hello [funzioni Azure pagina dei prezzi]. Informazioni sull'utilizzo vengono aggregati a livello di app di funzione hello e conta solo ora hello che esegue codice della funzione. di seguito Hello sono unità per la fatturazione. 
* **Utilizzo delle risorse in gigabyte al secondo (GB-s)**. Calcolato come combinazione di dimensioni di memoria e tempo di esecuzione per tutte le funzioni in un'app per le funzioni. 
* **Esecuzioni**. Contato ogni volta che viene eseguita una funzione nell'evento tooan di risposta, generato da un'associazione.

[funzioni Azure pagina dei prezzi]: https://azure.microsoft.com/pricing/details/functions
