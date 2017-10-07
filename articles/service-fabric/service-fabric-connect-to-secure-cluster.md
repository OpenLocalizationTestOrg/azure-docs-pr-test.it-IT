---
title: aaaConnect in modo sicuro i cluster di Azure Service Fabric tooan | Documenti Microsoft
description: Descrive come tooauthenticate client di accedere ai cluster di Service Fabric tooa e come toosecure comunicazione tra client e un cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a>Connettere il cluster protetto di tooa

Quando un client si connette nodo del cluster di Service Fabric tooa, client hello può essere comunicazioni autenticate e protette stabilite utilizzando la sicurezza di certificati o Azure Active Directory (AAD). Questa autenticazione assicura che solo gli utenti autorizzati possono accedere ai cluster hello e le applicazioni distribuite e attività di gestione.  Certificato o la sicurezza di Azure ad deve essere stata precedentemente abilitata in cluster hello quando hello cluster è stato creato.  Per altre informazioni sugli scenari di sicurezza dei cluster, vedere [Sicurezza del cluster](service-fabric-cluster-security.md). Se ci si connette tooa cluster protetti con i certificati, [impostare hello client certificato](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) computer hello che collega toohello cluster. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Connettersi tooa cluster sicuro utilizzando Azure Service Fabric CLI (sfctl)

Esistono alcuni modi diversi tooconnect tooa cluster sicuro utilizzando hello servizio infrastruttura CLI (sfctl). Quando si utilizza un certificato client per l'autenticazione, il certificato di hello dettagli devono corrispondere al certificato distribuito toohello i nodi del cluster. Se il certificato dispone di autorità di certificazione (CA), è necessario tooadditionally specificare hello attendibile l'autorità di certificazione.

È possibile connettersi tooa cluster utilizzando hello `sfctl cluster select` comando.

È possibile specificare i certificati client in due modi diversi, come una coppia chiave-certificato o come un file con estensione pem singolo. Per la protezione con password `pem` file, sarà richiesto automaticamente password hello tooenter.

certificato client di hello toospecify come un file con estensione pem, specificare il percorso di file hello in hello `--pem` argomento. ad esempio:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

File pem protetti da password verranno richiesta la password precedente toorunning qualsiasi comando.

toospecify un certificato, coppia di chiavi utilizza hello `--cert` e `--key` toospecify hello percorsi tooeach rispettivo file di argomenti.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

In alcuni casi i certificati utilizzati toosecure test o i cluster di sviluppo non superano la convalida di certificati. toobypass certificato di verifica, specificare hello `--no-verify` opzione. ad esempio:

> [!WARNING]
> Non utilizzare hello `no-verify` opzione quando si connettono i cluster di Service Fabric tooproduction.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Inoltre, è possibile specificare i percorsi toodirectories di certificati CA attendibili o i singoli certificati. toospecify questi percorsi, usare hello `--ca` argomento. ad esempio:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Dopo la connessione, dovrebbe essere possibile troppo[eseguire altri comandi sfctl](service-fabric-cli.md) toointeract con cluster hello.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Connettere il cluster tooa tramite PowerShell
Prima di eseguire operazioni su un cluster tramite PowerShell, è necessario stabilire prima un cluster di toohello di connessione. connessione di Hello del cluster viene utilizzato per tutti i comandi successivi hello dato sessione di PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Connettere il cluster non sicuri di tooan

tooan tooconnect non sicura del cluster, fornire hello cluster endpoint indirizzo toohello **Connect-ServiceFabricCluster** comando:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Connettersi tooa cluster sicuro tramite Azure Active Directory

tooconnect tooa cluster protetto che utilizza l'accesso di amministratore cluster tooauthorize Azure Active Directory, fornire l'identificazione personale del certificato di cluster hello e utilizzare hello *AzureActiveDirectory* flag.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Connettersi tooa cluster sicuro usando un certificato client
Hello esecuzione dopo il comando PowerShell tooa tooconnect sicura del cluster che utilizza l'accesso come amministratore tooauthorize i certificati client. Fornire l'identificazione personale del certificato di hello cluster e l'identificazione personale hello del certificato client hello che disponga delle autorizzazioni per la gestione di cluster. dettagli del certificato Hello devono corrispondere al certificato sui nodi del cluster hello.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* è hello identificazione personale del certificato server hello installato nei nodi del cluster hello. *FindValue* è hello identificazione personale del certificato client di amministrazione hello.
Quando vengono compilati i parametri di hello, comando hello è simile al seguente esempio hello: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Connettersi tooa cluster sicuro tramite Active Directory di Windows
Se il cluster autonomo viene distribuito utilizzando la protezione di Active Directory, è possibile connettere il cluster di toohello aggiungendo il parametro hello "WindowsCredential".

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Connettere il cluster tooa utilizzando hello FabricClient APIs
Hello Service Fabric SDK fornisce hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe per la gestione di cluster. hello toouse APIs FabricClient, ottenere il pacchetto Microsoft.ServiceFabric NuGet hello.

