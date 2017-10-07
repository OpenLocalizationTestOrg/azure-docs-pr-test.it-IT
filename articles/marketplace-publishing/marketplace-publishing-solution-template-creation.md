---
title: aaaGuide toocreating un modello di soluzione hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un modello di soluzione Multi-VM immagine per l'acquisto in hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Guida toocreate un modello di soluzione di Azure Marketplace
Dopo aver completato il passaggio 1, [creazione di Account e la registrazione][link-acct-creation], è interattiva è al momento della creazione hello di un modello di soluzione Azure compatibile in [tecnici prerequisiti per la creazione di un modello di soluzione](marketplace-publishing-solution-template-creation-prerequisites.md). Ora è verranno illustrati i passaggi di hello per la creazione di un modello di soluzione per più macchine virtuali di hello [portale pubblicazione] [ link-pubportal] per hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Creare l'offerta di modello di soluzione in hello portale di pubblicazione
Andare troppo [https://publish.windowsazure.com](http://publish.windowsazure.com). Durante l'accesso per hello prima ora toohello [portale pubblicazione](https://publish.windowsazure.com/), utilizzare hello stesso account con cui è stato registrato profilo venditore della società. Successivamente, è possibile aggiungere qualsiasi dipendente della società come co-amministratore in hello portale di pubblicazione.

### <a name="1-select-solution-templates"></a>1. Selezionare "Modelli di soluzione"
  ![disegno][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Creare un nuovo modello di soluzione
  ![disegno][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Iniziare con le topologie
Un modello di soluzione è un tooall "padre" relativo topologie. È possibile definire più topologie in un singolo modello di soluzione/offerta. Quando un'offerta viene inserita toostaging, esso viene inserito con le relative topologie. Seguire i passaggi di hello seguito toodefine l'offerta:     

* Creare una topologia: "Identificatore topologia" è in genere nome hello della topologia hello per il modello di soluzione hello. Identificatore di topologia Hello viene utilizzato nell'URL di hello, come illustrato di seguito:

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}

  Portale di Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}
* Aggiungere una nuova versione

### <a name="4-get-your-topology-versions-certified"></a>4. Ottenere la certificazione per le versioni della topologia
Caricare un file zip che contiene tutti i file necessari tooprovision quella versione specifica della topologia hello. Il file zip deve contenere i seguenti hello:

* File *mainTemplate.json* e *createUiDefinition.json* nella directory radice.
* Tutti i modelli collegati e tutti gli script necessari.

  > [!TIP]
  > Mentre gli sviluppatori di lavoro per la creazione di soluzioni hello topologie di modello e ottenendoli certificate, business hello, marketing e/o legali reparti della società possono sul contenuto di marketing e legali hello.
  >
  >

## <a name="next-steps"></a>Passaggi successivi
Ora che si crea il modello di soluzione e caricamento del file zip hello, seguire le istruzioni hello hello [Guida contenuto marketing Marketplace](marketplace-publishing-push-to-staging.md) prima push toostaging offerta hello. set completo di hello toosee di marketplace la pubblicazione di articoli, visitare [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md).

Articoli correlati:

* Immagini di macchina virtuale: [Informazioni sulle immagini di macchine virtuali in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Estensioni di macchina virtuale: [Panoramica sull'agente VM e sulle estensioni VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) e [Estensioni VM e funzionalità di Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Semplici modelli di esempio](https://github.com/rjmax/ArmExamples)
* Account di archiviazione limita: [come tooMonitor per la limitazione di Account di archiviazione](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) e [archiviazione Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
