---
title: un modello tabulare utilizzando Progettazione Web di Azure Analysis Services hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un modello tabulare di Analysis Services di Azure tramite hello designer Web nel portale di Azure.
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
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Creare un modello nel portale di Azure

funzionalità di progettazione (anteprima) Hello Azure Analysis Services web nel portale di Azure fornisce un modo semplice e rapido di toocreate e modificare i modelli tabulari e query modello dati direttamente nel browser. 

Tenere presente, finestra di progettazione web hello è **anteprima**. Mentre la nuova funzionalità viene aggiunto ogni volta hello, in anteprima, la funzionalità è limitata. Per più avanzate modello lo sviluppo e test, è migliore toouse Visual Studio (SSDT) e SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Prerequisiti

- Un server di Azure Analysis Services a livello di hello Standard o Developer. I nuovi modelli creati utilizzando la finestra di progettazione Web hello sono DirectQuery, supportato solo da questi livelli.
- Un database SQL di Azure, Azure SQL Data Warehouse o un file di Power BI Desktop (con estensione pbix) come origine dati. I nuovi modelli creati a partire da file di Power BI Desktop supportano origini dati di database SQL di Azure, Azure SQL Data Warehouse, Oracle e Teradata.
- Un account di SQL Server e una password per la connessione a origini di dati di Database SQL o Azure SQL Data Warehouse tooAzure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate un nuovo modello tabulare

1. Nel pannello **Panoramica**  del server > **Web designer** (Finestra di progettazione Web) fare clic su **Apri**.

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. In **Web designer** (Finestra di progettazione Web)  >  **Modelli** fare clic su **+ Aggiungi**.

    ![Creare un modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. In **Nuovo modello** digitare un nome di modello e quindi selezionare un'origine dati.

    ![Finestra di dialogo Nuovo modello nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. In **Connetti**, immettere le proprietà di connessione hello. Il nome utente e la password devono fare riferimento a un account di SQL Server.

     ![Finestra di dialogo Connetti nel portale di Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. In **tabelle e viste**selezionare hello tooinclude di tabelle nel modello e quindi fare clic su **crea**. Tra le tabelle con una coppia di chiavi vengono automaticamente create relazioni.

     ![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

Nel browser verrà visualizzato il nuovo modello. A questo punto è possibile:   

- Dati del modello di query trascinando campi toohello query della finestra di progettazione e l'aggiunta di filtri.
- Creare nuove misure nelle tabelle.
- Modificare i metadati del modello utilizzando l'editor json hello.
- Aprire il modello di hello in Visual Studio (SSDT), Power BI Desktop o Excel.

![Selezionare Viste e tabelle](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Quando si modificano i metadati del modello o creare nuove misure nel browser, salvato del modello tooyour tali modifiche in Azure. Se si stanno eseguendo operazioni sul modello anche in SSDT, Power BI Desktop o Excel, è possibile che il modello non venga sincronizzato.


## <a name="next-steps"></a>Passaggi successivi 
[Gestire ruoli e utenti del database](analysis-services-database-users.md)  
[Stabilire la connessione con Excel](analysis-services-connect-excel.md)  


