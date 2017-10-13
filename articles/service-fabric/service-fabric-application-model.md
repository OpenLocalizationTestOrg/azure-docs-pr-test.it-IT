---
title: Modello di applicazione di Azure Service Fabric | Documentazione Microsoft
description: Come modellare e descrivere le applicazioni e servizi in infrastruttura di servizi.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modellare un'applicazione in Service Fabric
Questo articolo fornisce una panoramica del modello applicativo di Azure Service Fabric e come definire un'applicazione e un servizio attraverso file manifesto.

## <a name="understand-the-application-model"></a>Informazioni sul modello applicativo
Un'applicazione è una raccolta di servizi costituenti che eseguono determinate funzioni. Un servizio esegue una funzione completa e autonoma e può essere avviato ed eseguito in modo indipendente da altri servizi.  Un servizio è costituito da codice, configurazione e dati. Per ogni servizio, il codice è costituito dai file binari eseguibili, la configurazione è costituita dalle impostazioni del servizio che possono essere caricate in fase di esecuzione e i dati sono costituiti da dati statici arbitrari che devono essere usati dal servizio. Per ogni componente di questo modello applicativo gerarchico è possibile eseguire il controllo delle versioni e l'aggiornamento in modo indipendente.

![Modello di applicazione di Service Fabric][appmodel-diagram]

Un tipo di applicazione è una categorizzazione di un'applicazione e consiste in un'aggregazione di tipi di servizi. Un tipo di servizio è una categorizzazione di un servizio. La categorizzazione di un servizio può disporre di impostazioni e configurazioni diverse, ma la funzionalità di base resta la stessa. Le istanze di un servizio sono le diverse varianti di configurazione dello stesso tipo di servizio.  