### <a name="connect-tooan-unsecure-cluster"></a>Connettere il cluster non sicuri di tooan

tooconnect tooa protetta cluster remoto, creare un'istanza di FabricClient e fornire l'indirizzo del cluster hello:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Per il codice che viene eseguito all'interno di un cluster, ad esempio, in un servizio affidabile, creare un FabricClient *senza* specificando l'indirizzo del cluster hello. FabricClient si connette la gestione locale toohello gateway in codice hello del nodo hello è attualmente in esecuzione, evitando un hop di rete aggiuntiva.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Connettersi tooa cluster sicuro usando un certificato client

i nodi nel cluster hello Hello devono avere un certificato valido il cui nome comune o nome DNS nella rete SAN viene visualizzata nella hello [RemoteCommonNames proprietà](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) impostato su [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Seguendo questo processo consente l'autenticazione reciproca tra client hello e i nodi del cluster hello.

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Connettersi tooa cluster sicuro in modo interattivo tramite Azure Active Directory

Hello seguente viene illustrato come utilizzare Azure Active Directory per il certificato di identità e i server client per l'identità del server.

Una finestra di dialogo visualizzata automaticamente per interactive sign-al momento della connessione toohello cluster.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Connettersi tooa cluster sicuro in modo non interattivo tramite Azure Active Directory

Hello esempio seguente si basa su ActiveDirectory, versione: 2.19.208020213.

Per ulteriori informazioni sull'acquisizione di token di AAD, vedere [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Connettersi cluster sicuro tooa senza una conoscenza preliminare di metadati tramite Azure Active Directory

esempio Hello utilizza acquisizione del token non interattiva, ma hello stesso approccio può essere utilizzato toobuild un'esperienza di acquisizione del token interattivo personalizzato. Hello i metadati di Azure Active Directory necessari per l'acquisizione del token viene letto dalla configurazione del cluster.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Connettersi tooa cluster sicuro usando Service Fabric Explorer
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) per un determinato cluster, puntare il browser per:

`http://<your-cluster-endpoint>:19080/Explorer`

URL completo di Hello è disponibile anche nel riquadro di essentials cluster hello di hello portale di Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Connettersi tooa cluster sicuro tramite Azure Active Directory

tooconnect tooa cluster che è protetta con AAD, puntare il browser per:

`https://<your-cluster-endpoint>:19080/Explorer`

Sarà automaticamente richiesta toolog con AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Connettersi tooa cluster sicuro usando un certificato client

tooconnect tooa cluster protetta con i certificati, puntare il browser per:

`https://<your-cluster-endpoint>:19080/Explorer`

Sarà automaticamente tooselect richiesto un certificato client.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Configurare un certificato client nel computer remoto hello
Almeno due certificati devono essere utilizzati per la protezione dei cluster hello, uno per il certificato di cluster e server hello e un altro per l'accesso client.  È consigliabile usare anche altri certificati secondari e certificati di accesso client.  comunicazione hello toosecure tra un client e un nodo di cluster mediante certificati di sicurezza, innanzitutto necessario tooobtain e installare il certificato client hello. Hello certificato può essere installato in hello (My) archivio personale del computer locale hello o dell'utente corrente di hello.  Identificazione personale hello hello del certificato del server è necessario anche in modo che hello client può autenticare cluster hello.

Eseguire hello seguente tooset di cmdlet di PowerShell backup del certificato client hello computer hello da cui si accedere cluster hello.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Se un certificato autofirmato, è necessario tooimport ciò "persone attendibili" della macchina tooyour archiviazione prima di poter usare certificato tooconnect tooa sicura del cluster.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Passaggi successivi

* [Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente](service-fabric-cluster-upgrade.md)
* [Gestione delle applicazioni di Service Fabric in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Introduzione al modello di integrità di Infrastruttura di servizi](service-fabric-health-introduction.md)
* [Sicurezza delle applicazioni e RunAs](service-fabric-application-runas-security.md)
* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)
