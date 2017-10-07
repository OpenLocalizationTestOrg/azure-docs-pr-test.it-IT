---
title: 'Backup di Azure: backup coerente con le applicazioni di VM Linux | Microsoft Docs'
description: Utilizzare gli script tooguarantee backup coerenti con l'applicazione tooAzure, per le macchine virtuali Linux. gli script di Hello si applicano solo le macchine virtuali tooLinux in una distribuzione di gestione delle risorse; gli script Hello non si applicano tooWindows macchine virtuali o le distribuzioni di service manager. In questo articolo illustra i passaggi di hello per la configurazione script hello, tra cui la risoluzione dei problemi.
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: backup coerente delle app; backup coerente delle applicazioni di VM di Azure; backup di VM Linux; Backup di Azure
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Backup coerente con le applicazioni di VM Linux di Azure (anteprima)

In questo articolo parla hello pre-script di Linux e post-script di framework e come può essere utilizzato tootake backup coerenti con l'applicazione di macchine virtuali Linux di Azure.

> [!Note]
> il framework di pre- script di e post-Hello è supportato solo per le macchine virtuali Linux distribuite di gestione risorse di Azure. Gli script per la coerenza con l'applicazione non sono supportati per le macchine virtuali distribuite di Service Manager o le macchine virtuali di Windows.
>

## <a name="how-hello-framework-works"></a>Funzionamento di framework hello

framework Hello fornisce un'opzione toorun personalizzato pre- script e post-script durante la scrittura delle snapshot macchina virtuale. Gli pre-script di vengono eseguiti solo prima di creare snapshot VM hello e post script vengono eseguiti immediatamente dopo l'esecuzione di snapshot di macchina virtuale hello. In questo modo si hello flessibilità toocontrol dell'applicazione e l'ambiente durante la scrittura delle snapshot macchina virtuale.

