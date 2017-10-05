---
title: Comprendere e risolvere gli errori di WebHCat in HDInsight - Azure | Microsoft Docs
description: Informazioni sugli errori comuni restituiti da WebHCat in HDInsight e su come risolverli.
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
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="cfb0b-103">Comprendere e risolvere gli errori ricevuti da WebHCat in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cfb0b-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="cfb0b-104">Informazioni sugli errori che si ricevono durante l'utilizzo di WebHCat con HDInsight e su come risolverli.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="cfb0b-105">WebHCat viene usato internamente dagli strumenti sul lato client, ad esempio Azure PowerShell e Strumenti Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="cfb0b-106">Che cos'è WebHCat</span><span class="sxs-lookup"><span data-stu-id="cfb0b-106">What is WebHCat</span></span>

<span data-ttu-id="cfb0b-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) è un'API REST per [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), un livello di gestione tabelle e risorse di archiviazione per Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="cfb0b-108">WebHCat è abilitato per impostazione predefinita nei cluster HDInsight e viene usato da vari strumenti per inviare processi, recuperare lo stato dei processi e così via, senza effettuare l'accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="cfb0b-109">Modifica della configurazione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfb0b-110">Alcuni degli errori elencati in questo documento si verificano perché è stato superato un valore massimo configurato.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="cfb0b-111">La procedura di risoluzione indica che è possibile modificare un valore, per eseguire la modifica è necessario usare uno dei seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="cfb0b-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="cfb0b-112">Per cluster **Windows** : usare un'azione di script per configurare il valore durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="cfb0b-113">Per altre informazioni, vedere [Sviluppare azioni di script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="cfb0b-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="cfb0b-114">Per cluster **Linux** : usare Ambari (web o API REST) per modificare il valore.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="cfb0b-115">Per altre informazioni, vedere [Gestire HDInsight tramite Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfb0b-116">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cfb0b-117">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cfb0b-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="cfb0b-118">Configurazione predefinita</span><span class="sxs-lookup"><span data-stu-id="cfb0b-118">Default configuration</span></span>

<span data-ttu-id="cfb0b-119">Il superamento dei valori predefiniti seguenti può determinare una riduzione delle prestazioni di WebHCat o la generazione di errori:</span><span class="sxs-lookup"><span data-stu-id="cfb0b-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="cfb0b-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-120">Setting</span></span> | <span data-ttu-id="cfb0b-121">Risultato</span><span class="sxs-lookup"><span data-stu-id="cfb0b-121">What it does</span></span> | <span data-ttu-id="cfb0b-122">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="cfb0b-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cfb0b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="cfb0b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="cfb0b-124">Il numero massimo di processi che possono essere attivi contemporaneamente (in sospeso o in esecuzione)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="cfb0b-125">10.000</span><span class="sxs-lookup"><span data-stu-id="cfb0b-125">10,000</span></span> |
| <span data-ttu-id="cfb0b-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="cfb0b-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="cfb0b-127">Il numero massimo di richieste che possono essere gestite contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="cfb0b-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="cfb0b-128">20</span><span class="sxs-lookup"><span data-stu-id="cfb0b-128">20</span></span> |
| <span data-ttu-id="cfb0b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="cfb0b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="cfb0b-130">Il numero di giorni durante i quali verrà mantenuta la cronologia del processo</span><span class="sxs-lookup"><span data-stu-id="cfb0b-130">The number of days that job history are retained</span></span> |<span data-ttu-id="cfb0b-131">7 giorni</span><span class="sxs-lookup"><span data-stu-id="cfb0b-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="cfb0b-132">Numero eccessivo di richieste</span><span class="sxs-lookup"><span data-stu-id="cfb0b-132">Too many requests</span></span>

<span data-ttu-id="cfb0b-133">**Codice di stato HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="cfb0b-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="cfb0b-134">Causa</span><span class="sxs-lookup"><span data-stu-id="cfb0b-134">Cause</span></span> | <span data-ttu-id="cfb0b-135">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="cfb0b-136">È stato superato il numero massimo di richieste contemporanee gestite da WebHCat al minuto (il valore predefinito è 20)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="cfb0b-137">Ridurre il carico di lavoro per garantire che non venga inviato più del numero massimo di richieste contemporanee o aumentare il limite di richieste contemporanee modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="cfb0b-138">Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="cfb0b-139">Server non disponibile</span><span class="sxs-lookup"><span data-stu-id="cfb0b-139">Server unavailable</span></span>

<span data-ttu-id="cfb0b-140">**Codice di stato HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="cfb0b-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="cfb0b-141">Causa</span><span class="sxs-lookup"><span data-stu-id="cfb0b-141">Cause</span></span> | <span data-ttu-id="cfb0b-142">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="cfb0b-143">Questo codice di stato si verifica in genere durante il failover tra il nodo head primario e secondario per il cluster</span><span class="sxs-lookup"><span data-stu-id="cfb0b-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="cfb0b-144">Attendere due minuti, quindi ripetere l'operazione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="cfb0b-145">Contenuto richiesta non valido: impossibile trovare il processo</span><span class="sxs-lookup"><span data-stu-id="cfb0b-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="cfb0b-146">**Codice di stato HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="cfb0b-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="cfb0b-147">Causa</span><span class="sxs-lookup"><span data-stu-id="cfb0b-147">Cause</span></span> | <span data-ttu-id="cfb0b-148">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="cfb0b-149">I dettagli dei processi sono stati rimossi dalla pulitura della cronologia dei processi</span><span class="sxs-lookup"><span data-stu-id="cfb0b-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="cfb0b-150">Il periodo di conservazione predefinito per la cronologia dei processi è 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="cfb0b-151">Il periodo di conservazione predefinito può essere cambiato modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="cfb0b-152">Per altre informazioni, vedere [Modifica della configurazione](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="cfb0b-153">Il processo è stato terminato a causa di un failover</span><span class="sxs-lookup"><span data-stu-id="cfb0b-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="cfb0b-154">Ripetere l'invio del processo per due minuti</span><span class="sxs-lookup"><span data-stu-id="cfb0b-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="cfb0b-155">È stato utilizzato un ID processo non valido</span><span class="sxs-lookup"><span data-stu-id="cfb0b-155">An Invalid job id was used</span></span> |<span data-ttu-id="cfb0b-156">Controllare se l'ID processo è corretto</span><span class="sxs-lookup"><span data-stu-id="cfb0b-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="cfb0b-157">Gateway non valido</span><span class="sxs-lookup"><span data-stu-id="cfb0b-157">Bad gateway</span></span>

<span data-ttu-id="cfb0b-158">**Codice di stato HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="cfb0b-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="cfb0b-159">Causa</span><span class="sxs-lookup"><span data-stu-id="cfb0b-159">Cause</span></span> | <span data-ttu-id="cfb0b-160">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="cfb0b-161">Operazione interna di Garbage Collection nel processo WebHCat</span><span class="sxs-lookup"><span data-stu-id="cfb0b-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="cfb0b-162">Attendere che l’operazione di Garbage Collection venga completata o riavviare il servizio WebHCat</span><span class="sxs-lookup"><span data-stu-id="cfb0b-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="cfb0b-163">Timeout in attesa di una risposta dal servizio Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="cfb0b-164">Questo errore può verificarsi quando il numero di applicazioni attive supera il numero massimo configurato (il valore predefinito è 10.000)</span><span class="sxs-lookup"><span data-stu-id="cfb0b-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="cfb0b-165">Attendere che i processi attualmente in esecuzione vengano completati o aumentare il limite di processi simultanei modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="cfb0b-166">Per altre informazioni, vedere la sezione [Modifica della configurazione](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="cfb0b-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="cfb0b-167">Quando si tenta di recuperare tutti i processi tramite la chiamata [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) mentre `Fields`è impostato su `*`</span><span class="sxs-lookup"><span data-stu-id="cfb0b-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="cfb0b-168">Non recuperare i dettagli di *tutti* i processi.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="cfb0b-169">Usare invece `jobid` per recuperare i dettagli solo dei processi successivi a un determinato ID processo.</span><span class="sxs-lookup"><span data-stu-id="cfb0b-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="cfb0b-170">Oppure, non utilizzare `Fields`</span><span class="sxs-lookup"><span data-stu-id="cfb0b-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="cfb0b-171">Il servizio WebHCat è inattivo durante il failover del nodo head</span><span class="sxs-lookup"><span data-stu-id="cfb0b-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="cfb0b-172">Attendere due minuti e ripetere l'operazione</span><span class="sxs-lookup"><span data-stu-id="cfb0b-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="cfb0b-173">Sono presenti più di 500 processi in sospeso inviati tramite WebHCat</span><span class="sxs-lookup"><span data-stu-id="cfb0b-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="cfb0b-174">Attendere il completamento dei processi attualmente in sospeso prima di inviare altri processi</span><span class="sxs-lookup"><span data-stu-id="cfb0b-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
