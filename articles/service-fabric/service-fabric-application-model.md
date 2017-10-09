---
title: modello di applicazione di Service Fabric aaaAzure | Documenti Microsoft
description: Come toomodel e descrivere applicazioni e servizi di Service Fabric.
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modellare un'applicazione in Service Fabric
In questo articolo viene fornita una panoramica del modello di applicazione di Azure Service Fabric hello e come toodefine un'applicazione e servizio tramite file manifesto.

## <a name="understand-hello-application-model"></a>Comprendere il modello di applicazione hello
Un'applicazione è una raccolta di servizi costituenti che eseguono determinate funzioni. Un servizio esegue una funzione completa e autonoma e può essere avviato ed eseguito in modo indipendente da altri servizi.  Un servizio è costituito da codice, configurazione e dati. Per ogni servizio, codice è costituito da file binari eseguibili hello e dati è costituito da dati statici arbitrario toobe utilizzato dal servizio hello configurazione è costituita da impostazioni del servizio che possono essere caricate in fase di esecuzione. Per ogni componente di questo modello applicativo gerarchico è possibile eseguire il controllo delle versioni e l'aggiornamento in modo indipendente.

![modello dell'applicazione Hello Service Fabric][appmodel-diagram]

Un tipo di applicazione è una categorizzazione di un'applicazione e consiste in un'aggregazione di tipi di servizi. Un tipo di servizio è una categorizzazione di un servizio. categorizzazione di Hello può avere diverse impostazioni e configurazioni, ma rimane la funzionalità di base hello hello stesso. le istanze di un servizio Hello sono variazioni di configurazione di servizio diverso hello di hello stesso tipo di servizio.  

Le classi (o "tipi") di applicazioni e servizi vengono descritte nei file XML (manifesti dell'applicazione e manifesti del servizio).  i manifesti di Hello sono modelli hello rispetto al quale è possono creare applicazioni dall'archivio di immagini del cluster hello istanze. viene installato con hello Service Fabric SDK Hello definizione dello schema per il file ServiceManifest.xml e ApplicationManifest.xml di hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

codice Hello per le istanze dell'applicazione diverso eseguiti come processi distinti, anche quando sono ospitati da hello stesso nodo di Service Fabric. Inoltre, hello ciclo di vita di ogni istanza dell'applicazione può essere gestito (ad esempio, l'aggiornamento) in modo indipendente. Hello diagramma seguente mostra come tipi di applicazioni sono costituiti da tipi di servizio, che a sua volta sono costituiti da codice, configurazione e i pacchetti di dati. diagramma di hello toosimplify, solo i pacchetti dati/config/codice hello per `ServiceType4` vengono visualizzati, anche se ogni tipo di servizio include alcuni o tutti i tipi di pacchetti.

![Tipi di applicazioni di Service Fabric e tipi di servizio][cluster-imagestore-apptypes]

Due diversi file manifesti vengono usate toodescribe applicazioni e servizi: hello manifesto del servizio e manifesto dell'applicazione. I manifesti sono illustrati in dettaglio nelle sezioni che seguono hello.

Può essere attivo nel cluster hello uno o più istanze di un tipo di servizio. Ad esempio, le istanze del servizio con stato, o repliche, ottenere affidabilità replica dello stato tra le repliche che si trova in nodi diversi cluster hello. Essenzialmente fornisce la ridondanza per hello servizio toobe disponibile anche se un nodo in un cluster non riesce. Oggetto [partizionata servizio](service-fabric-concepts-partitioning.md) ulteriormente divide il relativo stato (e stato toothat modelli di accesso) tra i nodi del cluster di hello.

Hello diagramma seguente mostra la relazione hello tra applicazioni e le istanze del servizio, partizioni e repliche.

![Partizioni e repliche in un servizio][cluster-application-instances]

> [!TIP]
> È possibile visualizzare il layout di hello delle applicazioni in un cluster con lo strumento Service Fabric Explorer hello disponibile in http://&lt;yourclusteraddress&gt;: 19080/Explorer. Per altre informazioni, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Descrivere un servizio
manifesto del servizio Hello definisce in modo dichiarativo il tipo di servizio di hello e versione. Specifica i metadati del servizio, ad esempio il tipo di servizio, le proprietà di integrità, le metriche del bilanciamento del carico, i file binari del servizio e i file di configurazione.  In altre parole, pacchetti di codice, configurazione e dati hello che compongono un toosupport pacchetto servizio descrive uno o più tipi di servizio. Questo è un semplice esempio di manifesto del servizio:

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

**Versione** gli attributi sono stringhe non strutturate e non analizzato dal sistema hello. Attributi della versione sono utilizzati tooversion ogni componente per gli aggiornamenti.

**ServiceTypes** dichiara i tipi di servizi supportati da **CodePackages** nel manifesto. Quando viene creata un'istanza di un servizio sulla base di uno di questi tipi di servizi, tutti i pacchetti di codice dichiarati nel manifesto vengono attivati eseguendo i relativi punti di ingresso. processi risultanti Hello sono tipi di servizio previsto tooregister hello è supportato in fase di esecuzione. Tipi di servizio vengono dichiarati a livello di manifesto hello e non livello di pacchetto codice hello. Pertanto, quando sono presenti più pacchetti di codice, sono tutte attivate ogni volta che il sistema hello cerca uno qualsiasi dei tipi di servizio dichiarati hello.

**SetupEntryPoint** è un punto di ingresso con privilegi che viene eseguito con hello stesso credenziali come Service Fabric (in genere hello *LocalSystem* account) prima di qualsiasi altro punto di ingresso. eseguibile Hello specificato da **EntryPoint** è in genere l'host del servizio hello con esecuzione prolungata. presenza di Hello di un punto di ingresso del programma di installazione separato evita l'host del servizio hello toorun con privilegi elevati per lunghi periodi di tempo. eseguibile Hello specificato da **EntryPoint** viene eseguito dopo **SetupEntryPoint** termina correttamente. Se il processo di hello mai termina o si blocca, processo risultante hello viene monitorato e riavviato (a partire da nuovamente con **SetupEntryPoint**).  

Scenari tipici per l'utilizzo di **SetupEntryPoint** sono quando si esegue un file eseguibile prima dell'avvio del servizio hello o si esegue un'operazione con privilegi elevati. ad esempio:

* Impostazione e l'inizializzazione di variabili di ambiente hello esigenze eseguibile del servizio. Non si tratta di file eseguibili tooonly limitato scritti tramite modelli di programmazione di Service Fabric hello. Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.
* Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.

Per ulteriori informazioni su come hello tooconfigure **SetupEntryPoint** vedere [configurare criteri di hello per un punto di ingresso del programma di installazione del servizio](service-fabric-application-runas-security.md)

**EnvironmentVariables** offre un elenco di variabili di ambiente impostate per questo pacchetto di codice. Le variabili Environmentment possono essere sottoposto a override in hello `ApplicationManifest.xml` tooprovide valori diversi per diverse istanze del servizio. 

**DataPackage** dichiara una cartella, denominata da hello **nome** attributo, che contiene i dati statici arbitrario toobe utilizzata dal processo hello in fase di esecuzione.

**ConfigPackage** dichiara una cartella, denominata da hello **nome** attributo, che contiene un *Settings* file. file di impostazioni Hello contiene sezioni di impostazioni di coppia chiave-valore specifico definito dall'utente che il processo di hello legge nuovamente in fase di esecuzione. Durante un aggiornamento, se solo hello **ConfigPackage** **versione** è stata modificata, quindi hello esecuzione processo non viene riavviato. Al contrario, un callback di notifica processo hello che le impostazioni di configurazione sono state modificate in modo che possa essere ricaricati in modo dinamico. Questo è un esempio di file *Settings.xml* :

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
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Descrivere un'applicazione
manifesto dell'applicazione Hello descrive in modo dichiarativo il tipo di applicazione hello e la versione. Specifica i metadati di composizione dei servizi, ad esempio i nomi stabili, lo schema di partizionamento, il numero di istanze/fattore di replica, i criteri di sicurezza/isolamento, i vincoli di posizionamento, gli override di configurazione e i tipi di servizi costituenti. sono descritti anche i domini di bilanciamento del carico Hello in cui viene inserita l'applicazione hello.

Di conseguenza, un manifesto dell'applicazione vengono descritti gli elementi a livello di applicazione hello e fa riferimento a uno o più servizio manifesti toocompose un tipo di applicazione. Questo è un semplice esempio di manifesto dell'applicazione:

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

Ad esempio i manifesti del servizio, **versione** gli attributi sono stringhe non strutturate e non vengono analizzati dal sistema hello. Attributi della versione sono anche utilizzati tooversion ogni componente per gli aggiornamenti.

**Oggetto ServiceManifestImport** contiene manifesti tooservice riferimenti che compongono questo tipo di applicazione. I manifesti di servizi importati determinano i tipi di servizi validi per questo tipo di applicazione. All'interno di hello oggetto ServiceManifestImport, eseguire l'override dei valori di configurazione nelle variabili di ambiente e Settings nel file ServiceManifest.xml. 


**DefaultServices** dichiara le istanze dei servizi create automaticamente ogni volta che viene creata un'istanza di un'applicazione sulla base di questo tipo di applicazione. I servizi predefiniti vengono forniti per comodità e dopo la creazione si comportano come normali servizi sotto ogni aspetto. Essi vengono aggiornati con tutti gli altri servizi nell'istanza di applicazione hello e possono essere rimossi anche.

> [!NOTE]
> Un manifesto dell'applicazione può contenere più importazioni di manifesti di servizi e servizi predefiniti. È possibile controllare le versioni di ogni manifesto del servizio in modo indipendente.
> 
> 

toolearn toomaintain altra applicazione e i parametri di servizio per i singoli ambienti, vedere [la gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Passaggi successivi
[Pacchetto di un'applicazione](service-fabric-package-apps.md) e renderlo pronto toodeploy.

[Distribuire e rimuovere le applicazioni] [ 10] viene descritto come le istanze dell'applicazione toomanage toouse PowerShell.

[Gestione dei parametri dell'applicazione per più ambienti] [ 11] viene descritto come tooconfigure parametri e variabili di ambiente per le istanze dell'applicazione diverso.

[Configurare i criteri di sicurezza per l'applicazione] [ 12] viene descritto come toorun servizi con accesso toorestrict criteri di sicurezza.

[Modelli di hosting dell'applicazione][13] descrive la relazione tra le repliche (o istanze) di un servizio distribuito e il processo host del servizio.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