In questo scenario, è importante tooensure backup di VM coerenti con l'applicazione. pre-script di Hello può richiamare applicazione nativa API tooquiesce hello IOs e scaricamento su disco toohello contenuto in memoria. In questo modo si garantisce che snapshot hello è coerente con l'applicazione (vale a dire che un'applicazione hello arriva quando post-ripristino hello VM è avviato). Post-script di può essere utilizzato toothaw hello, IOs. Ciò avviene tramite le API dell'applicazione nativa in modo che un'applicazione hello possibile riprendere le normali operazioni post-snapshot della macchina virtuale.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Passaggi tooconfigure pre- script di e post-

1. Accedere in hello radice utente toohello VM Linux che si desidera ripristinare tooback.

2. Scaricare **VMSnapshotScriptPluginConfig.json** da [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)e quindi copiarlo toohello **/e così via/azure** cartella tutte le macchine virtuali hello eseguirai tooback backup. Creare hello **/e così via/azure** directory se non esiste già.

3. Copiare hello pre- script di e post-per l'applicazione su hello tutte le macchine virtuali che si prevede di tooback backup. È possibile copiare hello script tooany percorso hello macchina virtuale. Essere percorso completo di hello tooupdate assicurarsi di hello file di script in hello **VMSnapshotScriptPluginConfig.json** file.

4. Assicurarsi che queste autorizzazioni per questi file hello:

   - **VMSnapshotScriptPluginConfig.json**: autorizzazione "600". Ad esempio, solo l'utente "root" deve avere file toothis di autorizzazioni "lettura" e "scrittura", e nessun utente deve disporre di autorizzazioni "Esegui".

   - **File script di pre-backup**: autorizzazione "700".  Ad esempio, è necessario solo l'utente "root" "lettura", "scrittura" ed "eseguire" file toothis di autorizzazioni.
  
   - **Script di post-backup**: autorizzazione "700". Ad esempio, è necessario solo l'utente "root" "lettura", "scrittura" ed "eseguire" file toothis di autorizzazioni.

   > [!Important]
   > framework Hello offre agli utenti un potente. È importante che è protetta e tale utente "root" solo con i file JSON e script toocritical di accesso.
   > Se non sono soddisfatti i requisiti precedenti hello, hello script non viene eseguito. In questo modo si genera un backup coerente con file system e arresto anomalo.
   >

5. Configurare **VMSnapshotScriptPluginConfig.json** come illustrato di seguito:
    - **pluginName**: lasciare invariato il campo, altrimenti gli script potrebbero non funzionare come previsto.

    - **preScriptLocation**: fornire il percorso completo di hello dello pre-script di hello in hello VM toobe corso che il backup.

    - **postScriptLocation**: fornire il percorso completo di hello dello post-script di hello in hello VM toobe corso che il backup.

    - **preScriptParams**: specificare i parametri facoltativi hello necessarie toobe passato toohello pre script di. Tutti i parametri devono essere racchiusi tra virgolette e, se sono presenti più parametri, devono essere separati da virgole.

    - **postScriptParams**: fornire parametri facoltativi hello necessarie toobe passato post-script toohello. Tutti i parametri devono essere racchiusi tra virgolette e, se sono presenti più parametri, devono essere separati da virgole.

    - **preScriptNoOfRetries**: impostare il numero di hello di tentativi di esecuzione dello pre-script di hello se si verifica un errore prima della chiusura. Zero indica un solo tentativo, senza alcun nuovo tentativo in caso di errore.

    - **postScriptNoOfRetries**: impostare il numero di hello di tentativi di esecuzione dello post-script di hello se si verifica un errore prima della chiusura. Zero indica un solo tentativo, senza alcun nuovo tentativo in caso di errore.
    
    - **timeoutInSeconds**: specificare i singoli timeout per gli pre-script di hello e post-script di hello.

    - **continueBackupOnFailure**: impostare questo valore troppo**true** se si desidera Azure Backup toofall tooa indietro coerente un arresto anomalo di coerente/backup del file system, se uno pre- script di o post-script ha esito negativo. L'impostazione troppo**false** hello backup in caso di errore di script (tranne quando si dispone di VM disco singolo che rientra nuovamente toocrash coerente backup indipendentemente da questa impostazione) ha esito negativo.

    - **fsFreezeEnabled**: specificare se fsfreeze Linux deve essere chiamato durante la scrittura delle coerenza del hello VM snapshot tooensure file system. È consigliabile mantenere questa impostazione troppo**true** , a meno che l'applicazione presenta una dipendenza sulla disattivazione fsfreeze.

6. il framework di script Hello è ora configurato. Se il backup di VM hello è già configurato, backup successivo hello richiama script hello e attiva backup coerenti con l'applicazione. Se non è configurato il backup di VM hello, configurare utilizzando [gli insiemi di credenziali di macchine virtuali di Azure tooRecovery servizi di backup.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Risoluzione dei problemi

Assicurarsi che aggiungere la registrazione appropriata durante la scrittura di pre- script di e post- script di e, esaminare gli eventuali problemi di script del toofix i registri di script. Se continuano a verificarsi problemi di esecuzione di script, fare riferimento toohello per ulteriori informazioni nella tabella seguente.

| Errore | Messaggio di errore | Azione consigliata |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |pre-script di Hello ha restituito un errore, in modo backup potrebbe non essere coerenti con l'applicazione. | Esaminare i registri errori hello relativi al problema di hello toofix script.|  
|   Post-ScriptExecutionFailed |    post-script di Hello ha restituito un errore che potrebbe influire sullo stato dell'applicazione. |  Esaminare i registri errori hello relativi al problema di hello toofix script e controllare lo stato dell'applicazione hello. |
| Pre-ScriptNotFound |  Hello pre-script non trovato nel percorso di hello specificato in hello **VMSnapshotScriptPluginConfig.json** file di configurazione. | Verificare che pre-che script sia presente nel percorso specificato nel backup coerenti con l'applicazione hello config file tooensure hello.|
| Post-ScriptNotFound | Hello post-script non è stato trovato nel percorso di hello specificato in hello **VMSnapshotScriptPluginConfig.json** file di configurazione. | Assicurarsi che dopo questo script sono presente nel percorso specificato nel backup coerenti con l'applicazione hello config file tooensure hello.|
| IncorrectPluginhostFile | Hello **Pluginhost** , incluso in hello VmSnapshotLinux estensione, è danneggiato, quindi non è possibile eseguire pre- script di e post-backup hello non saranno coerenti con l'applicazione.   | Disinstallare hello **VmSnapshotLinux** estensione e verranno reinstallati automaticamente con il problema successivo backup toofix hello hello. |
| IncorrectJSONConfigFile | Hello **VMSnapshotScriptPluginConfig.json** file non è corretto, pertanto pre- script e non è possibile eseguire post-script di backup hello non saranno coerenti con l'applicazione. | Scaricare la copia hello da [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) e configurarlo nuovamente. |
| InsufficientPermissionforPre-Script | Per l'esecuzione di script utente "root" deve essere proprietario di hello del file hello e file hello deve disporre di autorizzazioni "700" (ovvero, è necessario solo "proprietario" "lettura" e "scrittura" autorizzazioni "Esegui"). | Verificare che l'utente "root" hello "proprietario" hello del file di script e che solo "proprietario" con "autorizzazioni di lettura", "scrittura", "Esegui". |
| InsufficientPermissionforPost-Script | Per l'esecuzione di script utente root deve essere proprietario di hello del file hello e file hello deve disporre di autorizzazioni "700" (ovvero, è necessario solo "proprietario" "lettura" e "scrittura" autorizzazioni "Esegui"). | Verificare che l'utente "root" hello "proprietario" hello del file di script e che solo "proprietario" con "autorizzazioni di lettura", "scrittura", "Esegui". |
| Pre-ScriptTimeout | Hello l'esecuzione dello pre-script di backup coerenti con l'applicazione hello timeout. | Controllare lo script hello e aumentare il timeout di hello in hello **VMSnapshotScriptPluginConfig.json** file che si trova in **/e così via/azure**. |
| Post-ScriptTimeout | timeout dell'esecuzione di Hello dello post-script di backup coerenti con l'applicazione hello. | Controllare lo script hello e aumentare il timeout di hello in hello **VMSnapshotScriptPluginConfig.json** file che si trova in **/e così via/azure**. |

## <a name="next-steps"></a>Passaggi successivi
[Configurare l'archivio di servizi di ripristino backup tooa VM](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
