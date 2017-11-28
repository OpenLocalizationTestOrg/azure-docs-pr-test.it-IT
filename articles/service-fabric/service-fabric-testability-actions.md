---
title: errori aaaSimulate in Azure microservizi | Documenti Microsoft
description: "In questo articolo comunica sulle azioni di testabilità hello disponibili in Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="e07c5-103">Azioni di Testabilità</span><span class="sxs-lookup"><span data-stu-id="e07c5-103">Testability actions</span></span>
<span data-ttu-id="e07c5-104">In ordine toosimulate un'infrastruttura affidabile, Azure Service Fabric fornisce sviluppatore hello e con toosimulate modi diversi del mondo reale errori e le transizioni di stato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="e07c5-105">esposti come azioni di testabilità.</span><span class="sxs-lookup"><span data-stu-id="e07c5-105">These are exposed as testability actions.</span></span> <span data-ttu-id="e07c5-106">azioni Hello sono hello API di basso livello che causano un attacco intrusivo nel codice di errore specifico, la transizione dello stato o la convalida.</span><span class="sxs-lookup"><span data-stu-id="e07c5-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="e07c5-107">La combinazione di queste azioni consente di scrivere scenari di test completi per i servizi.</span><span class="sxs-lookup"><span data-stu-id="e07c5-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="e07c5-108">Service Fabric fornisce alcuni scenari di test comuni costituiti da queste azioni.</span><span class="sxs-lookup"><span data-stu-id="e07c5-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="e07c5-109">Si consiglia di utilizzare questi scenari predefiniti, che vengono scelti attentamente le transizioni di stato comuni tootest e casi di errore.</span><span class="sxs-lookup"><span data-stu-id="e07c5-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="e07c5-110">Tuttavia, azioni possono essere scenari di test personalizzata toocreate utilizzato quando si desidera tooadd copertura per gli scenari che non rientrano scenari incorporato hello ancora o che sono personalizzati specifici per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="e07c5-111">In c# le implementazioni di azioni di hello si trovano in hello System.Fabric.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="e07c5-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="e07c5-112">modulo di PowerShell dell'infrastruttura di sistema Hello viene trovato nell'assembly Microsoft.ServiceFabric.Powershell.dll hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="e07c5-113">Come parte dell'installazione di runtime, hello modulo ServiceFabric di PowerShell è installato tooallow per facilità d'uso.</span><span class="sxs-lookup"><span data-stu-id="e07c5-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="e07c5-114">Azioni di errore normali e anomale</span><span class="sxs-lookup"><span data-stu-id="e07c5-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="e07c5-115">Le azioni di Testabilità sono classificate in due bucket principali:</span><span class="sxs-lookup"><span data-stu-id="e07c5-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="e07c5-116">Errori anomali: questi errori simulano errori come il riavvio del computer e gli arresti anomali dei processi.</span><span class="sxs-lookup"><span data-stu-id="e07c5-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="e07c5-117">In questi casi di errori, il contesto di esecuzione hello del processo di interruzione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="e07c5-118">Ciò significa che alcuna pulizia dello stato di hello può essere eseguito prima dell'applicazione hello è stato riavviato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="e07c5-119">Errori normali: questi errori simulano azioni normali come gli spostamenti delle repliche e le eliminazioni attivate dal bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e07c5-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="e07c5-120">In questi casi, il servizio di hello Ottiene una notifica di hello Chiudi e possibile pulire lo stato di hello prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="e07c5-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="e07c5-121">Per la convalida di qualità migliore, eseguire il servizio di hello e carico di lavoro di business durante la generazione di diversi errori normale e anomali.</span><span class="sxs-lookup"><span data-stu-id="e07c5-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="e07c5-122">Errori anomali esercitare scenari in cui il processo di servizio hello termina improvvisamente centro hello di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e07c5-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="e07c5-123">Ciò consente di verificare il percorso di recupero hello una volta ripristinato replica del servizio hello dall'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="e07c5-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="e07c5-124">Ciò consentirà di verificare la coerenza dei dati e se lo stato del servizio hello viene mantenuto correttamente dopo gli errori.</span><span class="sxs-lookup"><span data-stu-id="e07c5-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="e07c5-125">Hello altri set di errori (hello normale) verificare che il servizio hello reagisce correttamente tooreplicas viene spostata dal Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e07c5-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="e07c5-126">Ciò consente di verificare la gestione dell'annullamento nel metodo RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="e07c5-127">servizio Hello deve toocheck hello annullamento token elaborate per impostare correttamente il salvataggio dello stato ed esce dal metodo RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="e07c5-128">Elenco delle azioni di Testabilità</span><span class="sxs-lookup"><span data-stu-id="e07c5-128">Testability actions list</span></span>
| <span data-ttu-id="e07c5-129">Azione</span><span class="sxs-lookup"><span data-stu-id="e07c5-129">Action</span></span> | <span data-ttu-id="e07c5-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e07c5-130">Description</span></span> | <span data-ttu-id="e07c5-131">API gestita</span><span class="sxs-lookup"><span data-stu-id="e07c5-131">Managed API</span></span> | <span data-ttu-id="e07c5-132">Cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="e07c5-132">PowerShell cmdlet</span></span> | <span data-ttu-id="e07c5-133">Errori normali/anomali</span><span class="sxs-lookup"><span data-stu-id="e07c5-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e07c5-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="e07c5-134">CleanTestState</span></span> |<span data-ttu-id="e07c5-135">Rimuove tutti gli stati di test hello dal cluster hello in caso di chiusura non valido di driver di test hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="e07c5-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-136">CleanTestStateAsync</span></span> |<span data-ttu-id="e07c5-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="e07c5-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="e07c5-138">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="e07c5-138">Not applicable</span></span> |
| <span data-ttu-id="e07c5-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="e07c5-139">InvokeDataLoss</span></span> |<span data-ttu-id="e07c5-140">Provoca la perdita di dati in una partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="e07c5-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="e07c5-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="e07c5-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="e07c5-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="e07c5-143">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-143">Graceful</span></span> |
| <span data-ttu-id="e07c5-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e07c5-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="e07c5-145">Inserisce una partizione del servizio con stato in una perdita di quorum.</span><span class="sxs-lookup"><span data-stu-id="e07c5-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="e07c5-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="e07c5-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="e07c5-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="e07c5-148">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-148">Graceful</span></span> |
| <span data-ttu-id="e07c5-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="e07c5-149">Move Primary</span></span> |<span data-ttu-id="e07c5-150">Sposta hello specificato replica primaria di un nodo di servizio con stato toohello cluster specificato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="e07c5-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-151">MovePrimaryAsync</span></span> |<span data-ttu-id="e07c5-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="e07c5-153">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-153">Graceful</span></span> |
| <span data-ttu-id="e07c5-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="e07c5-154">Move Secondary</span></span> |<span data-ttu-id="e07c5-155">Sposta una replica secondaria hello corrente di un nodo di cluster diverso tooa servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="e07c5-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="e07c5-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="e07c5-158">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-158">Graceful</span></span> |
| <span data-ttu-id="e07c5-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-159">RemoveReplica</span></span> |<span data-ttu-id="e07c5-160">Simula un errore di replica tramite la rimozione di una replica da un cluster.</span><span class="sxs-lookup"><span data-stu-id="e07c5-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="e07c5-161">Questo comporta la chiusura replica hello e passerà il toorole 'None', il relativo stato rimozione dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="e07c5-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="e07c5-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="e07c5-164">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-164">Graceful</span></span> |
| <span data-ttu-id="e07c5-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="e07c5-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="e07c5-166">Simula un errore di processo del pacchetto di codice mediante il riavvio di un pacchetto di codice distribuito in un nodo in un cluster.</span><span class="sxs-lookup"><span data-stu-id="e07c5-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="e07c5-167">Questo processo pacchetto codice hello, che verrà riavviato tutti hello utente servizio le repliche ospitate in tale processo si interrompe.</span><span class="sxs-lookup"><span data-stu-id="e07c5-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="e07c5-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="e07c5-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="e07c5-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="e07c5-170">Anomalo</span><span class="sxs-lookup"><span data-stu-id="e07c5-170">Ungraceful</span></span> |
| <span data-ttu-id="e07c5-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-171">RestartNode</span></span> |<span data-ttu-id="e07c5-172">Simula un errore del nodo cluster Infrastruttura di servizi tramite il riavvio di un nodo.</span><span class="sxs-lookup"><span data-stu-id="e07c5-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="e07c5-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-173">RestartNodeAsync</span></span> |<span data-ttu-id="e07c5-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="e07c5-175">Anomalo</span><span class="sxs-lookup"><span data-stu-id="e07c5-175">Ungraceful</span></span> |
| <span data-ttu-id="e07c5-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="e07c5-176">RestartPartition</span></span> |<span data-ttu-id="e07c5-177">Simula uno scenario di blackout del data center o del cluster mediante il riavvio di alcune o di tutte le repliche di una partizione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="e07c5-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-178">RestartPartitionAsync</span></span> |<span data-ttu-id="e07c5-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="e07c5-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="e07c5-180">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-180">Graceful</span></span> |
| <span data-ttu-id="e07c5-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-181">RestartReplica</span></span> |<span data-ttu-id="e07c5-182">Simula un errore di replica tramite il riavvio di una replica persistente in un cluster, la chiusura replica hello e riaprirlo.</span><span class="sxs-lookup"><span data-stu-id="e07c5-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="e07c5-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-183">RestartReplicaAsync</span></span> |<span data-ttu-id="e07c5-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="e07c5-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="e07c5-185">Normale</span><span class="sxs-lookup"><span data-stu-id="e07c5-185">Graceful</span></span> |
| <span data-ttu-id="e07c5-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-186">StartNode</span></span> |<span data-ttu-id="e07c5-187">Avvia un nodo in un cluster già arrestato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="e07c5-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-188">StartNodeAsync</span></span> |<span data-ttu-id="e07c5-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="e07c5-190">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="e07c5-190">Not applicable</span></span> |
| <span data-ttu-id="e07c5-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-191">StopNode</span></span> |<span data-ttu-id="e07c5-192">Simula l’errore in un nodo mediante l’arresto di un nodo in un cluster.</span><span class="sxs-lookup"><span data-stu-id="e07c5-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="e07c5-193">nodo Hello resterà verso il basso fino a quando viene chiamato StartNode.</span><span class="sxs-lookup"><span data-stu-id="e07c5-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="e07c5-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-194">StopNodeAsync</span></span> |<span data-ttu-id="e07c5-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="e07c5-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="e07c5-196">Anomalo</span><span class="sxs-lookup"><span data-stu-id="e07c5-196">Ungraceful</span></span> |
| <span data-ttu-id="e07c5-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="e07c5-197">ValidateApplication</span></span> |<span data-ttu-id="e07c5-198">Convalida integrità di tutti i servizi di Service Fabric all'interno di un'applicazione, in genere dopo la generazione di un errore nel sistema hello e disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="e07c5-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="e07c5-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="e07c5-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="e07c5-201">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="e07c5-201">Not applicable</span></span> |
| <span data-ttu-id="e07c5-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="e07c5-202">ValidateService</span></span> |<span data-ttu-id="e07c5-203">Convalida la disponibilità di hello e l'integrità di un servizio di Service Fabric, in genere dopo la generazione di un errore nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="e07c5-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="e07c5-204">ValidateServiceAsync</span></span> |<span data-ttu-id="e07c5-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="e07c5-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="e07c5-206">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="e07c5-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="e07c5-207">Esecuzione di un'azione di testabilità con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e07c5-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="e07c5-208">In questa esercitazione illustra come toorun un'azione di testabilità tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e07c5-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="e07c5-209">Si apprenderà come toorun un'azione di testabilità rispetto a un cluster (uno-box) locale o un cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c5-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="e07c5-210">Microsoft.Fabric.Powershell.dll - hello modulo PowerShell di Service Fabric - viene installato automaticamente quando si installa Microsoft Service Fabric MSI hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="e07c5-211">modulo Hello viene caricato automaticamente quando si apre un prompt dei comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e07c5-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="e07c5-212">Sezioni dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="e07c5-212">Tutorial segments:</span></span>

