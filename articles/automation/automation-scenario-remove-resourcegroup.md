---
title: aaaAutomate la rimozione di gruppi di risorse | Documenti Microsoft
description: Versione del flusso di lavoro di PowerShell di uno scenario di automazione di Azure, inclusi i runbook tooremove gruppi di tutte le risorse nella sottoscrizione.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Scenario di Automazione di Azure: automatizzare la rimozione di gruppi di risorse
Molti clienti creano più gruppi di risorse. Alcuni potrebbero essere usati per gestire applicazioni di produzione e altri come ambienti di sviluppo, test e staging. L'automatizzazione della distribuzione hello di queste risorse è un aspetto, ma la toodecommission in grado di un gruppo di risorse con un clic del pulsante hello è un altro. È possibile semplificare questa comune attività di gestione con Automazione di Azure. Questo è utile se si lavora con una sottoscrizione di Azure che ha un limite di spesa tramite un'offerta di membro come MSDN o il programma Microsoft Partner Network Cloud Essentials hello.

Questo scenario è basato su un runbook PowerShell ed è progettato tooremove uno o più gruppi di risorse specificato dalla sottoscrizione. impostazione predefinita Hello runbook hello è tootest prima di procedere. In questo modo si garantisce che non eliminate accidentalmente il gruppo di risorse hello prima si è pronti toocomplete questa procedura.   

## <a name="getting-hello-scenario"></a>Scenario di recupero hello
Questo scenario è costituito da un runbook di PowerShell che è possibile scaricare da hello [PowerShell Gallery](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). È possibile anche importare direttamente da hello [raccolta Runbook](automation-runbook-gallery.md) in hello portale di Azure.<br><br>

| Runbook | Descrizione |
| --- | --- |
| Remove-ResourceGroup |Rimuove uno o più gruppi di risorse di Azure e le risorse associate dalla sottoscrizione hello. |

<br>
Hello seguenti parametri di input definito per questo runbook:

| . | Descrizione |
| --- | --- |
| NameFilter (obbligatorio) |Specifica un nome filtro toolimit hello gruppi di risorse che si prevede l'eliminazione. È possibile passare più valori usando un elenco delimitato da virgole.<br>filtro di Hello non è tra maiuscole e minuscole e corrisponderà a qualsiasi gruppo di risorse che contiene la stringa hello. |
| PreviewMode (facoltativo) |Esegue hello runbook toosee quali gruppi di risorse verranno eliminati, ma non esegue alcuna azione.<br>valore predefinito di Hello è **true** toohelp evitare l'eliminazione accidentale di uno o più gruppi di risorse passato toohello runbook. |

## <a name="install-and-configure-this-scenario"></a>Installare e configurare lo scenario
### <a name="prerequisites"></a>Prerequisiti
Questo runbook viene autenticato mediante hello [account RunAs di Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Installare e pubblicare i runbook hello
Dopo aver scaricato hello runbook, è possibile importare tramite la procedura hello in [l'importazione di runbook procedure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Pubblicare il runbook hello dopo essere stato importato correttamente nell'account di automazione.

## <a name="using-hello-runbook"></a>Utilizzo di runbook hello
Hello passaggi seguenti verranno illustrati esecuzione hello di questo runbook e la Guida che è acquisire familiarità con il funzionamento. Si verrà solo test hello runbook in questo esempio, non effettivamente eliminazione gruppo di risorse hello.  

1. Hello portale di Azure, aprire l'account di automazione e fare clic su **runbook**.
2. Seleziona hello **Rimuovi gruppo di risorse** runbook e fare clic su **avviare**.
3. Quando si avvia runbook hello, hello **avvia Runbook** pannello viene aperto ed è possibile configurare i parametri di hello. Immettere i nomi di hello di gruppi di risorse nella sottoscrizione che è possibile utilizzare per il testing e non genererà causa problemi se accidentalmente eliminato.<br> ![Parametri di Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Assicurarsi che **Previewmode** è troppo**true** tooavoid eliminazione hello selezionato di gruppi di risorse.  **Nota** questo runbook non rimuoverà i gruppo di risorse hello che contiene account di automazione hello che è in esecuzione il runbook.  
   >
   >
4. Dopo aver configurato tutti i valori di parametro hello, fare clic su **OK**, e hello runbook verranno accodate per l'esecuzione.  

dettagli di hello tooview di hello **Rimuovi gruppo di risorse** processo del runbook nel portale di Azure selezionare hello **processi** hello runbook. flusso inoltre Hello processo Visualizza riepilogo hello i parametri di input e output di hello toogeneral informazioni processo hello e tutte le eccezioni che si è verificato.<br> ![Stato del processo del runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png)

Hello **riepilogo** include i messaggi da flussi di errore, avviso e di output di hello. Selezionare **Output** tooview dettagliate dei risultati dell'esecuzione di runbook hello.<br> ![Risultati di output del runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Passaggi successivi
* tooget cominciare a creare runbook, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md).
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il runbook del flusso di lavoro di PowerShell prima](automation-first-runbook-textual.md).
