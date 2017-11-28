---
title: aaaAzure Service Fabric Docker comporre Preview | Documenti Microsoft
description: "Azure Service Fabric accetta Docker Compose toomake formato è più facile tooorchestrate exsiting contenitori di usando Service Fabric. Questo supporto è attualmente disponibile in versione di anteprima."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="34f74-104">Specifica di plug-in di volume e driver di registrazione per il contenitore</span><span class="sxs-lookup"><span data-stu-id="34f74-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="34f74-105">Service Fabric supporta la specifica di [plug-in di volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) e i [driver di registrazione Docker](https://docs.docker.com/engine/admin/logging/overview/) per il servizio di contenitore.</span><span class="sxs-lookup"><span data-stu-id="34f74-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="34f74-106">Hello i plug-in vengono specificati nel manifesto dell'applicazione hello, come illustrato nel seguente manifesto hello:</span><span class="sxs-lookup"><span data-stu-id="34f74-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


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

<span data-ttu-id="34f74-107">In hello sopra riportato, hello `Source` tag per hello `Volume` fa riferimento la cartella di origine toohello.</span><span class="sxs-lookup"><span data-stu-id="34f74-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="34f74-108">cartella di origine Hello potrebbe essere una cartella nella macchina virtuale che ospita i contenitori di hello o un archivio remoto permanente hello.</span><span class="sxs-lookup"><span data-stu-id="34f74-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="34f74-109">Hello `Destination` tag è percorso hello hello `Source` è mappato toowithin hello contenitore in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="34f74-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="34f74-110">Quando si specifica un plug-in di volume, Service Fabric crea automaticamente il volume di hello usando hello parametri specificati.</span><span class="sxs-lookup"><span data-stu-id="34f74-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="34f74-111">Hello `Source` tag è il nome di hello del volume hello e hello `Driver` tag specifica plug-in di hello volume driver.</span><span class="sxs-lookup"><span data-stu-id="34f74-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="34f74-112">È possibile specificare opzioni utilizzando hello `DriverOption` come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="34f74-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="34f74-113">Se viene specificato un driver di log di Docker, è necessario toodeploy hello toohandle agenti (o contenitori) registra nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="34f74-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="34f74-114">Hello `DriverOption` tag può essere anche opzioni di driver log toospecify utilizzato.</span><span class="sxs-lookup"><span data-stu-id="34f74-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="34f74-115">Fare riferimento toohello cluster di Service Fabric tooa contenitori toodeploy gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="34f74-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="34f74-116">Distribuire un contenitore in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="34f74-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

