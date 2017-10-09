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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Set di scalabilità di macchine virtuali (VMSS) Windows e Desired State Configuration (DSC) con modelli di Azure Resource Manager
In questo articolo viene descritto il modello di gestione risorse hello per hello [gestore dell'estensione DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Esempio di modello per una VM Windows
Hello frammento seguente inseriti nella sezione delle risorse del modello di hello hello.

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

## <a name="template-example-for-windows-vmss"></a>Esempio di modello per set di scalabilità di macchine virtuali (VMSS) Windows
Un nodo VMSS ha una sezione "proprietà" con hello "VirtualMachineProfile", "extensionProfile" attributo. DSC viene aggiunto sotto "extensions". 

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

## <a name="detailed-settings-information"></a>Informazioni dettagliate sulle impostazioni
Hello nello schema seguente è per parte di impostazioni hello hello estensione DSC di Azure in un modello di gestione risorse di Azure.

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

## <a name="details"></a>Dettagli
| Nome proprietà | Tipo | Descrizione |
| --- | --- | --- |
| settings.wmfVersion |string |Specifica la versione di hello di hello Windows Management Framework che deve essere installato nella macchina virtuale. L'impostazione di questa proprietà too'latest' Installa hello versione più recente WMF. Hello corrente solo i valori possibili per questa proprietà sono **'4.0', '5.0', ' 5.0PP' e 'versione più recente'**. Questi valori possibili sono tooupdates soggetto. valore predefinito di Hello è "più di recente". |
| settings.configuration.url |string |Specifica il percorso URL hello da cui toodownload file zip configurazione DSC. Se l'URL di hello fornito richiede un token di firma di accesso condiviso per l'accesso, è necessario tooset hello protectedSettings.configurationUrlSasToken proprietà toohello valore del token di firma di accesso condiviso. Questa proprietà è obbligatoria se settings.configuration.script e/o settings.configuration.function sono definiti. |
| settings.configuration.script |string |Specifica il nome file hello dello script hello contenente hello definizione della configurazione DSC. Questo script deve trovarsi nella cartella radice di hello del file zip hello scaricato dall'URL hello specificato dalla proprietà configuration.url hello. Questa proprietà è obbligatoria se settings.configuration.url e/o settings.configuration.script sono definiti. |
| settings.configuration.function |string |Specifica il nome di hello della configurazione DSC. configurazione di Hello denominata deve essere contenuta nello script hello definito da configuration.script. Questa proprietà è obbligatoria se settings.configuration.url e/o settings.configuration.function sono definiti. |
| settings.configurationArguments |Raccolta |Definisce i parametri che si desidera una configurazione di DSC tooyour toopass. Questa proprietà non è crittografata. |
| settings.configurationData.url |string |Specifica l'URL di hello da cui toodownload i dati di configurazione (con estensione psd1) file toouse come input per la configurazione DSC. Se l'URL di hello fornito richiede un token di firma di accesso condiviso per l'accesso, è necessario tooset hello protectedSettings.configurationDataUrlSasToken proprietà toohello valore del token di firma di accesso condiviso. |
| settings.privacy.dataEnabled |string |Abilita o disabilita la raccolta di dati di telemetria. Hello solo i valori possibili per questa proprietà sono **'Enable', 'Disable', ', o $null**. Lasciando questa proprietà vuota o con valore null verrà abilitata la raccolta di dati di telemetria. valore predefinito di Hello è '. [Altre informazioni](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Raccolta |Definisce i percorsi alternativi che da cui toodownload hello WMF. [Altre informazioni](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Raccolta |Definisce i parametri che si desidera una configurazione di DSC tooyour toopass. Questa proprietà è crittografata. |
| protectedSettings.configurationUrlSasToken |string |Specifica URL hello tooaccess token SAS hello definito da configuration.url. Questa proprietà è crittografata. |
| protectedSettings.configurationDataUrlSasToken |string |Specifica URL hello tooaccess token SAS hello definito da configurationData.url. Questa proprietà è crittografata. |

## <a name="settings-vs-protectedsettings"></a>Differenze tra settings e protectedSettings
Tutte le impostazioni vengono salvate in un file di testo di impostazioni in hello macchina virtuale.
Proprietà in 'impostazioni' sono proprietà pubbliche, perché non sono crittografate nel file di testo hello impostazioni.
Proprietà in 'protectedSettings' sono crittografate con un certificato e non vengono visualizzate in testo normale nel file al momento del hello macchina virtuale.

Se è necessario fornire credenziali configurazione hello, possono essere inclusi nei protectedSettings:

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

## <a name="example"></a>Esempio
Hello esempio deriva dalla sezione "Getting Started" hello di hello [pagina Panoramica di gestore dell'estensione DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Questo esempio Usa modelli di gestione risorse anziché cmdlet toodeploy hello. Salvare la configurazione "IisInstall.ps1" hello, inserirlo in una. COMPRIMERE file e caricare file hello in un URL accessibile. In questo esempio viene utilizzata l'archiviazione blob di Azure, ma è possibile toodownload. File ZIP da qualsiasi posizione arbitraria.

Nel modello di gestione risorse di Azure hello, hello codice riportato di seguito indica al file corretto hello toodownload VM hello ed eseguire la funzione di PowerShell appropriato hello:

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

## <a name="updating-from-hello-previous-format"></a>L'aggiornamento da hello formato precedente
Le impostazioni in hello formato precedente (contenente la proprietà pubbliche di hello ModulesUrl, ConfigurationFunction, SasToken o proprietà) automaticamente adattano formato corrente toohello ed eseguire esattamente come in precedenza.

Hello seguente schema è quale schema delle impostazioni precedenti hello simile:

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

Ecco come formato precedente hello si adatta toohello di formato corrente:

| Nome proprietà | Equivalente nello schema precedente |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |Prima parte di settings.ConfigurationFunction (prima di "\\\\") |
| settings.configuration.function |Seconda parte di settings.ConfigurationFunction (dopo "\\\\") |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (senza token di firma di accesso condiviso) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |Token di firma di accesso condiviso di protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Risoluzione dei problemi - Codice errore 1100
Il codice di errore 1100 indica che si è verificato un problema con hello estensione DSC toohello input dell'utente.
testo Hello di questi errori è variabile e può cambiare.
Di seguito sono riportate alcune che si verifichino errori di hello e come è possibile correggerli.

### <a name="invalid-values"></a>Valori non validi
"Privacy.dataCollection è '{0}'. Hello solo i valori possibili sono ', 'Enable' e 'Disable' ""WmfVersion è '{0}'. Gli unici valori possibili sono: ... e "più recenti"

Problema: un valore specificato non è consentito.

Soluzione: Modifica hello valore non valido tooa valore valido. Vedere la tabella hello nella sezione dettagli hello.

### <a name="invalid-url"></a>URL non valido
"ConfigurationData.url è '{0}'. URL non valido" "DataBlobUri è '{0}'. URL non valido" "Configuration.url è '{0}'. URL non valido"

Problema: un URL specificato non è valido.

Soluzione: verificare tutti gli URL specificati. Assicurarsi che tutti gli URL consente di risolvere i percorsi toovalid estensione hello accessibile nel computer remoto hello.

### <a name="invalid-configurationargument-type"></a>Tipo ConfigurationArgument non valido
"Tipo configurationArguments {0} non valido"

Problema: hello ConfigurationArguments proprietà non è possibile risolvere oggetto Hashtable tooa. 

Soluzione: rendere la proprietà ConfigurationArguments un oggetto Hashtable. Seguire il formato di hello fornito nell'esempio precedente hello. Prestare attenzione alle virgolette, alle virgole e alle parentesi graffe.

### <a name="duplicate-configurationarguments"></a>ConfigurationArguments duplicato
"Trovati argomenti duplicati '{0}' in configurationArguments pubblici e protetti"

Problema: hello ConfigurationArguments nelle impostazioni pubbliche e ConfigurationArguments nelle impostazioni protette hello contengono proprietà con hello stesso nome.

Soluzione: Rimuovere una delle proprietà duplicate hello.

### <a name="missing-properties"></a>Proprietà mancanti
"Configuration.function richiede che venga specificato configuration.url o configuration.module"

"Configuration.url richiede che venga specificato configuration.script"

"Configuration.script richiede che venga specificato configuration.url"

"Configuration.url richiede che venga specificato configuration.function"

"ConfigurationUrlSasToken richiede che venga specificato configuration.url"

"ConfigurationDataUrlSasToken richiede che venga specificato configurationData.url"

Problema: una proprietà definita richiede un'altra proprietà mancante.

Soluzioni: 

* Fornire proprietà mancante hello.
* Rimuovere proprietà hello che deve essere hello di proprietà mancanti.

## <a name="next-steps"></a>Passaggi successivi
Informazioni su DSC e imposta scalabilità della macchina virtuale in [utilizzando set di scalabilità macchina virtuale con hello estensione DSC di Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Per altre informazioni dettagliate, leggere l'articolo sulla [gestione delle credenziali protette di DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

