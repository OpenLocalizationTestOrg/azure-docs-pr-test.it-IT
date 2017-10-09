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
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Guida tooconverting servizi Web e ruoli di lavoro tooService infrastruttura senza stati
Questo articolo viene descritto come toomigrate i ruoli di lavoro e Web dei servizi Cloud tooService infrastruttura senza stati servizi. Si tratta di percorso di migrazione più semplice di hello da servizi Cloud tooService dell'infrastruttura per applicazioni la cui architettura complessiva verrà toostay approssimativamente hello stesso.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Progetto di applicazione di servizio progetto tooService dell'infrastruttura cloud
 Un progetto servizio Cloud e un progetto di applicazione di Service Fabric presentano una struttura simile e unità di distribuzione hello entrambi rappresentano per l'applicazione, vale a dire, ognuno di essi definiscono hello completo pacchetto toorun distribuito l'applicazione. Un progetto di Servizi cloud contiene uno o più ruoli di lavoro o Web. In modo analogo un progetto di applicazione di Service Fabric contiene uno o più servizi. 

differenza Hello è che legato progetto servizio Cloud di hello hello distribuzione dell'applicazione con una distribuzione della macchina virtuale e pertanto contiene le impostazioni di configurazione macchina virtuale, mentre il progetto di applicazione di Service Fabric hello definisce solo un'applicazione che verrà distribuita tooa set di macchine virtuali esistenti in un cluster di Service Fabric. cluster di Service Fabric Hello stesso viene distribuito solo una volta, tramite un modello di gestione risorse o hello portale di Azure, più infrastruttura dei servizi e le applicazioni possono essere distribuiti tooit.

![Confronto tra i progetti di Servizi cloud e Service Fabric][3]

## <a name="worker-role-toostateless-service"></a>Servizio toostateless ruolo di lavoro
Concettualmente, un ruolo di lavoro rappresenta un carico di lavoro senza stato, pertanto ogni istanza di carico di lavoro hello è identica e le richieste possono essere indirizzati tooany istanza in qualsiasi momento. Ogni istanza non è richiesta precedente di hello tooremember previsto. Stato di tale carico di lavoro hello opera su è gestito da un archivio di stato esterno, ad esempio l'archiviazione tabelle di Azure o Azure Documentdb. In Service Fabric questo tipo di carico di lavoro è rappresentato da un servizio senza stato. toomigrating approccio più semplice di Hello tooService un ruolo di lavoro infrastruttura può essere eseguita ruolo di lavoro codice tooa servizio senza stato di conversione.

![Ruolo di lavoro tooStateless servizio][4]

## <a name="web-role-toostateless-service"></a>Ruolo toostateless servizio Web
TooWorker simile ruolo, un ruolo Web rappresenta anche un carico di lavoro senza stato e pertanto concettualmente troppo può essere mappato tooa servizio senza stato Service Fabric. Tuttavia, a differenza dei ruoli Web, Service Fabric non supporta IIS. toomigrate un'applicazione web da un servizio senza stato tooa di ruolo Web è necessario prima framework web tooa mobile che possono essere indipendenti e non dipendono da IIS o System. Web, ad esempio ASP.NET Core 1.

| **Applicazione** | **Supportato** | **Percorso di migrazione** |
| --- | --- | --- |
| Web Form ASP.NET |No |Convertire tooASP.NET Core 1 MVC |
| ASP.NET MVC |Con migrazione |Aggiornamento tooASP.NET Core 1 MVC |
| API Web ASP.NET |Con migrazione |Usare un server self-hosted o ASP.NET Core 1 |
| ASP.NET Core 1 |Sì |N/D |

## <a name="entry-point-api-and-lifecycle"></a>API del punto di ingresso e ciclo di vita
Le API del servizio di Service Fabric e del ruolo di lavoro offrono punti di ingresso simili: 

| **Punto di ingresso** | **Istanze del ruolo di lavoro** | **Servizio di Service Fabric** |
| --- | --- | --- |
| Elaborazione in corso |`Run()` |`RunAsync()` |
| Avvio della macchina virtuale |`OnStart()` |N/D |
| Arresto della macchina virtuale |`OnStop()` |N/D |
| Apertura del listener per le richieste client |N/D |<ul><li> `CreateServiceInstanceListener()` per servizi senza stato</li><li>`CreateServiceReplicaListener()` per servizi con stato</li></ul> |

### <a name="worker-role"></a>Istanze del ruolo di lavoro
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

