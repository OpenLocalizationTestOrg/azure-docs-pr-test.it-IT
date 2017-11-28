---
title: aaaCreate Hadoop cluster utilizzando modelli - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come cluster toocreate per HDInsight utilizzando modelli di gestione risorse
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="a3e24-103">Creare cluster Hadoop in HDInsight mediante modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3e24-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a3e24-104">In questo articolo vengono modi toocreate Azure HDInsight cluster con i modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e24-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="a3e24-105">Per altre informazioni, vedere [Distribuire un'applicazione con il modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="a3e24-106">toolearn su altri strumenti di creazione del cluster e le funzionalità, fare clic su selettore scheda hello in primo piano hello di questa pagina o vedere [metodi di creazione del Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="a3e24-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3e24-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a3e24-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a3e24-108">istruzioni di hello toofollow in questo articolo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="a3e24-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="a3e24-109">Una [sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a3e24-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="a3e24-110">Azure PowerShell e/o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e24-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="a3e24-111">Modelli di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="a3e24-111">Resource Manager templates</span></span>
<span data-ttu-id="a3e24-112">Un modello di gestione risorse rende facile toocreate hello seguenti per l'applicazione in un'operazione singola, coordinata:</span><span class="sxs-lookup"><span data-stu-id="a3e24-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="a3e24-113">Cluster HDInsight e le relative risorse dipendenti (ad esempio account di archiviazione predefinito hello)</span><span class="sxs-lookup"><span data-stu-id="a3e24-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="a3e24-114">Altre risorse (ad esempio, Database SQL di Azure toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="a3e24-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="a3e24-115">Nel modello di hello, definire le risorse hello necessarie per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="a3e24-116">È inoltre possibile specificare i valori tooinput i parametri di distribuzione per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="a3e24-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="a3e24-117">modello Hello è costituito da JSON ed espressioni si utilizzano valori tooconstruct per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a3e24-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="a3e24-118">È possibile trovare modelli di HDInsight di esempio in [Modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="a3e24-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="a3e24-119">Utilizzare multipiattaforma [codice di Visual Studio](https://code.visualstudio.com/#alt-downloads) con hello [estensione Gestione risorse](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o un modello hello toosave editor di testo in un file nella workstation.</span><span class="sxs-lookup"><span data-stu-id="a3e24-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="a3e24-120">Viene illustrato come toocall hello modello utilizzando metodi diversi.</span><span class="sxs-lookup"><span data-stu-id="a3e24-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="a3e24-121">Per ulteriori informazioni sui modelli di gestione delle risorse, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="a3e24-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="a3e24-122">Creazione di modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a3e24-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="a3e24-123">Distribuire un'applicazione con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a3e24-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="a3e24-124">Generare modelli</span><span class="sxs-lookup"><span data-stu-id="a3e24-124">Generate templates</span></span>

<span data-ttu-id="a3e24-125">Utilizzando hello portale di Azure, è possibile configurare tutte le proprietà di hello di un cluster e quindi salvare il modello di hello prima di distribuirlo.</span><span class="sxs-lookup"><span data-stu-id="a3e24-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="a3e24-126">È quindi possibile riutilizzare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-126">You can then reuse hello template.</span></span>

<span data-ttu-id="a3e24-127">**un modello usando il portale di Azure hello toogenerate**</span><span class="sxs-lookup"><span data-stu-id="a3e24-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="a3e24-128">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3e24-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a3e24-129">Fare clic su **New** scegliere dal menu a sinistra, hello **Intelligence + analitica**, quindi fare clic su **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a3e24-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="a3e24-130">Seguono hello istruzioni tooenter proprietà.</span><span class="sxs-lookup"><span data-stu-id="a3e24-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="a3e24-131">È possibile utilizzare entrambi hello **creazione rapida** o hello **personalizzato** opzione.</span><span class="sxs-lookup"><span data-stu-id="a3e24-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="a3e24-132">In hello **riepilogo** scheda, fare clic su **Scarica modello e i parametri**:</span><span class="sxs-lookup"><span data-stu-id="a3e24-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="a3e24-134">Verrà visualizzato un elenco di file di modello hello, file dei parametri e modello di codice campioni utilizzati toodeploy hello:</span><span class="sxs-lookup"><span data-stu-id="a3e24-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![Opzioni di download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="a3e24-136">Da qui, si può scaricare il modello di hello, salvarlo tooyour libreria di modelli o distribuire il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="a3e24-137">Fare clic su un modello nella libreria, tooaccess **più servizi** dal menu a sinistra di hello e quindi fare clic su **modelli** (in hello **altri** categoria).</span><span class="sxs-lookup"><span data-stu-id="a3e24-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="a3e24-138">file di modello e i parametri di Hello deve essere usato insieme.</span><span class="sxs-lookup"><span data-stu-id="a3e24-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="a3e24-139">in caso contrario, è possibile che si ottengano risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="a3e24-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="a3e24-140">Ad esempio, hello predefinito **clusterKind** valore della proprietà è sempre **hadoop**, nonostante ciò che si specifica prima di scaricare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="a3e24-141">Distribuire con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3e24-141">Deploy with PowerShell</span></span>

<span data-ttu-id="a3e24-142">La procedura seguente consente di creare un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3e24-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="a3e24-143">Salvare il file JSON di hello in hello [appendice](#appx-a-arm-template) tooyour workstation.</span><span class="sxs-lookup"><span data-stu-id="a3e24-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="a3e24-144">In uno script di PowerShell hello, il nome di file hello è `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="a3e24-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="a3e24-145">Se necessario, impostare hello parametri e variabili.</span><span class="sxs-lookup"><span data-stu-id="a3e24-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="a3e24-146">Eseguire il modello di hello usando hello lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a3e24-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="a3e24-147">script di PowerShell Hello configura solo il nome di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="a3e24-148">nome account di archiviazione Hello è hardcoded nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="a3e24-149">Si è password utente della richiesta tooenter hello cluster.</span><span class="sxs-lookup"><span data-stu-id="a3e24-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="a3e24-150">(nome utente predefinito hello **admin**.) Si è anche richiesta tooenter password dell'utente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="a3e24-151">(nome utente SSH predefinito di hello **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="a3e24-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="a3e24-152">Per altre informazioni, vedere [Distribuire con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="a3e24-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="a3e24-153">Eseguire la distribuzione con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="a3e24-153">Deploy with CLI</span></span>
<span data-ttu-id="a3e24-154">Hello seguente esempio Usa Azure interfaccia della riga di comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="a3e24-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="a3e24-155">Vengono creati un cluster e i relativi account di archiviazione e contenitore dipendenti chiamando un modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="a3e24-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="a3e24-156">Si è tooenter richiesta:</span><span class="sxs-lookup"><span data-stu-id="a3e24-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="a3e24-157">nome del cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-157">hello cluster name.</span></span>
* <span data-ttu-id="a3e24-158">password dell'utente cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-158">hello cluster user password.</span></span> <span data-ttu-id="a3e24-159">(nome utente predefinito hello **admin**.)</span><span class="sxs-lookup"><span data-stu-id="a3e24-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="a3e24-160">password dell'utente SSH Hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-160">hello SSH user password.</span></span> <span data-ttu-id="a3e24-161">(nome utente SSH predefinito di hello **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="a3e24-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="a3e24-162">Hello seguente di codice sono disponibili parametri inline:</span><span class="sxs-lookup"><span data-stu-id="a3e24-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="a3e24-163">Distribuire con hello API REST</span><span class="sxs-lookup"><span data-stu-id="a3e24-163">Deploy with hello REST API</span></span>
<span data-ttu-id="a3e24-164">Vedere [Distribuisci con hello API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="a3e24-165">Distribuire con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3e24-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="a3e24-166">Usare Visual Studio toocreate un progetto di gruppo di risorse e distribuirlo tooAzure tramite interfaccia utente di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="a3e24-167">Selezionare il tipo di hello di tooinclude risorse nel progetto.</span><span class="sxs-lookup"><span data-stu-id="a3e24-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="a3e24-168">Tali risorse vengono aggiunti automaticamente il modello di gestione risorse di toohello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="a3e24-169">progetto di Hello fornisce anche un modello di hello toodeploy script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3e24-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="a3e24-170">Per un'introduzione toousing Visual Studio con gruppi di risorse, vedere [creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="a3e24-171">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a3e24-171">Troubleshoot</span></span>

<span data-ttu-id="a3e24-172">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="a3e24-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3e24-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3e24-173">Next steps</span></span>
<span data-ttu-id="a3e24-174">In questo articolo sono state fornite diverse modi toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a3e24-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="a3e24-175">toolearn informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="a3e24-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="a3e24-176">Per un esempio di distribuzione delle risorse tramite una libreria client .NET di hello, vedere [distribuire le risorse tramite librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3e24-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a3e24-177">Per un esempio dettagliato di distribuzione di un'applicazione, vedere [Effettuare il provisioning di microservizi e distribuirli in modo prevedibile in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="a3e24-178">Per istruzioni sulla distribuzione negli ambienti toodifferent soluzione, vedere [gli ambienti di sviluppo e test in Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="a3e24-179">toolearn sulle sezioni hello del modello di gestione risorse di Azure hello, vedere [creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a3e24-180">Per un elenco di funzioni hello è possibile utilizzare un modello di gestione risorse di Azure, vedere [funzioni di modello](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="a3e24-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="a3e24-181">Appendice: Gestione risorse modello toocreate un cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3e24-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="a3e24-182">Hello seguente modello di gestione risorse di Azure crea un cluster Hadoop basati su Linux con hello dipendenti account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e24-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="a3e24-183">L'esempio include informazioni di configurazione per il metastore Hive e il metastore Oozie.</span><span class="sxs-lookup"><span data-stu-id="a3e24-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="a3e24-184">Rimuovere la sezione hello o configurare sezione hello prima di usare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="a3e24-185">Appendice: Gestione risorse modello toocreate un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="a3e24-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="a3e24-186">In questa sezione fornisce un modello di gestione risorse che è possibile utilizzare un cluster HDInsight Spark toocreate.</span><span class="sxs-lookup"><span data-stu-id="a3e24-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="a3e24-187">Questo modello include le configurazioni per `spark-defaults` e `spark-thrift-sparkconf` (per i cluster Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (per i cluster Spark 2).</span><span class="sxs-lookup"><span data-stu-id="a3e24-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="a3e24-188">Inoltre, toothis HDInsight calcola e imposta le configurazioni, ad esempio `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` in base alle dimensioni di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a3e24-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="a3e24-189">Se si imposta alcun un parametro in una sezione come parte del modello hello, HDInsight non calcolare e impostare hello altri parametri di hello stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="a3e24-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="a3e24-190">Ad esempio, parametro `spark.executor.instances` in hello `spark-defaults` configurazione.</span><span class="sxs-lookup"><span data-stu-id="a3e24-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="a3e24-191">Se si imposta un altro parametro (ad esempio, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configurazione, HDInsight non calcolare e impostare hello `spark.executor.instances` nonché parametro.</span><span class="sxs-lookup"><span data-stu-id="a3e24-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
