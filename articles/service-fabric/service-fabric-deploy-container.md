---
title: Service Fabric e distribuzione di contenitori | Microsoft Docs
description: "Service Fabric e l'uso di contenitori per la distribuzione di applicazioni di microservizi. Questo articolo illustra le funzionalità offerte da Service Fabric per i contenitori e la modalità di distribuzione di un'immagine contenitore Windows in un cluster."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a>Distribuire un contenitore Windows in Service Fabric
> [!div class="op_single_selector"]
> * [Distribuire un contenitore Windows](service-fabric-deploy-container.md)
> * [Distribuire un contenitore Docker](service-fabric-deploy-container-linux.md)
> 
> 

Questo articolo descrive in dettaglio il processo di creazione di servizi in contenitori Windows.

Service Fabric offre diverse funzionalità che consentono di creare applicazioni costituite da microservizi eseguiti in contenitori. 

Le funzionalità includono:

* Distribuzione e attivazione di immagini contenitore
* Governance delle risorse
* Autenticazione nel repository
* Mapping tra porta del contenitore e porta dell'host
* Individuazione e comunicazione da contenitore a contenitore
* Possibilità di configurare e impostare variabili di ambiente

Verranno ora esaminate le singole funzionalità coinvolte nella creazione del pacchetto di un servizio in contenitori da includere nell'applicazione.