### <a name="service-fabric-stateless-service"></a>Servizio senza stato di Service Fabric
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

Entrambe dispongono di un override primario "Esegui" in cui toobegin l'elaborazione. I servizi di Service Fabric combinano `Run`, `Start` e `Stop` in un singolo punto di ingresso, `RunAsync`. Il servizio deve iniziare a lavorare quando `RunAsync` viene avviato e deve smettere di funzionare quando hello `RunAsync` segnalata CancellationToken del metodo. 

Esistono alcune differenze principali tra hello del ciclo di vita e la durata dei servizi di infrastruttura dei servizi e i ruoli di lavoro:

* **Ciclo di vita:** hello differenza principale è che un ruolo di lavoro è una macchina virtuale e pertanto il ciclo di vita è abbinato toohello macchina virtuale, che include eventi per quando hello VM avvia e arresta. Un servizio di Service Fabric dispone di un ciclo di vita è separato dal ciclo di vita di hello macchina virtuale, in modo non include gli eventi per quando hello host macchina virtuale o l'avvio della macchina e stop, poiché non sono correlate.
* **Durata:** un'istanza del ruolo di lavoro verrà riciclati se hello `Run` metodo esce. Hello `RunAsync` metodo in un servizio di Service Fabric può tuttavia eseguire toocompletion e viene mantenuta l'istanza del servizio hello backup. 

Service Fabric fornisce un punto di ingresso facoltativo di configurazione della comunicazione per i servizi in ascolto delle richieste client. Hello RunAsync sia il punto di ingresso di comunicazione sono sostituzioni facoltative in servizi di Service Fabric - il servizio può scegliere tooonly tooclient le richieste o solo di eseguire un ciclo di elaborazione o entrambi - motivo per cui può tooexit senza hello RunAsync (metodo) riavviare l'istanza di servizio di hello, perché può continuare toolisten per le richieste client.

## <a name="application-api-and-environment"></a>API dell'applicazione e ambiente
ambiente di servizi Cloud Hello API fornisce informazioni e funzionalità per l'istanza corrente della macchina virtuale hello, nonché informazioni sulle altre istanze del ruolo VM. Service Fabric fornisce informazioni correlate tooits runtime e alcune informazioni sul nodo hello un servizio in esecuzione. 

| **Attività dell'ambiente** | **Servizi cloud** | **Service Fabric** |
| --- | --- | --- |
| Impostazioni di configurazione e notifica di modifiche |`RoleEnvironment` |`CodePackageActivationContext` |
| Archiviazione locale |`RoleEnvironment` |`CodePackageActivationContext` |
| Informazioni sull'endpoint |`RoleInstance` <ul><li>Istanza corrente: `RoleEnvironment.CurrentRoleInstance`</li><li>Altri ruoli e istanze: `RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` per l'indirizzo del nodo corrente</li><li>`FabricClient` e `ServicePartitionResolver` per l'individuazione di endpoint di servizio</li> |
| Emulazione dell'ambiente |`RoleEnvironment.IsEmulated` |N/D |
| Evento di modifica simultanea |`RoleEnvironment` |N/D |

## <a name="configuration-settings"></a>Impostazioni di configurazione
Le impostazioni di configurazione di servizi Cloud vengono impostate per un ruolo VM e applicano tooall istanze del ruolo VM. Queste impostazioni sono coppie chiave-valore impostate nei file ServiceConfiguration.*.cscfg e sono accessibili direttamente tramite RoleEnvironment. Nell'infrastruttura del servizio, impostazioni si applicano singolarmente tooeach servizio e applicazione tooeach anziché tooa VM, perché una macchina virtuale può ospitare più servizi e applicazioni. Un servizio è composto da tre pacchetti:

* **Codice:** contiene file eseguibili del servizio hello, i file binari, dll e qualsiasi altro file di un servizio deve toorun.
* **Config:** tutti i file di configurazione e le impostazioni per un servizio.
* **Dati:** i file di dati statici associati al servizio hello.

Per ognuno di questi pacchetti l'aggiornamento e il controllo delle versioni possono essere gestiti in modo indipendente. Servizi tooCloud simili, un pacchetto di configurazione è possibile accedere a livello di codice tramite un'API e gli eventi sono disponibili toonotify hello del servizio di una modifica della configurazione del pacchetto. Un file Settings. XML può essere utilizzato per la configurazione di chiave-valore e l'accesso programmatico simile toohello app sezione Impostazioni di un file app. config. Tuttavia, a differenza di Servizi cloud, un pacchetto di configurazione di Service Fabric può contenere qualsiasi file di configurazione in qualsiasi formato, ovvero XML, JSON, YAML o un formato binario personalizzato. 

