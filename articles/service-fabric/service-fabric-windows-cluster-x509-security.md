---
title: Proteggere un cluster di Azure Service Fabric in Windows usando i certificati | Microsoft Docs
description: "Questo articolo descrive come proteggere le comunicazioni all'interno del cluster autonomo o privato, nonché tra i client e il cluster."
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
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="38032-103">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="38032-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="38032-104">Questo articolo descrive come proteggere la comunicazione tra i diversi nodi del cluster Windows autonomo e come autenticare i client che si connettono a questo cluster usando certificati X.509.</span><span class="sxs-lookup"><span data-stu-id="38032-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="38032-105">In questo modo, solo gli utenti autorizzati possano accedere al cluster e alle applicazioni distribuite ed eseguire attività di gestione.</span><span class="sxs-lookup"><span data-stu-id="38032-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="38032-106">La sicurezza basata su certificati deve essere abilitata nel cluster durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="38032-107">Per altre informazioni sulla sicurezza del cluster da nodo a nodo e da client a nodo e sul controllo degli accessi in base al ruolo, vedere [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="38032-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="38032-108">Certificati necessari</span><span class="sxs-lookup"><span data-stu-id="38032-108">Which certificates will you need?</span></span>
<span data-ttu-id="38032-109">Per iniziare, [scaricare il pacchetto del cluster autonomo](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) in uno dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="38032-110">Nel pacchetto scaricato è incluso il file **ClusterConfig.X509.MultiMachine.json** .</span><span class="sxs-lookup"><span data-stu-id="38032-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="38032-111">Aprire il file ed esaminare la sezione **security** nella sezione **properties**:</span><span class="sxs-lookup"><span data-stu-id="38032-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

