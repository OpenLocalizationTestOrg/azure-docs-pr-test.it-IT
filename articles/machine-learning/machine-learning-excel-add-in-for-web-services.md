---
title: il componente aggiuntivo aaaExcel per i servizi Web di Machine Learning | Documenti Microsoft
description: Come toouse Web di Azure Machine Learning services direttamente in Excel senza scrivere alcun codice.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning
Excel rende facile toocall i servizi web direttamente senza hello necessario toowrite qualsiasi codice.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Passaggi tooUse un servizio web esistente nella cartella di lavoro hello

1. Aprire hello [file di Excel di esempio](http://aka.ms/amlexcel-sample-2), che contiene hello aggiuntivo Excel e dati sul passeggeri in hello Titanic.
2. Scegliere servizio web hello facendovi clic sopra-"Titanic superstite predittive (componente aggiuntivo di Excel esempio) [punteggio]" in questo esempio.
   
    ![Selezionare il servizio Web][01]
3. Consente di passare toohello **Predict** sezione.  Questa cartella di lavoro contiene già dati di esempio, ma per una cartella di lavoro vuota è anche possibile selezionare una cella in Excel e fare clic su **Use sample data**(Usa dati di esempio).
4. Selezionare i dati di hello con intestazioni e fare clic sull'icona di intervallo di hello dati di input.  Verificare che sia selezionata la casella "dati con intestazioni" hello.
5. In **Output**, immettere il numero di celle hello in cui si desidera hello toobe output, ad esempio "H1" di seguito.
6. Fare clic su **Stima**.
   
    ![Sezione Stima][02]

Distribuire un servizio Web o usarne uno esistente. Per ulteriori informazioni sulla distribuzione di un servizio web, vedere [passaggio 5 di questa procedura dettagliata: distribuzione di servizio Web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).

Ottenere la chiave API hello per il servizio web. La posizione in cui viene eseguita l'operazione varia a seconda che sia stato pubblicato un servizio Web classico o un nuovo servizio Web di Machine Learning.

**Usare un servizio Web classico** 

1. In Machine Learning Studio, fare clic su hello **servizi WEB** sezione nel riquadro di sinistra hello e quindi selezionare servizio web hello.
   
    ![Selezione di un servizio Web in Studio][04]
2. Copiare la chiave API hello per il servizio web hello.
   
    ![Chiave API in Studio][05]
3. In hello **DASHBOARD** per servizio web hello scheda, fare clic su hello **richiesta/risposta** collegamento.
4. Cercare hello **URI della richiesta** sezione.  Copiare e salvare hello URL.

> [!NOTE]
> È ora possibile toosign in hello [servizi Web di Azure Machine Learning](https://services.azureml.net) chiave hello API tooobtain portale per un servizio web classico Machine Learning.
> 
> 

**Usare un nuovo servizio Web**

1. In hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale, fare clic su **servizi Web**, quindi selezionare il servizio web. 
2. Fare clic su **Consume**(Uso).
3. Cercare hello **informazioni di base al consumo** sezione. Copiare e salvare hello **chiave primaria** hello e **richiesta-risposta** URL.

## <a name="steps-tooadd-a-new-web-service"></a>Passaggi tooAdd un nuovo servizio web

1. Distribuire un servizio Web o usarne uno esistente. Per ulteriori informazioni sulla distribuzione di un servizio web, vedere [passaggio 5 di questa procedura dettagliata: distribuzione di servizio Web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).
2. Fare clic su **Consume**(Uso).
3. Cercare hello **informazioni di base al consumo** sezione. Copiare e salvare hello **chiave primaria** hello e **richiesta-risposta** URL.
4. In Excel, visitare toohello **servizi Web** sezione (in hello **Predict** sezione, fare clic su hello freccia indietro toogo toohello elenco dei servizi web).
   
    ![Passare la selezione di servizio tooWeb][03]
5. Fare clic su **Aggiungi servizio Web**.
6. Incollare hello URL nella casella di testo di componente aggiuntivo di Excel hello **URL**.
7. Chiave API o primario di hello Incolla nella casella di testo hello **chiave API**.
8. Fare clic su **Aggiungi**.
   
    ![URL e chiave API per un servizio Web classico.][06]
9. servizio web di hello toouse, hello precedono le direzioni, consultare "Passaggi tooUse un servizio web di esistente."

## <a name="sharing-your-workbook"></a>Condivisione della cartella di lavoro
Se si salva la cartella di lavoro, viene salvata anche chiave API o primario hello per servizi web hello che è stato aggiunto. Pertanto, che si deve solo condivisione hello con utenti che attendibili.

Porre domande in hello seguenti commento sezione o nella nostri [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
