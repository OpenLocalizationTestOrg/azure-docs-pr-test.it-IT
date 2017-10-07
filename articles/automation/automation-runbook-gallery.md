---
title: le raccolte di aaaRunbook e modulo per l'automazione di Azure | Documenti Microsoft
description: I runbook e moduli dalla community di Microsoft e hello sono disponibili per si tooinstall e utilizzano nell'ambiente di automazione di Azure.  In questo articolo viene illustrato come accedere queste risorse e toocontribute toohello runbook nella raccolta.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Raccolte di runbook e moduli per l'automazione di Azure
Anziché creare runbook e moduli personalizzati in automazione di Azure, è possibile accedere a un'ampia gamma di scenari in cui siano già stati compilati dalla community di Microsoft e hello.  Questi scenari possono essere usati senza alcuna modifica oppure possono essere utilizzati come punto di partenza apportando tutte le modifiche necessarie in base alle specifiche esigenze.

È possibile ottenere i runbook da hello [raccolta Runbook](#runbooks-in-runbook-gallery) e i moduli da hello [PowerShell Gallery](#modules-in-powerShell-gallery).  È anche possibile contribuire toohello community condividendo scenari che si sviluppano.

## <a name="runbooks-in-runbook-gallery"></a>Runbook nella raccolta di runbook
Hello [raccolta Runbook](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) offre un'ampia gamma di runbook dalla community di Microsoft e hello che è possibile importare in automazione di Azure. È possibile scaricare i runbook dalla raccolta hello che è ospitata in hello [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), oppure è possibile importare direttamente i runbook dalla raccolta hello dal portale di Azure classico hello o il portale di Azure.

È possibile importare solo direttamente dalla raccolta di Runbook hello mediante hello portale di Azure classico o il portale di Azure. Non è possibile eseguire questa funzione tramite Windows PowerShell.

> [!NOTE]
> È consigliabile convalidare il contenuto di hello di qualsiasi runbook ottenuto dalla raccolta di Runbook hello e usare estrema cautela nell'installazione e ad eseguirli in un ambiente di produzione. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport un runbook da hello raccolta di Runbook con hello portale di Azure classico
1. Nel portale di Azure, hello fare clic su, **New**, **servizi App**, **automazione**, **Runbook**, **dalla raccolta**.
2. Selezionare una categoria di tooview runbook correlati e selezionare i dettagli di tooview un runbook. Quando si seleziona il runbook hello desiderato, fare clic sulla freccia destra hello.
   
    ![raccolta di runbook](media/automation-runbook-gallery/runbook-gallery.png)
3. Esaminare il contenuto di hello di hello runbook e prendere nota di eventuali requisiti nella descrizione hello. Al termine, fare clic su pulsante freccia destra hello.
4. Immettere i dettagli di runbook hello e quindi sul pulsante hello segno di spunta. nome del runbook Hello sarà già inserito.
5. Hello runbook verrà visualizzato nella hello **runbook** scheda hello Account di automazione.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport un runbook da hello raccolta di Runbook con hello portale di Azure
1. Nel portale di Azure hello, aprire l'account di automazione.
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.
3. Fare clic sul pulsante **Sfoglia raccolta** .
   
    ![Pulsante Sfoglia raccolta](media/automation-runbook-gallery/browse-gallery-button.png)
4. Individuare l'elemento della raccolta hello desiderato e selezionarlo tooview i dettagli.
   
    ![Sfoglia raccolta](media/automation-runbook-gallery/browse-gallery.png)
5. Fare clic su **progetto origine vista** tooview elemento hello hello [TechNet Script Center](http://gallery.technet.microsoft.com/).
6. tooimport un elemento, fare clic su di esso tooview i dettagli e quindi fare clic su hello **importazione** pulsante.
   
    ![Pulsante Importa](media/automation-runbook-gallery/gallery-item-detail.png)
7. Facoltativamente, modificare il nome di hello di hello runbook e quindi fare clic su **OK** tooimport hello runbook.
8. Hello runbook verrà visualizzato nella hello **runbook** scheda hello Account di automazione.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Aggiunta di una raccolta di runbook toohello runbook
Microsoft incoraggia gli utenti tooadd runbook toohello raccolta di Runbook che si ritengono utili tooother clienti.  È possibile aggiungere un runbook da [caricarli toohello Script Center](http://gallery.technet.microsoft.com/site/upload) tenendo hello account seguenti dettagli.

* È necessario specificare *Windows Azure* per hello **categoria** e *automazione* per hello **Subcategory** per hello runbook toobe visualizzato Nella procedura guidata hello.  
* caricamento di Hello deve essere un singolo file con estensione ps1 o graphrunbook.  Se runbook hello richiede tutti i moduli, runbook figlio o asset, è necessario elencare quelle nella descrizione hello dell'invio hello e nella sezione commenti hello hello runbook.  Se si dispone di uno scenario che richiedono più runbook, quindi caricare ogni separatamente e nomi di hello elenco di hello correlati i runbook in ciascuna delle relative descrizioni. Assicurarsi di utilizzare di hello stesso tag in modo che verranno visualizzati in hello stessa categoria. Un utente abbia tooread hello descrizione tooknow che altri runbook sono necessari hello scenario toowork.
* Aggiungere tag hello "GraphicalPS" Se si pubblica un **runbook grafico** (non un flusso di lavoro con interfaccia grafica). 
* Inserire il frammento di codice del flusso di lavoro di PowerShell o PowerShell in hello descrizione utilizzando **inserire codice sezione** icona.
* Hello riepilogo per il caricamento di hello verrà visualizzato nella raccolta di Runbook risultante, pertanto è necessario fornire informazioni dettagliate che consentano a un utente di identificare funzionalità hello di runbook hello hello.
* È necessario assegnare uno toothree di hello dopo il caricamento di toohello tag.  Hello runbook verranno elencati nella procedura guidata hello in categorie hello corrispondenti ai tag specificati.  Qualsiasi tag non presenti in questo elenco verrà ignorato dalla procedura guidata hello. Se non si specifica alcun tag corrispondente, hello runbook sarà elencato in hello altra categoria.
  
  * Backup
  * Capacity Management
  * Controllo modifiche
  * Conformità
  * Ambiente di testing/sviluppo
  * Ripristino di emergenza
  * Monitoraggio
  * Applicazione di patch
  * Provisioning
  * Correzione
  * Gestione del ciclo di vita VM
* Automazione Aggiorna hello raccolta una volta all'ora, pertanto non verrà visualizzato immediatamente i contributi.

## <a name="modules-in-powershell-gallery"></a>Moduli in PowerShell Gallery
I moduli di PowerShell contengono cmdlet che è possibile utilizzare dei runbook e moduli esistenti che è possibile installare in automazione di Azure sono disponibili in hello [PowerShell Gallery](http://www.powershellgallery.com).  È possibile avviare la raccolta dal portale di Azure hello e installarli direttamente in automazione di Azure oppure è possibile scaricarli e installarli manualmente.  È possibile installare i moduli di hello direttamente dal portale di Azure classico hello, ma è possibile scaricarli installarli come si farebbe con qualsiasi altro modulo.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport un modulo da hello raccolta di moduli di automazione con hello portale di Azure
1. Nel portale di Azure hello, aprire l'account di automazione.
2. Fare clic su hello **asset** riquadro tooopen hello elenco degli asset.
3. Fare clic su hello **moduli** riquadro tooopen hello elenco dei moduli.
4. Fare clic su hello **Sfoglia raccolta** Pannello di raccolta hello e pulsante Sfoglia viene avviata.
   
    ![Raccolta di moduli](media/automation-runbook-gallery/modules-blade.png) <br>
5. Dopo aver avviato Pannello di hello Sfoglia raccolta, è possibile cercare per hello seguenti campi:
   
   * Nome modulo
   * Tag
   * Autore
   * Nome della risorsa cmdlet/DSC
6. Individuare un modulo che si è interessati e selezionarlo tooview i dettagli.  
   Quando si analizza un modulo specifico, è possibile visualizzare ulteriori informazioni sul modulo hello, incluso un toohello indietro collegamento PowerShell Gallery, le dipendenze di richieste e contiene tutti i cmdlet di hello e/o le risorse DSC che hello modulo.
   
    ![Informazioni sul modulo di PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. modulo hello tooinstall direttamente in automazione di Azure, fare clic su hello **importazione** pulsante.
   
    ![Pulsante Importa modulo](media/automation-runbook-gallery/module-import-button.png)
8. Quando si fa clic sul pulsante Importa hello, si noterà nome del modulo che si sta tooimport hello. Se vengono installate tutte le dipendenze di hello, hello **OK** pulsante sarà attivo. Se non sono presenti dipendenze, è necessario tooimport quelli prima di poter importare questo modulo.
9. Fare clic su **OK** tooimport hello modulo e blade modulo hello verrà avviato. Quando un account tooyour modulo di importazione di automazione di Azure, estrae i metadati relativi al modulo hello e i cmdlet di hello.
   
    ![Pannello Importa modulo](media/automation-runbook-gallery/module-import-blade.png)
   
    Poiché ogni attività deve toobe estratto, l'operazione potrebbe richiedere alcuni minuti.
10. Si riceverà una notifica viene distribuito il modulo hello e una notifica quando è stata completata.
11. Dopo aver importato il modulo di hello, si noterà che le attività disponibili hello ed è possibile utilizzare le risorse nel runbook e configurazione dello stato desiderato.

## <a name="requesting-a-runbook-or-module"></a>Richiesta di un runbook o un modulo
È possibile inviare richieste troppo[Uservoice](https://feedback.azure.com/forums/246290-azure-automation/).  Per assistenza nella scrittura di un runbook o domande su PowerShell, registrare un tooour domanda [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md)
* differenze di hello toounderstand tra PowerShell e del flusso di lavoro di PowerShell con i runbook, vedere [flusso di lavoro PowerShell di apprendimento](automation-powershell-workflow.md)

