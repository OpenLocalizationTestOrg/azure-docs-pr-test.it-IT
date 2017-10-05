---
title: Simulare errori nei microservizi di Azure | Documentazione Microsoft
description: "In questo articolo vengono illustrate le azioni di Testabilità trovate in Infrastruttura di servizi di Microsoft Azure."
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
ms.openlocfilehash: c8ddc7732999ae555323bebaef60aa34c8f2ec17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="testability-actions"></a><span data-ttu-id="29ab6-103">Azioni di Testabilità</span><span class="sxs-lookup"><span data-stu-id="29ab6-103">Testability actions</span></span>
<span data-ttu-id="29ab6-104">Per simulare un'infrastruttura non affidabile, Azure Service Fabric offre agli sviluppatori la possibilità di simulare errori e transizioni di stato reali,</span><span class="sxs-lookup"><span data-stu-id="29ab6-104">In order to simulate an unreliable infrastructure, Azure Service Fabric provides you, the developer, with ways to simulate various real-world failures and state transitions.</span></span> <span data-ttu-id="29ab6-105">esposti come azioni di testabilità.</span><span class="sxs-lookup"><span data-stu-id="29ab6-105">These are exposed as testability actions.</span></span> <span data-ttu-id="29ab6-106">Le azioni sono le API di basso livello che causano una specifica fault injection, una transizione di stato o una convalida.</span><span class="sxs-lookup"><span data-stu-id="29ab6-106">The actions are the low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="29ab6-107">La combinazione di queste azioni consente di scrivere scenari di test completi per i servizi.</span><span class="sxs-lookup"><span data-stu-id="29ab6-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="29ab6-108">Service Fabric fornisce alcuni scenari di test comuni costituiti da queste azioni.</span><span class="sxs-lookup"><span data-stu-id="29ab6-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="29ab6-109">È consigliabile usare questi scenari predefiniti, poiché vengono scelti con attenzione per testare le transizioni di stato e i casi di errore comuni.</span><span class="sxs-lookup"><span data-stu-id="29ab6-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen to test common state transitions and failure cases.</span></span> <span data-ttu-id="29ab6-110">È comunque possibile creare anche scenari di test personalizzati, costituiti dalle stesse azioni, quando si vuole aggiungere la copertura per scenari specifici di un'applicazione o non ancora presenti negli scenari integrati.</span><span class="sxs-lookup"><span data-stu-id="29ab6-110">However, actions can be used to create custom test scenarios when you want to add coverage for scenarios that are not covered by the built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="29ab6-111">Implementazioni in C# delle azioni sono disponibili nell'assembly System.Fabric.dll.</span><span class="sxs-lookup"><span data-stu-id="29ab6-111">C# implementations of the actions are found in the System.Fabric.dll assembly.</span></span> <span data-ttu-id="29ab6-112">Il modulo di PowerShell System Fabric si trova nell'assembly Microsoft.ServiceFabric.Powershell.dll.</span><span class="sxs-lookup"><span data-stu-id="29ab6-112">The System Fabric PowerShell module is found in the Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="29ab6-113">Nell'ambito dell'installazione del runtime viene installato il modulo ServiceFabric di PowerShell per garantire una maggiore semplicità d'uso.</span><span class="sxs-lookup"><span data-stu-id="29ab6-113">As part of runtime installation, the ServiceFabric PowerShell module is installed to allow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="29ab6-114">Azioni di errore normali e anomale</span><span class="sxs-lookup"><span data-stu-id="29ab6-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="29ab6-115">Le azioni di Testabilità sono classificate in due bucket principali:</span><span class="sxs-lookup"><span data-stu-id="29ab6-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="29ab6-116">Errori anomali: questi errori simulano errori come il riavvio del computer e gli arresti anomali dei processi.</span><span class="sxs-lookup"><span data-stu-id="29ab6-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="29ab6-117">In caso di errori di questo tipo, il contesto di esecuzione del processo si interrompe in modo brusco.</span><span class="sxs-lookup"><span data-stu-id="29ab6-117">In such cases of failures, the execution context of process stops abruptly.</span></span> <span data-ttu-id="29ab6-118">Non è quindi possibile eseguire alcuna pulizia dello stato prima che l'applicazione venga avviata nuovamente.</span><span class="sxs-lookup"><span data-stu-id="29ab6-118">This means no cleanup of the state can run before the application starts up again.</span></span>
* <span data-ttu-id="29ab6-119">Errori normali: questi errori simulano azioni normali come gli spostamenti delle repliche e le eliminazioni attivate dal bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="29ab6-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="29ab6-120">In questi casi, il servizio riceve una notifica dello stato di chiusura e può eseguire la pulizia dello stato prima di uscire.</span><span class="sxs-lookup"><span data-stu-id="29ab6-120">In such cases, the service gets a notification of the close and can clean up the state before exiting.</span></span>

