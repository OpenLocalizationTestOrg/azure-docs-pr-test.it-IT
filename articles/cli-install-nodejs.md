---
title: aaaInstall hello Azure CLI 1.0 | Documenti Microsoft
description: Installare hello 1.0 CLI di Azure per Mac, Linux e Windows toostart utilizzando servizi di Azure
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Installare hello Azure CLI 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Interfaccia della riga di comando di Azure 1.0](cli-install-nodejs.md)
> * [Interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Questo argomento viene descritto come tooinstall hello Azure CLI 1.0, che si basa su nodeJs e supporta tutte le API di distribuzione classica chiama nonché un numero elevato di attività di distribuzione di gestione risorse. È consigliabile utilizzare hello [CLI di Azure 2.0](/cli/azure/overview) per la gestione e le distribuzioni di CLI nuove o stampa.

Installare rapidamente hello interfaccia della riga di comando di Azure (Azure CLI 1.0) toouse un set di comandi basati su shell open source per la creazione e la gestione delle risorse in Microsoft Azure. Si dispongono di diverse opzioni tooinstall questi strumenti multipiattaforma nel computer in uso:

* **pacchetto npm** - esecuzione npm (hello package manager per JavaScript) tooinstall hello pacchetto più recente di Azure 1.0 CLI sul sistema operativo o la distribuzione di Linux. Nel computer devono essere installati node.js e npm.
* **Programma di installazione** - È possibile scaricare un programma di installazione per agevolare l'installazione in Mac o Windows.
* **Contenitore docker** : iniziare a utilizzare hello CLI più recente in un contenitore Docker ready to run. Nel computer deve essere installato l'host Docker.

Per altre opzioni e in background, vedere repository progetto hello in [GitHub](https://github.com/azure/azure-xplat-cli).

Una volta installato, hello Azure CLI 1.0 [connetterlo con la sottoscrizione di Azure](xplat-cli-connect.md) esecuzione hello e **azure** comandi dall'interfaccia della riga di comando (Bash Terminal, il prompt dei comandi e così via) toowork con le risorse di Azure.

## <a name="option-1-install-an-npm-package"></a>Opzione 1: Installare un pacchetto npm
tooinstall hello CLI da un pacchetto npm, assicurarsi aver scaricato e installato hello [più recenti di Node.js e npm](https://nodejs.org/en/download/package-manager/). Eseguire quindi **npm installare** pacchetto di tooinstall hello cli di azure:

```bash
npm install -g azure-cli
```

Nelle distribuzioni di Linux, potrebbe essere necessario toouse **sudo** toosuccessfully eseguire hello **npm** comando, come indicato di seguito:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Se è necessario tooinstall o aggiornare Node.js e npm sul sistema operativo o la distribuzione di Linux, è consigliabile installare hello versione di Node. js LTS più recente (4. x). Se si usa una versione precedente, potrebbero verificarsi errori di installazione.

Se si preferisce, scaricare hello Linux più recente [file con estensione tar] [ linux-installer] per npm hello pacchetto localmente. Quindi, installare il pacchetto di npm scaricato hello come indicato di seguito (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Opzione 2: Usare un programma di installazione
Se si utilizza un computer Mac o Windows, hello seguenti programmi di installazione CLI sono disponibile per il download:

* [Programma di installazione di Mac OS X][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> In Windows, è anche possibile scaricare hello [installazione guidata piattaforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI. In questo modo di programma di installazione si hello tooinstall opzione aggiuntive Azure SDK e strumenti da riga di comando dopo l'installazione di hello CLI.

## <a name="option-3-use-a-docker-container"></a>Opzione 3: Usare un contenitore Docker
Se è stato configurato il computer come un [Docker](https://docs.docker.com/engine/understanding-docker/) host, è possibile eseguire hello 1.0 CLI di Azure più recente in un contenitore Docker. Esecuzione hello il seguente comando (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Eseguire i comandi dell'interfaccia della riga di comando 1.0 di Azure
Dopo l'installazione hello Azure CLI 1.0, eseguire hello **azure** comando dall'interfaccia utente della riga di comando (Bash Terminal, il prompt dei comandi e così via). Ad esempio toorun hello help comando, digitare seguente hello:

```azurecli
azure help
```

> [!NOTE]
> In alcune distribuzioni Linux, è possibile che venga visualizzato un messaggio di errore simile troppo`/usr/bin/env: ‘node’: No such file or directory`. Questo errore è causato dalle installazioni recenti di Node.js che vengono installate in /usr/bin/nodejs. toofix, creare un collegamento simbolico troppo/usr/bin/nodo eseguendo questo comando:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

versione di hello toosee di hello Azure CLI 1.0 è stato installato, hello tipo seguente:

```azurecli
azure --version
```

È ora possibile iniziare la distribuzione. tooaccess tutti hello toowork comandi CLI con le risorse, [connettersi tooyour sottoscrizione di Azure da hello Azure CLI](xplat-cli-connect.md).

> [!NOTE]
> Quando si usa CLI di Azure, viene visualizzato un messaggio che chiede se si desidera tooallow informazioni sull'utilizzo di Microsoft toocollect. La partecipazione è facoltativa. Se si sceglie tooparticipate, è possibile interrompere in qualsiasi momento eseguendo `azure telemetry --disable`. la partecipazione di tooenable in qualsiasi momento, eseguire `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Aggiornare hello CLI
Spesso, Microsoft rilascia versioni aggiornate di hello CLI di Azure. Reinstallare hello CLI utilizzando Installazione guidata di hello del sistema operativo, oppure eseguire il contenitore Docker più recente di hello. O, se si hanno hello più recenti di Node.js e npm installati, aggiornare digitando hello segue (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Attivare il completamento con tasto TAB
Il completamento con tasto TAB dei comandi dell'interfaccia della riga di comando è supportato per Mac e Linux.

tooenable in zsh, eseguire:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable in bash, eseguire:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Passaggi successivi
* [Connettersi da hello CLI tooyour sottoscrizione di Azure](xplat-cli-connect.md) toocreate e gestire le risorse di Azure.
* toolearn ulteriori informazioni su hello CLI di Azure, scaricare il codice sorgente, segnalare i problemi, o collaborazione progetto toohello, visitare hello [repository GitHub per hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* In caso di domande sull'utilizzo di hello CLI di Azure o Azure, visitare hello [forum di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
