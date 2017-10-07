---
title: aaaService dell'infrastruttura e la distribuzione di contenitori | Documenti Microsoft
description: "Service Fabric e hello utilizzare contenitori toodeploy microservizio applicazioni. Questo articolo descrive le funzionalità di hello forniti per i contenitori e come toodeploy immagine di un contenitore di Windows in un cluster di Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Distribuire un tooService di contenitore di Windows Fabric
> [!div class="op_single_selector"]
> * [Distribuire un contenitore Windows](service-fabric-deploy-container.md)
> * [Distribuire un contenitore Docker](service-fabric-deploy-container-linux.md)
> 
> 

In questo articolo illustra hello processo di compilazione di servizi nei contenitori in contenitori di Windows.

Service Fabric offre diverse funzionalità che consentono di creare applicazioni costituite da microservizi eseguiti in contenitori. 

funzionalità di Hello includono:

* Distribuzione e attivazione di immagini contenitore
* Governance delle risorse
* Autenticazione nel repository
* Mapping tra porta del contenitore e porta dell'host
* Individuazione e comunicazione da contenitore a contenitore
* Tooconfigure possibilità e impostare le variabili di ambiente

Ecco come funziona ciascuna di funzionalità quando si crea un pacchetto toobe un servizio nei contenitori inclusi nell'applicazione.

## <a name="package-a-windows-container"></a>Creare il pacchetto di un contenitore Windows
Quando si comprime un contenitore, è possibile scegliere toouse un modello di progetto Visual Studio o [creare manualmente il pacchetto di applicazione hello](#manually).  Quando si usa Visual Studio, struttura del pacchetto dell'applicazione hello e i file manifesto vengono creati dal modello di progetto nuovo hello.

> [!TIP]
> toopackage modo più semplice di Hello un'immagine contenitore esistente in un servizio è toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Utilizzare Visual Studio toopackage un'immagine contenitore esistente
Visual Studio fornisce un'infrastruttura a servizio toohelp modello di servizio si distribuisce un cluster di Service Fabric tooa contenitore.

1. Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.
2. Scegliere **contenitore Guest** come modello di servizio hello.
3. Scegliere **nome immagine** e fornire hello percorso toohello immagine nel repository del contenitore. Ad esempio `myrepo/myimage:v1` in https://hub.docker.com
4. Assegnare un nome al servizio e fare clic su **OK**.
5. Se il servizio nei contenitori necessita di un endpoint per la comunicazione, è ora possibile aggiungere hello protocollo, porta e il file ServiceManifest.xml toohello del tipo. ad esempio: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Fornendo hello `UriScheme`, Service Fabric registra automaticamente l'endpoint del contenitore hello con il servizio di denominazione per il rilevamento di hello. porta Hello può essere risolto (come illustrato nell'esempio sopra riportato hello) o allocata dinamicamente. Se non si specifica una porta, viene dinamicamente allocato dall'intervallo di porte applicazione hello (come accade con qualsiasi servizio).
    È inoltre necessario mapping delle porte toohost tooconfigure hello contenitore specificando un `PortBinding` criteri nel manifesto dell'applicazione hello. Per ulteriori informazioni, vedere [configurare il mapping di porta del contenitore toohost](#Portsection).
6. Se per il contenitore è necessaria una governance delle risorse, aggiungere un elemento `ResourceGovernancePolicy`.
8. Se il contenitore deve tooauthenticate con un repository privato, quindi aggiungere `RepositoryCredentials`.
7. Se si esegue in un computer Windows Server 2016 con supporto contenitore abilitato, è possibile utilizzare i pacchetti hello e pubblicare cluster locale tooyour toodeploy di azione. 
8. Quando si è pronti, è possibile pubblicare hello applicazione tooa remota del cluster o archiviare hello soluzione toosource controllo del codice. 

