---
title: Servizi Cloud di Azure App toomicroservices aaaConvert | Documenti Microsoft
description: Questa Guida Confronta Web dei servizi Cloud e la migrazione dei ruoli di lavoro e Service Fabric servizi senza stato toohelp da tooService servizi Cloud dell'infrastruttura.
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
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="820d6-103">Guida tooconverting servizi Web e ruoli di lavoro tooService infrastruttura senza stati</span><span class="sxs-lookup"><span data-stu-id="820d6-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="820d6-104">Questo articolo viene descritto come toomigrate i ruoli di lavoro e Web dei servizi Cloud tooService infrastruttura senza stati servizi.</span><span class="sxs-lookup"><span data-stu-id="820d6-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="820d6-105">Si tratta di percorso di migrazione più semplice di hello da servizi Cloud tooService dell'infrastruttura per applicazioni la cui architettura complessiva verrà toostay approssimativamente hello stesso.</span><span class="sxs-lookup"><span data-stu-id="820d6-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="820d6-106">Progetto di applicazione di servizio progetto tooService dell'infrastruttura cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="820d6-107">Un progetto servizio Cloud e un progetto di applicazione di Service Fabric presentano una struttura simile e unità di distribuzione hello entrambi rappresentano per l'applicazione, vale a dire, ognuno di essi definiscono hello completo pacchetto toorun distribuito l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="820d6-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="820d6-108">Un progetto di Servizi cloud contiene uno o più ruoli di lavoro o Web.</span><span class="sxs-lookup"><span data-stu-id="820d6-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="820d6-109">In modo analogo un progetto di applicazione di Service Fabric contiene uno o più servizi.</span><span class="sxs-lookup"><span data-stu-id="820d6-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="820d6-110">differenza Hello è che legato progetto servizio Cloud di hello hello distribuzione dell'applicazione con una distribuzione della macchina virtuale e pertanto contiene le impostazioni di configurazione macchina virtuale, mentre il progetto di applicazione di Service Fabric hello definisce solo un'applicazione che verrà distribuita tooa set di macchine virtuali esistenti in un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="820d6-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="820d6-111">cluster di Service Fabric Hello stesso viene distribuito solo una volta, tramite un modello di gestione risorse o hello portale di Azure, più infrastruttura dei servizi e le applicazioni possono essere distribuiti tooit.</span><span class="sxs-lookup"><span data-stu-id="820d6-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Confronto tra i progetti di Servizi cloud e Service Fabric][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="820d6-113">Servizio toostateless ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="820d6-113">Worker Role toostateless service</span></span>
<span data-ttu-id="820d6-114">Concettualmente, un ruolo di lavoro rappresenta un carico di lavoro senza stato, pertanto ogni istanza di carico di lavoro hello è identica e le richieste possono essere indirizzati tooany istanza in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="820d6-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="820d6-115">Ogni istanza non è richiesta precedente di hello tooremember previsto.</span><span class="sxs-lookup"><span data-stu-id="820d6-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="820d6-116">Stato di tale carico di lavoro hello opera su è gestito da un archivio di stato esterno, ad esempio l'archiviazione tabelle di Azure o Azure Documentdb.</span><span class="sxs-lookup"><span data-stu-id="820d6-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="820d6-117">In Service Fabric questo tipo di carico di lavoro è rappresentato da un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="820d6-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="820d6-118">toomigrating approccio più semplice di Hello tooService un ruolo di lavoro infrastruttura può essere eseguita ruolo di lavoro codice tooa servizio senza stato di conversione.</span><span class="sxs-lookup"><span data-stu-id="820d6-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Ruolo di lavoro tooStateless servizio][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="820d6-120">Ruolo toostateless servizio Web</span><span class="sxs-lookup"><span data-stu-id="820d6-120">Web Role toostateless service</span></span>
<span data-ttu-id="820d6-121">TooWorker simile ruolo, un ruolo Web rappresenta anche un carico di lavoro senza stato e pertanto concettualmente troppo può essere mappato tooa servizio senza stato Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="820d6-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="820d6-122">Tuttavia, a differenza dei ruoli Web, Service Fabric non supporta IIS.</span><span class="sxs-lookup"><span data-stu-id="820d6-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="820d6-123">toomigrate un'applicazione web da un servizio senza stato tooa di ruolo Web è necessario prima framework web tooa mobile che possono essere indipendenti e non dipendono da IIS o System. Web, ad esempio ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="820d6-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="820d6-124">**Applicazione**</span><span class="sxs-lookup"><span data-stu-id="820d6-124">**Application**</span></span> | <span data-ttu-id="820d6-125">**Supportato**</span><span class="sxs-lookup"><span data-stu-id="820d6-125">**Supported**</span></span> | <span data-ttu-id="820d6-126">**Percorso di migrazione**</span><span class="sxs-lookup"><span data-stu-id="820d6-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="820d6-127">Web Form ASP.NET</span><span class="sxs-lookup"><span data-stu-id="820d6-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="820d6-128">No</span><span class="sxs-lookup"><span data-stu-id="820d6-128">No</span></span> |<span data-ttu-id="820d6-129">Convertire tooASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="820d6-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="820d6-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="820d6-130">ASP.NET MVC</span></span> |<span data-ttu-id="820d6-131">Con migrazione</span><span class="sxs-lookup"><span data-stu-id="820d6-131">With Migration</span></span> |<span data-ttu-id="820d6-132">Aggiornamento tooASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="820d6-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="820d6-133">API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="820d6-133">ASP.NET Web API</span></span> |<span data-ttu-id="820d6-134">Con migrazione</span><span class="sxs-lookup"><span data-stu-id="820d6-134">With Migration</span></span> |<span data-ttu-id="820d6-135">Usare un server self-hosted o ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="820d6-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="820d6-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="820d6-136">ASP.NET Core 1</span></span> |<span data-ttu-id="820d6-137">Sì</span><span class="sxs-lookup"><span data-stu-id="820d6-137">Yes</span></span> |<span data-ttu-id="820d6-138">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="820d6-139">API del punto di ingresso e ciclo di vita</span><span class="sxs-lookup"><span data-stu-id="820d6-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="820d6-140">Le API del servizio di Service Fabric e del ruolo di lavoro offrono punti di ingresso simili:</span><span class="sxs-lookup"><span data-stu-id="820d6-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="820d6-141">**Punto di ingresso**</span><span class="sxs-lookup"><span data-stu-id="820d6-141">**Entry Point**</span></span> | <span data-ttu-id="820d6-142">**Istanze del ruolo di lavoro**</span><span class="sxs-lookup"><span data-stu-id="820d6-142">**Worker Role**</span></span> | <span data-ttu-id="820d6-143">**Servizio di Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="820d6-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="820d6-144">Elaborazione in corso</span><span class="sxs-lookup"><span data-stu-id="820d6-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="820d6-145">Avvio della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="820d6-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="820d6-146">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-146">N/A</span></span> |
| <span data-ttu-id="820d6-147">Arresto della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="820d6-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="820d6-148">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-148">N/A</span></span> |
| <span data-ttu-id="820d6-149">Apertura del listener per le richieste client</span><span class="sxs-lookup"><span data-stu-id="820d6-149">Open listener for client requests</span></span> |<span data-ttu-id="820d6-150">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-150">N/A</span></span> |<ul><li> <span data-ttu-id="820d6-151">`CreateServiceInstanceListener()` per servizi senza stato</span><span class="sxs-lookup"><span data-stu-id="820d6-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="820d6-152">`CreateServiceReplicaListener()` per servizi con stato</span><span class="sxs-lookup"><span data-stu-id="820d6-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="820d6-153">Istanze del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="820d6-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="820d6-154">Servizio senza stato di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="820d6-155">Entrambe dispongono di un override primario "Esegui" in cui toobegin l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="820d6-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="820d6-156">I servizi di Service Fabric combinano `Run`, `Start` e `Stop` in un singolo punto di ingresso, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="820d6-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="820d6-157">Il servizio deve iniziare a lavorare quando `RunAsync` viene avviato e deve smettere di funzionare quando hello `RunAsync` segnalata CancellationToken del metodo.</span><span class="sxs-lookup"><span data-stu-id="820d6-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="820d6-158">Esistono alcune differenze principali tra hello del ciclo di vita e la durata dei servizi di infrastruttura dei servizi e i ruoli di lavoro:</span><span class="sxs-lookup"><span data-stu-id="820d6-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="820d6-159">**Ciclo di vita:** hello differenza principale è che un ruolo di lavoro è una macchina virtuale e pertanto il ciclo di vita è abbinato toohello macchina virtuale, che include eventi per quando hello VM avvia e arresta.</span><span class="sxs-lookup"><span data-stu-id="820d6-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="820d6-160">Un servizio di Service Fabric dispone di un ciclo di vita è separato dal ciclo di vita di hello macchina virtuale, in modo non include gli eventi per quando hello host macchina virtuale o l'avvio della macchina e stop, poiché non sono correlate.</span><span class="sxs-lookup"><span data-stu-id="820d6-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="820d6-161">**Durata:** un'istanza del ruolo di lavoro verrà riciclati se hello `Run` metodo esce.</span><span class="sxs-lookup"><span data-stu-id="820d6-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="820d6-162">Hello `RunAsync` metodo in un servizio di Service Fabric può tuttavia eseguire toocompletion e viene mantenuta l'istanza del servizio hello backup.</span><span class="sxs-lookup"><span data-stu-id="820d6-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="820d6-163">Service Fabric fornisce un punto di ingresso facoltativo di configurazione della comunicazione per i servizi in ascolto delle richieste client.</span><span class="sxs-lookup"><span data-stu-id="820d6-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="820d6-164">Hello RunAsync sia il punto di ingresso di comunicazione sono sostituzioni facoltative in servizi di Service Fabric - il servizio può scegliere tooonly tooclient le richieste o solo di eseguire un ciclo di elaborazione o entrambi - motivo per cui può tooexit senza hello RunAsync (metodo) riavviare l'istanza di servizio di hello, perché può continuare toolisten per le richieste client.</span><span class="sxs-lookup"><span data-stu-id="820d6-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="820d6-165">API dell'applicazione e ambiente</span><span class="sxs-lookup"><span data-stu-id="820d6-165">Application API and environment</span></span>
<span data-ttu-id="820d6-166">ambiente di servizi Cloud Hello API fornisce informazioni e funzionalità per l'istanza corrente della macchina virtuale hello, nonché informazioni sulle altre istanze del ruolo VM.</span><span class="sxs-lookup"><span data-stu-id="820d6-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="820d6-167">Service Fabric fornisce informazioni correlate tooits runtime e alcune informazioni sul nodo hello un servizio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="820d6-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="820d6-168">**Attività dell'ambiente**</span><span class="sxs-lookup"><span data-stu-id="820d6-168">**Environment Task**</span></span> | <span data-ttu-id="820d6-169">**Servizi cloud**</span><span class="sxs-lookup"><span data-stu-id="820d6-169">**Cloud Services**</span></span> | <span data-ttu-id="820d6-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="820d6-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="820d6-171">Impostazioni di configurazione e notifica di modifiche</span><span class="sxs-lookup"><span data-stu-id="820d6-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="820d6-172">Archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="820d6-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="820d6-173">Informazioni sull'endpoint</span><span class="sxs-lookup"><span data-stu-id="820d6-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="820d6-174">Istanza corrente: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="820d6-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="820d6-175">Altri ruoli e istanze: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="820d6-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="820d6-176">`NodeContext` per l'indirizzo del nodo corrente</span><span class="sxs-lookup"><span data-stu-id="820d6-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="820d6-177">`FabricClient` e `ServicePartitionResolver` per l'individuazione di endpoint di servizio</span><span class="sxs-lookup"><span data-stu-id="820d6-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="820d6-178">Emulazione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="820d6-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="820d6-179">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-179">N/A</span></span> |
| <span data-ttu-id="820d6-180">Evento di modifica simultanea</span><span class="sxs-lookup"><span data-stu-id="820d6-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="820d6-181">N/D</span><span class="sxs-lookup"><span data-stu-id="820d6-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="820d6-182">Impostazioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="820d6-182">Configuration settings</span></span>
<span data-ttu-id="820d6-183">Le impostazioni di configurazione di servizi Cloud vengono impostate per un ruolo VM e applicano tooall istanze del ruolo VM.</span><span class="sxs-lookup"><span data-stu-id="820d6-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="820d6-184">Queste impostazioni sono coppie chiave-valore impostate nei file ServiceConfiguration.*.cscfg e sono accessibili direttamente tramite RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="820d6-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="820d6-185">Nell'infrastruttura del servizio, impostazioni si applicano singolarmente tooeach servizio e applicazione tooeach anziché tooa VM, perché una macchina virtuale può ospitare più servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="820d6-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="820d6-186">Un servizio è composto da tre pacchetti:</span><span class="sxs-lookup"><span data-stu-id="820d6-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="820d6-187">**Codice:** contiene file eseguibili del servizio hello, i file binari, dll e qualsiasi altro file di un servizio deve toorun.</span><span class="sxs-lookup"><span data-stu-id="820d6-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="820d6-188">**Config:** tutti i file di configurazione e le impostazioni per un servizio.</span><span class="sxs-lookup"><span data-stu-id="820d6-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="820d6-189">**Dati:** i file di dati statici associati al servizio hello.</span><span class="sxs-lookup"><span data-stu-id="820d6-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="820d6-190">Per ognuno di questi pacchetti l'aggiornamento e il controllo delle versioni possono essere gestiti in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="820d6-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="820d6-191">Servizi tooCloud simili, un pacchetto di configurazione è possibile accedere a livello di codice tramite un'API e gli eventi sono disponibili toonotify hello del servizio di una modifica della configurazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="820d6-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="820d6-192">Un file Settings. XML può essere utilizzato per la configurazione di chiave-valore e l'accesso programmatico simile toohello app sezione Impostazioni di un file app. config.</span><span class="sxs-lookup"><span data-stu-id="820d6-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="820d6-193">Tuttavia, a differenza di Servizi cloud, un pacchetto di configurazione di Service Fabric può contenere qualsiasi file di configurazione in qualsiasi formato, ovvero XML, JSON, YAML o un formato binario personalizzato.</span><span class="sxs-lookup"><span data-stu-id="820d6-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="820d6-194">Accesso alla configurazione</span><span class="sxs-lookup"><span data-stu-id="820d6-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="820d6-195">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-195">Cloud Services</span></span>
<span data-ttu-id="820d6-196">Le impostazioni di configurazione di ServiceConfiguration.*.cscfg sono accessibili tramite `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="820d6-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="820d6-197">Queste impostazioni sono disponibili globalmente tooall le istanze del ruolo in hello stessa distribuzione del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="820d6-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="820d6-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-198">Service Fabric</span></span>
<span data-ttu-id="820d6-199">Ogni servizio ha un pacchetto di configurazione individuale.</span><span class="sxs-lookup"><span data-stu-id="820d6-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="820d6-200">Non esiste un meccanismo predefinito per le impostazioni di configurazione globali accessibile da tutte le applicazioni in un cluster.</span><span class="sxs-lookup"><span data-stu-id="820d6-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="820d6-201">Quando si usa speciali Settings file di configurazione del Service Fabric all'interno di un pacchetto di configurazione, i valori nel file Settings.xml possono essere sovrascritte a livello di applicazione hello, rendendo possibili impostazioni di configurazione a livello di applicazione.</span><span class="sxs-lookup"><span data-stu-id="820d6-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="820d6-202">Impostazioni di configurazione sono gli accessi all'interno di ogni istanza del servizio tramite servizio di hello `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="820d6-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="820d6-203">Eventi di aggiornamento della configurazione</span><span class="sxs-lookup"><span data-stu-id="820d6-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="820d6-204">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-204">Cloud Services</span></span>
<span data-ttu-id="820d6-205">Hello `RoleEnvironment.Changed` evento è utilizzata toonotify si verifica tutte le istanze del ruolo quando una modifica nell'ambiente di hello, ad esempio una modifica della configurazione.</span><span class="sxs-lookup"><span data-stu-id="820d6-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="820d6-206">Si tratta di aggiornamenti della configurazione tooconsume utilizzato senza il riciclo delle istanze del ruolo o riavviare un processo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="820d6-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="820d6-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-207">Service Fabric</span></span>
<span data-ttu-id="820d6-208">Ciascuno di hello tre tipi di pacchetto in un servizio di codice, configurazione e dati - dispongono di eventi che notificano un'istanza del servizio viene aggiornato, aggiunto o rimosso un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="820d6-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="820d6-209">Un servizio può contenere più pacchetti di ogni tipo.</span><span class="sxs-lookup"><span data-stu-id="820d6-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="820d6-210">Ad esempio, un servizio può avere più pacchetti Config, ognuno aggiornabile e con controllo delle versioni gestito in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="820d6-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="820d6-211">Questi eventi sono modifiche tooconsume disponibili nei pacchetti del servizio senza dover riavviare l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="820d6-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="820d6-212">Attività di avvio</span><span class="sxs-lookup"><span data-stu-id="820d6-212">Startup tasks</span></span>
<span data-ttu-id="820d6-213">Le attività di avvio sono azioni eseguite prima dell'avvio di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="820d6-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="820d6-214">Un'attività di avvio è generalmente usati toorun gli script di installazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="820d6-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="820d6-215">Sia Servizi Cloud che Service Fabric supportano attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="820d6-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="820d6-216">Hello differenza principale è che in servizi Cloud, un'attività di avvio è abbinato tooa VM perché fa parte di un'istanza del ruolo, mentre nell'infrastruttura del servizio un'attività di avvio è servizio tooa collegati, che non è vincolata tooany determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="820d6-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="820d6-217">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-217">Cloud Services</span></span> | <span data-ttu-id="820d6-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="820d6-219">Percorso di configurazione</span><span class="sxs-lookup"><span data-stu-id="820d6-219">Configuration location</span></span> |<span data-ttu-id="820d6-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="820d6-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="820d6-221">Privilegi</span><span class="sxs-lookup"><span data-stu-id="820d6-221">Privileges</span></span> |<span data-ttu-id="820d6-222">"limitato" o "con privilegi elevati"</span><span class="sxs-lookup"><span data-stu-id="820d6-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="820d6-223">Sequenziazione</span><span class="sxs-lookup"><span data-stu-id="820d6-223">Sequencing</span></span> |<span data-ttu-id="820d6-224">"semplice", "background", "in primo piano"</span><span class="sxs-lookup"><span data-stu-id="820d6-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="820d6-225">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-225">Cloud Services</span></span>
<span data-ttu-id="820d6-226">In Servizi cloud è configurato un punto di ingresso di avvio per ogni ruolo in ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="820d6-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="820d6-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-227">Service Fabric</span></span>
<span data-ttu-id="820d6-228">In Service Fabric è configurato un punto di ingresso di avvio per ogni servizio in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="820d6-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="820d6-229">Note sull'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="820d6-229">A note about development environment</span></span>
<span data-ttu-id="820d6-230">Servizi Cloud e infrastruttura di servizio sono integrati con Visual Studio con modelli di progetto e il supporto per il debug, la configurazione e distribuzione sia in locale e tooAzure.</span><span class="sxs-lookup"><span data-stu-id="820d6-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="820d6-231">Servizi cloud e Service Fabric forniscono anche un ambiente di runtime di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="820d6-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="820d6-232">Hello differenza consiste nel fatto che il servizio Cloud sviluppo runtime emula hello hello ambiente Azure in cui viene eseguito, Service Fabric non usa un emulatore - Usa il runtime di Service Fabric completo hello.</span><span class="sxs-lookup"><span data-stu-id="820d6-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="820d6-233">Hello Service Fabric è di ambiente viene eseguita nel computer di sviluppo locale hello stesso ambiente che viene eseguito nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="820d6-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="820d6-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="820d6-234">Next steps</span></span>
<span data-ttu-id="820d6-235">Altre informazioni sui servizi di Service Fabric affidabile e sulle differenze fondamentali di hello tra servizi Cloud e toounderstand di architettura dell'applicazione di Service Fabric configurazione tootake sfruttare hello completo delle funzionalità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="820d6-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="820d6-236">Introduzione a Reliable Services di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="820d6-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="820d6-237">Guida concettuale toohello differenze infrastruttura dei servizi e i servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="820d6-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
