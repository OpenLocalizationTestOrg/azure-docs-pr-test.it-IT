---
title: documentazione della Guida aaaMulti geografica | Documenti Microsoft
description: Informazioni su come toocreate un'area di lavoro e pubblicare un servizio web in un'area di Azure diversa da hello meridionale centrale United States (SCUS) regione di Azure.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Guida per più aree geografiche
Questo articolo illustra come creare un'area di lavoro e pubblicare un servizio Web in altre aree geografiche di Azure.  Hello [prodotti Azure dalla pagina area](https://azure.microsoft.com/en-us/regions/services/) sono elencate le aree in cui Azure Machine Learning è disponibile.

## <a name="create-a-workspace"></a>Creare un'area di lavoro
1. Accedi toohello portale classico di Azure.
2. Fare clic su **+ NUOVO** > **SERVIZI DATI** > **MACHINE LEARNING** > **CREAZIONE RAPIDA**.  In **INDIRIZZO** selezionare un'altra area, ad esempio **Asia sud-orientale**.
   ![Guida per più aree geografiche immagine 1][1]
3. Selezionare l'area di lavoro hello e quindi fare clic su **Accedi tooML Studio**.
   ![Guida per più aree geografiche immagine 2][2]
4. Ora si dispone di un'area di lavoro in un'altra area geografica che può essere utilizzata come qualsiasi altra area di lavoro. tooswitch tra le aree di lavoro, aspetto toohello superiore destro dello schermo. Fare clic su elenco a discesa hello, hello selezionare area e area di lavoro selezionare hello. Tutti gli elementi è l'area dell'area di lavoro locale toohello.  Ad esempio, i servizi web creati da un'area di lavoro si trovano nella stessa area di lavoro area hello hello.
   ![Guida per più aree geografiche immagine 3][3]

## <a name="open-an-experiment-from-gallery"></a>Aprire un esperimento dalla raccolta
Se si apre un esperimento dalla raccolta, è possibile selezionare l'area da toocopy hello esperimento.

![Guida per più aree geografiche immagine 4][4a]

## <a name="web-service-management"></a>Gestione del servizio Web
tooprogrammatically gestire servizi web, ad esempio per la ripetizione di training, Usa hello specifiche indirizzo:

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>Operazioni toonote
1. È possibile copiare solo esperimenti tra aree di lavoro che appartengono toohello stessa area in questo modo. Se è necessario toocopy esperimento nelle aree di lavoro in aree diverse, è possibile utilizzare hello [PowerShell](http://aka.ms/amlps) cmdlet [ *copia AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish che. Un'altra soluzione alternativa è toopublish hello esperimento nella raccolta in modalità non in elenco, quindi aprirlo nell'area di lavoro hello hello altre aree.
2. selettore di Hello area verrà visualizzate solo le aree di lavoro per un'area alla volta.  
3. Un’area di lavoro con accesso libero o Guest (anonimo) verrà creata e ospitata in Stati Uniti centro-meridionali.  
4. I servizi Web distribuiti da un'area di lavoro nell’Asia sudorientale verranno anche ospitati in Asia sudorientale.  

## <a name="more-information"></a>Altre informazioni
Porre una domanda su hello [forum di Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
