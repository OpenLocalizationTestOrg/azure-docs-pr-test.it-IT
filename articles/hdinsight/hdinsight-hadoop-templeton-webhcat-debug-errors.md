---
title: aaaUnderstand e risolvere gli errori di WebHCat in HDInsight - Azure | Documenti Microsoft
description: "Informazioni su come gli errori più comuni di tooabout restituito da WebHCat in HDInsight e come tooresolve li."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="c7e8b-103">Comprendere e risolvere gli errori ricevuti da WebHCat in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7e8b-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="c7e8b-104">Informazioni sugli errori ricevuti quando si utilizza WebHCat con HDInsight e come tooresolve li.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="c7e8b-105">WebHCat viene utilizzata internamente dagli strumenti sul lato client, ad esempio Azure PowerShell e hello Data Lake Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="c7e8b-106">Che cos'è WebHCat</span><span class="sxs-lookup"><span data-stu-id="c7e8b-106">What is WebHCat</span></span>

<span data-ttu-id="c7e8b-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) è un'API REST per [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), un livello di gestione tabelle e risorse di archiviazione per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="c7e8b-108">WebHCat è abilitata per impostazione predefinita nei cluster HDInsight e viene utilizzato dai processi di toosubmit vari strumenti, ottenere lo stato del processo e così via senza registrazione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="c7e8b-109">Modifica della configurazione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7e8b-110">Numerosi errori hello elencati in questo documento si verificano perché è stato superato un numero massimo configurato.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="c7e8b-111">Quando la procedura di risoluzione hello viene indicato che è possibile modificare un valore, è necessario utilizzare uno di seguito modifica hello tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="c7e8b-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="c7e8b-112">Per **Windows** cluster: usare un valore di hello tooconfigure azione script durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="c7e8b-113">Per altre informazioni, vedere [Sviluppare azioni di script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="c7e8b-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="c7e8b-114">Per **Linux** cluster: valore di hello toomodify utilizzare Ambari (web o l'API REST).</span><span class="sxs-lookup"><span data-stu-id="c7e8b-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="c7e8b-115">Per altre informazioni, vedere [Gestire HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7e8b-116">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c7e8b-117">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c7e8b-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="c7e8b-118">Configurazione predefinita</span><span class="sxs-lookup"><span data-stu-id="c7e8b-118">Default configuration</span></span>

<span data-ttu-id="c7e8b-119">Se viene superato hello seguente i valori predefiniti, può influire negativamente sulle prestazioni WebHCat o causare errori:</span><span class="sxs-lookup"><span data-stu-id="c7e8b-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="c7e8b-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-120">Setting</span></span> | <span data-ttu-id="c7e8b-121">Risultato</span><span class="sxs-lookup"><span data-stu-id="c7e8b-121">What it does</span></span> | <span data-ttu-id="c7e8b-122">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="c7e8b-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c7e8b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="c7e8b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="c7e8b-124">numero massimo di processi che possono essere attive contemporaneamente Hello (in sospeso o in esecuzione)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="c7e8b-125">10.000</span><span class="sxs-lookup"><span data-stu-id="c7e8b-125">10,000</span></span> |
| <span data-ttu-id="c7e8b-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="c7e8b-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="c7e8b-127">numero massimo di Hello di richieste che possono essere serviti contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="c7e8b-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="c7e8b-128">20</span><span class="sxs-lookup"><span data-stu-id="c7e8b-128">20</span></span> |
| <span data-ttu-id="c7e8b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="c7e8b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="c7e8b-130">Hello numero di giorni per cui la cronologia dei processi di conservazione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="c7e8b-131">7 giorni</span><span class="sxs-lookup"><span data-stu-id="c7e8b-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="c7e8b-132">Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="c7e8b-132">Too many requests</span></span>

<span data-ttu-id="c7e8b-133">**Codice di stato HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="c7e8b-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="c7e8b-134">Causa</span><span class="sxs-lookup"><span data-stu-id="c7e8b-134">Cause</span></span> | <span data-ttu-id="c7e8b-135">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="c7e8b-136">È stato superato hello massimo di richieste simultanee gestite da WebHCat al minuto (impostazione predefinita 20)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="c7e8b-137">Ridurre tooensure il carico di lavoro che non presenta più di hello numero massimo di richieste simultanee o aumentare il limite di richieste simultanee hello modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="c7e8b-138">Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="c7e8b-139">Server non disponibile</span><span class="sxs-lookup"><span data-stu-id="c7e8b-139">Server unavailable</span></span>

<span data-ttu-id="c7e8b-140">**Codice di stato HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="c7e8b-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="c7e8b-141">Causa</span><span class="sxs-lookup"><span data-stu-id="c7e8b-141">Cause</span></span> | <span data-ttu-id="c7e8b-142">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="c7e8b-143">Questo codice di stato si verifica in genere durante il failover tra hello primari e secondari nodo head per cluster hello</span><span class="sxs-lookup"><span data-stu-id="c7e8b-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="c7e8b-144">Attendere due minuti, quindi ripetere l'operazione di hello</span><span class="sxs-lookup"><span data-stu-id="c7e8b-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="c7e8b-145">Contenuto richiesta non valido: impossibile trovare il processo</span><span class="sxs-lookup"><span data-stu-id="c7e8b-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="c7e8b-146">**Codice di stato HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="c7e8b-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="c7e8b-147">Causa</span><span class="sxs-lookup"><span data-stu-id="c7e8b-147">Cause</span></span> | <span data-ttu-id="c7e8b-148">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="c7e8b-149">I dettagli dei processi sono stati rimossi in base alla cronologia processo hello pulitura</span><span class="sxs-lookup"><span data-stu-id="c7e8b-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="c7e8b-150">periodo di memorizzazione Hello predefinito per la cronologia processo è 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="c7e8b-151">periodo di memorizzazione predefinito Hello può essere cambiato modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="c7e8b-152">Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="c7e8b-153">Processo è stato terminato a causa di failover tooa</span><span class="sxs-lookup"><span data-stu-id="c7e8b-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="c7e8b-154">Ripetere l'invio di processi di backup tootwo minuti</span><span class="sxs-lookup"><span data-stu-id="c7e8b-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="c7e8b-155">È stato utilizzato un ID processo non valido</span><span class="sxs-lookup"><span data-stu-id="c7e8b-155">An Invalid job id was used</span></span> |<span data-ttu-id="c7e8b-156">Controllare se l'id di processo hello è corretto</span><span class="sxs-lookup"><span data-stu-id="c7e8b-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="c7e8b-157">Gateway non valido</span><span class="sxs-lookup"><span data-stu-id="c7e8b-157">Bad gateway</span></span>

<span data-ttu-id="c7e8b-158">**Codice di stato HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="c7e8b-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="c7e8b-159">Causa</span><span class="sxs-lookup"><span data-stu-id="c7e8b-159">Cause</span></span> | <span data-ttu-id="c7e8b-160">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="c7e8b-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="c7e8b-161">Interno operazione di garbage collection in hello WebHCat processo</span><span class="sxs-lookup"><span data-stu-id="c7e8b-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="c7e8b-162">Attendere che l'operazione di garbage collection toofinish o riavviare servizio WebHCat hello</span><span class="sxs-lookup"><span data-stu-id="c7e8b-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="c7e8b-163">Timeout in attesa di una risposta dal servizio ResourceManager hello.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="c7e8b-164">Questo errore può verificarsi quando il numero di hello delle applicazioni attive esce massimo configurato di hello (impostazione predefinita a 10.000)</span><span class="sxs-lookup"><span data-stu-id="c7e8b-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="c7e8b-165">Attende attualmente in esecuzione processi toocomplete o aumentare il limite di processi simultanei di hello modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="c7e8b-166">Per ulteriori informazioni, vedere hello [Modifica configurazione](#modifying-configuration) sezione.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="c7e8b-167">Il tentativo di tutti i processi tramite hello tooretrieve [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) chiamata durante `Fields` è troppo`*`</span><span class="sxs-lookup"><span data-stu-id="c7e8b-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="c7e8b-168">Non recuperare i dettagli di *tutti* i processi.</span><span class="sxs-lookup"><span data-stu-id="c7e8b-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="c7e8b-169">Usare invece `jobid` tooretrieve dettagli per i processi di maggiori solo a determinati id di processo. Oppure, non utilizzare `Fields`</span><span class="sxs-lookup"><span data-stu-id="c7e8b-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="c7e8b-170">servizio WebHCat Hello è inattivo durante il failover del nodo head</span><span class="sxs-lookup"><span data-stu-id="c7e8b-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="c7e8b-171">Attendere per due minuti e ripetere l'operazione hello</span><span class="sxs-lookup"><span data-stu-id="c7e8b-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="c7e8b-172">Sono presenti più di 500 processi in sospeso inviati tramite WebHCat</span><span class="sxs-lookup"><span data-stu-id="c7e8b-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="c7e8b-173">Attendere il completamento dei processi attualmente in sospeso prima di inviare altri processi</span><span class="sxs-lookup"><span data-stu-id="c7e8b-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
