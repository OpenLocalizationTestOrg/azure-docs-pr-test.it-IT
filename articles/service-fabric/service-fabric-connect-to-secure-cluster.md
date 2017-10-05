---
title: Connettersi a un cluster sicuro di Azure Service Fabric | Microsoft Docs
description: Descrive come autenticare l'accesso client a un cluster di Service Fabric e come proteggere la comunicazione tra i client e un cluster.
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
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="8a017-103">Connettersi a un cluster sicuro</span><span class="sxs-lookup"><span data-stu-id="8a017-103">Connect to a secure cluster</span></span>

<span data-ttu-id="8a017-104">Quando un client si connette a un nodo di un cluster di Service Fabric, è possibile autenticare il client e proteggere la comunicazione stabilita usando la sicurezza basata su certificati o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8a017-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="8a017-105">Questa autenticazione garantisce che solo gli utenti autorizzati possano accedere al cluster e alle applicazioni distribuite ed eseguire attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="8a017-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="8a017-106">La sicurezza basata su certificati o AAD deve essere stata abilitata in precedenza nel cluster durante la creazione del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="8a017-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="8a017-107">Per altre informazioni sugli scenari di sicurezza dei cluster, vedere [Sicurezza del cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="8a017-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="8a017-108">Se ci si connette a un cluster protetto con certificati, [configurare il certificato client](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) nel computer che si connette al cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="8a017-109">Connettersi a un cluster sicuro usando l'interfaccia della riga di comando di Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="8a017-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="8a017-110">Esistono modi diversi per connettersi a un cluster protetto usando l'interfaccia della riga di comando di Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="8a017-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="8a017-111">Quando si usa un certificato client per l'autenticazione, i dettagli del certificato devono corrispondere al certificato distribuito ai nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="8a017-112">Se il certificato dispone di autorità di certificazione (CA), è necessario specificare anche le autorità di certificazione attendibili.</span><span class="sxs-lookup"><span data-stu-id="8a017-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="8a017-113">È possibile connettersi a un cluster con il comando `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="8a017-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="8a017-114">È possibile specificare i certificati client in due modi diversi, come una coppia chiave-certificato o come un file con estensione pem singolo.</span><span class="sxs-lookup"><span data-stu-id="8a017-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="8a017-115">Per i file `pem` protetti da password verrà chiesto automaticamente di immettere la password.</span><span class="sxs-lookup"><span data-stu-id="8a017-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="8a017-116">Per specificare il certificato client come file con estensione pem, specificare il percorso del file nell'argomento `--pem`.</span><span class="sxs-lookup"><span data-stu-id="8a017-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="8a017-117">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8a017-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="8a017-118">I file con estensione pem protetti da password chiederanno la password prima di eseguire qualsiasi comando.</span><span class="sxs-lookup"><span data-stu-id="8a017-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="8a017-119">Per specificare una coppia certificato-chiave, usare gli argomenti `--cert` e `--key` per specificare i percorsi di file a ogni rispettivo file.</span><span class="sxs-lookup"><span data-stu-id="8a017-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="8a017-120">In alcuni casi i certificati usati per proteggere i cluster di test o di sviluppo non superano la convalida.</span><span class="sxs-lookup"><span data-stu-id="8a017-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="8a017-121">Per ignorare la verifica del certificato, specificare l'opzione `--no-verify`.</span><span class="sxs-lookup"><span data-stu-id="8a017-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="8a017-122">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8a017-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="8a017-123">Non usare l'opzione `no-verify` quando ci si connette a cluster di Service Fabric di produzione.</span><span class="sxs-lookup"><span data-stu-id="8a017-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="8a017-124">È anche possibile specificare i percorsi a directory di certificati CA attendibili o a certificati individuali.</span><span class="sxs-lookup"><span data-stu-id="8a017-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="8a017-125">Per specificare questi percorsi, usare l'argomento `--ca`.</span><span class="sxs-lookup"><span data-stu-id="8a017-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="8a017-126">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8a017-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="8a017-127">Dopo la connessione, sarà possibile [eseguire altri comandi sfctl](service-fabric-cli.md) per interagire con il cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="8a017-128">Connessione a un cluster mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a017-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="8a017-129">Prima di eseguire operazioni su un cluster tramite PowerShell, stabilire una connessione al cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="8a017-130">La connessione al cluster verrà usata per tutti i successivi comandi nella specifica sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a017-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="8a017-131">Connettersi a un cluster non sicuro</span><span class="sxs-lookup"><span data-stu-id="8a017-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="8a017-132">Per connettersi a un cluster non sicuro, specificare l'indirizzo dell'endpoint del cluster nel comando **Connect-ServiceFabricCluster**:</span><span class="sxs-lookup"><span data-stu-id="8a017-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="8a017-133">Connettersi a un cluster sicuro con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="8a017-134">Per connettersi a un cluster sicuro che usa Azure Active Directory per autorizzare l'accesso di amministratore al cluster, specificare l'identificazione personale del certificato del cluster e usare il flag *AzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="8a017-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8a017-135">Connettersi a un cluster sicuro con un certificato client</span><span class="sxs-lookup"><span data-stu-id="8a017-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="8a017-136">Per connettersi a un cluster sicuro che usa certificati client per autorizzare l'accesso di amministratore, eseguire il comando di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="8a017-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="8a017-137">Specificare l'identificazione personale del certificato del cluster e l'identificazione personale del certificato client a cui sono state concesse le autorizzazioni per la gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="8a017-138">I dettagli del certificato devono corrispondere a un certificato sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="8a017-139">*ServerCertThumbprint* è l'identificazione personale del certificato del server installato nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="8a017-140">*FindValue* è l'identificazione personale del certificato client di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="8a017-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="8a017-141">Dopo l'immissione dei parametri, il comando sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8a017-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="8a017-142">Connettersi a un cluster sicuro con Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="8a017-143">Se il cluster autonomo viene distribuito usando la protezione di Active Directory, connettersi al cluster aggiungendo l'opzione "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="8a017-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="8a017-144">Connettersi a un cluster mediante le API FabricClient</span><span class="sxs-lookup"><span data-stu-id="8a017-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="8a017-145">Service Fabric SDK fornisce la classe [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) per la gestione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="8a017-146">Per usare le API di FabricClient, è necessario disporre del pacchetto NuGet Microsoft.ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="8a017-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="8a017-147">Connettersi a un cluster non sicuro</span><span class="sxs-lookup"><span data-stu-id="8a017-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="8a017-148">Per connettersi a un cluster remoto non protetto, creare un'istanza di FabricClient e specificare l'indirizzo del cluster:</span><span class="sxs-lookup"><span data-stu-id="8a017-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="8a017-149">Per il codice in esecuzione in un cluster, ad esempio in un servizio Reliable Services, creare un'istanza di FabricClient *senza* specificare l'indirizzo del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="8a017-150">FabricClient si connette al gateway di gestione locale nel nodo in cui il codice è attualmente in esecuzione, evitando un hop di rete aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="8a017-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8a017-151">Connettersi a un cluster sicuro con un certificato client</span><span class="sxs-lookup"><span data-stu-id="8a017-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="8a017-152">I nodi del cluster devono avere certificati validi il cui nome comune o nome DNS nella rete SAN è contenuto nella [proprietà RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) impostata in [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="8a017-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="8a017-153">Questo processo consente l'autenticazione reciproca tra il client e i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="8a017-154">Connessione interattiva a un cluster protetto con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="8a017-155">Nell'esempio seguente viene utilizzata Azure Active Directory per l'identità del client e il certificato del server per l'identità del server.</span><span class="sxs-lookup"><span data-stu-id="8a017-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="8a017-156">Al momento della connessione al cluster viene visualizzata automaticamente una finestra di dialogo per l'accesso interattivo.</span><span class="sxs-lookup"><span data-stu-id="8a017-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="8a017-157">Connessione non interattiva a un cluster protetto con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="8a017-158">L'esempio è basato su Microsoft.IdentityModel.Clients.ActiveDirectory, Versione: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="8a017-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="8a017-159">Per ulteriori informazioni sull'acquisizione di token di AAD, vedere [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a017-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="8a017-160">Connessione a un cluster protetto senza conoscere a priori i metadati tramite Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="8a017-161">L'esempio seguente usa l'acquisizione dei token non interattiva, ma lo stesso approccio consente di creare un'esperienza di acquisizione dei token interattiva personalizzata.</span><span class="sxs-lookup"><span data-stu-id="8a017-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="8a017-162">I metadati di Azure Active Directory necessari per l'acquisizione dei token vengono letti dalla configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="8a017-163">Connettersi a un cluster sicuro usando Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8a017-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="8a017-164">Per raggiungere [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) per un determinato cluster, inserire nel browser l'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a017-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8a017-165">L'URL completo è disponibile anche nel riquadro essentials del cluster del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a017-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="8a017-166">Connettersi a un cluster sicuro con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a017-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="8a017-167">Per connettersi a un cluster protetto con AAD, inserire nel browser l'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a017-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8a017-168">Viene automaticamente richiesto di accedere con AAD.</span><span class="sxs-lookup"><span data-stu-id="8a017-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="8a017-169">Connettersi a un cluster sicuro con un certificato client</span><span class="sxs-lookup"><span data-stu-id="8a017-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="8a017-170">Per connettersi a un cluster protetto con certificati, inserire nel browser l'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="8a017-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="8a017-171">Viene automaticamente richiesto di selezionare un certificato del client.</span><span class="sxs-lookup"><span data-stu-id="8a017-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="8a017-172">Configurare un certificato client nel computer remoto</span><span class="sxs-lookup"><span data-stu-id="8a017-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="8a017-173">È necessario usare almeno due certificati per proteggere il cluster, uno per il certificato del server e del cluster e un altro per l'accesso client.</span><span class="sxs-lookup"><span data-stu-id="8a017-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="8a017-174">È consigliabile usare anche altri certificati secondari e certificati di accesso client.</span><span class="sxs-lookup"><span data-stu-id="8a017-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="8a017-175">Per proteggere la comunicazione tra un client e un nodo del cluster con la sicurezza basata su certificati, è prima necessario ottenere e installare il certificato client.</span><span class="sxs-lookup"><span data-stu-id="8a017-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="8a017-176">Il certificato può essere installato nell'archivio personale del computer locale o dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="8a017-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="8a017-177">È necessaria anche l'identificazione personale del certificato del server in modo che il client possa autenticare il cluster.</span><span class="sxs-lookup"><span data-stu-id="8a017-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="8a017-178">Per configurare il certificato del client nel computer che si userà per accedere al cluster, eseguire il cmdlet PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="8a017-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="8a017-179">Se si tratta di un certificato autofirmato, è necessario importarlo nell'archivio "Persone attendibili" del computer prima di poterlo usare per la connessione a un cluster sicuro.</span><span class="sxs-lookup"><span data-stu-id="8a017-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="8a017-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a017-180">Next steps</span></span>

* [<span data-ttu-id="8a017-181">Processo di aggiornamento del cluster di infrastruttura di servizi e operazioni eseguibile dall'utente</span><span class="sxs-lookup"><span data-stu-id="8a017-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="8a017-182">Gestione delle applicazioni di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a017-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="8a017-183">Introduzione al modello di integrità di Infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="8a017-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="8a017-184">Sicurezza delle applicazioni e RunAs</span><span class="sxs-lookup"><span data-stu-id="8a017-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="8a017-185">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8a017-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
