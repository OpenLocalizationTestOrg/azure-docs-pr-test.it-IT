---
title: aaaSet un ambiente di sviluppo per Azure microservizi | Documenti Microsoft
description: "Installare il runtime di hello, SDK e strumenti e creare un cluster di sviluppo locale. Dopo aver completato il programma di installazione, sarà pronto toobuild applicazioni."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a>Preparare l'ambiente di sviluppo
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 toobuild ed eseguire [applicazioni Azure Service Fabric] [ 1] nel computer di sviluppo, installare il runtime di hello, SDK e strumenti. È inoltre necessario tooenable esecuzione degli script di Windows PowerShell hello incluso in hello SDK.

## <a name="prerequisites"></a>Prerequisiti
### <a name="supported-operating-system-versions"></a>Versioni del sistema operativo supportate
Hello seguenti versioni del sistema operativo è supportato per lo sviluppo:

* Windows 7
* Windows 8 e Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Per impostazione predefinita, Windows 7 include solo Windows PowerShell 2.0. I cmdlet di PowerShell per Service Fabric richiedono PowerShell 3.0 o versione successiva. È possibile [scaricare Windows PowerShell 5.0] [ powershell5-download] da hello Microsoft Download Center.
> 
> 

## <a name="install-hello-sdk-and-tools"></a>Installare gli strumenti e SDK hello
### <a name="toouse-visual-studio-2017"></a>toouse 2017 di Visual Studio
Strumenti di Service Fabric fanno parte di hello Azure sviluppo e gestione del carico di lavoro in Visual Studio 2017. Abilitare questo carico di lavoro durante l'installazione di Visual Studio.
Inoltre, è necessario tooinstall hello Microsoft Azure Service Fabric SDK, tramite l'installazione guidata piattaforma Web.

* [Installare Microsoft Azure Service Fabric SDK hello][core-sdk]

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>toouse Visual Studio 2015 (richiede Visual Studio 2015 Update 2 o versioni successive)
Per Visual Studio 2015, gli strumenti di Service Fabric vengono installati insieme a SDK, tramite l'installazione guidata piattaforma Web hello hello:

* [Installare Microsoft Azure Service Fabric SDK hello e strumenti][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>Installazione solo dell'SDK
Se è necessario solo hello SDK, è possibile installare questo pacchetto:
* [Installare Microsoft Azure Service Fabric SDK hello][core-sdk]

le versioni correnti di Hello sono:
* Service Fabric SDK 2.7.198
* Runtime di Service Fabric 5.7.198
* Strumenti di Service Fabric per Visual Studio 2015 1.7.50721
* Visual Studio 2017 Update 2 include Strumenti di Service Fabric per Visual Studio 1.6.20170504
* Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) include Strumenti di Service Fabric per Visual Studio 1.7.20170721

Per un elenco delle versioni supportate, vedere [Service Fabric support](service-fabric-support.md) (Supporto di Service Fabric)

## <a name="enable-powershell-script-execution"></a>Consentire l'esecuzione di script di PowerShell
Service Fabric usa script di Windows PowerShell per creare un cluster di sviluppo locale e per distribuire le applicazioni da Visual Studio. Per impostazione predefinita, Windows blocca l'esecuzione di questi script. tooenable usarle, è necessario modificare i criteri di esecuzione di PowerShell. Aprire PowerShell come amministratore e immettere hello comando seguente:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Passaggi successivi
Dopo avere configurato l'ambiente di sviluppo, iniziare a compilare ed eseguire le app.

* [Creare la prima applicazione Infrastruttura di servizi in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Informazioni su come toodeploy e gestire le applicazioni nel cluster locale](service-fabric-get-started-with-a-local-cluster.md)
* [Informazioni sui modelli di programmazione hello: servizi affidabili e Reliable Actors](service-fabric-choose-framework.md)
* [Vedere gli esempi di codice su GitHub hello Service Fabric](https://aka.ms/servicefabricsamples)
* [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Seguire hello tooget percorso di apprendimento una piattaforma toohello introduzione esaustiva di Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Pagina della campagna di Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Collegamento WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Collegamento WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Collegamento WebPI Core SDK"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
