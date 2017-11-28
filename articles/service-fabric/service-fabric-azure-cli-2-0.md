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
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="23df1-104">Azure Service Fabric e interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="23df1-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="23df1-105">Hello Azure strumento da riga di comando (CLI di Azure) versione 2.0 include comandi toohelp gestire i cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23df1-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="23df1-106">Informazioni su come tooget iniziare con l'infrastruttura dei servizi e CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="23df1-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="23df1-107">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="23df1-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="23df1-108">È possibile utilizzare toointeract comandi CLI di Azure 2.0 con e gestire i cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23df1-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="23df1-109">versione più recente di hello tooget di CLI di Azure, seguire hello [il processo di installazione standard CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23df1-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="23df1-110">Per ulteriori informazioni, vedere hello [Panoramica CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23df1-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="23df1-111">Sintassi dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="23df1-111">Azure CLI syntax</span></span>

<span data-ttu-id="23df1-112">Nell'interfaccia della riga di comando di Azure, tutti i comandi di Service Fabric sono preceduti da `az sf`.</span><span class="sxs-lookup"><span data-stu-id="23df1-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="23df1-113">Per informazioni generali sui comandi hello è possibile utilizzare, utilizzare `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="23df1-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="23df1-114">Per informazioni su un singolo comando, usare `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="23df1-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="23df1-115">I comandi di Service Fabric nell'interfaccia della riga di comando di Azure seguono questo modello di denominazione:</span><span class="sxs-lookup"><span data-stu-id="23df1-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="23df1-116">`<object>`destinazione hello per `<action>`.</span><span class="sxs-lookup"><span data-stu-id="23df1-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="23df1-117">Selezionare un cluster</span><span class="sxs-lookup"><span data-stu-id="23df1-117">Select a cluster</span></span>

<span data-ttu-id="23df1-118">Prima di eseguire qualsiasi operazione, è necessario selezionare un cluster di tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="23df1-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="23df1-119">Per un esempio, vedere hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="23df1-119">For an example, see hello following code.</span></span> <span data-ttu-id="23df1-120">codice di Hello connette tooan protetta cluster.</span><span class="sxs-lookup"><span data-stu-id="23df1-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="23df1-121">Non usare cluster di Service Fabric non protetti in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="23df1-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="23df1-122">endpoint del cluster Hello devono essere preceduti da `http` o `https`.</span><span class="sxs-lookup"><span data-stu-id="23df1-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="23df1-123">Deve includere la porta hello per gateway HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="23df1-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="23df1-124">indirizzo e porta hello sono hello uguali a quelli hello URL Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="23df1-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="23df1-125">Per i cluster protetti con un certificato, è possibile usare file con estensione pem non crittografati oppure file con estensione crt o key.</span><span class="sxs-lookup"><span data-stu-id="23df1-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="23df1-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23df1-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="23df1-127">Per ulteriori informazioni, vedere [cluster di Azure Service Fabric sicuro Connetti tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="23df1-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="23df1-128">Hello `select` comando non agirà su tutte le richieste prima della restituzione.</span><span class="sxs-lookup"><span data-stu-id="23df1-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="23df1-129">tooverify di avere specificato un cluster in modo corretto, usare un comando simile `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="23df1-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="23df1-130">Verificare che il comando hello non restituisce eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="23df1-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="23df1-131">Operazioni di base</span><span class="sxs-lookup"><span data-stu-id="23df1-131">Basic operations</span></span>

<span data-ttu-id="23df1-132">Le informazioni di connessione al cluster vengono mantenute per più sessioni dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="23df1-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="23df1-133">Dopo aver selezionato un cluster di Service Fabric, è possibile eseguire qualsiasi comando di Service Fabric nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="23df1-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="23df1-134">Ad esempio hello tooget stato di integrità dell'infrastruttura del servizio cluster, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="23df1-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="23df1-135">comando Hello produce output (presupponendo che l'output JSON è specificato nella configurazione di Azure CLI hello) seguente di hello:</span><span class="sxs-lookup"><span data-stu-id="23df1-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="23df1-136">Suggerimenti e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="23df1-136">Tips and troubleshooting</span></span>

<span data-ttu-id="23df1-137">È possibile trovare hello le seguenti informazioni utili se si verificano problemi durante l'uso di comandi di Service Fabric in CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="23df1-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="23df1-138">Convertire un certificato dal formato tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="23df1-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="23df1-139">L'interfaccia della riga di comando di Azure supporta i certificati lato client come file con estensione pem.</span><span class="sxs-lookup"><span data-stu-id="23df1-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="23df1-140">Se si utilizzano file con estensione PFX di Windows, è necessario convertire tali formato tooPEM certificati.</span><span class="sxs-lookup"><span data-stu-id="23df1-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="23df1-141">un file PEM tooa file PFX, tooconvert utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="23df1-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="23df1-142">Per ulteriori informazioni, vedere hello [OpenSSL documentazione](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="23df1-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="23df1-143">Problemi di connessione</span><span class="sxs-lookup"><span data-stu-id="23df1-143">Connection issues</span></span>

<span data-ttu-id="23df1-144">Alcune operazioni potrebbero generare hello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="23df1-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="23df1-145">Verificare che hello specificato l'endpoint del cluster è disponibile e in attesa.</span><span class="sxs-lookup"><span data-stu-id="23df1-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="23df1-146">Inoltre, verificare che hello che dell'interfaccia utente di Service Fabric Explorer è disponibile all'host e porta.</span><span class="sxs-lookup"><span data-stu-id="23df1-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="23df1-147">endpoint hello tooupdate, utilizzare `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="23df1-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="23df1-148">Log dettagliati</span><span class="sxs-lookup"><span data-stu-id="23df1-148">Detailed logs</span></span>

<span data-ttu-id="23df1-149">I log dettagliati si rivelano spesso utili per il debug o la segnalazione di un problema.</span><span class="sxs-lookup"><span data-stu-id="23df1-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="23df1-150">CLI di Azure offre globale `--debug` flag che consentono di aumentare il livello di dettaglio hello dei file di log.</span><span class="sxs-lookup"><span data-stu-id="23df1-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="23df1-151">Informazioni sui comandi e sintassi</span><span class="sxs-lookup"><span data-stu-id="23df1-151">Command help and syntax</span></span>

<span data-ttu-id="23df1-152">Eseguire i comandi di Service Fabric hello stesse convenzioni CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="23df1-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="23df1-153">Per informazioni su un comando specifico o un gruppo di comandi, utilizzare hello `-h` flag:</span><span class="sxs-lookup"><span data-stu-id="23df1-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="23df1-154">Di seguito è riportato un altro esempio:</span><span class="sxs-lookup"><span data-stu-id="23df1-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
