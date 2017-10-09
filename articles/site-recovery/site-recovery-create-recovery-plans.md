---
title: aaaCreate i piani di ripristino per il failover e ripristino in Azure Site Recovery | Documenti Microsoft
description: Viene descritto come toocreate e personalizzare i piani di ripristino in Azure Site Recovery, toofail su e ripristinare le macchine virtuali e server fisici
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Creare piani di ripristino


L'articolo contiene informazioni sulla creazione e la personalizzazione dei piani di ripristino in [Azure Site Recovery](site-recovery-overview.md).

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Creare hello toodo piani di ripristino seguente:

* Definire gruppi di computer che eseguono il failover insieme e quindi si avviano contemporaneamente.
* Creare le dipendenze tra i computer raggruppandoli in un gruppo di piano di ripristino. Ad esempio, toofail su e visualizzare una specifica applicazione, si raggruppano le macchine virtuali di hello per l'applicazione in hello stesso gruppo di piano di ripristino.
* Eseguire un failover. È possibile eseguire un failover non pianificato o un test, pianificato, in un piano di ripristino.


## <a name="create-a-recovery-plan"></a>Creare un piano di ripristino

1. Fare clic su **Piani di ripristino** > **Crea piano di ripristino**.
   Specificare un nome per il piano di ripristino di hello e un'origine e destinazione. percorso di origine di Hello deve avere le macchine virtuali che sono abilitate per il failover e ripristino.

    - Per la replica tooVMM VMM, selezionare **tipo di origine** > **VMM**e hello di origine e il server VMM di destinazione. Fare clic su **Hyper-V** toosee cloud protetti.
    - Per VMM tooAzure, selezionare **tipo di origine** > **VMM**.  Server VMM di origine selezionare hello e **Azure** come destinazione di hello.
    - Per Hyper-V replica tooAzure (senza VMM), selezionare **tipo di origine** > **sito Hyper-V**. Sito hello selezionare come origine di hello, e **Azure** come destinazione di hello.
    - Per una VM VMware o fisico locale tooAzure server, selezionare un server di configurazione come origine di hello, e **Azure** come destinazione di hello.
    - Per un piano di ripristino di Azure tooAzure, selezionare una regione di Azure come origine di hello e un'area secondaria di Azure come destinazione di hello. aree di Azure secondario Hello sono che protetti solo le macchine virtuali toowhich.
2. In **selezionare le macchine virtuali**, selezionare le macchine virtuali hello (o gruppo di replica) che si desidera tooadd toohello gruppo predefinito (gruppo 1) nel piano di ripristino hello.

## <a name="customize-and-extend-recovery-plans"></a>Personalizzare ed estendere i piani di ripristino

È possibile personalizzare ed estendere i piani di ripristino:

- **Aggiungere nuovi gruppi**, aggiungere il gruppo predefinito toohello di ripristino aggiuntivi piano gruppi (backup tooseven) e quindi aggiungere ulteriori macchine o replica gruppi toothose gruppi del piano di ripristino. I gruppi sono numerati in ordine di hello in cui viene aggiunta. Una macchina virtuale o un gruppo di replica può essere incluso solo in un gruppo del piano di ripristino.
- **Aggiungere un'azione manuale**: è possibile aggiungere azioni manuali da eseguire prima o dopo un gruppo del piano di ripristino. Quando viene eseguito il piano di ripristino di hello, si ferma in corrispondenza punto hello in corrispondenza del quale è stata inserita azione manuale hello. Una finestra di dialogo viene richiesto che è stata completata l'azione manuale hello toospecify.
- **Aggiungere uno script**: è possibile aggiungere script che vengono eseguiti prima o dopo un gruppo del piano di ripristino. Quando si aggiunge uno script, viene aggiunto un nuovo set di azioni per il gruppo di hello. Ad esempio, è verrà creato un set di passaggi preliminari per gruppo 1 con nome hello: gruppo 1: passaggi preliminari. Tutti i passaggi preliminari verranno elencati in questo set. È possibile aggiungere uno script nel sito primario di hello solo se si dispone di un server VMM distribuito.
- **Aggiungere runbook di Azure**: è possibile estendere i piani di ripristino con i runbook di Azure. Ad esempio, tooautomate attività o il ripristino di passo-passo toocreate. [Altre informazioni](site-recovery-runbook-automation.md)

## <a name="add-scripts"></a>Aggiungere script

È possibile usare gli script di PowerShell nei piani di ripristino.

 - Verificare che gli script utilizzano blocchi try-catch in modo che hello eccezioni vengono gestite normalmente.
    - Se si verifica un'eccezione nello script hello, arresta l'esecuzione e attività hello viene indicata come non riuscita.
    - Se si verifica un errore, non viene eseguita qualsiasi parte rimanente dello script hello.
    - Se si verifica un errore quando si esegue un failover non pianificato, il piano di ripristino hello continua.
    - Se si verifica un errore quando si esegue un failover pianificato, il piano di ripristino hello arresta. È necessario toofix hello script, verificare che il funzionamento sia quello previsto e quindi eseguire di nuovo piano di ripristino di hello.