## <a name="package-a-windows-container"></a>Creare il pacchetto di un contenitore Windows
Quando si crea il pacchetto di un contenitore, si può scegliere di usare un modello di progetto di Visual Studio oppure di [creare manualmente il pacchetto dell'applicazione](#manually).  Se si usa Visual Studio, la struttura del pacchetto dell'applicazione e i file manifesto vengono creati automaticamente dal modello Nuovo progetto.

> [!TIP]
> Il modo più semplice per creare il pacchetto di un'immagine contenitore esistente in un servizio consiste nell'usare Visual Studio.

## <a name="use-visual-studio-to-package-an-existing-container-image"></a>Usare Visual Studio per creare il pacchetto di un'immagine contenitore esistente
Visual Studio include un modello di servizio Service Fabric che consente di distribuire un contenitore in un cluster di Service Fabric.

1. Scegliere **File** > **Nuovo progetto** e creare un'applicazione di Service Fabric.
2. Scegliere **Guest Container (Contenitore guest)** come modello del servizio.
3. Scegliere **Nome immagine** e specificare il percorso dell'immagine nell'archivio del contenitore. Ad esempio `myrepo/myimage:v1` in https://hub.docker.com
4. Assegnare un nome al servizio e fare clic su **OK**.
5. Se il servizio nel contenitore richiede un endpoint per la comunicazione, è ora possibile aggiungere il protocollo, la porta e il tipo al file ServiceManifest.xml. ad esempio: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Se si specifica `UriScheme` Service Fabric registra automaticamente l'endpoint del contenitore con Naming Service per l'individuazione. La porta può essere fissa (come nell'esempio precedente) o allocata in modo dinamico. Se non si specifica una porta, questa viene allocata in modo dinamico nell'intervallo di porte dell'applicazione (come per qualsiasi servizio).
    È anche necessario configurare il mapping tra contenitore e porta dell'host specificando una norma `PortBinding` nel manifesto dell'applicazione. Per altre informazioni, vedere [Configurare il mapping tra porta del contenitore e porta dell'host](#Portsection).
6. Se per il contenitore è necessaria una governance delle risorse, aggiungere un elemento `ResourceGovernancePolicy`.
8. Se il contenitore deve eseguire l'autenticazione con un repository privato, aggiungere `RepositoryCredentials`.
7. Se si usa un computer Windows Server 2016 con il supporto dei contenitori abilitato è possibile usare l'azione di creazione pacchetto e pubblicazione per la distribuzione nel cluster locale. 
8. Quando si è pronti, pubblicare l'applicazione in un cluster remoto o archiviare la soluzione nel controllo del codice sorgente. 

Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).

## <a name="creating-a-windows-server-2016-cluster"></a>Creazione di un cluster di Windows Server 2016
Per distribuire l'applicazione nei contenitori, è necessario creare un cluster che esegue Windows Server 2016 con il supporto di contenitore abilitato. Il cluster può essere eseguito localmente o distribuito con Azure Resource Manager in Azure. 

Per distribuire un cluster con Azure Resource Manager scegliere l'opzione di immagine **Windows Server 2016 with Containers** (Windows Server 2016 con contenitori) in Azure. Vedere l'articolo [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Assicurarsi di usare le seguenti impostazioni di Azure Resource Manager:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
Per creare un cluster è anche possibile usare il [modello di Azure Resource Manager con cinque nodi](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype). In alternativa è consigliabile leggere un [post di blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) della community sull'uso di Service Fabric e dei contenitori di Windows.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Creare manualmente il pacchetto e distribuire un'immagine del contenitore
Il processo per creare manualmente il pacchetto di un servizio in contenitore prevede i passaggi seguenti:

1. Pubblicare i contenitori nel repository.
2. Creare la struttura di directory del pacchetto.
3. Modificare il file manifesto del servizio.
4. Modificare il file manifesto dell’applicazione.

## <a name="deploy-and-activate-a-container-image"></a>Distribuire e attivare un'immagine contenitore
Nel [modello applicativo](service-fabric-application-model.md)di Service Fabric, un contenitore rappresenta un host applicazione in cui sono inserite più repliche dei servizi. Per distribuire e attivare un contenitore, inserire il nome dell'immagine contenitore in un elemento `ContainerHost` nel manifesto del servizio.

Nel manifesto del servizio aggiungere un `ContainerHost` per il punto di ingresso. Impostare quindi il nome dell'immagine e del repository del contenitore in `ImageName`. Il manifesto parziale seguente mostra un esempio di come distribuire il contenitore denominato `myimage:v1` da un repository denominato `myrepo`:

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

È possibile specificare i comandi facoltativi da eseguire all'avvio del contenitore all'interno dell'elemento `Commands`. Per aggiungere più comandi, separarli con virgole. 

## <a name="understand-resource-governance"></a>Informazioni sulla governance delle risorse
La governance delle risorse è una funzionalità del contenitore che limita le risorse che possono essere usate dal contenitore nell'host. L'impostazione `ResourceGovernancePolicy`, specificata nel manifesto dell'applicazione, viene usata per dichiarare limiti di risorse per il pacchetto di codice di un servizio. È possibile impostare limiti per le risorse seguenti:

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
Per scaricare un contenitore potrebbe essere necessario specificare credenziali di accesso per il relativo repository. Le credenziali di accesso, specificate nel manifesto dell'applicazione, vengono usate per specificare le informazioni di accesso o la chiave SSH per scaricare l'immagine contenitore dal repository delle immagini. L'esempio seguente illustra un account denominato *TestUser* con password non crittografata (scenario *non* consigliato):

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

È consigliabile crittografare la password con un certificato distribuito nel computer.

L'esempio seguente illustra un account denominato *TestUser* con password crittografata con un certificato denominato *MyCert*. È possibile usare il comando `Invoke-ServiceFabricEncryptText` di PowerShell per creare il testo crittografato segreto per la password. Per altre informazioni, vedere [Gestione dei segreti nelle applicazioni di Service Fabric](service-fabric-application-secret-management.md).

La chiave privata del certificato usata per decrittografare la password deve essere distribuita nel computer locale con un metodo fuori banda. (In Azure, questo metodo è Azure Resource Manager.) Quando Service Fabric distribuisce il pacchetto del servizio nel computer, potrà quindi decrittografare il segreto. Usando il segreto insieme al nome dell'account, potrà quindi eseguire l'autenticazione nel repository del contenitore.

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

## <a name ="Portsection"></a> Configurare il mapping tra contenitore e porta dell'host
È possibile configurare una porta dell'host per la comunicazione con il contenitore specificando `PortBinding` nel manifesto dell'applicazione. Il binding di porta esegue il mapping tra la porta su cui il servizio è in ascolto all'interno del contenitore e una porta nell'host.

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
È possibile usare l'elemento `PortBinding` per eseguire il mapping di una porta del contenitore a un endpoint nel manifesto del servizio. Nell'esempio seguente l'endpoint `Endpoint1` specifica la porta fissa 8905. oppure non specificarne alcuna. Nel secondo caso verrà scelta automaticamente una porta casuale nell'intervallo di porte dell'applicazione del cluster.


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
Se si specifica un endpoint, usando il tag `Endpoint` nel manifesto del servizio di un contenitore guest, Service Fabric può pubblicare automaticamente questo endpoint per Naming Service. Altri servizi in esecuzione nel cluster possono così individuare questo contenitore usando query REST per la risoluzione.

Eseguendo la registrazione in Naming Service è possibile implementare la comunicazione tra contenitori all'interno del contenitore usando il [proxy inverso](service-fabric-reverseproxy.md). La comunicazione avviene specificando la porta di ascolto HTTP del proxy inverso e il nome dei servizi con cui si vuole comunicare come variabili di ambiente. Per altre informazioni, vedere la sezione seguente. 

## <a name="configure-and-set-environment-variables"></a>Configurare e impostare variabili di ambiente
È possibile specificare variabili di ambiente per ogni pacchetto di codice nel manifesto del servizio. Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest. È possibile sostituire i valori delle variabili di ambiente nel manifesto dell'applicazione oppure specificarli durante la distribuzione come parametri dell'applicazione.

Il frammento XML del manifesto del servizio seguente offre un esempio di come specificare le variabili di ambiente per un pacchetto di codice:

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

È possibile eseguire l'override di queste variabili di ambiente a livello di manifesto dell'applicazione:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Nell'esempio precedente è stato specificato un valore esplicito per la variabile di ambiente `HttpGateway` (19000), mentre il valore per il parametro `BackendServiceName` viene impostato tramite il parametro dell'applicazione `[BackendSvc]`. Queste impostazioni consentono di specificare il valore per `BackendServiceName` quando si distribuisce l'applicazione anziché avere un valore fisso nel manifesto.

## <a name="configure-isolation-mode"></a>Configurare la modalità di isolamento

Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V.  Nella modalità di isolamento del processo tutti i contenitori in esecuzione nello stesso computer host condividono il kernel con l'host. Nella modalità di isolamento Hyper-V i kernel sono isolati tra i singoli contenitori Hyper-V e il contenitore host. La modalità di isolamento è specificata nel tag `ContainerHostPolicies` nel file manifesto dell'applicazione.  Le modalità di isolamento specificabili sono `process`, `hyperv` e `default`. La modalità di isolamento `default` assume come impostazione predefinita `process` negli host Windows Server e `hyperv` negli host Windows 10.  Il frammento seguente indica come è specificata la modalità di isolamento nel file manifesto dell'applicazione.

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

Di seguito è riportato un manifesto del servizio di esempio (specificato nel manifesto dell'applicazione precedente):

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
Ora che è stato distribuito un servizio in contenitori, vedere [Ciclo di vita dell'applicazione Service Fabric](service-fabric-application-lifecycle.md) per informazioni su come gestire il ciclo di vita del servizio.

* [Panoramica di Service Fabric e contenitori](service-fabric-containers-overview.md)
* Per un esempio vedere gli [esempi di codice di contenitore Service Fabric su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).
