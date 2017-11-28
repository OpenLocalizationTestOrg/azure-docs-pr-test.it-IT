---
title: Configurare i ruoli per un servizio cloud di Azure con Visual Studio | Documentazione Microsoft
description: Informazioni su come impostare e configurare i ruoli per i servizi cloud di Azure usando Visual Studio.
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
ms.openlocfilehash: 17da71ac0c5ab9330b9244c0354e4d161d98229e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="0c4ea-103">Configurare un ruolo per un servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c4ea-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="0c4ea-104">Un servizio cloud di Azure può includere uno o più ruoli di lavoro o ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="0c4ea-105">Per ogni ruolo è necessario definire la modalità di configurazione e configurare la modalità di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-105">For each role, you need to define how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="0c4ea-106">Per altre informazioni sui ruoli nei servizi cloud, vedere il video [Introduzione ai servizi cloud di Azure](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-106">To learn more about roles in cloud services, see the video [Introduction to Azure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="0c4ea-107">Le informazioni per il servizio cloud vengono archiviate nei file seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-107">The information for your cloud service is stored in the following files:</span></span>

- <span data-ttu-id="0c4ea-108">**ServiceDefinition.csdef** - Il file di definizione del servizio definisce le impostazioni di runtime per il servizio cloud e include i ruoli richiesti, gli endpoint e le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-108">**ServiceDefinition.csdef** - The service definition file defines the runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="0c4ea-109">Nessun dato archiviato in `ServiceDefinition.csdef` può essere modificato durante l'esecuzione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-109">None of the data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="0c4ea-110">**ServiceConfiguration.cscfg** - Il file di configurazione del servizio configura il numero delle istanze di un ruolo che vengono eseguite e i valori delle impostazioni definiti per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-110">**ServiceConfiguration.cscfg** - The service configuration file configures how many instances of a role are run and the values of the settings defined for a role.</span></span> <span data-ttu-id="0c4ea-111">I dati archiviati in `ServiceConfiguration.cscfg` possono essere modificati durante l'esecuzione del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-111">The data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="0c4ea-112">Per archiviare valori diversi per le impostazioni che controllano l'esecuzione del ruolo, è possibile creare più configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-112">To store different values for the settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="0c4ea-113">È possibile usare una configurazione del servizio diversa per ogni ambiente di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="0c4ea-114">Ad esempio, è possibile configurare la stringa di connessione dell'account di archiviazione in modo che usi l'emulatore di archiviazione di Azure locale in una configurazione del servizio locale e creare un'altra configurazione del servizio in modo che usi l'archiviazione di Azure nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-114">For example, you can set your storage account connection string to use the local Azure storage emulator in a local service configuration and create another service configuration to use Azure storage in the cloud.</span></span>

<span data-ttu-id="0c4ea-115">Quando si crea un servizio cloud in Visual Studio, vengono automaticamente create due configurazioni del servizio che sono poi aggiunte al progetto Azure:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added to your Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="0c4ea-116">Configurare un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="0c4ea-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="0c4ea-117">È possibile configurare un servizio cloud di Azure da Esplora soluzioni in Visual Studio, come illustrato nella procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in the following steps:</span></span>

1. <span data-ttu-id="0c4ea-118">Creare o aprire un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0c4ea-119">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-119">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
    ![Menu di scelta rapida di Esplora soluzioni](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="0c4ea-121">Nella pagina delle proprietà del progetto, selezionare la scheda **Sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-121">In the project's properties page, select the **Development** tab.</span></span> 

    ![Pagina delle proprietà del progetto - Scheda Sviluppo](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="0c4ea-123">Nell'elenco **Configurazione del servizio** scegliere il nome della configurazione del servizio da modificare.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-123">In the **Service Configuration** list, select the name of the service configuration that you want to edit.</span></span> <span data-ttu-id="0c4ea-124">Per apportare modifiche a tutte le configurazioni del servizio per questo ruolo, è possibile scegliere **Tutte le configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-124">(If you want to make changes to all the service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="0c4ea-125">Se si sceglie una configurazione del servizio specifica, alcune proprietà verranno disabilitate perché possono essere impostate solo per tutte le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="0c4ea-126">Per modificare queste proprietà, è necessario scegliere **Tutte le configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-126">To edit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Elenco Configurazione del servizio per un servizio cloud di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a><span data-ttu-id="0c4ea-128">Cambiare il numero di istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="0c4ea-128">Change the number of role instances</span></span>
<span data-ttu-id="0c4ea-129">Per migliorare le prestazioni del servizio cloud, è possibile cambiare il numero di istanze di un ruolo in esecuzione, in base al numero di utenti o al carico previsto per un ruolo specifico.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-129">To improve the performance of your cloud service, you can change the number of instances of a role that are running, based on the number of users or the load expected for a particular role.</span></span> <span data-ttu-id="0c4ea-130">Una macchina virtuale separata viene creata per ogni istanza di un ruolo quando il servizio cloud è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-130">A separate virtual machine is created for each instance of a role when the cloud service runs in Azure.</span></span> <span data-ttu-id="0c4ea-131">Ciò influirà sulla fatturazione per la distribuzione di questo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-131">This affects the billing for the deployment of this cloud service.</span></span> <span data-ttu-id="0c4ea-132">Per altre informazioni sulla fatturazione, vedere l'argomento contenente [informazioni sulla fatturazione per Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="0c4ea-133">Creare o aprire un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0c4ea-134">In **Esplora soluzioni** espandere il nodo del progetto.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-134">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="0c4ea-135">Nel nodo **Ruoli**, fare clic con il pulsante destro del mouse sul ruolo da aggiornare e selezionare **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-135">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="0c4ea-137">Scegliere la scheda **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-137">Select the **Configuration** tab.</span></span>

    ![Scheda Configurazione](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="0c4ea-139">Nell'elenco **Configurazione servizio** scegliere la configurazione del servizio da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-139">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>
   
    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="0c4ea-141">Nella casella di testo **Conteggio istanze** immettere il numero di istanze da avviare per questo ruolo.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-141">In the **Instance count** text box, enter the number of instances that you want to start for this role.</span></span> <span data-ttu-id="0c4ea-142">Quando il servizio cloud viene pubblicato in Azure, ogni istanza viene eseguita in una macchina virtuale diversa.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-142">Each instance runs on a separate virtual machine when you publish the cloud service to Azure.</span></span>

    ![Aggiornamento del conteggio istanze](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="0c4ea-144">Dalla barra degli strumenti di Visual Studio selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-144">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="0c4ea-145">Gestire le stringhe di connessione per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0c4ea-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="0c4ea-146">È possibile aggiungere, rimuovere o modificare le stringhe di connessione per le configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="0c4ea-147">Ad esempio, è possibile che si voglia creare una stringa di connessione locale per una configurazione del servizio locale con valore `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="0c4ea-148">È anche possibile che si voglia definire una configurazione del servizio cloud che usa un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-148">You might also want to configure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="0c4ea-149">Quando si immettono le informazioni chiave dell'account di archiviazione di Azure per una stringa di connessione dell'account di archiviazione, tali informazioni vengono archiviate localmente nel file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-149">When you enter the Azure storage account key information for a storage account connection string, this information is stored locally in the service configuration file.</span></span> <span data-ttu-id="0c4ea-150">Queste informazioni, tuttavia, non vengono attualmente archiviate come testo crittografato.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="0c4ea-151">Se si usa un valore diverso per ogni configurazione del servizio, non sarà necessario usare stringhe di connessione diverse nel servizio cloud o modificare il codice quando si pubblica il servizio cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-151">By using a different value for each service configuration, you do not have to use different connection strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="0c4ea-152">È possibile usare lo stesso nome per la stringa di connessione nel codice e il valore sarà diverso in base alla configurazione del servizio selezionata quando si compila il servizio cloud o quando lo si pubblica.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-152">You can use the same name for the connection string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="0c4ea-153">Creare o aprire un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0c4ea-154">In **Esplora soluzioni** espandere il nodo del progetto.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-154">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="0c4ea-155">Nel nodo **Ruoli**, fare clic con il pulsante destro del mouse sul ruolo da aggiornare e selezionare **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-155">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="0c4ea-157">Fare clic sulla scheda **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-157">Select the **Settings** tab.</span></span>

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="0c4ea-159">Nell'elenco **Configurazione servizio** scegliere la configurazione del servizio da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-159">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Service Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="0c4ea-161">Per aggiungere una stringa di connessione, scegliere **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-161">To add a connection string, select **Add Setting**.</span></span>

    ![Aggiungere una stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="0c4ea-163">Dopo aver aggiunto la nuova impostazione all'elenco, aggiornare la riga nell'elenco con le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-163">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nuova stringa di connessione](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="0c4ea-165">**Nome**: digitare il nome da usare per la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-165">**Name** - Enter the name that you want to use for the connection string.</span></span>
    - <span data-ttu-id="0c4ea-166">**Tipo**: scegliere **Stringa di connessione** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-166">**Type** - Select **Connection String** from the drop-down list.</span></span>
    - <span data-ttu-id="0c4ea-167">**Valore**: è possibile immettere la stringa di connessione direttamente nella cella **Valore** o selezionare i puntini di sospensione (...) per lavorare nella finestra di dialogo **Crea stringa di connessione a risorsa di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-167">**Value** - You can either enter the connection string directly into the **Value** cell, or select the ellipsis (...) to work in the **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="0c4ea-168">Nella finestra di dialogo **Crea stringa di connessione a risorsa di archiviazione**, selezionare un'opzione per **Connetti tramite**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-168">In the **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="0c4ea-169">Seguire quindi le istruzioni relative all'opzione selezionata:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-169">Then follow the instructions for the option you select:</span></span>

    - <span data-ttu-id="0c4ea-170">**Emulatore di archiviazione di Microsoft Azure**: se si seleziona questa opzione, le impostazioni rimanenti nella finestra di dialogo vengono disabilitate, poiché sono valide solo per Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-170">**Microsoft Azure storage emulator** - If you select this option, the remaining settings on the dialog are disabled as they apply only to Azure.</span></span> <span data-ttu-id="0c4ea-171">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-171">Select **OK**.</span></span>
    - <span data-ttu-id="0c4ea-172">**Sottoscrizione**: se si seleziona questa opzione, usare l'elenco a discesa per selezionare e accedere a un account Microsoft oppure aggiungere un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-172">**Your subscription** - If you select this option, use the dropdown list to either select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="0c4ea-173">Selezionare una sottoscrizione e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="0c4ea-174">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-174">Select **OK**.</span></span>
    - <span data-ttu-id="0c4ea-175">**Credenziali immesse manualmente**: immettere il nome dell'account di archiviazione e la chiave primaria o secondaria.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-175">**Manually entered credentials** - Enter the storage account name, and either the primary or second key.</span></span> <span data-ttu-id="0c4ea-176">Selezionare un'opzione per **Connessione**. Nella maggior parte dei casi è consigliato HTTPS. Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="0c4ea-177">Per eliminare una stringa di connessione, selezionarla e quindi scegliere **Rimuovi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-177">To delete a connection string, select the connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="0c4ea-178">Dalla barra degli strumenti di Visual Studio selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-178">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="0c4ea-179">Accedere a una stringa di connessione a livello di codice</span><span class="sxs-lookup"><span data-stu-id="0c4ea-179">Programmatically access a connection string</span></span>

<span data-ttu-id="0c4ea-180">La procedura seguente illustra come accedere a una stringa di connessione a livello di codice usando C#.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-180">The following steps show how to programmatically access a connection string using C#.</span></span>

1. <span data-ttu-id="0c4ea-181">Aggiungere le seguenti direttive using al file C# in cui si vuole usare l'impostazione:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-181">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="0c4ea-182">Il codice seguente è un esempio di come accedere a una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-182">The following code illustrates an example of how to access a connection string.</span></span> <span data-ttu-id="0c4ea-183">Sostituire il segnaposto &lt;ConnectionStringName > con il valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-183">Replace the &lt;ConnectionStringName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a><span data-ttu-id="0c4ea-184">Aggiungere impostazioni personalizzate da usare nel servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="0c4ea-184">Add custom settings to use in your Azure cloud service</span></span>
<span data-ttu-id="0c4ea-185">Le impostazioni personalizzate nel file di configurazione del servizio consentono di aggiungere un nome e un valore per una stringa per una configurazione del servizio specifica.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-185">Custom settings in the service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="0c4ea-186">È possibile scegliere di usare questa impostazione per configurare una funzionalità nel servizio cloud leggendo il valore dell'impostazione e usando questo valore per controllare la logica nel codice.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-186">You might choose to use this setting to configure a feature in your cloud service by reading the value of the setting and using this value to control the logic in your code.</span></span> <span data-ttu-id="0c4ea-187">È possibile cambiare questi valori della configurazione del servizio senza dovere ricompilare il pacchetto del servizio o quando il servizio cloud è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-187">You can change these service configuration values without having to rebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="0c4ea-188">Il codice può cercare notifiche in caso di modifiche di un'impostazione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="0c4ea-189">Vedere l' [Evento RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="0c4ea-190">È possibile aggiungere, rimuovere o modificare impostazioni personalizzate per le configurazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="0c4ea-191">Potrebbero essere necessari diversi valori per queste stringhe per configurazioni del servizio diverse.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="0c4ea-192">Se si usa un valore diverso per ogni configurazione del servizio, non sarà necessario usare stringhe diverse nel servizio cloud o modificare il codice quando si pubblica il servizio cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-192">By using a different value for each service configuration, you do not have to use different strings in your cloud service or modify your code when you publish your cloud service to Azure.</span></span> <span data-ttu-id="0c4ea-193">È possibile usare lo stesso nome per la stringa nel codice e il valore sarà diverso in base alla configurazione del servizio selezionata quando si compila il servizio cloud o quando lo si pubblica.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-193">You can use the same name for the string in your code and the value is different, based on the service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="0c4ea-194">Creare o aprire un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0c4ea-195">In **Esplora soluzioni** espandere il nodo del progetto.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-195">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="0c4ea-196">Nel nodo **Ruoli**, fare clic con il pulsante destro del mouse sul ruolo da aggiornare e selezionare **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-196">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="0c4ea-198">Fare clic sulla scheda **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-198">Select the **Settings** tab.</span></span>

    ![Scheda Settings](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="0c4ea-200">Nell'elenco **Configurazione servizio** scegliere la configurazione del servizio da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-200">In the **Service Configuration** list, select the service configuration that you want to update.</span></span>

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="0c4ea-202">Per aggiungere un'impostazione personalizzata, selezionare **Aggiungi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-202">To add a custom setting, select **Add Setting**.</span></span>

    ![Aggiungere impostazioni personalizzate](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="0c4ea-204">Dopo aver aggiunto la nuova impostazione all'elenco, aggiornare la riga nell'elenco con le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-204">Once the new setting has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nuova impostazione personalizzata](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="0c4ea-206">**Nome**: inserire il nome dell'impostazione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-206">**Name** - Enter the name of the setting.</span></span>
    - <span data-ttu-id="0c4ea-207">**Tipo**: scegliere **Stringa di connessione** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-207">**Type** - Select **String** from the drop-down list.</span></span>
    - <span data-ttu-id="0c4ea-208">**Valore**: inserire il valore dell'impostazione.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-208">**Value** - Enter the value of the setting.</span></span> <span data-ttu-id="0c4ea-209">È possibile immettere il valore direttamente nella cella **Valore** o selezionare i puntini di sospensione (...) per immettere il valore nella finestra di dialogo **Modifica stringa**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-209">You can either enter the value directly into the **Value** cell, or select the ellipsis (...) to enter the value in the **Edit String** dialog.</span></span>  

1. <span data-ttu-id="0c4ea-210">Per eliminare un'impostazione personalizzata, selezionarla e quindi scegliere **Rimuovi impostazione**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-210">To delete a custom setting, select the setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="0c4ea-211">Dalla barra degli strumenti di Visual Studio selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-211">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="0c4ea-212">Accedere al valore dell'impostazione personalizzata a livello di codice</span><span class="sxs-lookup"><span data-stu-id="0c4ea-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="0c4ea-213">La procedura seguente illustra come accedere a un'impostazione personalizzata a livello di codice usando C#.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-213">The following steps show how to programmatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="0c4ea-214">Aggiungere le seguenti direttive using al file C# in cui si vuole usare l'impostazione:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-214">Add the following using directives to a C# file where you are going to use the setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="0c4ea-215">Il codice seguente è un esempio di come accedere a un'impostazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-215">The following code illustrates an example of how to access a custom setting.</span></span> <span data-ttu-id="0c4ea-216">Sostituire il segnaposto &lt;SettingName> con il valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-216">Replace the &lt;SettingName> placeholder with the appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="0c4ea-217">Gestire le risorse di archiviazione locali per ogni istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="0c4ea-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="0c4ea-218">È possibile aggiungere una risorsa di archiviazione del file system locale per ogni istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="0c4ea-219">I dati archiviati nella risorsa di archiviazione non sono accessibili da altre istanze del ruolo per il quale sono archiviati, né da altri ruoli.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-219">The data stored in that storage is not accessible by other instances of the role for which the data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="0c4ea-220">Creare o aprire un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="0c4ea-221">In **Esplora soluzioni** espandere il nodo del progetto.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-221">In **Solution Explorer**, expand the project node.</span></span> <span data-ttu-id="0c4ea-222">Nel nodo **Ruoli**, fare clic con il pulsante destro del mouse sul ruolo da aggiornare e selezionare **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-222">Under the **Roles** node, right-click the role you want to update, and, from the context menu, select **Properties**.</span></span>

    ![Menu di scelta rapida di Esplora soluzioni di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="0c4ea-224">Selezionare la scheda **Risorsa di archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-224">Select the **Local Storage** tab.</span></span>

    ![Scheda Archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="0c4ea-226">Nell'elenco **Configurazione del servizio**, verificare che l'opzione selezionata sia **Tutte le configurazioni**, poiché le impostazioni di archiviazione locale si applicano a tutte le configurazioni di servizio.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-226">In the **Service Configuration** list, ensure that **All Configurations** is selected as the local storage settings apply to all service configurations.</span></span> <span data-ttu-id="0c4ea-227">Qualsiasi altro valore comporta la disabilitazione di tutti i campi di input della pagina.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-227">Any other value results in all the input fields on the page being disabled.</span></span> 

    ![Elenco Configurazione servizio](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="0c4ea-229">Per aggiungere una voce relativa a una risorsa di archiviazione locale, selezionare **Aggiungi risorsa di archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-229">To add a local storage entry, select **Add Local Storage**.</span></span>

    ![Aggiungi risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="0c4ea-231">Dopo aver aggiunto la nuova risorsa di archiviazione locale all'elenco, aggiornare la riga nell'elenco con le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-231">Once the new local storage entry has been added to the list, update the row in the list with the necessary information.</span></span>

    ![Nuova risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="0c4ea-233">**Nome**: digitare il nome da usare per la nuova risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-233">**Name** - Enter the name that you want to use for the new local storage.</span></span>
    - <span data-ttu-id="0c4ea-234">**Dimensione (MB)**: immettere la dimensione in MB necessaria per la nuova risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-234">**Size (MB)** - Enter the size in MB that you need for the new local storage.</span></span>
    - <span data-ttu-id="0c4ea-235">**Pulisci a riciclo ruolo**: selezionare questa opzione per rimuovere i dati dalla nuova risorsa di archiviazione locale quando la macchina virtuale per il ruolo viene riciclata.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-235">**Clean on role recycle** - Select this option to remove the data in the new local storage when the virtual machine for the role is recycled.</span></span>

1. <span data-ttu-id="0c4ea-236">Per eliminare una risorsa di archiviazione locale, selezionarla e scegliere **Remove Local Storage** (Rimuovi risorsa di archiviazione locale).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-236">To delete a local storage entry, select the entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="0c4ea-237">Dalla barra degli strumenti di Visual Studio selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-237">From the Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="0c4ea-238">Accedere alla risorsa di archiviazione locale a livello di codice</span><span class="sxs-lookup"><span data-stu-id="0c4ea-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="0c4ea-239">Questa sezione illustra come accedere alla risorsa di archiviazione locale a livello di codice usando C# per scrivere il file di testo di prova `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-239">This section illustrates how to programmatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-to-local-storage"></a><span data-ttu-id="0c4ea-240">Scrivere un file di testo in una risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="0c4ea-240">Write a text file to local storage</span></span>

<span data-ttu-id="0c4ea-241">Il codice seguente è un esempio di come scrivere un file di testo in una risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-241">The following code shows an example of how to write a text file to local storage.</span></span> <span data-ttu-id="0c4ea-242">Sostituire il segnaposto &lt;LocalStorageName> con il valore appropriato.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-242">Replace the &lt;LocalStorageName> placeholder with the appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a><span data-ttu-id="0c4ea-243">Trovare un file scritto in una risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="0c4ea-243">Find a file written to local storage</span></span>

<span data-ttu-id="0c4ea-244">Per visualizzare il file creato dal codice nella sezione precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0c4ea-244">To view the file created by the code in the previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="0c4ea-245">Nell'area di notifica di Windows, fare clic con il pulsante destro del mouse sull'icona di Azure e, dal menu di scelta rapida, selezionare **Show Compute Emulator UI** (Mostra interfaccia utente dell'emulatore di calcolo).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-245">In the Windows notification area, right-click the Azure icon, and, from the context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Mostra emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="0c4ea-247">Selezionare il ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-247">Select the web role.</span></span>

    ![Emulatore di calcolo di Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="0c4ea-249">Dal menu **Emulatore di calcolo di Microsoft Azure**, selezionare **Strumenti** > **Open local store** (Apri risorsa di archiviazione locale).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-249">On the **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Voce di menu Apri risorsa di archiviazione locale](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="0c4ea-251">Nella finestra di Esplora risorse visualizzata, immettere "MyLocalStorageTest.txt" nella casella di testo **Cerca** e premere **Invio** per avviare la ricerca.</span><span class="sxs-lookup"><span data-stu-id="0c4ea-251">When the Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into the **Search** text box, and select **Enter** to start the search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c4ea-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c4ea-252">Next steps</span></span>
<span data-ttu-id="0c4ea-253">Per altre informazioni sui progetti Azure in Visual Studio, vedere [Configurazione di un progetto Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="0c4ea-254">Per altre informazioni sullo schema del servizio cloud, vedere [Guida di riferimento agli schemi](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="0c4ea-254">Learn more about the cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

