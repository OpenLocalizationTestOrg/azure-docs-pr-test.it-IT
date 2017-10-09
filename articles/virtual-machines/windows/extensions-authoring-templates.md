---
title: aaaAuthoring modelli con le estensioni di macchina virtuale di Windows | Documenti Microsoft
description: Informazioni sulla creazione di modelli Azure Resource Manager con le estensioni per VM Windows
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Creazione di modelli Azure Resource Manager con le estensioni di VM Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Da Azure PowerShell, eseguire hello cmdlet di Azure PowerShell seguente:

      Get-AzureVMAvailableExtension


Questo cmdlet restituisce il nome di server di pubblicazione hello, nome di estensione e versione come indicato di seguito:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Mapping di queste tre proprietà troppo "publisher", "type" e "typeHandlerVersion" rispettivamente in hello sopra il frammento di modello.

> [!NOTE]
> È sempre consigliato toouse hello più recente versione tooget hello aggiornato più funzionalità dell'estensione.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Identificazione dello schema di hello per i parametri di configurazione di estensione hello
passaggio successivo di Hello alla creazione di un modello di estensione è formato hello tooidentify per fornire i parametri di configurazione. Ogni estensione supporta il proprio set di parametri.

toolook in configurazioni di esempio per le estensioni di Windows, vedere [degli esempi di estensioni Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Consultare toohello seguente tooget un modello completato con le estensioni VM.

[Estensione di script personalizzato in una macchina virtuale Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Una volta creato il modello di hello, è possibile distribuire usando Azure PowerShell.

