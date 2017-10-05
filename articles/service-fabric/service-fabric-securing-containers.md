---
title: Sicurezza del contenitore di Azure Service Fabric | Microsoft Docs
description: Informazioni su come proteggere i servizi del contenitore.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a><span data-ttu-id="04ac9-103">Sicurezza del contenitore</span><span class="sxs-lookup"><span data-stu-id="04ac9-103">Container security</span></span>

<span data-ttu-id="04ac9-104">Service Fabric fornisce un meccanismo per i servizi all'interno di un contenitore per accedere a un certificato che viene installato nei nodi in un cluster di Windows o Linux (versione 5.7 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="04ac9-104">Service Fabric provides a mechanism for services inside a container to access a certificate that is installed on the nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="04ac9-105">Service Fabric supporta anche gMSA (account del servizio gestito del gruppo) per i contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="04ac9-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="04ac9-106">Gestione dei certificati per i contenitori</span><span class="sxs-lookup"><span data-stu-id="04ac9-106">Certificate management for containers</span></span>

<span data-ttu-id="04ac9-107">È possibile proteggere i servizi del contenitore specificando un certificato.</span><span class="sxs-lookup"><span data-stu-id="04ac9-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="04ac9-108">Questo certificato deve essere installato sui nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="04ac9-108">The certificate must be installed on the nodes of the cluster.</span></span> <span data-ttu-id="04ac9-109">Le informazioni del certificato vengono fornite nel manifesto dell'applicazione sotto il tag `ContainerHostPolicies` come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="04ac9-109">The certificate information is provided in the application manifest under the `ContainerHostPolicies` tag as the following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="04ac9-110">All'avvio dell'applicazione, il runtime legge i certificati e genera un file PFX e una password per ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="04ac9-110">When starting the application, the runtime reads the certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="04ac9-111">Il file PFX e la password sono accessibili all'interno del contenitore usando le variabili di ambiente seguenti:</span><span class="sxs-lookup"><span data-stu-id="04ac9-111">This PFX file and password are accessible inside the container using the following environment variables:</span></span> 

* <span data-ttu-id="04ac9-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="04ac9-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="04ac9-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="04ac9-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="04ac9-114">Il servizio del contenitore o del processo è responsabile dell'importazione del file PFX nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="04ac9-114">The container service or process is responsible for importing the PFX file into the container.</span></span> <span data-ttu-id="04ac9-115">Per importare il certificato, è possibile usare gli script `setupentrypoint.sh` o il codice personalizzato in esecuzione all'interno del processo del contenitore.</span><span class="sxs-lookup"><span data-stu-id="04ac9-115">To import the certificate, you can use `setupentrypoint.sh` scripts or executed custom code within the container process.</span></span> <span data-ttu-id="04ac9-116">Codice di esempio in C# per l'importazione del file PFX seguente:</span><span class="sxs-lookup"><span data-stu-id="04ac9-116">Sample code in C# for importing the PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="04ac9-117">Questo certificato PFX può essere usato per autenticare l'applicazione o il servizio o per proteggere la comunicazione con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="04ac9-117">This PFX certificate can be used for authenticate the application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="04ac9-118">Configurare gMSA per i contenitori di Windows</span><span class="sxs-lookup"><span data-stu-id="04ac9-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="04ac9-119">Per configurare gMSA (account del servizio gestito del gruppo), un file di specifica delle credenziali (`credspec`) viene posizionato in tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="04ac9-119">To set up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in the cluster.</span></span> <span data-ttu-id="04ac9-120">Il file può essere copiato in tutti i nodi tramite un'estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="04ac9-120">The file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="04ac9-121">Il file `credspec` deve contenere le informazioni dell'account gMSA.</span><span class="sxs-lookup"><span data-stu-id="04ac9-121">The `credspec` file must contain the gMSA account information.</span></span> <span data-ttu-id="04ac9-122">Per altre informazioni sul file `credspec`, vedere [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts) (Account del servizio).</span><span class="sxs-lookup"><span data-stu-id="04ac9-122">For more information on the `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="04ac9-123">La specifica della credenziale e il tag `Hostname` vengono specificati nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="04ac9-123">The credential specification and the `Hostname` tag are specified in the application manifest.</span></span> <span data-ttu-id="04ac9-124">Il tag `Hostname` deve corrispondere al nome dell'account gMSA in cui viene eseguito il contenitore.</span><span class="sxs-lookup"><span data-stu-id="04ac9-124">The `Hostname` tag must match the gMSA account name that the container runs under.</span></span>  <span data-ttu-id="04ac9-125">Il tag `Hostname` consente al contenitore di autenticarsi presso altri servizi nel dominio tramite l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="04ac9-125">The `Hostname` tag allows the container to authenticate itself to other services in the domain using Kerberos authentication.</span></span>  <span data-ttu-id="04ac9-126">Un esempio per specificare `Hostname` e `credspec` nel manifesto dell'applicazione è illustrato nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="04ac9-126">A sample for specifying the `Hostname` and the `credspec` in the application manifest is shown in the following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="04ac9-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04ac9-127">Next steps</span></span>

* [<span data-ttu-id="04ac9-128">Distribuire un contenitore Windows in Service Fabric su Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="04ac9-128">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="04ac9-129">Distribuire un contenitore Docker in Service Fabric su Linux</span><span class="sxs-lookup"><span data-stu-id="04ac9-129">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
