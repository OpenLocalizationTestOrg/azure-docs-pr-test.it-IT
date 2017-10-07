---
title: aaaUse Case - cliente di profilatura
description: Informazioni su come Data Factory di Azure viene utilizzato toocreate basati sui dati del flusso di lavoro (pipeline) tooprofile giochi clienti.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Caso di utilizzo - Profilo clienti
Data Factory di Azure è uno dei molti servizi utilizzati tooimplement hello Cortana Intelligence Suite di acceleratori.  Per ulteriori informazioni su Cortana Intelligence, vedere [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). In questo documento viene descritto un toohelp case semplice utilizzo di iniziare a utilizzare la comprensione di come Data Factory di Azure può risolvere i problemi comuni analitica.

## <a name="scenario"></a>Scenario
Contoso è una società di giochi online che crea giochi per più piattaforme: console di gioco, dispositivi palmari e personal computer (PC). Come i lettori riprodurre questi giochi, viene prodotta volume elevato di dati di log che tiene traccia hello modelli di utilizzo, stile di gioco e le preferenze dell'utente hello.  In combinazione con dati demografici, internazionali, e dati del prodotto può eseguire tooguide analitica loro sull'esperienza tooenhance giocatori e usarli come destinazione per gli aggiornamenti e di gioco Contoso acquisti. 

Obiettivo di Contoso è tooidentify up-vendere/cross-selling in base alla cronologia di gioco hello del relativo lettori e aggiungere di crescita aziendale toodrive funzionalità interessanti e fornire una migliore toocustomers esperienza. In questo caso, usiamo una società di giochi come esempio di società. società Hello vuole toooptimize relativo giochi basati sul comportamento dei lettori. Questi principi applicano business tooany che desidera tooengage intorno propri prodotti e servizi clienti e migliorano l'esperienza dei clienti.

In questa soluzione, poiché Contoso desidera efficacia hello tooevaluate di una campagna di marketing che recente è avviato. È iniziare con i log di hello giochi non elaborati, processo e li arricchire i dati di georilevazione join ai dati di riferimento di annuncio e infine copiare i file in impatto della campagna un Database SQL di Azure tooanalyze hello.

## <a name="deploy-solution"></a>Distribuire la soluzione
Tutto è necessario tooaccess e provare questo caso di utilizzo semplice un [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/), un [account di archiviazione Blob di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)e un [Database SQL di Azure](../sql-database/sql-database-get-started.md). Distribuire cliente hello profilatura pipeline dall'hello **pipeline di esempio** riquadro hello home page della data factory.

1. Creare una data factory o aprire una data factory esistente. Vedere [copiare i dati da archiviazione Blob tooSQL Database tramite Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per passaggi toocreate una data factory.
2. In hello **DATA FACTORY** pannello per data factory di hello, fare clic su hello **pipeline di esempio** riquadro.

    ![Riquadro Pipeline di esempio](./media/data-factory-samples/SamplePipelinesTile.png)
3. In hello **pipeline di esempio** pannello, fare clic su hello **profilo clienti** che si desidera toodeploy.

    ![Pannello Pipeline di esempio](./media/data-factory-samples/SampleTile.png)
4. Specificare le impostazioni di configurazione per l'esempio hello. ad esempio il nome e la chiave dell'account di archiviazione di Azure, il nome del server di Azure SQL, il database, l'ID utente e la password.

    ![Pannello Esempio](./media/data-factory-samples/SampleBlade.png)
5. Dopo avere completato con impostazioni di configurazione hello, fare clic su **crea** toocreate/distribuire hello pipeline di esempio e servizi/tabelle collegate utilizzate dalle pipeline hello.
6. Viene visualizzato lo stato di hello di distribuzione nel riquadro di esempio hello selezionato in precedenza hello **pipeline di esempio** blade.

    ![Stato della distribuzione](./media/data-factory-samples/DeploymentStatus.png)
7. Quando viene visualizzato hello **distribuzione ha avuto esito positivo** messaggio nel riquadro hello per esempio hello, chiude hello **pipeline di esempio** blade.  
8. In **DATA FACTORY** pannello vedere che i servizi collegati, set di dati e pipeline vengono aggiunti tooyour data factory di.  

    ![Pannello Data factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Panoramica della soluzione
In questo caso di utilizzo semplice utilizzabile come esempio di come è possibile utilizzare tooingest Data Factory di Azure, preparare, trasformare, analizzare e pubblicare i dati.

![Flusso di lavoro end-to-end](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Questa figura viene illustrato come pipeline di dati hello vengono visualizzati in hello portale di Azure dopo la distribuzione.

1. Hello **PartitionGameLogsPipeline** legge gli eventi di gioco raw hello dall'archiviazione blob e crea partizioni basate su anno, mese e giorno.
2. Hello **EnrichGameLogsPipeline** unisce gli eventi di giochi partizionati con dati di riferimento codice di area geografica e arricchisce dati hello eseguendo il mapping IP indirizzi toohello corrispondente posizioni geografiche.
3. Hello **AnalyzeMarketingCampaignPipeline** pipeline utilizza i dati sono stato arricchito hello e lo elabora con hello pubblicità toocreate hello finale output dei dati che contiene dell'efficacia della campagna di marketing.

In questo esempio, Data Factory è tooorchestrate usate attività che copia i dati di input, trasformazione e hello elaborare i dati e di output hello dati finali tooan Database SQL di Azure.  È anche possibile visualizzare rete hello della pipeline di dati, gestirli e monitorarne lo stato da hello dell'interfaccia utente.

## <a name="benefits"></a>Vantaggi
Ottimizzazione loro analitica del profilo utente e allinearla agli obiettivi aziendali, società giochi è tooquickly in grado di raccogliere utilizzo modelli e analizzare l'efficacia di hello relativo campagne di marketing.