<span data-ttu-id="29ab6-121">Per una convalida migliore in termini di qualità, eseguire il carico di lavoro del servizio e del business, includendo diversi errori normali e anomali.</span><span class="sxs-lookup"><span data-stu-id="29ab6-121">For better quality validation, run the service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="29ab6-122">Gli errori anomali danno luogo a scenari in cui il processo di servizio si chiude improvvisamente nel corso di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="29ab6-122">Ungraceful faults exercise scenarios where the service process abruptly exits in the middle of some workflow.</span></span> <span data-ttu-id="29ab6-123">Ciò consente di verificare il percorso di ripristino una volta che Service Fabric ripristina la replica del servizio.</span><span class="sxs-lookup"><span data-stu-id="29ab6-123">This tests  the recovery path once the service replica is restored by Service Fabric.</span></span> <span data-ttu-id="29ab6-124">Ciò consentirà di verificare la coerenza dei dati e se lo stato del servizio viene conservato correttamente dopo gli errori.</span><span class="sxs-lookup"><span data-stu-id="29ab6-124">This will help test data consistency and whether the service state is maintained correctly after failures.</span></span> <span data-ttu-id="29ab6-125">L'altro set di errori, ovvero gli errori normali, verifica che il servizio risponda correttamente alle repliche spostate da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29ab6-125">The other set of failures (the graceful failures) test that the service correctly reacts to replicas being moved around by Service Fabric.</span></span> <span data-ttu-id="29ab6-126">Ciò consente di verificare la gestione dell'annullamento nel metodo RunAsync.</span><span class="sxs-lookup"><span data-stu-id="29ab6-126">This tests handling of cancellation in the RunAsync method.</span></span> <span data-ttu-id="29ab6-127">Il servizio deve controllare che il token di annullamento sia impostato, salvarne correttamente lo stato e chiudere il metodo RunAsync.</span><span class="sxs-lookup"><span data-stu-id="29ab6-127">The service needs to check for the cancellation token being set, correctly save its state, and exit the RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="29ab6-128">Elenco delle azioni di Testabilità</span><span class="sxs-lookup"><span data-stu-id="29ab6-128">Testability actions list</span></span>
| <span data-ttu-id="29ab6-129">Azione</span><span class="sxs-lookup"><span data-stu-id="29ab6-129">Action</span></span> | <span data-ttu-id="29ab6-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="29ab6-130">Description</span></span> | <span data-ttu-id="29ab6-131">API gestita</span><span class="sxs-lookup"><span data-stu-id="29ab6-131">Managed API</span></span> | <span data-ttu-id="29ab6-132">Cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="29ab6-132">PowerShell cmdlet</span></span> | <span data-ttu-id="29ab6-133">Errori normali/anomali</span><span class="sxs-lookup"><span data-stu-id="29ab6-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="29ab6-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="29ab6-134">CleanTestState</span></span> |<span data-ttu-id="29ab6-135">Rimuove lo stato di tutti i test dal cluster in caso di arresto anomalo del driver di test.</span><span class="sxs-lookup"><span data-stu-id="29ab6-135">Removes all the test state from the cluster in case of a bad shutdown of the test driver.</span></span> |<span data-ttu-id="29ab6-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-136">CleanTestStateAsync</span></span> |<span data-ttu-id="29ab6-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="29ab6-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="29ab6-138">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="29ab6-138">Not applicable</span></span> |
| <span data-ttu-id="29ab6-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="29ab6-139">InvokeDataLoss</span></span> |<span data-ttu-id="29ab6-140">Provoca la perdita di dati in una partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="29ab6-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="29ab6-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="29ab6-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="29ab6-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="29ab6-143">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-143">Graceful</span></span> |
| <span data-ttu-id="29ab6-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="29ab6-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="29ab6-145">Inserisce una partizione del servizio con stato in una perdita di quorum.</span><span class="sxs-lookup"><span data-stu-id="29ab6-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="29ab6-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="29ab6-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="29ab6-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="29ab6-148">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-148">Graceful</span></span> |
| <span data-ttu-id="29ab6-149">Move Primary</span><span class="sxs-lookup"><span data-stu-id="29ab6-149">Move Primary</span></span> |<span data-ttu-id="29ab6-150">Sposta la replica primaria specificata di un servizio con stato nel nodo cluster specificato.</span><span class="sxs-lookup"><span data-stu-id="29ab6-150">Moves the specified primary replica of a stateful service to the specified cluster node.</span></span> |<span data-ttu-id="29ab6-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-151">MovePrimaryAsync</span></span> |<span data-ttu-id="29ab6-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="29ab6-153">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-153">Graceful</span></span> |
| <span data-ttu-id="29ab6-154">Move Secondary</span><span class="sxs-lookup"><span data-stu-id="29ab6-154">Move Secondary</span></span> |<span data-ttu-id="29ab6-155">Sposta la replica secondaria corrente di un servizio con stato a un nodo di cluster diverso.</span><span class="sxs-lookup"><span data-stu-id="29ab6-155">Moves the current secondary replica of a stateful service to a different cluster node.</span></span> |<span data-ttu-id="29ab6-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="29ab6-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="29ab6-158">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-158">Graceful</span></span> |
| <span data-ttu-id="29ab6-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-159">RemoveReplica</span></span> |<span data-ttu-id="29ab6-160">Simula un errore di replica tramite la rimozione di una replica da un cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="29ab6-161">In tal modo la replica verrà chiusa e passata al ruolo 'None', rimuovendo tutto lo stato dal cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-161">This will close the replica and will transition it to role 'None', removing all of its state from the cluster.</span></span> |<span data-ttu-id="29ab6-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="29ab6-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="29ab6-164">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-164">Graceful</span></span> |
| <span data-ttu-id="29ab6-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="29ab6-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="29ab6-166">Simula un errore di processo del pacchetto di codice mediante il riavvio di un pacchetto di codice distribuito in un nodo in un cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="29ab6-167">In questo modo, il processo del pacchetto di codice viene interrotto e verranno riavviate tutte le repliche del servizio utente ospitate nel processo.</span><span class="sxs-lookup"><span data-stu-id="29ab6-167">This aborts the code package process, which will restart all the user service replicas hosted in that process.</span></span> |<span data-ttu-id="29ab6-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="29ab6-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="29ab6-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="29ab6-170">Anomalo</span><span class="sxs-lookup"><span data-stu-id="29ab6-170">Ungraceful</span></span> |
| <span data-ttu-id="29ab6-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-171">RestartNode</span></span> |<span data-ttu-id="29ab6-172">Simula un errore del nodo cluster Infrastruttura di servizi tramite il riavvio di un nodo.</span><span class="sxs-lookup"><span data-stu-id="29ab6-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="29ab6-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-173">RestartNodeAsync</span></span> |<span data-ttu-id="29ab6-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="29ab6-175">Anomalo</span><span class="sxs-lookup"><span data-stu-id="29ab6-175">Ungraceful</span></span> |
| <span data-ttu-id="29ab6-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="29ab6-176">RestartPartition</span></span> |<span data-ttu-id="29ab6-177">Simula uno scenario di blackout del data center o del cluster mediante il riavvio di alcune o di tutte le repliche di una partizione.</span><span class="sxs-lookup"><span data-stu-id="29ab6-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="29ab6-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-178">RestartPartitionAsync</span></span> |<span data-ttu-id="29ab6-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="29ab6-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="29ab6-180">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-180">Graceful</span></span> |
| <span data-ttu-id="29ab6-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-181">RestartReplica</span></span> |<span data-ttu-id="29ab6-182">Simula un errore di replica mediante il riavvio di una replica persistente in un cluster, la chiusura della replica e quindi la riapertura.</span><span class="sxs-lookup"><span data-stu-id="29ab6-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing the replica and then reopening it.</span></span> |<span data-ttu-id="29ab6-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-183">RestartReplicaAsync</span></span> |<span data-ttu-id="29ab6-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="29ab6-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="29ab6-185">Normale</span><span class="sxs-lookup"><span data-stu-id="29ab6-185">Graceful</span></span> |
| <span data-ttu-id="29ab6-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-186">StartNode</span></span> |<span data-ttu-id="29ab6-187">Avvia un nodo in un cluster già arrestato.</span><span class="sxs-lookup"><span data-stu-id="29ab6-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="29ab6-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-188">StartNodeAsync</span></span> |<span data-ttu-id="29ab6-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="29ab6-190">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="29ab6-190">Not applicable</span></span> |
| <span data-ttu-id="29ab6-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-191">StopNode</span></span> |<span data-ttu-id="29ab6-192">Simula l’errore in un nodo mediante l’arresto di un nodo in un cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="29ab6-193">Il nodo resterà inattivo fino a quando non viene chiamato StartNode.</span><span class="sxs-lookup"><span data-stu-id="29ab6-193">The node will stay down until StartNode is called.</span></span> |<span data-ttu-id="29ab6-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-194">StopNodeAsync</span></span> |<span data-ttu-id="29ab6-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="29ab6-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="29ab6-196">Anomalo</span><span class="sxs-lookup"><span data-stu-id="29ab6-196">Ungraceful</span></span> |
| <span data-ttu-id="29ab6-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="29ab6-197">ValidateApplication</span></span> |<span data-ttu-id="29ab6-198">Convalida la disponibilità e l’integrità di tutti i servizi Infrastruttura di servizi all’interno dell’applicazione, in genere dopo aver causato un errore nel sistema.</span><span class="sxs-lookup"><span data-stu-id="29ab6-198">Validates the availability and health of all Service Fabric services within an application, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="29ab6-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="29ab6-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="29ab6-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="29ab6-201">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="29ab6-201">Not applicable</span></span> |
| <span data-ttu-id="29ab6-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="29ab6-202">ValidateService</span></span> |<span data-ttu-id="29ab6-203">Convalida la disponibilità e l’integrità di un servizio Infrastruttura di servizi, in genere dopo aver causato un errore nel sistema.</span><span class="sxs-lookup"><span data-stu-id="29ab6-203">Validates the availability and health of a Service Fabric service, usually after inducing some fault into the system.</span></span> |<span data-ttu-id="29ab6-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="29ab6-204">ValidateServiceAsync</span></span> |<span data-ttu-id="29ab6-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="29ab6-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="29ab6-206">Non applicabile</span><span class="sxs-lookup"><span data-stu-id="29ab6-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="29ab6-207">Esecuzione di un'azione di testabilità con PowerShell</span><span class="sxs-lookup"><span data-stu-id="29ab6-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="29ab6-208">Questa esercitazione illustra come eseguire un'azione di testabilità con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29ab6-208">This tutorial shows you how to run a testability action by using PowerShell.</span></span> <span data-ttu-id="29ab6-209">Si apprenderà come eseguire un'azione di testabilità in un cluster locale (di una casella) o in un cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="29ab6-209">You will learn how to run a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="29ab6-210">Microsoft.Fabric.Powershell.dll, il modulo di PowerShell Service Fabric, viene installato automaticamente quando si installa MSI di Microsoft Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29ab6-210">Microsoft.Fabric.Powershell.dll--the Service Fabric PowerShell module--is installed automatically when you install the Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="29ab6-211">e caricato automaticamente quando si apre un prompt di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29ab6-211">The module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="29ab6-212">Sezioni dell'esercitazione:</span><span class="sxs-lookup"><span data-stu-id="29ab6-212">Tutorial segments:</span></span>

