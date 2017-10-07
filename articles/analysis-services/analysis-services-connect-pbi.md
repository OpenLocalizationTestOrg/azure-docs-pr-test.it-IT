---
title: aaaConnect tooAzure Analysis Services con Power BI | Documenti Microsoft
description: Informazioni su come tooconnect tooan Azure Analysis Services server tramite Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a>Connettersi con Power BI

Dopo avere creato un server in Azure e distribuiti tooit un modello tabulare, gli utenti dell'organizzazione tooconnect pronto e iniziano l'esplorazione dei dati. 

> [!TIP]
> Essere certi toouse hello versione [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a>Connettersi in Power BI Desktop

1. In Power BI Desktop fare clic su **Recupera dati** > **Azure** > **Database di Azure Analysis Services**.

2. In **Server**, immettere il nome di server hello. 
    
    Essere l'URL completo che tooinclude hello. Ad esempio, asazure://westcentralus.asazure.windows.net/advworks.

3. In **Database**, se si conosce il nome di hello del database modello tabulare hello o una prospettiva si desidera tooconnect per incollarlo qui. In caso contrario, è possibile lasciare vuoto questo campo e selezionare un database o una prospettiva in un secondo momento.

4. Lasciare l'impostazione predefinita hello **connessione in tempo reale** opzione, quindi premere **Connetti**. 

5. Immettere le credenziali di accesso, se richieste. 

6. In **Navigator**, espandere server hello, quindi selezionare il modello di hello o una prospettiva che si desidera tooconnect su, quindi fare clic su **Connetti**. Fare clic su un modello o della prospettiva di tooshow tutti gli oggetti di hello per la visualizzazione.

    modello di Hello viene visualizzato in Power BI Desktop con un report vuoto nella visualizzazione di Report. elenco di campi Hello Visualizza tutti gli oggetti modello non nascosto. Stato di connessione viene visualizzato nell'angolo inferiore destro hello.

## <a name="connect-in-power-bi-service"></a>Connettersi in Power BI (servizio)

1. Creare un file di Power BI Desktop che dispone di un modello di connessione in tempo reale tooyour sul server.
2. In [Power BI](https://powerbi.microsoft.com) fare clic su **Recupera dati** > **File**. Individuare e selezionare il file.



## <a name="see-also"></a>Vedere anche
[Connettersi tooAzure Analysis Services](analysis-services-connect.md)   
[Librerie client](analysis-services-data-providers.md)