Le classi (o "tipi") di applicazioni e servizi vengono descritte nei file XML (manifesti dell'applicazione e manifesti del servizio).  I manifesti sono i modelli in base ai quali è possibile creare istanze delle applicazioni dall'archivio immagini del cluster. La definizione dello schema per i file ServiceManifest.xml e ApplicationManifest.xml viene installata con l'SDK e gli strumenti di Service Fabric in *C:\Programmi\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

Il codice di istanze di applicazioni diverse viene eseguito come processo separato anche se ospitato dallo stesso nodo di Service Fabric. Il ciclo di vita di ogni istanza dell'applicazione può inoltre essere gestito, ad esempio aggiornato, in modo indipendente. Il diagramma seguente illustra come i tipi di applicazioni siano costituiti da tipi di servizi, che a loro volta sono costituiti da codice, configurazione e pacchetti di dati. Per semplificare il diagramma, vengono visualizzati solo i pacchetti codice/configurazione/dati relativi a `ServiceType4`, anche se ogni tipo di servizio può includere tutti questi tipi di pacchetti o solo alcuni.

![Tipi di applicazioni di Service Fabric e tipi di servizio][cluster-imagestore-apptypes]

Vengono usati due diversi file manifesto per descrivere le applicazioni e i servizi: il manifesto del servizio e il manifesto dell'applicazione. I manifesti sono descritti dettagliatamente nelle sezioni seguenti.

Nel cluster possono essere attive una o più istanze di un tipo di servizio. Le istanze o le repliche del servizio con stato ad esempio raggiungono un'elevata affidabilità replicando lo stato tra le repliche contenute in nodi diversi del cluster. Essenzialmente, la replica fornisce ridondanza in modo che il servizio sia disponibile anche se un nodo in un cluster ha un malfunzionamento. Un [servizio partizionato](service-fabric-concepts-partitioning.md) suddivide ulteriormente il proprio stato e i modelli di accesso a tale stato tra i nodi del cluster.

Il diagramma seguente illustra la relazione tra applicazioni e istanze di servizi, partizioni e repliche.

![Partizioni e repliche in un servizio][cluster-application-instances]

> [!TIP]
> È possibile visualizzare il layout delle applicazioni in un cluster usando lo strumento Service Fabric Explorer disponibile all'indirizzo http://&lt;yourclusteraddress&gt;:19080/Explorer. Per altre informazioni, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Descrivere un servizio
Il manifesto del servizio definisce in modo dichiarativo il tipo di servizio e la versione. Specifica i metadati del servizio, ad esempio il tipo di servizio, le proprietà di integrità, le metriche del bilanciamento del carico, i file binari del servizio e i file di configurazione.  In altri termini, descrive i pacchetti di codice, configurazione e dati che costituiscono un pacchetto servizio per supportare uno o più tipi di servizi. Questo è un semplice esempio di manifesto del servizio:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**Version** sono stringhe non strutturate e non analizzate dal sistema. Gli attributi Version vengono usati per il controllo delle versioni di ogni componente per gli aggiornamenti.

**ServiceTypes** dichiara i tipi di servizi supportati da **CodePackages** nel manifesto. Quando viene creata un'istanza di un servizio sulla base di uno di questi tipi di servizi, tutti i pacchetti di codice dichiarati nel manifesto vengono attivati eseguendo i relativi punti di ingresso. I processi risultanti devono registrare i tipi di servizi supportati in fase di esecuzione. I tipi di servizi sono dichiarati a livello di manifesto e non a livello di pacchetto di codice. Se pertanto sono presenti più pacchetti di codice, questi verranno tutti attivati ogni volta che il sistema ricerca uno dei tipi di servizi dichiarati.

**SetupEntryPoint** è un punto di ingresso con privilegi che viene eseguito con le stesse credenziali di Service Fabric (in genere l'account *LocalSystem* ) prima di qualsiasi altro punto di ingresso. L'eseguibile specificato da **EntryPoint** è in genere l'host del servizio a esecuzione prolungata. La presenza di un punto di ingresso di configurazione separato consente di evitare di dover eseguire l'host del servizio con privilegi elevati per lunghi periodi di tempo. L'eseguibile specificato da **EntryPoint** viene eseguito dopo che **SetupEntryPoint** termina correttamente. Se il processo termina o si arresta in modo anomalo, il processo risultante viene monitorato e riavviato (iniziando di nuovo con **SetupEntryPoint**).  

Gli scenari tipici per l'uso di **SetupEntryPoint** sono l'esecuzione di un file eseguibile prima dell'avvio del servizio o l'esecuzione di un'operazione con privilegi elevati. ad esempio:

* Impostazione e inizializzazione di variabili di ambiente necessari per il file eseguibile del servizio. Questo non è limitato solo agli eseguibili scritti tramite i modelli di programmazione di Service Fabric. Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.
* Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.

Per altre informazioni su come configurare **SetupEntryPoint**, vedere [Configurare i criteri per il punto di ingresso dell'installazione del servizio](service-fabric-application-runas-security.md)

**EnvironmentVariables** offre un elenco di variabili di ambiente impostate per questo pacchetto di codice. Le variabili di ambiente possono essere sostituite in `ApplicationManifest.xml` per specificare valori diversi per diverse istanze del servizio. 

**DataPackage** dichiara una cartella, denominata dall'attributo **Name**, che contiene i dati statici arbitrari che devono essere usati dal processo in fase di esecuzione.

**ConfigPackage** dichiara una cartella, denominata dall'attributo **Name**, che contiene un file *Settings.xml*. Questo file di impostazioni contiene sezioni di impostazioni di coppie chiave-valore definite dall'utente che vengono lette dal processo in fase di esecuzione. Se durante un aggiornamento è cambiato solo l'attributo **version** **ConfigPackage**, il processo in esecuzione non viene riavviato. Un callback piuttosto notifica al processo che le impostazioni di configurazione sono cambiate affinché vengano ricaricate in modo dinamico. Questo è un esempio di file *Settings.xml* :

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Un manifesto del servizio può contenere più pacchetti di codice, configurazione e dati. Ognuna di queste può essere creata in modo indipendente.
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Descrivere un'applicazione
Il manifesto dell'applicazione descrive in modo dichiarativo il tipo di applicazione e la versione. Specifica i metadati di composizione dei servizi, ad esempio i nomi stabili, lo schema di partizionamento, il numero di istanze/fattore di replica, i criteri di sicurezza/isolamento, i vincoli di posizionamento, gli override di configurazione e i tipi di servizi costituenti. Vengono descritti anche i domini di bilanciamento del carico in cui viene posizionata l'applicazione.

Un manifesto dell'applicazione quindi descrive elementi a livello di applicazione e fa riferimento a uno o più manifesti dei servizi per comporre un tipo di applicazione. Questo è un semplice esempio di manifesto dell'applicazione:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Analogamente ai manifesti dei servizi, gli attributi **Version** sono stringhe non strutturate e non analizzate dal sistema. Gli attributi Version vengono anche usati per il controllo delle versioni di ogni componente per gli aggiornamenti.

**ServiceManifestImport** contiene riferimenti a manifesti di servizi che costituiscono questo tipo di applicazione. I manifesti di servizi importati determinano i tipi di servizi validi per questo tipo di applicazione. In ServiceManifestImport si esegue l'override dei valori di configurazione nel file Settings.xml e delle variabili di ambiente nel file ServiceManifest.xml. 


**DefaultServices** dichiara le istanze dei servizi create automaticamente ogni volta che viene creata un'istanza di un'applicazione sulla base di questo tipo di applicazione. I servizi predefiniti vengono forniti per comodità e dopo la creazione si comportano come normali servizi sotto ogni aspetto. Vengono aggiornati insieme agli altri servizi nell'istanza dell'applicazione e possono anche essere rimossi.

> [!NOTE]
> Un manifesto dell'applicazione può contenere più importazioni di manifesti di servizi e servizi predefiniti. È possibile controllare le versioni di ogni manifesto del servizio in modo indipendente.
> 
> 

Per informazioni su come mantenere applicazioni diverse e parametri di servizio per ambienti singoli, vedere [Gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Passaggi successivi
[Creare il pacchetto di un'applicazione](service-fabric-package-apps.md) e prepararlo per la distribuzione.

[Distribuire e rimuovere applicazioni con PowerShell][10]: descrive come usare PowerShell per gestire le istanze dell'applicazione.

[Gestire i parametri dell'applicazione per più ambienti][11]: descrive come configurare parametri e variabili di ambiente per istanze di applicazione diverse.

[Configurare i criteri di sicurezza per l'applicazione][12]: descrive come eseguire i servizi nell'ambito dei criteri di sicurezza per limitare l'accesso.

[Modelli di hosting dell'applicazione][13] descrive la relazione tra le repliche (o istanze) di un servizio distribuito e il processo host del servizio.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
