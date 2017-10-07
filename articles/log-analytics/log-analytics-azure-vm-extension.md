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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Connessione di macchine virtuali di Azure tooLog Analitica con un agente di Log Analitica

Per i computer Windows e Linux, la metrica è tramite l'installazione dell'agente di Log Analitica hello hello consigliabile metodo per la raccolta di log.

Hello più semplice modo tooinstall hello Analitica Log agente in macchine virtuali di Azure è tramite hello Log Analitica estensione della macchina virtuale.  Utilizzando l'estensione hello semplifica il processo di installazione di hello e verranno configurati automaticamente hello agente toosend dati toohello Log Analitica dell'area di lavoro specificato. agente Hello inoltre viene aggiornato automaticamente, assicurarsi di disporre di funzionalità più recenti hello e correzioni.

Per le macchine virtuali Windows, si abilita hello *Microsoft Monitoring Agent* estensione della macchina virtuale.
Per le macchine virtuali Linux, si abilita hello *agente OMS per Linux* estensione della macchina virtuale.

Altre informazioni, vedere [estensioni di macchina virtuale di Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello e [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando si utilizza basato su agenti di raccolta per i dati di log, è necessario configurare [origini dati nel Log Analitica](log-analytics-data-sources.md) toospecify hello metriche che si desidera toocollect e log.

> [!IMPORTANT]
> Se si configurare dati dei log tooindex Log Analitica utilizzando [diagnostica Windows Azure](log-analytics-azure-storage.md), e si configura hello toocollect di agente hello stesso log, quindi hello log vengono raccolti due volte. e verranno addebitati costi per entrambe le origini dati. Se è installato l'agente hello, raccogliere dati di log utilizzando solo l'agente di hello - non configurare dati dei registri toocollect Log Analitica da diagnostica di Azure.
>
>

Esistono tre metodi semplici estensione della macchina virtuale tooenable hello Analitica Log:

* Tramite il portale di Azure hello
* Usando Azure PowerShell
* Usando un modello di Azure Resource Manager.

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Abilitare l'estensione della macchina virtuale nel portale di Azure hello hello
È possibile installare l'agente di hello per Log Analitica e connettersi hello macchina virtuale di Azure cui è in esecuzione utilizzando hello [portale di Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello agente Analitica di Log e la connessione dell'area di lavoro di hello macchina virtuale tooa Log Analitica
1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Selezionare **Sfoglia** su hello il lato sinistro di hello portale e quindi tornare troppo**Analitica Log (OMS)** e selezionarlo.
3. Nell'elenco delle aree di lavoro Log Analitica, selezionare hello uno che si desidera toouse con hello macchina virtuale di Azure.  
   ![Aree di lavoro di OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. In **Log analytics management** (Gestione di Log Analytics) selezionare **Macchine virtuali**.  
   ![Macchine virtuali](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Nell'elenco di hello di **macchine virtuali**, selezionare hello macchina virtuale in cui si desidera agente hello tooinstall. Hello **lo stato della connessione di OMS** per hello VM indica che si è **non connesso**.  
   ![VM non connessa](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Nei dettagli hello per la macchina virtuale, selezionare **Connetti**. agente Hello viene automaticamente installato e configurato per l'area di lavoro Log Analitica. Questo processo richiede pochi minuti, durante i quali è stato della connessione di OMS hello *connessione...*  
   ![Connessione della VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Dopo aver installato e connettere agente hello, hello **OMS connection** stato sarà aggiornato tooshow **questa area di lavoro**.  
   ![Connessione effettuata](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Abilitare l'estensione della macchina virtuale hello tramite PowerShell
Quando si configura la macchina virtuale mediante PowerShell, è necessario hello tooprovide **Idareadilavoro** e **workspaceKey**. i nomi delle proprietà Hello nella configurazione json **tra maiuscole e minuscole**.

È possibile trovare hello Id e la chiave in hello **impostazioni** pagina del portale OMS hello o usando PowerShell, come illustrato nell'esempio sopra riportato hello.

![ID area di lavoro e chiave primaria](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

I comandi per le macchine virtuali classiche di Azure e per le macchine virtuali di Resource Manager sono diversi. Di seguito sono riportati esempi sia per le macchine virtuali classiche che per quelle di Resource Manager.

Per le macchine virtuali classiche, utilizzare hello esempio PowerShell seguente:

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

Per le macchine virtuali Linux di gestione risorse utilizzando hello seguente CLI
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Per le macchine virtuali di gestione delle risorse, utilizzare hello esempio PowerShell seguente:

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>Distribuire l'estensione della macchina virtuale hello utilizzando un modello
Tramite Gestione risorse di Azure, è possibile creare un modello che definisce hello distribuzione e la configurazione dell'applicazione (in formato JSON). Questo modello è noto come modello di gestione delle risorse e fornisce una distribuzione toodefine modalità dichiarativa. Utilizzando un modello, è possibile distribuire l'applicazione in tutto il ciclo di vita di hello app ripetutamente ed essere certi che le risorse vengono distribuite in uno stato coerente.

Includendo l'agente di Log Analitica hello come parte del modello di gestione risorse, è possibile garantire che ogni macchina virtuale dell'area di lavoro di tooreport preconfigurato tooyour Analitica Log.

Per altre informazioni sui modelli di Resource Manager, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Ecco un esempio di un modello di gestione risorse che viene utilizzato per la distribuzione di una macchina virtuale che esegue Windows con estensione Microsoft Monitoring Agent installato hello. Questo modello è un modello tipico macchina virtuale, con hello le aggiunte seguenti:

* Parametri workspaceId e workspaceName
* Sezione di estensione di risorsa Microsoft.EnterpriseCloud.Monitoring
* Toolook output di hello Idareadilavoro e workspaceSharedKey

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

È possibile distribuire un modello utilizzando hello comando PowerShell seguente:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Risoluzione dei problemi di estensione della macchina virtuale di Log Analitica hello
Quando si verifica un malfunzionamento in genere si riceve un messaggio dal portale di Azure o da Azure PowerShell.

1. Sign in hello [portale di Azure](http://portal.azure.com).
2. Hello VM di individuare e aprire i dettagli di macchina virtuale.
3. Fare clic su **estensioni** toocheck se l'estensione OMS è abilitato o meno.

   ![Visualizzazione dell'estensione della VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Fare clic su hello *MicrosoftMonitoringAgent*(Windows) o *OmsAgentForLinux*(Linux) estensione e visualizzarne i dettagli. 

   ![Dettagli dell'estensione VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Risoluzione dei problemi delle macchine virtuali Windows
Se hello *Microsoft Monitoring Agent* estensione agente della macchina virtuale non è l'installazione o la creazione di report, è possibile eseguire hello problema hello tootroubleshoot di passaggi seguente.

1. Verificare se è installato l'agente VM di Azure hello e passaggi di lavoro in modo corretto tramite hello [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * È inoltre possibile rivedere i file di log dell'agente VM hello`C:\WindowsAzure\logs\WaAppAgent.log`
   * Se il log di hello non esiste, l'agente VM hello non è installato.
     * [Installare hello agente VM di Azure nelle macchine virtuali classiche](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Conferma hello Microsoft Monitoring Agent attività heartbeat di estensione viene eseguito tramite hello alla procedura seguente:
   * Log nella macchina virtuale toohello
   * Aprire l'utilità di pianificazione e trovare hello `update_azureoperationalinsight_agent_heartbeat` attività
   * Confermare l'attività hello è abilitato e sia in esecuzione ogni minuto
   * Controllare i file di registro di hello heartbeat in`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Esaminare i file di log di estensione hello macchina virtuale di Microsoft Monitoring Agent in`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Assicurarsi di macchina virtuale hello è possibile eseguire gli script di PowerShell
5. Verificare che le autorizzazioni per C:\Windows\temp non siano state modificate
6. Visualizzare lo stato di hello di Microsoft Monitoring Agent hello digitando i seguenti comandi in una finestra di PowerShell con privilegi elevato nella macchina virtuale hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Esaminare i file di log il programma di installazione di Microsoft Monitoring Agent hello in`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Per altre informazioni, vedere l'articolo relativo alla [risoluzione dei problemi delle estensioni Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Risoluzione dei problemi delle macchine virtuali Linux
Se hello *agente OMS per Linux* estensione agente della macchina virtuale non è l'installazione o la creazione di report, è possibile eseguire hello problema hello tootroubleshoot di passaggi seguente.

1. Se lo stato dell'estensione hello *sconosciuto* controllare se è installato l'agente VM di Azure hello e funzionando correttamente, esaminare il file di log dell'agente VM hello`/var/log/waagent.log`
   * Se il log di hello non esiste, l'agente VM hello non è installato.
   * [Installare hello agente VM di Azure nelle macchine virtuali Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Per gli altri Stati non integri, revisione hello agente OMS per l'estensione VM Linux file di log `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Se lo stato dell'estensione hello è integro, ma non viene caricati dati esaminare hello agente OMS per Linux i file di log in`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Passaggi successivi
* Configurare [origini dati nel Log Analitica](log-analytics-data-sources.md) toospecify hello metriche e log toocollect.
* dati toogather dalle macchine virtuali [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
* [Raccogliere dati con Diagnostica di Azure](log-analytics-azure-storage.md) per altre risorse in esecuzione in Azure.

Per i computer che non sono in Azure, è possibile installare l'agente di Log Analitica di hello utilizzando metodi hello descritti nei seguenti articoli hello:

* [Connettere i computer di Windows tooLog Analitica](log-analytics-windows-agents.md)
* [Connettersi tooLog computer Linux Analitica](log-analytics-linux-agents.md)