* [<span data-ttu-id="e07c5-213">Eseguire un'azione su un cluster di una casella</span><span class="sxs-lookup"><span data-stu-id="e07c5-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="e07c5-214">Eseguire un'azione su un cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="e07c5-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="e07c5-215">Eseguire un'azione su un cluster di una casella</span><span class="sxs-lookup"><span data-stu-id="e07c5-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="e07c5-216">toorun un'azione di testabilità su un cluster locale, connettersi innanzitutto toohello cluster e il prompt PowerShell hello aperto in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="e07c5-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="e07c5-217">Esaminiamo hello **riavvio ServiceFabricNode** azione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="e07c5-218">Qui hello azione **riavvio ServiceFabricNode** è in esecuzione in un nodo denominato "Node1".</span><span class="sxs-lookup"><span data-stu-id="e07c5-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="e07c5-219">modalità di terminazione Hello specifica non deve verificare se azione di riavvio del nodo hello è effettivamente riuscito.</span><span class="sxs-lookup"><span data-stu-id="e07c5-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="e07c5-220">Modalità di completamento hello specificando come "Verifica" determinerà tooverify se l'azione di riavvio hello è effettivamente riuscito.</span><span class="sxs-lookup"><span data-stu-id="e07c5-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="e07c5-221">Anziché specificare direttamente il nodo hello in base al nome, è possibile specificare tramite un tipo di chiave e hello partizione della replica, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e07c5-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="e07c5-222">**Riavvio ServiceFabricNode** deve essere un nodo di Service Fabric in un cluster toorestart utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="e07c5-223">Processo di Fabric.exe hello, che verrà riavviato tutte hello sistema utente e servizio servizio repliche ospitate su tale nodo verrà interrotta.</span><span class="sxs-lookup"><span data-stu-id="e07c5-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="e07c5-224">Utilizzando questo tootest API del servizio consente di rilevare i bug ai percorsi di recupero di failover hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="e07c5-225">Consente di simulare errori di nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="e07c5-226">Hello schermata riportata di seguito viene illustrato hello **riavvio ServiceFabricNode** comando testabilità azione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="e07c5-227">Hello di output di hello innanzitutto **Get ServiceFabricNode** (un cmdlet dal modulo di PowerShell di Service Fabric hello) viene illustrato il cluster locale hello include cinque nodi: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="e07c5-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="e07c5-228">Dopo l'azione di testabilità hello (cmdlet) **riavvio ServiceFabricNode** viene eseguita nel nodo hello, denominato Node.4, vediamo tempi di attività del nodo hello è stata reimpostata.</span><span class="sxs-lookup"><span data-stu-id="e07c5-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="e07c5-229">Eseguire un'azione su un cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="e07c5-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="e07c5-230">Esecuzione di un'azione di testabilità (tramite PowerShell) su un cluster di Azure è l'azione hello toorunning simile su un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="e07c5-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="e07c5-231">Hello solo differenza è che, prima di eseguire l'azione di hello, anziché connessione cluster locale toohello, è necessario tooconnect toohello Azure prima del cluster.</span><span class="sxs-lookup"><span data-stu-id="e07c5-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="e07c5-232">Esecuzione di un'azione di testabilità con C&#35;</span><span class="sxs-lookup"><span data-stu-id="e07c5-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="e07c5-233">toorun un'azione di testabilità mediante c#, è necessario innanzitutto tooconnect toohello cluster utilizzando FabricClient.</span><span class="sxs-lookup"><span data-stu-id="e07c5-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="e07c5-234">Ottenere quindi hello parametri necessari toorun hello azione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="e07c5-235">È possibile utilizzare diversi parametri toorun hello stessa azione.</span><span class="sxs-lookup"><span data-stu-id="e07c5-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="e07c5-236">Ricerca di hello RestartServiceFabricNode action toorun unidirezionale è utilizzando le informazioni sul nodo hello (nome del nodo e ID istanza del nodo) in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e07c5-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="e07c5-237">Spiegazione di alcuni parametri:</span><span class="sxs-lookup"><span data-stu-id="e07c5-237">Parameter explanation:</span></span>

* <span data-ttu-id="e07c5-238">**CompleteMode** specifica che la modalità hello non deve verificare se azione di riavvio hello è effettivamente riuscito.</span><span class="sxs-lookup"><span data-stu-id="e07c5-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="e07c5-239">Modalità di completamento hello specificando come "Verifica" determinerà tooverify se l'azione di riavvio hello è effettivamente riuscito.</span><span class="sxs-lookup"><span data-stu-id="e07c5-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="e07c5-240">**OperationTimeout** set hello di hello operazione toofinish intervallo di tempo prima che venga generata un'eccezione TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="e07c5-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="e07c5-241">**CancellationToken** consente un toobe in sospeso chiamata annullata.</span><span class="sxs-lookup"><span data-stu-id="e07c5-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="e07c5-242">Anziché specificare direttamente il nodo hello in base al nome, è possibile specificare tramite un tipo di chiave e hello partizione della replica.</span><span class="sxs-lookup"><span data-stu-id="e07c5-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="e07c5-243">Per altre informazioni vedere [PartitionSelector e ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="e07c5-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="e07c5-244">PartitionSelector e ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="e07c5-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="e07c5-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="e07c5-245">PartitionSelector</span></span>
<span data-ttu-id="e07c5-246">PartitionSelector è un helper esposto in testabilità ed è tooselect usato un oggetto specifico di partizione in cui tooperform hello testabilità azioni.</span><span class="sxs-lookup"><span data-stu-id="e07c5-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="e07c5-247">Può essere utilizzato tooselect una partizione specifica se l'ID di partizione hello è noto in anticipo.</span><span class="sxs-lookup"><span data-stu-id="e07c5-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="e07c5-248">In alternativa, è possibile fornire la chiave di partizione hello e operazione hello risolverà l'ID di partizione hello internamente.</span><span class="sxs-lookup"><span data-stu-id="e07c5-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="e07c5-249">È anche possibile hello selezionare una partizione casuale.</span><span class="sxs-lookup"><span data-stu-id="e07c5-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="e07c5-250">toouse questo supporto, creare l'oggetto PartitionSelector hello e selezionare la partizione hello utilizzando uno dei metodi di hello Select *.</span><span class="sxs-lookup"><span data-stu-id="e07c5-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="e07c5-251">Passare quindi hello PartitionSelector oggetto toohello API che lo richiede.</span><span class="sxs-lookup"><span data-stu-id="e07c5-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="e07c5-252">Se viene selezionata alcuna opzione, per impostazione predefinita la partizione casuale tooa.</span><span class="sxs-lookup"><span data-stu-id="e07c5-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="e07c5-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="e07c5-253">ReplicaSelector</span></span>
<span data-ttu-id="e07c5-254">ReplicaSelector è un helper esposto in testabilità e viene utilizzato toohelp selezionare una replica su quali tooperform hello testabilità azioni.</span><span class="sxs-lookup"><span data-stu-id="e07c5-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="e07c5-255">Può essere utilizzato tooselect una replica specifica se l'ID replica hello è noto in anticipo.</span><span class="sxs-lookup"><span data-stu-id="e07c5-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="e07c5-256">Inoltre, è possibile hello la selezione di una replica primaria o secondaria casuale.</span><span class="sxs-lookup"><span data-stu-id="e07c5-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="e07c5-257">ReplicaSelector deriva da PartitionSelector, pertanto è necessario tooselect entrambi hello replica e hello partizione in cui si desidera operazione testabilità di hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="e07c5-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="e07c5-258">toouse questo supporto, creare un oggetto ReplicaSelector e set di partizioni di replica e hello hello tooselect hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e07c5-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="e07c5-259">È quindi possibile passare in hello API che lo richiede.</span><span class="sxs-lookup"><span data-stu-id="e07c5-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="e07c5-260">Se viene selezionata alcuna opzione, per impostazione predefinita replica casuale tooa e partizione casuale.</span><span class="sxs-lookup"><span data-stu-id="e07c5-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="e07c5-261">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e07c5-261">Next steps</span></span>
* [<span data-ttu-id="e07c5-262">Scenari di testabilità</span><span class="sxs-lookup"><span data-stu-id="e07c5-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="e07c5-263">Come tootest il servizio</span><span class="sxs-lookup"><span data-stu-id="e07c5-263">How tootest your service</span></span>
  * [<span data-ttu-id="e07c5-264">Simulare gli errori durante i carichi di lavoro del servizio</span><span class="sxs-lookup"><span data-stu-id="e07c5-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="e07c5-265">Errori di comunicazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="e07c5-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

