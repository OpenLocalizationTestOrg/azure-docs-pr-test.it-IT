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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="5c28c-103">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="5c28c-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="5c28c-104">In questo articolo viene descritto come toosecure hello comunicazione hello vari nodi del cluster di Windows autonoma, nonché il modo tooauthenticate client che si connettono toothis cluster, utilizzando i certificati x. 509.</span><span class="sxs-lookup"><span data-stu-id="5c28c-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="5c28c-105">Ciò garantisce che solo gli utenti autorizzati possono accedere cluster hello, hello applicazioni distribuite e attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="5c28c-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="5c28c-106">Sicurezza di certificato deve essere abilitata nel cluster hello quando viene creato il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="5c28c-107">Per altre informazioni sulla sicurezza del cluster da nodo a nodo e da client a nodo e sul controllo degli accessi in base al ruolo, vedere [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="5c28c-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="5c28c-108">Certificati necessari</span><span class="sxs-lookup"><span data-stu-id="5c28c-108">Which certificates will you need?</span></span>
<span data-ttu-id="5c28c-109">toostart, [download del pacchetto del cluster autonomo hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone dei nodi di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="5c28c-110">In hello scaricato pacchetto, si noterà un **ClusterConfig.X509.MultiMachine.json** file.</span><span class="sxs-lookup"><span data-stu-id="5c28c-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="5c28c-111">Aprire il file hello e sezione hello **sicurezza** in hello **proprietà** sezione:</span><span class="sxs-lookup"><span data-stu-id="5c28c-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

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

<span data-ttu-id="5c28c-112">In questa sezione illustra i certificati di hello che è necessario per proteggere il cluster di Windows autonoma.</span><span class="sxs-lookup"><span data-stu-id="5c28c-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="5c28c-113">Se si specifica un certificato del cluster, impostare il valore di hello di **ClusterCredentialType** too_**X509**_. Se si specifica il certificato server per le connessioni esterne, impostare hello **ServerCredentialType** troppo_**X509**_. Sebbene non obbligatorio, è consigliabile toohave entrambi questi certificati per un cluster protetto correttamente. Se si imposta questi valori troppo*X509* è necessario specificare anche hello certificati corrispondenti o Service Fabric genererà un'eccezione. In alcuni scenari, può essere solo hello toospecify _ClientCertificateThumbprints_ o _ReverseProxyCertificate_. In tali scenari, non è necessario impostare _ClusterCredentialType_ o _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="5c28c-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="5c28c-114">Oggetto [identificazione personale](https://en.wikipedia.org/wiki/Public_key_fingerprint) hello identità primaria di un certificato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="5c28c-115">Lettura [come tooretrieve identificazione personale di un certificato](https://msdn.microsoft.com/library/ms734695.aspx) toofind all'identificazione personale hello di hello che i certificati creati.</span><span class="sxs-lookup"><span data-stu-id="5c28c-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="5c28c-116">Hello nella tabella seguente elenca i certificati di hello che sarà necessario nel programma di installazione del cluster:</span><span class="sxs-lookup"><span data-stu-id="5c28c-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="5c28c-117">**CertificateInformation Setting**</span><span class="sxs-lookup"><span data-stu-id="5c28c-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="5c28c-118">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="5c28c-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5c28c-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="5c28c-119">ClusterCertificate</span></span> |<span data-ttu-id="5c28c-120">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5c28c-120">Recommended for test environment.</span></span> <span data-ttu-id="5c28c-121">Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="5c28c-122">È possibile usare due diversi certificati, uno primario e uno secondario per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5c28c-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="5c28c-123">Impostare l'identificazione personale hello del certificato primario hello in hello **identificazione personale** sezione e quello di hello secondario nel hello **ThumbprintSecondary** variabili.</span><span class="sxs-lookup"><span data-stu-id="5c28c-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="5c28c-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5c28c-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="5c28c-125">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5c28c-125">Recommended for production environment.</span></span> <span data-ttu-id="5c28c-126">Questo certificato è obbligatorio toosecure hello comunicazione tra i nodi di hello in un cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="5c28c-127">È possibile usare uno o due nomi comuni del certificato del cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="5c28c-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="5c28c-128">ServerCertificate</span></span> |<span data-ttu-id="5c28c-129">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5c28c-129">Recommended for test environment.</span></span> <span data-ttu-id="5c28c-130">Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="5c28c-131">Per praticità, è possibile scegliere toouse hello stesso certificato per *ClusterCertificate* e *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="5c28c-132">È possibile usare due diversi certificati del server, uno primario e uno secondario per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5c28c-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="5c28c-133">Impostare l'identificazione personale hello del certificato primario hello in hello **identificazione personale** sezione e quello di hello secondario nel hello **ThumbprintSecondary** variabili.</span><span class="sxs-lookup"><span data-stu-id="5c28c-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="5c28c-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5c28c-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="5c28c-135">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5c28c-135">Recommended for production environment.</span></span> <span data-ttu-id="5c28c-136">Questo certificato viene presentato toohello client durante il tentativo di tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="5c28c-137">Per praticità, è possibile scegliere toouse hello stesso certificato per *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="5c28c-138">È possibile usare uno o due nomi comuni del certificato del server.</span><span class="sxs-lookup"><span data-stu-id="5c28c-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="5c28c-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="5c28c-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="5c28c-140">Si tratta di un set di certificati che si desidera tooinstall nei client hello autenticato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="5c28c-141">Si può avere un numero diverso di certificati di client installati in computer hello che si desidera che tooallow accesso toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="5c28c-142">Impostare l'identificazione personale hello di ogni certificato in hello **CertificateThumbprint** variabile.</span><span class="sxs-lookup"><span data-stu-id="5c28c-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="5c28c-143">Se si imposta hello **IsAdmin** troppo*true*, quindi client hello con il certificato installato può eseguire amministratore attività di gestione in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="5c28c-144">Se hello **IsAdmin** è *false*, client hello con questo certificato può eseguire solo azioni hello consentite per i diritti di accesso utente, in genere di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="5c28c-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="5c28c-145">Per altre informazioni sui ruoli, vedere [Controllo degli accessi in base al ruolo (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="5c28c-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="5c28c-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5c28c-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="5c28c-147">Set hello nome comune del certificato client prima di hello hello **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="5c28c-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="5c28c-148">Hello **CertificateIssuerThumbprint** è l'identificazione personale hello per emittente hello del certificato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="5c28c-149">Lettura [utilizzo dei certificati](https://msdn.microsoft.com/library/ms731899.aspx) tooknow informazioni sui nomi comuni e dell'autorità emittente hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="5c28c-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="5c28c-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="5c28c-151">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5c28c-151">Recommended for test environment.</span></span> <span data-ttu-id="5c28c-152">Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="5c28c-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="5c28c-153">Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes.</span><span class="sxs-lookup"><span data-stu-id="5c28c-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="5c28c-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="5c28c-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="5c28c-155">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5c28c-155">Recommended for production environment.</span></span> <span data-ttu-id="5c28c-156">Si tratta di un certificato facoltativo che può essere specificato se si desidera toosecure il [Proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="5c28c-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="5c28c-157">Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes.</span><span class="sxs-lookup"><span data-stu-id="5c28c-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="5c28c-158">Di seguito è esempio di configurazione di cluster in cui sono stati forniti i certificati Client, Server e Cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="5c28c-159">Si noti che per cluster / server / reverseProxy certificati, l'identificazione personale e nome comune non sono consentiti toobe configurati insieme per hello stesso tipo di certificato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

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

## <a name="certificate-roll-over"></a><span data-ttu-id="5c28c-160">Rollover del certificato</span><span class="sxs-lookup"><span data-stu-id="5c28c-160">Certificate roll over</span></span>
<span data-ttu-id="5c28c-161">Quando si usa il nome comune del certificato al posto dell'identificazione personale, il rollover del certificato non richiede l'aggiornamento della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="5c28c-162">Se prevede di rollover certificato dell'autorità di certificazione continuata, tenere il certificato dell'autorità di certificazione precedente di hello nell'archivio cert hello almeno 2 ore dopo l'installazione del certificato dell'autorità di certificazione nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="5c28c-163">Acquisire i certificati x. 509 hello</span><span class="sxs-lookup"><span data-stu-id="5c28c-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="5c28c-164">comunicazione toosecure all'interno di cluster hello, è necessario innanzitutto i certificati x. 509 tooobtain per i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="5c28c-165">Inoltre, toolimit connessione toothis cluster tooauthorized macchine/gli utenti, sarà anche necessario tooobtain e installare i certificati per i computer client hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="5c28c-166">Per i cluster che eseguono carichi di lavoro di produzione, è necessario utilizzare un [autorità di certificazione (CA)](https://en.wikipedia.org/wiki/Certificate_authority) firmato cluster hello toosecure di certificato x. 509.</span><span class="sxs-lookup"><span data-stu-id="5c28c-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="5c28c-167">Per informazioni dettagliate su come ottenere questi certificati, vedere troppo[procedura: ottenere un certificato](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c28c-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="5c28c-168">Per i cluster che si usa per scopi di test, è possibile scegliere un certificato autofirmato toouse.</span><span class="sxs-lookup"><span data-stu-id="5c28c-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="5c28c-169">Facoltativo: creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="5c28c-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="5c28c-170">Un modo toocreate un certificato autofirmato che può essere protetta correttamente è hello toouse *CertSetup.ps1* script nella cartella di Service Fabric SDK hello nella directory di hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="5c28c-171">Modificare questo nome di file toochange hello predefinito del certificato hello (cercare il valore di hello *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="5c28c-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="5c28c-172">Eseguire questo script come `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="5c28c-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="5c28c-173">Ora, esportare file di hello certificato tooa PFX con una password protetta.</span><span class="sxs-lookup"><span data-stu-id="5c28c-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="5c28c-174">Ottenere innanzitutto l'identificazione personale hello del certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="5c28c-175">Da hello *avviare* menu, eseguire hello *gestire i certificati del computer*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="5c28c-176">Passare toohello **locale\Personale.** cartella e individuare hello certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="5c28c-177">Fare doppio clic su tooopen certificato hello è hello seleziona *dettagli* scheda e scorrere verso il basso toohello *identificazione personale* campo.</span><span class="sxs-lookup"><span data-stu-id="5c28c-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="5c28c-178">Copiare il valore di identificazione personale hello nel comando di PowerShell hello seguito, dopo aver rimosso gli spazi hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="5c28c-179">Hello modifica `String` valore tooa password sicura adatto tooprotect e hello esecuzione seguente in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5c28c-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="5c28c-180">toosee hello dettagli di un certificato installato hello del computer è possibile eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="5c28c-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="5c28c-181">In alternativa, se si dispone di una sottoscrizione di Azure, attenersi alla sezione hello [aggiungere certificati tooKey insieme di credenziali](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="5c28c-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="5c28c-182">Installare i certificati di hello</span><span class="sxs-lookup"><span data-stu-id="5c28c-182">Install hello certificates</span></span>
<span data-ttu-id="5c28c-183">Dopo aver creato uno o più certificati, è possibile installare nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="5c28c-184">I nodi devono toohave hello più recente di Windows PowerShell 3. x installati su di essi.</span><span class="sxs-lookup"><span data-stu-id="5c28c-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="5c28c-185">Sarà necessario toorepeat questi passaggi in ogni nodo, per i certificati di Cluster sia del Server e i certificati secondari.</span><span class="sxs-lookup"><span data-stu-id="5c28c-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="5c28c-186">Nodo di toohello file con estensione pfx hello copia.</span><span class="sxs-lookup"><span data-stu-id="5c28c-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="5c28c-187">Aprire una finestra di PowerShell come amministratore e immettere i seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="5c28c-188">Sostituire hello *$pswd* con password hello utilizzato toocreate questo certificato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="5c28c-189">Sostituire hello *$PfxFilePath* con percorso completo di hello del nodo di hello PFX toothis copiato.</span><span class="sxs-lookup"><span data-stu-id="5c28c-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="5c28c-190">Impostare ora il controllo di accesso hello presente sul certificato in modo che il processo Service Fabric hello, che viene eseguito con l'account del servizio di rete hello, usarlo eseguendo lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="5c28c-191">Specificare hello identificazione personale del certificato di hello e "Servizio di rete" per l'account del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="5c28c-192">È possibile verificare che gli ACL hello certificato hello siano corrette, aprire il certificato di hello in *avviare* > *gestire i certificati del computer* ed esaminando *tutteleattività*  >  *Gestisci chiavi Private*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
4. <span data-ttu-id="5c28c-193">Ripetere i passaggi di hello sopra per ogni certificato del server.</span><span class="sxs-lookup"><span data-stu-id="5c28c-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="5c28c-194">È inoltre possibile utilizzare questi passaggi tooinstall hello certificati client sul computer hello che si desidera che tooallow accesso toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="5c28c-195">Creare cluster sicuro hello</span><span class="sxs-lookup"><span data-stu-id="5c28c-195">Create hello secure cluster</span></span>
<span data-ttu-id="5c28c-196">Dopo aver configurato hello **sicurezza** sezione di hello **ClusterConfig.X509.MultiMachine.json** file, è possibile procedere troppo[creare il cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure sezione Hello nodi e creare cluster autonomi di hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="5c28c-197">Ricordare hello toouse **ClusterConfig.X509.MultiMachine.json** file durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5c28c-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="5c28c-198">Il comando, ad esempio, potrebbe essere hello seguente:</span><span class="sxs-lookup"><span data-stu-id="5c28c-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="5c28c-199">Dopo aver protetto hello autonomo Windows cluster correttamente in esecuzione e il programma di installazione hello client autenticati tooconnect tooit, attenersi alla sezione hello [Connetti tooa cluster protetto tramite PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="5c28c-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="5c28c-200">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5c28c-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="5c28c-201">È quindi possibile eseguire altri toowork i comandi di PowerShell con questo cluster.</span><span class="sxs-lookup"><span data-stu-id="5c28c-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="5c28c-202">Ad esempio, [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow un elenco di nodi nel cluster protetto.</span><span class="sxs-lookup"><span data-stu-id="5c28c-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="5c28c-203">cluster hello tooremove, connettere toohello nodo nel cluster hello in cui è stato scaricato il pacchetto di Service Fabric hello, aprire una riga di comando e passare toohello cartella del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5c28c-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="5c28c-204">A questo punto eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5c28c-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="5c28c-205">Configurazione di un certificato non corretto può impedire a cluster hello presentarsi durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5c28c-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="5c28c-206">tooself-diagnosticare i problemi di sicurezza, consultare il gruppo di Visualizzatore eventi *registri applicazioni e servizi* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="5c28c-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