<span data-ttu-id="38032-112">Questa sezione descrive i certificati necessari per proteggere il cluster Windows autonomo.</span><span class="sxs-lookup"><span data-stu-id="38032-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="38032-113">Se si specifica un certificato del cluster, impostare il valore di **ClusterCredentialType** su _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="38032-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="38032-114">Se si specifica un certificato del server per le connessioni esterne, impostare il valore di **ServerCredentialType** su _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="38032-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="38032-115">Benché non sia obbligatorio, è consigliabile disporre di entrambi questi certificati per un cluster adeguatamente protetto.</span><span class="sxs-lookup"><span data-stu-id="38032-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="38032-116">Se si impostano questi valori su *X509*, sarà inoltre necessario specificare i certificati corrispondenti o Service Fabric genererà un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="38032-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="38032-117">In alcuni scenari può essere preferibile specificare solo _ClientCertificateThumbprints_ o _ReverseProxyCertificate_.</span><span class="sxs-lookup"><span data-stu-id="38032-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="38032-118">In questi scenari non è necessario impostare _ClusterCredentialType_ o _ServerCredentialType_ su _X509_.</span><span class="sxs-lookup"><span data-stu-id="38032-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="38032-119">Un' [identificazione personale](https://en.wikipedia.org/wiki/Public_key_fingerprint) è l'identità primaria di un certificato.</span><span class="sxs-lookup"><span data-stu-id="38032-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="38032-120">Per trovare l'identificazione personale dei certificati creati dall'utente, vedere [Procedura: Recuperare l'identificazione personale di un certificato](https://msdn.microsoft.com/library/ms734695.aspx) .</span><span class="sxs-lookup"><span data-stu-id="38032-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="38032-121">La tabella seguente include un elenco dei certificati necessari per la configurazione del cluster:</span><span class="sxs-lookup"><span data-stu-id="38032-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="38032-122">**CertificateInformation Setting**</span><span class="sxs-lookup"><span data-stu-id="38032-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="38032-123">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="38032-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="38032-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="38032-124">ClusterCertificate</span></span> |<span data-ttu-id="38032-125">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38032-125">Recommended for test environment.</span></span> <span data-ttu-id="38032-126">Questo certificato è necessario per proteggere la comunicazione tra i nodi di un cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="38032-127">È possibile usare due diversi certificati, uno primario e uno secondario per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="38032-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="38032-128">Impostare l'identificazione personale del certificato primario nella sezione **Thumbprint** e quella del certificato secondario nelle variabili **ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="38032-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="38032-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="38032-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="38032-130">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="38032-130">Recommended for production environment.</span></span> <span data-ttu-id="38032-131">Questo certificato è necessario per proteggere la comunicazione tra i nodi di un cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="38032-132">È possibile usare uno o due nomi comuni del certificato del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="38032-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="38032-133">ServerCertificate</span></span> |<span data-ttu-id="38032-134">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38032-134">Recommended for test environment.</span></span> <span data-ttu-id="38032-135">Questo certificato viene presentato al client quando tenta di connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="38032-136">Per praticità, è possibile scegliere di usare lo stesso certificato per *ClusterCertificate* e *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="38032-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="38032-137">È possibile usare due diversi certificati del server, uno primario e uno secondario per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="38032-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="38032-138">Impostare l'identificazione personale del certificato primario nella sezione **Thumbprint** e quella del certificato secondario nelle variabili **ThumbprintSecondary**.</span><span class="sxs-lookup"><span data-stu-id="38032-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="38032-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="38032-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="38032-140">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="38032-140">Recommended for production environment.</span></span> <span data-ttu-id="38032-141">Questo certificato viene presentato al client quando tenta di connettersi al cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="38032-142">Per praticità, è possibile scegliere di usare lo stesso certificato per *ClusterCertificateCommonNames* e *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="38032-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="38032-143">È possibile usare uno o due nomi comuni del certificato del server.</span><span class="sxs-lookup"><span data-stu-id="38032-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="38032-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="38032-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="38032-145">Si tratta di un set di certificati che da installare nei client autenticati.</span><span class="sxs-lookup"><span data-stu-id="38032-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="38032-146">È possibile avere diversi certificati client installati nei computer a cui si vuole consentire l'accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="38032-147">Impostare l'identificazione personale di ogni certificato nella variabile **CertificateThumbprint** .</span><span class="sxs-lookup"><span data-stu-id="38032-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="38032-148">Se si imposta **IsAdmin** su *true*, il client in cui è installato questo certificato può eseguire attività di gestione degli amministratori per il cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="38032-149">Se **IsAdmin** è *false*, il client con questo certificato può eseguire solo le azioni consentite con diritti di accesso utente, in genere di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="38032-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="38032-150">Per altre informazioni sui ruoli, vedere [Controllo degli accessi in base al ruolo (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="38032-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="38032-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="38032-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="38032-152">Impostare il nome comune del primo certificato client per **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="38032-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="38032-153">**CertificateIssuerThumbprint** è l'identificazione personale dell'autorità emittente del certificato.</span><span class="sxs-lookup"><span data-stu-id="38032-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="38032-154">Per altre informazioni sui nomi comuni e sull'autorità emittente, vedere [Utilizzo dei certificati](https://msdn.microsoft.com/library/ms731899.aspx) .</span><span class="sxs-lookup"><span data-stu-id="38032-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="38032-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="38032-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="38032-156">Consigliato per l'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38032-156">Recommended for test environment.</span></span> <span data-ttu-id="38032-157">Si tratta di un certificato facoltativo che è possibile specificare se si vuole proteggere il [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="38032-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="38032-158">Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes.</span><span class="sxs-lookup"><span data-stu-id="38032-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="38032-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="38032-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="38032-160">Consigliato per l'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="38032-160">Recommended for production environment.</span></span> <span data-ttu-id="38032-161">Si tratta di un certificato facoltativo che è possibile specificare se si vuole proteggere il [proxy inverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="38032-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="38032-162">Se si usa questo certificato, assicurarsi che reverseProxyEndpointPort sia impostato in nodeTypes.</span><span class="sxs-lookup"><span data-stu-id="38032-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="38032-163">Ecco un esempio di una configurazione cluster in cui sono stati specificati certificati cluster, server e client.</span><span class="sxs-lookup"><span data-stu-id="38032-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="38032-164">Si noti che per i certificati del cluster/server/proxy inverso, non è consentito configurare insieme l'identificazione personale e il nome comune per lo stesso tipo di certificato.</span><span class="sxs-lookup"><span data-stu-id="38032-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

## <a name="certificate-roll-over"></a><span data-ttu-id="38032-165">Rollover del certificato</span><span class="sxs-lookup"><span data-stu-id="38032-165">Certificate roll over</span></span>
<span data-ttu-id="38032-166">Quando si usa il nome comune del certificato al posto dell'identificazione personale, il rollover del certificato non richiede l'aggiornamento della configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="38032-167">Se il rollover del certificato implica il rollover dell'autorità di certificazione, mantenere il certificato dell'autorità di certificazione precedente nell'archivio del certificato per almeno 2 ore dopo aver installato il nuovo certificato dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="38032-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="38032-168">Acquisire i certificati X.509</span><span class="sxs-lookup"><span data-stu-id="38032-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="38032-169">Per proteggere la comunicazione nel cluster, è prima necessario ottenere i certificati X.509 per i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="38032-170">Per limitare inoltre la connessione al cluster a computer o utenti autorizzati, è necessario ottenere e installare i certificati per i computer client.</span><span class="sxs-lookup"><span data-stu-id="38032-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="38032-171">Per proteggere i cluster che eseguono carichi di lavoro di produzione, è consigliabile usare un certificato X.509 firmato da un' [autorità di certificazione (CA)](https://en.wikipedia.org/wiki/Certificate_authority) .</span><span class="sxs-lookup"><span data-stu-id="38032-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="38032-172">Per informazioni dettagliate su come ottenere questi certificati, vedere [Procedura: ottenere un certificato (WCF)](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="38032-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="38032-173">Per i cluster usati solo a scopo di test, si può scegliere di usare un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="38032-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="38032-174">Facoltativo: creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="38032-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="38032-175">Un modo per creare un certificato autofirmato che possa essere protetto correttamente consiste nell'usare lo script *CertSetup.ps1* della cartella Service Fabric SDK nella directory *C:\Programmi\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="38032-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="38032-176">Modificare questo file per cambiare il nome predefinito del certificato (cercare il valore *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="38032-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="38032-177">Eseguire questo script come `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="38032-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="38032-178">Esportare ora il certificato in un file PFX con una password protetta.</span><span class="sxs-lookup"><span data-stu-id="38032-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="38032-179">Ottenere per prima cosa l'identificazione personale del certificato.</span><span class="sxs-lookup"><span data-stu-id="38032-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="38032-180">Dal menu *Start* eseguire *Gestisci i certificati computer*.</span><span class="sxs-lookup"><span data-stu-id="38032-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="38032-181">Passare alla cartella **Computer locale\Personale** e cercare il certificato appena creato.</span><span class="sxs-lookup"><span data-stu-id="38032-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="38032-182">Fare doppio clic sul certificato per aprirlo, selezionare la scheda *Dettagli* e quindi scorrere verso il basso fino al campo *Identificazione personale*.</span><span class="sxs-lookup"><span data-stu-id="38032-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="38032-183">Copiare il valore dell'identificazione personale nel comando PowerShell di seguito, dopo aver rimosso gli spazi.</span><span class="sxs-lookup"><span data-stu-id="38032-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="38032-184">Modificare il valore `String` in una password sicura idonea di protezione ed eseguire quanto segue in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="38032-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="38032-185">Per visualizzare i dettagli di un certificato installato nel computer, è possibile eseguire il comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="38032-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="38032-186">In alternativa, se si dispone di una sottoscrizione di Azure, vedere la sezione [Aggiungere i certificati all'insieme di credenziali delle chiavi](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="38032-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="38032-187">Installare i certificati</span><span class="sxs-lookup"><span data-stu-id="38032-187">Install the certificates</span></span>
<span data-ttu-id="38032-188">Dopo aver ottenuto i certificati, è possibile installarli nei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="38032-189">È necessario che nei nodi sia già installata la versione più recente di Windows PowerShell 3.x.</span><span class="sxs-lookup"><span data-stu-id="38032-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="38032-190">È necessario ripetere questi passaggi in ogni nodo, sia per i certificati cluster e server che per gli eventuali certificati secondari.</span><span class="sxs-lookup"><span data-stu-id="38032-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="38032-191">Copiare i file PFX nel nodo.</span><span class="sxs-lookup"><span data-stu-id="38032-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="38032-192">Aprire una finestra di PowerShell come amministratore e immettere i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="38032-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="38032-193">Sostituire *$pswd* con la password usata per creare il certificato.</span><span class="sxs-lookup"><span data-stu-id="38032-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="38032-194">Sostituire *$PfxFilePath* con il percorso completo del file PFX copiato nel nodo.</span><span class="sxs-lookup"><span data-stu-id="38032-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="38032-195">Impostare ora il controllo di accesso per questo certificato in modo che possa essere usato dal processo di Service Fabric, eseguito con l'account Servizio di rete, con lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="38032-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="38032-196">Specificare l'identificazione personale del certificato e "NETWORK SERVICE" come account del servizio.</span><span class="sxs-lookup"><span data-stu-id="38032-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="38032-197">È possibile controllare che gli ACL per il certificato siano corretti aprendo il certificato in *Start* > *Gestisci i certificati computer* ed esaminando *Tutte le attività* > *Gestisci chiavi private*.</span><span class="sxs-lookup"><span data-stu-id="38032-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="38032-198">Ripetere i passaggi precedenti per ogni certificato del server.</span><span class="sxs-lookup"><span data-stu-id="38032-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="38032-199">Questa procedura può essere usata anche per installare i certificati client nei computer a cui si vuole consentire l'accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="38032-200">Creare il cluster sicuro</span><span class="sxs-lookup"><span data-stu-id="38032-200">Create the secure cluster</span></span>
<span data-ttu-id="38032-201">Dopo aver configurato la sezione **sicurezza** del file **ClusterConfig.X509.MultiMachine.json**, passare alla sezione [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) (Crea il cluster) per configurare i nodi e creare il cluster autonomo.</span><span class="sxs-lookup"><span data-stu-id="38032-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="38032-202">Ricordarsi di usare il file **ClusterConfig.X509.MultiMachine.json** mentre si crea il cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="38032-203">Ad esempio, il comando può essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="38032-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="38032-204">Quando il cluster Windows autonomo sicuro è in esecuzione e sono stati configurati i client autenticati per la connessione al cluster, vedere la sezione [Connect to a secure cluster using PowerShell (Connettersi a un cluster sicuro mediante PowerShell)](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) per stabilire la connessione.</span><span class="sxs-lookup"><span data-stu-id="38032-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="38032-205">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="38032-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="38032-206">È quindi possibile eseguire altri comandi di PowerShell per usare questo cluster.</span><span class="sxs-lookup"><span data-stu-id="38032-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="38032-207">È possibile, ad esempio, usare il comando [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) per visualizzare un elenco di nodi nel cluster protetto.</span><span class="sxs-lookup"><span data-stu-id="38032-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="38032-208">Per rimuovere il cluster, connettersi al nodo del cluster in cui è stato scaricato il pacchetto di Service Fabric, aprire una riga di comando e passare alla cartella del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="38032-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="38032-209">Eseguire ora il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="38032-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="38032-210">La configurazione non corretta del certificato può impedire la visualizzazione del cluster durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="38032-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="38032-211">Per diagnosticare automaticamente problemi di sicurezza, consultare il gruppo di Visualizzatore eventi *Registri applicazioni e servizi* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="38032-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

