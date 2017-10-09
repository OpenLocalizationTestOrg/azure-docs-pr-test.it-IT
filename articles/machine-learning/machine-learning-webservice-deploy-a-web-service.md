---
title: un nuovo servizio web in Azure Machine Learning aaaDeploying | Documenti Microsoft
description: servizio web basato su flusso di lavoro Hello della distribuzione di un ramo
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Distribuire un nuovo servizio Web
Microsoft Azure Machine learning ora fornisce i servizi web basati su [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) consentendo nuove opzioni del piano di fatturazione e le aree toomultiple del servizio web di distribuzione.

flusso di lavoro generale di Hello toodeploy un servizio web tramite i servizi Web di Microsoft Azure Machine Learning è:

* Creare un esperimento predittivo
* distribuirlo
* configurare il relativo nome
* piano di fatturazione
* eseguirne il test
* usarlo.

Hello seguente immagine illustra del flusso di lavoro di hello.

![Flusso di lavoro per la distribuzione di un servizio Web][1]

## <a name="deploy-web-service-from-studio"></a>Distribuire il servizio Web da Studio
toodeploy un esperimento come un nuovo servizio web. Accedere al hello Machine Learning Studio e creare un nuovo servizio web predittivo. 

**Nota**: se un esperimento è già stato distribuito come servizio Web classico non è possibile distribuirlo come un nuovo servizio Web.

Fare clic su **eseguire** nella parte inferiore di hello di hello provare l'area di disegno e quindi fare clic su **distribuzione servizio Web** e **distribuzione servizio Web [New]**. verrà visualizzata la pagina distribuzione Hello di Gestione servizio Web di Machine Learning hello.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Pagina Deploy Experiment (Sperimentazione distribuzione) di Machine Learning Web Service Manager
Nella pagina distribuzione esperimento hello, immettere un nome per il servizio web hello.
Selezionare un piano tariffario. Se si dispone di un piano tariffario esistente che è possibile selezionarlo, in caso contrario è necessario creare un nuovo piano di prezzo per servizio hello. 

1. In hello **prezzo piano** elenco a discesa, selezionare un piano esistente o hello **Seleziona nuovo piano** opzione.
2. In **nome piano**, digitare un nome che identifichi il piano di hello nella fattura.
3. Selezionare una delle hello **livelli di pianificazione mensile**. Si noti che i livelli di hello piano predefinito toohello piani per l'area predefinita e il servizio web sono distribuito toothat area.

Fare clic su **Distribuisci** e verrà visualizzata la pagina avvio rapido di hello per il servizio web.

## <a name="quickstart-page"></a>Pagina Avvio rapido
pagina avvio rapido del servizio web di Hello consente di ottenere accesso e informazioni aggiuntive sulle attività più comuni di hello che verranno eseguite dopo la creazione di un nuovo servizio web. Da qui è possibile accedere facilmente entrambi hello **Test** pagina e **consumare** pagina.

## <a name="testing-your-web-service"></a>Test del servizio Web
Dalla pagina avvio rapido di hello, fare clic su servizio web di Test nell'area attività comuni.   

servizio web tootest hello come un servizio di richiesta-risposta (RR):

* Fare clic su **Test** sulla barra dei menu hello.
* Fare clic su **Request-Response**(Richiesta-risposta).
* Immettere i valori appropriati per le colonne di input hello dell'esperimento.
* Fare clic su Test **Request-Response**(Test Richiesta-risposta).

Risultati verranno visualizzati in hello lato destro della pagina hello.

tootest un servizio web servizio esecuzione Batch (BES), si utilizzerà un file CSV:

* Fare clic su **Test** sulla barra dei menu hello.
* Fare clic su **Batch**.
* Nell'input dell'utente, fare clic su Sfoglia e passare i file di dati di esempio tooyour.
* Fare clic su **Test**.

stato Hello del test viene visualizzato in **testare i processi Batch**.

## <a name="consuming-your-web-service"></a>Uso del servizio Web
Quando viene pubblicato come servizio Web, gli esperimenti Azure Machine Learning forniscono un'API REST che può essere utilizzata da un'ampia gamma di dispositivi e piattaforme. Questo avviene perché i messaggi in formato hello simple API REST accetti e risponda con JSON. portale di Azure Machine Learning Hello fornisce codice che può essere utilizzato servizio web di hello toocall in R, c# e Python.

Nella pagina di consumo hello è possibile trovare:

* chiave API Hello e l'URI per l'utilizzo del servizio web nelle app.
* Excel e web tookick di modelli di app di avviare il processo di utilizzo.
* Codice di esempio in c#, python e R tooget è stato avviato.

Per ulteriori informazioni sull'utilizzo di servizi web, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'utilizzo dei servizi Web, vedere:

[Come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md)

[Servizi Web di Azure Machine Learning: distribuzione e uso](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
