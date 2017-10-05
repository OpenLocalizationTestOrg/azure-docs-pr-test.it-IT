---
title: Creare cluster Hadoop mediante modelli - Azure Microsoft Azure HDInsight | Documentazione Microsoft
description: Informazioni su come creare cluster per HDInsight usando modelli di Resource Manager
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="5906f-103">Creare cluster Hadoop in HDInsight mediante modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5906f-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="5906f-104">In questo articolo vengono illustrati diversi modi per creare cluster Azure HDInsight con modelli Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5906f-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="5906f-105">Per altre informazioni, vedere [Distribuire un'applicazione con il modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="5906f-106">Per informazioni su altri strumenti e funzionalità per la creazione di cluster, fare clic sul selettore di schede nella parte superiore della pagina o vedere [Metodi di creazione di cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="5906f-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5906f-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5906f-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="5906f-108">Per seguire le istruzioni di questo articolo sono necessari:</span><span class="sxs-lookup"><span data-stu-id="5906f-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="5906f-109">Una [sottoscrizione di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5906f-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5906f-110">Azure PowerShell e/o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5906f-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="5906f-111">Modelli di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="5906f-111">Resource Manager templates</span></span>
<span data-ttu-id="5906f-112">I modelli di Resource Manager consentono di creare quanto segue per l'applicazione in un'unica operazione coordinata:</span><span class="sxs-lookup"><span data-stu-id="5906f-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="5906f-113">Cluster HDInsight e le relative risorse dipendenti, come ad esempio l'account di archiviazione predefinito</span><span class="sxs-lookup"><span data-stu-id="5906f-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="5906f-114">Altre risorse, come ad esempio il database SQL di Azure per usare Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="5906f-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="5906f-115">Nel modello si definiscono le risorse necessarie per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5906f-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="5906f-116">È anche possibile specificare i parametri di distribuzione per immettere valori per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="5906f-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="5906f-117">Il modello è composto da JSON ed espressioni da usare per creare valori per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5906f-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="5906f-118">È possibile trovare modelli di HDInsight di esempio in [Modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="5906f-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="5906f-119">Usare lo strumento multipiattaforma [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) con l'[estensione per Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) o un editor di testo per salvare il modello in un file sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="5906f-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="5906f-120">Si apprenderà come chiamare il modello usando metodi diversi.</span><span class="sxs-lookup"><span data-stu-id="5906f-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="5906f-121">Per altre informazioni sui modelli di Resource Manager, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="5906f-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="5906f-122">Creazione di modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="5906f-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="5906f-123">Distribuire un'applicazione con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5906f-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="5906f-124">Generare modelli</span><span class="sxs-lookup"><span data-stu-id="5906f-124">Generate templates</span></span>

<span data-ttu-id="5906f-125">Tramite il portale di Azure è possibile configurare tutte le proprietà di un cluster e salvare il modello prima di distribuirlo,</span><span class="sxs-lookup"><span data-stu-id="5906f-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="5906f-126">in modo da poterlo riutilizzare.</span><span class="sxs-lookup"><span data-stu-id="5906f-126">You can then reuse the template.</span></span>

<span data-ttu-id="5906f-127">**Per generare un modello usando il portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="5906f-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="5906f-128">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5906f-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5906f-129">Fare clic su **Nuovo** nel menu a sinistra, su **Intelligence e analisi** e quindi su **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5906f-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="5906f-130">Immettere le proprietà seguendo le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="5906f-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="5906f-131">È possibile usare l'opzione **Creazione rapida** o **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="5906f-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="5906f-132">Nella scheda **Riepilogo** fare clic su **Scarica modello e parametri**:</span><span class="sxs-lookup"><span data-stu-id="5906f-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="5906f-134">Viene visualizzato l'elenco di file del modello, file dei parametri ed esempi di codice necessari per distribuire il modello:</span><span class="sxs-lookup"><span data-stu-id="5906f-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![Opzioni di download del modello di Resource Manager per la creazione del cluster HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="5906f-136">Da questa pagina è possibile scaricare il modello e salvarlo nella libreria di modelli oppure distribuirlo.</span><span class="sxs-lookup"><span data-stu-id="5906f-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="5906f-137">Per accedere a un modello nella libreria, fare clic su **Altri servizi** nel menu a sinistra e quindi fare clic su **Modelli** (nella categoria **Altro**).</span><span class="sxs-lookup"><span data-stu-id="5906f-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="5906f-138">Il modello e il file dei parametri devono essere usati insieme.</span><span class="sxs-lookup"><span data-stu-id="5906f-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="5906f-139">in caso contrario, è possibile che si ottengano risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="5906f-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="5906f-140">Il valore predefinito della proprietà **clusterKind**, ad esempio, è sempre **hadoop**, indipendentemente da quanto specificato prima di scaricare il modello.</span><span class="sxs-lookup"><span data-stu-id="5906f-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="5906f-141">Distribuire con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5906f-141">Deploy with PowerShell</span></span>

<span data-ttu-id="5906f-142">La procedura seguente consente di creare un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5906f-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="5906f-143">Salvare nella workstation il file JSON dell'[Appendice](#appx-a-arm-template).</span><span class="sxs-lookup"><span data-stu-id="5906f-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="5906f-144">Nello script di PowerShell il nome del file è `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="5906f-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="5906f-145">Se necessario, impostare i parametri e le variabili.</span><span class="sxs-lookup"><span data-stu-id="5906f-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="5906f-146">Eseguire il modello tramite lo script PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5906f-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="5906f-147">Lo script PowerShell configura soltanto il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="5906f-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="5906f-148">Il nome dell'account di archiviazione è hardcoded nel modello.</span><span class="sxs-lookup"><span data-stu-id="5906f-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="5906f-149">Viene richiesto di immettere la password utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="5906f-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="5906f-150">Il nome utente predefinito è **admin**. Viene richiesto anche di immettere la password utente SSH.</span><span class="sxs-lookup"><span data-stu-id="5906f-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="5906f-151">Il nome utente SSH predefinito è **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="5906f-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="5906f-152">Per altre informazioni, vedere [Distribuire con PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="5906f-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="5906f-153">Eseguire la distribuzione con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="5906f-153">Deploy with CLI</span></span>
<span data-ttu-id="5906f-154">Nell'esempio seguente viene usata l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5906f-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="5906f-155">Vengono creati un cluster e i relativi account di archiviazione e contenitore dipendenti chiamando un modello di Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="5906f-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="5906f-156">Viene richiesto di immettere:</span><span class="sxs-lookup"><span data-stu-id="5906f-156">You are prompted to enter:</span></span>
* <span data-ttu-id="5906f-157">Il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="5906f-157">The cluster name.</span></span>
* <span data-ttu-id="5906f-158">La password utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="5906f-158">The cluster user password.</span></span> <span data-ttu-id="5906f-159">Il nome utente predefinito è **admin**.</span><span class="sxs-lookup"><span data-stu-id="5906f-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="5906f-160">La password utente SSH.</span><span class="sxs-lookup"><span data-stu-id="5906f-160">The SSH user password.</span></span> <span data-ttu-id="5906f-161">Il nome utente SSH predefinito è **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="5906f-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="5906f-162">Il codice seguente specifica i parametri inline:</span><span class="sxs-lookup"><span data-stu-id="5906f-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="5906f-163">Distribuire con l'API REST</span><span class="sxs-lookup"><span data-stu-id="5906f-163">Deploy with the REST API</span></span>
<span data-ttu-id="5906f-164">Vedere [Distribuire con l'API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="5906f-165">Distribuire con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5906f-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="5906f-166">Usare Visual Studio per creare un progetto del gruppo di risorse e distribuirlo in Azure mediante l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="5906f-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="5906f-167">Selezionare il tipo di risorse da includere nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5906f-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="5906f-168">Tali risorse vengono aggiunte automaticamente al modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5906f-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="5906f-169">Il progetto fornisce anche uno script di PowerShell per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="5906f-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="5906f-170">Per un'introduzione all'uso di Visual Studio con gruppi di risorse, vedere [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="5906f-171">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5906f-171">Troubleshoot</span></span>

<span data-ttu-id="5906f-172">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="5906f-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5906f-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5906f-173">Next steps</span></span>
<span data-ttu-id="5906f-174">Questo articolo ha spiegato vari modi per creare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5906f-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="5906f-175">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="5906f-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="5906f-176">Per un esempio di distribuzione delle risorse tramite la libreria client .NET, vedere [Distribuire le risorse usando le librerie .NET e un modello](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5906f-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5906f-177">Per un esempio dettagliato di distribuzione di un'applicazione, vedere [Effettuare il provisioning di microservizi e distribuirli in modo prevedibile in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="5906f-178">Per indicazioni sulla distribuzione della soluzione in ambienti diversi, vedere [Ambienti di sviluppo e test in Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="5906f-179">Per informazioni sulle sezioni del modello di Azure Resource Manager, vedere [Creazione di modelli](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5906f-180">Per un elenco delle funzioni che è possibile usare in un modello di Azure Resource Manager, vedere [Funzioni di modello](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="5906f-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="5906f-181">Appendice: modello di Resource Manager per creare un cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="5906f-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="5906f-182">Il modello di Azure Resource Manager seguente crea un cluster Hadoop basato su Linux con l'account di archiviazione di Azure dipendente.</span><span class="sxs-lookup"><span data-stu-id="5906f-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="5906f-183">L'esempio include informazioni di configurazione per il metastore Hive e il metastore Oozie.</span><span class="sxs-lookup"><span data-stu-id="5906f-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="5906f-184">Prima di utilizzare il modello, rimuovere o configurare la sezione.</span><span class="sxs-lookup"><span data-stu-id="5906f-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="5906f-185">Appendice: modello di Resource Manager per creare un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="5906f-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="5906f-186">In questa sezione viene fornito un modello di Resource Manager che è possibile usare per creare un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="5906f-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="5906f-187">Questo modello include le configurazioni per `spark-defaults` e `spark-thrift-sparkconf` (per i cluster Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (per i cluster Spark 2).</span><span class="sxs-lookup"><span data-stu-id="5906f-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="5906f-188">Oltre a ciò, HDInsight calcola e imposta le configurazioni, come `spark.executor.instances`, `spark.executor.memory` e `spark.executor.cores` in base alla dimensione del cluster.</span><span class="sxs-lookup"><span data-stu-id="5906f-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="5906f-189">Se si imposta un parametro in una sezione come parte del modello stesso, HDInsight non calcola e imposta gli altri parametri della stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="5906f-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="5906f-190">Ad esempio, il parametro `spark.executor.instances` è nella configurazione `spark-defaults`.</span><span class="sxs-lookup"><span data-stu-id="5906f-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="5906f-191">Se si imposta un altro parametro (ad esempio, `spark.yarn.exector.memoryOverhead`) nella configurazione `spark-defaults`, HDInsight non calcola e imposta il parametro `spark.executor.instances`.</span><span class="sxs-lookup"><span data-stu-id="5906f-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
