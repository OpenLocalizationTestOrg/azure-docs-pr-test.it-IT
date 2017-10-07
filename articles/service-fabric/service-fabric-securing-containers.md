---
title: sicurezza di Service Fabric contenitore aaaAzure | Documenti Microsoft
description: Informazioni su toosecure ora i servizi di contenitore.
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
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="0ab6c-103">Sicurezza del contenitore</span><span class="sxs-lookup"><span data-stu-id="0ab6c-103">Container security</span></span>

<span data-ttu-id="0ab6c-104">Service Fabric fornisce un meccanismo per i servizi all'interno di un contenitore di tooaccess un certificato installato nei nodi hello in un cluster di Windows o Linux (versione 5.7 o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="0ab6c-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="0ab6c-105">Service Fabric supporta anche gMSA (account del servizio gestito del gruppo) per i contenitori di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="0ab6c-106">Gestione dei certificati per i contenitori</span><span class="sxs-lookup"><span data-stu-id="0ab6c-106">Certificate management for containers</span></span>

<span data-ttu-id="0ab6c-107">È possibile proteggere i servizi del contenitore specificando un certificato.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="0ab6c-108">Hello certificato deve essere installato sui nodi del cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="0ab6c-109">Hello informazioni del certificato viene fornite nel manifesto dell'applicazione hello in hello `ContainerHostPolicies` tag come hello seguente mostra:</span><span class="sxs-lookup"><span data-stu-id="0ab6c-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="0ab6c-110">Quando si avvia un'applicazione hello, hello runtime legge certificati hello e genera un file PFX e una password per ogni certificato.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="0ab6c-111">Il file PFX e la password sono accessibili nel contenitore hello utilizzando hello seguenti variabili di ambiente:</span><span class="sxs-lookup"><span data-stu-id="0ab6c-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="0ab6c-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="0ab6c-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="0ab6c-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="0ab6c-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="0ab6c-114">il servizio di contenitore Hello o un processo è responsabile per l'importazione di file PFX hello in contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="0ab6c-115">certificato di hello tooimport, è possibile utilizzare `setupentrypoint.sh` script o codice personalizzato all'interno di processo del contenitore hello eseguita.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="0ab6c-116">Codice di esempio in c# per l'importazione di file PFX hello segue:</span><span class="sxs-lookup"><span data-stu-id="0ab6c-116">Sample code in C# for importing hello PFX file follows:</span></span>

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
<span data-ttu-id="0ab6c-117">Questo certificato PFX può essere utilizzato per autenticare un'applicazione hello o servizio oppure commmunication sicuro con altri servizi.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="0ab6c-118">Configurare gMSA per i contenitori di Windows</span><span class="sxs-lookup"><span data-stu-id="0ab6c-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="0ab6c-119">tooset backup gMSA (group Managed Service Accounts), un file di specifica delle credenziali (`credspec`) viene inserito in tutti i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="0ab6c-120">file Hello può essere copiati in tutti i nodi utilizzando un'estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="0ab6c-121">Hello `credspec` file deve contenere le informazioni di account gMSA hello.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="0ab6c-122">Per ulteriori informazioni su hello `credspec` file, vedere [gli account del servizio](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="0ab6c-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="0ab6c-123">Specifica credenziali Hello e hello `Hostname` tag specificati nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="0ab6c-124">Hello `Hostname` tag deve corrispondere a nome di account gMSA hello che hello contenitore viene eseguito in.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="0ab6c-125">Hello `Hostname` tag consente hello contenitore tooauthenticate stesso tooother servizi nel dominio hello mediante l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0ab6c-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="0ab6c-126">Un esempio per la specifica di hello `Hostname` hello e `credspec` in hello manifesto dell'applicazione è illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="0ab6c-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="0ab6c-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ab6c-127">Next steps</span></span>

* [<span data-ttu-id="0ab6c-128">Distribuire un tooService di contenitore di Windows Fabric in Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0ab6c-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="0ab6c-129">Distribuire un tooService contenitore Docker dell'infrastruttura in Linux</span><span class="sxs-lookup"><span data-stu-id="0ab6c-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
