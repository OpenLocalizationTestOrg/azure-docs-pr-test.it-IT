---
title: Modificare le impostazioni di FabricTransport nei microservizi di Azure | Microsoft Docs
description: Informazioni sulla configurazione delle impostazioni di comunicazione degli attori di Service Fabric di Azure.
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="5447c-103">Configurare le impostazioni di FabricTransport per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="5447c-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="5447c-104">Ecco le impostazioni che possono essere configurate:</span><span class="sxs-lookup"><span data-stu-id="5447c-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="5447c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="5447c-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="5447c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="5447c-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="5447c-107">È possibile modificare la configurazione predefinita di FabricTransport nei modi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5447c-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="5447c-108">Attributo assembly</span><span class="sxs-lookup"><span data-stu-id="5447c-108">Assembly attribute</span></span>

<span data-ttu-id="5447c-109">L'attributo [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) deve essere applicato negli assembly del client attore e del servizio attore.</span><span class="sxs-lookup"><span data-stu-id="5447c-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="5447c-110">L'esempio seguente illustra come modificare il valore predefinito delle impostazioni OperationTimeout di FabricTransport:</span><span class="sxs-lookup"><span data-stu-id="5447c-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="5447c-111">Il secondo esempio modifica i valori predefiniti di FabricTransport MaxMessageSize e OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="5447c-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="5447c-112">Pacchetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="5447c-112">Config package</span></span>

<span data-ttu-id="5447c-113">È possibile usare un [pacchetto di configurazione](service-fabric-application-model.md) per modificare la configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5447c-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="5447c-114">Configurare le impostazioni di FabricTransport per il servizio attore</span><span class="sxs-lookup"><span data-stu-id="5447c-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="5447c-115">Aggiungere una sezione TransportSettings nel file settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5447c-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="5447c-116">Per impostazione predefinita, il codice attore cerca il nome sezione "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5447c-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="5447c-117">Se non viene trovato, cerca il SectionName "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5447c-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="5447c-118">Configurare le impostazioni di FabricTransport per l'assembly del client attore</span><span class="sxs-lookup"><span data-stu-id="5447c-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="5447c-119">Se il client non è in esecuzione come parte di un servizio, è possibile creare un file XML "&lt;Nome EXE client&gt;.settings.xml" nello stesso percorso in cui si trova il file client .exe.</span><span class="sxs-lookup"><span data-stu-id="5447c-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="5447c-120">Aggiungere quindi una sezione TransportSettings in tale file.</span><span class="sxs-lookup"><span data-stu-id="5447c-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="5447c-121">SectionName deve essere "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="5447c-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="5447c-122">Configurazione delle impostazioni di FabricTransport per il client/servizio Actor protetto con certificato secondario.</span><span class="sxs-lookup"><span data-stu-id="5447c-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="5447c-123">È possibile aggiungere informazioni sul certificato secondario aggiungendo il parametro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="5447c-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="5447c-124">L'esempio seguente riguarda TransportSettings del listener.</span><span class="sxs-lookup"><span data-stu-id="5447c-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="5447c-125">L'esempio seguente riguarda TransportSettings del client.</span><span class="sxs-lookup"><span data-stu-id="5447c-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="5447c-126">Configurazione delle impostazioni di FabricTransport per il client/servizio Actor protetto usando il nome oggetto.</span><span class="sxs-lookup"><span data-stu-id="5447c-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="5447c-127">L'utente deve fornire findType come FindBySubjectName e aggiungere i valori di CertificateIssuerThumbprints e CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="5447c-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="5447c-128">L'esempio seguente riguarda TransportSettings del listener.</span><span class="sxs-lookup"><span data-stu-id="5447c-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="5447c-129">L'esempio seguente riguarda TransportSettings del client.</span><span class="sxs-lookup"><span data-stu-id="5447c-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
