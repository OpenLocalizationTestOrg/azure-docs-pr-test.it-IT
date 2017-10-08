---
title: integrazione di aaaContinuous in Visual Studio Team Services con i progetti di gruppo di risorse di Azure | Documenti Microsoft
description: Viene descritto come tooset integrazione continua in Visual Studio Team Services usando il gruppo di risorse di Azure la distribuzione di progetti in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Integrazione continua in Visual Studio Team Services con i progetti di distribuzione Gruppo di risorse di Azure
toodeploy un modello di Azure, di eseguire attività nelle varie fasi: compilazione, Test, copia tooAzure (detto anche "Gestione temporanea") e il modello di distribuzione. Esistono due modi diversi toodeploy modelli tooVisual Studio Team Services (Visual Studio Team Services). Entrambi i metodi forniscono hello stessi risultati, quindi scegliere hello che meglio si adatta il flusso di lavoro.

1. Aggiungere una definizione di compilazione tooyour singolo passaggio che esegue uno script di PowerShell hello incluso nel progetto di distribuzione gruppo di risorse di Azure hello (Deploy-azureresourcegroup.ps1). script Hello copia gli elementi e quindi distribuisce il modello di hello.
2. Aggiungere più istruzioni di compilazione di VS Team Services, ognuna delle quali esegue un'attività della fase.

Questo articolo illustra entrambe le opzioni. prima opzione Hello presenta il vantaggio di hello di utilizzando hello stesso script utilizzato dagli sviluppatori in Visual Studio e fornire coerenza all'interno del ciclo di vita di hello. seconda opzione Hello offre uno script semplice toohello alternativo. Entrambe le procedure presuppongono che sia già disponibile un progetto di distribuzione di Visual Studio archiviato in VS Team Services.

## <a name="copy-artifacts-tooazure"></a>Copia gli elementi tooAzure
Se si dispone di tutti gli elementi necessari per la distribuzione del modello, indipendentemente dal scenario hello, è necessario assegnare toothem di accesso di gestione risorse di Azure. Questi elementi possono includere file, ad esempio:

* Modelli annidati
* Script di configurazione e script DSC
* File binari dell'applicazione

### <a name="nested-templates-and-configuration-scripts"></a>Modelli annidati e script di configurazione
Quando si utilizzano modelli hello forniti da Visual Studio o compilate con i frammenti di codice di Visual Studio, hello script di PowerShell fasi non solo gli elementi di hello, anche Parametrizza hello URI per le risorse di hello per distribuzioni diverse. script Hello quindi copia contenitore protetto di hello elementi tooa in Azure, viene creato un token di firma di accesso condiviso per tale contenitore e quindi passa l'informazione sulla distribuzione modello toohello. Vedere [creare una distribuzione modello](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn ulteriori informazioni sui modelli nidificati.  Quando si utilizza l'attività in Visual Studio Team Services, è necessario selezionare l'attività appropriata hello per la distribuzione del modello e se necessario, passare i valori di parametro da hello passaggio toohello distribuzione del modello di gestione temporanea.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Configurare la distribuzione continua in VS Team Services
script di PowerShell toocall hello in Visual Studio Team Services, è necessario tooupdate la definizione di compilazione. In breve, hello passaggi: 

1. Modificare la definizione di compilazione hello.
2. Configurare l'autorizzazione di Azure in VS Team Services.
3. Aggiungere un'istruzione di compilazione di Azure PowerShell che fa riferimento a script di PowerShell hello nel progetto di distribuzione di hello il gruppo di risorse di Azure.
4. Impostare il valore di hello di hello *- ArtifactsStagingDirectory* toowork parametro con un progetto compilato in Visual Studio Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Procedura dettagliata per l'opzione 1
Hello nelle procedure seguenti consentono di eseguire distribuzione continua tooconfigure necessari passaggi di hello in Visual Studio Team Services con una singola attività che esegue uno script di PowerShell hello nel progetto. 

1. Modificare la definizione di compilazione di VS Team Services e aggiungere un'istruzione di compilazione di Azure PowerShell. Selezionare la definizione di compilazione hello in hello **le definizioni di compilazione** categoria e quindi scegliere hello **modifica** collegamento.
   
   ![Modificare la definizione di compilazione][0]
