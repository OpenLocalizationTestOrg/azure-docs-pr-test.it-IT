---
title: modelli aaaAuthoring con le estensioni VM Linux | Documenti Microsoft
description: Informazioni sulla creazione di modelli di Azure Resource Manager con le estensioni per VM Linux
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Dall'interfaccia CLI di Azure, eseguire hello seguente comando:

      Azure VM extension list

Questo comando restituisce il nome server di pubblicazione hello, nome dell'estensione e versione come riportato di seguito:

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

toolook in configurazioni di esempio per le estensioni di Linux, fare clic su documentazione hello per vedere [Linux eExtensions esempi](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Consultare toohello seguente tooget un modello completato con le estensioni VM.

[Estensione di script personalizzato in una VM Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Una volta creato il modello di hello, è possibile distribuirlo utilizzando hello CLI di Azure.

