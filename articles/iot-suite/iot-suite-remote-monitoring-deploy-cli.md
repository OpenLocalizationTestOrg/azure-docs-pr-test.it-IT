---
title: Distribuire la soluzione di monitoraggio remoto Java - Azure | Microsoft Docs
description: Questa esercitazione illustra come effettuare il provisioning dei microservizi Java della soluzione preconfigurata di monitoraggio remoto usando l'interfaccia della riga di comando.
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-suite
ms.date: 12/12/2017
ms.topic: article
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.workload: NA
ms.openlocfilehash: ea3764299d07f548abbc2857a3adbfb4dc50dec8
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2017
---
# <a name="deploy-the-remote-monitoring-preconfigured-solution-using-the-cli"></a>Distribuire la soluzione preconfigurata di monitoraggio remoto usando l'interfaccia della riga di comando

Questa esercitazione illustra come effettuare il provisioning della soluzione preconfigurata per il monitoraggio remoto. Distribuire la soluzione usando l'interfaccia della riga di comando. È anche possibile distribuire la soluzione usando l'interfaccia utente basata sul Web disponibile all'indirizzo azureiotsuite.com. Per informazioni su questa opzione, vedere [Distribuire la soluzione preconfigurata di monitoraggio remoto](iot-suite-remote-monitoring-deploy.md).

## <a name="prerequisites"></a>Prerequisiti

Per distribuire la soluzione preconfigurata di monitoraggio remoto, è necessaria una sottoscrizione di Azure attiva.

Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](http://azure.microsoft.com/pricing/free-trial/).

Per eseguire l'interfaccia della riga di comando, è necessario che [Node.js](https://nodejs.org/) sia installato nel computer locale.

## <a name="install-the-cli"></a>Installare l'interfaccia della riga di comando

Per installare l'interfaccia della riga di comando, eseguire il comando seguente nell'ambiente della riga di comando:

```cmd/sh
npm install iot-solutions -g
```

## <a name="sign-in-to-the-cli"></a>Accedere all'interfaccia della riga di comando

Prima di poter distribuire la soluzione preconfigurata, è necessario accedere alla sottoscrizione di Azure tramite l'interfaccia della riga di comando in questo modo:

```cmd/sh
pcs login
```

Seguire le istruzioni visualizzate sullo schermo per completare il processo di accesso.

## <a name="deployment-options"></a>Opzioni di distribuzione

Quando si distribuisce la soluzione preconfigurata, sono disponibili diverse opzioni per la configurazione del processo di distribuzione:

| Opzione | Valori | DESCRIZIONE |
| ------ | ------ | ----------- |
| SKU    | `basic`, `standard` | Una distribuzione _di base_ è destinata agli ambienti di test e demo e distribuisce tutti i microservizi in un'unica macchina virtuale. Una distribuzione _standard_ è destinata agli ambienti di produzione e distribuisce i microservizi in più macchine virtuali. |
| Runtime | `dotnet`, `java` | Seleziona l'implementazione del linguaggio dei microservizi. |

## <a name="deploy-the-preconfigured-solution"></a>Distribuire la soluzione preconfigurata

### <a name="example-deploy-net-version"></a>Esempio: Distribuire la versione .NET

L'esempio seguente mostra come distribuire la versione .NET di base della soluzione preconfigurata di monitoraggio remoto:

```cmd/sh
pcs -t remotemonitoring -s basic -r dotnet
```

### <a name="example-deploy-java-version"></a>Esempio: Distribuire la versione Java

L'esempio seguente mostra come distribuire la versione Java standard della soluzione preconfigurata di monitoraggio remoto:

```cmd/sh
pcs -t remotemonitoring -s standard -r java
```

### <a name="pcs-command-options"></a>Opzioni del comando pcs

Quando si esegue il comando `pcs` per distribuire una soluzione, vengono chiesti gli elementi seguenti:

- Nome per la soluzione. Il nome deve essere univoco.
- Sottoscrizione di Azure da usare.
- Posizione.
- Credenziali per le macchine virtuali che ospitano i microservizi. È possibile usare queste credenziali per accedere alle macchine virtuali per la risoluzione dei problemi.

Al termine del comando `pcs`, viene visualizzato l'URL della nuova distribuzione della soluzione preconfigurata. Il comando `pcs` crea anche un file `{deployment-name}-output.json` con informazioni aggiuntive, tra cui il nome dell'hub IoT di cui è stato effettuato automaticamente il provisioning.

Per altre informazioni sui parametri della riga di comando, eseguire:

```cmd/sh
pcs -h
```

Per altre informazioni sull'interfaccia della riga di comando, vedere [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md) (Come usare l'interfaccia della riga di comando).

## <a name="next-steps"></a>Passaggi successivi

Questa esercitazione illustra come:

> [!div class="checklist"]
> * Configurare la soluzione preconfigurata
> * Distribuire la soluzione preconfigurata
> * Accedere alla soluzione preconfigurata

Ora che è stata distribuita la soluzione di monitoraggio remoto, il passaggio successivo consiste nell'[esplorare le funzionalità del dashboard della soluzione](./iot-suite-remote-monitoring-deploy.md).

<!-- Next tutorials in the sequence -->