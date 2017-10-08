---
title: aaaSet di chiave dell'insieme di credenziali per le macchine virtuali Windows Azure Resource Manager | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di Azure Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Configurare l'insieme di credenziali delle chiavi per le macchine virtuali in Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Nello stack di gestione risorse di Azure, i segreti/certificati vengono modellati come risorse fornite dal provider di risorse hello dell'insieme di credenziali chiave. toolearn ulteriori informazioni sull'insieme di credenziali chiave, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello **EnabledForDeployment** in insieme di credenziali chiave deve essere impostata tootrue. È possibile farlo in vari tipi di client.
> 2. esigenze di insieme di credenziali chiave Hello toobe creato in hello stessa sottoscrizione e posizione come hello macchina virtuale.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Utilizzare PowerShell tooset backup insieme di credenziali chiave
toocreate un insieme di credenziali chiave usando PowerShell, vedere [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md#vault).

Per i nuovi insiemi di credenziali delle chiavi, è possibile usare questo cmdlet di PowerShell:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Per gli insiemi di credenziali delle chiavi esistenti, è possibile usare questo cmdlet di PowerShell:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Ci CLI tooset backup insieme di credenziali chiave
toocreate un insieme di credenziali chiave tramite l'interfaccia della riga di comando hello (CLI), vedere [gestire insieme di credenziali chiave usando CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

CLI, è possibile insieme di credenziali chiave hello toocreate prima di assegnare il criterio di distribuzione hello. È possibile farlo tramite hello comando seguente:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Utilizzare tooset di modelli di insieme di credenziali chiave
Mentre si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per hello risorsa insieme di credenziali chiave.

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
