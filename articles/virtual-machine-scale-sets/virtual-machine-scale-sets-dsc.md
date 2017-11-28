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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="5e3cc-103">Utilizzo di set di scalabilità di macchine virtuali con hello estensione DSC di Azure</span><span class="sxs-lookup"><span data-stu-id="5e3cc-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="5e3cc-104">[Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md) può essere utilizzato con hello [Azure configurazione DSC (Desired State)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) gestore dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="5e3cc-105">Set di scalabilità di macchine virtuali forniscono un modo toodeploy e gestire un numero elevato di macchine virtuali ed elastico può aumentare e ridurre in tooload di risposta.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="5e3cc-106">DSC è hello tooconfigure usate le macchine virtuali man mano che arrivano online in modo che eseguono software di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="5e3cc-107">Differenze tra la distribuzione di macchine tooVirtual e set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5e3cc-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5e3cc-108">struttura di modello per un set di scalabilità della macchina virtuale sottostante Hello è leggermente diversa da una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="5e3cc-109">In particolare, una singola macchina virtuale consente di distribuire le estensioni nel nodo "virtualMachines" hello.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="5e3cc-110">C'è una voce di tipo "estensioni" in cui DSC viene aggiunto il modello toohello</span><span class="sxs-lookup"><span data-stu-id="5e3cc-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="5e3cc-111">Un nodo di set di scalabilità macchina virtuale ha una sezione "proprietà" con "VirtualMachineProfile" attributo "extensionProfile" hello.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="5e3cc-112">DSC viene aggiunto sotto "extensions":</span><span class="sxs-lookup"><span data-stu-id="5e3cc-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="5e3cc-113">Comportamento di un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="5e3cc-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="5e3cc-114">comportamento di Hello per un set di scalabilità della macchina virtuale è toohello identiche per una singola macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="5e3cc-115">Quando viene creata una nuova macchina virtuale, viene automaticamente associato hello estensione DSC.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="5e3cc-116">Se una versione più recente di WMF richiesti dall'estensione hello hello, hello macchina virtuale verrà riavviata prima di connettersi.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="5e3cc-117">Una volta in linea, Scarica hello DSC configurazione ZIP ed effettuare il provisioning in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e3cc-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="5e3cc-118">Ulteriori informazioni, vedere [hello Panoramica di estensione di Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e3cc-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e3cc-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e3cc-119">Next steps</span></span>
<span data-ttu-id="5e3cc-120">Esaminare hello [il modello di gestione risorse di Azure per l'estensione DSC hello](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e3cc-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5e3cc-121">Informazioni su come hello [estensione DSC gestisce in modo sicuro le credenziali](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e3cc-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="5e3cc-122">Per ulteriori informazioni sul gestore di estensioni di hello DSC per Azure, vedere [gestore di estensioni di Azure DSC toohello Introduzione](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e3cc-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="5e3cc-123">Per ulteriori informazioni su PowerShell DSC, [visitare Centro documentazione di PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="5e3cc-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

