---
title: Connettere macchine virtuali di Azure a Log Analytics | Microsoft Docs
description: "Nelle macchine virtuali Windows e Linux in esecuzione in Azure, per la raccolta di log e metriche è consigliabile installare l'estensione macchina virtuale di Azure di Log Analytics. Per installare l'estensione macchina virtuale di Log Analytics nelle VM di Azure è possibile usare il portale di Azure o PowerShell."
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
ms.openlocfilehash: cdae291b546fef4d7fdb8b067c8e4f4c9708d43f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="c19a5-104">Connettere macchine virtuali di Azure a Log Analytics con un agente Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c19a5-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="c19a5-105">Nei computer Windows e Linux, è consigliabile raccogliere log e metriche installando l'agente di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c19a5-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="c19a5-106">Il modo più semplice per installare l'agente di Log Analytics nelle VM di Azure è tramite l'estensione macchina virtuale di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c19a5-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="c19a5-107">L'uso dell'estensione macchina virtuale consente di semplificare il processo di installazione e di configurare automaticamente l'agente per l'invio di dati all'area di lavoro di Log Analytics specificata.</span><span class="sxs-lookup"><span data-stu-id="c19a5-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="c19a5-108">L'agente viene anche aggiornato automaticamente in modo da garantire la presenza delle funzionalità e delle correzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="c19a5-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="c19a5-109">Per le macchine virtuali Windows si abilita l'estensione macchina virtuale *Microsoft Monitoring Agent*.</span><span class="sxs-lookup"><span data-stu-id="c19a5-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="c19a5-110">Per le macchine virtuali Linux si abilita l'estensione macchina virtuale *dell'agente OMS per Linux*.</span><span class="sxs-lookup"><span data-stu-id="c19a5-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="c19a5-111">Altre informazioni sulle [estensioni delle macchine virtuali](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e sull'[agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c19a5-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c19a5-112">Quando si usa la raccolta basata su agenti per i dati di log, è necessario configurare le [origini dati in Log Analytics](log-analytics-data-sources.md) per specificare i log e le metriche da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="c19a5-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c19a5-113">Se si configura Log Analytics per indicizzare i dati di log usando [Diagnostica di Azure](log-analytics-azure-storage.md) e si configura l'agente per raccogliere gli stessi log, i log verranno raccolti due volte</span><span class="sxs-lookup"><span data-stu-id="c19a5-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="c19a5-114">e verranno addebitati costi per entrambe le origini dati.</span><span class="sxs-lookup"><span data-stu-id="c19a5-114">You are charged for both data sources.</span></span> <span data-ttu-id="c19a5-115">Se è installato l'agente, raccogliere i dati di log usando solo l'agente e non configurare Log Analytics per raccogliere i dati di log da Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a5-115">If you have the agent installed, then collect log data by using only the agent - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="c19a5-116">È possibile abilitare l'estensione macchina virtuale di Log Analytics in tre semplici modi:</span><span class="sxs-lookup"><span data-stu-id="c19a5-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="c19a5-117">Usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c19a5-117">By using the Azure portal</span></span>
* <span data-ttu-id="c19a5-118">Usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c19a5-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="c19a5-119">Usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c19a5-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="c19a5-120">Abilitare l'estensione macchina virtuale nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c19a5-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="c19a5-121">È possibile installare l'agente per Log Analytics e connettere la macchina virtuale di Azure in cui viene eseguito usando il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c19a5-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="c19a5-122">Per installare l'agente di Log Analytics e connettere la macchina virtuale a un'area di lavoro di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c19a5-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="c19a5-123">Accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c19a5-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="c19a5-124">Selezionare **Esplora** sul lato sinistro del portale e quindi individuare e selezionare **Log Analytics (OMS)**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="c19a5-125">Nell'elenco delle aree di lavoro di Log Analytics selezionare quella da usare con la VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a5-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![Aree di lavoro di OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="c19a5-127">In **Log analytics management** (Gestione di Log Analytics) selezionare **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="c19a5-128">![Macchine virtuali](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="c19a5-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="c19a5-129">Nell'elenco di **Macchine virtuali** selezionare la macchina virtuale in cui si vuole installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="c19a5-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="c19a5-130">Lo **stato della connessione OMS** per la VM sarà **Non connesso**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="c19a5-131">![VM non connessa](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="c19a5-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="c19a5-132">Nei dettagli relativi alla macchina virtuale selezionare **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="c19a5-133">L'agente viene automaticamente installato e configurato per l'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c19a5-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="c19a5-134">Il processo richiede alcuni minuti, durante i quali lo stato della connessione OMS visualizzato è *Connessione*.</span><span class="sxs-lookup"><span data-stu-id="c19a5-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="c19a5-135">![Connessione della VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="c19a5-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="c19a5-136">Al termine dell'installazione e della connessione dell'agente, lo stato della **connessione OMS** verrà aggiornato in **Questa area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="c19a5-137">![Connessione effettuata](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="c19a5-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="c19a5-138">Abilitare l'estensione macchina virtuale con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c19a5-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="c19a5-139">Quando si configura la macchina virtuale con PowerShell, è necessario specificare il **workspaceId**e la **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="c19a5-140">I nomi di proprietà nella configurazione json fanno distinzione **tra maiuscole e minuscole**.</span><span class="sxs-lookup"><span data-stu-id="c19a5-140">The property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="c19a5-141">L'ID e la chiave sono riportati nella pagina **Impostazioni** del portale di OMS o sono reperibili usando PowerShell come illustrato nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="c19a5-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![ID area di lavoro e chiave primaria](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="c19a5-143">I comandi per le macchine virtuali classiche di Azure e per le macchine virtuali di Resource Manager sono diversi.</span><span class="sxs-lookup"><span data-stu-id="c19a5-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="c19a5-144">Di seguito sono riportati esempi sia per le macchine virtuali classiche che per quelle di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c19a5-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="c19a5-145">Per le macchine virtuali classiche usare l'esempio di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c19a5-145">For classic virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="c19a5-146">Per le macchine virtuali Linux di Resource Manager usando l'interfaccia della riga di comando seguente</span><span class="sxs-lookup"><span data-stu-id="c19a5-146">For Resource Manager Linux VMs using the following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="c19a5-147">Per le macchine virtuali di Resource Manager usare l'esempio di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c19a5-147">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="c19a5-148">Distribuire l'estensione macchina virtuale usando un modello</span><span class="sxs-lookup"><span data-stu-id="c19a5-148">Deploy the VM extension using a template</span></span>
<span data-ttu-id="c19a5-149">Azure Resource Manager consente di creare un modello (in formato JSON) che definisce la distribuzione e la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c19a5-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="c19a5-150">Questo modello è noto come modello di Resource Manager e permette di definire la distribuzione in modo dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="c19a5-150">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="c19a5-151">Usando un modello, è possibile distribuire ripetutamente l'applicazione in tutto il ciclo di vita dell'app avendo la certezza che le risorse verranno distribuite in uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="c19a5-151">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="c19a5-152">Includendo l'agente di Log Analytics nel modello di Resource Manager è possibile accertarsi che ogni macchina virtuale sia preconfigurata per la segnalazione di dati all'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c19a5-152">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="c19a5-153">Per altre informazioni sui modelli di Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c19a5-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="c19a5-154">Di seguito è riportato un modello di Resource Manager di esempio usato per distribuire una macchina virtuale che esegue Windows e in cui è installata l'estensione Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="c19a5-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="c19a5-155">Si tratta di un modello tipico di macchina virtuale con le aggiunte seguenti:</span><span class="sxs-lookup"><span data-stu-id="c19a5-155">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="c19a5-156">Parametri workspaceId e workspaceName</span><span class="sxs-lookup"><span data-stu-id="c19a5-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="c19a5-157">Sezione di estensione di risorsa Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="c19a5-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="c19a5-158">Output per la ricerca di workspaceId e workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="c19a5-158">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
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
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
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

<span data-ttu-id="c19a5-159">È possibile distribuire un modello con il comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c19a5-159">You can deploy a template by using the following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="c19a5-160">Risoluzione dei problemi relativi all'estensione della VM di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c19a5-160">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="c19a5-161">Quando si verifica un malfunzionamento in genere si riceve un messaggio dal portale di Azure o da Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c19a5-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="c19a5-162">Accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c19a5-162">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="c19a5-163">Individuare la VM e aprire i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="c19a5-163">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="c19a5-164">Fare clic su **Estensioni** per verificare se l'estensione OMS è abilitata o disabilitata.</span><span class="sxs-lookup"><span data-stu-id="c19a5-164">Click **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![Visualizzazione dell'estensione della VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="c19a5-166">Fare clic sull'estensione *MicrosoftMonitoringAgent*(Windows) o *OmsAgentForLinux* (Linux) e visualizzare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="c19a5-166">Click the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Dettagli dell'estensione VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="c19a5-168">Risoluzione dei problemi delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="c19a5-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="c19a5-169">Se l'estensione dell'agente di macchine virtuali *Microsoft Monitoring Agent* non viene installata o non segnala dati, è possibile seguire queste procedure per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="c19a5-169">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="c19a5-170">Controllare che l'agente di macchine virtuali di Azure sia installato e funzioni correttamente seguendo la procedura descritta nell'articolo [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="c19a5-170">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="c19a5-171">È anche possibile esaminare il file di log dell'agente di macchine virtuali `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="c19a5-171">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="c19a5-172">Se il log non esiste, l'agente di macchine virtuali non è installato</span><span class="sxs-lookup"><span data-stu-id="c19a5-172">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="c19a5-173">Installare l'agente di macchine virtuali di Azure in VM classiche</span><span class="sxs-lookup"><span data-stu-id="c19a5-173">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="c19a5-174">Verificare che l'attività dell'heartbeat dell'estensione Microsoft Monitoring Agent sia in esecuzione seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c19a5-174">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="c19a5-175">Accedere alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c19a5-175">Log in to the virtual machine</span></span>
   * <span data-ttu-id="c19a5-176">Aprire Utilità di pianificazione e trovare l'attività `update_azureoperationalinsight_agent_heartbeat`</span><span class="sxs-lookup"><span data-stu-id="c19a5-176">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="c19a5-177">Verificare che l'attività sia abilitata e venga eseguita ogni minuto</span><span class="sxs-lookup"><span data-stu-id="c19a5-177">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="c19a5-178">Controllare il file di log dell'heartbeat in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="c19a5-178">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="c19a5-179">Esaminare i file di log dell'estensione macchina virtuale Microsoft Monitoring Agent in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="c19a5-179">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="c19a5-180">Verificare che la macchina virtuale possa eseguire script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="c19a5-180">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="c19a5-181">Verificare che le autorizzazioni per C:\Windows\temp non siano state modificate</span><span class="sxs-lookup"><span data-stu-id="c19a5-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="c19a5-182">Visualizzare lo stato di Microsoft Monitoring Agent digitando il comando seguente in una finestra di PowerShell con privilegi elevati nella macchina virtuale `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="c19a5-182">View the status of the Microsoft Monitoring Agent by typing the following command in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="c19a5-183">Esaminare i file di log dell'installazione di Microsoft Monitoring Agent in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="c19a5-183">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="c19a5-184">Per altre informazioni, vedere l'articolo relativo alla [risoluzione dei problemi delle estensioni Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c19a5-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="c19a5-185">Risoluzione dei problemi delle macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="c19a5-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="c19a5-186">Se l'estensione dell'agente di macchine virtuali per l'*agente OMS per Linux* non viene installata o non segnala dati, è possibile seguire queste procedure per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="c19a5-186">If the *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="c19a5-187">Se lo stato dell'estensione è *Sconosciuto*, controllare che l'agente di macchine virtuali di Azure sia installato e funzioni correttamente esaminando il relativo file di log `/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="c19a5-187">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="c19a5-188">Se il log non esiste, l'agente di macchine virtuali non è installato</span><span class="sxs-lookup"><span data-stu-id="c19a5-188">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="c19a5-189">Installare l'agente di macchine virtuali di Azure nelle VM Linux</span><span class="sxs-lookup"><span data-stu-id="c19a5-189">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="c19a5-190">Per altri stati non integri, esaminare i file di log dell'estensione macchina virtuale dell'agente OMS per Linux in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="c19a5-190">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="c19a5-191">Se lo stato dell'estensione è integro ma i dati non vengono caricati, esaminare i file di log dell'agente OMS per Linux in `/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="c19a5-191">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="c19a5-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c19a5-192">Next steps</span></span>
* <span data-ttu-id="c19a5-193">Configurare [origini dati in Log Analytics](log-analytics-data-sources.md) per specificare i log e le metriche da raccogliere.</span><span class="sxs-lookup"><span data-stu-id="c19a5-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="c19a5-194">Per raccogliere dati dalle macchine virtuali, [aggiungere soluzioni di Log Analytics dalla Raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="c19a5-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="c19a5-195">[Raccogliere dati con Diagnostica di Azure](log-analytics-azure-storage.md) per altre risorse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="c19a5-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="c19a5-196">Per i computer non inclusi in Azure è possibile installare l'agente di Log Analytics usando i metodi descritti negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="c19a5-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="c19a5-197">Connettere computer Windows a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c19a5-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="c19a5-198">Connettere computer Linux a Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c19a5-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)