* [<span data-ttu-id="29ab6-213">Eseguire un'azione su un cluster di una casella</span><span class="sxs-lookup"><span data-stu-id="29ab6-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="29ab6-214">Eseguire un'azione su un cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="29ab6-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="29ab6-215">Eseguire un'azione su un cluster di una casella</span><span class="sxs-lookup"><span data-stu-id="29ab6-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="29ab6-216">Per eseguire un'azione di testabilità su un cluster locale, è necessario in primo luogo connettersi al cluster e aprire il prompt di PowerShell in modalità amministratore.</span><span class="sxs-lookup"><span data-stu-id="29ab6-216">To run a testability action against a local cluster, first connect to the cluster and open the PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="29ab6-217">Esaminiamo l’azione **Restart-ServiceFabricNode** .</span><span class="sxs-lookup"><span data-stu-id="29ab6-217">Let us look at the **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="29ab6-218">Qui l'azione **Restart-ServiceFabricNode** è in esecuzione in un nodo denominato "Node1".</span><span class="sxs-lookup"><span data-stu-id="29ab6-218">Here the action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="29ab6-219">e la modalità di completamento specifica che l'esito positivo dell'azione di riavvio del nodo non verrà verificato.</span><span class="sxs-lookup"><span data-stu-id="29ab6-219">The completion mode specifies that it should not verify whether the restart-node action actually succeeded.</span></span> <span data-ttu-id="29ab6-220">Per verificare l'esito positivo dell'azione di riavvio, è necessario specificare la modalità di completamento come "Verify".</span><span class="sxs-lookup"><span data-stu-id="29ab6-220">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="29ab6-221">Anziché specificare direttamente il nodo mediante il nome, è possibile specificarlo tramite una chiave di partizione e il tipo di replica, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="29ab6-221">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="29ab6-222">**Restart-ServiceFabricNode** deve essere utilizzata per riavviare un nodo Infrastruttura di servizi in un cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-222">**Restart-ServiceFabricNode** should be used to restart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="29ab6-223">In questo modo, il processo Fabric.exe verrà interrotto e tutte le repliche del servizio di sistema e del servizio utente ospitate in quel nodo verranno riavviate.</span><span class="sxs-lookup"><span data-stu-id="29ab6-223">This will stop the Fabric.exe process, which will restart all of the system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="29ab6-224">L’uso di questa API per il test del servizio consente di rilevare bug lungo i percorsi di ripristino del failover.</span><span class="sxs-lookup"><span data-stu-id="29ab6-224">Using this API to test your service helps uncover bugs along the failover recovery paths.</span></span> <span data-ttu-id="29ab6-225">Consente di simulare gli errori dei nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-225">It helps simulate node failures in the cluster.</span></span>

<span data-ttu-id="29ab6-226">La schermata seguente mostra il comando di testabilità **Restart-ServiceFabricNode** in azione.</span><span class="sxs-lookup"><span data-stu-id="29ab6-226">The following screenshot shows the **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="29ab6-227">L'output del primo **Get ServiceFabricNode** (un cmdlet dal modulo PowerShell di ServiceFabric) mostra che il cluster locale ha cinque nodi: da Node.1 a Node.5.</span><span class="sxs-lookup"><span data-stu-id="29ab6-227">The output of the first **Get-ServiceFabricNode** (a cmdlet from the Service Fabric PowerShell module) shows that the local cluster has five nodes: Node.1 to Node.5.</span></span> <span data-ttu-id="29ab6-228">Dopo l'esecuzione dell'azione di testabilità (cmdlet) **Restart-ServiceFabricNode** sul nodo, denominato Node.4, noteremo che il tempo di attività del nodo è stato reimpostato.</span><span class="sxs-lookup"><span data-stu-id="29ab6-228">After the testability action (cmdlet) **Restart-ServiceFabricNode** is executed on the node, named Node.4, we see that the node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="29ab6-229">Eseguire un'azione su un cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="29ab6-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="29ab6-230">L'esecuzione di un'azione di testabilità (con PowerShell) su un cluster di Azure è simile all'esecuzione della stessa azione su un cluster locale.</span><span class="sxs-lookup"><span data-stu-id="29ab6-230">Running a testability action (by using PowerShell) against an Azure cluster is similar to running the action against a local cluster.</span></span> <span data-ttu-id="29ab6-231">L'unica differenza è che, prima di poter eseguire l'azione, invece di connettersi al cluster locale, è necessario connettersi al cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="29ab6-231">The only difference is that before you can run the action, instead of connecting to the local cluster, you need to connect to the Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="29ab6-232">Esecuzione di un'azione di testabilità con C&#35;</span><span class="sxs-lookup"><span data-stu-id="29ab6-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="29ab6-233">Per eseguire un'azione di testabilità con C#, è necessario prima connettersi al cluster tramite FabricClient.</span><span class="sxs-lookup"><span data-stu-id="29ab6-233">To run a testability action by using C#, first you need to connect to the cluster by using FabricClient.</span></span> <span data-ttu-id="29ab6-234">Ottenere quindi i parametri necessari per eseguire l'azione.</span><span class="sxs-lookup"><span data-stu-id="29ab6-234">Then obtain the parameters needed to run the action.</span></span> <span data-ttu-id="29ab6-235">Per eseguire la stessa azione possono essere utilizzati parametri diversi.</span><span class="sxs-lookup"><span data-stu-id="29ab6-235">Different parameters can be used to run the same action.</span></span>
<span data-ttu-id="29ab6-236">In merito all'azione RestartServiceFabricNode, per eseguirla è possibile usare le informazioni sul nodo (nodo del nome e ID dell'istanza del nodo) disponibili nel cluster.</span><span class="sxs-lookup"><span data-stu-id="29ab6-236">Looking at the RestartServiceFabricNode action, one way to run it is by using the node information (node name and node instance ID) in the cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="29ab6-237">Spiegazione di alcuni parametri:</span><span class="sxs-lookup"><span data-stu-id="29ab6-237">Parameter explanation:</span></span>

