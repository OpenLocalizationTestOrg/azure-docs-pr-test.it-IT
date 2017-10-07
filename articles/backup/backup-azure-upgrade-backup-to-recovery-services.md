---
title: aaaUpgrade un archivio di Backup dell'insieme di credenziali tooa servizi di ripristino (anteprima) | Documenti Microsoft
description: Istruzioni e tooupgrade informazioni di supporto di Backup di Azure insieme di credenziali tooa insieme di credenziali di servizi di ripristino.
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>L'aggiornamento di un archivio di servizi di ripristino di Backup dell'insieme di credenziali tooa

In questo articolo viene illustrato come un insieme di credenziali di Backup tooupgrade tooa servizi di ripristino dell'insieme di credenziali. processo di aggiornamento Hello non avere alcun impatto tutti i processi di backup in esecuzione e non i dati di backup vanno persi. Hello primario motivi tooupgrade un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino:
- Tutte le funzionalità di un insieme di credenziali di Backup vengono mantenute in un insieme di credenziali di Servizi di ripristino.
- Gli insiemi di credenziali di Servizi di ripristino offrono maggiori funzionalità rispetto agli insiemi di credenziali di Backup, tra cui una migliore protezione, un monitoraggio integrato, ripristini più veloci e ripristini a livello di elemento.
- È anche possibile gestire gli elementi di backup da un portale migliorato e semplificato.
- Nuove funzionalità sono valide solo gli insiemi di credenziali di tooRecovery servizi.

## <a name="impact-toooperations-during-upgrade"></a>Impatto toooperations durante l'aggiornamento

Quando si aggiorna un archivio di servizi di ripristino di Backup dell'insieme di credenziali tooa, non vi è alcun impatto tooyour dati piano operazioni. Tutti i processi di backup continuano come al solito e i processi di ripristino attivi continuano senza interruzioni. Durante l'aggiornamento di hello, operazioni di gestione comportano un breve periodo di inattività, e non è possibile proteggere gli elementi nuovi o creazione di processi di backup ad hoc. Durante l'aggiornamento di hello non vengono eseguiti i processi di ripristino per le macchine virtuali IaaS. aggiornamento dell'insieme di credenziali Hello accetta in toocomplete un'ora. Una volta terminato, un insieme di credenziali di servizi di ripristino sostituisce l'insieme di credenziali Backup hello.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Strumento dopo l'aggiornamento e le modifiche tooyour automazione

