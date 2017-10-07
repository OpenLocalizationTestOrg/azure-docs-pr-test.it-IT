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
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="88ae1-103">Connettere il cluster protetto di tooa</span><span class="sxs-lookup"><span data-stu-id="88ae1-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="88ae1-104">Quando un client si connette nodo del cluster di Service Fabric tooa, client hello può essere comunicazioni autenticate e protette stabilite utilizzando la sicurezza di certificati o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="88ae1-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="88ae1-105">Questa autenticazione assicura che solo gli utenti autorizzati possono accedere ai cluster hello e le applicazioni distribuite e attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="88ae1-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="88ae1-106">Certificato o la sicurezza di Azure ad deve essere stata precedentemente abilitata in cluster hello quando hello cluster è stato creato.</span><span class="sxs-lookup"><span data-stu-id="88ae1-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="88ae1-107">Per altre informazioni sugli scenari di sicurezza dei cluster, vedere [Sicurezza del cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="88ae1-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="88ae1-108">Se ci si connette tooa cluster protetti con i certificati, [impostare hello client certificato](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) computer hello che collega toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="88ae1-109">Connettersi tooa cluster sicuro utilizzando Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="88ae1-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="88ae1-110">Esistono alcuni modi diversi tooconnect tooa cluster sicuro utilizzando hello servizio infrastruttura CLI (sfctl).</span><span class="sxs-lookup"><span data-stu-id="88ae1-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="88ae1-111">Quando si utilizza un certificato client per l'autenticazione, il certificato di hello dettagli devono corrispondere al certificato distribuito toohello i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="88ae1-112">Se il certificato dispone di autorità di certificazione (CA), è necessario tooadditionally specificare hello attendibile l'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="88ae1-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="88ae1-113">È possibile connettersi tooa cluster utilizzando hello `sfctl cluster select` comando.</span><span class="sxs-lookup"><span data-stu-id="88ae1-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="88ae1-114">È possibile specificare i certificati client in due modi diversi, come una coppia chiave-certificato o come un file con estensione pem singolo.</span><span class="sxs-lookup"><span data-stu-id="88ae1-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="88ae1-115">Per la protezione con password `pem` file, sarà richiesto automaticamente password hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="88ae1-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="88ae1-116">certificato client di hello toospecify come un file con estensione pem, specificare il percorso di file hello in hello `--pem` argomento.</span><span class="sxs-lookup"><span data-stu-id="88ae1-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="88ae1-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="88ae1-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="88ae1-118">File pem protetti da password verranno richiesta la password precedente toorunning qualsiasi comando.</span><span class="sxs-lookup"><span data-stu-id="88ae1-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="88ae1-119">toospecify un certificato, coppia di chiavi utilizza hello `--cert` e `--key` toospecify hello percorsi tooeach rispettivo file di argomenti.</span><span class="sxs-lookup"><span data-stu-id="88ae1-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="88ae1-120">In alcuni casi i certificati utilizzati toosecure test o i cluster di sviluppo non superano la convalida di certificati.</span><span class="sxs-lookup"><span data-stu-id="88ae1-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="88ae1-121">toobypass certificato di verifica, specificare hello `--no-verify` opzione.</span><span class="sxs-lookup"><span data-stu-id="88ae1-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="88ae1-122">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="88ae1-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="88ae1-123">Non utilizzare hello `no-verify` opzione quando si connettono i cluster di Service Fabric tooproduction.</span><span class="sxs-lookup"><span data-stu-id="88ae1-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="88ae1-124">Inoltre, è possibile specificare i percorsi toodirectories di certificati CA attendibili o i singoli certificati.</span><span class="sxs-lookup"><span data-stu-id="88ae1-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="88ae1-125">toospecify questi percorsi, usare hello `--ca` argomento.</span><span class="sxs-lookup"><span data-stu-id="88ae1-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="88ae1-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="88ae1-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="88ae1-127">Dopo la connessione, dovrebbe essere possibile troppo[eseguire altri comandi sfctl](service-fabric-cli.md) toointeract con cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="88ae1-128">Connettere il cluster tooa tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="88ae1-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="88ae1-129">Prima di eseguire operazioni su un cluster tramite PowerShell, è necessario stabilire prima un cluster di toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="88ae1-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="88ae1-130">connessione di Hello del cluster viene utilizzato per tutti i comandi successivi hello dato sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88ae1-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="88ae1-131">Connettere il cluster non sicuri di tooan</span><span class="sxs-lookup"><span data-stu-id="88ae1-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="88ae1-132">tooan tooconnect non sicura del cluster, fornire hello cluster endpoint indirizzo toohello **Connect-ServiceFabricCluster** comando:</span><span class="sxs-lookup"><span data-stu-id="88ae1-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="88ae1-133">Connettersi tooa cluster sicuro tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88ae1-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="88ae1-134">tooconnect tooa cluster protetto che utilizza l'accesso di amministratore cluster tooauthorize Azure Active Directory, fornire l'identificazione personale del certificato di cluster hello e utilizzare hello *AzureActiveDirectory* flag.</span><span class="sxs-lookup"><span data-stu-id="88ae1-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88ae1-135">Connettersi tooa cluster sicuro usando un certificato client</span><span class="sxs-lookup"><span data-stu-id="88ae1-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="88ae1-136">Hello esecuzione dopo il comando PowerShell tooa tooconnect sicura del cluster che utilizza l'accesso come amministratore tooauthorize i certificati client.</span><span class="sxs-lookup"><span data-stu-id="88ae1-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="88ae1-137">Fornire l'identificazione personale del certificato di hello cluster e l'identificazione personale hello del certificato client hello che disponga delle autorizzazioni per la gestione di cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="88ae1-138">dettagli del certificato Hello devono corrispondere al certificato sui nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="88ae1-139">*ServerCertThumbprint* è hello identificazione personale del certificato server hello installato nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="88ae1-140">*FindValue* è hello identificazione personale del certificato client di amministrazione hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="88ae1-141">Quando vengono compilati i parametri di hello, comando hello è simile al seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="88ae1-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="88ae1-142">Connettersi tooa cluster sicuro tramite Active Directory di Windows</span><span class="sxs-lookup"><span data-stu-id="88ae1-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="88ae1-143">Se il cluster autonomo viene distribuito utilizzando la protezione di Active Directory, è possibile connettere il cluster di toohello aggiungendo il parametro hello "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="88ae1-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="88ae1-144">Connettere il cluster tooa utilizzando hello FabricClient APIs</span><span class="sxs-lookup"><span data-stu-id="88ae1-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="88ae1-145">Hello Service Fabric SDK fornisce hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe per la gestione di cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="88ae1-146">hello toouse APIs FabricClient, ottenere il pacchetto Microsoft.ServiceFabric NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="88ae1-147">Connettere il cluster non sicuri di tooan</span><span class="sxs-lookup"><span data-stu-id="88ae1-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="88ae1-148">tooconnect tooa protetta cluster remoto, creare un'istanza di FabricClient e fornire l'indirizzo del cluster hello:</span><span class="sxs-lookup"><span data-stu-id="88ae1-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="88ae1-149">Per il codice che viene eseguito all'interno di un cluster, ad esempio, in un servizio affidabile, creare un FabricClient *senza* specificando l'indirizzo del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="88ae1-150">FabricClient si connette la gestione locale toohello gateway in codice hello del nodo hello è attualmente in esecuzione, evitando un hop di rete aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="88ae1-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88ae1-151">Connettersi tooa cluster sicuro usando un certificato client</span><span class="sxs-lookup"><span data-stu-id="88ae1-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="88ae1-152">i nodi nel cluster hello Hello devono avere un certificato valido il cui nome comune o nome DNS nella rete SAN viene visualizzata nella hello [RemoteCommonNames proprietà](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) impostato su [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="88ae1-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="88ae1-153">Seguendo questo processo consente l'autenticazione reciproca tra client hello e i nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="88ae1-154">Connettersi tooa cluster sicuro in modo interattivo tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88ae1-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="88ae1-155">Hello seguente viene illustrato come utilizzare Azure Active Directory per il certificato di identità e i server client per l'identità del server.</span><span class="sxs-lookup"><span data-stu-id="88ae1-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="88ae1-156">Una finestra di dialogo visualizzata automaticamente per interactive sign-al momento della connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="88ae1-157">Connettersi tooa cluster sicuro in modo non interattivo tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88ae1-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="88ae1-158">Hello esempio seguente si basa su ActiveDirectory, versione: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="88ae1-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="88ae1-159">Per ulteriori informazioni sull'acquisizione di token di AAD, vedere [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="88ae1-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="88ae1-160">Connettersi cluster sicuro tooa senza una conoscenza preliminare di metadati tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88ae1-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="88ae1-161">esempio Hello utilizza acquisizione del token non interattiva, ma hello stesso approccio può essere utilizzato toobuild un'esperienza di acquisizione del token interattivo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="88ae1-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="88ae1-162">Hello i metadati di Azure Active Directory necessari per l'acquisizione del token viene letto dalla configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="88ae1-163">Connettersi tooa cluster sicuro usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="88ae1-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="88ae1-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) per un determinato cluster, puntare il browser per:</span><span class="sxs-lookup"><span data-stu-id="88ae1-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88ae1-165">URL completo di Hello è disponibile anche nel riquadro di essentials cluster hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88ae1-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="88ae1-166">Connettersi tooa cluster sicuro tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88ae1-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="88ae1-167">tooconnect tooa cluster che è protetta con AAD, puntare il browser per:</span><span class="sxs-lookup"><span data-stu-id="88ae1-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88ae1-168">Sarà automaticamente richiesta toolog con AAD.</span><span class="sxs-lookup"><span data-stu-id="88ae1-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88ae1-169">Connettersi tooa cluster sicuro usando un certificato client</span><span class="sxs-lookup"><span data-stu-id="88ae1-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="88ae1-170">tooconnect tooa cluster protetta con i certificati, puntare il browser per:</span><span class="sxs-lookup"><span data-stu-id="88ae1-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88ae1-171">Sarà automaticamente tooselect richiesto un certificato client.</span><span class="sxs-lookup"><span data-stu-id="88ae1-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="88ae1-172">Configurare un certificato client nel computer remoto hello</span><span class="sxs-lookup"><span data-stu-id="88ae1-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="88ae1-173">Almeno due certificati devono essere utilizzati per la protezione dei cluster hello, uno per il certificato di cluster e server hello e un altro per l'accesso client.</span><span class="sxs-lookup"><span data-stu-id="88ae1-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="88ae1-174">È consigliabile usare anche altri certificati secondari e certificati di accesso client.</span><span class="sxs-lookup"><span data-stu-id="88ae1-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="88ae1-175">comunicazione hello toosecure tra un client e un nodo di cluster mediante certificati di sicurezza, innanzitutto necessario tooobtain e installare il certificato client hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="88ae1-176">Hello certificato può essere installato in hello (My) archivio personale del computer locale hello o dell'utente corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="88ae1-177">Identificazione personale hello hello del certificato del server è necessario anche in modo che hello client può autenticare cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="88ae1-178">Eseguire hello seguente tooset di cmdlet di PowerShell backup del certificato client hello computer hello da cui si accedere cluster hello.</span><span class="sxs-lookup"><span data-stu-id="88ae1-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="88ae1-179">Se un certificato autofirmato, è necessario tooimport ciò "persone attendibili" della macchina tooyour archiviazione prima di poter usare certificato tooconnect tooa sicura del cluster.</span><span class="sxs-lookup"><span data-stu-id="88ae1-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="88ae1-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88ae1-180">Next steps</span></span>

* [<span data-ttu-id="88ae1-181">Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente</span><span class="sxs-lookup"><span data-stu-id="88ae1-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="88ae1-182">Gestione delle applicazioni di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88ae1-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="88ae1-183">Introduzione al modello di integrità di Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="88ae1-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="88ae1-184">Sicurezza delle applicazioni e RunAs</span><span class="sxs-lookup"><span data-stu-id="88ae1-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="88ae1-185">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88ae1-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
