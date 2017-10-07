---
title: aaaHow toodeploy un servizio Web aree toomultiple | Documenti Microsoft
description: Passaggi toodeploy (copia) le aree tooother un nuovo servizio Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Come un servizio Web toodeploy toomultiple aree
Hello nuovi servizi Web di Azure consentono di tooeasily distribuire un toomultiple le aree del servizio web senza la necessità di più sottoscrizioni o aree di lavoro. 

I prezzi sono specifico, che pertanto è necessario definire un piano di fatturazione per ogni area in cui verranno distribuiti servizio web hello dell'area.

## <a name="toocreate-a-plan-in-another-region"></a>un piano in un'altra area toocreate
1. Accedere a [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)(Servizi Web Microsoft Azure Machine Learning).
2. Fare clic su hello **piani** opzione di menu.
3. Nei piani di hello sulla pagina di visualizzazione, fare clic su **New**.
4. Da hello **sottoscrizione** sottoscrizione selezionare hello in cui hello risiederà nuovo piano di elenco a discesa.
5. Da hello **area** elenco a discesa, selezionare un'area per il nuovo piano di hello. opzioni relative al piano di Hello per area selezionata hello visualizzerà in hello **opzioni relative al piano** sezione della pagina hello.
6. Da hello **gruppo di risorse** elenco a discesa Seleziona una risorsa di gruppo per il piano di hello. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. In **nome piano** nome hello del tipo di piano hello.
8. In **opzioni del piano**, fare clic su hello livello fatturazione per il nuovo piano di hello.
9. Fare clic su **Crea**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Distribuzione di hello web servizio tooanother area
1. Fare clic su hello **servizi Web** opzione di menu.
2. Selezionare servizio Web si sta distribuendo tooa nuova area hello.
3. Fare clic su **Copy**.
4. In **nome del servizio Web**, digitare un nuovo nome per il servizio web hello.
5. In **descrizione servizio Web**, digitare una descrizione per il servizio web hello.
6. Da hello **sottoscrizione** sottoscrizione selezionare hello in cui hello risiederà nuovo servizio web dal menu a discesa.
7. Da hello **gruppo di risorse** elenco a discesa Seleziona una risorsa di gruppo per il servizio web hello. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Da hello **area** area hello selezionare nel servizio web hello toodeploy elenco a discesa.
9. Da hello **account di archiviazione** elenco a discesa, seleziona un account di archiviazione in cui hello toostore servizio web.
10. Da hello **prezzo piano** elenco a discesa, selezionare un piano nell'area di hello selezionato nel passaggio 8.
11. Fare clic su **Copy**.