* <span data-ttu-id="29ab6-238">**CompleteMode** specifica che l'esito positivo dell'azione di riavvio non verrà verificato.</span><span class="sxs-lookup"><span data-stu-id="29ab6-238">**CompleteMode** specifies that the mode should not verify whether the restart action actually succeeded.</span></span> <span data-ttu-id="29ab6-239">Per verificare l'esito positivo dell'azione di riavvio, è necessario specificare la modalità di completamento come "Verify".</span><span class="sxs-lookup"><span data-stu-id="29ab6-239">Specifying the completion mode as "Verify" will cause it to verify whether the restart action actually succeeded.</span></span>  
* <span data-ttu-id="29ab6-240">**OperationTimeout** : imposta la quantità di tempo disponibile per completare l'operazione prima che venga generata un'eccezione TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="29ab6-240">**OperationTimeout** sets the amount of time for the operation to finish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="29ab6-241">**CancellationToken** : consente di annullare una chiamata in sospeso.</span><span class="sxs-lookup"><span data-stu-id="29ab6-241">**CancellationToken** enables a pending call to be canceled.</span></span>

<span data-ttu-id="29ab6-242">Anziché specificare direttamente il nodo mediante il nome, è possibile specificarlo tramite una chiave di partizione e il tipo di replica:</span><span class="sxs-lookup"><span data-stu-id="29ab6-242">Instead of directly specifying the node by its name, you can specify it via a partition key and the kind of replica.</span></span>

