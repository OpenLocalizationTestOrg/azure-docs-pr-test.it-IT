---
title: un laboratorio di Azure DevTest Labs aaaCreate | Documenti Microsoft
description: Creare un lab in Azure DevTest Labs per macchine virtuali
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>Creare un lab di sviluppo/test di Azure
Un laboratorio di Azure DevTest Labs è infrastruttura hello che comprende un gruppo di risorse, ad esempio macchine virtuali (VM), che consente una migliore gestione di tali risorse specificando i limiti e quote. In questo articolo illustra hello processo di creazione di un ambiente lab tramite hello portale di Azure.

## <a name="prerequisites"></a>Prerequisiti
toocreate un ambiente lab, è necessario:

* Una sottoscrizione di Azure. toolearn sulle opzioni di acquisto di Azure, vedere [come toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) o [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). È necessario essere proprietari di hello lab hello toocreate di hello sottoscrizione.

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>Passaggi toocreate un laboratorio di Azure DevTest Labs
Hello alla procedura seguente viene illustrato come toouse hello toocreate portale Azure un laboratorio di DevTest Labs di Azure. 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Dal menu principale di hello sul lato sinistro di hello, selezionare **più servizi** (nella parte inferiore di hello dell'elenco di hello).

    ![Opzione di menu Altri servizi](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. Dall'elenco di hello dei servizi disponibili, **DevTest Labs**.
1. In hello **DevTest Labs** pannello seleziona **Aggiungi**.
   
    ![Aggiungere un lab](./media/devtest-lab-create-lab/add-lab-button.png)

1. In hello **creare un laboratorio di DevTest** pannello:
   
    1. Immettere un **nome Lab** per lab nuovo hello.
    2. Seleziona hello **sottoscrizione** tooassociate con lab hello.
    3. Selezionare un **percorso** in cui lab hello toostore.
    4. Selezionare **arresto automatici** toospecify se si desidera tooenable - e definire parametri hello - hello automatica in corso l'arresto delle macchine virtuali del laboratorio di hello tutti. funzionalità di arresto automatici Hello è essenzialmente una funzionalità di riduzione dei costi in base al quale è possibile specificare quando si desidera hello VM tooautomatically essere arrestato. È possibile modificare le impostazioni di arresto automatico dopo la creazione di lab hello seguendo i passaggi di hello descritti nell'articolo hello, [gestire tutti i criteri per un ambiente lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).
    5. Selezionare **tooDashboard Pin** se si desidera creare un collegamento di hello lab tooappear nel dashboard del portale hello.
    6. Selezionare **opzioni di automazione** tooget modelli di gestione risorse di Azure per l'automazione di configurazione. 
    7. Selezionare **Crea**. Dopo aver selezionato **crea**, hello **DevTest Labs** pannello viene visualizzato. È possibile monitorare lo stato di hello del processo di creazione di hello lab, è possibile guardare hello **notifiche** area. Una volta completato, aggiornamento hello pagina toosee hello creato appena lab nell'elenco di hello del lab.  
    
    ![Creare un pannello lab](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato l'ambiente lab, ecco alcuni tooconsider passaggi successivi:

* [Lab tooa accesso sicuro](devtest-lab-add-devtest-user.md).
* [Definire i criteri del lab](devtest-lab-set-lab-policy.md).
* [Creare un modello di lab](devtest-lab-create-template.md).
* [Creare elementi personalizzati per le VM](devtest-lab-artifact-author.md).
* [Aggiungere una macchina virtuale con lab tooa elementi](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).

