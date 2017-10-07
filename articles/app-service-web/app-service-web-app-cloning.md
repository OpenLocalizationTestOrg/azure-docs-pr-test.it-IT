---
title: aaaWeb App clonazione tramite PowerShell
description: Informazioni su come tooclone App Web toonew App Web utilizzando PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Clonazione di app del servizio app di Azure con PowerShell
Con versione di hello di Microsoft Azure PowerShell versione 1.1.0 una nuova opzione è stata aggiunta AzureRMWebApp tooNew che hello utente hello possibilità tooclone un'app di tooa appena creato App Web esistente in un'area diversa o in hello stessa area. In questo modo i clienti toodeploy un numero di App in aree geografiche diverse in modo semplice e rapido.

La clonazione di app è attualmente supportata solo per i piani di servizio app Premium. Usa funzionalità nuova Hello hello stesso limitazioni delle funzionalità di Backup di applicazioni Web, vedere [eseguire il backup di un'app web in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sull'utilizzo di gestione risorse di Azure basato su toomanage cmdlet PowerShell di Azure l'archiviazione di applicazioni Web [Gestione risorse di Azure basato su comandi di PowerShell per App Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Clonazione di un'app esistente
Scenario: Un'app web esistente nell'area centro-meridionali, utente hello sarebbe tooclone hello contenuto tooa nuova app web nell'area North Central US. Questo può essere eseguito con versione di Azure Resource Manager hello di hello PowerShell cmdlet toocreate una nuova app web con l'opzione - SourceWebApp hello.

La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, è possibile utilizzare le seguenti informazioni PowerShell comando tooget hello origine dell'app web (denominate in questo caso origine webapp) hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate un piano di servizio App nuovo, è possibile utilizzare il comando New-AzureRmAppServicePlan come hello di esempio seguente

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Utilizzando il comando New-AzureRmWebApp hello, è possibile creare hello nuova app web nell'area di hello North Central US e ricollegarlo livello premium esistente tooan piano di servizio App, è inoltre possibile utilizzare hello stessa risorsa gruppo come app web di origine hello o definire un nuovo gruppo di risorse , esempio hello viene dimostrato che:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

un'app web esistente tra tutti gli slot di distribuzione associati, sarà necessario toouse l'utente hello tooclone hello parametro IncludeSourceWebAppSlots, hello comando PowerShell seguente viene illustrato l'utilizzo di hello del parametro con il comando New-AzureRmWebApp hello:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

un'app web esistente all'interno di hello tooclone stessa area, hello utente dovrà disporre di un nuovo gruppo di risorse e un nuovo servizio app piano hello toocreate stessa regione e utilizzando quindi hello seguenti app web di PowerShell comando tooclone hello

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>La clonazione di un tooan App esistenti di ambiente del servizio App
Scenario: Un'app web esistente nell'area centro-meridionali, utente hello sarebbe tooclone hello contenuto tooa nuova web app tooan ambiente del servizio App (ASE) esistente.

La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, è possibile utilizzare le seguenti informazioni PowerShell comando tooget hello origine dell'app web (denominate in questo caso origine webapp) hello:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

La conoscenza del hello ASE nome e nome di gruppo di risorse hello hello ASE a cui appartiene, utente di hello può utilizzare il comando New-AzureRmWebApp hello toocreate hello nuova app web in hello esistente ASE, hello seguente viene dimostrato che:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

parametro percorso Hello è necessario a causa di motivo toolegacy, ma nel caso di hello di creazione di un'app in un ASE verranno ignorato. 

## <a name="cloning-an-existing-app-slot"></a>Clonazione dello slot di un'app esistente
Scenario: utente hello sarebbe tooclone un tooeither Slot App Web esistente, una nuova App Web o un nuovo slot di App Web. nuova App Web può essere in hello Hello stessa area come slot di hello originale App Web o in un'area diversa.

La conoscenza delle risorse hello nome del gruppo che contiene l'app web di origine hello, possiamo utilizzare hello informazioni tooget hello origine web app dello slot (denominate in questo caso origine webappslot) associato tooWeb App origine-webapp comando di PowerShell seguente:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

esempio Hello viene illustrata la creazione di un clone di hello web app tooa nuova app web di origine:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Configurazione di Gestione traffico durante la clonazione di un'app
Creazione di applicazioni web con più aree e la configurazione di gestione traffico di Azure tooroute traffico tooall queste App web, è un tooinsure n scenario importante che le applicazioni dei clienti sono a disponibile elevata, durante la clonazione di un'app web esistente è hello opzione tooconnect i servizi web App tooeither un nuovo profilo di gestione traffico o utilizzarne uno esistente, si noti che Gestione risorse di Azure solo la versione di gestione traffico è supportato.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Creazione di un nuovo profilo di Gestione traffico durante la clonazione di un'app
Scenario: utente hello sarebbe tooclone un'area tooanother app web, durante la configurazione di un profilo di gestione traffico di gestione risorse di Azure che includono sia applicazioni web. esempio Hello viene illustrata la creazione di un clone di hello web app tooa nuova app web di origine durante la configurazione di un nuovo profilo di Traffic Manager:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Aggiunta di nuovo clonato App Web tooan esistente profilo di gestione traffico
Scenario: hello utente dispone già di un profilo di gestione traffico di gestione risorse di Azure che vorrebbe tooadd entrambi web App come endpoint. toodo in tal caso, è necessario innanzitutto tooassemble hello esistente id di profilo di gestione traffico, è necessario id sottoscrizione hello, nome del gruppo di risorse e hello traffic manager nome del profilo esistente.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Dopo avere l'id di gestione traffico hello, seguente hello viene illustrato come creare un clone di hello web app tooa nuova app web di origine durante l'aggiunta di tooan profilo di gestione traffico esistente:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Restrizioni attuali
Questa funzionalità è attualmente in anteprima, Microsoft è impegnata tooadd nuove funzionalità nel tempo, hello seguente elenco sono hello restrizioni note sulla versione corrente di hello di clonazione app:

* Le impostazioni di ridimensionamento automatico non vengono clonate.
* Le impostazioni di pianificazione del backup non vengono clonate.
* Le impostazioni della rete virtuale non vengono clonate.
* App Insights non automaticamente impostate nell'applicazione web di destinazione hello
* Le impostazioni di Easy Auth non vengono clonate.
* L'estensione Kudu non viene clonata.
* Le regole TiP non vengono clonate.
* Il contenuto di database non viene clonato.

### <a name="references"></a>Riferimenti
* [Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Clonazione di app Web con il portale di Azure](app-service-web-app-cloning-portal.md)
* [Eseguire il backup di un'app Web nel servizio app di Azure](web-sites-backup.md)
* [Supporto di Azure Resource Manager per la versione di anteprima di Gestione traffico di Azure](../traffic-manager/traffic-manager-powershell-arm.md)
* [Introduzione tooApp ambiente del servizio](app-service-app-service-environment-intro.md)
* [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)