Durante la preparazione dell'infrastruttura per l'aggiornamento dell'insieme di credenziali di hello, è necessario aggiornare l'automazione esistente o gli strumenti tooensure che continua toowork dopo l'aggiornamento di hello.
Consultare i riferimenti cmdlet PowerShell di hello hello [il modello di distribuzione di Service Manager](backup-client-automation-classic.md) hello e [il modello di distribuzione di gestione risorse](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Prima dell'aggiornamento

Controllo hello problemi indicati di seguito prima dell'aggiornamento insieme di credenziali di Backup tooRecovery gli insiemi di credenziali del servizio.

- **Versione minima dell'agente**: tooupgrade insieme di credenziali, agente di Microsoft Azure Recovery Services (MARS) verificare che hello è almeno versione 2.0.9070.0. Se l'agente MARS hello è antecedente a 2.0.9070.0, aggiornare agente hello prima di avviare la procedura di aggiornamento hello.
- **Modello di fatturazione basato su istanza**: insiemi di credenziali per il servizio di recupero supportano solo modello di fatturazione basato su istanza hello. Se si dispone di un insieme di credenziali di backup che utilizza hello precedente archiviazione basato su modello di fatturazione, convertire modello di fatturazione hello durante l'aggiornamento.
- **Nessuna operazione di configurazione del backup in corso**: durante l'aggiornamento, piano di gestione toohello di accesso è limitato. Completare tutte le azioni di gestione del piano e quindi avviare l'aggiornamento di hello.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Utilizzando PowerShell script tooupgrade insieme di credenziali

È possibile utilizzare PowerShell script tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup. Verificare che sono hello è richiesto l'aggiornamento dell'insieme di credenziali di PowerShell componenti tootrigger hello. Gli script di PowerShell per gli insiemi di credenziali di Backup non funzionano per gli insiemi di credenziali dei servizi di ripristino. Preparare l'ambiente gli insiemi di credenziali di tooupgrade hello:

1. Installare o aggiornare [tooversion Windows Management Framework (WMF) 5](https://www.microsoft.com/download/details.aspx?id=50395) o versione successiva.
2. [Installare il file MSI di Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Scaricare hello [script di PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade insieme di credenziali.

### <a name="run-hello-powershell-script"></a>Eseguire script PowerShell hello

Lo script seguente hello utilizzare tooupgrade insieme di credenziali. Hello lo script di esempio seguente contiene le spiegazioni dei parametri di hello.

RecoveryServicesVaultUpgrade-1.0.2.ps1 **-SubscriptionID** `<subscriptionID>` **-VaultName** `<vaultname>` **-Location** `<location>` **-ResourceType** `BackupVault` **-TargetResourceGroupName** `<rgname>`

**SubscriptionID** -hello numero ID sottoscrizione dell'insieme di credenziali hello che viene aggiornato.<br/>
**VaultName** : hello nome dell'insieme di credenziali di Backup hello che viene aggiornato.<br/>
**Percorso** -percorso dell'insieme di credenziali hello in corso l'aggiornamento.<br/>
**ResourceType**: usare BackupVault.<br/>
**TargetResourceGroupName** : poiché si sta aggiornando hello insieme di credenziali tooa basate su Gestione risorse di distribuzione, specificare un gruppo di risorse. È possibile usare un gruppo di risorse esistente o crearne uno inserendo un nome nuovo. Se è stato digitato correttamente il nome di hello di un gruppo di risorse, è possibile creare un nuovo gruppo di risorse. toolearn ulteriori informazioni sui gruppi di risorse, leggere questo [panoramica sui gruppi di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> I nomi dei gruppi di risorse hanno dei limiti. Impossibile verificare indicazioni di hello toofollow; Errore toodo così potrebbe causare toofail gli aggiornamenti dell'insieme di credenziali.
>
>

Hello frammento di codice seguente è riportato un esempio di comando quali PowerShell dovrebbe essere simile:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

È anche possibile eseguire script hello senza parametri e viene chiesto tooprovide input per tutti i parametri obbligatori.

Hello script di PowerShell richiesto è tooenter le credenziali. Immettere le credenziali due volte: una volta per l'account di Service Manager hello e una seconda volta per l'account di gestione risorse di hello.

### <a name="pre-requisites-checking"></a>Verifica dei prerequisiti
Dopo aver immesso le credenziali di Azure, Azure controlla che l'ambiente soddisfi i seguenti prerequisiti hello:

- **Versione minima dell'agente** -gli insiemi di credenziali di Backup con l'aggiornamento di insiemi di credenziali tooRecovery Services richiede hello MARS agente toobe almeno versione 2.0.9070. Se dispone di elementi registrato insieme di credenziali Backup tooa precedenti 2.0.9070 con un agente, hello di controllo dei prerequisiti ha esito negativo. Se hello di controllo dei prerequisiti non riesce, aggiornare l'agente di hello e riprovare l'insieme di credenziali tooupgrade hello. È possibile scaricare hello la versione più recente dell'agente di hello dalla [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **I processi di configurazione in corso**: se un utente è la configurazione di processo per un insieme di credenziali di Backup impostato toobe aggiornati oppure registrando un elemento, hello ha esito negativo di controllo dei prerequisiti. Completare la configurazione di hello, o completare la registrazione voce hello e quindi avviare processo di aggiornamento dell'insieme di credenziali di hello.
- **Modello di fatturazione basato su archiviazione**: servizi di ripristino gli insiemi di credenziali supporto hello basato su istanza modello di fatturazione. Se si esegue l'aggiornamento dell'insieme di credenziali hello un insieme di credenziali di Backup che utilizza il modello di fatturazione basato su archiviazione di hello, è richiesta tooupgrade il modello di fatturazione insieme hello insieme di credenziali. In caso contrario, è possibile aggiornare il modello di fatturazione in primo luogo, e quindi eseguire l'aggiornamento dell'insieme di credenziali di hello.
- Identificare un gruppo di risorse per l'insieme di credenziali di servizi di ripristino hello. sfruttare tootake hello funzionalità di distribuzione di gestione delle risorse, è necessario un insieme di credenziali di servizi di ripristino in un gruppo di risorse. Se non si conosce toouse quale gruppo di risorse, fornire che un nome e hello processo di aggiornamento crea hello gruppo di risorse. processo di aggiornamento Hello associa anche l'insieme di credenziali hello con hello nuovo gruppo di risorse.

Una volta al termine del processo di aggiornamento di hello, il controllo prerequisiti hello, il processo di hello richiede si toostart hello insieme di credenziali per l'aggiornamento. Dopo la conferma, processo di aggiornamento hello richiede in genere intorno toocomplete 15-20 minuti, a seconda delle dimensioni di hello dell'insieme di credenziali. Se si dispone di un insieme di credenziali di grandi dimensioni, l'aggiornamento può richiedere too90 minuti.

## <a name="managing-your-recovery-services-vaults"></a>Gestione degli insiemi di credenziali dei servizi di ripristino

Hello schermate seguenti Mostra un nuovo archivio di servizi di ripristino, aggiornato dall'insieme di credenziali di Backup, nel portale di Azure hello. Hello prima schermata dashboard dell'insieme di credenziali hello che consente di visualizzare le entità di chiave per l'insieme di credenziali hello.

![esempio dell'insieme di credenziali di Servizi di ripristino aggiornato da un insieme di credenziali di Backup](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

seconda schermata Hello Mostra i collegamenti della Guida hello toohelp disponibili introduttive sull'uso di servizi di ripristino hello insieme di credenziali.

![nel pannello Guida introduttiva hello collegamenti alla Guida](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Passaggi successivi all'aggiornamento
L'insieme di credenziali di Servizi di ripristino supporta l'indicazione delle informazioni sul fuso orario nei criteri di backup. Dopo che l'insieme di credenziali è stato aggiornato correttamente, andare tooBackup criteri dal menu Impostazioni insieme di credenziali e aggiornare le informazioni sul fuso orario hello per ognuno dei criteri di hello configurati nell'insieme di credenziali hello. In questa schermata viene già tempo di pianificazione del backup hello specificato come per il fuso orario locale utilizzato quando si creano i criteri. 

## <a name="enhanced-security"></a>Sicurezza avanzata

Quando si aggiorna un insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino tooa, hello impostazioni di sicurezza per tale insieme di credenziali vengono automaticamente attivate. Quando le impostazioni di sicurezza hello sono attivi, determinate operazioni, ad esempio l'eliminazione dei backup o la modifica di una passphrase richiede un [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) PIN. Per ulteriori informazioni sulla sicurezza hello avanzato, vedere l'articolo hello [funzionalità di sicurezza per i backup ibrida tooprotect](backup-azure-security-feature.md). 

Quando è attivata sicurezza avanzata di hello, i dati vengono mantenuti i too14 giorni dopo l'eliminazione di informazioni sui punti di ripristino hello dall'insieme di credenziali hello. Ai clienti viene fatturato lo spazio di archiviazione usato per questi dati sulla sicurezza. Conservazione dei dati di sicurezza si applica punti toorecovery impiegati per l'agente Azure Backup hello, Server di Backup di Azure e System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Raccogliere i dati nell'insieme di credenziali

Dopo l'aggiornamento dell'insieme di credenziali di tooa servizi di ripristino, configurare i report per il Backup di Azure (per le macchine virtuali IaaS e Microsoft Azure Recovery Services (MARS)) e utilizzare i report di Power BI tooaccess hello. Per ulteriori informazioni sulla raccolta dei dati, vedere l'articolo hello [configurare Backup di Azure segnala](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Domande frequenti

**Piano di aggiornamento hello interessa i backup in corso?**</br>
No. I backup in corso proseguono senza interruzioni durante e dopo l'aggiornamento.

**Se prevede di non aggiornamento appena, cosa accade toomy gli insiemi di credenziali?**</br>
Poiché tutte le nuove funzionalità sono valide solo tooRecovery servizi gli insiemi di credenziali, utente è invitato è tooupgrade insieme di credenziali. Microsoft infine dichiarerà portale classico hello. A partire dal 1 settembre 2017, Microsoft inizierà l'aggiornamento automatico degli archivi di servizi tooRecovery insiemi di credenziali di backup. Entro il 1 ° novembre 2017 Microsoft completerà processo di aggiornamento hello. L'insieme di credenziali può essere aggiornato automaticamente in qualsiasi momento nei mesi di settembre oppure ottobre. Microsoft consiglia di aggiornare l'insieme di credenziali il prima possibile.

**Qual è l'impatto di questo aggiornamento per gli strumenti esistenti?**</br>
Aggiornare il modello di distribuzione di strumenti toohello Gestione risorse. Servizi di ripristino creati insiemi di credenziali per utilizzano nel modello di distribuzione di gestione risorse di hello. Pianificazione per modello di distribuzione di gestione risorse di hello e accounting per differenza hello nell'insieme di credenziali è importante. 

**Durante l'aggiornamento di hello, è molto tempo di inattività?**</br>
Dipende dal numero di hello di risorse che vengono aggiornati. Per le distribuzioni di dimensioni minori (poche decine di istanze protette), aggiornamento intero hello richiederà meno di 20 minuti. Per distribuzioni di grandi dimensioni, dovrebbe richiedere al massimo un'ora.

**È possibile eseguire il ripristino dello stato precedente dopo l'aggiornamento?**</br>
No. Eseguire il rollback non è supportato dopo risorse hello sono state aggiornate.

**È possibile convalidare il toosee sottoscrizione o le risorse se sono in grado di aggiornamento?**</br>
Sì. Hello innanzitutto l'aggiornamento di convalida che le risorse di hello sono in grado di aggiornamento. Nel caso in cui la convalida di hello di prerequisiti non riesce, si ricevono messaggi per i motivi hello Impossibile completare l'aggiornamento di hello.

**Le autorizzazioni di cui è necessario disporre di aggiornamento dell'insieme di credenziali tootrigger?**</br>
hello tooperform insieme di credenziali di aggiornamento, deve essere aggiunto come coamministratore della sottoscrizione hello in hello portale di Azure classico. Ciò è necessario anche se si sono già presenti come proprietario nel portale di Azure hello. Provare tooadd coamministratore della sottoscrizione hello in Azure toofind portale classico out in caso di coamministratore della sottoscrizione hello. Se non si è in grado di tooadd un coamministratore, contattare l'amministratore del servizio o coamministratore per la sottoscrizione di hello, che è possibile aggiungere come coamministratore.

**È possibile aggiornare l'insieme di credenziali di Backup basato su CSP?**</br>
No. Non è attualmente possibile aggiornare gli insiemi di credenziali di Backup basati su CSP. Verrà aggiunto il supporto per l'aggiornamento di insiemi di credenziali di Backup basato su provider CSP in versioni successiva hello.

**È possibile visualizzare l'insieme di credenziali classico in seguito all'aggiornamento?**</br>
No. Non è possibile visualizzare o gestire l'insieme di credenziali classico in seguito all'aggiornamento. Solo sarà in grado di toouse hello nuovo portale di Azure per tutte le azioni di gestione di archivio hello.

**L'aggiornamento non riuscito, ma macchina hello mantenuto agente hello che richiedono l'aggiornamento, non esiste più. Quali sono le operazioni da eseguire in questo caso?**</br>
Se è necessario archivio hello toouse, hello i backup del computer per la conservazione a lungo termine, quindi non sarà insieme di credenziali in grado di tooupgrade hello. Il supporto per l'aggiornamento di questo tipo di insieme di credenziali verrà aggiunto nelle versioni future.
Se i backup di hello toostore di questo computer non è necessaria più, quindi, annullare la registrazione del computer dall'insieme di credenziali hello e ripetere l'aggiornamento di hello.

**Impossibile visualizzare informazioni sui processi di hello per le risorse locali dopo l'aggiornamento**</br>
Per il monitoraggio locale backup (agente MARS, DPM e i Server di Backup di Azure) è una nuova funzionalità che ottengono quando si aggiorna l'insieme di credenziali servizi di tooRecovery insieme di credenziali di Backup. informazioni sul monitoraggio Hello richiede too12 ore toosync con servizio hello.

**Come si segnala un problema?**</br>
Se qualsiasi parte dell'insieme di credenziali hello esegue l'aggiornamento ha esito negativo, hello nota OperationId elencati nell'errore hello. Supporto Microsoft funzionerà in modo proattivo problema hello tooresolve. È possibile raggiungere tooSupport o Microsoft all'indirizzo di posta elettronica rsvaultupgrade@service.microsoft.com con l'ID sottoscrizione, nome insieme di credenziali e l'ID operazione. Verrà effettuato un tentativo problema hello tooresolve più rapidamente possibile. Non ripetere l'operazione di hello a meno che non richiesto in modo esplicito toodo così da Microsoft.


## <a name="next-steps"></a>Passaggi successivi
Utilizzare hello articolo al seguente:</br>
[Eseguire il backup di una macchina virtuale IaaS](backup-azure-arm-vms-prepare.md)</br>
[Eseguire il backup del server di Backup di Azure](backup-azure-microsoft-azure-backup.md)</br>
[Eseguire il backup di Windows Server](backup-configure-vault.md).
