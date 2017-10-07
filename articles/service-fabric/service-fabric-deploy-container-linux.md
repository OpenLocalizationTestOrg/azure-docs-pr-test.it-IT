---
title: aaaService dell'infrastruttura e la distribuzione di contenitori di Linux | Documenti Microsoft
description: "Service Fabric e hello uso di applicazioni microservizio toodeploy contenitori di Linux. Questo articolo descrive le funzionalità di hello forniti per i contenitori e come toodeploy immagine di un contenitore di Linux in un cluster di Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Distribuire un tooService contenitore Linux dell'infrastruttura
> [!div class="op_single_selector"]
> * [Distribuire un contenitore Windows](service-fabric-deploy-container.md)
> * [Distribuire un contenitore Linux](service-fabric-deploy-container-linux.md)
>
>

Questo articolo descrive la creazione di servizi in contenitori Docker su Linux.

Service Fabric offre diverse funzionalità relative ai contenitori che consentono di creare applicazioni costituite da microservizi inseriti in contenitori, Questi servizi sono denominati servizi in contenitori.

include funzionalità di Hello;

* Distribuzione e attivazione di immagini contenitore
* Governance delle risorse
* Autenticazione nel repository
* Mapping delle porte toohost porta del contenitore
* Individuazione e comunicazione da contenitore a contenitore
* Tooconfigure possibilità e impostare le variabili di ambiente

