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
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="370df-103">Configurare un ruolo per un servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="370df-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="370df-104">Un servizio cloud di Azure può includere uno o più ruoli di lavoro o ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="370df-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="370df-105">Per ogni ruolo, è necessario toodefine come impostare tale ruolo e inoltre configurare la modalità di esecuzione di tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="370df-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="370df-106">toolearn ulteriori informazioni sui ruoli nei servizi cloud, vedere il video hello [tooAzure introduzione servizi Cloud](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="370df-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="370df-107">informazioni di Hello per il servizio cloud vengono archiviate in hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="370df-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="370df-108">**Servicedefinition. Csdef** -file di definizione del servizio hello definisce le impostazioni di runtime hello per il servizio cloud include i ruoli richiesti, endpoint e dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="370df-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="370df-109">Nessuno dei dati di hello archiviati in `ServiceDefinition.csdef` può essere modificato quando il ruolo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="370df-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="370df-110">**ServiceConfiguration. cscfg** : file di configurazione del servizio hello configura il numero di istanze di un ruolo viene eseguito e valori hello delle impostazioni di hello è definito per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="370df-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="370df-111">Hello dati archiviati in `ServiceConfiguration.cscfg` possono essere modificate mentre il ruolo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="370df-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="370df-112">toostore diversi valori per le impostazioni di hello che controllano la modalità di esecuzione di un ruolo, è possibile definire più configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="370df-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="370df-113">È possibile usare una configurazione del servizio diversa per ogni ambiente di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="370df-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="370df-114">Ad esempio, è possibile impostare l'emulatore di archiviazione di Azure locale di archiviazione account connessione stringa toouse hello in una configurazione del servizio locale e creare un altro toouse di configurazione del Servizio archiviazione di Azure nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="370df-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="370df-115">Quando si crea un servizio cloud di Azure in Visual Studio, due configurazioni del servizio vengono automaticamente create e aggiunti tooyour progetto Azure:</span><span class="sxs-lookup"><span data-stu-id="370df-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="370df-116">Configurare un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="370df-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="370df-117">È possibile configurare un servizio cloud di Azure da Esplora soluzioni in Visual Studio, come illustrato nell'hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="370df-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="370df-118">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="370df-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="370df-119">In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="370df-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Menu di scelta rapida di Esplora soluzioni](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="370df-121">Nella pagina delle proprietà del progetto hello, selezionare hello **sviluppo** scheda.</span><span class="sxs-lookup"><span data-stu-id="370df-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Pagina delle proprietà del progetto - Scheda Sviluppo](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="370df-123">In hello **configurazione del servizio** elenco, il nome di hello selezionare della configurazione del servizio hello che si desidera tooedit.</span><span class="sxs-lookup"><span data-stu-id="370df-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="370df-124">(Se si desidera toomake Modifica configurazioni del servizio hello tooall per questo ruolo, selezionare **tutte le configurazioni**.)</span><span class="sxs-lookup"><span data-stu-id="370df-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="370df-125">Se si sceglie una configurazione del servizio specifica, alcune proprietà verranno disabilitate perché possono essere impostate solo per tutte le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="370df-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="370df-126">tooedit queste proprietà, è necessario selezionare **tutte le configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="370df-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Elenco Configurazione del servizio per un servizio cloud di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="370df-128">Modificare hello il numero di istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="370df-128">Change hello number of role instances</span></span>
<span data-ttu-id="370df-129">prestazioni di hello tooimprove del servizio cloud, è possibile modificare il numero di hello di istanze di un ruolo in esecuzione, in base al numero di hello di utenti o hello carico previsto per un particolare ruolo.</span><span class="sxs-lookup"><span data-stu-id="370df-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="370df-130">Una macchina virtuale separata viene creata per ogni istanza di un ruolo quando il servizio cloud hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="370df-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="370df-131">Ciò influisce sulla fatturazione hello per la distribuzione di hello di questo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="370df-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="370df-132">Per altre informazioni sulla fatturazione, vedere l'argomento contenente [informazioni sulla fatturazione per Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="370df-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="370df-133">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="370df-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="370df-134">In **Esplora**, espandere il nodo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="370df-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="370df-135">In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="370df-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="370df-137">Seleziona hello **configurazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="370df-137">Select hello **Configuration** tab.</span></span>

    ![Scheda Configurazione](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="370df-139">In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.</span><span class="sxs-lookup"><span data-stu-id="370df-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="370df-141">In hello **numero** testo immettere il numero di hello di istanze che si desidera toostart per questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="370df-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="370df-142">Ogni istanza viene eseguita su una macchina virtuale separata quando si pubblica tooAzure servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="370df-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Numero di istanze di hello aggiornamento](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="370df-144">Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="370df-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="370df-145">Gestire le stringhe di connessione per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="370df-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="370df-146">È possibile aggiungere, rimuovere o modificare le stringhe di connessione per le configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="370df-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="370df-147">Ad esempio, è possibile che si voglia creare una stringa di connessione locale per una configurazione del servizio locale con valore `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="370df-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="370df-148">È inoltre possibile tooconfigure una configurazione del servizio cloud che utilizza un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="370df-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="370df-149">Quando si immettono informazioni chiave con account di archiviazione di Azure hello per una stringa di connessione di account di archiviazione, queste informazioni sono archiviate in locale il file di configurazione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="370df-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="370df-150">Queste informazioni, tuttavia, non vengono attualmente archiviate come testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="370df-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="370df-151">Utilizzando un valore diverso per ogni configurazione del servizio, si non sono stringhe di connessione diverse toouse nel servizio cloud o modificare il codice quando si pubblica il tooAzure servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="370df-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="370df-152">È possibile utilizzare hello stesso nome per la stringa di connessione hello nel valore del codice e hello è diverso, in base alla configurazione di servizio hello che si seleziona quando si compila il servizio cloud o quando si esegue la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="370df-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="370df-153">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="370df-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="370df-154">In **Esplora**, espandere il nodo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="370df-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="370df-155">In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="370df-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="370df-157">Seleziona hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="370df-157">Select hello **Settings** tab.</span></span>

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="370df-159">In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.</span><span class="sxs-lookup"><span data-stu-id="370df-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Service Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="370df-161">Selezionare una stringa di connessione tooadd **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="370df-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Aggiungere una stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="370df-163">Dopo l'aggiunta di nuova impostazione hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="370df-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nuova stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="370df-165">**Nome** -immettere il nome di hello che si desidera toouse hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="370df-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="370df-166">**Tipo** : selezionare questa opzione **stringa di connessione** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="370df-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="370df-167">**Valore** -è possibile immettere la stringa di connessione hello direttamente in hello **valore** cella o hello selezionare i puntini di sospensione (…) toowork in hello **crea stringa di connessione di archiviazione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="370df-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="370df-168">In hello **crea stringa di connessione di archiviazione** finestra di dialogo, selezionare un'opzione per **connettersi utilizzando**.</span><span class="sxs-lookup"><span data-stu-id="370df-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="370df-169">Seguire le istruzioni di hello per opzione hello selezionata:</span><span class="sxs-lookup"><span data-stu-id="370df-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="370df-170">**Emulatore di archiviazione di Microsoft Azure** -se si seleziona questa opzione, le impostazioni rimanenti hello nella finestra di dialogo hello sono disabilitate perché sono validi solo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="370df-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="370df-171">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="370df-171">Select **OK**.</span></span>
    - <span data-ttu-id="370df-172">**La sottoscrizione** : se si seleziona questa opzione, usare hello elenco a discesa elenco tooeither selezionare e accesso in un account Microsoft o aggiunta un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="370df-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="370df-173">Selezionare una sottoscrizione e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="370df-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="370df-174">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="370df-174">Select **OK**.</span></span>
    - <span data-ttu-id="370df-175">**Credenziali immesse manualmente** : immettere il nome di account di archiviazione hello e una chiave primaria o a seconda di hello.</span><span class="sxs-lookup"><span data-stu-id="370df-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="370df-176">Selezionare un'opzione per **Connessione**. Nella maggior parte dei casi è consigliato HTTPS. Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="370df-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="370df-177">Selezionare la stringa di connessione hello toodelete una stringa di connessione e quindi selezionare **Rimuovi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="370df-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="370df-178">Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="370df-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="370df-179">Accedere a una stringa di connessione a livello di codice</span><span class="sxs-lookup"><span data-stu-id="370df-179">Programmatically access a connection string</span></span>

<span data-ttu-id="370df-180">Hello passaggi seguenti viene illustrato come accedere a una stringa di connessione utilizzando il linguaggio c# tooprogrammatically.</span><span class="sxs-lookup"><span data-stu-id="370df-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="370df-181">Aggiungere il seguente hello utilizzando file di direttive tooa c# in cui si sta impostazione hello toouse:</span><span class="sxs-lookup"><span data-stu-id="370df-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="370df-182">Hello codice seguente viene illustrato un esempio di come tooaccess una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="370df-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="370df-183">Sostituire hello &lt;ConnectionStringName > segnaposto con il valore appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="370df-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="370df-184">Aggiungere impostazioni personalizzate toouse nel servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="370df-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="370df-185">Le impostazioni personalizzate nel file di configurazione del servizio hello consentono di aggiungere un nome e il valore di una stringa per una configurazione del servizio specifico.</span><span class="sxs-lookup"><span data-stu-id="370df-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="370df-186">È possibile scegliere toouse tooconfigure questa impostazione una funzionalità nel servizio cloud leggendo il valore di hello di hello impostazione e l'utilizzo di questa logica di hello toocontrol valore nel codice.</span><span class="sxs-lookup"><span data-stu-id="370df-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="370df-187">È possibile modificare questi valori di configurazione del servizio senza dovere toorebuild il pacchetto del servizio o quando è in esecuzione il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="370df-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="370df-188">Il codice può cercare notifiche in caso di modifiche di un'impostazione.</span><span class="sxs-lookup"><span data-stu-id="370df-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="370df-189">Vedere l' [Evento RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="370df-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="370df-190">È possibile aggiungere, rimuovere o modificare impostazioni personalizzate per le configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="370df-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="370df-191">Potrebbero essere necessari diversi valori per queste stringhe per configurazioni del servizio diverse.</span><span class="sxs-lookup"><span data-stu-id="370df-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="370df-192">Utilizzando un valore diverso per ogni configurazione del servizio, si non sono stringhe diverse toouse nel servizio cloud o modificare il codice quando si pubblica il tooAzure servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="370df-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="370df-193">È possibile utilizzare hello stesso nome per la stringa hello nel valore del codice e hello è diverso, in base alla configurazione di servizio hello che si seleziona quando si compila il servizio cloud o quando si esegue la pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="370df-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="370df-194">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="370df-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="370df-195">In **Esplora**, espandere il nodo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="370df-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="370df-196">In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="370df-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="370df-198">Seleziona hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="370df-198">Select hello **Settings** tab.</span></span>

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="370df-200">In hello **configurazione del servizio** elenco, selezionare hello sulla configurazione del servizio che si desidera tooupdate.</span><span class="sxs-lookup"><span data-stu-id="370df-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="370df-202">Selezionare un'impostazione personalizzata, tooadd **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="370df-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Aggiungere impostazioni personalizzate](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="370df-204">Dopo l'aggiunta di nuova impostazione hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="370df-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nuova impostazione personalizzata](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="370df-206">**Nome** -immettere il nome di hello dell'impostazione di hello.</span><span class="sxs-lookup"><span data-stu-id="370df-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="370df-207">**Tipo** : selezionare questa opzione **stringa** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="370df-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="370df-208">**Valore** -immettere il valore di hello dell'impostazione di hello.</span><span class="sxs-lookup"><span data-stu-id="370df-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="370df-209">È possibile immettere il valore di hello direttamente in hello **valore** cella o hello selezionare i puntini di sospensione (…) tooenter hello valore hello **Modifica stringa** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="370df-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="370df-210">toodelete un'impostazione personalizzata, selezionare l'impostazione di hello e quindi selezionare **Rimuovi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="370df-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="370df-211">Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="370df-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="370df-212">Accedere al valore dell'impostazione personalizzata a livello di codice</span><span class="sxs-lookup"><span data-stu-id="370df-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="370df-213">Hello passaggi seguenti viene illustrato come accedere a un'impostazione personalizzata in c# tooprogrammatically.</span><span class="sxs-lookup"><span data-stu-id="370df-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="370df-214">Aggiungere il seguente hello utilizzando file di direttive tooa c# in cui si sta impostazione hello toouse:</span><span class="sxs-lookup"><span data-stu-id="370df-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="370df-215">Hello codice seguente viene illustrato un esempio di come tooaccess un'impostazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="370df-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="370df-216">Sostituire hello &lt;SettingName > segnaposto con il valore appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="370df-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="370df-217">Gestire le risorse di archiviazione locali per ogni istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="370df-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="370df-218">È possibile aggiungere una risorsa di archiviazione del file system locale per ogni istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="370df-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="370df-219">Hello i dati memorizzati nell'archiviazione non è accessibile da altre istanze del ruolo di hello per cui hello dati vengono archiviati o da altri ruoli.</span><span class="sxs-lookup"><span data-stu-id="370df-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="370df-220">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="370df-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="370df-221">In **Esplora**, espandere il nodo di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="370df-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="370df-222">In hello **ruoli** nodo, pulsante destro del mouse sul ruolo hello desiderato tooupdate e, selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="370df-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="370df-224">Seleziona hello **archiviazione locale** scheda.</span><span class="sxs-lookup"><span data-stu-id="370df-224">Select hello **Local Storage** tab.</span></span>

    ![Scheda Archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="370df-226">In hello **configurazione del servizio** elenco, verificare che **tutte le configurazioni** selezionata come impostazioni di archiviazione locale hello applicano tooall configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="370df-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="370df-227">Qualsiasi altro valore comporta in tutti i campi di input hello nella pagina di hello è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="370df-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="370df-229">Selezionare una voce di archiviazione locale, tooadd **aggiungere archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="370df-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Aggiungi risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="370df-231">Dopo aver aggiunto la nuova voce archiviazione locale di hello toohello elenco, aggiornare la riga hello nell'elenco di hello con le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="370df-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nuova risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="370df-233">**Nome** -immettere il nome di hello che si desidera toouse per l'archiviazione locale nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="370df-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="370df-234">**Dimensioni (MB)** -immettere hello dimensione in MB necessaria per l'archiviazione locale nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="370df-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="370df-235">**Pulizia in riciclo ruolo** -selezionare dati opzione tooremove hello nella memoria locale nuovo hello quando hello di macchina virtuale per il ruolo di hello viene riciclato.</span><span class="sxs-lookup"><span data-stu-id="370df-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="370df-236">toodelete una voce di archiviazione locale, selezionare la voce hello e quindi selezionare **rimuovere spazio di archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="370df-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="370df-237">Da hello Visual Studio, sulla barra degli strumenti, seleziona **salvare**.</span><span class="sxs-lookup"><span data-stu-id="370df-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="370df-238">Accedere alla risorsa di archiviazione locale a livello di codice</span><span class="sxs-lookup"><span data-stu-id="370df-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="370df-239">In questa sezione viene illustrato come tooprogrammatically accedere all'archiviazione locale utilizzando c# mediante la scrittura di un file di testo test `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="370df-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="370df-240">Scrivere un'archiviazione toolocal file di testo</span><span class="sxs-lookup"><span data-stu-id="370df-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="370df-241">Hello seguente codice mostra un esempio di come un testo toowrite toolocal archiviazione di file.</span><span class="sxs-lookup"><span data-stu-id="370df-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="370df-242">Sostituire hello &lt;LocalStorageName > segnaposto con il valore appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="370df-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

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

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="370df-243">Trovare un file scritto toolocal archiviazione</span><span class="sxs-lookup"><span data-stu-id="370df-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="370df-244">file hello tooview creata dal codice hello nella sezione precedente hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="370df-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="370df-245">Nell'area di notifica Windows hello, fare doppio clic sull'icona Azure hello e, dal menu di scelta rapida hello, selezionare **Mostra interfaccia utente di emulatore di calcolo**.</span><span class="sxs-lookup"><span data-stu-id="370df-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Mostra emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="370df-247">Selezionare ruolo web hello.</span><span class="sxs-lookup"><span data-stu-id="370df-247">Select hello web role.</span></span>

    ![Emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="370df-249">In hello **emulatore di calcolo di Microsoft Azure** dal menu **strumenti** > **Apri archivio locale**.</span><span class="sxs-lookup"><span data-stu-id="370df-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Voce di menu Apri risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="370df-251">Quando si apre la finestra di Esplora hello, immettere ' MyLocalStorageTest.txt ' in hello **ricerca** casella di testo e selezionare **invio** ricerca hello toostart.</span><span class="sxs-lookup"><span data-stu-id="370df-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="370df-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="370df-252">Next steps</span></span>
<span data-ttu-id="370df-253">Per altre informazioni sui progetti Azure in Visual Studio, vedere [Configurazione di un progetto Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="370df-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="370df-254">Altre informazioni sullo schema di servizi cloud hello leggendo [riferimento allo Schema](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="370df-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