Per un esempio, hello estrazione [esempi di codice di contenitori di Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Creazione di un cluster di Windows Server 2016
toodeploy l'applicazione nei contenitori, è necessario un cluster che esegue Windows Server 2016 con supporto del contenitore abilitato toocreate. Il cluster può essere eseguito localmente o distribuito con Azure Resource Manager in Azure. 

toodeploy un cluster usando Gestione risorse di Azure, scegliere hello **Windows Server 2016 con contenitori** immagine opzione in Azure. Vedere l'articolo hello [creare un cluster di Service Fabric usando Gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md). Assicurarsi di usare hello seguendo le impostazioni di gestione risorse di Azure:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
È inoltre possibile utilizzare hello [modello cinque nodi Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate un cluster. In alternativa è consigliabile leggere un [post di blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) della community sull'uso di Service Fabric e dei contenitori di Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Creare manualmente il pacchetto e distribuire un'immagine del contenitore
il processo di Hello di creare manualmente il pacchetto del servizio nei contenitori si basa su hello alla procedura seguente:

1. Pubblicare hello contenitori tooyour repository.
2. Creare una struttura di directory hello del pacchetto.
3. Modificare i file manifesto del servizio hello.
4. Modificare i file manifesto dell'applicazione hello.

## <a name="deploy-and-activate-a-container-image"></a>Distribuire e attivare un'immagine contenitore
In Service Fabric hello [modello applicativo](service-fabric-application-model.md), un contenitore rappresenta un'applicazione host nel quale servizio più repliche vengono inserite. toodeploy e attivare un contenitore, un nome di hello put dell'immagine contenitore hello in un `ContainerHost` elemento nel manifesto del servizio hello.

Nel manifesto del servizio hello, aggiungere un `ContainerHost` per il punto di ingresso hello. Quindi set hello `ImageName` nome hello toobe del repository del contenitore hello e dell'immagine. Hello manifesto parziale seguente viene illustrato un esempio di come contenitore hello toodeploy chiamata `myimage:v1` da un repository denominato `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

È possibile specificare toorun facoltativo comandi all'avvio il contenitore di hello in hello `Commands` elemento. Per aggiungere più comandi, separarli con virgole. 

## <a name="understand-resource-governance"></a>Informazioni sulla governance delle risorse
Governance delle risorse è possibile utilizzare una funzionalità di contenitore hello che limita le risorse hello hello contenitore nell'host di hello. Hello `ResourceGovernancePolicy`, ed è specificato nel manifesto dell'applicazione hello è toodeclare utilizzati i limiti delle risorse per un pacchetto di codice servizio. È possibile impostare i limiti delle risorse per hello seguenti risorse:

* Memoria
* MemorySwap
* CpuShares (peso relativo CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo BlockIO)

> [!NOTE]
> Il supporto per la definizione di limiti di I/O di blocco specifici, come operazioni di I/O al secondo, BPS in lettura/scrittura e altro, è previsto per una versione futura.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Autenticare un repository
toodownload un contenitore, potrebbe essere repository del contenitore toohello tooprovide credenziali di accesso. Hello credenziali di accesso, specificate nel manifesto dell'applicazione hello, vengono utilizzati toospecify hello le informazioni di accesso o una chiave SSH, per il download di immagine contenitore hello dal repository immagini hello. Hello esempio seguente viene illustrato un account denominato *TestUser* insieme password hello in testo non crittografato (*non* consigliato):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

È consigliabile crittografare la password di hello usando un certificato che ha distribuito toohello macchina.

Hello esempio seguente viene illustrato un account denominato *TestUser*, in cui è stata crittografata utilizzando un certificato denominato password hello *NomeCert*. È possibile utilizzare hello `Invoke-ServiceFabricEncryptText` PowerShell toocreate hello crittografia segreta testo del comando per la password di hello. Per ulteriori informazioni, vedere l'articolo hello [dei dati segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).

chiave privata di Hello del certificato di hello utilizzate password hello toodecrypt deve essere distribuito toohello computer locale in un metodo fuori banda. (In Azure, questo metodo è Azure Resource Manager.) Quindi quando Service Fabric distribuisce computer toohello pacchetto del servizio hello, è possibile decrittografare il segreto hello. Utilizzando la chiave privata hello insieme al nome account hello, quindi l'autenticazione con repository del contenitore hello.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name ="Portsection"></a>Configurare i mapping delle porte toohost contenitore
È possibile configurare toocommunicate di porta usata un host con il contenitore di hello specificando un `PortBinding` nel manifesto dell'applicazione hello. Hello porta mappe hello porta toowhich hello servizio di associazione è in ascolto all'interno di hello contenitore tooa porta host hello.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Configurare individuazione e comunicazione da contenitore a contenitore
È possibile utilizzare hello `PortBinding` elemento toomap un endpoint di porta del contenitore tooan nel manifesto del servizio hello. Nell'esempio seguente di hello, hello endpoint `Endpoint1` specifica una porta fissa, 8905. Non può inoltre specificare alcuna porta, nel qual caso una porta casuale dall'intervallo di porte di applicazione del cluster hello viene scelto per l'utente.


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
Se si specifica un endpoint, utilizzando hello `Endpoint` tag nel manifesto del servizio hello di un contenitore di guest, Service Fabric è possibile pubblicare automaticamente questo toohello endpoint servizio di denominazione. Altri servizi in esecuzione nel cluster hello in questo modo è in grado di individuare questo contenitore utilizzando le query REST hello per la risoluzione.

La registrazione con il servizio di denominazione hello, è possibile eseguire contenitore a comunicazione all'interno del contenitore tramite hello [proxy inverso](service-fabric-reverseproxy.md). La comunicazione viene eseguita, fornendo una porta di attesa di hello proxy inverso http e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente. Per ulteriori informazioni, vedere la sezione successiva di hello. 

## <a name="configure-and-set-environment-variables"></a>Configurare e impostare variabili di ambiente
Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello. Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest. È possibile eseguire l'override di variabile di ambiente, i valori in un'applicazione hello manifesto o specificarli durante la distribuzione come parametri dell'applicazione.

Hello frammento XML del manifesto del servizio seguente viene illustrato un esempio di come le variabili di ambiente toospecify per un pacchetto di codice:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Queste variabili di ambiente possono essere sottoposto a override a livello di manifesto dell'applicazione hello:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Nell'esempio precedente hello è specificato un valore esplicito per hello `HttpGateway` variabile di ambiente (19000), mentre viene impostato il valore di hello per `BackendServiceName` parametro tramite hello `[BackendSvc]` parametro dell'applicazione. Queste impostazioni consentono di valore hello toospecify per `BackendServiceName`valore quando si distribuisce un'applicazione hello e non includere un valore fisso nel manifesto di hello.

## <a name="configure-isolation-mode"></a>Configurare la modalità di isolamento

Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.  In modalità di isolamento hello processo in esecuzione in tutti i contenitori di hello hello stesso host macchina condivisione hello kernel con host hello. Con la modalità di isolamento hello Hyper-V, sono isolate tra ogni contenitore di Hyper-V e host contenitore hello kernel hello. viene specificata la modalità di isolamento Hello in hello `ContainerHostPolicies` tag nel file manifesto dell'applicazione hello.  modalità di isolamento Hello che è possibile specificare sono `process`, `hyperv`, e `default`. Hello `default` modalità di isolamento predefinita troppo`process` in Windows Server ospita e il valore predefinito troppo`hyperv` in host Windows 10.  Hello frammento di codice seguente viene illustrato come specificare la modalità di isolamento hello nel file manifesto dell'applicazione hello.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a>Esempi completi per il manifesto dell'applicazione e del servizio

Di seguito è illustrato un manifesto dell'applicazione di esempio:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Di seguito è riportato un esempio di manifesto del servizio (specificato nella precedente manifesto dell'applicazione hello):

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Passaggi successivi
Dopo aver distribuito un servizio nei contenitori, consultare come toomanage il ciclo di vita leggendo [il ciclo di vita di Service Fabric applicazione](service-fabric-application-lifecycle.md).

* [Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)
* Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).