## <a name="packaging-a-docker-container-with-yeoman"></a>Creazione del pacchetto di un contenitore Docker con yeoman
Quando il pacchetto di un contenitore in Linux, è possibile scegliere entrambi toouse un modello yeoman o [creare manualmente il pacchetto di applicazione hello](#manually).

Un'applicazione di Service Fabric può contenere uno o più contenitori, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello. Hello Service Fabric SDK per Linux include un [Yeoman](http://yeoman.io/) generatore che rende facile toocreate l'applicazione e aggiungere un'immagine contenitore. Consente di usare Yeoman toocreate chiamata un'applicazione con un singolo contenitore Docker *SimpleContainerApp*. È possibile aggiungere più servizi in un secondo momento modificando i file manifesto hello generato.

## <a name="install-docker-on-your-development-box"></a>Installare Docker nell'ambiente di sviluppo

La seguente esecuzione hello comandi docker tooinstall nella casella di sviluppo di Linux (se si utilizza immagine vagrant hello in OSX, docker è già installato):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Creare un'applicazione hello
1. In un terminale digitare `yo azuresfcontainer`.
2. Assegnare un nome all'applicazione, ad esempio mycontainerap
3. Specificare l'URL di hello per l'immagine del contenitore da un repository DockerHub hello. Hello immagine parametro accetta hello modulo [repository] / [nome immagine]
4. Se hello immagine non ha un punto di ingresso del carico di lavoro definito, quindi è necessario tooexplicitly specificare i comandi di input con un set delimitato da virgole di comandi toorun hello contenitore, in modo che i contenitori di hello in esecuzione dopo l'avvio.

![Generatore Yeoman di Service Fabric per i contenitori][sf-yeoman]

## <a name="deploy-hello-application"></a>Distribuire un'applicazione hello

### <a name="using-xplat-cli"></a>Uso dell'interfaccia della riga di comando di XPlat
Una volta creata l'applicazione hello, è possibile distribuire cluster locale di toohello utilizzando hello CLI di Azure.

1. Connettere il cluster di Service Fabric locale toohello.

    ```bash
    azure servicefabric cluster connect
    ```

2. Hello utilizzare lo script di installazione fornite in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.

    ```bash
    ./install.sh
    ```

3. Aprire un browser e passare tooService Fabric Explorer in http://localhost:19080/Esplora (sostituire localhost con indirizzo IP privato di hello di hello VM se utilizza Vagrant su Mac OS X).
4. Espandere il nodo di applicazioni hello e si noti che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.
5. Utilizza script di disinstallazione hello fornito nell'istanza di applicazione hello toodelete modello hello e annullare la registrazione del tipo di applicazione hello.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Tramite l'interfaccia della riga di comando di Azure 2.0

Vedere il documento di riferimento hello sulla gestione di un [con ciclo di vita dell'applicazione hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Per un'applicazione di esempio, [hello estrazione codice contenitore Service Fabric esempi su GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Aggiunta di ulteriori servizi tooan esistente dell'applicazione

tooadd un altro contenitore del servizio applicazione tooan già creato utilizzando `yo`, eseguire hello alla procedura seguente:

1. Cambiare directory toohello principale di un'applicazione hello esistente.  Ad esempio, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` è un'applicazione hello creata da Yeoman.
2. Eseguire `yo azuresfcontainer:AddService`

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

È possibile specificare i comandi di input specificando hello facoltativo `Commands` elemento con un set delimitato da virgole di comandi toorun hello contenitore.

> [!NOTE]
> Se hello immagine non ha un punto di ingresso del carico di lavoro definito, quindi è necessario tooexplicitly specificare i comandi di input all'interno di `Commands` elemento con un set delimitato da virgole di comandi toorun hello contenitore, in modo che i contenitori di hello in esecuzione avvio.

## <a name="understand-resource-governance"></a>Informazioni sulla governance delle risorse
Governance delle risorse è possibile utilizzare una funzionalità di contenitore hello che limita le risorse hello hello contenitore nell'host di hello. Hello `ResourceGovernancePolicy`, ed è specificato nel manifesto dell'applicazione hello è toodeclare utilizzati i limiti delle risorse per un pacchetto di codice servizio. È possibile impostare i limiti delle risorse per hello seguenti risorse:

* Memoria
* MemorySwap
* CpuShares (peso relativo CPU)
* MemoryReservationInMB  
* BlkioWeight (peso relativo BlockIO)

> [!NOTE]
> In una versione futura sarà incluso il supporto della definizione di specifici limiti di I/O di blocco, come operazioni di I/O al secondo, BPS in lettura/scrittura e altri.
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

## <a name="configure-container-port-to-host-port-mapping"></a>Configurare il mapping tra porta del contenitore e porta dell'host
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
Utilizzando hello `PortBinding` criteri, è possibile mappare una porta del contenitore di tooan `Endpoint` nel manifesto del servizio hello. Hello endpoint `Endpoint1` possibile specificare una porta fissa (ad esempio, la porta 80). Non può inoltre specificare alcuna porta, nel qual caso una porta casuale dall'intervallo di porte di applicazione del cluster hello viene scelto per l'utente.

Se si specifica un endpoint, utilizzando hello `Endpoint` tag nel manifesto del servizio hello di un contenitore di guest, Service Fabric è possibile pubblicare automaticamente questo toohello endpoint servizio di denominazione. Altri servizi in esecuzione nel cluster hello in questo modo è in grado di individuare questo contenitore utilizzando le query REST hello per la risoluzione.

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

La registrazione con il servizio di denominazione hello, è possibile utilizzare comunicazione di contenitore a nel codice hello all'interno del contenitore tramite hello [proxy inverso](service-fabric-reverseproxy.md). La comunicazione viene eseguita, fornendo una porta di attesa di hello proxy inverso http e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente. Per ulteriori informazioni, vedere la sezione successiva di hello.

## <a name="configure-and-set-environment-variables"></a>Configurare e impostare variabili di ambiente
Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello, sia per i servizi che vengono distribuiti in contenitori o per i servizi che vengono distribuiti i file eseguibili di processi/guest. Questi valori di variabile di ambiente possono essere sottoposto a override in modo specifico nel manifesto dell'applicazione hello o specificati durante la distribuzione come parametri dell'applicazione.

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
* [L'interazione con i cluster di Service Fabric usando hello CLI di Azure](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Articoli correlati

* [Introduzione a Service Fabric e all'interfaccia della riga di comando di Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Introduzione all'interfaccia della riga di comando di XPlat per Service Fabric](service-fabric-azure-cli.md)