- comando Write-Host Hello non funziona in uno script di piano di ripristino e hello script avrà esito negativo. l'output di toocreate, creare uno script proxy che a sua volta esegue lo script principale. Assicurarsi che tutto l'output viene reindirizzato tramite hello >> comando.
  * Timeout script Hello se non viene restituito all'interno di 600 secondi.
  * Se scritto tooSTDERR, lo script di hello viene classificato come non riuscita. Queste informazioni vengono visualizzate nei dettagli di esecuzione di script hello.

Se si usa VMM nella distribuzione:

* Gli script in un piano di ripristino eseguite nel contesto di hello di hello account del servizio VMM. Verificare che l'account disponga delle autorizzazioni di lettura per la condivisione di hello remoto in cui hello script si trova. Test hello toorun di script a livello di privilegi di account del servizio VMM hello.
* I cmdlet di VMM vengono forniti in un modulo di Windows PowerShell. modulo Hello viene installato quando si installa la console di VMM hello. Può essere caricato nello script, hello comando nello script hello seguente:
   - Import-Module -Name virtualmachinemanager. [Altre informazioni](https://technet.microsoft.com/library/hh875013.aspx).
* Assicurarsi di disporre di almeno un server di libreria nella distribuzione di VMM. Per impostazione predefinita, percorso di condivisione di libreria hello per un server VMM si trova in locale nel server VMM, con il nome di cartella hello MSCVMMLibrary hello.
    * Se il percorso della condivisione di libreria è remoto (o locale, ma non condiviso con MSCVMMLibrary), configurare una condivisione di hello come segue (utilizzando \\libserver2.contoso.com\share\ come esempio):
      * Aprire l'Editor del Registro di sistema hello e passare troppo**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure sito Recovery\Registration**.
      * Modificare il valore di hello **ScriptLibraryPath** e inserirlo come \\libserver2.contoso.com\share\. Specificare hello FQDN completo. Fornire il percorso della condivisione toohello di autorizzazioni.
      * Assicurarsi di testare lo script hello con un account utente che ha hello stesso account del servizio autorizzazioni come hello VMM. Verifica che autonomi testati gli script eseguiti hello stesso modo come vengono riprodotti in piani di ripristino. Nel server VMM, hello impostare hello esecuzione criteri toobypass come segue:
        * Aprire la console di Windows PowerShell a 64 bit hello con privilegi elevati.
        * Digitare: **Set-executionpolicy bypass**. [Altre informazioni](https://technet.microsoft.com/library/ee176961.aspx)

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Aggiungere uno script o un piano di azione manuale tooa

Dopo aver aggiunto le macchine virtuali o tooit di gruppi di replica e il piano di hello creato, è possibile aggiungere un gruppo piano di ripristino di uno script toohello predefinito.

1. Piano di ripristino hello aperto.
2. Fare clic su un elemento hello **passaggio** elenco e quindi fare clic su **Script** o **azione manuale**.
3. Specificare se uno script di hello tooadd toowant o azione prima o dopo hello elemento selezionato. Hello utilizzare **Sposta su** e **Sposta giù** pulsanti, posizione hello toomove dello script hello verso l'alto o verso il basso.
4. Se si aggiunge uno script VMM, selezionare **Failover tooVMM script**. In **percorso dello Script**, condivisione toohello di tipo hello percorso relativo. Nell'esempio VMM hello seguente, specificare il percorso di hello: **\rpscripts\rpscript.ps1.**.
5. Se si aggiunge un'automazione di Azure esegue libro, specificare l'account di automazione di Azure hello in cui hello runbook è lo script del runbook di Azure appropriato hello individuare e selezionare.
6. Eseguire un failover del piano di ripristino hello, toomake che hello script funzioni come previsto.


### <a name="add-a-vmm-script"></a>Aggiungere uno script VMM

Se si dispone di un sito di origine VMM, si può creare uno script nel server VMM hello e includerla nel piano di ripristino.

1. Creare una nuova cartella nella condivisione di libreria hello. Ad esempio, \<VMMServerName>\MSSCVMMLibrary\RPScripts. Posizionarlo su origine hello e i server VMM di destinazione.
2. Creare script hello (ad esempio RPScript) e verificare che funzioni come previsto.
3. Posizionare script hello in posizione hello \<VMMServerName > \MSSCVMMLibrary, nei server VMM di origine e destinazione di hello.


## <a name="next-steps"></a>Passaggi successivi

[Altre informazioni](site-recovery-failover.md) sull'esecuzione dei failover.
