---
title: le immagini di macchina virtuale Windows aaaSelect in Azure | Documenti Microsoft
description: Informazioni su come toouse Azure PowerSHell toodetermine hello editore, offerta, SKU e la versione per le immagini VM Marketplace.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a>La modalità di immagini toofind macchina virtuale Windows in hello Azure Marketplace con Azure PowerShell

In questo argomento viene descritto come toouse Azure PowerShell toofind VM immagini in hello Azure Marketplace. Quando si crea una macchina virtuale di Windows, utilizzare questo toospecify informazioni un'immagine del Marketplace.

Assicurarsi che è installato e configurato hello più recente [modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).



## <a name="table-of-commonly-used-windows-images"></a>Tabella delle immagini Windows usate comunemente
| PublisherName | Offerta | Sku |
|:--- |:--- |:--- |:--- |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-Server-Core |
| MicrosoftWindowsServer |WindowsServer |2016-Datacenter-with-Containers |
| MicrosoftWindowsServer |WindowsServer |2016-Nano-Server |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |
| MicrosoftWindowsServer |WindowsServer |2008 R2-SP1 |
| MicrosoftDynamicsNAV |DynamicsNAV |2017 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2016 |
| MicrosoftSQLServer |SQL2016-WS2016 |Enterprise |
| MicrosoftSQLServer |SQL2014SP2-WS2012R2 |Enterprise |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |

## <a name="find-specific-images"></a>Trovare immagini specifiche


Quando si crea una nuova macchina virtuale con Azure Resource Manager, in alcuni casi è necessario toospecify un'immagine con una combinazione hello di hello le proprietà di immagine seguenti:

* Autore
* Offerta
* SKU

Ad esempio, utilizzare questi valori con hello [Set AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet di PowerShell o con un modello di gruppo di risorse in cui è necessario specificare il tipo di hello di toobe macchina virtuale creata.

Se è necessario toodetermine questi valori, è possibile eseguire hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), e [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet immagini di hello toonavigate. Questi valori possono essere determinati:

1. Elenco hello immagine server di pubblicazione.
2. Elencando le offerte di un determinato editore.
3. Elencando le SKU di una determinata offerta.

In primo luogo, elenco publishers hello con hello seguenti comandi:

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

Immettere il nome del server di pubblicazione selezionato ed eseguire hello seguenti comandi:

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Immettere il nome scelto offerta ed eseguire hello seguenti comandi:

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Output di hello di hello `Get-AzureRMVMImageSku` comando, si dispongano di tutte le informazioni di hello immagine hello toospecify è necessario per una nuova macchina virtuale.

Hello seguito è riportato un esempio completo è:

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

Output:

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

Per server di pubblicazione "MicrosoftWindowsServer" hello:

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

Output:

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

Per l'offerta di "Windows Server" hello:

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

Output:

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

Da questo elenco, copiare hello scelto nome SKU e si dispongano di tutte le informazioni per hello hello `Set-AzureRMVMSourceImage` cmdlet di PowerShell o per un modello di gruppo di risorse.

## <a name="next-steps"></a>Passaggi successivi
Ora è possibile scegliere l'immagine di hello precisamente desiderato toouse. toocreate una macchina virtuale rapidamente utilizzando informazioni sulle immagini hello solo disponibili, vedere [creare una macchina virtuale Windows con PowerShell](quick-create-powershell.md).
