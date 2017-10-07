---
title: "aaaManage più ambienti in Service Fabric | Documenti Microsoft"
description: "È possibile eseguire le applicazioni di Service Fabric in cluster in un intervallo dimensioni da una macchina toothousands di macchine. In alcuni casi, si desidererà tooconfigure l'applicazione in modo diverso per i diversi ambienti. Questo articolo descrive come parametri di toodefine applicazioni diverso per ogni ambiente."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Gestire i parametri dell'applicazione per più ambienti
È possibile creare cluster di Azure Service Fabric usando ovunque da uno toomany migliaia di computer. Mentre i file binari dell'applicazione può essere eseguito senza alcuna modifica tra l'ampia gamma di ambienti, è spesso necessario applicazione hello tooconfigure in modo diverso, in base al numero hello macchine, che esegue la distribuzione.

Ad esempio, considerare `InstanceCount` per un servizio senza stato. Quando si eseguono le applicazioni in Azure, è in genere opportuno tooset questo toohello speciale valore di parametro "-1". Questa configurazione assicura che il servizio sia in esecuzione in ogni nodo nel cluster hello (o tutti i nodi nel tipo di nodo hello se è stato impostato un vincolo di posizionamento). Tuttavia, questa configurazione non è adatta per un cluster singolo computer perché non è possibile avere più processi in attesa su hello stesso endpoint in un singolo computer. È invece in genere impostare `InstanceCount` troppo "1".

## <a name="specifying-environment-specific-parameters"></a>Definizione dei parametri specifici dell'ambiente
problema di configurazione toothis soluzione hello è un set di servizi con parametri predefiniti e i file dei parametri dell'applicazione che vengono compilati i valori dei parametri per un determinato ambiente. Servizi predefiniti e i parametri dell'applicazione vengono configurati in un'applicazione hello e manifesti del servizio. viene installato con hello Service Fabric SDK Hello definizione dello schema per file ServiceManifest.xml e ApplicationManifest.xml hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Servizi predefiniti
Le applicazioni di infrastruttura di servizi sono costituite da una raccolta di istanze del servizio. Mentre è possibile che si toocreate un'applicazione vuota e quindi creare tutte le istanze di servizio in modo dinamico, la maggior parte delle applicazioni dispongono di un set di servizi di base che deve sempre essere creata quando viene creata un'istanza di un'applicazione hello. Si tratta di cui viene fatto riferimento tooas "servizi predefiniti". Vengono specificati nel manifesto dell'applicazione hello, con segnaposto per la configurazione per ogni ambiente inclusi tra parentesi quadre:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Ognuno dei parametri denominato hello deve essere definito nell'elemento Parameters hello del manifesto dell'applicazione hello:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

l'attributo DefaultValue Hello specifica hello valore toobe utilizzata in assenza di hello di parametro più specifici per un determinato ambiente.

> [!NOTE]
> Non tutti i parametri di istanza del servizio sono idonei alla configurazione specifica per il singolo ambiente. Nell'esempio hello sopra, hello LowKey e i valori di HighKey per lo schema di partizionamento del servizio hello definiti in modo esplicito per tutte le istanze del servizio hello dall'intervallo di partizione hello è una funzione hello di domini di dati, non l'ambiente hello.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Impostazioni della configurazione del servizio specifica per il singolo ambiente
Hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md) Abilita servizi tooinclude i pacchetti di configurazione che contengono coppie chiave-valore personalizzate che sono leggibili in fase di esecuzione. i valori Hello di queste impostazioni possono essere distinti anche dall'ambiente specificando un `ConfigOverride` nel manifesto dell'applicazione hello.

Si supponga di avere hello seguente impostazione nel file hello Config\Settings.xml hello `Stateful1` servizio:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride questo valore per una coppia di applicazione/ambiente specifico, creare un `ConfigOverride` quando si importa hello manifesto del servizio nel manifesto dell'applicazione hello.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Questo parametro può quindi essere configurato dall'ambiente, come illustrato in precedenza, È possibile farlo dichiararla nella sezione parametri hello del manifesto dell'applicazione hello e specificando i valori specifici dell'ambiente nei file di parametro dell'applicazione hello.

