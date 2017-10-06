---
title: aaaSet di insieme di credenziali chiave per le macchine virtuali Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di gestione risorse di Azure con hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Impostare la chiave dell'insieme di credenziali per le macchine virtuali in Gestione risorse di Azure con hello Azure CLI 1.0
Nello stack di gestione risorse di Azure hello, segreti/certificati vengono modellati come risorse fornite dal provider di risorse hello dell'insieme di credenziali chiave. toolearn ulteriori informazioni sull'insieme di credenziali chiave di Azure, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md) Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello *EnabledForDeployment* in insieme di credenziali chiave deve essere impostata tootrue. È possibile farlo in vari tipi di client. In questo articolo illustra come tooset di insieme di credenziali chiave per l'utilizzo con macchine virtuali di Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile eseguire attività di hello tramite una delle seguenti versioni CLI hello

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="use-cli-10-tooset-up-key-vault"></a>Utilizzare tooset 1.0 CLI di insieme di credenziali chiave
toocreate un insieme di credenziali chiave tramite l'interfaccia della riga di comando hello (CLI), vedere [gestire insieme di credenziali chiave usando CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI 1.0, è possibile insieme di credenziali chiave hello toocreate prima di assegnare il criterio di distribuzione hello. È quindi possibile assegnare criteri hello utilizzando hello comando seguente:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Utilizzare tooset di modelli di insieme di credenziali chiave
Quando si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per hello risorsa insieme di credenziali chiave.

    {
      "type": "Microsoft.KeyVault/vaults",
      "name": "ContosoKeyVault",
      "apiVersion": "2015-06-01",
      "location": "<location-of-key-vault>",
      "properties": {
        "enabledForDeployment": "true",
        ....
        ....
      }
    }

Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi utilizzando i modelli, vedere l'articolo su come [creare un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
