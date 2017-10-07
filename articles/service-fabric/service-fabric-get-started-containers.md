---
title: un'applicazione contenitore di Azure Service Fabric aaaCreate | Documenti Microsoft
description: Creare la prima applicazione contenitore Windows in Azure Service Fabric.  Creazione di un'immagine di Docker con un'applicazione Python, eseguire il push del Registro di sistema di hello immagine tooa contenitore, compilare e distribuire un'applicazione contenitore di Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Creare la prima applicazione contenitore di Service Fabric in Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Esecuzione di un'applicazione esistente in un contenitore di Windows in un cluster di Service Fabric non richiede tutte le applicazioni tooyour le modifiche. Questo articolo vengono illustrati la creazione di un'immagine Docker che contiene un Python [pallone](http://flask.pocoo.org/) distribuzione di cluster di Service Fabric tooa e l'applicazione web.  Si condividerà anche l'applicazione in contenitore tramite [Registro contenitori di Azure](/azure/container-registry/).  L'articolo presuppone una conoscenza di base di Docker. Per informazioni su Docker, lettura hello [Panoramica Docker](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Prerequisiti
Un computer di sviluppo che esegue:
* Visual Studio 2015 o Visual Studio 2017.
* [SDK e strumenti di Service Fabric](service-fabric-get-started.md).
*  Docker per Windows.  [Scaricare Docker CE per Windows (stabile)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Dopo l'installazione e l'avvio di Docker, fare doppio clic sull'icona dell'area di notifica hello e selezionare **passare contenitori tooWindows**. Si tratta di immagini Docker toorun obbligatorio basate su Windows.

Un cluster di Windows con tre o più nodi in esecuzione in Windows Server 2016 con Contenitori. A questo scopo, [creare un cluster](service-fabric-cluster-creation-via-portal.md) o [provare Service Fabric gratuitamente](https://aka.ms/tryservicefabric).

Un registro all'interno del registro contenitori di Azure. A questo scopo, [creare un registro contenitori](../container-registry/container-registry-get-started-portal.md) nella sottoscrizione di Azure.

## <a name="define-hello-docker-container"></a>Definire contenitore Docker hello
Creare un'immagine basata su hello [immagine Python](https://hub.docker.com/_/python/) si trova nell'Hub Docker.

Definire il contenitore Docker in un Dockerfile. Hello Dockerfile contiene istruzioni per l'impostazione di ambiente hello all'interno del contenitore, il caricamento di un'applicazione hello desiderato toorun e il mapping delle porte. Hello Dockerfile è hello input toohello `docker build` comando che crea l'immagine di hello.

Creare una directory vuota e creare file hello *Dockerfile* (con alcuna estensione di file). Aggiungere il seguente troppo di hello*Dockerfile* e salvare le modifiche:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Hello lettura [riferimento a Dockerfile](https://docs.docker.com/engine/reference/builder/) per ulteriori informazioni.

## <a name="create-a-simple-web-application"></a>Creare un'applicazione Web semplice
Creare un'applicazione Web Flask in ascolto sulla porta 80 che restituisce "Hello World!".  Nella stessa directory di hello, creare file hello *requirements.txt*.  Aggiungere il seguente hello e salvare le modifiche:
```
Flask
```

Creare anche hello *app.py* file e aggiungere hello seguenti:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Creazione immagine hello
Eseguire hello `docker build` toocreate hello comando che esegue l'applicazione web. Aprire una finestra di PowerShell e passare toohello directory contenente hello Dockerfile. Eseguire hello comando seguente:

```
docker build -t helloworldapp .
```

Questo comando compilazioni hello nuova immagine con hello istruzioni del Dockerfile, denominazione (-t tag) immagine hello "helloworldapp". La creazione di un'immagine effettua il pull immagine di base hello verso il basso dall'Hub Docker e crea una nuova immagine che consente di aggiungere l'applicazione sopra l'immagine di base hello.  

Al termine del comando di compilazione hello, eseguire hello `docker images` informazioni toosee hello nuova immagine di comando:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Eseguire un'applicazione hello in locale
Verificare l'immagine localmente prima di pubblicarlo del Registro di sistema di hello contenitore.  

Eseguire un'applicazione hello:

```
docker run -d --name my-web-site helloworldapp
```

*nome* offre un toohello nome contenitore (invece di ID di contenitore hello) di esecuzione.

Una volta avviata contenitore hello, trovarne l'indirizzo IP in modo che sia possibile connettersi tooyour esecuzione contenitore da un browser:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Connettersi toohello esecuzione contenitore.  Aprire un web browser che punta toohello l'indirizzo IP restituito, ad esempio "http://172.31.194.61". Dovrebbe essere hello titolo "Hello World!" visualizzare nel browser hello.

toostop nel contenitore, eseguire:

```
docker stop my-web-site
```

Eliminare il contenitore di hello dal computer di sviluppo:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Eseguire il push del Registro di sistema di hello immagine toohello contenitore
Dopo aver verificato che il contenitore hello viene eseguito nel computer di sviluppo, eseguire il push del Registro di sistema di hello immagine tooyour nel Registro di sistema contenitore di Azure.

Eseguire ``docker login`` toolog nel Registro di sistema tooyour contenitore con il [le credenziali del Registro di sistema](../container-registry/container-registry-authentication.md).

Hello seguente esempio passa hello ID e la password di Azure Active Directory [dell'entità servizio](../active-directory/active-directory-application-objects.md). Ad esempio, è stato assegnato un registro di sistema tooyour dell'entità servizio per uno scenario di automazione. In alternativa, è possibile eseguire l'accesso usando il nome utente e la password del registro.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hello seguente comando crea un tag o l'alias dell'immagine di hello, con un registro di sistema tooyour il percorso completo. In questo esempio posizioni hello immagine hello ```samples``` disordine tooavoid dello spazio dei nomi nella directory radice del Registro di sistema hello hello.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Push del Registro di sistema di hello immagine tooyour contenitore:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Creare il servizio contenitore hello in Visual Studio
Hello Service Fabric SDK e strumenti di forniscono un toohelp modello di servizio si crea un'applicazione nei contenitori.

1. Avviare Visual Studio.  Selezionare **File** > **Nuovo** > **Progetto**.
2. Selezionare l'**applicazione di Service Fabric**, denominarla "MyFirstContainer" e fare clic su **OK**.
3. Selezionare **contenitore Guest** elenco hello di **i modelli di servizio**.
4. In **nome immagine** immettere "myregistry.azurecr.io/samples/helloworldapp", immagine hello è inserito tooyour repository del contenitore.
5. Assegnare un nome al servizio e fare clic su **OK**.

## <a name="configure-communication"></a>Configurare la comunicazione
servizio Hello contenitore è necessario un endpoint per la comunicazione. Aggiungere un `Endpoint` elemento con hello protocollo, porta e il file ServiceManifest.xml toohello del tipo. Per questo articolo, il servizio contenitore hello in ascolto sulla porta 8081.  In questo esempio viene usata una porta fissa 8081.  Se viene specificata alcuna porta, viene scelta una porta casuale dall'intervallo di porte applicazione hello.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

La definizione di un endpoint di Service Fabric pubblica hello toohello di endpoint del servizio di denominazione.  Altri servizi in esecuzione nel cluster hello è possono risolvere questo contenitore.  È inoltre possibile eseguire la comunicazione di contenitore a utilizzando hello [proxy inverso](service-fabric-reverseproxy.md).  La comunicazione viene eseguita, fornendo una porta di attesa di proxy inverso HTTP hello e il nome di hello dei servizi di hello che si desidera toocommunicate con come variabili di ambiente.

## <a name="configure-and-set-environment-variables"></a>Configurare e impostare variabili di ambiente
Le variabili di ambiente possono essere specificate per ogni pacchetto di codice nel manifesto del servizio hello. Questa funzionalità è disponibile per tutti i servizi, siano essi distribuiti come contenitori, processi o eseguibili guest. È possibile eseguire l'override di variabile di ambiente, i valori in un'applicazione hello manifesto o specificarli durante la distribuzione come parametri dell'applicazione.

Hello frammento XML del manifesto del servizio seguente viene illustrato un esempio di come le variabili di ambiente toospecify per un pacchetto di codice:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Queste variabili di ambiente possono essere sottoposto a override nel manifesto dell'applicazione hello:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Configurare il mapping tra porta del contenitore e porta dell'host e l'individuazione da contenitore a contenitore
Configurare toocommunicate di porta usata un host con il contenitore di hello. binding porta Hello esegue il mapping di porta hello su quale hello servizio è in attesa all'interno di hello contenitore tooa porta host hello. Aggiungere un `PortBinding` elemento `ContainerHostPolicies` elemento del file ApplicationManifest.xml hello.  Per questo articolo, `ContainerPort` è 80 (contenitore hello espone la porta 80, come specificato in hello Dockerfile) e `EndpointRef` è "Guest1TypeEndpoint" (hello endpoint definiti in precedenza nel manifesto del servizio hello).  Le richieste in ingresso toohello servizio sulla porta 8081 siano mappati tooport 80 sul contenitore hello.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Configurare l'autenticazione del registro contenitori
Configurare l'autenticazione di contenitore del Registro di sistema aggiungendo `RepositoryCredentials` troppo`ContainerHostPolicies` di file ApplicationManifest XML hello. Aggiungere account hello e una password per hello myregistry.azurecr.io contenitore del Registro di sistema, che consente l'immagine contenitore dal repository hello hello servizio toodownload hello.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

È consigliabile crittografare la password di repository hello usando un certificato di crittografia che ha distribuito tooall i nodi del cluster di hello. Quando Service Fabric distribuisce hello il pacchetto toohello cluster, il certificato di crittografia hello è di testo crittografato hello toodecrypt utilizzato.  cmdlet Invoke-ServiceFabricEncryptText Hello è testo crittografato hello di toocreate utilizzato per la password di hello, che viene aggiunto toohello file ApplicationManifest XML.

Hello lo script seguente crea un nuovo certificato autofirmato e li Esporta in file PFX tooa.  certificato di Hello viene importato in un insieme di credenziali chiave esistente e quindi distribuiti toohello cluster di Service Fabric.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Crittografare la password di hello utilizzando hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Sostituire hello password con testo crittografato hello restituito da hello [Invoke ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet e impostare `PasswordEncrypted` troppo "true".

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Configurare la modalità di isolamento
Windows supporta due modalità di isolamento per i contenitori: la modalità processo e la modalità Hyper-V. In modalità di isolamento hello processo in esecuzione in tutti i contenitori di hello hello stesso host macchina condivisione hello kernel con host hello. Con la modalità di isolamento hello Hyper-V, sono isolate tra ogni contenitore di Hyper-V e host contenitore hello kernel hello. viene specificata la modalità di isolamento Hello in hello `ContainerHostPolicies` elemento nel file manifesto dell'applicazione hello. modalità di isolamento Hello che è possibile specificare sono `process`, `hyperv`, e `default`. modalità di isolamento predefinita Hello predefinite troppo`process` in Windows Server ospita e il valore predefinito troppo`hyperv` in host Windows 10. Hello frammento di codice seguente viene illustrato come specificare la modalità di isolamento hello nel file manifesto dell'applicazione hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Configurare la governance delle risorse
[Governance delle risorse](service-fabric-resource-governance.md) limita le risorse che hello contenitore è possono utilizzare nell'host di hello hello. Hello `ResourceGovernancePolicy` elemento che è specificato nel manifesto dell'applicazione hello, viene utilizzato toodeclare i limiti delle risorse per un pacchetto di codice del servizio. I limiti delle risorse possono essere impostati per hello seguenti risorse: memoria, MemorySwap, CpuShares (peso relativo della CPU), MemoryReservationInMB, BlkioWeight (peso relativo BlockIO).  In questo esempio, il pacchetto di servizio Guest1Pkg Ottiene un core nei nodi del cluster hello in cui viene inserito.  I limiti di memoria sono assoluti, pertanto il pacchetto di codice hello è limitato too1024 MB di memoria (e una prenotazione soft garanzia di hello stesso). Pacchetti di codice (contenitori o processi) non sono in grado di tooallocate più memoria rispetto a questo limite e il tentativo di toodo operazione genera un'eccezione di memoria insufficiente. Per risorse limite imposizione toowork, tutti i pacchetti di codice all'interno di un pacchetto del servizio devono avere i limiti di memoria specificati.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Distribuire un'applicazione contenitore hello
Salvare tutte le modifiche e compilare un'applicazione hello. toopublish l'applicazione, il pulsante destro del mouse su **MyFirstContainer** in Esplora soluzioni e selezionare **pubblica**.

In **Endpoint della connessione**, immettere l'endpoint di gestione di hello per cluster hello.  ad esempio "containercluster.westus2.cloudapp.azure.com:19000". È possibile trovare una connessione client hello endpoint nel pannello della panoramica hello per il cluster in hello [portale di Azure](https://portal.azure.com).

Fare clic su **Pubblica**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) è uno strumento basato sul Web che permette di analizzare e gestire applicazioni e nodi in un cluster di Service Fabric. Aprire un browser e passare toohttp://containercluster.westus2.cloudapp.azure.com:19080 Esplora/e seguono la distribuzione di applicazioni hello.  un'applicazione Hello distribuisce ma non sono in stato di errore finché hello immagine viene scaricata nei nodi del cluster hello (che possono richiedere tempo, a seconda delle dimensioni dell'immagine hello): ![errore][1]

un'applicazione Hello è pronta quando è in ```Ready``` stato: ![pronto][2]

Aprire un browser e passare toohttp://containercluster.westus2.cloudapp.azure.com:8081. Dovrebbe essere hello titolo "Hello World!" visualizzare nel browser hello.

## <a name="clean-up"></a>Eseguire la pulizia
Continuare tooincur addebiti mentre hello cluster è in esecuzione, provare a [l'eliminazione del cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  I [party cluster](http://tryazureservicefabric.westus.cloudapp.azure.com/) vengono eliminati automaticamente dopo alcune ore.

Dopo che si esegue il push del Registro di sistema di hello immagine toohello contenitore è possibile eliminare l'immagine locale hello dal computer di sviluppo:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Manifesti di esempio completi del servizio e dell'applicazione di Service Fabric
Ecco completa del servizio hello e i manifesti dell'applicazione utilizzate in questo articolo.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>Configurare l'intervallo di tempo prima della terminazione forzata del contenitore

È possibile configurare un intervallo di tempo per hello runtime toowait prima contenitore hello viene rimosso dopo hello eliminazione servizio (o un nodo di spostamento tooanother) è stata avviata. Intervallo di tempo hello configurazione invia hello `docker stop <time in seconds>` contenitore toohello di comando.   Per altri dettagli, vedere [docker stop](https://docs.docker.com/engine/reference/commandline/stop/). toowait intervallo di tempo Hello viene specificato sotto hello `Hosting` sezione. Hello seguente frammento di codice del manifesto del cluster viene illustrato come intervallo di attesa tooset hello:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Hello intervallo di tempo predefinito è impostato too10 secondi. Poiché questa configurazione è dinamica, una configurazione aggiornare solo in caso di timeout hello aggiornamenti cluster hello. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Configurare hello runtime tooremove immagini contenitore inutilizzati

È possibile configurare hello Service Fabric cluster tooremove immagini contenitore inutilizzati dal nodo hello. Questa configurazione consente toobe di spazio su disco liberare se sono presenti nel nodo hello troppi immagini contenitore.  tooenable questa funzionalità, l'aggiornamento hello `Hosting` sezione manifesto del cluster hello come illustrato nel seguente frammento di codice hello: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Per le immagini che non devono essere eliminate, è possibile specificarle in hello `ContainerImagesToSkip` parametro. 



## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull'esecuzione di [contenitori in Service Fabric](service-fabric-containers-overview.md).
* Hello lettura [distribuire un'applicazione .NET in un contenitore](service-fabric-host-app-in-a-container.md) esercitazione.
* Informazioni su Service Fabric hello [del ciclo di vita dell'applicazione](service-fabric-application-lifecycle.md).
* Hello estrazione [esempi di codice di Service Fabric contenitore](https://github.com/Azure-Samples/service-fabric-dotnet-containers) su GitHub.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
