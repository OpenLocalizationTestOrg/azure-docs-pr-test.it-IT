---
title: dati aaaCapture dagli hub di eventi in un archivio Azure Data Lake | Documenti Microsoft
description: Dati toocapture archivio Azure Data Lake di uso di hub eventi
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Dati toocapture archivio Azure Data Lake di uso di hub eventi

Informazioni su come dati di archivio Azure Data Lake toocapture toouse ricevuto dall'hub eventi di Azure.

## <a name="prerequisites"></a>Prerequisiti

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Un account Azure Data Lake Store**. Per istruzioni su come toocreate uno, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md).

*  **Uno spazio dei nomi di Hub eventi**. Per istruzioni, vedere [Creare uno spazio dei nomi di Hub eventi](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Verificare che l'account archivio Data Lake hello e dello spazio dei nomi di hello hub eventi si trovano in hello stessa sottoscrizione di Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Assegnare autorizzazioni tooEvent hub

In questa sezione è creare una cartella all'interno di account hello in cui si desidera dati hello toocapture dagli hub eventi. È anche assegnare autorizzazioni tooEvent hub in modo da consentire la scrittura di dati in un account archivio Data Lake. 

1. Aprire l'account archivio Data Lake di hello in cui si desidera che i dati toocapture dagli hub eventi e quindi fare clic su **Esplora dati**.

    ![Esplora dati di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Esplora dati di Data Lake Store")

2.  Fare clic su **nuova cartella** e quindi immettere un nome per la cartella in cui i dati di hello toocapture.

    ![Creare una nuova cartella in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Creare una nuova cartella in Data Lake Store")

3. Assegnare autorizzazioni nella directory principale di hello di hello archivio Data Lake. 

    a. Fare clic su **Esplora dati**selezionare hello radice di hello account archivio Data Lake e quindi fare clic su **accesso**.

    ![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assegnare le autorizzazioni per la radice di Data Lake Store")

    b. In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`. 

    ![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la radice di Data Lake Store")
    
    Fare clic su **Seleziona**.

    c. In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**. Impostare **autorizzazioni** troppo**Execute**. Impostare **aggiungere** troppo**questa cartella e tutti gli elementi figlio**. Impostare **aggiungere come** troppo**una voce di autorizzazione di accesso e una voce di autorizzazione predefinito**.

    ![Assegnare le autorizzazioni per la radice di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assegnare le autorizzazioni per la radice di Data Lake Store")

    Fare clic su **OK**.

4. Assegnare le autorizzazioni per la cartella di hello account archivio Data Lake in cui si desidera toocapture dati.

    a. Fare clic su **Esplora dati**, selezionare la cartella hello hello account archivio Data Lake e quindi fare clic su **accesso**.

    ![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")

    b. In **Accesso** fare clic su **Aggiungi**, fare clic su **Selezionare l'utente o il gruppo** e quindi cercare `Microsoft.EventHubs`. 

    ![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")
    
    Fare clic su **Seleziona**.

    c. In **Assegna autorizzazioni** fare clic su **Selezionare le autorizzazioni**. Impostare **autorizzazioni** troppo**lettura, scrittura,** e **Execute**. Impostare **aggiungere** troppo**questa cartella e tutti gli elementi figlio**. Infine, impostare **aggiungere come** troppo**una voce di autorizzazione di accesso e una voce di autorizzazione predefinito**.

    ![Assegnare le autorizzazioni per la cartella di Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assegnare le autorizzazioni per la cartella di Data Lake Store")
    
    Fare clic su **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Configurare l'archivio di hub eventi toocapture dati tooData Lake

In questa sezione si crea un hub eventi in uno spazio dei nomi di Hub eventi. È inoltre possibile configurare hello Hub eventi toocapture dati tooan account archivio Azure Data Lake. Questa sezione presuppone che sia già stato creato uno spazio dei nomi di Hub eventi.

2. Da hello **Panoramica** riquadro dello spazio dei nomi di hub eventi hello, fare clic su **+ Hub eventi**.

    ![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Creare un hub eventi")

3. Fornire seguente hello valori tooconfigure hub eventi toocapture tooData Lake archivio.

    ![Creare un hub eventi](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Creare un hub eventi")

    a. Specificare un nome per hello Hub eventi.
    
    b. Per questa esercitazione, impostare **il numero di partizioni** e **memorizzazione dei messaggi** toohello predefinite.
    
    c. Impostare **acquisire** troppo**su**. Set hello **finestra temporale** (frequenza toocapture) e **dimensioni finestra** (toocapture dimensioni dati). 
    
    d. Per **acquisire Provider**selezionare **archivio Azure Data Lake** e selezionare hello hello archivio Data Lake creato in precedenza. Per **Data Lake percorso**, immettere il nome di hello della cartella di hello è stato creato in hello account archivio Data Lake. È necessario solo cartella toohello di tooprovide hello percorso relativo.

    e. Lasciare hello **formati del nome file acquisizione esempio** toohello predefinita. Questa opzione determina una struttura di cartelle hello che viene creato nella cartella di acquisizione hello.

    f. Fare clic su **Crea**.

## <a name="test-hello-setup"></a>Programma di installazione di prova hello

È ora possibile testare la soluzione hello inviando dati toohello Hub di eventi di Azure. Seguire le istruzioni di hello in [inviare eventi di hub di eventi tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Dopo aver iniziato l'invio dei dati di hello, vedrai dati hello riflessi in archivio Data Lake con struttura di cartelle hello specificato. Ad esempio, è visualizzata una struttura di cartelle, come illustrato nella seguente schermata, nell'archivio Data Lake hello.

![Dati dell'hub eventi di esempio in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Dati dell'hub eventi di esempio in Data Lake Store")

> [!NOTE]
> Anche se non si dispone di messaggi in arrivo nell'hub eventi, gli hub di eventi scrive file vuoti con solo le intestazioni di hello in hello account archivio Data Lake. Hello file vengono scritti in hello stesso intervallo di tempo specificato durante la creazione di hub eventi hello.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Analizzare i dati in Archivio Data Lake

Una volta dati hello in archivio Data Lake, è possibile eseguire i processi analitici tooprocess e elaborare dati hello. Vedere [USQL Avro esempio](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sulla toodo questo usando Azure Data Lake Analitica.
  

## <a name="see-also"></a>Vedere anche
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Copiare i dati da un archivio Azure archiviazione BLOB tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
