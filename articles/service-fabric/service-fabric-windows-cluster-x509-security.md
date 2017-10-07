---
title: aaaSecure un'infrastruttura di Azure del servizio cluster in Windows tramite i certificati | Documenti Microsoft
description: "In questo articolo viene descritto come toosecure comunicazione all'interno di hello autonomo o privato cluster nonché tra client e i cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Proteggere un cluster autonomo in Windows con certificati X.509
In questo articolo viene descritto come toosecure hello comunicazione hello vari nodi del cluster di Windows autonoma, nonché il modo tooauthenticate client che si connettono toothis cluster, utilizzando i certificati x. 509. Ciò garantisce che solo gli utenti autorizzati possono accedere cluster hello, hello applicazioni distribuite e attività di gestione.  Sicurezza di certificato deve essere abilitata nel cluster hello quando viene creato il cluster hello.  

Per altre informazioni sulla sicurezza del cluster da nodo a nodo e da client a nodo e sul controllo degli accessi in base al ruolo, vedere [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Certificati necessari
toostart, [download del pacchetto del cluster autonomo hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone dei nodi di hello del cluster. In hello scaricato pacchetto, si noterà un **ClusterConfig.X509.MultiMachine.json** file. Aprire il file hello e sezione hello **sicurezza** in hello **proprietà** sezione:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

In questa sezione illustra i certificati di hello che è necessario per proteggere il cluster di Windows autonoma. Se si specifica un certificato del cluster, impostare il valore di hello di **ClusterCredentialType** too_**X509**_. Se si specifica il certificato server per le connessioni esterne, impostare hello **ServerCredentialType** troppo_**X509**_. Sebbene non obbligatorio, è consigliabile toohave entrambi questi certificati per un cluster protetto correttamente. Se si imposta questi valori troppo*X509* è necessario specificare anche hello certificati corrispondenti o Service Fabric genererà un'eccezione. In alcuni scenari, può essere solo hello toospecify _ClientCertificateThumbprints_ o _ReverseProxyCertificate_. In tali scenari, non è necessario impostare _ClusterCredentialType_ o _ServerCredentialType_ too_X509_.


> [!NOTE]
> Oggetto [identificazione personale](https://en.wikipedia.org/wiki/Public_key_fingerprint) hello identità primaria di un certificato. Lettura [come tooretrieve identificazione personale di un certificato](https://msdn.microsoft.com/library/ms734695.aspx) toofind all'identificazione personale hello di hello che i certificati creati.
> 
> 

Hello nella tabella seguente elenca i certificati di hello che sarà necessario nel programma di installazione del cluster:

| **CertificateInformation Setting** | **Descrizione** |
| --- | --- |
| ClusterCertificate |Consigliato per l'ambiente di test. Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster. È possibile usare due diversi certificati, uno primario e uno secondario per l'aggiornamento. Impostare l'identificazione personale hello del certificato primario hello in hello **identificazione personale** sezione e quello di hello secondario nel hello **ThumbprintSecondary** variabili. |
| ClusterCertificateCommonNames |Consigliato per l'ambiente di produzione. Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster. È possibile usare uno o due nomi comuni del certificato del cluster. |
| ServerCertificate |Consigliato per l'ambiente di test. Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster. Per praticità, è possibile scegliere toouse hello stesso certificato per *ClusterCertificate* e *ServerCertificate*. È possibile usare due diversi certificati del server, uno primario e uno secondario per l'aggiornamento. Impostare l'identificazione personale hello del certificato primario hello in hello **identificazione personale** sezione e quello di hello secondario nel hello **ThumbprintSecondary** variabili. |
| ServerCertificateCommonNames |Consigliato per l'ambiente di produzione. Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster. Per praticità, è possibile scegliere toouse hello stesso certificato per *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*. È possibile usare uno o due nomi comuni del certificato del server. |
| ClientCertificateThumbprints |Si tratta di un set di certificati che si desidera tooinstall nei client hello autenticato. Si può avere un numero diverso di certificati di client installati in computer hello che si desidera che tooallow accesso toohello cluster. Impostare l'identificazione personale hello di ogni certificato in hello **CertificateThumbprint** variabile. Se si imposta hello **IsAdmin** troppo*true*, quindi client hello con il certificato installato può eseguire amministratore attività di gestione in cluster hello. Se hello **IsAdmin** è *false*, client hello con questo certificato può eseguire solo azioni hello consentite per i diritti di accesso utente, in genere di sola lettura. Per altre informazioni sui ruoli, vedere [Controllo degli accessi in base al ruolo (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Set hello nome comune del certificato client prima di hello hello **CertificateCommonName**. Hello **CertificateIssuerThumbprint** è l'identificazione personale hello per emittente hello del certificato. Lettura [utilizzo dei certificati](https://msdn.microsoft.com/library/ms731899.aspx) tooknow informazioni sui nomi comuni e dell'autorità emittente hello. |
| ReverseProxyCertificate |Consigliato per l'ambiente di test. Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](service-fabric-reverseproxy.md). Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes. |
| ReverseProxyCertificateCommonNames |Consigliato per l'ambiente di produzione. Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](service-fabric-reverseproxy.md). Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes. |

Di seguito è esempio di configurazione di cluster in cui sono stati forniti i certificati Client, Server e Cluster hello. Si noti che per cluster / server / reverseProxy certificati, l'identificazione personale e nome comune non sono consentiti toobe configurati insieme per hello stesso tipo di certificato.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Rollover del certificato
Quando si usa il nome comune del certificato al posto dell'identificazione personale, il rollover del certificato non richiede l'aggiornamento della configurazione del cluster.
Se prevede di rollover certificato dell'autorità di certificazione continuata, tenere il certificato dell'autorità di certificazione precedente di hello nell'archivio cert hello almeno 2 ore dopo l'installazione del certificato dell'autorità di certificazione nuovo hello.

## <a name="acquire-hello-x509-certificates"></a>Acquisire i certificati x. 509 hello
comunicazione toosecure all'interno di cluster hello, è necessario innanzitutto i certificati x. 509 tooobtain per i nodi del cluster. Inoltre, toolimit connessione toothis cluster tooauthorized macchine/gli utenti, sarà anche necessario tooobtain e installare i certificati per i computer client hello.

Per i cluster che eseguono carichi di lavoro di produzione, è necessario utilizzare un [autorità di certificazione (CA)](https://en.wikipedia.org/wiki/Certificate_authority) firmato cluster hello toosecure di certificato x. 509. Per informazioni dettagliate su come ottenere questi certificati, vedere troppo[procedura: ottenere un certificato](http://msdn.microsoft.com/library/aa702761.aspx).

Per i cluster che si usa per scopi di test, è possibile scegliere un certificato autofirmato toouse.

## <a name="optional-create-a-self-signed-certificate"></a>Facoltativo: creare un certificato autofirmato
Un modo toocreate un certificato autofirmato che può essere protetta correttamente è hello toouse *CertSetup.ps1* script nella cartella di Service Fabric SDK hello nella directory di hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Modificare questo nome di file toochange hello predefinito del certificato hello (cercare il valore di hello *CN = ServiceFabricDevClusterCert*). Eseguire questo script come `.\CertSetup.ps1 -Install`.

Ora, esportare file di hello certificato tooa PFX con una password protetta. Ottenere innanzitutto l'identificazione personale hello del certificato di hello. Da hello *avviare* menu, eseguire hello *gestire i certificati del computer*. Passare toohello **locale\Personale.** cartella e individuare hello certificato appena creato. Fare doppio clic su tooopen certificato hello è hello seleziona *dettagli* scheda e scorrere verso il basso toohello *identificazione personale* campo. Copiare il valore di identificazione personale hello nel comando di PowerShell hello seguito, dopo aver rimosso gli spazi hello.  Hello modifica `String` valore tooa password sicura adatto tooprotect e hello esecuzione seguente in PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

toosee hello dettagli di un certificato installato hello del computer è possibile eseguire il comando PowerShell seguente hello:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

In alternativa, se si dispone di una sottoscrizione di Azure, attenersi alla sezione hello [aggiungere certificati tooKey insieme di credenziali](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Installare i certificati di hello
Dopo aver creato uno o più certificati, è possibile installare nei nodi del cluster hello. I nodi devono toohave hello più recente di Windows PowerShell 3. x installati su di essi. Sarà necessario toorepeat questi passaggi in ogni nodo, per i certificati di Cluster sia del Server e i certificati secondari.

1. Nodo di toohello file con estensione pfx hello copia.
2. Aprire una finestra di PowerShell come amministratore e immettere i seguenti comandi hello. Sostituire hello *$pswd* con password hello utilizzato toocreate questo certificato. Sostituire hello *$PfxFilePath* con percorso completo di hello del nodo di hello PFX toothis copiato.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Impostare ora il controllo di accesso hello presente sul certificato in modo che il processo Service Fabric hello, che viene eseguito con l'account del servizio di rete hello, usarlo eseguendo lo script seguente hello. Specificare hello identificazione personale del certificato di hello e "Servizio di rete" per l'account del servizio hello. È possibile verificare che gli ACL hello certificato hello siano corrette, aprire il certificato di hello in *avviare* > *gestire i certificati del computer* ed esaminando *tutteleattività*  >  *Gestisci chiavi Private*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Ripetere i passaggi di hello sopra per ogni certificato del server. È inoltre possibile utilizzare questi passaggi tooinstall hello certificati client sul computer hello che si desidera che tooallow accesso toohello cluster.

## <a name="create-hello-secure-cluster"></a>Creare cluster sicuro hello
Dopo aver configurato hello **sicurezza** sezione di hello **ClusterConfig.X509.MultiMachine.json** file, è possibile procedere troppo[creare il cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure sezione Hello nodi e creare cluster autonomi di hello. Ricordare hello toouse **ClusterConfig.X509.MultiMachine.json** file durante la creazione di cluster hello. Il comando, ad esempio, potrebbe essere hello seguente:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Dopo aver protetto hello autonomo Windows cluster correttamente in esecuzione e il programma di installazione hello client autenticati tooconnect tooit, attenersi alla sezione hello [Connetti tooa cluster protetto tramite PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. ad esempio:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

È quindi possibile eseguire altri toowork i comandi di PowerShell con questo cluster. Ad esempio, [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow un elenco di nodi nel cluster protetto.


cluster hello tooremove, connettere toohello nodo nel cluster hello in cui è stato scaricato il pacchetto di Service Fabric hello, aprire una riga di comando e passare toohello cartella del pacchetto. A questo punto eseguire hello comando seguente:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Configurazione di un certificato non corretto può impedire a cluster hello presentarsi durante la distribuzione. tooself-diagnosticare i problemi di sicurezza, consultare il gruppo di Visualizzatore eventi *registri applicazioni e servizi* > *Microsoft Service Fabric*.
> 
> 

