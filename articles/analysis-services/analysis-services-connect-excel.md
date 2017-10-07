---
title: aaaConnect tooAzure Analysis Services con Excel | Documenti Microsoft
description: Informazioni su come tooconnect tooan Azure Analysis Services server utilizzando Excel.
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Connettersi con Excel

Dopo avere creato un server in Azure e distribuiti tooit un modello tabulare, è possibile tooconnect e iniziare l'esplorazione dei dati.


## <a name="connect-in-excel"></a>Connettersi in Excel

Connessione server tooa in Excel è supportata tramite recupera dati in Excel 2016. Connessione tramite l'importazione guidata tabella hello in Power Pivot non è supportata. 

**tooconnect in Excel 2016**

1. In Excel 2016, in hello **dati** della barra multifunzione, fare clic su **Carica dati esterni** > **da altre origini** > **da Analysis Services** .

2. Nella connessione guidata dati di hello in **nome Server**, immettere il nome di server hello compresi il protocollo e URI. Quindi, nel **le credenziali di accesso**selezionare **hello utilizzare seguito nome utente e Password**e quindi digitare il nome di account utente aziendale hello, ad esempio nancy@adventureworks.come la password.

    ![Connettersi dall'accesso a Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. In **seleziona Database e tabella**, selezionare il database di hello e modello o una prospettiva e quindi fare clic su **fine**.
   
    ![Connettersi dal modello di selezione in Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Vedere anche
[Librerie client](analysis-services-data-providers.md)   
[Gestire il server](analysis-services-manage.md)     


