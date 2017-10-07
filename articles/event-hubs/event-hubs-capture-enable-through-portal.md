---
title: abilitare aaaAzure acquisire gli hub di eventi tramite il portale | Documenti Microsoft
description: "Abilitare funzionalità hello acquisire gli hub di eventi utilizzando hello portale di Azure."
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
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Abilitare gli hub di eventi Capture utilizzando hello portale di Azure

È possibile configurare l'acquisizione al momento della creazione di hello evento hub utilizzando hello [portale di Azure](https://portal.azure.com). È possibile entrambi tooan di dati di acquisizione hello Azure [nell'archiviazione Blob](https://azure.microsoft.com/services/storage/blobs/) contenitore o tooan [archivio Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) account.

## <a name="capture-data-tooan-azure-storage-account"></a>Account di archiviazione di Azure tooan dati di acquisizione  

Quando si crea un hub eventi, è possibile abilitare l'acquisizione facendo hello **su** pulsante hello **creare Hub eventi** portale pannello. Specificare quindi un Account di archiviazione e un contenitore, fare clic su **di archiviazione di Azure** in hello **acquisire Provider** casella. Poiché gli hub di eventi acquisire utilizza l'autenticazione di service to service con l'archiviazione, non è necessario toospecify una stringa di connessione di archiviazione. selezione della risorsa Hello URI della risorsa hello dell'account di archiviazione viene selezionato automaticamente. Se si usa Azure Resource Manager, è necessario specificare questo URI in modo esplicito come stringa.

intervallo di tempo predefinito Hello è 5 minuti. valore minimo di Hello è 1, hello massimo 15. Hello **dimensioni** finestra dispone di un intervallo di 10-500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Account archivio Azure Data Lake tooan di dati di acquisizione

toocapture dati tooAzure archivio Data Lake, creare un account archivio Data Lake e un hub eventi:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Creare un account Azure Data Lake Store e le cartelle

1. Creare un account archivio Data Lake, attenendosi alle istruzioni hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Creare una cartella con questo account, attenendosi alle istruzioni hello in hello [creare cartelle nell'account archivio Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sezione.
3. Nel Pannello di account archivio Data Lake hello, fare clic su **Esplora dati**.
4. Fare clic su **Accesso**.
5. Fare clic su **Aggiungi**.
6. In hello **ricerca per nome o indirizzo email** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione. 
7. Hello **autorizzazioni** verrà visualizzata la scheda. Impostare le autorizzazioni di hello, come illustrato nella seguente illustrazione hello:

    ![][6]

8. Fare clic su **OK**.
9. A questo punto, è possibile creare una cartella nella cartella radice hello visualizzando la cartella di destinazione toohello e facendo clic sul nome della cartella hello.
10. Fare clic su **Accesso**.
11. Fare clic su **Aggiungi**.
12. In hello **ricerca per nome o indirizzo email** digitare **Microsoft.EventHubs** e quindi selezionare questa opzione.
13. Hello **autorizzazioni** verrà nuovamente visualizzata la scheda. Impostare le autorizzazioni di hello, come illustrato nella seguente illustrazione hello:

    ![][5]

### <a name="create-an-event-hub"></a>Creare un hub eventi

1. Hub eventi hello deve essere in hello stessa sottoscrizione Azure hello archivio Azure Data Lake appena creato. Hub di eventi hello create, fare clic su hello **su** pulsante sotto **acquisire** in hello **creare Hub eventi** portale pannello. 
2. In hello **creare Hub eventi** portale pannello seleziona **archivio Azure Data Lake** da hello **acquisire Provider** casella.
3. In **archivio Data Lake di selezionare**, specificare l'account archivio Data Lake è stato creato in precedenza e hello hello **Data Lake percorso** immettere hello toohello dati cartella creata.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Aggiungere o configurare l'acquisizione in un hub eventi esistente

È possibile configurare l'acquisizione in hub eventi esistenti che si trovano in spazi dei nomi di Hub eventi. tooenable acquisire in un hub eventi, o esistente toochange le impostazioni di acquisizione, fare clic su hello tooload dello spazio dei nomi di hello **Essentials** pannello, quindi fare clic su hub di eventi hello per cui si desidera tooenable o modifica l'impostazione di acquisizione hello. Infine, fare clic su hello **proprietà** sezione di hello aprire Pannello e quindi modificare le impostazioni di acquisizione hello, come mostrato nel seguente figure hello:

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
