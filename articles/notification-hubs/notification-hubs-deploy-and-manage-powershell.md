---
title: aaaDeploy e gestire gli hub di notifica tramite PowerShell
description: Come tooCreate e gestire la notifica hub mediante PowerShell per l'automazione
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Distribuire e gestire hub di notifica tramite PowerShell
## <a name="overview"></a>Panoramica
Questo articolo illustra come creare toouse e gestire Azure gli hub di notifica tramite PowerShell. Hello attività di automazione comuni di seguito è illustrato in questo argomento.

* Creare un hub di notifica
* Impostare le credenziali

Se è necessario anche toocreate un nuovo servizio bus dello spazio dei nomi per gli hub di notifica, vedere [gestione Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

La gestione degli hub di notifiche non è supportata direttamente dal cmdlet hello inclusi con Azure PowerShell. approccio migliore di Hello da PowerShell consiste assembly Microsoft.Azure.NotificationHubs.dll di tooreference hello. assembly Hello viene distribuita con hello [pacchetto NuGet hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure. Azure è una piattaforma basata su sottoscrizione. Per altre informazioni su come ottenere una sottoscrizione, vedere [Opzioni di acquisto], [Offerte per i membri] oppure [Versione di valutazione gratuita].
* Un computer con Azure PowerShell. Per istruzioni, vedere [Come installare e configurare Azure PowerShell].
* Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Tra cui un assembly .NET toohello di riferimento per il Bus di servizio
La gestione degli hub di notifica di Azure non è ancora inclusa con i cmdlet di PowerShell di Azure PowerShell hello. gli hub di notifica tooprovision, è possibile utilizzare il client di .NET hello cui hello [pacchetto NuGet hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Innanzitutto, assicurarsi che lo script in grado di individuare hello **Microsoft.Azure.NotificationHubs.dll** assembly, che viene installato come un pacchetto NuGet in un progetto di Visual Studio. In ordine toobe flessibile, script hello esegue queste operazioni:

1. Determina il percorso di hello in corrispondenza del quale è stato richiamato.
2. Attraversa hello percorso finché trova una cartella denominata `packages`. Questa cartella viene creata durante l'installazione dei pacchetti NuGet per Visual Studio.
3. In modo ricorsivo ricerche hello `packages` cartella per un assembly denominato **Microsoft.Azure.NotificationHubs.dll**.
4. Riferimenti hello assembly in modo che i tipi di hello sono disponibili per un uso successivo.

Di seguito viene illustrato in che modo questi passaggi vengono implementati in uno script di PowerShell:

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>Creare una classe NamespaceManager hello
tooprovision gli hub di notifica, creare un'istanza di hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe da hello SDK. 

È possibile utilizzare hello [Get AzureSBAuthorizationRule] cmdlet inclusi in Azure PowerShell tooretrieve una regola di autorizzazione che ha utilizzato tooprovide una stringa di connessione. È possibile archiviare toohello un riferimento `NamespaceManager` istanza in hello `$NamespaceManager` variabile. Si utilizzerà `$NamespaceManager` tooprovision un hub di notifica.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Provisioning di un nuovo hub di notifica
tooprovision un nuovo hub di notifica, utilizzare hello [API .NET per gli hub di notifica].

In questa parte dello script hello è quattro variabili locali. 

1. `$Namespace`: Impostare questo toohello nome dello spazio dei nomi hello in cui si desidera toocreate un hub di notifica.
2. `$Path`: Impostare il nome del nuovo hub di notifica hello toohello di percorso.  Ad esempio, "MyHub".    
3. `$WnsPackageSid`: Impostare questo SID del pacchetto toohello l'App di Windows da hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Impostare questa chiave segreta toohello l'App di Windows da hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Queste variabili sono dello spazio dei nomi di tooyour tooconnect utilizzato e creare un nuovo toohandle Hub di notifica configurato le notifiche di servizi di notifica di Windows (WNS) con le credenziali WNS per un'App di Windows. Per informazioni su come ottenere hello pacchetto SID e vedere chiave segreta, hello [Introduzione agli hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) esercitazione. 

* frammento di script Hello utilizza hello `NamespaceManager` toocheck toosee dell'oggetto se hello Hub di notifica è identificato da `$Path` esiste.
* Se non esiste, verrà creato uno script hello un `NotificationHubDescription` con WNS credenziali e passare tale toohello `NamespaceManager` classe `CreateNotificationHub` metodo.

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Risorse aggiuntive
* [Gestire Bus di servizio con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Il Bus di servizio toocreate code, argomenti e sottoscrizioni tramite uno script di PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Come toocreate Namespace Bus di servizio e un Hub di eventi tramite uno script di PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Sono disponibili per il download anche alcuni script predefiniti:

* [Script PowerShell del bus di servizio](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opzioni di acquisto]: http://azure.microsoft.com/pricing/purchase-options/
[Offerte per i membri]: http://azure.microsoft.com/pricing/member-offers/
[Versione di valutazione gratuita]: http://azure.microsoft.com/pricing/free-trial/
[Come installare e configurare Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET per gli hub di notifica]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

