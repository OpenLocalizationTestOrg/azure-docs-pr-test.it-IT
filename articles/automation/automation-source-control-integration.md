---
title: aaaSource integrazione del controllo in automazione di Azure | Documenti Microsoft
description: Questo articolo descrive l'integrazione del controllo del codice sorgente con GitHub in Automazione di Azure.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integrazione del controllo del codice sorgente in Automazione di Azure
Integrazione del controllo codice sorgente consente tooassociate runbook nel repository del controllo codice sorgente GitHub di automazione account tooa. Controllo del codice sorgente consente tooeasily collaborare con il team, tenere traccia delle modifiche e ripristinare le versioni tooearlier i runbook. Ad esempio, il codice sorgente consente si toosync diversi rami nel controllo del codice sorgente tooyour sviluppo, test o produzione gli account di automazione, rendendo semplice toopromote codice che è stato testato in produzione tooyour ambiente sviluppo automazione account.

Controllo del codice sorgente consente toopush codice dal controllo di automazione di Azure toosource o estrarre i runbook dall'origine controllo tooAzure automazione. Questo articolo descrive come controllare il tooset codice sorgente nell'ambiente di automazione di Azure. Verrà innanzitutto la configurazione di automazione di Azure tooaccess il repository GitHub e analizzerà diverse operazioni che possono essere eseguite utilizzando l'integrazione del controllo codice sorgente. 

