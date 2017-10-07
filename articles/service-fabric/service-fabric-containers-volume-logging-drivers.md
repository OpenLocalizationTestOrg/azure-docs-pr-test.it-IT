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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Specifica di plug-in di volume e driver di registrazione per il contenitore

Service Fabric supporta la specifica di [plug-in di volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) e i [driver di registrazione Docker](https://docs.docker.com/engine/admin/logging/overview/) per il servizio di contenitore. Hello i plug-in vengono specificati nel manifesto dell'applicazione hello, come illustrato nel seguente manifesto hello:


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

In hello sopra riportato, hello `Source` tag per hello `Volume` fa riferimento la cartella di origine toohello. cartella di origine Hello potrebbe essere una cartella nella macchina virtuale che ospita i contenitori di hello o un archivio remoto permanente hello. Hello `Destination` tag è percorso hello hello `Source` è mappato toowithin hello contenitore in esecuzione. 

Quando si specifica un plug-in di volume, Service Fabric crea automaticamente il volume di hello usando hello parametri specificati. Hello `Source` tag è il nome di hello del volume hello e hello `Driver` tag specifica plug-in di hello volume driver. È possibile specificare opzioni utilizzando hello `DriverOption` come illustrato nel seguente frammento di codice hello:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Se viene specificato un driver di log di Docker, è necessario toodeploy hello toohandle agenti (o contenitori) registra nel cluster hello.  Hello `DriverOption` tag può essere anche opzioni di driver log toospecify utilizzato.

Fare riferimento toohello cluster di Service Fabric tooa contenitori toodeploy gli articoli seguenti:


[Distribuire un contenitore in Service Fabric](service-fabric-deploy-container.md)

