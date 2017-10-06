---
title: un server Analysis Services in Azure aaaCreate | Documenti Microsoft
description: Informazioni su come istanza di un server Analysis Services toocreate in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Creare un server Azure Analysis Services nel portale di Azure
Questo articolo illustra la creazione di una risorsa server Analysis Services nella sottoscrizione di Azure.

## <a name="before-you-begin"></a>Prima di iniziare
toocomplete questa Guida rapida, è necessario:

* **Sottoscrizione di Azure**: visitare [versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un account.
* **Azure Active Directory**: la sottoscrizione deve essere associata a un tenant Azure Active Directory. E, è necessario toobe connessi tooAzure con un account in Azure Active Directory. Gli account Microsoft non sono supportati. vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).
* **Gruppo di risorse**: usare un gruppo di risorse già esistente o [crearne uno nuovo](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> La creazione di un server può avere come risultato un nuovo servizio fatturabile. vedere, più toolearn [dei prezzi di Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate un server nel portale di Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com).  
2. Fare clic su **+ Nuovo** > **Dati e analisi** > **Analysis Services**.
3. In hello **Analysis Services** pannello, compilare i campi di hello necessarie e quindi premere **crea**.
   
    ![Creazione del server](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nome del server**: tipo di server di hello tooreference un nome univoco utilizzato.
   * **Sottoscrizione**: selezionare questo server attivi per sottoscrizione di hello.
   * **Gruppo di risorse**: questi contenitori fanno toohelp progettato gestire una raccolta di risorse di Azure. vedere, più toolearn [gruppi di risorse](../azure-resource-manager/resource-group-overview.md).
   * **Percorso**: hello di host posizione Data Center di Azure questo server. Selezionare una località vicina alla base di utenti più estesa.
   * **Piano tariffario**: selezionare un piano tariffario. Sono supportati i modelli tabulari too400 GB. vedere, più toolearn [dei prezzi di Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Fare clic su **Crea**.

La creazione richiede in genere meno di un minuto e spesso solo alcuni secondi. Se si seleziona **aggiungere tooPortal**, passare toosee portale tooyour il nuovo server. In alternativa, passare troppo**più servizi** > **Analysis Services** toosee se il server è pronto.

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il server, è possibile [distribuire un modello](analysis-services-deploy.md) tooit mediante SSDT o con SQL Server Management Studio.

Se un modello di distribuzione tooyour server si connette a origini dati locali tooon, è necessario tooinstall un [gateway dati locale](analysis-services-gateway.md) in un computer nella rete.