> [!NOTE]
> Nel caso di hello di impostazioni di configurazione del servizio, ci sono tre posizioni in cui è possibile impostare il valore di hello di una chiave: pacchetto di configurazione del servizio hello manifesto dell'applicazione hello e file di parametro dell'applicazione hello. Service Fabric verrà sempre scegliere da file di parametro dell'applicazione hello prima (se specificato), quindi hello manifesto dell'applicazione e infine hello pacchetto di configurazione.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Impostazione e uso delle variabili di ambiente 
È possibile specificare e impostare le variabili di ambiente nel file ServiceManifest.xml hello e quindi eseguire l'override di questi elementi nel file ApplicationManifest XML hello in ogni istanza.
Hello di esempio seguente mostra che due variabili di ambiente, uno con un valore impostato e viene eseguito l'override di altri hello. È possibile utilizzare i parametri dell'applicazione, le variabili di ambiente tooset valori hello stesso modo che questi sono stati utilizzati per le sostituzioni di configurazione.

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
variabili di ambiente toooverride hello in ApplicationManifest.xml, pacchetto di codice hello riferimento nel manifesto del servizio di hello con hello hello `EnvironmentOverrides` elemento.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Una volta creato l'istanza di servizio denominata hello è possibile accedere a variabili di ambiente hello dal codice. ad esempio In c# è possibile eseguire il seguente hello

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Variabili di ambiente di Service Fabric
Service Fabric dispone di variabili di ambiente predefinite, impostate per ciascuna istanza di servizio. Hello elenco completo delle variabili di ambiente viene di seguito, dove hello quelle in grassetto sono hello quelle che si utilizzerà nel servizio, hello altro che utilizzate dal runtime di Service Fabric. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[NomeDelServizio]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Hello belows di codice viene illustrato come toolist hello le variabili di ambiente di Service Fabric
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Hello esempi seguenti vengono illustrate le variabili di ambiente per un tipo di applicazione denominato `GuestExe.Application` con un tipo di servizio denominato `FrontEndService` quando viene eseguito sul computer di sviluppo locale.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>File di parametri dell'applicazione
progetto di applicazione di Service Fabric Hello può includere uno o più file di parametro dell'applicazione. Ognuno di essi definisce hello specifici valori hello parametri definiti nel manifesto dell'applicazione hello:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Per impostazione predefinita, una nuova applicazione include tre file di parametro dell'applicazione, denominati Local.1Node.xml, Local.5Node.xml e Cloud.xml:

![File di parametri dell'applicazione in Esplora soluzioni][app-parameters-solution-explorer]

un file di parametro, toocreate semplicemente copiare e incollare uno esistente quindi assegnarle un nuovo nome.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Identificazione di parametri specifici per il singolo ambiente durante la distribuzione
In fase di distribuzione, è necessario toochoose hello parametro appropriato file tooapply con l'applicazione. È possibile farlo tramite una finestra di dialogo pubblicazione hello in Visual Studio o PowerShell.

### <a name="deploy-from-visual-studio"></a>Eseguire una distribuzione da Visual Studio
È possibile scegliere dall'elenco di hello del file dei parametri disponibili quando si pubblica l'applicazione in Visual Studio.

![Scegliere un file di parametri nella finestra di dialogo pubblicazione hello][publishdialog]

### <a name="deploy-from-powershell"></a>Distribuire da PowerShell
Hello `Deploy-FabricApplication.ps1` script di PowerShell incluso nel modello di progetto applicazione hello accetta come parametro di un profilo di pubblicazione e hello PublishProfile contiene un file di parametri di riferimento toohello dell'applicazione.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Passaggi successivi
toolearn informazioni su alcuni dei concetti di base hello discussi sono trattati in questo argomento, vedere hello [Panoramica tecnica di Service Fabric](service-fabric-technical-overview.md). Per informazioni su altre funzionalità di gestione delle app disponibili in Visual Studio, vedere [Usare Visual Studio per semplificare la scrittura e la gestione delle applicazioni di Service Fabric](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
