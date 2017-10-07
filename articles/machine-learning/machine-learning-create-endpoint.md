---
title: endpoint del servizio Web aaaCreating in Machine Learning | Documenti Microsoft
description: Creazione di endpoint del servizio Web in Azure Machine Learning
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Creazione di endpoint
> [!NOTE]
>  Questo argomento vengono descritte le tecniche applicabile tooa **classico** servizio Web di Machine Learning.
> 
> 

Quando si creano servizi Web che si vendono tooyour Avanti clienti, è necessario cliente tooeach di modelli di training tooprovide che sono ancora collegato toohello esperimento da quale hello Web servizio è stato creato. Inoltre, gli aggiornamenti toohello esperimento deve essere applicati in modo selettivo tooan endpoint senza sovrascrivere le personalizzazioni hello.

tooaccomplish, Azure Machine Learning consente toocreate più endpoint per un servizio Web distribuito. Ogni endpoint nel servizio Web hello in modo indipendente è indirizzata, limitata e gestito. Ogni endpoint è una chiave univoca di URL e l'autorizzazione che è possibile distribuire i clienti tooyour.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Aggiunta del servizio Web di endpoint tooa
Esistono tre modi tooadd un tooa endpoint servizio Web.

* A livello di codice
* Tramite il portale di servizi Web di Azure Machine Learning hello
* Sebbene hello portale di Azure classico

Dopo aver creato endpoint hello, è possibile utilizzarlo tramite le API sincrone, le API, batch e fogli di lavoro di excel. Inoltre tooadding endpoint tramite questa interfaccia, è inoltre possibile utilizzare hello API di gestione Endpoint tooprogrammatically aggiungere gli endpoint.

> [!NOTE]
> Se sono stati aggiunti toohello altri endpoint servizio Web, è possibile eliminare l'endpoint predefinito hello.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Aggiunta di un endpoint a livello di codice
È possibile aggiungere un servizio Web di tooyour endpoint a livello di programmazione utilizzando hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) codice di esempio.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Aggiunta di un endpoint tramite il portale di servizi Web di Azure Machine Learning hello
1. In Machine Learning Studio, nella colonna sinistra hello, fare clic su servizi Web.
2. Nella parte inferiore di hello del dashboard del servizio Web hello, fare clic su **gestire endpoint**. pagina endpoint toohello per hello servizio Web viene visualizzato il portale di servizi Web di Azure Machine Learning Hello.
3. Fare clic su **New**.
4. Digitare un nome e una descrizione per il nuovo endpoint di hello. I nomi degli endpoint devono contenere al massimo 24 caratteri alfanumerici (con lettere minuscole). Selezionare il livello di registrazione hello e indica se sono abilitati i dati di esempio. Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Aggiunta di un endpoint utilizzando hello portale di Azure classico
1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com), fare clic su **Machine Learning** nella colonna sinistra hello. Fare clic su area di lavoro hello che contiene il servizio Web hello in cui si è interessati.
   
    ![Passare tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Fare clic su **Servizi Web**.
   
    ![Passare a servizi tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. Fare clic su servizio Web hello desiderati nell'elenco di hello toosee di endpoint disponibili.
   
    ![Passare tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Nella parte inferiore di hello della pagina hello, fare clic su **Aggiungi Endpoint**. Digitare un nome e descrizione, verificare che non sono presenti altri endpoint con hello stesso nome in questo servizio Web. Lasciare il livello di limitazione hello con il valore predefinito a meno che non si hanno esigenze particolari. toolearn più sulla limitazione, vedere [gli endpoint dell'API scalabilità](machine-learning-scaling-webservice.md).
   
    ![Creare un endpoint](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Passaggi successivi
[Come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

