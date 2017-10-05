---
title: Distribuire e gestire hub di notifica tramite PowerShell
description: Come creare e gestire Hub di notifica utilizzando PowerShell per l'automazione
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
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="08ade-103">Distribuire e gestire hub di notifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="08ade-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="08ade-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="08ade-104">Overview</span></span>
<span data-ttu-id="08ade-105">In questo articolo viene illustrato come utilizzare Creazione e gestione di hub di notifica di Azure tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08ade-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="08ade-106">Le seguenti attività comuni di automazione sono illustrate in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="08ade-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="08ade-107">Creare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="08ade-107">Create a Notification Hub</span></span>
* <span data-ttu-id="08ade-108">Impostare le credenziali</span><span class="sxs-lookup"><span data-stu-id="08ade-108">Set Credentials</span></span>

<span data-ttu-id="08ade-109">Se si desidera anche creare un nuovo spazio dei nomi per l'hub di notifica, vedere [Gestire il bus di servizio con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="08ade-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="08ade-110">La gestione degli hub di notifica non è supportata direttamente tramite i cmdlet inclusi con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08ade-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="08ade-111">L'approccio migliore da PowerShell consiste nel fare riferimento all'assembly Microsoft.Azure.NotificationHubs.dll.</span><span class="sxs-lookup"><span data-stu-id="08ade-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="08ade-112">L'assembly viene distribuito con il [pacchetto NuGet degli hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="08ade-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08ade-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="08ade-113">Prerequisites</span></span>
<span data-ttu-id="08ade-114">Per eseguire le procedure descritte nell'articolo è necessario:</span><span class="sxs-lookup"><span data-stu-id="08ade-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="08ade-115">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="08ade-115">An Azure subscription.</span></span> <span data-ttu-id="08ade-116">Azure è una piattaforma basata su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="08ade-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="08ade-117">Per altre informazioni su come ottenere una sottoscrizione, vedere [Opzioni di acquisto], [Offerte per i membri] oppure [Versione di valutazione gratuita].</span><span class="sxs-lookup"><span data-stu-id="08ade-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="08ade-118">Un computer con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08ade-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="08ade-119">Per istruzioni, vedere [Come installare e configurare Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="08ade-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="08ade-120">Conoscenza generale degli script di PowerShell, dei pacchetti NuGet e di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="08ade-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="08ade-121">Inclusione di un riferimento all'assembly .NET per il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="08ade-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="08ade-122">La gestione degli hub di notifica di Azure non è ancora inclusa con i cmdlet PowerShell di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08ade-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="08ade-123">Per eseguire il provisioning degli hub di notifica, è possibile utilizzare il client .NET nel [pacchetto NuGet degli hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="08ade-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="08ade-124">Innanzitutto, assicurarsi che lo script sia in grado di individuare l'assembly **Microsoft.Azure.NotificationHubs.dll** , che viene installato con il pacchetto NuGet in un progetto Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08ade-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="08ade-125">Per essere flessibile, lo script esegue i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="08ade-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="08ade-126">Determina il percorso in cui è stato richiamato.</span><span class="sxs-lookup"><span data-stu-id="08ade-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="08ade-127">Scorre il percorso finché trova una cartella denominata `packages`.</span><span class="sxs-lookup"><span data-stu-id="08ade-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="08ade-128">Questa cartella viene creata durante l'installazione dei pacchetti NuGet per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08ade-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="08ade-129">Cerca in modo ricorsivo nella cartella `packages` , per trovare un assembly denominato **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="08ade-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="08ade-130">Fa quindi riferimento all'assembly in modo che i tipi siano disponibili per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="08ade-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="08ade-131">Di seguito viene illustrato in che modo questi passaggi vengono implementati in uno script di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="08ade-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="08ade-132">Creare la classe NamespaceManager</span><span class="sxs-lookup"><span data-stu-id="08ade-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="08ade-133">Per eseguire il provisioning degli hub di notifica creare un'istanza della classe [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) dall’SDK.</span><span class="sxs-lookup"><span data-stu-id="08ade-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="08ade-134">È possibile usare il cmdlet [Get-AzureSBAuthorizationRule] incluso con Azure PowerShell per recuperare una regola di autorizzazione usata per fornire una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="08ade-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="08ade-135">Verrà archiviato un riferimento all'istanza di `NamespaceManager` nella variabile `$NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="08ade-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="08ade-136">Si utilizzerà `$NamespaceManager` per eseguire il provisioning di un hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="08ade-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="08ade-137">Provisioning di un nuovo hub di notifica</span><span class="sxs-lookup"><span data-stu-id="08ade-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="08ade-138">Per eseguire il provisioning di un nuovo hub di notifica, utilizzare l’ [API .NET per Hub di notifica].</span><span class="sxs-lookup"><span data-stu-id="08ade-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="08ade-139">In questa parte dello script verranno impostate quattro variabili locali.</span><span class="sxs-lookup"><span data-stu-id="08ade-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="08ade-140">`$Namespace` : impostare sul nome dello spazio dei nomi in cui si desidera creare un hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="08ade-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="08ade-141">`$Path` : impostare il percorso sul nome del nuovo hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="08ade-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="08ade-142">Ad esempio, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="08ade-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="08ade-143">`$WnsPackageSid` : impostare sul SID di pacchetto per l’applicazione Windows dal [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="08ade-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="08ade-144">`$WnsSecretkey`: impostare sulla chiave privata per l’applicazione Windows dal [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="08ade-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="08ade-145">Queste variabili vengono utilizzate per connettersi allo spazio dei nomi e creare un nuovo Hub di notifica configurato per gestire le notifiche Windows Notification Services (WNS) con credenziali WNS per un’applicazione Windows.</span><span class="sxs-lookup"><span data-stu-id="08ade-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="08ade-146">Per informazioni su come ottenere il SID di pacchetto e la chiave privata, vedere l’esercitazione [Introduzione agli Hub di notifica](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="08ade-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="08ade-147">Il frammento di script utilizza l’oggetto `NamespaceManager` da controllare per verificare se l'Hub di notifica è identificato da `$Path` esiste.</span><span class="sxs-lookup"><span data-stu-id="08ade-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="08ade-148">Se non esiste, lo script creerà un `NotificationHubDescription` con credenziali WNS e lo passerà alla classe `NamespaceManager`, metodo `CreateNotificationHub`.</span><span class="sxs-lookup"><span data-stu-id="08ade-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="08ade-149">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="08ade-149">Additional Resources</span></span>
* [<span data-ttu-id="08ade-150">Gestire il bus di servizio con PowerShell</span><span class="sxs-lookup"><span data-stu-id="08ade-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="08ade-151">Come creare code, argomenti e sottoscrizioni del bus di servizio tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="08ade-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="08ade-152">Come creare uno spazio dei nomi del bus di servizio e un hub eventi tramite uno script PowerShell</span><span class="sxs-lookup"><span data-stu-id="08ade-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="08ade-153">Sono disponibili per il download anche alcuni script predefiniti:</span><span class="sxs-lookup"><span data-stu-id="08ade-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="08ade-154">Script PowerShell del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="08ade-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

<span data-ttu-id="08ade-155">[Opzioni di acquisto]: http://azure.microsoft.com/pricing/purchase-options/</span><span class="sxs-lookup"><span data-stu-id="08ade-155">[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/</span></span>
<span data-ttu-id="08ade-156">[Offerte per i membri]: http://azure.microsoft.com/pricing/member-offers/</span><span class="sxs-lookup"><span data-stu-id="08ade-156">[Member Offers]: http://azure.microsoft.com/pricing/member-offers/</span></span>
<span data-ttu-id="08ade-157">[Versione di valutazione gratuita]: http://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="08ade-157">[Free Trial]: http://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="08ade-158">[Come installare e configurare Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="08ade-158">[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="08ade-159">[API .NET per Hub di notifica]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span><span class="sxs-lookup"><span data-stu-id="08ade-159">[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span></span>
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
<span data-ttu-id="08ade-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span><span class="sxs-lookup"><span data-stu-id="08ade-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span></span>

