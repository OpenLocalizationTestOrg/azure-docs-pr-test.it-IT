---
title: aaaUse tootrigger di automazione di Azure un processo | Documenti Microsoft
description: Informazioni su come toouse automazione di Azure per l'attivazione dei processi di gestione di dati di StorSimple (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Utilizzare tootrigger di automazione di Azure (anteprima privata) un processo

In questo articolo viene descritto come toouse tootrigger di automazione di Azure un processo di gestione di dati di StorSimple.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di disporre di:

*   Azure Powershell installato. [Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configurazione processo impostazioni di tooinitialize hello la trasformazione dei dati (istruzioni tooobtain queste impostazioni sono incluse in questo caso).
*   Una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.
*   Scaricare `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file dal repository github hello.
*   Scaricare `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) dal repository github hello.
*   Scaricare `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) dal repository github hello.

## <a name="step-by-step"></a>Procedura dettagliata

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Ottenere le autorizzazioni di Azure Active Directory per la definizione di processo hello hello automazione processo toorun

1. parametri di configurazione di hello tooretrieve per Active Directory, hello i passaggi seguenti:

    1. Aprire Windows PowerShell nel computer locale. Assicurarsi che [Azure PowerShell](https://azure.microsoft.com/downloads/) sia installato.
    1. Eseguire hello `Get-ConfigurationParams.ps1` script (nella cartella hello è stato scaricato in precedenza). Digitare hello comando nella finestra di PowerShell hello seguente:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Hello ActiveDirectoryKey è una password in uso in un secondo momento. Immettere una password a propria scelta. AppName può essere una stringa qualsiasi.

2. Questo script genera hello seguente i valori che devono essere utilizzati durante l'attivazione di hello runbook di automazione. Prendere nota dei valori seguenti.

    - ID Client
    - ID tenant
    - Chiave di Directory attiva (quella hello uno sopra specificato)
    - ID sottoscrizione

### <a name="set-up-hello-automation-account"></a>Configurare Account di automazione hello

1. Accedere a tooAzure e aprire l'account di automazione.
2. Fare clic su **asset** riquadro tooopen hello elenco degli asset.
3. Fare clic su **moduli** riquadro tooopen hello elenco dei moduli.
4. Fare clic su **+ Aggiungi un modulo** Pannello di modulo Aggiungi pulsante e hello viene avviata.

    ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Dopo aver selezionato hello `DataTransformationApp.zip` file dal computer locale, fare clic su **OK** modulo hello tooimport.

   Quando un account tooyour modulo di importazione di automazione di Azure, estrae i metadati relativi a modulo hello. Questa operazione potrebbe richiedere alcuni minuti.

   ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Si riceve una notifica viene distribuito il modulo hello e un'altra notifica al termine il processo di hello.  È inoltre possibile verificare lo stato di hello in **moduli** riquadro.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>runbook hello tooimport che attiva la definizione di processo hello

1. Nel portale di Azure hello, aprire l'account di automazione.
2. Fare clic su **runbook** riquadro tooopen hello elenco di runbook.
3. Fare clic su **+ Aggiungi runbook** e poi **Importa un runbook esistente**.

   ![Importare un runbook esistente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Fare clic su **file Runbook** e hello selezionare file tooimport `Trigger-DataTransformation-Job.ps1`.
5. Fare clic su **crea** tooimport hello runbook. Hello nuovo runbook verrà visualizzato nell'elenco di hello di runbook per hello account di automazione.
7. Fare clic sul runbook **Trigger-DataTransformation-Job** quindi su **Modifica**.
8. Fare clic su **Pubblica** quindi su **Sì** quando viene richiesta la conferma.


### <a name="toorun-hello-runbook"></a>runbook hello toorun:
1. Nel portale di Azure hello, aprire l'account di automazione.
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.
3. Fare clic su **Trigger-DataTransformation-Job**.
4. Fare clic su **avviare** toostart hello runbook.

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. In hello **avviare runbook** pannello, immettere tutti i parametri di hello. Fare clic su **OK** processo di trasformazione dei dati toosubmit hello.

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Passaggi successivi

[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).
