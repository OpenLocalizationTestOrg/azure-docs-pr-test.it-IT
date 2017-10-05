---
title: Abilitazione di Acquisizione di Hub eventi di Azure tramite il portale | Microsoft Docs
description: "Abilitare la funzionalità Acquisizione di Hub eventi usando il portale di Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>Abilitare Acquisizione di Hub eventi usando il portale di Azure

È possibile configurare Acquisizione al momento della creazione dell'hub eventi usando il [portale di Azure](https://portal.azure.com). È possibile acquisire i dati in un contenitore di [archiviazione BLOB](https://azure.microsoft.com/services/storage/blobs/) di Azure o in un account [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

## <a name="capture-data-to-an-azure-storage-account"></a>Acquisire i dati in un account di archiviazione di Azure  

Quando si crea un hub eventi, è possibile abilitare l'acquisizione facendo il **su** pulsante il **creare Hub eventi** portale pannello. È quindi possibile specificare un account e un contenitore di archiviazione facendo clic su **Archiviazione di Azure** nella casella **Provider di acquisizione**. Poiché Acquisizione di Hub eventi usa l'autenticazione da servizio a servizio con la risorsa di archiviazione, non è necessario specificare una stringa di connessione di archiviazione. Il selettore risorse seleziona automaticamente l'URI della risorsa per l'account di archiviazione. Se si usa Azure Resource Manager, è necessario specificare questo URI in modo esplicito come stringa.

L'intervallo di tempo predefinito è di 5 minuti. Il valore minimo è 1, quello massimo 15. La finestra **Dimensione** ha un intervallo compreso tra 10 e 500 MB.

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>Acquisire i dati un account Azure Data Lake Store

Per acquisire i dati in Azure Data Lake Store, si creano un account Data Lake Store e un hub eventi.

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Creare un account Azure Data Lake Store e le cartelle

1. Creare un account Data Lake Store seguendo le istruzioni riportate in [Introduzione ad Azure Data Lake Store con il portale di Azure](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Creare una cartella in tale account seguendo le istruzioni riportate nella sezione relativa alla [creazione di cartelle nell'account Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).
3. Nel pannello account archivio Data Lake, fare clic su **Esplora dati**.
4. Fare clic su **Accesso**.
5. Fare clic su **Aggiungi**.
6. Nella casella **Cerca in base al nome o all'indirizzo di posta elettronica** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione. 
7. Verrà visualizzata la scheda **Autorizzazioni**. Impostare le autorizzazioni come illustrato nella figura seguente:

    ![][6]

8. Fare clic su **OK**.
9. Creare quindi una cartella nella cartella radice passando alla cartella di destinazione e facendo clic sul nome della cartella.
10. Fare clic su **Accesso**.
11. Fare clic su **Aggiungi**.
12. Nella casella **Cerca in base al nome o all'indirizzo di posta elettronica** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.
13. Verrà visualizzata di nuovo la scheda **Autorizzazioni**. Impostare le autorizzazioni come illustrato nella figura seguente:

    ![][5]

### <a name="create-an-event-hub"></a>Creare un hub eventi

1. Si noti che l'hub eventi deve trovarsi nella stessa sottoscrizione di Azure dell'account Azure Data Lake Store appena creato. Creazione dell'hub di eventi, fare clic sul **su** pulsante sotto **acquisire** nel **creare Hub eventi** portale pannello. 
2. Nel **creare Hub eventi** portale pannello seleziona **archivio Azure Data Lake** dal **acquisire Provider** casella.
3. In **Seleziona Data Lake Store** specificare l'account Data Lake Store creato in precedenza e nel campo **Percorso Data Lake** immettere il percorso della cartella dati creata.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Aggiungere o configurare l'acquisizione in un hub eventi esistente

È possibile configurare l'acquisizione in hub eventi esistenti che si trovano in spazi dei nomi di Hub eventi. Per abilitare Acquisizione in un hub eventi esistente o per modificarne le impostazioni, fare clic sullo spazio dei nomi per caricare il pannello **Informazioni di base**, quindi fare clic sull'hub eventi per cui si vuole abilitare o modificare l'impostazione di Acquisizione. Infine, fare clic su di **proprietà** sezione del pannello aperto e quindi modificare le impostazioni di acquisizione, come illustrato nella figura riportata di seguito:

### <a name="azure-blob-storage"></a>Archiviazione BLOB di Azure

![][2]

### <a name="azure-data-lake-store"></a>Archivio Azure Data Lake

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Passaggi successivi

È anche possibile configurare Acquisizione di Hub eventi usando i modelli di Azure Resource Manager. Per altre informazioni, vedere [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md) (Abilitare Acquisizione usando un modello di Azure Resource Manager).