### <a name="accessing-configuration"></a>Accesso alla configurazione
#### <a name="cloud-services"></a>Servizi cloud
Le impostazioni di configurazione di ServiceConfiguration.*.cscfg sono accessibili tramite `RoleEnvironment`. Queste impostazioni sono disponibili globalmente tooall le istanze del ruolo in hello stessa distribuzione del servizio Cloud.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Ogni servizio ha un pacchetto di configurazione individuale. Non esiste un meccanismo predefinito per le impostazioni di configurazione globali accessibile da tutte le applicazioni in un cluster. Quando si usa speciali Settings file di configurazione del Service Fabric all'interno di un pacchetto di configurazione, i valori nel file Settings.xml possono essere sovrascritte a livello di applicazione hello, rendendo possibili impostazioni di configurazione a livello di applicazione.

Impostazioni di configurazione sono gli accessi all'interno di ogni istanza del servizio tramite servizio di hello `CodePackageActivationContext`.

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

### <a name="configuration-update-events"></a>Eventi di aggiornamento della configurazione
#### <a name="cloud-services"></a>Servizi cloud
Hello `RoleEnvironment.Changed` evento è utilizzata toonotify si verifica tutte le istanze del ruolo quando una modifica nell'ambiente di hello, ad esempio una modifica della configurazione. Si tratta di aggiornamenti della configurazione tooconsume utilizzato senza il riciclo delle istanze del ruolo o riavviare un processo di lavoro.

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

#### <a name="service-fabric"></a>Service Fabric
Ciascuno di hello tre tipi di pacchetto in un servizio di codice, configurazione e dati - dispongono di eventi che notificano un'istanza del servizio viene aggiornato, aggiunto o rimosso un pacchetto. Un servizio può contenere più pacchetti di ogni tipo. Ad esempio, un servizio può avere più pacchetti Config, ognuno aggiornabile e con controllo delle versioni gestito in modo indipendente. 

Questi eventi sono modifiche tooconsume disponibili nei pacchetti del servizio senza dover riavviare l'istanza del servizio hello.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Attività di avvio
Le attività di avvio sono azioni eseguite prima dell'avvio di un'applicazione. Un'attività di avvio è generalmente usati toorun gli script di installazione con privilegi elevati. Sia Servizi Cloud che Service Fabric supportano attività di avvio. Hello differenza principale è che in servizi Cloud, un'attività di avvio è abbinato tooa VM perché fa parte di un'istanza del ruolo, mentre nell'infrastruttura del servizio un'attività di avvio è servizio tooa collegati, che non è vincolata tooany determinata macchina virtuale.

| Servizi cloud | Service Fabric |
| --- | --- | --- |
| Percorso di configurazione |ServiceDefinition.csdef |
| Privilegi |"limitato" o "con privilegi elevati" |
| Sequenziazione |"semplice", "background", "in primo piano" |

### <a name="cloud-services"></a>Servizi cloud
In Servizi cloud è configurato un punto di ingresso di avvio per ogni ruolo in ServiceDefinition.csdef. 

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

### <a name="service-fabric"></a>Service Fabric
In Service Fabric è configurato un punto di ingresso di avvio per ogni servizio in ServiceManifest.xml:

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

## <a name="a-note-about-development-environment"></a>Note sull'ambiente di sviluppo
Servizi Cloud e infrastruttura di servizio sono integrati con Visual Studio con modelli di progetto e il supporto per il debug, la configurazione e distribuzione sia in locale e tooAzure. Servizi cloud e Service Fabric forniscono anche un ambiente di runtime di sviluppo locale. Hello differenza consiste nel fatto che il servizio Cloud sviluppo runtime emula hello hello ambiente Azure in cui viene eseguito, Service Fabric non usa un emulatore - Usa il runtime di Service Fabric completo hello. Hello Service Fabric è di ambiente viene eseguita nel computer di sviluppo locale hello stesso ambiente che viene eseguito nell'ambiente di produzione.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sui servizi di Service Fabric affidabile e sulle differenze fondamentali di hello tra servizi Cloud e toounderstand di architettura dell'applicazione di Service Fabric configurazione tootake sfruttare hello completo delle funzionalità di Service Fabric.

* [Introduzione a Reliable Services di Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Guida concettuale toohello differenze infrastruttura dei servizi e i servizi Cloud](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
