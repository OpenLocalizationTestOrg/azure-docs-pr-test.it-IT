---
title: aaaDeploy tooAzure Analysis Services tramite SSDT | Documenti Microsoft
description: Informazioni su come toodeploy tooan un modello tabulare Azure Analysis Services server mediante SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Distribuire un modello da SSDT
Dopo aver creato un server nella sottoscrizione di Azure, si è pronti toodeploy un tooit database modello tabulare. È possibile utilizzare SQL Server Data Tools (SSDT) toobuild e distribuire un progetto di modello tabulare, che si sta lavorando. 

## <a name="prerequisites"></a>Prerequisiti
tooget avviato, è necessario:

* Un **server Analysis Services** in Azure. vedere, più toolearn [creare un server Azure Analysis Services](analysis-services-create-server.md).
* **Progetto di modello tabulare** in SSDT o un modello tabulare esistente in hello 1200 o livello di compatibilità superiore. Se non è mai stato creato un progetto simile, Provare a hello [esercitazione relativa alla modellazione tabulare delle vendite Internet di Adventure Works](https://msdn.microsoft.com/library/hh231691.aspx).
* **Gateway locale** -se uno o più origini dati locali nella rete dell'organizzazione, è necessario tooinstall un [gateway dati locale](analysis-services-gateway.md). gateway di Hello è necessario per il server nel cloud hello connettersi tooyour locale origini tooprocess e l'aggiornamento dati nel modello di hello.

> [!TIP]
> Prima di distribuire, assicurarsi che è possibile elaborare dati hello nelle tabelle. In SSDT fare clic su **Modello** > **Elabora** > **Elabora tutto**. Se l'elaborazione ha esito negativo, la distribuzione non potrà essere eseguita.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy un modello tabulare in SSDT

1. Prima di distribuire, è necessario il nome di server hello tooget. In **portale di Azure** > server > **Panoramica** > **nome Server**, nome del server hello copia.
   
    ![Ottenere il nome del server in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. In SSDT > **Esplora**, progetto hello rapida > **proprietà**. Quindi nel **distribuzione** > **Server** incollare il nome di server hello.   
   
    ![Incollare il nome del server nelle proprietà del server di distribuzione](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Proprietà** e quindi scegliere **Distribuisci**. Potrebbe essere richiesta toosign in tooAzure.
   
    ![Distribuire tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Nella finestra di Output sia hello e distribuzione, verrà visualizzato lo stato di distribuzione.
   
    ![Stato della distribuzione](./media/analysis-services-deploy/aas-deploy-status.png)

Questo è tutto è tooit!


## <a name="troubleshooting"></a>Risoluzione dei problemi
Se la distribuzione non riesce durante la distribuzione dei metadati, è probabile perché SSDT non riesce a connettersi tooyour server. Verificare che è possibile connettere il server tooyour tramite SSMS. Verificare quindi la proprietà Server di distribuzione per il progetto hello hello sia corretto.

Se la distribuzione non riesce in una tabella, è probabile perché il server non è stato possibile connettersi tooa origine dei dati. Se l'origine dati locale nella rete dell'organizzazione, tooinstall assicurarsi di essere un [gateway dati locale](analysis-services-gateway.md).

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il server di modello tabulare distribuito tooyour, si è pronti tooconnect tooit. È possibile [connettersi tooit con SSMS](analysis-services-manage.md) toomanage è. E, è possibile [tooit utilizzando uno strumento client di connettersi](analysis-services-connect.md) come Power BI, Power BI Desktop o Excel e avviare la creazione di report.

