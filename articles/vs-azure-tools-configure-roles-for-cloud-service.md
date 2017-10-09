---
title: i ruoli di hello aaaConfigure per un Azure cloud service con Visual Studio | Documenti Microsoft
description: Informazioni su come tooset e configurare i ruoli per servizi cloud di Azure con Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Configurare un ruolo per un servizio cloud di Azure con Visual Studio
Un servizio cloud di Azure può includere uno o più ruoli di lavoro o ruoli Web. Per ogni ruolo, è necessario toodefine come impostare tale ruolo e inoltre configurare la modalità di esecuzione di tale ruolo. toolearn ulteriori informazioni sui ruoli nei servizi cloud, vedere il video hello [tooAzure introduzione servizi Cloud](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

informazioni di Hello per il servizio cloud vengono archiviate in hello i seguenti file:

- **Servicedefinition. Csdef** -file di definizione del servizio hello definisce le impostazioni di runtime hello per il servizio cloud include i ruoli richiesti, endpoint e dimensioni della macchina virtuale. Nessuno dei dati di hello archiviati in `ServiceDefinition.csdef` può essere modificato quando il ruolo è in esecuzione.
- **ServiceConfiguration. cscfg** : file di configurazione del servizio hello configura il numero di istanze di un ruolo viene eseguito e valori hello delle impostazioni di hello è definito per un ruolo. Hello dati archiviati in `ServiceConfiguration.cscfg` possono essere modificate mentre il ruolo è in esecuzione.

toostore diversi valori per le impostazioni di hello che controllano la modalità di esecuzione di un ruolo, è possibile definire più configurazioni del servizio. È possibile usare una configurazione del servizio diversa per ogni ambiente di distribuzione. Ad esempio, è possibile impostare l'emulatore di archiviazione di Azure locale di archiviazione account connessione stringa toouse hello in una configurazione del servizio locale e creare un altro toouse di configurazione del Servizio archiviazione di Azure nel cloud hello.

Quando si crea un servizio cloud di Azure in Visual Studio, due configurazioni del servizio vengono automaticamente create e aggiunti tooyour progetto Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Configurare un servizio cloud di Azure
È possibile configurare un servizio cloud di Azure da Esplora soluzioni in Visual Studio, come illustrato nell'hello alla procedura seguente:

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.
   
    ![Menu di scelta rapida di Esplora soluzioni](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Nella pagina delle proprietà del progetto hello, selezionare hello **sviluppo** scheda. 

    ![Pagina delle proprietà del progetto - Scheda Sviluppo](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. In hello **configurazione del servizio** elenco, il nome di hello selezionare della configurazione del servizio hello che si desidera tooedit. (Se si desidera toomake Modifica configurazioni del servizio hello tooall per questo ruolo, selezionare **tutte le configurazioni**.)
   
    > [!IMPORTANT]
    > Se si sceglie una configurazione del servizio specifica, alcune proprietà verranno disabilitate perché possono essere impostate solo per tutte le configurazioni. tooedit queste proprietà, è necessario selezionare **tutte le configurazioni**.
    > 
    > 
   
    ![Elenco Configurazione del servizio per un servizio cloud di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Modificare hello il numero di istanze del ruolo
prestazioni di hello tooimprove del servizio cloud, è possibile modificare il numero di hello di istanze di un ruolo in esecuzione, in base al numero di hello di utenti o hello carico previsto per un particolare ruolo. Una macchina virtuale separata viene creata per ogni istanza di un ruolo quando il servizio cloud hello in esecuzione in Azure. Ciò influisce sulla fatturazione hello per la distribuzione di hello di questo servizio cloud. Per altre informazioni sulla fatturazione, vedere l'argomento contenente [informazioni sulla fatturazione per Microsoft Azure](billing/billing-understand-your-bill.md).

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello. In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleziona hello **configurazione** scheda.

    ![Scheda Configurazione](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.
   
    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. In hello **numero** testo immettere il numero di hello di istanze che si desidera toostart per questo ruolo. Ogni istanza viene eseguita su una macchina virtuale separata quando si pubblica tooAzure servizio cloud di hello.

    ![Numero di istanze di hello aggiornamento](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Gestire le stringhe di connessione per gli account di archiviazione
È possibile aggiungere, rimuovere o modificare le stringhe di connessione per le configurazioni del servizio. Ad esempio, è possibile che si voglia creare una stringa di connessione locale per una configurazione del servizio locale con valore `UseDevelopmentStorage=true`. È inoltre possibile tooconfigure una configurazione del servizio cloud che utilizza un account di archiviazione in Azure.

> [!WARNING]
> Quando si immettono informazioni chiave con account di archiviazione di Azure hello per una stringa di connessione di account di archiviazione, queste informazioni sono archiviate in locale il file di configurazione servizio hello. Queste informazioni, tuttavia, non vengono attualmente archiviate come testo crittografato.
> 
> 

Utilizzando un valore diverso per ogni configurazione del servizio, si non sono stringhe di connessione diverse toouse nel servizio cloud o modificare il codice quando si pubblica il tooAzure servizio cloud. È possibile utilizzare hello stesso nome per la stringa di connessione hello nel valore del codice e hello è diverso, in base alla configurazione di servizio hello che si seleziona quando si compila il servizio cloud o quando si esegue la pubblicazione.

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello. In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleziona hello **impostazioni** scheda.

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.

    ![Service Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Selezionare una stringa di connessione tooadd **Aggiungi impostazione**.

    ![Aggiungere una stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Dopo l'aggiunta di nuova impostazione hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.

    ![Nuova stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -immettere il nome di hello che si desidera toouse hello stringa di connessione.
    - **Tipo** : selezionare questa opzione **stringa di connessione** dall'elenco a discesa hello.
    - **Valore** -è possibile immettere la stringa di connessione hello direttamente in hello **valore** cella o hello selezionare i puntini di sospensione (…) toowork in hello **crea stringa di connessione di archiviazione** finestra di dialogo.  

1. In hello **crea stringa di connessione di archiviazione** finestra di dialogo, selezionare un'opzione per **connettersi utilizzando**. Seguire le istruzioni di hello per opzione hello selezionata:

    - **Emulatore di archiviazione di Microsoft Azure** -se si seleziona questa opzione, le impostazioni rimanenti hello nella finestra di dialogo hello sono disabilitate perché sono validi solo tooAzure. Selezionare **OK**.
    - **La sottoscrizione** : se si seleziona questa opzione, usare hello elenco a discesa elenco tooeither selezionare e accesso in un account Microsoft o aggiunta un account Microsoft. Selezionare una sottoscrizione e un account di archiviazione di Azure. Selezionare **OK**.
    - **Credenziali immesse manualmente** : immettere il nome di account di archiviazione hello e una chiave primaria o a seconda di hello. Selezionare un'opzione per **Connessione**. Nella maggior parte dei casi è consigliato HTTPS. Selezionare **OK**.

1. Selezionare la stringa di connessione hello toodelete una stringa di connessione e quindi selezionare **Rimuovi impostazione**.

1. Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.

## <a name="programmatically-access-a-connection-string"></a>Accedere a una stringa di connessione a livello di codice

Hello passaggi seguenti viene illustrato come accedere a una stringa di connessione utilizzando il linguaggio c# tooprogrammatically.

1. Aggiungere il seguente hello utilizzando file di direttive tooa c# in cui si sta impostazione hello toouse:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello codice seguente viene illustrato un esempio di come tooaccess una stringa di connessione. Sostituire hello &lt;ConnectionStringName > segnaposto con il valore appropriato hello. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Aggiungere impostazioni personalizzate toouse nel servizio cloud di Azure
Le impostazioni personalizzate nel file di configurazione del servizio hello consentono di aggiungere un nome e il valore di una stringa per una configurazione del servizio specifico. È possibile scegliere toouse tooconfigure questa impostazione una funzionalità nel servizio cloud leggendo il valore di hello di hello impostazione e l'utilizzo di questa logica di hello toocontrol valore nel codice. È possibile modificare questi valori di configurazione del servizio senza dovere toorebuild il pacchetto del servizio o quando è in esecuzione il servizio cloud. Il codice può cercare notifiche in caso di modifiche di un'impostazione. Vedere l' [Evento RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

È possibile aggiungere, rimuovere o modificare impostazioni personalizzate per le configurazioni del servizio. Potrebbero essere necessari diversi valori per queste stringhe per configurazioni del servizio diverse.

Utilizzando un valore diverso per ogni configurazione del servizio, si non sono stringhe diverse toouse nel servizio cloud o modificare il codice quando si pubblica il tooAzure servizio cloud. È possibile utilizzare hello stesso nome per la stringa hello nel valore del codice e hello è diverso, in base alla configurazione di servizio hello che si seleziona quando si compila il servizio cloud o quando si esegue la pubblicazione.

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello. In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleziona hello **impostazioni** scheda.

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Selezionare un'impostazione personalizzata, tooadd **Aggiungi impostazione**.

    ![Aggiungere impostazioni personalizzate](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Dopo l'aggiunta di nuova impostazione hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.

    ![Nuova impostazione personalizzata](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -immettere il nome di hello dell'impostazione di hello.
    - **Tipo** : selezionare questa opzione **stringa** dall'elenco a discesa hello.
    - **Valore** -immettere il valore di hello dell'impostazione di hello. È possibile immettere il valore di hello direttamente in hello **valore** cella o hello selezionare i puntini di sospensione (…) tooenter hello valore hello **Modifica stringa** finestra di dialogo.  

1. toodelete un'impostazione personalizzata, selezionare l'impostazione di hello e quindi selezionare **Rimuovi impostazione**.

1. Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.

## <a name="programmatically-access-a-custom-settings-value"></a>Accedere al valore dell'impostazione personalizzata a livello di codice
 
Hello passaggi seguenti viene illustrato come accedere a un'impostazione personalizzata in c# tooprogrammatically.

1. Aggiungere il seguente hello utilizzando file di direttive tooa c# in cui si sta impostazione hello toouse:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello codice seguente viene illustrato un esempio di come tooaccess un'impostazione personalizzata. Sostituire hello &lt;SettingName > segnaposto con il valore appropriato hello. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Gestire le risorse di archiviazione locali per ogni istanza del ruolo
È possibile aggiungere una risorsa di archiviazione del file system locale per ogni istanza del ruolo. Hello i dati memorizzati nell'archiviazione non è accessibile da altre istanze del ruolo di hello per cui hello dati vengono archiviati o da altri ruoli.  

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, espandere il nodo di progetto hello. In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Seleziona hello **archiviazione locale** scheda.

    ![Scheda Archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. In hello **configurazione del servizio** elenco, verificare che **tutte le configurazioni** selezionata come impostazioni di archiviazione locale hello applicano tooall configurazioni del servizio. Qualsiasi altro valore comporta in tutti i campi di input hello nella pagina di hello è disabilitata. 

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. Selezionare una voce di archiviazione locale, tooadd **aggiungere archiviazione locale**.

    ![Aggiungi risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Dopo aver aggiunto la nuova voce archiviazione locale di hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.

    ![Nuova risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nome** -immettere il nome di hello che si desidera toouse per l'archiviazione locale nuovo hello.
    - **Dimensioni (MB)** -immettere hello dimensione in MB necessaria per l'archiviazione locale nuovo hello.
    - **Pulizia in riciclo ruolo** -selezionare dati opzione tooremove hello nella memoria locale nuovo hello quando hello di macchina virtuale per il ruolo di hello viene riciclato.

1. toodelete una voce di archiviazione locale, selezionare la voce hello e quindi selezionare **rimuovere spazio di archiviazione locale**.

1. Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.

## <a name="programmatically-accessing-local-storage"></a>Accedere alla risorsa di archiviazione locale a livello di codice

In questa sezione viene illustrato come tooprogrammatically accedere all'archiviazione locale utilizzando c# mediante la scrittura di un file di testo test `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Scrivere un'archiviazione toolocal file di testo

Hello seguente codice mostra un esempio di come un testo toowrite toolocal archiviazione di file. Sostituire hello &lt;LocalStorageName > segnaposto con il valore appropriato hello. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Trovare un file scritto toolocal archiviazione

file hello tooview creata dal codice hello nella sezione precedente hello, seguire questi passaggi:
    
1.  Nell'area di notifica Windows hello, fare doppio clic sull'icona Azure hello e, dal menu di scelta rapida hello, selezionare **Mostra interfaccia utente di emulatore di calcolo**. 

    ![Mostra emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Selezionare ruolo web hello.

    ![Emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. In hello **emulatore di calcolo di Microsoft Azure** dal menu **strumenti** > **Apri archivio locale**.

    ![Voce di menu Apri risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Quando si apre la finestra di Esplora hello, immettere ' MyLocalStorageTest.txt ' in hello **ricerca** casella di testo e selezionare **invio** ricerca hello toostart. 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sui progetti Azure in Visual Studio, vedere [Configurazione di un progetto Azure](vs-azure-tools-configuring-an-azure-project.md). Altre informazioni sullo schema di servizi cloud hello leggendo [riferimento allo Schema](https://msdn.microsoft.com/library/azure/dd179398).