2. Aggiungere un nuovo **Azure PowerShell** passaggio toohello compilazione definizione di compilazione e quindi scegliere hello **Aggiungi istruzione di compilazione...** .
   
   ![Aggiungere un'istruzione di compilazione][1]
3. Scegliere hello **attività di distribuzione** categoria, seleziona hello **Azure PowerShell** attività e quindi scegliere il relativo **Aggiungi** pulsante.
   
   ![Aggiungere attività][2]
4. Scegliere hello **Azure PowerShell** istruzione di compilazione, quindi compilare i relativi valori.
   
   1. Se si dispone già di un endpoint di servizio di Azure aggiunta tooVS Team Services, scegliere la sottoscrizione hello in hello **sottoscrizione Azure** casella di riepilogo a discesa e quindi ignora toohello nella sezione successiva. 
      
      Se non si dispone di un endpoint di servizio di Azure in Visual Studio Team Services, è necessario tooadd uno. In questa sottosezione illustra il processo di hello. Se l'account di Azure Usa un account Microsoft (ad esempio Hotmail), è necessario eseguire hello seguendo i passaggi tooget un'entità servizio di autenticazione.
   2. Scegliere hello **Gestisci** collegamento successivo toohello **sottoscrizione Azure** casella di riepilogo a discesa.
      
      ![Gestire le sottoscrizioni di Azure][3]
   3. Scegliere **Azure** in hello **nuovo Endpoint del servizio** casella di riepilogo a discesa.
      
      ![Nuovo endpoint di servizio][4]
   4. In hello **Aggiungi sottoscrizione di Azure** la finestra di dialogo, seleziona hello **dell'entità servizio** opzione.
      
      ![Oggetto entità servizio][5]
   5. Aggiungere il toohello di informazioni di sottoscrizione di Azure **Aggiungi sottoscrizione di Azure** la finestra di dialogo. È necessario hello tooprovide seguenti elementi:
      
      * ID sottoscrizione
      * Nome sottoscrizione
      * ID entità servizio
      * Chiave entità servizio
      * ID tenant
   6. Aggiungere un nome di toohello la scelta **sottoscrizione** casella nome. Questo valore viene visualizzato più avanti in hello **sottoscrizione Azure** elenco a discesa in Visual Studio Team Services. 
   7. Se non si conosce l'ID sottoscrizione Azure, è possibile utilizzare uno dei seguenti comandi tooretrieve hello è.
      
      Per gli script di Azure PowerShell usare:
      
      `Get-AzureRmSubscription`
      
      Per l'interfaccia della riga di comando di Azure usare:
      
      `azure account show`
   8. tooget un ID dell'entità servizio, la chiave dell'entità servizio e ID Tenant, attenersi alla procedura hello in [applicazione creare Active Directory e l'entità servizio utilizzando portale](resource-group-create-service-principal-portal.md) o [l'autenticazione di un'entità servizio con Gestione risorse di Azure](resource-group-authenticate-service-principal.md).
   9. Aggiungi hello toohello valori ID dell'entità servizio, la chiave dell'entità servizio e ID Tenant **Aggiungi sottoscrizione di Azure** finestra di dialogo, quindi scegliere hello **OK** pulsante.
      
      È ora disponibile un hello toorun toouse dell'entità servizio valido script di PowerShell di Azure.
5. Modificare la definizione di compilazione hello e scegliere hello **Azure PowerShell** istruzione di compilazione. Selezionare la sottoscrizione hello in hello **sottoscrizione Azure** casella di riepilogo a discesa. (Se la sottoscrizione hello non viene visualizzata, scegliere hello **aggiornamento** hello successivo pulsante **Gestisci** collegamento.) 
   
   ![Configurare l'attività di compilazione di Azure PowerShell][8]
6. Fornire un toohello percorso script deploy-azureresourcegroup.ps1 PowerShell. toodo, scegliere hello puntini di sospensione (…) pulsante Avanti toohello **percorso dello Script** passare script deploy-azureresourcegroup.ps1 PowerShell toohello hello **script** cartella del progetto, selezionare e quindi scegliere hello **OK** pulsante.    
   
   ![Scegliere il percorso tooscript][9]
7. Dopo aver selezionato script hello, script di aggiornamento hello percorso toohello in modo che viene eseguito dalla hello Build.StagingDirectory (hello stessa directory che *ArtifactsLocation* è impostato su). Questo scopo, è possibile aggiungere "$(Build.StagingDirectory)/" toohello inizio del percorso dello script hello.
   
    ![Modifica percorso tooscript][10]
8. In hello **argomenti Script** immettere hello seguenti parametri (in una singola riga). Quando si esegue uno script hello in Visual Studio, è possibile visualizzare come utilizza Visual Studio hello parametri hello **Output** finestra. È possibile utilizzare come punto di partenza per l'impostazione di valori di parametro hello in dell'istruzione di compilazione.
   
   | . | Descrizione |
   | --- | --- |
   | -ResourceGroupLocation |il valore di posizione geografica in cui si trova, ad esempio il gruppo di risorse hello Hello **eastus** o **'Stati Uniti orientali'**. (Aggiungere le virgolette singole se è presente uno spazio nel nome hello). Per altre informazioni, vedere [Aree di Azure](https://azure.microsoft.com/en-us/regions/). |
   | -ResourceGroupName |nome Hello hello del gruppo di risorse usato per la distribuzione. |
   | -UploadArtifacts |Questo parametro, se presente, specifica che gli elementi che devono toobe caricato tooAzure dal sistema locale hello. È necessario solo tooset questa opzione se la distribuzione modello richiede elementi aggiuntivi che si desidera toostage hello lo script di PowerShell (ad esempio gli script di configurazione o modelli annidati). |
   | -StorageAccountName |nome Hello hello dell'account di archiviazione usati toostage elementi per la distribuzione. Questo parametro viene usato solo se si sta eseguendo la gestione temporanea di elementi per la distribuzione. Se questo parametro viene specificato, viene creato un nuovo account di archiviazione se script hello non ha creato uno durante una distribuzione precedente. Se viene specificato il parametro hello, account di archiviazione hello deve esistere. |
   | -StorageAccountResourceGroupName |nome Hello hello del gruppo di risorse associato con account di archiviazione hello. Questo parametro è obbligatorio solo se si specifica un valore per il parametro StorageAccountName hello. |
   | -TemplateFile |Hello percorso toohello file modello nel progetto di distribuzione di hello il gruppo di risorse di Azure. tooenhance flessibilità, usare un percorso per questo parametro è il percorso relativo toohello di hello script di PowerShell anziché un percorso assoluto. |
   | -TemplateParametersFile |Hello percorso toohello file dei parametri nel progetto di distribuzione di hello il gruppo di risorse di Azure. tooenhance flessibilità, usare un percorso per questo parametro è il percorso relativo toohello di hello script di PowerShell anziché un percorso assoluto. |
   | -ArtifactStagingDirectory |Questo parametro consente di script di PowerShell hello SA cartella hello in cui devono essere copiati i file binari del progetto hello. Questo valore sostituisce il valore di predefinito hello utilizzato da uno script di PowerShell hello. Per utilizzare Visual Studio Team Services, impostare il valore di hello: $(Build.StagingDirectory) - ArtifactStagingDirectory |
   
   Ecco un esempio di argomenti dello script, la riga è interrotta per facilitare la lettura:
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Al termine, hello **argomenti Script** casella dovrebbe essere simile a hello seguente elenco:
   
   ![Argomenti script][11]
9. Dopo aver aggiunto tutti gli elementi richiesti toohello Azure PowerShell istruzione di compilazione di hello, scegliere hello **coda** compilare pulsante toobuild hello progetto. Hello **compilare** schermata mostra l'output di hello dalla hello script di PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Procedura dettagliata per l'opzione 2
Hello nelle procedure seguenti consentono di eseguire distribuzione continua tooconfigure necessari passaggi di hello in Visual Studio Team Services con attività predefinite di hello.

1. Modificare le Visual Studio Team Services compilazione definizione tooadd due nuove istruzioni di compilazione. Selezionare la definizione di compilazione hello in hello **le definizioni di compilazione** categoria e quindi scegliere hello **modifica** collegamento.
   
   ![Modificare la definizione di compilazione][12]
2. Istruzioni di compilazione hello Aggiungi nuova definizione di compilazione toohello utilizzando hello **Aggiungi istruzione di compilazione...** .
   
   ![Aggiungere un'istruzione di compilazione][13]
3. Scegliere hello **Distribuisci** categoria attività, seleziona hello **copia dei File di Azure** attività e quindi scegliere il relativo **Aggiungi** pulsante.
   
   ![Aggiungere l'attività Copia dei file di Azure][14]
4. Scegliere hello **distribuzione gruppo di risorse di Azure** attività, quindi scegliere il relativo **Aggiungi** pulsante e quindi **Chiudi** hello **attività catalogo**.
   
   ![Aggiungere attività Distribuzione gruppo di risorse di Azure][15]
5. Scegliere hello **copia dei File di Azure** compilare i relativi valori e delle attività.
   
   Se si dispone già di un endpoint di servizio di Azure aggiunta tooVS Team Services, scegliere la sottoscrizione hello in hello **sottoscrizione Azure** casella di riepilogo a discesa. Se non si dispone di una sottoscrizione vedere l'[opzione 1](#detailed-walkthrough-for-option-1) per istruzioni sull'impostazione di una sottoscrizione in VS Team Services.
   
   * Origine: immettere **$(Build.StagingDirectory)**
   * Tipo di connessione ad Azure: selezionare **Azure Resource Manager**
   * Sottoscrizione di Azure RM - sottoscrizione selezionare hello per account di archiviazione hello da toouse in hello **sottoscrizione Azure** casella di riepilogo a discesa. Se la sottoscrizione hello non viene visualizzata, scegliere hello **aggiornamento** hello successivo pulsante **Gestisci** collegamento.
   * Tipo di destinazione: selezionare **Blob di Azure**
   * RM Account di archiviazione - selezione dell'account di archiviazione hello si vorrebbe toouse per gli elementi di gestione temporanea
   * Nome del contenitore - immettere il nome di hello del contenitore hello desideri toouse per la gestione temporanea; può essere qualsiasi nome di contenitore valido, ma utilizzare una definizione di compilazione toothis dedicato
   
   Per i valori di output di hello:
   
   * URI contenitore di archiviazione: immettere **artifactsLocation**
   * Token di firma di accesso condiviso contenitore di archiviazione: immettere **artifactsLocationSasToken**
   
   ![Configurare l'attività Copia dei file di Azure][16]
6. Scegliere hello **distribuzione gruppo di risorse di Azure** istruzione di compilazione, quindi compilare i relativi valori.
   
   * Tipo di connessione ad Azure: selezionare **Azure Resource Manager**
   * Sottoscrizione di Azure RM - sottoscrizione hello selezionare per la distribuzione in hello **sottoscrizione Azure** casella di riepilogo a discesa. In genere si tratterà hello stessa sottoscrizione utilizzata nel passaggio precedente hello
   * Azione - selezionare **Creare o aggiornare un gruppo di risorse**
   * Gruppo di risorse - selezionare un gruppo di risorse o immettere nome hello del nuovo gruppo di risorse per la distribuzione di hello
   * Posizione - hello selezionare per il gruppo di risorse hello
   * Modello - immettere hello percorso e nome di hello modello toobe distribuito anteponendo **$(Build.StagingDirectory)**, ad esempio: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parametri di modello, immettere il percorso di hello e nome di hello parametri toobe utilizzato, anteponendo **$(Build.StagingDirectory)**, ad esempio: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Eseguire l'override di parametri di modello - immettere o copiare e incollare hello seguente codice:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configurare l'attività Distribuzione gruppo di risorse di Azure][17]
7. Dopo aver aggiunto tutti gli elementi di hello richiesto, salvare la definizione di compilazione hello e scegliere **Accoda nuova compilazione** nella parte superiore di hello.

## <a name="next-steps"></a>Passaggi successivi
Lettura [Panoramica di gestione risorse di Azure](azure-resource-manager/resource-group-overview.md) toolearn ulteriori informazioni su Gestione risorse di Azure e i gruppi di risorse di Azure.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
