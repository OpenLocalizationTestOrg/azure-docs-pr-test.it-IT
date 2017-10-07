---
title: le impostazioni di FabricTransport aaaChange in Azure microservizi | Documenti Microsoft
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
ms.openlocfilehash: e312b475407eb95a435b93d80c0f2e9618b9ea1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="da502-103">Configurare le impostazioni di FabricTransport per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="da502-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="da502-104">Ecco le impostazioni di hello che è possibile configurare:</span><span class="sxs-lookup"><span data-stu-id="da502-104">Here are hello settings that you can configure:</span></span>
- <span data-ttu-id="da502-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="da502-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="da502-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="da502-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="da502-107">È possibile modificare una configurazione predefinita di hello di FabricTransport nei modi seguenti.</span><span class="sxs-lookup"><span data-stu-id="da502-107">You can modify hello default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="da502-108">Attributo assembly</span><span class="sxs-lookup"><span data-stu-id="da502-108">Assembly attribute</span></span>

<span data-ttu-id="da502-109">Hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attributo necessario toobe applicato in assembly del servizio client e l'attore hello attore.</span><span class="sxs-lookup"><span data-stu-id="da502-109">hello [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs toobe applied on hello actor client and actor service assemblies.</span></span>

<span data-ttu-id="da502-110">Hello di esempio seguente viene illustrato come toochange hello il valore predefinito delle impostazioni FabricTransport OperationTimeout:</span><span class="sxs-lookup"><span data-stu-id="da502-110">hello following example shows how toochange hello default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="da502-111">Il secondo esempio modifica i valori predefiniti di FabricTransport MaxMessageSize e OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="da502-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="da502-112">Pacchetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="da502-112">Config package</span></span>

<span data-ttu-id="da502-113">È possibile utilizzare un [pacchetto di configurazione](service-fabric-application-model.md) configurazione predefinita di toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="da502-113">You can use a [config package](service-fabric-application-model.md) toomodify hello default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-hello-actor-service"></a><span data-ttu-id="da502-114">Configurare le impostazioni di FabricTransport per servizio actor hello</span><span class="sxs-lookup"><span data-stu-id="da502-114">Configure FabricTransport settings for hello actor service</span></span>

<span data-ttu-id="da502-115">Aggiungere una sezione TransportSettings nel file Settings hello.</span><span class="sxs-lookup"><span data-stu-id="da502-115">Add a TransportSettings section in hello settings.xml file.</span></span>

<span data-ttu-id="da502-116">Per impostazione predefinita, il codice attore cerca il nome sezione "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="da502-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="da502-117">Se non viene trovato, cerca il SectionName "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="da502-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

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

### <a name="configure-fabrictransport-settings-for-hello-actor-client-assembly"></a><span data-ttu-id="da502-118">Configurare le impostazioni di FabricTransport per assembly client di hello attore</span><span class="sxs-lookup"><span data-stu-id="da502-118">Configure FabricTransport settings for hello actor client assembly</span></span>

<span data-ttu-id="da502-119">Se il client di hello non è in esecuzione come parte di un servizio, è possibile creare un "&lt;Nome Exe Client&gt;. Settings" file in hello stesso percorso del file di .exe hello client.</span><span class="sxs-lookup"><span data-stu-id="da502-119">If hello client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in hello same location as hello client .exe file.</span></span> <span data-ttu-id="da502-120">Aggiungere quindi una sezione TransportSettings in tale file.</span><span class="sxs-lookup"><span data-stu-id="da502-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="da502-121">SectionName deve essere "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="da502-121">SectionName should be "TransportSettings".</span></span>

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

  * <span data-ttu-id="da502-122">Configurazione delle impostazioni di FabricTransport per il client/servizio Actor protetto con certificato secondario.</span><span class="sxs-lookup"><span data-stu-id="da502-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="da502-123">È possibile aggiungere informazioni sul certificato secondario aggiungendo il parametro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="da502-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="da502-124">Di seguito è riportato hello per hello TransportSettings Listener.</span><span class="sxs-lookup"><span data-stu-id="da502-124">Below is hello example for hello Listener TransportSettings.</span></span>

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
     <span data-ttu-id="da502-125">Di seguito è riportato hello per hello Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="da502-125">Below is hello example for hello Client TransportSettings.</span></span>

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
    * <span data-ttu-id="da502-126">Configurazione delle impostazioni di FabricTransport per il client/servizio Actor protetto usando il nome oggetto.</span><span class="sxs-lookup"><span data-stu-id="da502-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="da502-127">Utente esigenze tooprovide findType come FindBySubjectName, aggiungere i valori CertificateIssuerThumbprints e CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="da502-127">User needs tooprovide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="da502-128">Di seguito è riportato hello per hello TransportSettings Listener.</span><span class="sxs-lookup"><span data-stu-id="da502-128">Below is hello example for hello Listener TransportSettings.</span></span>

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
  <span data-ttu-id="da502-129">Di seguito è riportato hello per hello Client TransportSettings.</span><span class="sxs-lookup"><span data-stu-id="da502-129">Below is hello example for hello Client TransportSettings.</span></span>

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
