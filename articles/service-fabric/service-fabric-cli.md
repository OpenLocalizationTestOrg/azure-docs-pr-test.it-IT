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
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="b8956-104">Riga di comando di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b8956-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="b8956-105">Hello Azure Service Fabric CLI (sfctl) è un'utilità della riga di comando per l'interazione e la gestione delle entità di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8956-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="b8956-106">È possibile usare sfctl con cluster Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b8956-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="b8956-107">Sfctl viene eseguito solo sulle piattaforme che supportano Python.</span><span class="sxs-lookup"><span data-stu-id="b8956-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8956-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b8956-108">Prerequisites</span></span>

<span data-ttu-id="b8956-109">Tooinstallation precedente, assicurarsi che l'ambiente dispone sia di python e pip installato.</span><span class="sxs-lookup"><span data-stu-id="b8956-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="b8956-110">Per ulteriori informazioni, esaminare hello [pip documentazione delle Guide rapide](https://pip.pypa.io/en/latest/quickstart/)e ufficiale [python installare la documentazione](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="b8956-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="b8956-111">Mentre sono supportati entrambi python 2.7 e 3.6, si consiglia di python toouse 3.6.</span><span class="sxs-lookup"><span data-stu-id="b8956-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="b8956-112">Installa</span><span class="sxs-lookup"><span data-stu-id="b8956-112">Install</span></span>

<span data-ttu-id="b8956-113">Hello Azure Service Fabric CLI (sfctl) viene fornito come un pacchetto di python.</span><span class="sxs-lookup"><span data-stu-id="b8956-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="b8956-114">tooinstall hello versione più recente esecuzione:</span><span class="sxs-lookup"><span data-stu-id="b8956-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="b8956-115">Dopo l'installazione, eseguire `sfctl -h` tooget informazioni sui comandi disponibili.</span><span class="sxs-lookup"><span data-stu-id="b8956-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="b8956-116">Sintassi dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="b8956-116">CLI syntax</span></span>

<span data-ttu-id="b8956-117">I comandi sono sempre preceduti da `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="b8956-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="b8956-118">Per informazioni generali su tutti i comandi utilizzabili, usare `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="b8956-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="b8956-119">Per informazioni su un singolo comando, usare `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="b8956-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="b8956-120">I comandi seguenti, una struttura ripetibile, con destinazione hello hello comando precedente verbo hello o azione:</span><span class="sxs-lookup"><span data-stu-id="b8956-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="b8956-121">In questo esempio, `<object>` destinazione hello per `<action>`.</span><span class="sxs-lookup"><span data-stu-id="b8956-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="b8956-122">Selezionare un cluster</span><span class="sxs-lookup"><span data-stu-id="b8956-122">Select a cluster</span></span>

<span data-ttu-id="b8956-123">Prima di eseguire qualsiasi operazione, è necessario selezionare un cluster di tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="b8956-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="b8956-124">Ad esempio, eseguire hello seguente tooselect e connettersi toohello cluster con nome hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="b8956-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="b8956-125">Non usare cluster di Service Fabric non protetti in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b8956-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="b8956-126">endpoint del cluster Hello devono essere preceduti da `http` o `https`.</span><span class="sxs-lookup"><span data-stu-id="b8956-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="b8956-127">Deve includere la porta hello per gateway HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="b8956-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="b8956-128">indirizzo e porta hello sono hello uguali a quelli hello URL Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b8956-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="b8956-129">Per i cluster protetti da un certificato, è possibile specificare un certificato con codifica PEM.</span><span class="sxs-lookup"><span data-stu-id="b8956-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="b8956-130">certificato Hello può essere specificato come un singolo file o un certificato e una coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="b8956-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="b8956-131">Per ulteriori informazioni, vedere [cluster di Azure Service Fabric sicuro Connetti tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b8956-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="b8956-132">Operazioni di base</span><span class="sxs-lookup"><span data-stu-id="b8956-132">Basic operations</span></span>

<span data-ttu-id="b8956-133">Le informazioni di connessione al cluster vengono mantenute per più sessioni sfctl.</span><span class="sxs-lookup"><span data-stu-id="b8956-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="b8956-134">Dopo aver selezionato un cluster di Service Fabric, è possibile eseguire qualsiasi comando di Service Fabric nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8956-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="b8956-135">Ad esempio hello tooget stato di integrità dell'infrastruttura del servizio cluster, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8956-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="b8956-136">risultati del comando Hello in hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="b8956-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="b8956-137">Suggerimenti e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b8956-137">Tips and troubleshooting</span></span>

<span data-ttu-id="b8956-138">Alcuni suggerimenti per risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="b8956-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="b8956-139">Convertire un certificato dal formato tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="b8956-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="b8956-140">Hello servizio infrastruttura CLI supporta i certificati sul lato client come file (con estensione PEM) PEM.</span><span class="sxs-lookup"><span data-stu-id="b8956-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="b8956-141">Se si utilizzano file con estensione PFX di Windows, è necessario convertire tali formato tooPEM certificati.</span><span class="sxs-lookup"><span data-stu-id="b8956-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="b8956-142">tooconvert un file PEM tooa file PFX, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b8956-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="b8956-143">Per ulteriori informazioni, vedere hello [OpenSSL documentazione](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="b8956-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="b8956-144">Problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="b8956-144">Connection issues</span></span>

<span data-ttu-id="b8956-145">Alcune operazioni potrebbero generare hello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="b8956-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="b8956-146">Verificare che hello specificato l'endpoint del cluster è disponibile e in attesa.</span><span class="sxs-lookup"><span data-stu-id="b8956-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="b8956-147">Inoltre, verificare che hello che dell'interfaccia utente di Service Fabric Explorer è disponibile all'host e porta.</span><span class="sxs-lookup"><span data-stu-id="b8956-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="b8956-148">endpoint hello tooupdate, utilizzare `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="b8956-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="b8956-149">Log dettagliati</span><span class="sxs-lookup"><span data-stu-id="b8956-149">Detailed logs</span></span>

<span data-ttu-id="b8956-150">I log dettagliati si rivelano spesso utili per il debug o la segnalazione di un problema.</span><span class="sxs-lookup"><span data-stu-id="b8956-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="b8956-151">È globale `--debug` flag che consentono di aumentare il livello di dettaglio hello dei file di log.</span><span class="sxs-lookup"><span data-stu-id="b8956-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="b8956-152">Informazioni sui comandi e sintassi</span><span class="sxs-lookup"><span data-stu-id="b8956-152">Command help and syntax</span></span>

<span data-ttu-id="b8956-153">Per informazioni su un comando specifico o un gruppo di comandi, utilizzare hello `-h` flag:</span><span class="sxs-lookup"><span data-stu-id="b8956-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="b8956-154">Un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="b8956-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="b8956-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8956-155">Next steps</span></span>

* [<span data-ttu-id="b8956-156">Distribuire un'applicazione hello CLI di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b8956-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="b8956-157">Introduzione a Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="b8956-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
