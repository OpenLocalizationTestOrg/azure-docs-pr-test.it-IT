---
title: "aaaUsing desiderato stato configurazione con scalabilità set di macchine virtuali | Documenti Microsoft"
description: "Utilizzo di set di scalabilità di macchine virtuali con hello estensione DSC di Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Utilizzo di set di scalabilità di macchine virtuali con hello estensione DSC di Azure
[Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md) può essere utilizzato con hello [Azure configurazione DSC (Desired State)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) gestore dell'estensione. Set di scalabilità di macchine virtuali forniscono un modo toodeploy e gestire un numero elevato di macchine virtuali ed elastico può aumentare e ridurre in tooload di risposta. DSC è hello tooconfigure usate le macchine virtuali man mano che arrivano online in modo che eseguono software di produzione hello.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Differenze tra la distribuzione di macchine tooVirtual e set di scalabilità di macchine virtuali
struttura di modello per un set di scalabilità della macchina virtuale sottostante Hello è leggermente diversa da una singola macchina virtuale. In particolare, una singola macchina virtuale consente di distribuire le estensioni nel nodo "virtualMachines" hello. C'è una voce di tipo "estensioni" in cui DSC viene aggiunto il modello toohello

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
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
          }
      ]
```

Un nodo di set di scalabilità macchina virtuale ha una sezione "proprietà" con "VirtualMachineProfile" attributo "extensionProfile" hello. DSC viene aggiunto sotto "extensions":

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
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
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Comportamento di un set di scalabilità di macchine virtuali
comportamento di Hello per un set di scalabilità della macchina virtuale è toohello identiche per una singola macchina virtuale. Quando viene creata una nuova macchina virtuale, viene automaticamente associato hello estensione DSC. Se una versione più recente di WMF richiesti dall'estensione hello hello, hello macchina virtuale verrà riavviata prima di connettersi. Una volta in linea, Scarica hello DSC configurazione ZIP ed effettuare il provisioning in hello macchina virtuale. Ulteriori informazioni, vedere [hello Panoramica di estensione di Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Passaggi successivi
Esaminare hello [il modello di gestione risorse di Azure per l'estensione DSC hello](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Informazioni su come hello [estensione DSC gestisce in modo sicuro le credenziali](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

