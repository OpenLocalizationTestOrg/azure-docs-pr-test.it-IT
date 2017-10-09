---
title: configurazione aaaSample per le estensioni di macchina virtuale di Windows | Documenti Microsoft
description: Configurazione di esempio per la creazione di modelli con le estensioni
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 7697be969dbcf609423f64b75c7edf80ca1bfd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a>Esempi di configurazione dell’estensione delle macchine virtuali di Microsoft Azure.
> [!div class="op_single_selector"]
> * [PowerShell - Modello](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [Interfaccia della riga di comando - Modello](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Questo articolo fornisce una configurazione di esempio per la configurazione di estensioni di macchina virtuale di Azure per macchine virtuali di Windows.

toolearn ulteriori informazioni su queste estensioni, vedere [Cenni preliminari sulle estensioni VM di Azure.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

toolearn più sulla creazione di modelli di estensione, vedere [la creazione di modelli di estensione.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Questo articolo vengono elencati i valori di configurazione previsto per alcune delle estensioni di Windows hello.

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a>Frammento di modello di esempio per le estensioni VM con VM IaaS.
Hello modello frammento di codice per la distribuzione ha un aspetto estensioni come riportato di seguito:

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a>Frammento di modello di esempio per le estensioni VM con set di scalabilità di VM.
    {
     "type":"Microsoft.Compute/virtualMachineScaleSets",
    ....
           "extensionProfile":{
           "extensions":[
             {
               "name":"extension Name",
               "properties":{
                 "publisher":"Publisher Namespace",
                 "type":"extension Name",
                 "typeHandlerVersion":"extension version",
                 "autoUpgradeMinorVersion":true,
                 "settings":{
                 // Extension specific configuration goes in here.
                 }
               }
              }
            }
          }

Prima di distribuire l'estensione hello verificare versione più recente dell'estensione hello e sostituire typeHandlerVersion"hello" con la versione più recente di hello corrente.

Articolo hello fornisce configurazioni di esempio per le estensioni VM di Windows.

Prima di distribuire l'estensione hello verificare versione più recente dell'estensione hello e sostituire typeHandlerVersion"hello" con la versione più recente di hello corrente.

### <a name="customscript-extension-14"></a>Estensione CustomScript 1.4
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a>Descrizione dei parametri:
* fileUris: elenco separati da virgole degli URL di file hello che saranno scaricati in hello VM da hello estensione. Se non si specifica alcun valore, non verrà scaricato alcun file. Se il file hello in archiviazione di Azure, hello fileURLs può essere contrassegnato come privato e hello storageAccountKey e storageAccountName corrispondente possono essere passati come parametri privati tooaccess questi file.
* commandToExecute: [parametro obbligatorio]: si tratta di comando hello che verrà eseguito dall'estensione hello.
* storageAccountName: [parametro facoltativo]: nome di Account di archiviazione per l'accesso a proprietà fileURLs hello, se sono contrassegnati come privati.
* storageAccountKey: [parametro facoltativo]: chiave Account di archiviazione per l'accesso a proprietà fileURLs hello, se sono contrassegnati come privati.

### <a name="customscript-extension-17"></a>Estensione CustomScript 1.7
Per una descrizione del parametro, fare riferimento tooCustomScript versione 1.4. La versione 1.7 introduce il supporto per l'invio di parametri di script (commandToExecute) come protectedSettings, nel qual caso i parametri vengono crittografati prima dell'invio. Il parametro 'commandToExecute' può essere specificato nelle impostazioni o in protectedSettings ma non in entrambe le posizioni.

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a>Estensione VMAccess.
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a>Estensione DSC.
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is toouse hello latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points tooAzure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference tooa member of hello Items object in hello protected settings)"
                  },
                  "ParameterOfTypePSCredential2": {
                      "UserName": "UsernameValue2",
                      "Password": "PrivateSettingsRef:Key2"
                  }
              }
          },
          "protectedSettings": {
              "Items": {
                  "Key1": "PasswordValue1",
                  "Key2": "PasswordValue2"
              },
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a>Protezione Symantec Endpoint.
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a>Agente di sicurezza Trend Micro Deep.
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter hello externally accessible DNS name or IP address of hello Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter hello port number of hello Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter hello tenant ID, which is a hyphenated, 36-character string available in hello Deployment Scripts dialog box in hello Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter hello tenant activation password, which is a hyphenated, 36-character string available in hello Deployment Scripts dialog box in hello Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter hello name or numeric ID of hello security policy defined in hello Deep Security Manager which will be applied on agent activation tooprotect this virtual machine (recommended). No security policy will be applied toohello virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a>Agente di crittografia trasparente Vormertric.
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a>Agente Enterprise puppet.
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a>Agente di monitoraggio Microsoft per le Operational Insights di Azure
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "hello Workspace ID is available from within hello Direct Agent Configuration section of hello Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "hello Workspace Key is a string that is available from within hello Direct Agent Configuration section of hello Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a>McAfee EndpointSecurity
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not tooinstall hello Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not tooinstall hello Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not tooinstall hello Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on hello local subnet tooreceive updates through this VM when they are not connected toohello internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a>IaaS Antimalware di Azure
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When tooperform hello scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a>Sicurezza dei File ESET
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a>Agente Datadog
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a>Conferisce Prevenzione da minacce avanzate e Risposta agli incidenti per Azure
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank tooregister later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a>Agente di macchine virtuali CloudLink Secure
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN tooCloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a>Agente di connettività VPN barracuda per Microsoft Azure
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of hello VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used tooencrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used tooauthenticate against hello VPN server",
              "PKCS12FilePassword" : "Password for hello file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a>Gestione Avviso Log di logica
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a>Agente Chef
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a>Diagnostica Azure
Per ulteriori informazioni sulla diagnostica tooconfigure, vedere [estensione diagnostica di Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a>Agente Tentacle di Octopus Deploy

Per ulteriori informazioni su come tooconfigure hello Polipo bendato di distribuire in Azure, vedere hello [Polipo documentazione](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) hello url toohello Octopus server portal.",
              "Environments": [ "(array of strings, required) hello environments toowhich hello Tentacle should be added." ],
              "Roles": [ "(array of strings, required) hello roles tooassign toohello Tentacle." ],
              "CommunicationMode": "(string, required) Whether hello Tentacle should wait for connections from hello server ('Listen') or should poll hello server ('Poll').",
              "Port": (int, required) hello port toolisten on for connections from hello server (in 'Listen' mode), or hello port on which tooconnect toohello Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how hello server should contact hello Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults too'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set too'Custom', hello address that hello server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) hello Machine Policy tooassign toohello Tentacle. If not specified, uses hello default Machine Policy.",
              "Tenants": [ "(array of strings, optional) hello tenants tooassign toohello Tentacle. hello tenants feature must be enabled on hello Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) hello tenant tags tooassign toohello Tentacle, in hello format 'TagSet/TagName'. hello tenants feature must be enabled on hello Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) hello Api Key toouse tooconnect toohello Octopus server."
            }
          }

Negli esempi di hello precedenti, sostituire il numero di versione di hello con numero di versione più recente di hello.

Di seguito è riportato un esempio di un modello di macchina virtuale completo con estensione dello Script personalizzato.

[Estensione di script personalizzato in una macchina virtuale Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

