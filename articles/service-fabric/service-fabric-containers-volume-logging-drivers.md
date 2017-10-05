---
title: Anteprima di Docker Compose di Azure Service Fabric | Microsoft Docs
description: "Azure Service Fabric accetta il formato Docker Compose per semplificare l'orchestrazione di contenitori esistenti usando Service Fabric. Questo supporto è attualmente disponibile in versione di anteprima."
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
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="b2e47-104">Specifica di plug-in di volume e driver di registrazione per il contenitore</span><span class="sxs-lookup"><span data-stu-id="b2e47-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="b2e47-105">Service Fabric supporta la specifica di [plug-in di volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) e i [driver di registrazione Docker](https://docs.docker.com/engine/admin/logging/overview/) per il servizio di contenitore.</span><span class="sxs-lookup"><span data-stu-id="b2e47-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="b2e47-106">I plug-in sono specificati nel manifesto dell'applicazione, come illustrato nel manifesto seguente:</span><span class="sxs-lookup"><span data-stu-id="b2e47-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="b2e47-107">Nell'esempio precedente, il tag `Source` per `Volume` fa riferimento alla cartella di origine.</span><span class="sxs-lookup"><span data-stu-id="b2e47-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="b2e47-108">La cartella di origine potrebbe essere una cartella nella macchina virtuale che ospita i contenitori o un archivio remoto persistente.</span><span class="sxs-lookup"><span data-stu-id="b2e47-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="b2e47-109">Il tag `Destination` è il percorso in cui viene eseguito il mapping di `Source` all'interno del contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b2e47-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="b2e47-110">Quando si specifica un plug-in di un volume, Service Fabric crea automaticamente il volume usando i parametri specificati.</span><span class="sxs-lookup"><span data-stu-id="b2e47-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="b2e47-111">Il tag `Source` è il nome del volume e il tag `Driver` specifica il plug-in del driver del volume.</span><span class="sxs-lookup"><span data-stu-id="b2e47-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="b2e47-112">Le opzioni possono essere specificate usando il tag `DriverOption`, come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b2e47-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="b2e47-113">Se viene specificato un driver di registro Docker, è necessario distribuire gli agenti o i contenitori per gestire i registri nel cluster.</span><span class="sxs-lookup"><span data-stu-id="b2e47-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="b2e47-114">Il tag `DriverOption` può essere usato anche per specificare le opzioni del driver di log.</span><span class="sxs-lookup"><span data-stu-id="b2e47-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="b2e47-115">Vedere gli articoli seguenti per distribuire i contenitori a un cluster Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="b2e47-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="b2e47-116">Distribuire un contenitore in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b2e47-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

