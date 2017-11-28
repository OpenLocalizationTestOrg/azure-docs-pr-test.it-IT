---
title: aaaEnable connessione Desktop remoto per un ruolo in servizi Cloud di Azure tramite PowerShell
description: Tooconfigure cloud di azure tramite le connessioni desktop remoto di PowerShell tooallow applicazione del servizio
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="e3655-103">Abilitare una connessione Desktop remoto per un ruolo in Servizi cloud di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3655-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3655-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3655-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="e3655-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="e3655-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="e3655-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3655-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="e3655-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3655-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="e3655-108">Desktop remoto consente desktop hello tooaccess di un ruolo in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3655-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="e3655-109">È possibile utilizzare un tootroubleshoot connessione Desktop remoto e diagnosticare i problemi dell'applicazione mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e3655-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="e3655-110">Questo articolo viene descritto come tooenable desktop remoto i ruoli dei servizi Cloud tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3655-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="e3655-111">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e3655-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="e3655-112">PowerShell Usa hello estensione Desktop remoto, pertanto è possibile abilitare Desktop remoto dopo la distribuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="e3655-113">Configurare Remote Desktop da PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3655-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="e3655-114">Hello [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet consente tooenable Desktop remoto su tutti i ruoli di distribuzione del servizio cloud o di ruoli specificati.</span><span class="sxs-lookup"><span data-stu-id="e3655-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="e3655-115">Hello cmdlet consente di specificare hello nome utente e Password per utente desktop remoto hello tramite hello *credenziali* parametro che accetta un oggetto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="e3655-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="e3655-116">Se si usa PowerShell in modo interattivo, è possibile impostare facilmente oggetto PSCredential hello dal chiamante hello [Ottieni credenziali](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3655-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="e3655-117">Questo comando Visualizza una finestra di dialogo che consente di tooenter hello nome utente e password per l'utente remoto hello in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="e3655-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="e3655-118">Poiché consente di PowerShell in scenari di automazione, è possibile anche impostare hello **PSCredential** oggetto in modo che non richiede l'intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e3655-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="e3655-119">In primo luogo, è necessario tooset una password sicura.</span><span class="sxs-lookup"><span data-stu-id="e3655-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="e3655-120">Iniziare con specificando una password in testo normale convertire la stringa sicura tooa utilizzando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3655-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="e3655-121">È quindi necessario tooconvert questa stringa protetta in una stringa standard crittografata usando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3655-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="e3655-122">Ora è possibile salvare questo file tooa stringa standard crittografata utilizzando [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3655-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="e3655-123">È anche possibile creare un file di password di protezione in modo che non è tootype password hello ogni volta.</span><span class="sxs-lookup"><span data-stu-id="e3655-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="e3655-124">Inoltre, un file della password di protezione è preferibile a un file di testo normale.</span><span class="sxs-lookup"><span data-stu-id="e3655-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="e3655-125">Utilizzare hello PowerShell toocreate un file di password di protezione seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3655-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="e3655-126">Quando si imposta la password di hello, assicurarsi che siano soddisfatti hello [i requisiti di complessità](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3655-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="e3655-127">oggetto credenziale di hello toocreate dal file di password sicura hello, è necessario leggere il contenuto del file hello e convertirli tooa indietro secure stringa utilizzando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3655-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="e3655-128">Hello [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet accetta inoltre un *scadenza* parametro che specifica un **DateTime** utente hello scadenza account.</span><span class="sxs-lookup"><span data-stu-id="e3655-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="e3655-129">Ad esempio, è possibile impostare hello account tooexpire pochi giorni dalla data e ora correnti di hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="e3655-130">In questo esempio di PowerShell viene illustrato come tooset hello estensione Desktop remoto in un servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="e3655-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="e3655-131">È anche possibile specificare lo slot di distribuzione hello e i ruoli che si desidera includere tooenable desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="e3655-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="e3655-132">Se questi parametri vengono omessi, hello cmdlet Abilita desktop remoto su tutti i ruoli di hello **produzione** slot di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e3655-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="e3655-133">Hello estensione Desktop remoto è associata a una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e3655-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="e3655-134">Se si crea una nuova distribuzione per il servizio di hello, è necessario tooenable desktop remoto nella distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e3655-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="e3655-135">Se si desidera comunque toohave desktop remoto abilitato, è necessario considerare l'integrazione di script di PowerShell hello nel flusso di lavoro di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e3655-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="e3655-136">Desktop remoto in un'istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="e3655-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="e3655-137">Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet è desktop tooremote utilizzato in un'istanza del ruolo specifico del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e3655-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="e3655-138">È possibile utilizzare hello *LocalPath* hello toodownload di parametro RDP file localmente.</span><span class="sxs-lookup"><span data-stu-id="e3655-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="e3655-139">Oppure è possibile utilizzare hello *avviare* tooaccess di finestra di dialogo connessione Desktop remoto di parametro toodirectly avvio hello hello istanza del ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="e3655-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="e3655-140">Verificare se l'estensione di Desktop remoto è attivata in un servizio</span><span class="sxs-lookup"><span data-stu-id="e3655-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="e3655-141">Hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet Visualizza che desktop remoto è abilitato o disabilitato su una distribuzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="e3655-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="e3655-142">cmdlet di Hello restituisce hello username per utente desktop remoto hello e i ruoli di hello abilitata per l'estensione di desktop remoto hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="e3655-143">Per impostazione predefinita, in questo caso nello slot di distribuzione hello ed è possibile scegliere hello toouse invece slot di staging.</span><span class="sxs-lookup"><span data-stu-id="e3655-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="e3655-144">Rimuovere l'estensione di Desktop remoto da un servizio</span><span class="sxs-lookup"><span data-stu-id="e3655-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="e3655-145">Estensione di desktop remoto hello in una distribuzione è già stato abilitato, se necessario tooupdate hello impostazioni desktop remoto, è necessario rimuovere prima estensione hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="e3655-146">E abilitarlo di nuovo con nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="e3655-147">Ad esempio, se si desidera tooset una nuova password per l'account utente remoto hello o hello account scaduto.</span><span class="sxs-lookup"><span data-stu-id="e3655-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="e3655-148">Questa operazione è necessaria per le distribuzioni esistenti che presentano hello estensione desktop remoto abilitato.</span><span class="sxs-lookup"><span data-stu-id="e3655-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="e3655-149">Per nuove distribuzioni, è possibile applicare estensione hello semplicemente direttamente.</span><span class="sxs-lookup"><span data-stu-id="e3655-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="e3655-150">tooremove hello remote desktop estensione dalla distribuzione hello, è possibile utilizzare hello [Remove AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3655-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="e3655-151">È anche possibile specificare lo slot di distribuzione hello e il ruolo da cui si desidera l'estensione di desktop remoto di tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="e3655-152">configurazione dell'estensione hello remove toocompletely, è necessario chiamare hello *rimuovere* cmdlet con hello **UninstallConfiguration** parametro.</span><span class="sxs-lookup"><span data-stu-id="e3655-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="e3655-153">Hello **UninstallConfiguration** parametro consente di disinstallare qualsiasi configurazione dell'estensione che è applicato toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="e3655-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="e3655-154">Ogni configurazione dell'estensione è associata a una configurazione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="e3655-155">Chiamare il metodo hello *rimuovere* cmdlet senza **UninstallConfiguration** disassocia hello <mark>distribuzione</mark> dalla configurazione dell'estensione hello, in modo efficace rimuovendo estensione Hello.</span><span class="sxs-lookup"><span data-stu-id="e3655-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="e3655-156">Configurazione dell'estensione hello rimane tuttavia associato hello servizio.</span><span class="sxs-lookup"><span data-stu-id="e3655-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="e3655-157">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e3655-157">Additional resources</span></span>

<span data-ttu-id="e3655-158">[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e3655-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
