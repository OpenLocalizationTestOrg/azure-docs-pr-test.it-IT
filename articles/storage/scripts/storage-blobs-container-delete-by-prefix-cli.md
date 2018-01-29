---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Eliminare i contenitori mediante prefisso | Microsoft Docs
description: Eliminare i contenitori BLOB dell'Archiviazione di Azure in base a un prefisso del nome.
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: sample
ms.date: 06/22/2017
ms.author: tamram
ms.openlocfilehash: d14195abf1c17d11e259ed9edb5112626b063112
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2017
---
# <a name="delete-containers-based-on-container-name-prefix"></a>Eliminare i contenitori in base al prefisso del nome

Per prima cosa, lo script crea alcuni contenitori di esempio nell'Archiviazione BLOB di Azure, quindi ne elimina alcuni in base a un prefisso nel nome dei contenitori stessi.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/storage/delete-containers-by-prefix/delete-containers-by-prefix.sh?highlight=2-3 "Delete containers by prefix")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Eseguire il comando seguente per rimuovere il gruppo di risorse, i contenitori rimanenti e tutte le risorse correlate.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Lo script usa i comandi seguenti per eliminare i contenitori in base al prefisso contenuto nel nome dei contenitori stessi. Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.

| Comando | Note |
|---|---|
| [az group create](/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az storage account create](/cli/azure/storage/account#create) | Crea un account di Archiviazione di Azure nel gruppo di risorse specificato. |
| [az storage container create](/cli/azure/storage/container#create) | Crea un contenitore nell'Archiviazione BLOB di Azure. |
| [az storage container list](/cli/azure/storage/container#list) | Elenca i contenitori nell'account di Archiviazione di Azure. |
| [az storage container delete](/cli/azure/storage/container#delete) | Elimina i contenitori nell'account di Archiviazione di Azure. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview).

Altri esempi di script dell'interfaccia della riga di comando sono disponibili in [Interfaccia della riga di comando di Azure](../blobs/storage-samples-blobs-cli.md).
