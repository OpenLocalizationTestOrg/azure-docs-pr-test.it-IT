---
title: il modello di gestione risorse di configurazione di stato aaaDesired | Documenti Microsoft
description: Definizione del modello di Resource Manager per Desired State Configuration in Azure con esempi e risoluzione dei problemi
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="c456c-103">Set di scalabilità di macchine virtuali (VMSS) Windows e Desired State Configuration (DSC) con modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c456c-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="c456c-104">In questo articolo viene descritto il modello di gestione risorse hello per hello [gestore dell'estensione DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c456c-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="c456c-105">Esempio di modello per una VM Windows</span><span class="sxs-lookup"><span data-stu-id="c456c-105">Template example for a Windows VM</span></span>
<span data-ttu-id="c456c-106">Hello frammento seguente inseriti nella sezione delle risorse del modello di hello hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="c456c-107">Esempio di modello per set di scalabilità di macchine virtuali (VMSS) Windows</span><span class="sxs-lookup"><span data-stu-id="c456c-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="c456c-108">Un nodo VMSS ha una sezione "proprietà" con hello "VirtualMachineProfile", "extensionProfile" attributo.</span><span class="sxs-lookup"><span data-stu-id="c456c-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="c456c-109">DSC viene aggiunto sotto "extensions".</span><span class="sxs-lookup"><span data-stu-id="c456c-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="c456c-110">Informazioni dettagliate sulle impostazioni</span><span class="sxs-lookup"><span data-stu-id="c456c-110">Detailed Settings Information</span></span>
<span data-ttu-id="c456c-111">Hello nello schema seguente è per parte di impostazioni hello hello estensione DSC di Azure in un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c456c-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="c456c-112">Dettagli</span><span class="sxs-lookup"><span data-stu-id="c456c-112">Details</span></span>
| <span data-ttu-id="c456c-113">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="c456c-113">Property Name</span></span> | <span data-ttu-id="c456c-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="c456c-114">Type</span></span> | <span data-ttu-id="c456c-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c456c-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c456c-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c456c-116">settings.wmfVersion</span></span> |<span data-ttu-id="c456c-117">string</span><span class="sxs-lookup"><span data-stu-id="c456c-117">string</span></span> |<span data-ttu-id="c456c-118">Specifica la versione di hello di hello Windows Management Framework che deve essere installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c456c-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="c456c-119">L'impostazione di questa proprietà too'latest' Installa hello versione più recente WMF.</span><span class="sxs-lookup"><span data-stu-id="c456c-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="c456c-120">Hello corrente solo i valori possibili per questa proprietà sono **'4.0', '5.0', ' 5.0PP' e 'versione più recente'**.</span><span class="sxs-lookup"><span data-stu-id="c456c-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="c456c-121">Questi valori possibili sono tooupdates soggetto.</span><span class="sxs-lookup"><span data-stu-id="c456c-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="c456c-122">valore predefinito di Hello è "più di recente".</span><span class="sxs-lookup"><span data-stu-id="c456c-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="c456c-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c456c-123">settings.configuration.url</span></span> |<span data-ttu-id="c456c-124">string</span><span class="sxs-lookup"><span data-stu-id="c456c-124">string</span></span> |<span data-ttu-id="c456c-125">Specifica il percorso URL hello da cui toodownload file zip configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="c456c-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="c456c-126">Se l'URL di hello fornito richiede un token di firma di accesso condiviso per l'accesso, è necessario tooset hello protectedSettings.configurationUrlSasToken proprietà toohello valore del token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c456c-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="c456c-127">Questa proprietà è obbligatoria se settings.configuration.script e/o settings.configuration.function sono definiti.</span><span class="sxs-lookup"><span data-stu-id="c456c-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c456c-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c456c-128">settings.configuration.script</span></span> |<span data-ttu-id="c456c-129">string</span><span class="sxs-lookup"><span data-stu-id="c456c-129">string</span></span> |<span data-ttu-id="c456c-130">Specifica il nome file hello dello script hello contenente hello definizione della configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="c456c-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="c456c-131">Questo script deve trovarsi nella cartella radice di hello del file zip hello scaricato dall'URL hello specificato dalla proprietà configuration.url hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="c456c-132">Questa proprietà è obbligatoria se settings.configuration.url e/o settings.configuration.script sono definiti.</span><span class="sxs-lookup"><span data-stu-id="c456c-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="c456c-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c456c-133">settings.configuration.function</span></span> |<span data-ttu-id="c456c-134">string</span><span class="sxs-lookup"><span data-stu-id="c456c-134">string</span></span> |<span data-ttu-id="c456c-135">Specifica il nome di hello della configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="c456c-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="c456c-136">configurazione di Hello denominata deve essere contenuta nello script hello definito da configuration.script.</span><span class="sxs-lookup"><span data-stu-id="c456c-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="c456c-137">Questa proprietà è obbligatoria se settings.configuration.url e/o settings.configuration.function sono definiti.</span><span class="sxs-lookup"><span data-stu-id="c456c-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c456c-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c456c-138">settings.configurationArguments</span></span> |<span data-ttu-id="c456c-139">Raccolta</span><span class="sxs-lookup"><span data-stu-id="c456c-139">Collection</span></span> |<span data-ttu-id="c456c-140">Definisce i parametri che si desidera una configurazione di DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="c456c-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="c456c-141">Questa proprietà non è crittografata.</span><span class="sxs-lookup"><span data-stu-id="c456c-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="c456c-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c456c-142">settings.configurationData.url</span></span> |<span data-ttu-id="c456c-143">string</span><span class="sxs-lookup"><span data-stu-id="c456c-143">string</span></span> |<span data-ttu-id="c456c-144">Specifica l'URL di hello da cui toodownload i dati di configurazione (con estensione psd1) file toouse come input per la configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="c456c-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="c456c-145">Se l'URL di hello fornito richiede un token di firma di accesso condiviso per l'accesso, è necessario tooset hello protectedSettings.configurationDataUrlSasToken proprietà toohello valore del token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c456c-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="c456c-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c456c-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c456c-147">string</span><span class="sxs-lookup"><span data-stu-id="c456c-147">string</span></span> |<span data-ttu-id="c456c-148">Abilita o disabilita la raccolta di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c456c-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="c456c-149">Hello solo i valori possibili per questa proprietà sono **'Enable', 'Disable', ', o $null**.</span><span class="sxs-lookup"><span data-stu-id="c456c-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="c456c-150">Lasciando questa proprietà vuota o con valore null verrà abilitata la raccolta di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c456c-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="c456c-151">valore predefinito di Hello è '.</span><span class="sxs-lookup"><span data-stu-id="c456c-151">hello default value is ''.</span></span> [<span data-ttu-id="c456c-152">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="c456c-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="c456c-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c456c-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c456c-154">Raccolta</span><span class="sxs-lookup"><span data-stu-id="c456c-154">Collection</span></span> |<span data-ttu-id="c456c-155">Definisce i percorsi alternativi che da cui toodownload hello WMF.</span><span class="sxs-lookup"><span data-stu-id="c456c-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="c456c-156">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="c456c-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="c456c-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c456c-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c456c-158">Raccolta</span><span class="sxs-lookup"><span data-stu-id="c456c-158">Collection</span></span> |<span data-ttu-id="c456c-159">Definisce i parametri che si desidera una configurazione di DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="c456c-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="c456c-160">Questa proprietà è crittografata.</span><span class="sxs-lookup"><span data-stu-id="c456c-160">This property is encrypted.</span></span> |
| <span data-ttu-id="c456c-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c456c-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c456c-162">string</span><span class="sxs-lookup"><span data-stu-id="c456c-162">string</span></span> |<span data-ttu-id="c456c-163">Specifica URL hello tooaccess token SAS hello definito da configuration.url.</span><span class="sxs-lookup"><span data-stu-id="c456c-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="c456c-164">Questa proprietà è crittografata.</span><span class="sxs-lookup"><span data-stu-id="c456c-164">This property is encrypted.</span></span> |
| <span data-ttu-id="c456c-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c456c-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c456c-166">string</span><span class="sxs-lookup"><span data-stu-id="c456c-166">string</span></span> |<span data-ttu-id="c456c-167">Specifica URL hello tooaccess token SAS hello definito da configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="c456c-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="c456c-168">Questa proprietà è crittografata.</span><span class="sxs-lookup"><span data-stu-id="c456c-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="c456c-169">Differenze tra settings e protectedSettings</span><span class="sxs-lookup"><span data-stu-id="c456c-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="c456c-170">Tutte le impostazioni vengono salvate in un file di testo di impostazioni in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c456c-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="c456c-171">Proprietà in 'impostazioni' sono proprietà pubbliche, perché non sono crittografate nel file di testo hello impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c456c-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="c456c-172">Proprietà in 'protectedSettings' sono crittografate con un certificato e non vengono visualizzate in testo normale nel file al momento del hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c456c-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="c456c-173">Se è necessario fornire credenziali configurazione hello, possono essere inclusi nei protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="c456c-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="c456c-174">Esempio</span><span class="sxs-lookup"><span data-stu-id="c456c-174">Example</span></span>
<span data-ttu-id="c456c-175">Hello esempio deriva dalla sezione "Getting Started" hello di hello [pagina Panoramica di gestore dell'estensione DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c456c-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="c456c-176">Questo esempio Usa modelli di gestione risorse anziché cmdlet toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="c456c-177">Salvare la configurazione "IisInstall.ps1" hello, inserirlo in una. COMPRIMERE file e caricare file hello in un URL accessibile.</span><span class="sxs-lookup"><span data-stu-id="c456c-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="c456c-178">In questo esempio viene utilizzata l'archiviazione blob di Azure, ma è possibile toodownload. File ZIP da qualsiasi posizione arbitraria.</span><span class="sxs-lookup"><span data-stu-id="c456c-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="c456c-179">Nel modello di gestione risorse di Azure hello, hello codice riportato di seguito indica al file corretto hello toodownload VM hello ed eseguire la funzione di PowerShell appropriato hello:</span><span class="sxs-lookup"><span data-stu-id="c456c-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="c456c-180">L'aggiornamento da hello formato precedente</span><span class="sxs-lookup"><span data-stu-id="c456c-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="c456c-181">Le impostazioni in hello formato precedente (contenente la proprietà pubbliche di hello ModulesUrl, ConfigurationFunction, SasToken o proprietà) automaticamente adattano formato corrente toohello ed eseguire esattamente come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c456c-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="c456c-182">Hello seguente schema è quale schema delle impostazioni precedenti hello simile:</span><span class="sxs-lookup"><span data-stu-id="c456c-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
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
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="c456c-183">Ecco come formato precedente hello si adatta toohello di formato corrente:</span><span class="sxs-lookup"><span data-stu-id="c456c-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="c456c-184">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="c456c-184">Property Name</span></span> | <span data-ttu-id="c456c-185">Equivalente nello schema precedente</span><span class="sxs-lookup"><span data-stu-id="c456c-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="c456c-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c456c-186">settings.wmfVersion</span></span> |<span data-ttu-id="c456c-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c456c-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="c456c-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c456c-188">settings.configuration.url</span></span> |<span data-ttu-id="c456c-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="c456c-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="c456c-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c456c-190">settings.configuration.script</span></span> |<span data-ttu-id="c456c-191">Prima parte di settings.ConfigurationFunction (prima di "\\\\")</span><span class="sxs-lookup"><span data-stu-id="c456c-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="c456c-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c456c-192">settings.configuration.function</span></span> |<span data-ttu-id="c456c-193">Seconda parte di settings.ConfigurationFunction (dopo "\\\\")</span><span class="sxs-lookup"><span data-stu-id="c456c-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="c456c-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c456c-194">settings.configurationArguments</span></span> |<span data-ttu-id="c456c-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="c456c-195">settings.Properties</span></span> |
| <span data-ttu-id="c456c-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c456c-196">settings.configurationData.url</span></span> |<span data-ttu-id="c456c-197">protectedSettings.DataBlobUri (senza token di firma di accesso condiviso)</span><span class="sxs-lookup"><span data-stu-id="c456c-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="c456c-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c456c-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c456c-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c456c-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="c456c-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c456c-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c456c-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c456c-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="c456c-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c456c-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c456c-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="c456c-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="c456c-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c456c-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c456c-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="c456c-205">settings.SasToken</span></span> |
| <span data-ttu-id="c456c-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c456c-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c456c-207">Token di firma di accesso condiviso di protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="c456c-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="c456c-208">Risoluzione dei problemi - Codice errore 1100</span><span class="sxs-lookup"><span data-stu-id="c456c-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="c456c-209">Il codice di errore 1100 indica che si è verificato un problema con hello estensione DSC toohello input dell'utente.</span><span class="sxs-lookup"><span data-stu-id="c456c-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="c456c-210">testo Hello di questi errori è variabile e può cambiare.</span><span class="sxs-lookup"><span data-stu-id="c456c-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="c456c-211">Di seguito sono riportate alcune che si verifichino errori di hello e come è possibile correggerli.</span><span class="sxs-lookup"><span data-stu-id="c456c-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="c456c-212">Valori non validi</span><span class="sxs-lookup"><span data-stu-id="c456c-212">Invalid Values</span></span>
<span data-ttu-id="c456c-213">"Privacy.dataCollection è '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c456c-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="c456c-214">Hello solo i valori possibili sono ', 'Enable' e 'Disable' ""WmfVersion è '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c456c-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="c456c-215">Gli unici valori possibili sono: ...</span><span class="sxs-lookup"><span data-stu-id="c456c-215">Only possible values are …</span></span> <span data-ttu-id="c456c-216">e "più recenti"</span><span class="sxs-lookup"><span data-stu-id="c456c-216">and 'latest'"</span></span>

<span data-ttu-id="c456c-217">Problema: un valore specificato non è consentito.</span><span class="sxs-lookup"><span data-stu-id="c456c-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="c456c-218">Soluzione: Modifica hello valore non valido tooa valore valido.</span><span class="sxs-lookup"><span data-stu-id="c456c-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="c456c-219">Vedere la tabella hello nella sezione dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="c456c-220">URL non valido</span><span class="sxs-lookup"><span data-stu-id="c456c-220">Invalid URL</span></span>
<span data-ttu-id="c456c-221">"ConfigurationData.url è '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c456c-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="c456c-222">URL non valido" "DataBlobUri è '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c456c-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="c456c-223">URL non valido" "Configuration.url è '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c456c-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="c456c-224">URL non valido"</span><span class="sxs-lookup"><span data-stu-id="c456c-224">This is not a valid URL"</span></span>

<span data-ttu-id="c456c-225">Problema: un URL specificato non è valido.</span><span class="sxs-lookup"><span data-stu-id="c456c-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="c456c-226">Soluzione: verificare tutti gli URL specificati.</span><span class="sxs-lookup"><span data-stu-id="c456c-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="c456c-227">Assicurarsi che tutti gli URL consente di risolvere i percorsi toovalid estensione hello accessibile nel computer remoto hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="c456c-228">Tipo ConfigurationArgument non valido</span><span class="sxs-lookup"><span data-stu-id="c456c-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="c456c-229">"Tipo configurationArguments {0} non valido"</span><span class="sxs-lookup"><span data-stu-id="c456c-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="c456c-230">Problema: hello ConfigurationArguments proprietà non è possibile risolvere oggetto Hashtable tooa.</span><span class="sxs-lookup"><span data-stu-id="c456c-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="c456c-231">Soluzione: rendere la proprietà ConfigurationArguments un oggetto Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c456c-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="c456c-232">Seguire il formato di hello fornito nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="c456c-233">Prestare attenzione alle virgolette, alle virgole e alle parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="c456c-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="c456c-234">ConfigurationArguments duplicato</span><span class="sxs-lookup"><span data-stu-id="c456c-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="c456c-235">"Trovati argomenti duplicati '{0}' in configurationArguments pubblici e protetti"</span><span class="sxs-lookup"><span data-stu-id="c456c-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="c456c-236">Problema: hello ConfigurationArguments nelle impostazioni pubbliche e ConfigurationArguments nelle impostazioni protette hello contengono proprietà con hello stesso nome.</span><span class="sxs-lookup"><span data-stu-id="c456c-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="c456c-237">Soluzione: Rimuovere una delle proprietà duplicate hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="c456c-238">Proprietà mancanti</span><span class="sxs-lookup"><span data-stu-id="c456c-238">Missing Properties</span></span>
<span data-ttu-id="c456c-239">"Configuration.function richiede che venga specificato configuration.url o configuration.module"</span><span class="sxs-lookup"><span data-stu-id="c456c-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="c456c-240">"Configuration.url richiede che venga specificato configuration.script"</span><span class="sxs-lookup"><span data-stu-id="c456c-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="c456c-241">"Configuration.script richiede che venga specificato configuration.url"</span><span class="sxs-lookup"><span data-stu-id="c456c-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="c456c-242">"Configuration.url richiede che venga specificato configuration.function"</span><span class="sxs-lookup"><span data-stu-id="c456c-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="c456c-243">"ConfigurationUrlSasToken richiede che venga specificato configuration.url"</span><span class="sxs-lookup"><span data-stu-id="c456c-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="c456c-244">"ConfigurationDataUrlSasToken richiede che venga specificato configurationData.url"</span><span class="sxs-lookup"><span data-stu-id="c456c-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="c456c-245">Problema: una proprietà definita richiede un'altra proprietà mancante.</span><span class="sxs-lookup"><span data-stu-id="c456c-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="c456c-246">Soluzioni:</span><span class="sxs-lookup"><span data-stu-id="c456c-246">Solutions:</span></span> 

* <span data-ttu-id="c456c-247">Fornire proprietà mancante hello.</span><span class="sxs-lookup"><span data-stu-id="c456c-247">Provide hello missing property.</span></span>
* <span data-ttu-id="c456c-248">Rimuovere proprietà hello che deve essere hello di proprietà mancanti.</span><span class="sxs-lookup"><span data-stu-id="c456c-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c456c-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c456c-249">Next Steps</span></span>
<span data-ttu-id="c456c-250">Informazioni su DSC e imposta scalabilità della macchina virtuale in [utilizzando set di scalabilità macchina virtuale con hello estensione DSC di Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="c456c-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="c456c-251">Per altre informazioni dettagliate, leggere l'articolo sulla [gestione delle credenziali protette di DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c456c-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c456c-252">Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c456c-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c456c-253">Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="c456c-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

