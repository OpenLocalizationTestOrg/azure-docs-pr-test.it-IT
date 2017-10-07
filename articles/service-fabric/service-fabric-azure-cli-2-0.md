---
title: "aaaGet familiarità CLI di Azure 2.0 e Azure Service Fabric"
description: Informazioni su come toouse hello Azure Service Fabric comandi modulo CLI di Azure, versione 2.0. Informazioni su come tooconnect tooa cluster e come toomanage applicazioni.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a>Azure Service Fabric e interfaccia della riga di comando di Azure 2.0

Hello Azure strumento da riga di comando (CLI di Azure) versione 2.0 include comandi toohelp gestire i cluster di Azure Service Fabric. Informazioni su come tooget iniziare con l'infrastruttura dei servizi e CLI di Azure.

## <a name="install-azure-cli-20"></a>Installare l'interfaccia della riga di comando di Azure 2.0

È possibile utilizzare toointeract comandi CLI di Azure 2.0 con e gestire i cluster di Service Fabric. versione più recente di hello tooget di CLI di Azure, seguire hello [il processo di installazione standard CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

Per ulteriori informazioni, vedere hello [Panoramica CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="azure-cli-syntax"></a>Sintassi dell'interfaccia della riga di comando di Azure

Nell'interfaccia della riga di comando di Azure, tutti i comandi di Service Fabric sono preceduti da `az sf`. Per informazioni generali sui comandi hello è possibile utilizzare, utilizzare `az sf -h`. Per informazioni su un singolo comando, usare `az sf <command> -h`.

I comandi di Service Fabric nell'interfaccia della riga di comando di Azure seguono questo modello di denominazione:

```azurecli
az sf <object> <action>
```

`<object>`destinazione hello per `<action>`.

## <a name="select-a-cluster"></a>Selezionare un cluster

Prima di eseguire qualsiasi operazione, è necessario selezionare un cluster di tooconnect per. Per un esempio, vedere hello seguente codice. codice di Hello connette tooan protetta cluster.

> [!WARNING]
> Non usare cluster di Service Fabric non protetti in un ambiente di produzione.

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

endpoint del cluster Hello devono essere preceduti da `http` o `https`. Deve includere la porta hello per gateway HTTP hello. indirizzo e porta hello sono hello uguali a quelli hello URL Service Fabric Explorer.

Per i cluster protetti con un certificato, è possibile usare file con estensione pem non crittografati oppure file con estensione crt o key. ad esempio:

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Per ulteriori informazioni, vedere [cluster di Azure Service Fabric sicuro Connetti tooa](service-fabric-connect-to-secure-cluster.md).

> [!NOTE]
> Hello `select` comando non agirà su tutte le richieste prima della restituzione. tooverify di avere specificato un cluster in modo corretto, usare un comando simile `az sf cluster health`. Verificare che il comando hello non restituisce eventuali errori.

## <a name="basic-operations"></a>Operazioni di base

Le informazioni di connessione al cluster vengono mantenute per più sessioni dell'interfaccia della riga di comando di Azure. Dopo aver selezionato un cluster di Service Fabric, è possibile eseguire qualsiasi comando di Service Fabric nel cluster hello.

Ad esempio hello tooget stato di integrità dell'infrastruttura del servizio cluster, utilizzare hello comando seguente:

```azurecli
az sf cluster health
```

comando Hello produce output (presupponendo che l'output JSON è specificato nella configurazione di Azure CLI hello) seguente di hello:

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

È possibile trovare hello le seguenti informazioni utili se si verificano problemi durante l'uso di comandi di Service Fabric in CLI di Azure.

### <a name="convert-a-certificate-from-pfx-toopem-format"></a>Convertire un certificato dal formato tooPEM PFX

L'interfaccia della riga di comando di Azure supporta i certificati lato client come file con estensione pem. Se si utilizzano file con estensione PFX di Windows, è necessario convertire tali formato tooPEM certificati. un file PEM tooa file PFX, tooconvert utilizzare hello comando seguente:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Per ulteriori informazioni, vedere hello [OpenSSL documentazione](https://www.openssl.org/docs/).

### <a name="connection-issues"></a>Problemi di connessione

Alcune operazioni potrebbero generare hello seguente messaggio:

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

Verificare che hello specificato l'endpoint del cluster è disponibile e in attesa. Inoltre, verificare che hello che dell'interfaccia utente di Service Fabric Explorer è disponibile all'host e porta. endpoint hello tooupdate, utilizzare `az sf cluster select`.

### <a name="detailed-logs"></a>Log dettagliati

I log dettagliati si rivelano spesso utili per il debug o la segnalazione di un problema. CLI di Azure offre globale `--debug` flag che consentono di aumentare il livello di dettaglio hello dei file di log.

### <a name="command-help-and-syntax"></a>Informazioni sui comandi e sintassi

Eseguire i comandi di Service Fabric hello stesse convenzioni CLI di Azure. Per informazioni su un comando specifico o un gruppo di comandi, utilizzare hello `-h` flag:

```azurecli
az sf application -h
```

Di seguito è riportato un altro esempio:

```azurecli
az sf application create -h
```
