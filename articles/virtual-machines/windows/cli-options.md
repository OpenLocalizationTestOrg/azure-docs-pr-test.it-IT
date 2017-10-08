---
title: hello aaaUsing CLI di Azure in Windows | Documenti Microsoft
description: Usa hello CLI di Azure in Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Usa hello CLI di Azure in Windows

Hello interfaccia della riga di comando (CLI) di Azure fornisce una riga di comando e l'ambiente di scripting per la creazione e la gestione delle risorse di Azure. Hello CLI di Azure è disponibile per i sistemi operativi Windows, Linux e macOS. In questi sistemi operativi, i comandi CLI hello sono identici, tuttavia la sintassi di scripting specifici del sistema operativo può essere diverso.

Questa modalità di hello dettagli documento hello CLI di Azure può essere installato ed eseguito in Windows e i dettagli requisiti sintattici per ognuno. Per la documentazione dettagliata sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Sottosistema di Windows per Linux

Hello sottosistema Windows per Linux (WSL) offre un ambiente Ubuntu Linux su anniversario di Windows 10 e versioni successive. Quando abilitato, WSL offre un'esperienza Bash nativa, che può essere usata per la creazione e l'esecuzione di script dell'interfaccia della riga di comando di Azure. Dal momento che WSL fornisce un'esperienza Bash nativa, gli script dell'interfaccia della riga di comando di Azure possono essere condivisi tra macOS, Linux e Windows senza alcuna modifica.

hello toouse CLI di Azure in WSL, completare i seguenti hello.

|Attività | Istruzioni |
|---|---|
| Abilitare WLS | [Documentazione sull'installazione di WSL](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Installare hello CLI di Azure |[Installare hello CLI in WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Hello CLI di Azure può essere eseguito in modo nativo in Windows. In questa configurazione, hello CLI di Azure viene installato nel sistema operativo di Windows hello e comandi possono essere eseguiti da PowerShell. In questa configurazione, gli script e i comandi dell'interfaccia della riga di comando di Azure sono eseguibili in qualsiasi versione di Windows supportata. È tuttavia necessaria la sintassi di scripting specifica della piattaforma. Per questo motivo, gli script non devono necessariamente essere condivisi tra macOS, Linux e Windows senza modifiche.

hello toouse CLI di Azure in Windows, installare il pacchetto di hello usando queste istruzioni, [installazione hello CLI in Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Immagine Docker

Quando si usa Docker per Windows, può essere avviata un'immagine Docker che include hello CLI di Azure. Questa immagine si basa su Linux e include un'esperienza Bash nativa.  Quando si usa Docker per Windows e l'immagine di hello CLI di Azure, toobe script condivisi tra macOS, Linux e Windows. 

hello toouse CLI di Azure per Docker per Windows, assicurarsi che Docker per Windows e l'esecuzione hello comando seguente.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Una volta completato, un Bash sessione inizierà ovvero precaricato con gli strumenti di hello CLI di Azure.

## <a name="next-steps"></a>Passaggi successivi

[Esempio di interfaccia della riga di comando per macchine virtuali di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Esempi di interfaccia della riga di comando per App Web di Azure](../../app-service-web/app-service-cli-samples.md)

[Esempi di interfaccia della riga di comando per Azure SQL](../../sql-database/sql-database-cli-samples.md)
