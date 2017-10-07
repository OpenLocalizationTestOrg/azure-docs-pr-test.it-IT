---
title: distribuzione aaaAutomating di una macchina virtuale in Amazon Web Services | Documenti Microsoft
description: In questo articolo viene illustrato come toouse creazione tooautomate di automazione di Azure di una macchina virtuale del servizio Web di Amazon
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a>Scenario di Automazione di Azure - Provisioning di una macchina virtuale di AWS
In questo articolo viene illustrato come è possibile sfruttare tooprovision di automazione di Azure di una macchina virtuale nella sottoscrizione di Amazon Web Service (AWS) e assegnare tale macchina virtuale un nome specifico, quale AWS fa riferimento tooas "tag" hello macchina virtuale.

## <a name="prerequisites"></a>Prerequisiti
Ai fini di hello di questo articolo, è necessario toohave un account di automazione di Azure e una sottoscrizione di AWS. Per altre informazioni sulla configurazione di un account di Automazione di Azure e sulla configurazione delle credenziali della sottoscrizione di AWS, vedere l'articolo relativo alla [configurazione dell'autenticazione in Amazon Web Services](automation-configure-aws-account.md).  Questo account deve essere creato o aggiornato con le credenziali di sottoscrizione AWS prima di procedere, come si farà riferimento questo account in seguito hello.

## <a name="deploy-amazon-web-services-powershell-module"></a>Distribuire il modulo di PowerShell di Amazon Web Services
La macchina virtuale provisioning runbook userà hello AWS PowerShell modulo toodo il proprio lavoro. Eseguire i seguenti passaggi tooadd hello modulo tooyour account di automazione che è configurato con le credenziali di sottoscrizione AWS hello.  

1. Aprire il web browser e passare toohello [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) e fare clic su hello **pulsante di automazione tooAzure Distribuisci**.<br><br> ![Importazione del modulo PS per AWS](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)
2. Che viene visualizzata una pagina di accesso di Azure toohello e dopo l'autenticazione, sarà indirizzato toohello portale di Azure e presentati con hello seguente blade.<br><br> ![Pannello Importa modulo](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. Hello Seleziona gruppo di risorse da hello **gruppo di risorse** elenco a discesa elenco e nel pannello parametri hello, fornire hello le seguenti informazioni:
   
   * Da hello **nuovo o Account di automazione esistente (string)** elenco a discesa selezionare **esistente**.  
   * In hello **nome Account di automazione (stringa)** casella, digitare il nome esatto di hello di account di automazione che include le credenziali di hello per la sottoscrizione di AWS hello.  Ad esempio, se è stato creato un account dedicato denominato **AWSAutomation**, che è il testo digitato nella casella hello.
   * Selezionare il paese appropriato da hello di hello **località dell'Account di automazione** elenco a discesa.
4. Dopo aver completato l'immissione dei dati di hello necessarie, fare clic su **crea**.
   
   > [!NOTE]
   > Durante l'importazione di un modulo di PowerShell in automazione di Azure, è anche estrazione cmdlet hello e queste attività non verranno visualizzate finché non modulo hello ha completato l'importazione e l'estrazione di hello cmdlet. Il processo potrebbe richiedere alcuni minuti.  
   > <br>
   > 
   > 
5. Nel portale di Azure hello, aprire l'account di automazione cui viene fatto riferimento nel passaggio 3.
6. Fare clic su hello **asset** riquadro e hello **asset** blade, seleziona hello **moduli** riquadro.
7. In hello **moduli** pannello verrà visualizzato hello **AWSPowerShell** modulo nell'elenco di hello.

## <a name="create-aws-deploy-vm-runbook"></a>Creare un runbook per la distribuzione di una VM in AWS
Una volta hello che AWS modulo di PowerShell è stato distribuito, è possibile creare un tooautomate runbook provisioning di una macchina virtuale in AWS tramite uno script di PowerShell. procedura di Hello seguente verrà illustrato come tooleverage script di PowerShell nativa in automazione di Azure.  

> [!NOTE]
> Per ulteriori informazioni e opzioni riguardanti questo script, visitare hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).
> 

