---
title: "Uso di Configurazione dello stato desiderato (DSC) con i set di scalabilità di macchine virtuali | Microsoft Docs"
description: "Utilizzo dei set di scalabilità di macchine virtuali con l'estensione DSC di Azure"
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
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="e3140-103">Utilizzo dei set di scalabilità di macchine virtuali con l'estensione DSC di Azure</span><span class="sxs-lookup"><span data-stu-id="e3140-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="e3140-104">I [set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md) possono essere usati con il gestore dell'estensione [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Configurazione dello stato desiderato (DSC) di Azure).</span><span class="sxs-lookup"><span data-stu-id="e3140-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="e3140-105">Il set di scalabilità di macchine virtuali consente di distribuire e gestire un numero elevato di macchine virtuali e di aumentare o ridurre la dimensione in risposta al carico.</span><span class="sxs-lookup"><span data-stu-id="e3140-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="e3140-106">DSC viene usato per la configurazione delle VM mano a mano che sono in linea, in modo che eseguano il software di produzione.</span><span class="sxs-lookup"><span data-stu-id="e3140-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="e3140-107">Differenze tra la distribuzione di macchine virtuali e i set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e3140-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="e3140-108">La struttura del modello sottostante di un set di scalabilità di macchine virtuali è leggermente diversa da quella di una singola VM.</span><span class="sxs-lookup"><span data-stu-id="e3140-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="e3140-109">In particolare, una singola VM distribuisce le estensioni nel nodo "virtualMachines".</span><span class="sxs-lookup"><span data-stu-id="e3140-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="e3140-110">È presente una voce del tipo "extensions" nella quale DSC viene aggiunto al modello:</span><span class="sxs-lookup"><span data-stu-id="e3140-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

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

<span data-ttu-id="e3140-111">Il nodo di un set di scalabilità di macchine virtuali ha una sezione "properties" con gli attributi "VirtualMachineProfile", "extensionProfile".</span><span class="sxs-lookup"><span data-stu-id="e3140-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="e3140-112">DSC viene aggiunto sotto "extensions":</span><span class="sxs-lookup"><span data-stu-id="e3140-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="e3140-113">Comportamento di un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e3140-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="e3140-114">Il comportamento di un set di scalabilità di macchine virtuali è identico a quello di una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3140-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="e3140-115">Quando viene creata una nuova VM, il provisioning viene automaticamente eseguito con l'estensione DSC.</span><span class="sxs-lookup"><span data-stu-id="e3140-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="e3140-116">Se l'estensione richiede una versione più recente del file WMF, la VM verrà riavviata prima di passare online.</span><span class="sxs-lookup"><span data-stu-id="e3140-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="e3140-117">Una volta online, il file con estensione zip di configurazione DSC viene scaricato e ne viene eseguito il provisioning nella VM.</span><span class="sxs-lookup"><span data-stu-id="e3140-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="e3140-118">Altre informazioni sono reperibili nella [panoramica sull'estensione DSC di Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3140-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3140-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3140-119">Next steps</span></span>
<span data-ttu-id="e3140-120">Esaminare il [modello di Azure Resource Manager per l'estensione DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3140-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e3140-121">Informazioni su come l' [estensione DSC gestisce in modo sicuro le credenziali](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3140-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="e3140-122">Per altre informazioni sul gestore dell'estensione DSC, vedere [Introduzione al gestore dell'estensione DSC (Desired State Configuration) di Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3140-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="e3140-123">Per altre informazioni su PowerShell DSC, [vedere il centro di documentazione di PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="e3140-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

