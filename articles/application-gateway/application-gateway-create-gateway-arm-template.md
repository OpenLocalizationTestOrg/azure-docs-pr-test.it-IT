---
title: un Gateway di applicazione di Azure - modelli aaaCreate | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate un gateway applicazione Azure utilizzando il modello di gestione risorse di Azure hello
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
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="8eb93-103">Creare un gateway applicazione utilizzando il modello di gestione risorse di Azure hello</span><span class="sxs-lookup"><span data-stu-id="8eb93-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8eb93-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="8eb93-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8eb93-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="8eb93-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="8eb93-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="8eb93-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8eb93-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="8eb93-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="8eb93-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="8eb93-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="8eb93-110">Fornisce il failover e il routing delle prestazioni delle richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="8eb93-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre.</span><span class="sxs-lookup"><span data-stu-id="8eb93-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="8eb93-112">toofind un elenco completo delle funzionalità supportate, visitare [Panoramica di Gateway applicazione](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8eb93-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="8eb93-113">In questo articolo viene illustrato il download e modifica di un modello di gestione risorse di Azure esistente da GitHub e la distribuzione modello hello da GitHub, PowerShell e hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb93-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="8eb93-114">Se si distribuiscono semplicemente il modello di Azure Resource Manager hello direttamente da GitHub senza apportare modifiche, è possibile ignorare toodeploy un modello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="8eb93-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="8eb93-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="8eb93-115">Scenario</span></span>

<span data-ttu-id="8eb93-116">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8eb93-116">In this scenario you will:</span></span>

* <span data-ttu-id="8eb93-117">Creare un gateway applicazione con web application firewall.</span><span class="sxs-lookup"><span data-stu-id="8eb93-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="8eb93-118">Creare una rete virtuale denominata VirtualNetwork1 con un blocco CIDR riservato 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="8eb93-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="8eb93-119">Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="8eb93-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="8eb93-120">Configurare due indirizzi IP back-end configurato in precedenza per i server web hello si desidera bilanciare il traffico in hello tooload.</span><span class="sxs-lookup"><span data-stu-id="8eb93-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="8eb93-121">In questo esempio di modello, hello IP back-end sono 10.0.1.10 e 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="8eb93-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="8eb93-122">Tali impostazioni sono parametri di hello per questo modello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="8eb93-123">modello di hello toocustomize, è possibile modificare le regole, i listener di hello, SSL e altre opzioni nel file azuredeploy.json hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="8eb93-125">Scaricare e comprendere il modello di Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="8eb93-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="8eb93-126">È possibile scaricare hello esistente Azure Resource Manager modello toocreate una rete virtuale e due subnet da GitHub, apportare le modifiche potrebbe essere necessario e riutilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="8eb93-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="8eb93-127">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8eb93-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="8eb93-128">Passare troppo[crea applicazioni Gateway con firewall applicazione web abilitata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="8eb93-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="8eb93-129">Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="8eb93-130">Salvare una cartella locale di hello file tooa nel computer.</span><span class="sxs-lookup"><span data-stu-id="8eb93-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="8eb93-131">Se si ha familiarità con i modelli di gestione risorse di Azure, ignorare toostep 7.</span><span class="sxs-lookup"><span data-stu-id="8eb93-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="8eb93-132">Aprire il file hello salvato ed esaminare il contenuto di hello in **parametri** nella riga</span><span class="sxs-lookup"><span data-stu-id="8eb93-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="8eb93-133">La sezione parameters del modello di Gestione risorse di Azure è un segnaposto per i valori che possono essere inseriti durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="8eb93-134">Parametro</span><span class="sxs-lookup"><span data-stu-id="8eb93-134">Parameter</span></span> | <span data-ttu-id="8eb93-135">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8eb93-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="8eb93-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="8eb93-136">**subnetPrefix**</span></span> |<span data-ttu-id="8eb93-137">Blocco CIDR per la subnet del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="8eb93-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="8eb93-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="8eb93-139">Dimensioni del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-139">Size of hello application gateway.</span></span>  <span data-ttu-id="8eb93-140">WAF consente solo gateway di medie e grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="8eb93-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="8eb93-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="8eb93-141">**backendIpaddress1**</span></span> |<span data-ttu-id="8eb93-142">Indirizzo IP del server web prima di hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="8eb93-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="8eb93-143">**backendIpaddress2**</span></span> |<span data-ttu-id="8eb93-144">Indirizzo IP del server web secondo hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="8eb93-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="8eb93-145">**wafEnabled**</span></span> | <span data-ttu-id="8eb93-146">Impostazione toodetermine se WAF è abilitata.</span><span class="sxs-lookup"><span data-stu-id="8eb93-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="8eb93-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="8eb93-147">**wafMode**</span></span> | <span data-ttu-id="8eb93-148">Modalità di hello web application firewall.</span><span class="sxs-lookup"><span data-stu-id="8eb93-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="8eb93-149">Le opzioni disponibili sono **prevention** (prevenzione) e **detection** (rilevamento).</span><span class="sxs-lookup"><span data-stu-id="8eb93-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="8eb93-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="8eb93-150">**wafRuleSetType**</span></span> | <span data-ttu-id="8eb93-151">Tipo di set di regole per WAF.</span><span class="sxs-lookup"><span data-stu-id="8eb93-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="8eb93-152">Attualmente OWASP è hello supportata solo l'opzione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="8eb93-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="8eb93-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="8eb93-154">Versione del set di regole.</span><span class="sxs-lookup"><span data-stu-id="8eb93-154">Ruleset version.</span></span> <span data-ttu-id="8eb93-155">OWASP CRS 2.2.9 e 3.0 sono attualmente opzioni hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="8eb93-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="8eb93-156">Controllare il contenuto hello **risorse** e notifica hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="8eb93-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="8eb93-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-157">**type**.</span></span> <span data-ttu-id="8eb93-158">Tipo di risorsa viene creato dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="8eb93-159">In questo caso, è di tipo hello `Microsoft.Network/applicationGateways`, che rappresenta un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="8eb93-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-160">**name**.</span></span> <span data-ttu-id="8eb93-161">Nome per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-161">Name for hello resource.</span></span> <span data-ttu-id="8eb93-162">Avviso hello utilizzo di `[parameters('applicationGatewayName')]`, significa che tale nome hello viene fornito come input dall'utente o da un file dei parametri durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="8eb93-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-163">**properties**.</span></span> <span data-ttu-id="8eb93-164">Elenco di proprietà per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-164">List of properties for hello resource.</span></span> <span data-ttu-id="8eb93-165">Il modello utilizza la rete virtuale hello e indirizzo IP pubblico durante la creazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8eb93-166">Per altre informazioni sui modelli, visitare la pagina [Resource Manager templates reference (Riferimenti ai modelli di Resource Manager)](/templates/)</span><span class="sxs-lookup"><span data-stu-id="8eb93-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="8eb93-167">Passare troppo[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="8eb93-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="8eb93-168">Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="8eb93-169">Salvare una cartella locale di hello file tooa nel computer.</span><span class="sxs-lookup"><span data-stu-id="8eb93-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="8eb93-170">Aprire il file hello che è stato salvato e modificare i valori hello per i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="8eb93-171">Utilizzare hello gateway applicazione hello toodeploy valori nello scenario descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="8eb93-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="8eb93-172">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-172">Save hello file.</span></span> <span data-ttu-id="8eb93-173">È possibile testare i modelli di parametro e JSON hello utilizzando strumenti di convalida JSON online come [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="8eb93-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="8eb93-174">Distribuire il modello di gestione risorse di Azure hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eb93-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="8eb93-175">Se non si è mai usato PowerShell di Azure, visitare: [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire toosign istruzioni hello in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="8eb93-176">Account di accesso tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="8eb93-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="8eb93-177">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="8eb93-178">Si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="8eb93-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="8eb93-179">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb93-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="8eb93-180">Se necessario, creare un gruppo di risorse utilizzando hello **New AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8eb93-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="8eb93-181">Nell'esempio seguente di hello, si crea un gruppo di risorse denominato AppgatewayRG nel percorso di Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="8eb93-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="8eb93-182">Eseguire hello **New AzureRmResourceGroupDeployment** cmdlet toodeploy hello nuova rete virtuale tramite hello che precede i file di modello e sui parametri è stato scaricato e modificato.</span><span class="sxs-lookup"><span data-stu-id="8eb93-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="8eb93-183">Distribuire il modello di gestione risorse di Azure hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="8eb93-184">modello di gestione risorse di Azure hello toodeploy scaricato tramite l'interfaccia CLI di Azure, seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8eb93-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="8eb93-185">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8eb93-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="8eb93-186">Se necessario, hello esecuzione `az group create` comando toocreate un gruppo di risorse, come illustrato nel seguente frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="8eb93-187">Notare l'output di hello del comando hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-187">Notice hello output of hello command.</span></span> <span data-ttu-id="8eb93-188">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="8eb93-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="8eb93-189">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8eb93-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="8eb93-190">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-190">**-n (or --name)**.</span></span> <span data-ttu-id="8eb93-191">Nome per il nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-191">Name for hello new resource group.</span></span> <span data-ttu-id="8eb93-192">Per questo scenario, *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="8eb93-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="8eb93-193">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-193">**-l (or --location)**.</span></span> <span data-ttu-id="8eb93-194">Area di Azure in cui viene creato il nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="8eb93-195">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="8eb93-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="8eb93-196">Eseguire hello `az group deployment create` cmdlet toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato nel precedente passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="8eb93-197">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="8eb93-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="8eb93-198">Distribuire il modello di gestione risorse di Azure hello utilizzando fare clic su da distribuire</span><span class="sxs-lookup"><span data-stu-id="8eb93-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="8eb93-199">Fare clic su per la distribuzione è un altro modo toouse modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb93-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="8eb93-200">Si tratta di modelli di toouse un modo semplice con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb93-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="8eb93-201">Andare troppo[creare un gateway applicazione con firewall applicazione web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="8eb93-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="8eb93-202">Fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-202">Click **Deploy tooAzure**.</span></span>

    ![Distribuire tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="8eb93-204">Compilare i parametri di hello per il modello di distribuzione hello nel portale di hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="8eb93-206">Selezionare **accetto le condizioni indicate in precedenza toohello** e fare clic su **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="8eb93-207">Nel Pannello di distribuzione personalizzata hello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="8eb93-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="8eb93-208">Fornisce gestione modelli di certificato dati tooResource</span><span class="sxs-lookup"><span data-stu-id="8eb93-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="8eb93-209">Quando si usa SSL con un modello, certificato hello deve toobe fornito in una stringa base64 anziché in fase di caricamento.</span><span class="sxs-lookup"><span data-stu-id="8eb93-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="8eb93-210">stringa base64 pfx o CER tooa tooconvert utilizzare uno dei seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="8eb93-211">Hello seguenti comandi convertono hello certificato tooa stringa base64, che può essere fornita toohello modello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="8eb93-212">Hello è previsto output è una stringa che può essere archiviata in una variabile e incollata nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8eb93-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="8eb93-213">macOS</span><span class="sxs-lookup"><span data-stu-id="8eb93-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="8eb93-214">Windows</span><span class="sxs-lookup"><span data-stu-id="8eb93-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="8eb93-215">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="8eb93-215">Delete all resources</span></span>

<span data-ttu-id="8eb93-216">toodelete tutte le risorse create in questo articolo, completare una delle hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8eb93-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="8eb93-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eb93-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="8eb93-218">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="8eb93-219">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8eb93-219">Next steps</span></span>

<span data-ttu-id="8eb93-220">Se si desidera tooconfigure offload SSL, visitare: [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="8eb93-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="8eb93-221">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, visitare: [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="8eb93-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="8eb93-222">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="8eb93-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="8eb93-223">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="8eb93-224">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="8eb93-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

