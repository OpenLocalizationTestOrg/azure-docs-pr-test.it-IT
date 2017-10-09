---
title: aaaAutomate distribuzione dell'applicazione Azure con gli strumenti da riga di comando | Documenti Microsoft
description: Individuare le informazioni su come distribuire l'app di Azure da hello della riga di comando
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatizzare la distribuzione di un'app di Azure con gli strumenti da riga di comando
È possibile automatizzare la distribuzione di un'app di Azure con gli strumenti da riga di comando. Questo articolo vengono elencati gli strumenti disponibili e collegamenti utili hello che mostrano come toouse nel flusso di lavoro di distribuzione. 

## <a name="msbuild"></a>Automatizzare la distribuzione con MSBuild
Se si utilizza hello [IDE di Visual Studio](#vs) per lo sviluppo, è possibile utilizzare [MSBuild](http://msbuildbook.com/) tooautomate le operazioni eseguibili dell'IDE. È possibile configurare MSBuild toouse sia [distribuzione Web](#webdeploy) o [FTP o FTPS](#ftp) toocopy file. Distribuzione Web consente inoltre di automatizzare molte altre attività relative alla distribuzione, ad esempio la distribuzione dei database.

Per ulteriori informazioni sulla distribuzione della riga di comando utilizzando MSBuild, vedere hello seguenti risorse:

* [Distribuzione Web ASP.NET con Visual Studio: distribuzione da riga di comando](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). Decimo in una serie di esercitazioni relative alla distribuzione tooAzure utilizzando Visual Studio. Viene illustrato come toouse hello toodeploy riga di comando dopo aver impostato i profili di pubblicazione in Visual Studio.
* [Hello interno Microsoft Build Engine: uso di MSBuild e Team Foundation Build](http://msbuildbook.com/). Disco rigido copybook che include capitoli sul toouse MSBuild per la distribuzione.

## <a name="powershell"></a>Automatizzare la distribuzione con Windows PowerShell
In [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx)è possibile eseguire funzioni di distribuzione MSBuild o FTP. Se a tale scopo, è possibile utilizzare anche un insieme di cmdlet di Windows PowerShell che rendono hello Azure REST gestione API semplice toocall.

Per ulteriori informazioni, vedere hello seguenti risorse:

* [Distribuire un repository di GitHub tooa collegato app web](app-service-web-arm-from-github-provision.md)
* [Eseguire il provisioning di un'app Web con un database SQL](app-service-web-arm-with-sql-database-provision.md)
* [Effettuare il provisioning di microservizi e distribuirli in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md)
* Capitolo dell'e-book relativo a come [automatizzare tutto e creare app per cloud reali con Azure](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything), Capitolo di E-book che spiega come applicazione di esempio hello nella hello e-book Usa toocreate gli script di Windows PowerShell di Azure ambiente di test e distribuire tooit. Vedere hello [risorse](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) sezione per i collegamenti tooadditional documentazione di Azure PowerShell.
* [Utilizzo di script di Windows PowerShell tooPublish tooDev e negli ambienti di Test](../vs-azure-tools-publishing-using-powershell-scripts.md). Come la distribuzione di Windows PowerShell toouse gli script in Visual Studio genera l'errore.

## <a name="api"></a>Automatizzare la distribuzione con API di gestione .NET
È possibile scrivere codice c# tooperform funzioni di MSBuild o FTP per la distribuzione. Se a tale scopo, è possibile accedere a funzioni di gestione del sito API REST tooperform hello gestione di Azure.

Per ulteriori informazioni, vedere hello seguenti risorse:

* [Automazione di tutti gli elementi con hello Azure Management Libraries e .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Introduzione toohello .NET documentazione per la gestione API e i collegamenti toomore.

## <a name="cli"></a>Distribuire dall'interfaccia della riga di comando di Azure
È possibile utilizzare la riga di comando hello in Windows, Mac o Linux toodeploy macchine tramite FTP. Se a tale scopo, è possibile accedere anche hello API di gestione di Azure REST mediante Azure CLI hello.

Per ulteriori informazioni, vedere hello seguenti risorse:

* [Strumenti da riga di comando di Azure](https://azure.microsoft.com/downloads/). Pagina del portale su Azure.com per le informazioni sullo strumento da riga di comando.

## <a name="webdeploy"></a>Distribuire dalla riga di comando di distribuzione Web
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) è software Microsoft per tooIIS di distribuzione che non solo fornisce file intelligente le funzionalità di sincronizzazione, ma anche possibile eseguire o coordinare molte altre attività relative alla distribuzione che non può essere automatizzato quando si utilizza FTP. Ad esempio, con Distribuzione Web è possibile distribuire un nuovo database oppure gli aggiornamenti al database assieme all'app Web. Distribuzione Web può inoltre ridurre hello tempi tooupdate un sito esistente poiché è possibile copiare in modo intelligente solo i file modificati. Microsoft Visual Studio e Team Foundation Server dispone del supporto per la distribuzione di Web incorporato, ma è anche possibile usare distribuzione Web direttamente dalla distribuzione di tooautomate hello riga di comando. Comandi di distribuzione Web sono molto potenti ma hello curva di apprendimento può essere ripida.

## <a name="more-resources"></a>Altre risorse
Automazione di un'altra distribuzione opzione toocommand riga è servizio toouse basato su cloud quali [Polipo distribuire](http://en.wikipedia.org/wiki/Octopus_Deploy). Per ulteriori informazioni, vedere [tooAzure applicazioni ASP.NET distribuire siti Web](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Per ulteriori informazioni sugli strumenti da riga di comando, vedere hello seguenti risorse:

* [Simple Web Apps: Deployment](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/). Post di blog di David Ebbo su uno strumento ha scritto toomake è più facile toouse distribuzione Web.
* [Strumento di distribuzione Web](http://technet.microsoft.com/library/dd568996). Documentazione ufficiale nel sito Microsoft TechNet hello. In data ma ancora un toostart buona.
* [Uso di Distribuzione Web](http://www.iis.net/learn/publish/using-web-deploy). Documentazione ufficiale nel sito Microsoft IIS.NET hello. Anche in data ma toostart un buon punto.
* [Distribuzione Web ASP.NET con Visual Studio: distribuzione da riga di comando](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment). MSBuild è hello Compila modulo utilizzato da Visual Studio e può essere usato anche da hello applicazioni web di riga di comando toodeploy tooWeb app. Questa esercitazione fa parte di una serie dedicata principalmente alla distribuzione con Visual Studio.

