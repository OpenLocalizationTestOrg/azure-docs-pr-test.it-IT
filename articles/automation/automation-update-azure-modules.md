---
title: aaaUpdate Azure i moduli in automazione di Azure | Documenti Microsoft
description: "L'articolo descrive in che modo è ora possibile aggiornare i moduli di Azure PowerShell comuni disponibili per impostazione predefinita in Automazione di Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Come i moduli di Azure PowerShell tooupdate in automazione di Azure

i moduli di PowerShell di Azure più comuni di Hello vengono forniti per impostazione predefinita in ogni account di automazione.  gli aggiornamenti di Azure team Hello hello moduli di Azure regolarmente, pertanto nell'account di automazione hello è fornire un modo per si moduli hello tooupdate nell'account hello quando sono disponibili dal portale hello nuove versioni.  

Poiché i moduli vengono aggiornati regolarmente per gruppo di prodotti hello, possono verificarsi modifiche con hello incluso cmdlet, che potrebbe compromettere i runbook in base al tipo di hello di modifica, ad esempio la ridenominazione di un parametro o deprecazione di un cmdlet completamente. conseguenze per i runbook e hello tooavoid processi automatizzare, si consiglia di testare e convalidare prima di procedere.  Se non si dispone di un account di automazione dedicato a questo scopo, è consigliabile creare uno in modo da poter testare numerosi scenari diversi e permutazioni durante lo sviluppo di hello i runbook, le modifiche tooiterative aggiunta, come l'aggiornamento di hello Moduli di PowerShell.  Dopo aver applicato le modifiche necessarie vengono convalidati i risultati di hello e procedere con il coordinamento di migrazione hello di tutti i runbook che hanno richiesto la modifica ed eseguire l'aggiornamento hello come descritto di seguito in produzione.     

## <a name="updating-azure-modules"></a>Aggiornamento dei moduli di Azure

1. Nei moduli hello pannello dell'account di automazione sono è un'opzione denominata **i moduli di Azure Update**.  Tale opzione è sempre abilitata.<br><br> ![Opzione di aggiornamento dei moduli di Azure nel pannello Moduli](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Fare clic su **i moduli di Azure Update** e verrà visualizzata una notifica di conferma in cui viene chiesto se si desidera toocontinue.<br><br> ![Notifica di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Fare clic su **Sì** e processo di aggiornamento del modulo hello avrà inizio.  il processo di aggiornamento Hello richiede circa hello tooupdate 15-20 minuti seguenti moduli:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Se i moduli di hello sono già backup toodate, processo hello verrà completata in pochi secondi.  Dopo aver completato il processo di aggiornamento hello si riceverà la notifica.<br><br> ![Stato di aggiornamento dei moduli di Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Quando viene eseguito un nuovo processo pianificato, automazione di Azure utilizzerà i moduli più recenti di hello nell'account di automazione.    

Se si utilizzano i cmdlet da questi moduli PowerShell di Azure nel toomanage runbook Azure le risorse, quindi si desidererà tooperform questo processo di aggiornamento ogni mese o così tooassure che è necessario hello moduli più recenti.

## <a name="next-steps"></a>Passaggi successivi

* toolearn ulteriori informazioni sui moduli di integrazione e come toocreate moduli personalizzati toofurther integrare automazione con altri sistemi, servizi o soluzioni, vedere [moduli di integrazione](automation-integration-modules.md).

* Considerare l'utilizzo di integrazione controllo origine [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) o [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gestire e controllare le versioni del portafoglio automazione di runbook e la configurazione.  
