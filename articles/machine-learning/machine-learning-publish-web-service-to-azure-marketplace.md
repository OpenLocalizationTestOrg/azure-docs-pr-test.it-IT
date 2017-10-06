---
title: AAA(deprecated) pubblica machine learning tooAzure servizio web Marketplace | Documenti Microsoft
description: (obsoleto) Come toopublish il toohello servizio Web di Azure Machine Learning Azure Marketplace
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(obsoleto) Pubblicazione servizio Web di Azure Machine Learning toohello Azure Marketplace

> [!NOTE]
> DataMarket e Servizi dati verranno ritirati e le sottoscrizioni esistenti verranno ritirate e annullate a partire dal 31/3/2017. Di conseguenza, questo articolo è deprecato. 
> 
> In alternativa, è possibile pubblicare il toohello esperimenti di Machine Learning [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) benefit hello della community di analisi scientifica dei dati hello. Per ulteriori informazioni, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hello Azure Marketplace consente hello servizi web di Azure Machine Learning toopublish come a pagamento o gratuito servizi per l'utilizzo da parte dei clienti esterni. In questo articolo viene fornita una panoramica del processo con collegamenti tooguidelines tooget che è stato avviato. Tramite questo processo, apportare i servizi web disponibili per altri tooconsume sviluppatori nelle proprie applicazioni.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Panoramica del processo di pubblicazione hello
esempio Hello hello passaggi per la pubblicazione di un tooAzure di servizio web Azure Machine Learning Marketplace:

1. Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.
2. Distribuire tooproduction servizio hello e ottenere informazioni sull'endpoint chiave API e OData hello.
3. Utilizzo URL hello di hello pubblicati toopublish servizio web troppo[Azure Marketplace (dati di mercato)](https://publish.windowsazure.com/workspace/) 
4. Una volta inviato, viene esaminato l'offerta e deve toobe approvata prima i clienti possono avviare acquisto. processo di pubblicazione Hello può richiedere qualche giorno lavorativo. 

## <a name="walk-through"></a>Procedura dettagliata
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Passaggio 1: Creare e pubblicare un servizio di richiesta-risposta di Machine Learning.
 Se non è già stato fatto, vedere questa [procedura dettagliata](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Passaggio 2: Distribuire tooproduction servizio hello e ottenere informazioni sull'endpoint chiave API e OData hello
1. Da hello [portale di Azure classico](http://manage.windowsazure.com)selezionare hello **MACHINE LEARNING** opzione hello barra di navigazione sinistra e selezionare l'area di lavoro. 
2. Fare clic su hello **servizi WEB** scheda e servizio web selezionare hello desideri toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Selezionare l'endpoint di hello che comporta come toohave hello marketplace l'utilizzo. Se non è stato creato alcun endpoint aggiuntivi, è possibile selezionare hello **predefinito** endpoint.
4. Dopo aver selezionato sull'endpoint hello, sarà in grado di toosee hello **chiave API**. Copiare la chiave, perché queste informazioni saranno necessarie in seguito nel passaggio 3.
   
    ![Azure Marketplace][apikey]
5. Fare clic su hello **richiesta/risposta** toohello marketplace di servizi (metodo), a questo punto di pubblicazione dell'esecuzione batch non è supportata. Si passerà toohello API pagina della Guida per il metodo di richiesta/risposta hello.
6. Hello copia **indirizzo dell'Endpoint OData**, è necessario che queste informazioni in un secondo momento nel passaggio 3.
   
    ![Azure Marketplace][odata]

distribuire il servizio di hello nell'ambiente di produzione.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Passaggio 3: Utilizzo hello URL di hello pubblicati web servizio toopublish tooAzure Marketplace (DataMarket)
1. Passare troppo[Azure Marketplace (dati di mercato)](http://datamarket.azure.com/home) 
2. Fare clic su hello **pubblica** collegamento nella parte superiore di hello della pagina hello. L'operazione richiederà toohello [portale di pubblicazione di Microsoft Azure](https://publish.windowsazure.com)
3. Fare clic su hello **editori** sezione tooregister come server di pubblicazione.
4. Quando si crea una nuova offerta, selezionare **Servizi dati**, quindi fare clic su **Crea un nuovo documento di servizio dati**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. In **Piani** fornire le informazioni relative all'offerta, incluso un piano tariffario. Decidere se offrire un servizio gratuito o a pagamento. tooget a pagamento, fornire le informazioni di pagamento, ad esempio le informazioni bancari e fiscali.
6. In **Marketing** forniscono informazioni sull'offerta, ad esempio titolo hello e una descrizione per l'offerta.
7. In **prezzi** è possibile impostare il prezzo di hello per i piani di paesi specifici, oppure consentire al sistema di hello "autoprice" l'offerta.
8. In hello **servizio dati** scheda, fare clic su **servizio Web** come hello **origine dati**.
   
    ![Azure Marketplace][image2]
9. Ottenere hello web service URL e la chiave API da hello portale classico di Azure, come illustrato nel passaggio 2 precedente.
10. Nella casella di finestra di dialogo programma di installazione del servizio dati di Marketplace hello, incollare l'indirizzo dell'endpoint OData hello in hello **URL del servizio** casella di testo.
11. Per **autenticazione**, scegliere **intestazione** come hello **schema di autenticazione**.
    
    * Immettere "Authorization" per hello **nome intestazione**.
    * Per hello **valore dell'intestazione**, immettere "Bearer" (senza virgolette hello), fare clic su hello **spazio** barra e quindi incollare la chiave API hello.
    * Seleziona hello **questo servizio è OData** casella di controllo.
    * Fare clic su **Test connessione** connessione hello tootest.
12. In **Categorie** assicurarsi che sia selezionata l'opzione **Machine Learning**.
13. Dopo avere immesso tutti hello metadati sull'offerta, fare clic su **pubblica**e quindi **Push tooStaging**. A questo punto, si verrà informato di eventuali problemi rimanenti che è necessario toofix.
14. Dopo aver verificato il completamento di tutti i problemi in sospeso hello, fare clic su **richiesta approvazione toopush tooProduction**. processo di pubblicazione Hello può richiedere qualche giorno lavorativo. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

