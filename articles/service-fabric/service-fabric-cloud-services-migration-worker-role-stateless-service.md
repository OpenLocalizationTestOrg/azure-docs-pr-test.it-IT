---
title: Convertire app di Servizi cloud di Azure in microservizi | Microsoft Docs
description: Questa guida confronta i ruoli di lavoro e Web di Servizi Cloud con i servizi senza stato di Service Fabric per facilitare la migrazione da Servizi cloud a Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="fddce-103">Guida alla conversione di ruoli di lavoro e Web in servizi senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="fddce-104">Questo articolo descrive come eseguire la migrazione di ruoli di lavoro e Web di Servizi cloud a servizi senza stato di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fddce-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="fddce-105">Questo è il percorso di migrazione più semplice da Servizi cloud a Service Fabric per le applicazioni la cui architettura complessiva rimarrà approssimativamente la stessa.</span><span class="sxs-lookup"><span data-stu-id="fddce-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="fddce-106">Da progetto di Servizi cloud a progetto di applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="fddce-107">Un progetto di Servizi cloud e un progetto di applicazione di Service Fabric hanno una struttura simile ed entrambi rappresentano l'unità di distribuzione per l'applicazione, ovvero ognuno definisce il pacchetto completo che viene distribuito per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="fddce-108">Un progetto di Servizi cloud contiene uno o più ruoli di lavoro o Web.</span><span class="sxs-lookup"><span data-stu-id="fddce-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="fddce-109">In modo analogo un progetto di applicazione di Service Fabric contiene uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="fddce-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="fddce-110">La differenza è che il progetto di Servizi cloud abbina la distribuzione dell'applicazione con la distribuzione di una macchina virtuale e quindi contiene le impostazioni di configurazione della macchina virtuale, mentre il progetto di applicazione di Service Fabric definisce solo un'applicazione che verrà distribuita a un set di macchine virtuali esistenti in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fddce-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="fddce-111">Il cluster di Service Fabric viene distribuito solo una volta, tramite un modello di Azure Resource Manager o tramite il portale di Azure, e possono esservi distribuite più applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fddce-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Confronto tra i progetti di Servizi cloud e Service Fabric][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="fddce-113">Da ruolo di lavoro a servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="fddce-113">Worker Role to stateless service</span></span>
<span data-ttu-id="fddce-114">Concettualmente un ruolo di lavoro rappresenta un carico di lavoro senza stato, ovvero ogni istanza del carico di lavoro è identica e le richieste possono essere indirizzate a qualsiasi istanza in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="fddce-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="fddce-115">Non è previsto che ogni istanza ricordi la richiesta precedente.</span><span class="sxs-lookup"><span data-stu-id="fddce-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="fddce-116">Lo stato in cui opera il carico di lavoro viene gestito da un archivio stati esterno, ad esempio un archivio tabelle di Azure o Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fddce-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="fddce-117">In Service Fabric questo tipo di carico di lavoro è rappresentato da un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="fddce-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="fddce-118">L'approccio più semplice per la migrazione di un ruolo di lavoro a Service Fabric può avvenire mediante la conversione di codice del ruolo di lavoro in un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="fddce-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![Da ruolo di lavoro a servizio senza stato][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="fddce-120">Da ruolo Web a servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="fddce-120">Web Role to stateless service</span></span>
<span data-ttu-id="fddce-121">Analogamente a un ruolo di lavoro, anche un ruolo Web rappresenta un carico di lavoro senza stato e quindi concettualmente può essere associato anch'esso a un servizio senza stato di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fddce-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="fddce-122">Tuttavia, a differenza dei ruoli Web, Service Fabric non supporta IIS.</span><span class="sxs-lookup"><span data-stu-id="fddce-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="fddce-123">Per eseguire la migrazione di un'applicazione Web da un ruolo Web a un servizio senza stato è necessario passare prima a un framework Web che possa essere self-hosted e non dipenda da IIS o System.Web, ad esempio ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="fddce-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="fddce-124">**Applicazione**</span><span class="sxs-lookup"><span data-stu-id="fddce-124">**Application**</span></span> | <span data-ttu-id="fddce-125">**Supportato**</span><span class="sxs-lookup"><span data-stu-id="fddce-125">**Supported**</span></span> | <span data-ttu-id="fddce-126">**Percorso di migrazione**</span><span class="sxs-lookup"><span data-stu-id="fddce-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fddce-127">Web Form ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fddce-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="fddce-128">No</span><span class="sxs-lookup"><span data-stu-id="fddce-128">No</span></span> |<span data-ttu-id="fddce-129">Convertire in ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="fddce-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="fddce-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="fddce-130">ASP.NET MVC</span></span> |<span data-ttu-id="fddce-131">Con migrazione</span><span class="sxs-lookup"><span data-stu-id="fddce-131">With Migration</span></span> |<span data-ttu-id="fddce-132">Eseguire l'aggiornamento ad ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="fddce-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="fddce-133">API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fddce-133">ASP.NET Web API</span></span> |<span data-ttu-id="fddce-134">Con migrazione</span><span class="sxs-lookup"><span data-stu-id="fddce-134">With Migration</span></span> |<span data-ttu-id="fddce-135">Usare un server self-hosted o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="fddce-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="fddce-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="fddce-136">ASP.NET Core 1</span></span> |<span data-ttu-id="fddce-137">Sì</span><span class="sxs-lookup"><span data-stu-id="fddce-137">Yes</span></span> |<span data-ttu-id="fddce-138">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="fddce-139">API del punto di ingresso e ciclo di vita</span><span class="sxs-lookup"><span data-stu-id="fddce-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="fddce-140">Le API del servizio di Service Fabric e del ruolo di lavoro offrono punti di ingresso simili:</span><span class="sxs-lookup"><span data-stu-id="fddce-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="fddce-141">**Punto di ingresso**</span><span class="sxs-lookup"><span data-stu-id="fddce-141">**Entry Point**</span></span> | <span data-ttu-id="fddce-142">**Istanze del ruolo di lavoro**</span><span class="sxs-lookup"><span data-stu-id="fddce-142">**Worker Role**</span></span> | <span data-ttu-id="fddce-143">**Servizio di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="fddce-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fddce-144">Elaborazione in corso</span><span class="sxs-lookup"><span data-stu-id="fddce-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="fddce-145">Avvio della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fddce-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="fddce-146">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-146">N/A</span></span> |
| <span data-ttu-id="fddce-147">Arresto della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fddce-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="fddce-148">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-148">N/A</span></span> |
| <span data-ttu-id="fddce-149">Apertura del listener per le richieste client</span><span class="sxs-lookup"><span data-stu-id="fddce-149">Open listener for client requests</span></span> |<span data-ttu-id="fddce-150">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-150">N/A</span></span> |<ul><li> <span data-ttu-id="fddce-151">`CreateServiceInstanceListener()` per servizi senza stato</span><span class="sxs-lookup"><span data-stu-id="fddce-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="fddce-152">`CreateServiceReplicaListener()` per servizi con stato</span><span class="sxs-lookup"><span data-stu-id="fddce-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="fddce-153">Istanze del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="fddce-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="fddce-154">Servizio senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="fddce-155">Entrambi hanno un override "Run" primario in cui iniziare l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="fddce-156">I servizi di Service Fabric combinano `Run`, `Start` e `Stop` in un singolo punto di ingresso, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="fddce-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="fddce-157">Il servizio inizierà a funzionare all'avvio di `RunAsync` e verrà arrestato quando viene segnalato CancellationToken del metodo `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="fddce-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="fddce-158">Esistono alcune differenze principali tra il ciclo di vita e la durata dei servizi di Service Fabric e dei ruoli di lavoro:</span><span class="sxs-lookup"><span data-stu-id="fddce-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="fddce-159">**Ciclo di vita:** la differenza principale è che un ruolo di lavoro è una VM e quindi il ciclo di vita è associato alla VM e include gli eventi relativi all'avvio e all'arresto della VM.</span><span class="sxs-lookup"><span data-stu-id="fddce-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="fddce-160">Un servizio di Service Fabric ha un ciclo di vita separato dal ciclo di vita della macchina virtuale, quindi non include gli eventi relativi all'avvio e all'arresto della macchina virtuale host o del computer, perché non sono correlati.</span><span class="sxs-lookup"><span data-stu-id="fddce-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="fddce-161">**Durata:** un'istanza del ruolo di lavoro verrà riciclata se il metodo `Run` viene chiuso.</span><span class="sxs-lookup"><span data-stu-id="fddce-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="fddce-162">Il metodo `RunAsync` in un servizio di Service Fabric può tuttavia essere eseguito fino al completamento e l'istanza del servizio rimarrà operativa.</span><span class="sxs-lookup"><span data-stu-id="fddce-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="fddce-163">Service Fabric fornisce un punto di ingresso facoltativo di configurazione della comunicazione per i servizi in ascolto delle richieste client.</span><span class="sxs-lookup"><span data-stu-id="fddce-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="fddce-164">Sia il punto di ingresso di comunicazione che quello di RunAsync sono sostituzioni facoltative nei servizi di Service Fabric, ovvero il servizio può scegliere di restare in ascolto solo delle richieste client o eseguire solo un ciclo di elaborazione oppure entrambi, motivo per cui il metodo RunAsync può terminare senza riavviare l'istanza del servizio, perché può continuare a rimanere in ascolto delle richieste client.</span><span class="sxs-lookup"><span data-stu-id="fddce-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="fddce-165">API dell'applicazione e ambiente</span><span class="sxs-lookup"><span data-stu-id="fddce-165">Application API and environment</span></span>
<span data-ttu-id="fddce-166">L'API dell'ambiente di Servizi cloud fornisce informazioni e funzionalità per l'istanza corrente della macchina virtuale, nonché informazioni su altre istanze del ruolo VM.</span><span class="sxs-lookup"><span data-stu-id="fddce-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="fddce-167">Service Fabric fornisce informazioni correlate al relativo runtime e alcune informazioni relative al nodo su cui un servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fddce-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="fddce-168">**Attività dell'ambiente**</span><span class="sxs-lookup"><span data-stu-id="fddce-168">**Environment Task**</span></span> | <span data-ttu-id="fddce-169">**Servizi cloud**</span><span class="sxs-lookup"><span data-stu-id="fddce-169">**Cloud Services**</span></span> | <span data-ttu-id="fddce-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="fddce-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fddce-171">Impostazioni di configurazione e notifica di modifiche</span><span class="sxs-lookup"><span data-stu-id="fddce-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="fddce-172">Archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="fddce-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="fddce-173">Informazioni sull'endpoint</span><span class="sxs-lookup"><span data-stu-id="fddce-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="fddce-174">Istanza corrente: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="fddce-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="fddce-175">Altri ruoli e istanze: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="fddce-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="fddce-176">`NodeContext` per l'indirizzo del nodo corrente</span><span class="sxs-lookup"><span data-stu-id="fddce-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="fddce-177">`FabricClient` e `ServicePartitionResolver` per l'individuazione di endpoint di servizio</span><span class="sxs-lookup"><span data-stu-id="fddce-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="fddce-178">Emulazione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="fddce-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="fddce-179">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-179">N/A</span></span> |
| <span data-ttu-id="fddce-180">Evento di modifica simultanea</span><span class="sxs-lookup"><span data-stu-id="fddce-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="fddce-181">N/D</span><span class="sxs-lookup"><span data-stu-id="fddce-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="fddce-182">Impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="fddce-182">Configuration settings</span></span>
<span data-ttu-id="fddce-183">Le impostazioni di configurazione in Servici cloud vengono impostate per un ruolo VM e si applicano a tutte le istanze di quel ruolo VM.</span><span class="sxs-lookup"><span data-stu-id="fddce-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="fddce-184">Queste impostazioni sono coppie chiave-valore impostate nei file ServiceConfiguration.*.cscfg e sono accessibili direttamente tramite RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="fddce-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="fddce-185">In Service Fabric le impostazioni si applicano singolarmente a ogni servizio e ogni applicazione, invece che a una VM, perché una VM può ospitare più servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="fddce-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="fddce-186">Un servizio è composto da tre pacchetti:</span><span class="sxs-lookup"><span data-stu-id="fddce-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="fddce-187">**Code:** contiene i file eseguibili del servizio, i file binari, le DLL e qualsiasi altro file necessario per l'esecuzione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="fddce-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="fddce-188">**Config:** tutti i file di configurazione e le impostazioni per un servizio.</span><span class="sxs-lookup"><span data-stu-id="fddce-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="fddce-189">**Data:** file di dati statici associati al servizio.</span><span class="sxs-lookup"><span data-stu-id="fddce-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="fddce-190">Per ognuno di questi pacchetti l'aggiornamento e il controllo delle versioni possono essere gestiti in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="fddce-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="fddce-191">Analogamente a Servizi cloud, è possibile accedere a un pacchetto di configurazione a livello di codice tramite un'API e sono disponibili eventi per notificare al servizio una modifica del pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="fddce-192">È possibile usare un file Settings.xml per la configurazione di chiave-valore e l'accesso a livello di codice simile alla sezione app settings di un file App.config.</span><span class="sxs-lookup"><span data-stu-id="fddce-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="fddce-193">Tuttavia, a differenza di Servizi cloud, un pacchetto di configurazione di Service Fabric può contenere qualsiasi file di configurazione in qualsiasi formato, ovvero XML, JSON, YAML o un formato binario personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fddce-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="fddce-194">Accesso alla configurazione</span><span class="sxs-lookup"><span data-stu-id="fddce-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="fddce-195">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fddce-195">Cloud Services</span></span>
<span data-ttu-id="fddce-196">Le impostazioni di configurazione di ServiceConfiguration.*.cscfg sono accessibili tramite `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="fddce-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="fddce-197">Queste impostazioni sono disponibili globalmente per tutte le istanze del ruolo nella stessa distribuzione di Servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="fddce-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="fddce-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-198">Service Fabric</span></span>
<span data-ttu-id="fddce-199">Ogni servizio ha un pacchetto di configurazione individuale.</span><span class="sxs-lookup"><span data-stu-id="fddce-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="fddce-200">Non esiste un meccanismo predefinito per le impostazioni di configurazione globali accessibile da tutte le applicazioni in un cluster.</span><span class="sxs-lookup"><span data-stu-id="fddce-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="fddce-201">Quando si usa il file di configurazione speciale Settings.xml di Service Fabric all'interno di un pacchetto di configurazione, i valori in Settings.XML possono essere sovrascritti a livello di applicazione, rendendo possibili le impostazioni di configurazione a livello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="fddce-202">Alle impostazioni di configurazione è possibile accedere all'interno di ogni istanza del servizio tramite `CodePackageActivationContext`del servizio.</span><span class="sxs-lookup"><span data-stu-id="fddce-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="fddce-203">Eventi di aggiornamento della configurazione</span><span class="sxs-lookup"><span data-stu-id="fddce-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="fddce-204">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fddce-204">Cloud Services</span></span>
<span data-ttu-id="fddce-205">L'evento `RoleEnvironment.Changed` viene usato per notificare a tutte le istanze del ruolo quando si verifica una modifica nell'ambiente, ad esempio una modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="fddce-206">Viene usato per gli aggiornamenti della configurazione senza riciclare le istanze del ruolo o riavviare un processo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fddce-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="fddce-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-207">Service Fabric</span></span>
<span data-ttu-id="fddce-208">Ognuno dei tre tipi di pacchetto in un servizio, ovvero Code, Config e Data, include eventi che inviano una notifica a un'istanza del servizio quando un pacchetto viene aggiornato, aggiunto o rimosso.</span><span class="sxs-lookup"><span data-stu-id="fddce-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="fddce-209">Un servizio può contenere più pacchetti di ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="fddce-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="fddce-210">Ad esempio, un servizio può avere più pacchetti Config, ognuno aggiornabile e con controllo delle versioni gestito in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="fddce-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="fddce-211">Questi eventi sono disponibili per l'utilizzo in caso di modifiche nei pacchetti del servizio senza riavviare l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="fddce-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="fddce-212">Attività di avvio</span><span class="sxs-lookup"><span data-stu-id="fddce-212">Startup tasks</span></span>
<span data-ttu-id="fddce-213">Le attività di avvio sono azioni eseguite prima dell'avvio di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fddce-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="fddce-214">Un'attività di avvio viene in genere usata per eseguire script di installazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fddce-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="fddce-215">Sia Servizi Cloud che Service Fabric supportano attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="fddce-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="fddce-216">La differenza principale riguarda il fatto che in Servizi cloud un'attività di avvio è collegata a una VM, perché fa parte di un'istanza del ruolo, mentre in Service Fabric un'attività di avvio è collegata a un servizio che non è associato a una VM specifica.</span><span class="sxs-lookup"><span data-stu-id="fddce-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="fddce-217">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fddce-217">Cloud Services</span></span> | <span data-ttu-id="fddce-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fddce-219">Percorso di configurazione</span><span class="sxs-lookup"><span data-stu-id="fddce-219">Configuration location</span></span> |<span data-ttu-id="fddce-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="fddce-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="fddce-221">Privilegi</span><span class="sxs-lookup"><span data-stu-id="fddce-221">Privileges</span></span> |<span data-ttu-id="fddce-222">"limitato" o "con privilegi elevati"</span><span class="sxs-lookup"><span data-stu-id="fddce-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="fddce-223">Sequenziazione</span><span class="sxs-lookup"><span data-stu-id="fddce-223">Sequencing</span></span> |<span data-ttu-id="fddce-224">"semplice", "background", "in primo piano"</span><span class="sxs-lookup"><span data-stu-id="fddce-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="fddce-225">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fddce-225">Cloud Services</span></span>
<span data-ttu-id="fddce-226">In Servizi cloud è configurato un punto di ingresso di avvio per ogni ruolo in ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="fddce-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="fddce-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-227">Service Fabric</span></span>
<span data-ttu-id="fddce-228">In Service Fabric è configurato un punto di ingresso di avvio per ogni servizio in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="fddce-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="fddce-229">Note sull'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="fddce-229">A note about development environment</span></span>
<span data-ttu-id="fddce-230">Sia Servizi Cloud che Service Fabric sono integrati in Visual Studio con modelli di progetto e il supporto per il debug, la configurazione e la distribuzione sia locale che in Azure.</span><span class="sxs-lookup"><span data-stu-id="fddce-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="fddce-231">Servizi cloud e Service Fabric forniscono anche un ambiente di runtime di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="fddce-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="fddce-232">La differenza è che mentre il runtime di sviluppo di Servizi cloud emula l'ambiente Azure in cui viene eseguito, Service Fabric non usa un emulatore, ma il runtime di Service Fabric completo.</span><span class="sxs-lookup"><span data-stu-id="fddce-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="fddce-233">L'ambiente di Service Fabric che viene eseguito nel computer di sviluppo locale è lo stesso ambiente eseguito nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="fddce-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fddce-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fddce-234">Next steps</span></span>
<span data-ttu-id="fddce-235">Altre informazioni su Reliable Services di Service Fabric e le differenze fondamentali tra Servizi cloud e l'architettura dell'applicazione di Service Fabric per comprendere come sfruttare il set completo di funzionalità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fddce-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="fddce-236">Introduzione a Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="fddce-237">Guida concettuale alle differenze tra Servizi cloud e Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fddce-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