1. Scaricare uno script di PowerShell New-AwsVM hello da PowerShell Gallery hello aprendo una sessione di PowerShell e digitare hello seguente:<br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. Hello portale di Azure, aprire l'account di automazione e fare clic su hello **runbook** riquadro.  
3. Da hello **runbook** pannello seleziona **aggiungere un runbook**.
4. In hello **aggiungere un runbook** pannello seleziona **creazione rapida** (creare un nuovo runbook).
5. In hello **Runbook** Pannello proprietà, digitare un nome nella casella Nome hello per il runbook e da hello **tipo Runbook** elenco a discesa selezionare **PowerShell**, quindi fare clic su  **Creare**.<br><br> ![Pannello Importa modulo](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)
6. Quando viene visualizzato il pannello di modifica PowerShell Runbook hello, copiare e incollare l'area di disegno di creazione dei runbook hello script di PowerShell hello.<br><br> ![Script di PowerShell per il runbook](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > Si noti seguenti hello quando si lavora con l'esempio hello script di PowerShell:
    > 
    > * Hello runbook contiene un numero di valori di parametro predefiniti. Valutare tutti i valori predefiniti e apportare gli aggiornamenti necessari.
    > * Se si hanno le AWS le credenziali archiviate in un asset credenziali denominato in modo diverso rispetto a **AWScred**, sarà necessario script hello tooupdate nella riga 57 toomatch di conseguenza.  
    > * Quando si lavora con hello i comandi CLI AWS in PowerShell, soprattutto con questo runbook di esempio, è necessario specificare l'area AWS hello. In caso contrario, i cmdlet di hello avrà esito negativo.  Visualizza argomento AWS [specificare area AWS](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in hello AWS strumenti per il documento di PowerShell per altri dettagli.  
    >

7. tooretrieve un elenco di nomi di immagine dalla sottoscrizione di AWS, avviare PowerShell ISE e importare il modulo di PowerShell AWS hello.  Eseguire l'autenticazione in AWS sostituendo **Get-AutomationPSCredential** nell'ambiente ISE con **AWScred = Get-Credential**.  Questo richiederà l'immissione delle credenziali ed è possibile fornire il **ID chiave di accesso** per nome utente hello e **chiave di accesso privata** password hello.  Vedere l'esempio hello riportato di seguito:  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    Hello output seguente viene restituito:<br><br>
   ![Ottenere immagini AWS](./media/automation-scenario-aws-deployment/powershell-ise-output.png)<br>  
8. Copiare e incollare hello uno dei nomi di immagine hello in una variabile di automazione a cui fa riferimento hello runbook come **$InstanceType**. Poiché in questo esempio si sta usando hello AWS disponibile a più livelli di sottoscrizione, si userà **t2.micro** per questo esempio di runbook.  
9. Salvare il runbook hello, quindi fare clic su **pubblica** toopublish hello runbook e quindi **Sì** quando richiesto.

### <a name="testing-hello-aws-vm-runbook"></a>Test hello runbook AWS VM
Prima di procedere con test hello runbook, è necessario tooverify alcuni aspetti. In particolare:  

* È stata creata una risorsa per l'autenticazione di base AWS chiamata **AWScred** o script hello è stata nome hello tooreference aggiornato dell'asset delle credenziali.    
* non è stato importato il modulo di PowerShell di AWS Hello in automazione di Azure  
* È stato creato un nuovo runbook e i valori dei parametri sono stati verificati e aggiornati, se necessario  
* **Registrazione dei record dettagliati** e facoltativamente **registrazione dei record di stato di avanzamento** con impostazione del runbook hello **registrazione e traccia** sono stati impostati troppo**su**.<br><br> ![Registrazione e traccia per i runbook](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)  

1. Si desidera toostart hello runbook, quindi fare clic su **avviare** e quindi fare clic su **OK** quando si apre Pannello avvia Runbook hello.
2. Nel pannello avvia Runbook hello, fornire un **VMname**.  Accettare i valori predefiniti di hello per hello altri parametri che è preconfigurato nello script hello in precedenza.  Fare clic su **OK** toostart processo del runbook hello.<br><br> ![Avvio del runbook New-AwsVM](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)
3. Il riquadro di un processo viene aperto per il processo di runbook hello che abbiamo appena creato. Chiudere questo riquadro.
4. È possibile visualizzare lo stato di avanzamento dell'output di hello processo e visualizzazione **flussi** selezionando hello **tutti i log** riquadro dal Pannello di processo runbook hello.<br><br> ![Output del flusso](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)
5. Se non si è attualmente connessi, hello tooconfirm macchina virtuale è in corso il provisioning accedere hello AWS Management Console.<br><br> ![Macchina virtuale distribuita in una console di AWS](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
* tooknow ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)
* Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [supporto di script PowerShell nativi in Automazione di Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

