---
title: Introduzione a Azure Service Fabric CLI (sfctl) aaaGet
description: Informazioni su come toouse hello Azure Service Fabric CLI. Informazioni su come tooconnect tooa cluster e come toomanage applicazioni.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a>Riga di comando di Azure Service Fabric

Hello Azure Service Fabric CLI (sfctl) è un'utilità della riga di comando per l'interazione e la gestione delle entità di Azure Service Fabric. È possibile usare sfctl con cluster Windows o Linux. Sfctl viene eseguito solo sulle piattaforme che supportano Python.

## <a name="prerequisites"></a>Prerequisiti

Tooinstallation precedente, assicurarsi che l'ambiente dispone sia di python e pip installato. Per ulteriori informazioni, esaminare hello [pip documentazione delle Guide rapide](https://pip.pypa.io/en/latest/quickstart/)e ufficiale [python installare la documentazione](https://wiki.python.org/moin/BeginnersGuide/Download).

Mentre sono supportati entrambi python 2.7 e 3.6, si consiglia di python toouse 3.6.

## <a name="install"></a>Installa

Hello Azure Service Fabric CLI (sfctl) viene fornito come un pacchetto di python. tooinstall hello versione più recente esecuzione:

```bash
pip install sfctl
```

Dopo l'installazione, eseguire `sfctl -h` tooget informazioni sui comandi disponibili.

## <a name="cli-syntax"></a>Sintassi dell'interfaccia della riga di comando

I comandi sono sempre preceduti da `sfctl`. Per informazioni generali su tutti i comandi utilizzabili, usare `sfctl -h`. Per informazioni su un singolo comando, usare `sfctl <command> -h`.

I comandi seguenti, una struttura ripetibile, con destinazione hello hello comando precedente verbo hello o azione:

```azurecli
sfctl <object> <action>
```

In questo esempio, `<object>` destinazione hello per `<action>`.

## <a name="select-a-cluster"></a>Selezionare un cluster

Prima di eseguire qualsiasi operazione, è necessario selezionare un cluster di tooconnect per. Ad esempio, eseguire hello seguente tooselect e connettersi toohello cluster con nome hello `testcluster.com`.

> [!WARNING]
> Non usare cluster di Service Fabric non protetti in un ambiente di produzione.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

endpoint del cluster Hello devono essere preceduti da `http` o `https`. Deve includere la porta hello per gateway HTTP hello. indirizzo e porta hello sono hello uguali a quelli hello URL Service Fabric Explorer.

Per i cluster protetti da un certificato, è possibile specificare un certificato con codifica PEM. certificato Hello può essere specificato come un singolo file o un certificato e una coppia di chiavi.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Per ulteriori informazioni, vedere [cluster di Azure Service Fabric sicuro Connetti tooa](service-fabric-connect-to-secure-cluster.md).

## <a name="basic-operations"></a>Operazioni di base

Le informazioni di connessione al cluster vengono mantenute per più sessioni sfctl. Dopo aver selezionato un cluster di Service Fabric, è possibile eseguire qualsiasi comando di Service Fabric nel cluster hello.

Ad esempio hello tooget stato di integrità dell'infrastruttura del servizio cluster, utilizzare hello comando seguente:

```azurecli
sfctl cluster health
```

risultati del comando Hello in hello seguente output:

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Suggerimenti e risoluzione dei problemi

Alcuni suggerimenti per risolvere i problemi comuni.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertire un certificato dal formato tooPEM PFX

Hello servizio infrastruttura CLI supporta i certificati sul lato client come file (con estensione PEM) PEM. Se si utilizzano file con estensione PFX di Windows, è necessario convertire tali formato tooPEM certificati. tooconvert un file PEM tooa file PFX, usare il comando seguente:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Per ulteriori informazioni, vedere hello [OpenSSL documentazione](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemi di connessione

Alcune operazioni potrebbero generare hello seguente messaggio:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Verificare che hello specificato l'endpoint del cluster è disponibile e in attesa. Inoltre, verificare che hello che dell'interfaccia utente di Service Fabric Explorer è disponibile all'host e porta. endpoint hello tooupdate, utilizzare `sfctl cluster select`.

### <a name="detailed-logs"></a>Log dettagliati

I log dettagliati si rivelano spesso utili per il debug o la segnalazione di un problema. È globale `--debug` flag che consentono di aumentare il livello di dettaglio hello dei file di log.

### <a name="command-help-and-syntax"></a>Informazioni sui comandi e sintassi

Per informazioni su un comando specifico o un gruppo di comandi, utilizzare hello `-h` flag:

```azurecli
sfctl application -h
```

Un altro esempio:

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a>Passaggi successivi

* [Distribuire un'applicazione hello CLI di Azure Service Fabric](service-fabric-application-lifecycle-sfctl.md)
* [Introduzione a Service Fabric in Linux](service-fabric-get-started-linux.md)