> [!NOTE]
> Il controllo del codice sorgente supporta il pull e il push di [Runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) e [Runbook di PowerShell](automation-runbook-types.md#powershell-runbooks). I [Runbook grafici](automation-runbook-types.md#graphical-runbooks) non sono ancora supportati.<br><br>
> 
> 

Esistono due semplici passaggi necessarie tooconfigure controllo del codice sorgente per l'account di automazione e uno solo se si dispone già di un account GitHub. Sono:

## <a name="step-1--create-a-github-repository"></a>Passaggio 1: Creare un repository GitHub
Se si dispone già di un account GitHub e un repository che si desidera toolink tooAzure automazione, quindi esistente tooyour account di accesso dell'account e iniziare dal passaggio 2 di seguito. In caso contrario, passare troppo[GitHub](https://github.com/), effettuare l'iscrizione per un nuovo account e [creare un nuovo repository](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Passaggio 2 - Configurazione del controllo del codice sorgente in Automazione di Azure
1. Dal Pannello di Account di automazione hello in hello portale di Azure, fare clic su **Set di controllo del codice sorgente.** 
   
    ![Impostare il controllo codice sorgente](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Hello **controllo del codice sorgente** pannello viene aperto, in cui è possibile configurare i dettagli dell'account GitHub. Di seguito è elenco hello di tooconfigure parametri:  
   
   | **Parametro** | **Descrizione** |
   |:--- |:--- |
   | Scegliere l'origine |Selezionare l'origine hello. Attualmente è supportato solo **GitHub** . |
   | Authorization |Fare clic su hello **Authorize** del repository di GitHub tooyour pulsante toogrant automazione di Azure l'accesso. Se si è già connessi tooyour account GitHub in un'altra finestra, hello vengono utilizzate credenziali dell'account. Una volta autorizzazione ha esito positivo, il pannello hello verrà visualizzati il nome utente GitHub in **autorizzazione proprietà**. |
   | Scegliere un archivio |Selezionare un repository GitHub hello elenco dei repository disponibili. |
   | Scegliere il ramo |Selezionare un ramo hello elenco di rami disponibili. Solo hello **master** ramo viene visualizzato se non sono stati creati rami. |
   | Percorso della cartella runbook |percorso della cartella runbook Hello Specifica percorso hello nel repository di GitHub hello da cui si desidera toopush o estrarre il codice. Deve essere immesso nel formato hello **/nomecartella/nomesottocartella**. Solo i runbook nel percorso della cartella runbook hello saranno sincronizzati tooyour account di automazione. I runbook in sottocartelle hello hello runbook del percorso della cartella verranno **non** verrà sincronizzato. Utilizzare  **/**  toosync tutti hello runbook nel repository di hello. |
3. Ad esempio, se è disponibile un repository denominato **PowerShellScripts** che contiene una cartella denominata **RootFolder**, che a sua volta contiene una cartella denominata **SubFolder**. È possibile utilizzare hello seguenti stringhe toosync ogni livello di cartella:
   
   1. i runbook toosync **repository**, percorso della cartella runbook*/*
   2. i runbook toosync **RootFolder**, percorso della cartella runbook è */RootFolder della*
   3. i runbook toosync **sottocartella**, percorso della cartella runbook è *RootFolder/sottocartella*.
4. Dopo aver configurato i parametri di hello, vengono visualizzate su hello **Pannello di controllo Set origine.**  
   
    ![Pannello Configura](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Dopo aver fatto clic su OK, l'integrazione del controllo del codice sorgente è ora configurata per l'account di Automazione e deve essere aggiornata con le informazioni su GitHub. È possibile ora fare clic su questo tooview parte tutti di controllo del codice sorgente Cronologia processo di sincronizzazione.  
   
    ![Valori del repository](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Dopo aver impostato il controllo codice sorgente, hello risorse di automazione seguenti verranno create nell'account di automazione:  
   Vengono creati due [asset di tipo variabile](automation-variables.md).  
   
   * variabile Hello **Microsoft.Azure.Automation.SourceControl.Connection** contiene i valori hello della stringa di connessione hello, come illustrato di seguito.  
     
     | **Parametro** | **Valore** |
     |:--- |:--- |
     | Nome |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tipo |String |
     | Valore |{"Branch":\<*Nome del ramo*>,"RunbookFolderPath":\<*Percorso della cartella del runbook*>,"ProviderType":\< *con valore 1 per GitHub*>,"Repository":\<*Nome del repository*>,"Username":\<*Nome utente di GitHub*>} |

    * variabile Hello **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contiene hello valore crittografato protetto del OAuthToken.  

    |**Parametro**            |**Valore** |
    |:---|:---|
    | Nome  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tipo | Unknown(Encrypted) |
    | Valore | <*OAuthToken crittografato*> |  

    ![variables](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Controllo del codice sorgente automazione** viene aggiunto come un account GitHub di tooyour applicazioni autorizzate. un'applicazione hello tooview: dalla home page GitHub, passare tooyour **profilo** > **impostazioni** > **applicazioni**. Questa applicazione consente di automazione di Azure toosync il tooan repository GitHub account di automazione.  

    ![Applicazione Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Uso del controllo del codice sorgente in Automazione
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Controllo in un runbook dal controllo toosource di automazione di Azure
Archiviazione runbook consente toopush hello le modifiche apportate tooa runbook in automazione di Azure nel repository del controllo del codice sorgente. Di seguito sono riportati passaggi hello toocheck-in un runbook:

1. Dall'account di automazione [creare un nuovo runbook testuale](automation-first-runbook-textual.md) o [modificare un runbook testuale esistente](automation-edit-textual-runbook.md). Il runbook può essere un flusso di lavoro PowerShell o un runbook di script PowerShell.  
2. Dopo aver modificato il runbook, salvarlo e fare clic su **archiviazione** da hello **modifica** blade.  
   
    ![Pulsante Archivia](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Check-in automazione di Azure sovrascriverà il codice hello attualmente presenti nel controllo del codice sorgente. istruzione di riga di comando equivalente Git toocheck aggiuntivo Hello è **aggiungere git + commit git + git push**  

1. Quando fa clic su **archiviazione**, si verrà visualizzato un messaggio di conferma, fare clic su Sì toocontinue.  
   
    ![Messaggio di archiviazione](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Archiviazione avvia hello origine controllo runbook: **sincronizzazione MicrosoftAzureAutomationAccountToGitHubV1**. Questo runbook si connette tooGitHub e inserisce le modifiche apportate dal repository tooyour di automazione di Azure. tooview hello archiviazione la cronologia dei processi, tornare indietro toohello **integrazione del controllo codice sorgente** scheda e fare clic su Pannello di sincronizzazione di Repository tooopen hello. Questo pannello mostra tutti i processi di controllo del codice sorgente.  Selezionare il processo di hello tooview desiderato e fare clic su Dettagli hello tooview.  
   
    ![Archiviazione del runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > I runbook di controllo del codice sorgente sono runbook di automazione speciali che non è possibile visualizzare o modificare. Mentre verranno visualizzati nell'elenco di runbook, verranno visualizzati i processi di sincronizzazione nell'elenco dei processi.
   > 
   > 
3. nome Hello di runbook hello modificato viene inviato come un parametro di input toohello archiviazione runbook. È possibile [consente di visualizzare i dettagli dei processi hello](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) espandendo runbook **Repository sincronizzazione** blade.  
   
    ![Archiviazione dell'input](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Una volta completata la processo hello modifiche hello tooview, aggiornare il repository di GitHub.  Dovrebbe esserci un commit nel repository con un messaggio commit: **aggiornato *nome Runbook* in automazione di Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Runbook di sincronizzazione dall'origine controllo tooAzure automazione
pulsante Sincronizza Hello nel Pannello di sincronizzazione di Repository hello consente toopull tutti hello runbook nel percorso di cartella runbook hello del tooyour repository account di automazione. Hello stesso repository può essere sincronizzata toomore rispetto a un account di automazione. Di seguito sono hello passaggi toosync un runbook:

1. Account di automazione in cui impostare il controllo del codice sorgente hello, aprire hello **pannello sincronizzazione integrazione/Repository del controllo origine** e fare clic su **sincronizzazione** richiesto con un messaggio di conferma messaggio, fare clic su **Sì** toocontinue.  
   
    ![Pulsante Sincronizza](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Sincronizzazione avvia runbook hello: **sincronizzazione MicrosoftAzureAutomationAccountFromGitHubV1**. Questo runbook tooGitHub connette ed estrae le modifiche di hello dal tooAzure repository automazione. Verrà visualizzato un nuovo processo in hello **Repository sincronizzazione** pannello per questa azione. Dettagli tooview del processo di sincronizzazione di hello, fare clic su Pannello di dettagli processo hello tooopen.  
   
    ![Sincronizzazione dei runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > La sincronizzazione dal controllo del codice sorgente sovrascrive versione di hello bozza di runbook hello attualmente presenti nell'account di automazione per **tutti** runbook incluse nel controllo del codice sorgente. Hello è toosync istruzione equivalente riga di comando Git **pull git**


## <a name="troubleshooting-source-control-problems"></a>Risoluzione dei problemi di controllo del codice sorgente
Se sono presenti errori con un processo di archiviazione o di sincronizzazione, è possibile visualizzare ulteriori dettagli sull'errore hello nel Pannello di hello processo deve essere sospeso lo stato del processo hello.  Hello **tutti i log** parte mostrerà tutti hello associati al processo di flussi di PowerShell. Questo verrà fornito che con i dettagli di hello necessari toohelp avere risolto i problemi con il controllo o la sincronizzazione. Verranno inoltre visualizzati si hello sequenza di azioni che si è verificato durante la sincronizzazione o verifica in un runbook.  

![Immagine AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Disconnessione del controllo del codice sorgente
toodisconnect dall'account GitHub, aprire il pannello di sincronizzazione di Repository hello e fare clic su **Disconnect**. Dopo la disconnessione di controllo del codice sorgente, i runbook che sono stati sincronizzati in precedenza rimarranno nell'account di automazione ma pannello Repository sincronizzazione hello non verrà abilitato.  

  ![Pulsante Disconnetti](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'integrazione del controllo codice sorgente, vedere hello seguenti risorse:  

* [Automazione di Azure: Integrazione del controllo del codice sorgente in Automazione di Azure](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Scelta del sistema di controllo del codice sorgente preferito](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Automazione di Azure: Integrazione del controllo del codice sorgente dei runbook usando Visual Studio Team Services](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