<span data-ttu-id="29ab6-243">Per altre informazioni vedere [PartitionSelector e ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="29ab6-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference to System.Fabric.Testability.dll and System.Fabric.dll
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
            //Restart the node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way to restart node is by using nodeName and nodeInstanceId
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

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="29ab6-244">PartitionSelector e ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="29ab6-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="29ab6-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="29ab6-245">PartitionSelector</span></span>
<span data-ttu-id="29ab6-246">PartitionSelector è un helper esposto in fase di testabilità che consente di selezionare una partizione specifica in cui eseguire le azioni di testabilità.</span><span class="sxs-lookup"><span data-stu-id="29ab6-246">PartitionSelector is a helper exposed in testability and is used to select a specific partition on which to perform any of the testability actions.</span></span> <span data-ttu-id="29ab6-247">Può essere utilizzato per selezionare una partizione specifica se l'ID partizione è noto in anticipo.</span><span class="sxs-lookup"><span data-stu-id="29ab6-247">It can be used to select a specific partition if the partition ID is known beforehand.</span></span> <span data-ttu-id="29ab6-248">In alternativa, è possibile fornire la chiave di partizione; l'operazione risolverà internamente l'ID partizione.</span><span class="sxs-lookup"><span data-stu-id="29ab6-248">Or, you can provide the partition key and the operation will resolve the partition ID internally.</span></span> <span data-ttu-id="29ab6-249">È inoltre possibile selezionare una partizione casuale.</span><span class="sxs-lookup"><span data-stu-id="29ab6-249">You also have the option of selecting a random partition.</span></span>

<span data-ttu-id="29ab6-250">Per usare questo helper, creare l'oggetto PartitionSelector e selezionare la partizione ricorrendo a uno dei metodi Select*.</span><span class="sxs-lookup"><span data-stu-id="29ab6-250">To use this helper, create the PartitionSelector object and select the partition by using one of the Select* methods.</span></span> <span data-ttu-id="29ab6-251">Passare quindi l'oggetto PartitionSelector all'API che lo richiede.</span><span class="sxs-lookup"><span data-stu-id="29ab6-251">Then pass in the PartitionSelector object to the API that requires it.</span></span> <span data-ttu-id="29ab6-252">Se non è selezionata alcuna opzione, per impostazione predefinita viene selezionata una partizione casuale.</span><span class="sxs-lookup"><span data-stu-id="29ab6-252">If no option is selected, it defaults to a random partition.</span></span>

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

### <a name="replicaselector"></a><span data-ttu-id="29ab6-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="29ab6-253">ReplicaSelector</span></span>
<span data-ttu-id="29ab6-254">ReplicaSelector è un helper esposto in fase di testabilità che consente di selezionare una replica in cui eseguire le azioni di testabilità.</span><span class="sxs-lookup"><span data-stu-id="29ab6-254">ReplicaSelector is a helper exposed in testability and is used to help select a replica on which to perform any of the testability actions.</span></span> <span data-ttu-id="29ab6-255">Può essere usato per selezionare una replica specifica se l'ID di replica è noto in anticipo.</span><span class="sxs-lookup"><span data-stu-id="29ab6-255">It can be used to select a specific replica if the replica ID is known beforehand.</span></span> <span data-ttu-id="29ab6-256">È possibile selezionare anche una replica primaria o una replica secondaria casuale.</span><span class="sxs-lookup"><span data-stu-id="29ab6-256">In addition, you have the option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="29ab6-257">ReplicaSelector deriva da PartitionSelector ed è quindi necessario selezionare sia la replica sia la partizione in cui si vuole eseguire l'operazione di testabilità.</span><span class="sxs-lookup"><span data-stu-id="29ab6-257">ReplicaSelector derives from PartitionSelector, so you need to select both the replica and the partition on which you wish to perform the testability operation.</span></span>

<span data-ttu-id="29ab6-258">Per usare l'helper, creare un oggetto ReplicaSelector e impostare il modo in cui si vuole selezionare la replica e la partizione.</span><span class="sxs-lookup"><span data-stu-id="29ab6-258">To use this helper, create a ReplicaSelector object and set the way you want to select the replica and the partition.</span></span> <span data-ttu-id="29ab6-259">Quindi è possibile passarlo nell'API che lo richiede.</span><span class="sxs-lookup"><span data-stu-id="29ab6-259">You can then pass it into the API that requires it.</span></span> <span data-ttu-id="29ab6-260">Se non è selezionata alcuna opzione, per impostazione predefinita vengono selezionate una replica casuale e una partizione casuale.</span><span class="sxs-lookup"><span data-stu-id="29ab6-260">If no option is selected, it defaults to a random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select the primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select the replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="29ab6-261">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29ab6-261">Next steps</span></span>
* [<span data-ttu-id="29ab6-262">Scenari di testabilità</span><span class="sxs-lookup"><span data-stu-id="29ab6-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="29ab6-263">Come eseguire il test del servizio</span><span class="sxs-lookup"><span data-stu-id="29ab6-263">How to test your service</span></span>
  * [<span data-ttu-id="29ab6-264">Simulare gli errori durante i carichi di lavoro del servizio</span><span class="sxs-lookup"><span data-stu-id="29ab6-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="29ab6-265">Errori di comunicazione da servizio a servizio</span><span class="sxs-lookup"><span data-stu-id="29ab6-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

