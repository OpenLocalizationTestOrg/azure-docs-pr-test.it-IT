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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="966ff-103">Distribuire e gestire hub di notifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="966ff-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="966ff-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="966ff-104">Overview</span></span>
<span data-ttu-id="966ff-105">Questo articolo illustra come creare toouse e gestire Azure gli hub di notifica tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="966ff-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="966ff-106">Hello attività di automazione comuni di seguito è illustrato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="966ff-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="966ff-107">Creare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="966ff-107">Create a Notification Hub</span></span>
* <span data-ttu-id="966ff-108">Impostare le credenziali</span><span class="sxs-lookup"><span data-stu-id="966ff-108">Set Credentials</span></span>

<span data-ttu-id="966ff-109">Se è necessario anche toocreate un nuovo servizio bus dello spazio dei nomi per gli hub di notifica, vedere [gestione Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="966ff-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="966ff-110">La gestione degli hub di notifiche non è supportata direttamente dal cmdlet hello inclusi con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="966ff-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="966ff-111">approccio migliore di Hello da PowerShell consiste assembly Microsoft.Azure.NotificationHubs.dll di tooreference hello.</span><span class="sxs-lookup"><span data-stu-id="966ff-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="966ff-112">assembly Hello viene distribuita con hello [pacchetto NuGet hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="966ff-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="966ff-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="966ff-113">Prerequisites</span></span>
<span data-ttu-id="966ff-114">Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="966ff-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="966ff-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="966ff-115">An Azure subscription.</span></span> <span data-ttu-id="966ff-116">Azure è una piattaforma basata su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="966ff-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="966ff-117">Per altre informazioni su come ottenere una sottoscrizione, vedere [Opzioni di acquisto], [Offerte per i membri] oppure [Versione di valutazione gratuita].</span><span class="sxs-lookup"><span data-stu-id="966ff-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="966ff-118">Un computer con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="966ff-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="966ff-119">Per istruzioni, vedere [Come installare e configurare Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="966ff-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="966ff-120">Una conoscenza generale di script di PowerShell, i pacchetti NuGet e hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="966ff-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="966ff-121">Tra cui un assembly .NET toohello di riferimento per il Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="966ff-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="966ff-122">La gestione degli hub di notifica di Azure non è ancora inclusa con i cmdlet di PowerShell di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="966ff-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="966ff-123">gli hub di notifica tooprovision, è possibile utilizzare il client di .NET hello cui hello [pacchetto NuGet hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="966ff-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="966ff-124">Innanzitutto, assicurarsi che lo script in grado di individuare hello **Microsoft.Azure.NotificationHubs.dll** assembly, che viene installato come un pacchetto NuGet in un progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="966ff-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="966ff-125">In ordine toobe flessibile, script hello esegue queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="966ff-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="966ff-126">Determina il percorso di hello in corrispondenza del quale è stato richiamato.</span><span class="sxs-lookup"><span data-stu-id="966ff-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="966ff-127">Attraversa hello percorso finché trova una cartella denominata `packages`.</span><span class="sxs-lookup"><span data-stu-id="966ff-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="966ff-128">Questa cartella viene creata durante l'installazione dei pacchetti NuGet per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="966ff-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="966ff-129">In modo ricorsivo ricerche hello `packages` cartella per un assembly denominato **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="966ff-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="966ff-130">Riferimenti hello assembly in modo che i tipi di hello sono disponibili per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="966ff-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="966ff-131">Di seguito viene illustrato in che modo questi passaggi vengono implementati in uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="966ff-131">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="966ff-132">Creare una classe NamespaceManager hello</span><span class="sxs-lookup"><span data-stu-id="966ff-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="966ff-133">tooprovision gli hub di notifica, creare un'istanza di hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) classe da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="966ff-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="966ff-134">È possibile utilizzare hello [Get AzureSBAuthorizationRule] cmdlet inclusi in Azure PowerShell tooretrieve una regola di autorizzazione che ha utilizzato tooprovide una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="966ff-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="966ff-135">È possibile archiviare toohello un riferimento `NamespaceManager` istanza in hello `$NamespaceManager` variabile.</span><span class="sxs-lookup"><span data-stu-id="966ff-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="966ff-136">Si utilizzerà `$NamespaceManager` tooprovision un hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="966ff-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="966ff-137">Provisioning di un nuovo hub di notifica</span><span class="sxs-lookup"><span data-stu-id="966ff-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="966ff-138">tooprovision un nuovo hub di notifica, utilizzare hello [API .NET per gli hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="966ff-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="966ff-139">In questa parte dello script hello è quattro variabili locali.</span><span class="sxs-lookup"><span data-stu-id="966ff-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="966ff-140">`$Namespace`: Impostare questo toohello nome dello spazio dei nomi hello in cui si desidera toocreate un hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="966ff-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="966ff-141">`$Path`: Impostare il nome del nuovo hub di notifica hello toohello di percorso.</span><span class="sxs-lookup"><span data-stu-id="966ff-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="966ff-142">Ad esempio, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="966ff-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="966ff-143">`$WnsPackageSid`: Impostare questo SID del pacchetto toohello l'App di Windows da hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="966ff-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="966ff-144">`$WnsSecretkey`: Impostare questa chiave segreta toohello l'App di Windows da hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="966ff-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="966ff-145">Queste variabili sono dello spazio dei nomi di tooyour tooconnect utilizzato e creare un nuovo toohandle Hub di notifica configurato le notifiche di servizi di notifica di Windows (WNS) con le credenziali WNS per un'App di Windows.</span><span class="sxs-lookup"><span data-stu-id="966ff-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="966ff-146">Per informazioni su come ottenere hello pacchetto SID e vedere chiave segreta, hello [Introduzione agli hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="966ff-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="966ff-147">frammento di script Hello utilizza hello `NamespaceManager` toocheck toosee dell'oggetto se hello Hub di notifica è identificato da `$Path` esiste.</span><span class="sxs-lookup"><span data-stu-id="966ff-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="966ff-148">Se non esiste, verrà creato uno script hello un `NotificationHubDescription` con WNS credenziali e passare tale toohello `NamespaceManager` classe `CreateNotificationHub` metodo.</span><span class="sxs-lookup"><span data-stu-id="966ff-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="966ff-149">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="966ff-149">Additional Resources</span></span>
* [<span data-ttu-id="966ff-150">Gestire Bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="966ff-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="966ff-151">Il Bus di servizio toocreate code, argomenti e sottoscrizioni tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="966ff-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="966ff-152">Come toocreate Namespace Bus di servizio e un Hub di eventi tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="966ff-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="966ff-153">Sono disponibili per il download anche alcuni script predefiniti:</span><span class="sxs-lookup"><span data-stu-id="966ff-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="966ff-154">Script PowerShell del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="966ff-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opzioni di acquisto]: http://azure.microsoft.com/pricing/purchase-options/
[Offerte per i membri]: http://azure.microsoft.com/pricing/member-offers/
[Versione di valutazione gratuita]: http://azure.microsoft.com/pricing/free-trial/
[Come installare e configurare Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET per gli hub di notifica]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

