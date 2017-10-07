---
title: aaaDeploy host Docker remoto un ASP.NET Core Linux Docker contenitore tooa | Documenti Microsoft
description: Informazioni su come toouse Visual Studio Tools per Docker toodeploy un Core di ASP.NET web contenitori di Docker tooa app in esecuzione in una macchina virtuale Linux di Azure Docker Host
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Distribuire un host di Docker remoto ASP.NET contenitore tooa
## <a name="overview"></a>Panoramica
Docker è un motore di contenitore leggero, simile per alcuni macchina virtuale tooa modi, che è possibile utilizzare toohost applicazioni e servizi.
In questa esercitazione illustra utilizzando hello [Visual Studio Tools per Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) toodeploy estensione un host di ASP.NET Core app tooa Docker in Azure tramite PowerShell.

## <a name="prerequisites"></a>Prerequisiti
esempio Hello è toocomplete necessari in questa esercitazione:

* Creare una macchina virtuale Host Docker di Azure, come descritto in [come toouse docker-computer con Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Installare una versione più recente di hello di [Visual Studio](https://www.visualstudio.com/downloads/)
* Scaricare hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* Installare [Docker per Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Creare un'app Web ASP.NET Core
Hello passaggi seguenti illustrano come creare un'applicazione ASP.NET Core di base che verrà utilizzata in questa esercitazione.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Aggiungere il supporto di Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Utilizzare uno Script di PowerShell DockerTask.ps1 hello
1. Aprire una directory radice toohello prompt dei comandi di PowerShell del progetto. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Convalidare host remoto hello è in esecuzione. Dovrebbe essere visualizzato lo stato = Running 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Compilazione hello app usando hello - parametro di compilazione
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Eseguire app hello, utilizzando hello - parametro di esecuzione
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Al termine del processo di docker, verrà visualizzato risultati simili toohello segue:
   
   ![Visualizzare l'app][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
