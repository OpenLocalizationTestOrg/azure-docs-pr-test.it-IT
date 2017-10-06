---
title: gli endpoint del servizio Service Fabric aaaSpecifying | Documenti Microsoft
description: "Il manifesto toodescribe risorse di endpoint in un servizio, compresa la modalità tooset degli endpoint HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a>Specificare le risorse in un manifesto del servizio
## <a name="overview"></a>Panoramica
manifesto del servizio Hello consente le risorse usate da hello servizio toobe dichiarato modificato senza modificare il codice compilato hello. Azure Service Fabric supporta la configurazione delle risorse di endpoint per il servizio di hello. è possibile controllare le risorse di toohello accesso Hello specificate nel manifesto del servizio hello tramite hello SecurityGroup nel manifesto dell'applicazione hello. dichiarazione di Hello delle risorse consente toobe queste risorse modificato in fase di distribuzione, vale a dire servizio hello non deve necessariamente toointroduce un nuovo meccanismo di configurazione. viene installato con hello Service Fabric SDK Hello definizione dello schema per il file ServiceManifest.xml hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Endpoint
Quando una risorsa endpoint viene definita nel manifesto del servizio hello, Service Fabric assegna le porte dall'intervallo di porte riservata hello applicazione quando non è specificata una porta in modo esplicito. Ad esempio, esaminare endpoint hello *ServiceEndpoint1* specificato nel frammento di manifesto hello fornito dopo il paragrafo. Inoltre, i servizi possono richiedere anche una porta specifica in una risorsa. Le repliche del servizio in esecuzione in nodi di cluster diversi possono essere assegnate diversi numeri di porta, mentre le repliche di un servizio in esecuzione su hello stessa porta hello condivisione di nodo. repliche servizio Hello è quindi possono utilizzare queste porte come necessario per la replica e per le richieste client in ascolto.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Fare riferimento troppo[configurazione servizi affidabili con stato](service-fabric-reliable-services-configuration.md) tooread ulteriori informazioni sull'endpoint di riferimento dal file di impostazioni pacchetto config hello (Settings).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Esempio: specificare un endpoint HTTP per il servizio
Hello manifesto del servizio seguente definisce una risorsa di endpoint TCP e due risorse di endpoint HTTP in hello &lt;risorse&gt; elemento.

Gli endpoint HTTP vengono automaticamente inseriti nell'elenco di controllo di accesso da Service Fabric.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Esempio: specificare un endpoint HTTPS per il servizio
Hello il protocollo HTTPS fornisce l'autenticazione server e viene usato anche per crittografare le comunicazioni client-server. tooenable HTTPS nel servizio Service Fabric, specificare il protocollo di hello in hello *risorse -> endpoint -> Endpoint* sezione hello del manifesto del servizio, come illustrato in precedenza per l'endpoint di hello *ServiceEndpoint3* .

> [!NOTE]
> Un protocollo del servizio non può essere modificato durante l'aggiornamento dell'applicazione. Se viene modificato durante l'aggiornamento, si tratta di una modifica importante.
> 
> 

Di seguito è riportato un esempio ApplicationManifest che è necessario tooset per HTTPS. è necessario specificare l'identificazione personale Hello per il certificato. Hello EndpointRef è tooEndpointResource un riferimento nel manifesto del servizio, per cui impostare il protocollo HTTPS hello. È possibile aggiungere più Endpointcertificate.  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Override degli endpoint in ServiceManifest.xml

In hello ApplicationManifest aggiungere una sezione ResourceOverrides che sarà una sezione tooConfigOverrides di pari livello. In questa sezione è possibile specificare hello override per la sezione di endpoint hello nella sezione risorse hello specificato nel manifesto del servizio hello.

In ordine toooverride EndPoint nel manifesto del servizio utilizzando Modifica ApplicationParameters hello ApplicationManifest come riportato di seguito:

Nella sezione oggetto ServiceManifestImport hello aggiungere una nuova sezione "ResourceOverrides"

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

In hello che aggiungono parametri di seguito:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Durante la distribuzione di un'applicazione hello ora è possibile passare questi valori come ApplicationParameters ad esempio:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Nota: Se i valori hello forniscono per hello ApplicationParameters è vuota tornando predefinito toohello valore fornito in hello manifesto del servizio per hello EndPointName corrispondente.

ad esempio:

Se nel manifesto del servizio specificato hello

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Hello Port1 e il valore di Protocol1 per i parametri dell'applicazione è null o vuoto. porta Hello è ancora stabilita dalla ServiceFabric. E hello protocollo tcp.

Si supponga di specificare un valore errato. Ad esempio per la porta è stato specificato un valore stringa "Foo" anziché di tipo int.  Nuovo ServiceFabricApplication comando avrà esito negativo con errore: parametro di sostituzione hello dell'attributo name 'ServiceEndpoint1' "Port1" nella sezione 'ResourceOverrides' non è valido. il valore di Hello specificato è "Foo" e necessario 'int'.
