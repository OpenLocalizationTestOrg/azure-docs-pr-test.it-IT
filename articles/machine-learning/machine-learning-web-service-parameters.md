---
title: Parametri del servizio Web Azure Machine Learning aaaUse | Documenti Microsoft
description: Come toouse parametri del servizio Web Azure Machine Learning toomodify hello comportamento del modello quando accede al servizio web hello.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Usare i parametri del servizio Web di Azure Machine Learning
Un servizio Web di Azure Machine Learning viene creato mediante la pubblicazione di un esperimento contenente moduli con parametri configurabili. In alcuni casi, è consigliabile comportamento del modulo hello toochange durante l'esecuzione di servizio web hello. *I parametri di servizio Web* consentono toodo questa attività. 

Un esempio comune è impostazione hello [l'importazione dei dati] [ reader] modulo utente hello di hello pubblicato il servizio web è possibile specificare un'origine dati diversa quando accede al servizio web hello. O configurazione hello [Esporta dati] [ writer] modulo in modo che è possibile specificare una destinazione diversa. Alcuni altri esempi includono la modifica hello numero di bit per hello [Feature Hashing] [ feature-hashing] modulo o hello numero di funzioni desiderate per hello [Filter-Based Feature Selection] [ filter-based-feature-selection] modulo. 

È possibile impostare i parametri del servizio Web e associarli a uno o più parametri di modulo nell’esperimento, e specificare se sono obbligatori o facoltativi. utente Hello del servizio web hello può quindi fornire valori per questi parametri quando si chiamano un servizio web hello. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Come tooset e utilizzare i parametri di servizio Web
Per definire un parametro del servizio Web, fare clic sul parametro successivo toohello hello icona per un modulo e selezionando "Imposta come parametro del servizio web". Questo crea un nuovo parametro del servizio Web e lo connette parametro module toothat. Quindi, quando si accede a servizio web hello, hello utente può specificare un valore per hello parametro del servizio Web ed è il parametro di modulo toohello applicato.

Quando si definisce un parametro di servizio Web, è disponibile tooany altro parametro di modulo nell'esperimento hello. Se si definisce un parametro di servizio Web associato a un parametro per un modulo, è possibile utilizzare tale parametro di servizio Web stesso per qualsiasi altro modulo come parametro di hello prevede hello dello stesso tipo di valore. Ad esempio, se hello parametro del servizio Web è un valore numerico, quindi utilizzabile solo per i parametri di modulo che prevede un valore numerico. Quando l'utente hello imposta un valore per hello parametro del servizio Web, verrà applicato tooall associati parametri del modulo.

È possibile decidere se il valore predefinito tooprovide per hello parametro del servizio Web. Se quindi, hello parametro è facoltativo per l'utente hello del servizio web hello. Se non si fornisce un valore predefinito, utente hello è tooenter richiesto un valore quando accede al servizio web hello.

documentazione dell'API per servizi web hello Hello include informazioni per utente del servizio web hello in modo toospecify hello parametro del servizio Web a livello di codice quando l'accesso al servizio web hello.

> [!NOTE]
> Hello documentazione dell'API per un servizio web classico è fornito da hello **pagina della Guida API** collegamento nel servizio web hello **DASHBOARD** in Machine Learning Studio. Hello documentazione dell'API per un nuovo servizio web viene fornito da hello [servizi Web di Azure Machine Learning](https://services.azureml.net/Quickstart) portale su hello **consumare** e **Swagger API** pagine per il servizio Web.
> 
> 

## <a name="example"></a>Esempio
Ad esempio, si supponga di disporre un esperimento con un [Esporta dati] [ writer] modulo che invia informazioni sull'archiviazione di blob tooAzure. Definiamo un parametro di servizio Web denominato "Percorso Blob" che consente di hello web servizio utente toochange hello percorso toohello archiviazione blob quando accede al servizio hello.

1. In Machine Learning Studio, fare clic su hello [Esporta dati] [ writer] tooselect modulo è. Le relative proprietà vengono visualizzate in hello proprietà riquadro toohello destra dell'area di disegno esperimento hello.
2. Specificare il tipo di archiviazione hello:
   
   * In **Please specify data destination**(Specificare la destinazione dei dati) selezionare "Azure Blob Storage" (Archivio BLOB di Azure).
   * In **Please specify authentication type**selezionare "Account".
   * Immettere le informazioni sull'account hello per hello archiviazione blob di Azure. 
     <p />
3.Fare clic su hello icona toohello diritto di hello **tooblob che inizia con il parametro contenitore**. L'aspetto sarà simile al seguente:
   
   ![Icona del parametro del servizio Web][icon]
   
   Selezionare "Set as web service parameter".
   
   Viene aggiunta una voce in **parametri del servizio Web** nella parte inferiore di hello del riquadro Proprietà hello hello "percorso tooblob che iniziano con con contenitore". Si tratta di hello parametro del servizio Web che è ora associato a questo [Esporta dati] [ writer] parametro module.
4. toorename hello parametro del servizio Web, fare clic sul nome di hello, immettere "Percorso Blob" e premere hello **invio** chiave. 
5. tooprovide un valore predefinito per hello parametro del servizio Web, fare clic su hello icona toohello destra del nome hello selezionare "Ottenere il valore predefinito", immettere un valore (ad esempio, "container1/output1.csv") e premere hello **invio** chiave.
   
   ![Parametro del servizio Web][parameter]
6. Fare clic su **Run**. 
7. Fare clic su **distribuzione servizio Web** e selezionare **distribuzione di un servizio Web [classica]** o **distribuzione servizio Web [New]** servizio web di toodeploy hello.

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

utente Hello del servizio web hello ora è possibile specificare una nuova destinazione per hello [Esporta dati] [ writer] modulo quando l'accesso al servizio web hello.

## <a name="more-information"></a>Altre informazioni
Per un esempio più dettagliato, vedere hello [parametri del servizio Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) voce hello [Blog di Machine Learning](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Per ulteriori informazioni sull'accesso a un servizio web Machine Learning, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

