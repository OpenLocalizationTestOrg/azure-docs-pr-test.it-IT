---
title: Abilitare una connessione Desktop remoto per un ruolo in Servizi cloud di Azure con PowerShell
description: Come configurare l'applicazione del servizio cloud di Azure utilizzando PowerShell per consentire le connessioni Desktop remoto
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="f5f66-103">Abilitare una connessione Desktop remoto per un ruolo in Servizi cloud di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5f66-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5f66-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f5f66-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="f5f66-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="f5f66-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="f5f66-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5f66-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="f5f66-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5f66-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="f5f66-108">Desktop remoto consente di accedere al desktop di un ruolo in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f66-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="f5f66-109">È possibile usare una connessione Desktop remoto per risolvere e diagnosticare i problemi dell'applicazione mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="f5f66-110">Questo articolo descrive come abilitare Desktop remoto nei ruoli dei servizi cloud con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5f66-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="f5f66-111">Per i prerequisiti necessari per questo articolo, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="f5f66-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="f5f66-112">PowerShell usa l'estensione di Desktop remoto per poter abilitare Desktop remoto dopo la distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="f5f66-113">Configurare Remote Desktop da PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5f66-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="f5f66-114">Il cmdlet [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) consente di abilitare Desktop remoto su tutti o specifici ruoli di distribuzione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="f5f66-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="f5f66-115">Il cmdlet consente di specificare il nome utente e la password per l'utente Desktop remoto tramite il parametro *Credential* che accetta un oggetto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="f5f66-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="f5f66-116">Se si usa PowerShell in modo interattivo è possibile impostare facilmente l'oggetto PSCredential chiamando il cmdlet [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f5f66-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="f5f66-117">Il comando visualizza una finestra di dialogo in cui immettere in modo sicuro il nome utente e la password per l'utente remoto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="f5f66-118">Poiché PowerShell è utile negli scenari di automazione, è anche possibile configurare l'oggetto **PSCredential** in modo che non richieda l'interazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f5f66-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="f5f66-119">In questo caso, è necessario configurare una password di protezione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="f5f66-120">Per iniziare, specificare una password non crittografata e convertirla in una stringa sicura con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f66-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="f5f66-121">Quindi è necessario convertire questa stringa sicura in una stringa standard crittografata con [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f66-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="f5f66-122">Ora è possibile salvare questa stringa crittografata standard in un file con [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f66-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="f5f66-123">È anche possibile creare un file della password di protezione in modo che non sia necessario digitarla ogni volta.</span><span class="sxs-lookup"><span data-stu-id="f5f66-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="f5f66-124">Inoltre, un file della password di protezione è preferibile a un file di testo normale.</span><span class="sxs-lookup"><span data-stu-id="f5f66-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="f5f66-125">Usare il codice di PowerShell seguente per creare un file della password sicura:</span><span class="sxs-lookup"><span data-stu-id="f5f66-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="f5f66-126">Quando si imposta la password, assicurarsi che soddisfi i [requisiti di complessità](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f66-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="f5f66-127">Per creare l'oggetto credential dal file della password di protezione, è necessario leggere il contenuto del file e riconvertirlo in una stringa sicura con [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5f66-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="f5f66-128">Il cmdlet [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) accetta anche un parametro *Expiration* che specifica un valore **DateTime** che specifica la scadenza dell'account utente.</span><span class="sxs-lookup"><span data-stu-id="f5f66-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="f5f66-129">Ad esempio, è possibile impostare la scadenza dell'account alcuni giorni dopo la data e l'ora correnti.</span><span class="sxs-lookup"><span data-stu-id="f5f66-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="f5f66-130">Questo esempio di PowerShell illustra come impostare l'estensione di Desktop remoto in un servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="f5f66-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="f5f66-131">È anche possibile specificare lo slot di distribuzione e i ruoli per i quali si vuole abilitare Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="f5f66-132">Se questi parametri non vengono specificati, il cmdlet abilita Desktop remoto su tutti i ruoli nello slot di distribuzione **Produzione** .</span><span class="sxs-lookup"><span data-stu-id="f5f66-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="f5f66-133">L'estensione per il Desktop remoto è associata a una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="f5f66-134">Se si crea una nuova distribuzione per il servizio, si dovrà abilitare Desktop remoto in quella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="f5f66-135">Se si vuole che Desktop remoto sia sempre abilitato, considerare la possibilità di integrare gli script di PowerShell nel flusso di lavoro di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f5f66-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="f5f66-136">Desktop remoto in un'istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="f5f66-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="f5f66-137">Il cmdlet [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) viene usato per integrare Desktop remoto in una specifica istanza del ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="f5f66-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="f5f66-138">È possibile usare il parametro *LocalPath* per scaricare il file RDP in locale.</span><span class="sxs-lookup"><span data-stu-id="f5f66-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="f5f66-139">In alternativa si può usare il parametro *Launch* per avviare direttamente la finestra di dialogo Connessione Desktop remoto per accedere all'istanza del ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="f5f66-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="f5f66-140">Verificare se l'estensione di Desktop remoto è attivata in un servizio</span><span class="sxs-lookup"><span data-stu-id="f5f66-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="f5f66-141">Il cmdlet [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) indica che Desktop remoto è abilitato o disabilitato in una distribuzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="f5f66-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="f5f66-142">Il cmdlet restituisce il nome utente per l'utente Desktop remoto e i ruoli per quali è abilitata l'estensione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="f5f66-143">Per impostazione predefinita, ciò avviene nello slot di distribuzione ed è possibile scegliere di usare in alternativa lo slot di staging.</span><span class="sxs-lookup"><span data-stu-id="f5f66-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="f5f66-144">Rimuovere l'estensione di Desktop remoto da un servizio</span><span class="sxs-lookup"><span data-stu-id="f5f66-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="f5f66-145">Se già stata abilitata l'estensione di Desktop remoto in una distribuzione ed è necessario aggiornare le impostazioni di Desktop remoto, occorre prima di tutto rimuovere l'estensione</span><span class="sxs-lookup"><span data-stu-id="f5f66-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="f5f66-146">e quindi riabilitarla con le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f5f66-146">And enable it again with the new settings.</span></span> <span data-ttu-id="f5f66-147">Ad esempio, se si vuole impostare una nuova password per l'account utente remoto o l'account scaduto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="f5f66-148">Questa operazione è necessaria nelle distribuzioni esistenti in cui è abilitata l'estensione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="f5f66-149">Per le nuove distribuzioni è possibile applicare semplicemente l'estensione direttamente.</span><span class="sxs-lookup"><span data-stu-id="f5f66-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="f5f66-150">Per rimuovere l'estensione di Desktop remoto dalla distribuzione, è possibile usare il cmdlet [Remove AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="f5f66-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="f5f66-151">È anche possibile specificare lo slot di distribuzione e il ruolo dal quale si vuole rimuovere l'estensione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f5f66-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="f5f66-152">Per rimuovere completamente la configurazione dell'estensione, è necessario chiamare il cmdlet *remove* con il parametro **UninstallConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="f5f66-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="f5f66-153">Il parametro **UninstallConfiguration** disinstalla qualsiasi configurazione dell'estensione applicata al servizio.</span><span class="sxs-lookup"><span data-stu-id="f5f66-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="f5f66-154">Ogni configurazione dell'estensione è associata alla configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="f5f66-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="f5f66-155">Se si chiama il cmdlet *remove* senza **UninstallConfiguration**, la <mark>distribuzione</mark> verrà dissociata dalla configurazione dell'estensione, che verrà così rimossa.</span><span class="sxs-lookup"><span data-stu-id="f5f66-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="f5f66-156">La configurazione dell'estensione rimane comunque associata al servizio.</span><span class="sxs-lookup"><span data-stu-id="f5f66-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="f5f66-157">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f5f66-157">Additional resources</span></span>

<span data-ttu-id="f5f66-158">[Come configurare i servizi cloud](cloud-services-how-to-configure.md)
[Domande frequenti sui servizi cloud - Desktop remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="f5f66-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
