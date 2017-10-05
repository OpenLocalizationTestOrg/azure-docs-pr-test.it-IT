---
title: Creare un gateway applicazione di Azure - Modelli | Microsoft Docs
description: Questa pagina fornisce istruzioni per la creazione di un gateway applicazione di Azure usando il modello di Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="a4e19-103">Creare un gateway applicazione usando il modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4e19-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="a4e19-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4e19-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="a4e19-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="a4e19-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="a4e19-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4e19-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="a4e19-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="a4e19-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="a4e19-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a4e19-110">Fornisce richieste HTTP con routing delle prestazioni e failover tra server diversi, sia nel cloud che in locale.</span><span class="sxs-lookup"><span data-stu-id="a4e19-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="a4e19-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre.</span><span class="sxs-lookup"><span data-stu-id="a4e19-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a4e19-112">Per un elenco completo delle funzionalità supportate, vedere [Panoramica del gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4e19-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="a4e19-113">Questo articolo illustra come scaricare e modificare un modello di Azure Resource Manager esistente da GitHub e distribuire il modello da GitHub, da PowerShell e dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e19-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="a4e19-114">Se si sta distribuendo il modello di Gestione risorse di Azure direttamente da GitHub, senza alcuna modifica, andare al passaggio che illustra la distribuzione di un modello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4e19-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="a4e19-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="a4e19-115">Scenario</span></span>

<span data-ttu-id="a4e19-116">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="a4e19-116">In this scenario you will:</span></span>

* <span data-ttu-id="a4e19-117">Creare un gateway applicazione con web application firewall.</span><span class="sxs-lookup"><span data-stu-id="a4e19-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="a4e19-118">Creare una rete virtuale denominata VirtualNetwork1 con un blocco CIDR riservato 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="a4e19-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="a4e19-119">Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="a4e19-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="a4e19-120">Impostare due indirizzi IP back-end configurati in precedenza per i server Web da usare per bilanciare il carico del traffico.</span><span class="sxs-lookup"><span data-stu-id="a4e19-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="a4e19-121">In questo esempio di modello vengono usati gli indirizzi IP back-end 10.0.1.10 e 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="a4e19-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="a4e19-122">Tali impostazioni sono i parametri per il modello.</span><span class="sxs-lookup"><span data-stu-id="a4e19-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="a4e19-123">Per personalizzare il modello, è possibile modificare le regole, il listener, il protocollo SSL e altre opzioni nel file azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="a4e19-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="a4e19-125">Scaricare e comprendere il modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="a4e19-126">È possibile scaricare da GitHub il modello di Gestione risorse di Azure esistente per creare una rete virtuale e due subnet, apportare eventuali modifiche e riutilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="a4e19-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="a4e19-127">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4e19-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="a4e19-128">Passare a [Create Application Gateway with web application firewall enabled (Creare un gateway applicazione con web application firewall abilitato)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="a4e19-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="a4e19-129">Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="a4e19-130">Salvare il file in una cartella locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="a4e19-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="a4e19-131">Se si ha familiarità con i modelli di Gestione risorse di Azure, procedere al passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="a4e19-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="a4e19-132">Aprire il file salvato e visualizzare il contenuto in **parameters** nella riga</span><span class="sxs-lookup"><span data-stu-id="a4e19-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="a4e19-133">La sezione parameters del modello di Gestione risorse di Azure è un segnaposto per i valori che possono essere inseriti durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="a4e19-134">Parametro</span><span class="sxs-lookup"><span data-stu-id="a4e19-134">Parameter</span></span> | <span data-ttu-id="a4e19-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a4e19-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="a4e19-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="a4e19-136">**subnetPrefix**</span></span> |<span data-ttu-id="a4e19-137">Blocco CIDR della subnet del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="a4e19-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="a4e19-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="a4e19-139">Dimensione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-139">Size of the application gateway.</span></span>  <span data-ttu-id="a4e19-140">WAF consente solo gateway di medie e grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a4e19-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="a4e19-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="a4e19-141">**backendIpaddress1**</span></span> |<span data-ttu-id="a4e19-142">Indirizzo IP del primo server Web.</span><span class="sxs-lookup"><span data-stu-id="a4e19-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="a4e19-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="a4e19-143">**backendIpaddress2**</span></span> |<span data-ttu-id="a4e19-144">Indirizzo IP del secondo server Web.</span><span class="sxs-lookup"><span data-stu-id="a4e19-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="a4e19-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="a4e19-145">**wafEnabled**</span></span> | <span data-ttu-id="a4e19-146">Impostazione per determinare se WAF è abilitato.</span><span class="sxs-lookup"><span data-stu-id="a4e19-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="a4e19-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="a4e19-147">**wafMode**</span></span> | <span data-ttu-id="a4e19-148">Modalità di web application firewall.</span><span class="sxs-lookup"><span data-stu-id="a4e19-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="a4e19-149">Le opzioni disponibili sono **prevention** (prevenzione) e **detection** (rilevamento).</span><span class="sxs-lookup"><span data-stu-id="a4e19-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="a4e19-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="a4e19-150">**wafRuleSetType**</span></span> | <span data-ttu-id="a4e19-151">Tipo di set di regole per WAF.</span><span class="sxs-lookup"><span data-stu-id="a4e19-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="a4e19-152">Attualmente OWASP è l'unica opzione supportata.</span><span class="sxs-lookup"><span data-stu-id="a4e19-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="a4e19-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="a4e19-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="a4e19-154">Versione del set di regole.</span><span class="sxs-lookup"><span data-stu-id="a4e19-154">Ruleset version.</span></span> <span data-ttu-id="a4e19-155">Attualmente, sono supportate le opzioni OWASP CRS 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="a4e19-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="a4e19-156">Controllare il contenuto in **resources** e prendere nota delle proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a4e19-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="a4e19-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-157">**type**.</span></span> <span data-ttu-id="a4e19-158">Tipo di risorsa che sarà creato dal modello.</span><span class="sxs-lookup"><span data-stu-id="a4e19-158">Type of resource being created by the template.</span></span> <span data-ttu-id="a4e19-159">In questo caso il tipo è `Microsoft.Network/applicationGateways`, che rappresenta un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="a4e19-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-160">**name**.</span></span> <span data-ttu-id="a4e19-161">Nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="a4e19-161">Name for the resource.</span></span> <span data-ttu-id="a4e19-162">Si noti l'uso di `[parameters('applicationGatewayName')]`, che indica che il nome viene specificato come input dell'utente o di un file di parametri durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="a4e19-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-163">**properties**.</span></span> <span data-ttu-id="a4e19-164">Elenco di proprietà per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="a4e19-164">List of properties for the resource.</span></span> <span data-ttu-id="a4e19-165">Questo modello usa la rete virtuale e l'indirizzo IP pubblico durante la creazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a4e19-166">Per altre informazioni sui modelli, visitare la pagina [Resource Manager templates reference (Riferimenti ai modelli di Resource Manager)](/templates/)</span><span class="sxs-lookup"><span data-stu-id="a4e19-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="a4e19-167">Tornare a [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="a4e19-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="a4e19-168">Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="a4e19-169">Salvare il file in una cartella locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="a4e19-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="a4e19-170">Aprire il file salvato e modificare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="a4e19-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="a4e19-171">Usare i valori riportati di seguito per la distribuzione del gateway applicazione descritto in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="a4e19-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="a4e19-172">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="a4e19-172">Save the file.</span></span> <span data-ttu-id="a4e19-173">È possibile testare il modello JSON e il modello di parametri usando strumenti online di convalida di JSON come [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="a4e19-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="a4e19-174">Distribuire il modello di Gestione risorse di Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4e19-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="a4e19-175">Se è la prima volta che si usa Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni per accedere ad Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a4e19-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="a4e19-176">Accesso a PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4e19-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="a4e19-177">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="a4e19-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="a4e19-178">Verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="a4e19-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="a4e19-179">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="a4e19-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="a4e19-180">Se necessario, creare un gruppo di risorse usando il cmdlet **New-AzureResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="a4e19-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="a4e19-181">Nell'esempio seguente viene creato un nuovo gruppo di risorse denominato AppgatewayRG nella località Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="a4e19-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="a4e19-182">Eseguire il cmdlet **New-AzureRmResourceGroupDeployment** per distribuire la nuova rete virtuale usando il modello e i file di parametri scaricati e modificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a4e19-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="a4e19-183">Distribuire il modello di Gestione risorse di Azure usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="a4e19-184">Per distribuire il modello di Azure Resource Manager scaricato usando l'interfaccia della riga di comando di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4e19-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="a4e19-185">Se è la prima volta che si usa l'interfaccia della riga di comando di Azure, vedere [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e19-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="a4e19-186">Se necessario, eseguire il comando `az group create` per creare un nuovo gruppo di risorse, come illustrato nel frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="a4e19-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="a4e19-187">Si noti l'output del comando.</span><span class="sxs-lookup"><span data-stu-id="a4e19-187">Notice the output of the command.</span></span> <span data-ttu-id="a4e19-188">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="a4e19-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="a4e19-189">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4e19-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="a4e19-190">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-190">**-n (or --name)**.</span></span> <span data-ttu-id="a4e19-191">Nome del nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4e19-191">Name for the new resource group.</span></span> <span data-ttu-id="a4e19-192">Per questo scenario, *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="a4e19-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="a4e19-193">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-193">**-l (or --location)**.</span></span> <span data-ttu-id="a4e19-194">Area di Azure in cui viene creato il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a4e19-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="a4e19-195">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="a4e19-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="a4e19-196">Eseguire il cmdlet `az group deployment create` per distribuire la nuova rete virtuale usando il modello e i file di parametri scaricati e modificati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="a4e19-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="a4e19-197">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="a4e19-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="a4e19-198">Distribuire il modello di Gestione risorse di Azure usando il pulsante per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a4e19-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="a4e19-199">Il pulsante per la distribuzione offre un altro modo per usare i modelli di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e19-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="a4e19-200">Questo è un modo semplice di usare i modelli con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4e19-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="a4e19-201">Andare a [Creare un gateway applicazione con web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="a4e19-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="a4e19-202">Fare clic su **Distribuzione in Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-202">Click **Deploy to Azure**.</span></span>

    ![Distribuzione in Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="a4e19-204">Inserire i parametri per il modello di distribuzione nel portale e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Parametri](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="a4e19-206">Selezionare **Accetto le condizioni riportate sopra** e quindi fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="a4e19-207">Nel pannello Distribuzione personalizzata fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a4e19-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="a4e19-208">Fornire i dati certificato ai modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4e19-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="a4e19-209">Quando si usa SSL con un modello, il certificato deve essere fornito in una stringa base64 anziché essere caricato.</span><span class="sxs-lookup"><span data-stu-id="a4e19-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="a4e19-210">Per convertire un formato PFX o CER in una stringa base64, usare uno dei comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a4e19-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="a4e19-211">I comandi seguenti convertono il certificato in una stringa base64 che può essere assegnata al modello.</span><span class="sxs-lookup"><span data-stu-id="a4e19-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="a4e19-212">L'output previsto è una stringa che può essere archiviata in una variabile e incollata nel modello.</span><span class="sxs-lookup"><span data-stu-id="a4e19-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="a4e19-213">macOS</span><span class="sxs-lookup"><span data-stu-id="a4e19-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="a4e19-214">Windows</span><span class="sxs-lookup"><span data-stu-id="a4e19-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="a4e19-215">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="a4e19-215">Delete all resources</span></span>

<span data-ttu-id="a4e19-216">Per eliminare tutte le risorse create durante l'esecuzione dell'esercizio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="a4e19-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="a4e19-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4e19-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="a4e19-218">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="a4e19-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4e19-219">Next steps</span></span>

<span data-ttu-id="a4e19-220">Per configurare l'offload SSL, visitare [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="a4e19-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a4e19-221">Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, visitare [Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="a4e19-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="a4e19-222">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="a4e19-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="a4e19-223">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a4e19-224">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="a4e19-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

