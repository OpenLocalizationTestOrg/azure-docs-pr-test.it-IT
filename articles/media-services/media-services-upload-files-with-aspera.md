---
title: file aaaUpload in un account di servizi multimediali di Azure tramite Aspera | Documenti Microsoft
description: "In questa esercitazione illustra i passaggi hello di caricamento di file in un account di archiviazione che è associato a un account di servizi multimediali tramite hello * * il servizio Aspera Server su richiesta * * in Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Caricare file in un account di servizi multimediali con il servizio di Aspera Server On Demand hello in Azure

## <a name="overview"></a>Panoramica

**Aspera** è un software di trasferimento di file ad alta velocità. **Aspera Server On Demand** per Azure consente il caricamento ad alta velocità e il download di file di grandi dimensioni direttamente nell'archivio di oggetti BLOB di Azure. Per informazioni su **Aspera On Demand**, vedere hello [Aspera Cloud](http://cloud.asperasoft.com/) sito. 
  
**Aspera Server On Demand** per Azure è disponibile per l'acquisto di hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). Ordinare toocomplete un acquisto **Aspera Server On Demand** per Azure, accedere in Azure Marketplace con Windows Live ID.

In questa esercitazione illustra i passaggi hello di caricamento di file in un account di archiviazione che è associato a un account di servizi multimediali tramite hello **Aspera Server On Demand** servizio in Azure. 

È possibile trovare un esempio che illustra il funzionamento di Azure toouse con servizi multimediali e di Aspera [qui](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Vi è limite toohello dimensioni massime supportate per l'elaborazione con servizi multimediali di Azure processori di contenuti multimediali (MP). Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.
>

## <a name="prerequisites"></a>Prerequisiti 

toocomplete questa esercitazione, è necessario:

* Un Windows Live ID.
* Un [account Azure](https://azure.microsoft.com). Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Un [account Servizi multimediali di Azure](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Acquistare Aspera On Demand per Azure

Dopo aver eseguito l'accesso in Azure Marketplace, seguire questi passaggi di base di toocomplete l'acquisto di Aspera On Demand per Azure.

1. Cercare Aspera e selezionare "Server On Demand".

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Esaminare i piani di abbonamento hello e fare clic su 'Iscrizione'

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Compilare le specifiche di hello del Server per la sottoscrizione richiesta.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Fare clic su hello **tariffario** e selezionare il volume mensile desiderato nel Pannello di hello sub. In hello **pianificare dettagli** Pannello di seleziona **OK**. Quindi, nel hello **scegliere il livello di prezzo** pannello, fare clic su **selezionare**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Fare clic su **legali** tooview e accettare i termini legali specifici hello nel Pannello di hello sub. Dopo avere esaminato le note legali hello, fare clic su **acquisto**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Completare l'acquisto di hello facendo **crea**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. dashboard di Azure Hello annuncerà che esegue il provisioning del servizio hello.  Una volta completata con il provisioning, è possibile trovare una nuova sottoscrizione hello eseguendo una ricerca delle risorse per il nome del servizio hello hello. Dopo avere trovato servizio hello, fare doppio clic su di esso toolaunch hello portale.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Avviare il portale di gestione di hello Aspera. Dopo aver individuato il nuovo servizio Aspera, è possibile delineare portale di gestione di accessi toohello, facendo clic sul servizio hello.  Verrà aperto un nuovo pannello. Da all'interno di tale pannello nuova, è necessario tooclick su hello **nome risorsa** del nuovo servizio.  Nella seguente schermata di hello, il nome di risorsa hello è 'AsperaTransferDemo'. Quando si fa clic sul nome di risorsa hello, viene avviato un altro pannello. Nel nuovo pannello aperto sarà visualizzato un collegamento "Manage" (Gestisci). Fare clic su hello portale di gestione di Aspera hello toolaunch di collegamento 'Gestisci'.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Facendo clic su hello gestire collegamento, si otterrà una pagina di registrazione toohello, che è necessario tooaccess hello del servizio.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. A questo punto, è necessario disporre di accesso toohello Aspera servizio portale di gestione, in cui è possibile creare chiavi di accesso, scaricare le licenze e i client di Aspera, visualizzare l'utilizzo e informazioni sulle API hello.

    Hello figura seguente viene illustrata la creazione di accesso hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Hello seguente schermata Mostra utilizzo hello reporting interfacce nel portale di hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Caricare file con Aspera

1. Scaricare e installare il software client di Aspera hello:
    
    * [Plug-in del browser](http://downloads.asperasoft.com/connect2/)
    * [Rich client](http://downloads.asperasoft.com/en/downloads/2)

2. Eseguire il primo trasferimento. In ordine toouse hello Aspera client tootransfer con servizio trasferimento Aspera hello, è necessario seguente hello toocomplete: 

    1. Creare una chiave di accesso, tramite il portale di Aspera hello.  
    2. Download, l'installazione e client delle licenze hello Aspera (software sono disponibili nel portale di Aspera hello).  

    >[!NOTE]
    >Leggere una Guida di client Aspera hello per le informazioni di configurazione.
    
    3. Recuperare alcune informazioni dell'account di archiviazione che è associato con l'Account di supporto di Azure tramite hello [portale di Azure](https://portal.azure.com/). In particolare, nome e chiave e al nome contenitore blob di archiviazione hello in toowhich desiderato tooplace il contenuto. 

        * informazioni di archiviazione hello tooget dal portale hello: trovare account di archiviazione, fare clic sulle chiavi di accesso hello e copia hello nome e hello la chiave dell'account.
        * nome del contenitore hello tooget: trovare l'account di archiviazione, seleziona **BLOB**, selezionare il nome di hello del contenitore di hello si desidera tooupload hello contenuto in. 

    Di seguito è la schermata di hello del client di Aspera hello **Connection Manager** in cui è necessario specificare il tipo di archiviazione 'Azure' hello e le credenziali, nonché il contenitore di blob hello.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Risorse

Hello seguenti risorse è citata in questo articolo. 

* [Collegare il plug-in del browser](http://downloads.asperasoft.com/connect2/)
* [Guida alla connessione](http://downloads.asperasoft.com/en/documentation/8)
* [Client Aspera](http://downloads.asperasoft.com/en/downloads/2)
* [Guida al client](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Passaggi successivi

È ora possibile [copiare BLOB da un account di archiviazione in un account AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

