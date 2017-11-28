---
title: macchine virtuali di Azure di aaaConnect tooLog Analitica | Documenti Microsoft
description: "Per Windows e Linux la metrica è installando l'estensione della macchina virtuale di Azure di Log Analitica hello macchine virtuali in esecuzione in Azure, hello consigliabile modo dei log raccolti. È possibile utilizzare hello portale di Azure o PowerShell tooinstall hello estensione Log Analitica della macchina virtuale in macchine virtuali di Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="3ee5d-104">Connessione di macchine virtuali di Azure tooLog Analitica con un agente di Log Analitica</span><span class="sxs-lookup"><span data-stu-id="3ee5d-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="3ee5d-105">Per i computer Windows e Linux, la metrica è tramite l'installazione dell'agente di Log Analitica hello hello consigliabile metodo per la raccolta di log.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="3ee5d-106">Hello più semplice modo tooinstall hello Analitica Log agente in macchine virtuali di Azure è tramite hello Log Analitica estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="3ee5d-107">Utilizzando l'estensione hello semplifica il processo di installazione di hello e verranno configurati automaticamente hello agente toosend dati toohello Log Analitica dell'area di lavoro specificato.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="3ee5d-108">agente Hello inoltre viene aggiornato automaticamente, assicurarsi di disporre di funzionalità più recenti hello e correzioni.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="3ee5d-109">Per le macchine virtuali Windows, si abilita hello *Microsoft Monitoring Agent* estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="3ee5d-110">Per le macchine virtuali Linux, si abilita hello *agente OMS per Linux* estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="3ee5d-111">Altre informazioni, vedere [estensioni di macchina virtuale di Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello e [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3ee5d-112">Quando si utilizza basato su agenti di raccolta per i dati di log, è necessario configurare [origini dati nel Log Analitica](log-analytics-data-sources.md) toospecify hello metriche che si desidera toocollect e log.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ee5d-113">Se si configurare dati dei log tooindex Log Analitica utilizzando [diagnostica Windows Azure](log-analytics-azure-storage.md), e si configura hello toocollect di agente hello stesso log, quindi hello log vengono raccolti due volte.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="3ee5d-114">e verranno addebitati costi per entrambe le origini dati.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-114">You are charged for both data sources.</span></span> <span data-ttu-id="3ee5d-115">Se è installato l'agente hello, raccogliere dati di log utilizzando solo l'agente di hello - non configurare dati dei registri toocollect Log Analitica da diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="3ee5d-116">Esistono tre metodi semplici estensione della macchina virtuale tooenable hello Analitica Log:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="3ee5d-117">Tramite il portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3ee5d-117">By using hello Azure portal</span></span>
* <span data-ttu-id="3ee5d-118">Usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ee5d-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="3ee5d-119">Usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="3ee5d-120">Abilitare l'estensione della macchina virtuale nel portale di Azure hello hello</span><span class="sxs-lookup"><span data-stu-id="3ee5d-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="3ee5d-121">È possibile installare l'agente di hello per Log Analitica e connettersi hello macchina virtuale di Azure cui è in esecuzione utilizzando hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="3ee5d-122">tooinstall hello agente Analitica di Log e la connessione dell'area di lavoro di hello macchina virtuale tooa Log Analitica</span><span class="sxs-lookup"><span data-stu-id="3ee5d-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="3ee5d-123">Sign in hello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3ee5d-124">Selezionare **Sfoglia** su hello il lato sinistro di hello portale e quindi tornare troppo**Analitica Log (OMS)** e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="3ee5d-125">Nell'elenco delle aree di lavoro Log Analitica, selezionare hello uno che si desidera toouse con hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Aree di lavoro di OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="3ee5d-127">In **Log analytics management** (Gestione di Log Analytics) selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="3ee5d-128">![Macchine virtuali](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="3ee5d-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="3ee5d-129">Nell'elenco di hello di **macchine virtuali**, selezionare hello macchina virtuale in cui si desidera agente hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="3ee5d-130">Hello **lo stato della connessione di OMS** per hello VM indica che si è **non connesso**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="3ee5d-131">![VM non connessa](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="3ee5d-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="3ee5d-132">Nei dettagli hello per la macchina virtuale, selezionare **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="3ee5d-133">agente Hello viene automaticamente installato e configurato per l'area di lavoro Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="3ee5d-134">Questo processo richiede pochi minuti, durante i quali è stato della connessione di OMS hello *connessione...*</span><span class="sxs-lookup"><span data-stu-id="3ee5d-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="3ee5d-135">![Connessione della VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="3ee5d-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="3ee5d-136">Dopo aver installato e connettere agente hello, hello **OMS connection** stato sarà aggiornato tooshow **questa area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="3ee5d-137">![Connessione effettuata](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="3ee5d-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="3ee5d-138">Abilitare l'estensione della macchina virtuale hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ee5d-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="3ee5d-139">Quando si configura la macchina virtuale mediante PowerShell, è necessario hello tooprovide **Idareadilavoro** e **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="3ee5d-140">i nomi delle proprietà Hello nella configurazione json **tra maiuscole e minuscole**.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="3ee5d-141">È possibile trovare hello Id e la chiave in hello **impostazioni** pagina del portale OMS hello o usando PowerShell, come illustrato nell'esempio sopra riportato hello.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![ID area di lavoro e chiave primaria](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="3ee5d-143">I comandi per le macchine virtuali classiche di Azure e per le macchine virtuali di Resource Manager sono diversi.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="3ee5d-144">Di seguito sono riportati esempi sia per le macchine virtuali classiche che per quelle di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="3ee5d-145">Per le macchine virtuali classiche, utilizzare hello esempio PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="3ee5d-146">Per le macchine virtuali Linux di gestione risorse utilizzando hello seguente CLI</span><span class="sxs-lookup"><span data-stu-id="3ee5d-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="3ee5d-147">Per le macchine virtuali di gestione delle risorse, utilizzare hello esempio PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="3ee5d-148">Distribuire l'estensione della macchina virtuale hello utilizzando un modello</span><span class="sxs-lookup"><span data-stu-id="3ee5d-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="3ee5d-149">Tramite Gestione risorse di Azure, è possibile creare un modello che definisce hello distribuzione e la configurazione dell'applicazione (in formato JSON).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="3ee5d-150">Questo modello è noto come modello di gestione delle risorse e fornisce una distribuzione toodefine modalità dichiarativa.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="3ee5d-151">Utilizzando un modello, è possibile distribuire l'applicazione in tutto il ciclo di vita di hello app ripetutamente ed essere certi che le risorse vengono distribuite in uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="3ee5d-152">Includendo l'agente di Log Analitica hello come parte del modello di gestione risorse, è possibile garantire che ogni macchina virtuale dell'area di lavoro di tooreport preconfigurato tooyour Analitica Log.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="3ee5d-153">Per altre informazioni sui modelli di Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3ee5d-154">Ecco un esempio di un modello di gestione risorse che viene utilizzato per la distribuzione di una macchina virtuale che esegue Windows con estensione Microsoft Monitoring Agent installato hello.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="3ee5d-155">Questo modello è un modello tipico macchina virtuale, con hello le aggiunte seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="3ee5d-156">Parametri workspaceId e workspaceName</span><span class="sxs-lookup"><span data-stu-id="3ee5d-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="3ee5d-157">Sezione di estensione di risorsa Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="3ee5d-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="3ee5d-158">Toolook output di hello Idareadilavoro e workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="3ee5d-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="3ee5d-159">È possibile distribuire un modello utilizzando hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="3ee5d-160">Risoluzione dei problemi di estensione della macchina virtuale di Log Analitica hello</span><span class="sxs-lookup"><span data-stu-id="3ee5d-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="3ee5d-161">Quando si verifica un malfunzionamento in genere si riceve un messaggio dal portale di Azure o da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="3ee5d-162">Sign in hello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3ee5d-163">Hello VM di individuare e aprire i dettagli di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="3ee5d-164">Fare clic su **estensioni** toocheck se l'estensione OMS è abilitato o meno.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Visualizzazione dell'estensione della VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="3ee5d-166">Fare clic su hello *MicrosoftMonitoringAgent*(Windows) o *OmsAgentForLinux*(Linux) estensione e visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Dettagli dell'estensione VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="3ee5d-168">Risoluzione dei problemi delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="3ee5d-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="3ee5d-169">Se hello *Microsoft Monitoring Agent* estensione agente della macchina virtuale non è l'installazione o la creazione di report, è possibile eseguire hello problema hello tootroubleshoot di passaggi seguente.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="3ee5d-170">Verificare se è installato l'agente VM di Azure hello e passaggi di lavoro in modo corretto tramite hello [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="3ee5d-171">È inoltre possibile rivedere i file di log dell'agente VM hello`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="3ee5d-172">Se il log di hello non esiste, l'agente VM hello non è installato.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="3ee5d-173">Installare hello agente VM di Azure nelle macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="3ee5d-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="3ee5d-174">Conferma hello Microsoft Monitoring Agent attività heartbeat di estensione viene eseguito tramite hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="3ee5d-175">Log nella macchina virtuale toohello</span><span class="sxs-lookup"><span data-stu-id="3ee5d-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="3ee5d-176">Aprire l'utilità di pianificazione e trovare hello `update_azureoperationalinsight_agent_heartbeat` attività</span><span class="sxs-lookup"><span data-stu-id="3ee5d-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="3ee5d-177">Confermare l'attività hello è abilitato e sia in esecuzione ogni minuto</span><span class="sxs-lookup"><span data-stu-id="3ee5d-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="3ee5d-178">Controllare i file di registro di hello heartbeat in`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="3ee5d-179">Esaminare i file di log di estensione hello macchina virtuale di Microsoft Monitoring Agent in`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="3ee5d-180">Assicurarsi di macchina virtuale hello è possibile eseguire gli script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ee5d-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="3ee5d-181">Verificare che le autorizzazioni per C:\Windows\temp non siano state modificate</span><span class="sxs-lookup"><span data-stu-id="3ee5d-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="3ee5d-182">Visualizzare lo stato di hello di Microsoft Monitoring Agent hello digitando i seguenti comandi in una finestra di PowerShell con privilegi elevato nella macchina virtuale hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="3ee5d-183">Esaminare i file di log il programma di installazione di Microsoft Monitoring Agent hello in`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="3ee5d-184">Per altre informazioni, vedere l'articolo relativo alla [risoluzione dei problemi delle estensioni Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="3ee5d-185">Risoluzione dei problemi delle macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="3ee5d-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="3ee5d-186">Se hello *agente OMS per Linux* estensione agente della macchina virtuale non è l'installazione o la creazione di report, è possibile eseguire hello problema hello tootroubleshoot di passaggi seguente.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="3ee5d-187">Se lo stato dell'estensione hello *sconosciuto* controllare se è installato l'agente VM di Azure hello e funzionando correttamente, esaminare il file di log dell'agente VM hello`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="3ee5d-188">Se il log di hello non esiste, l'agente VM hello non è installato.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="3ee5d-189">Installare hello agente VM di Azure nelle macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="3ee5d-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="3ee5d-190">Per gli altri Stati non integri, revisione hello agente OMS per l'estensione VM Linux file di log `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="3ee5d-191">Se lo stato dell'estensione hello è integro, ma non viene caricati dati esaminare hello agente OMS per Linux i file di log in`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="3ee5d-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ee5d-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ee5d-192">Next steps</span></span>
* <span data-ttu-id="3ee5d-193">Configurare [origini dati nel Log Analitica](log-analytics-data-sources.md) toospecify hello metriche e log toocollect.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="3ee5d-194">dati toogather dalle macchine virtuali [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3ee5d-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="3ee5d-195">[Raccogliere dati con Diagnostica di Azure](log-analytics-azure-storage.md) per altre risorse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="3ee5d-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="3ee5d-196">Per i computer che non sono in Azure, è possibile installare l'agente di Log Analitica di hello utilizzando metodi hello descritti nei seguenti articoli hello:</span><span class="sxs-lookup"><span data-stu-id="3ee5d-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="3ee5d-197">Connettere i computer di Windows tooLog Analitica</span><span class="sxs-lookup"><span data-stu-id="3ee5d-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="3ee5d-198">Connettersi tooLog computer Linux Analitica</span><span class="sxs-lookup"><span data-stu-id="3ee5d-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
