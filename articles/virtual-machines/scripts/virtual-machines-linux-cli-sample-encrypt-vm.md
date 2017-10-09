---
title: aaaAzure CLI Script di esempio - crittografare una VM Linux | Documenti Microsoft
description: 'Esempio di script dell''interfaccia della riga di comando di Azure: crittografare una VM Linux'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a>Crittografare una macchina virtuale Linux in Azure

Questo script crea un insieme di credenziali delle chiavi di Azure sicuro, le chiavi di crittografia, un'entità servizio di Azure Active Directory e una macchina virtuale (VM) Linux. Hello macchina virtuale viene quindi crittografata con la chiave di crittografia hello dall'insieme di credenziali chiave e le credenziali dell'entità servizio.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello toocreate i comandi seguenti di una risorsa gruppo, insieme di credenziali chiave di Azure, servizio principale, macchina virtuale, e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crea un insieme credenziali chiavi Azure toostore sicura di dati, ad esempio le chiavi di crittografia. |
| [az keyvault key create](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Crea una chiave di crittografia in Key Vault. |
| [az ad sp create-for-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Crea un servizio di Azure Active Directory principale toosecurely autenticare e controllare le chiavi di accesso tooencryption. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Imposta le autorizzazioni per hello insieme di credenziali chiave toogrant hello servizio principale tooencryption tasti di scelta. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az vm encryption enable](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Abilita la crittografia in una macchina virtuale con le credenziali dell'entità servizio di hello e la chiave di crittografia. |
| [az vm encryption show](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Mostra stato hello di hello il processo di crittografia di macchina virtuale. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
