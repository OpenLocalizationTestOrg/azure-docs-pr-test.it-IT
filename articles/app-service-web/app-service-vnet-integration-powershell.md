---
title: aaaConnect la rete virtuale tooyour di app tramite PowerShell
description: Istruzioni sull'uso delle tooconnect tooand con le reti virtuali con PowerShell
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="0cd65-103">La connessione di rete virtuale tooyour app tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cd65-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="0cd65-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0cd65-104">Overview</span></span>
<span data-ttu-id="0cd65-105">Nel servizio App di Azure, è possibile connettere l'app (web, mobili o API) tooan rete virtuale di Azure (VNet) nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0cd65-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="0cd65-106">Questa funzionalità è detta integrazione rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="0cd65-107">funzionalità di integrazione della rete virtuale Hello non deve essere confuso con la funzionalità dell'ambiente del servizio App di hello, che permette toorun un'istanza di servizio App di Azure nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="0cd65-108">la funzionalità di integrazione della rete virtuale Hello ha un'interfaccia utente (UI) nel nuovo portale di hello che è possibile utilizzare toointegrate con le reti virtuali che vengono distribuite tramite il modello di distribuzione classica hello o modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0cd65-109">Per ulteriori informazioni sulla funzionalità hello toolearn, vedere [integrare l'app con una rete virtuale di Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="0cd65-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="0cd65-110">In questo articolo è non sulla modalità toouse hello dell'interfaccia utente, ma piuttosto sull'integrazione tooenable tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0cd65-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="0cd65-111">Poiché i comandi di hello per ogni modello di distribuzione sono diversi, in questo articolo contiene una sezione per ogni modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0cd65-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="0cd65-112">Prima di continuare con l'articolo, verificare la disponibilità di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0cd65-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="0cd65-113">Hello che più recente di Azure PowerShell SDK installato.</span><span class="sxs-lookup"><span data-stu-id="0cd65-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="0cd65-114">È possibile installarlo con hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="0cd65-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="0cd65-115">Un'app nel servizio app di Azure in esecuzione all'interno di uno SKU Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="0cd65-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="0cd65-116">Reti virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="0cd65-116">Classic virtual networks</span></span>
<span data-ttu-id="0cd65-117">Questa sezione vengono illustrate tre attività per le reti virtuali che utilizzano il modello di distribuzione classica hello:</span><span class="sxs-lookup"><span data-stu-id="0cd65-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="0cd65-118">Connettere l'app tooa preesistenti rete virtuale che dispone di un gateway ed è configurata per la connettività point-to-site.</span><span class="sxs-lookup"><span data-stu-id="0cd65-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="0cd65-119">Aggiornare le informazioni di integrazione della rete virtuale per l'app</span><span class="sxs-lookup"><span data-stu-id="0cd65-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="0cd65-120">Disconnettere l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="0cd65-121">Connettersi a un'app tooa classico rete virtuale</span><span class="sxs-lookup"><span data-stu-id="0cd65-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="0cd65-122">tooconnect una rete virtuale tooa app, seguire questi tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="0cd65-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="0cd65-123">Dichiarare toohello web app che verrà aggiunta una rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="0cd65-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="0cd65-124">app Hello genererà un certificato che verrà assegnato toohello di rete virtuale per la connettività point-to-site.</span><span class="sxs-lookup"><span data-stu-id="0cd65-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="0cd65-125">Caricamento di rete virtuale di hello web app certificato toohello e quindi recuperare l'URI del pacchetto VPN point-to-site hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="0cd65-126">Aggiornare la connessione di rete virtuale dell'applicazione web hello con l'URI del pacchetto hello point-to-site.</span><span class="sxs-lookup"><span data-stu-id="0cd65-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="0cd65-127">Hello primo e il terzi passaggi sono interamente configurabile tramite script, ma secondo passaggio hello richiede un'azione manuale monouso tramite il portale di hello o accesso tooperform **inserire** o **PATCH** azioni nella rete virtuale hello Endpoint di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd65-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="0cd65-128">Contattare questo abilitato toohave supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd65-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="0cd65-129">Prima di iniziare, assicurarsi che sia già abilitata una rete virtuale classica con connettività da punto a sito e che sia disponibile un gateway distribuito.</span><span class="sxs-lookup"><span data-stu-id="0cd65-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="0cd65-130">toocreate hello gateway e abilitare point-to-site connettività, è necessario portale hello toouse come descritto in [creazione di un gateway VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="0cd65-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="0cd65-131">rete virtuale classica Hello deve toobe in hello stessa sottoscrizione del servizio App del piano che si sta integrando con app hello contiene.</span><span class="sxs-lookup"><span data-stu-id="0cd65-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="0cd65-132">Configurare Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="0cd65-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="0cd65-133">Aprire una finestra di PowerShell e configurare l'account e la sottoscrizione di Azure con:</span><span class="sxs-lookup"><span data-stu-id="0cd65-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="0cd65-134">Tale comando consente di aprire un prompt dei comandi tooget le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="0cd65-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="0cd65-135">Dopo l'accesso, utilizzare uno dei seguenti sottoscrizione hello tooselect di comandi che si desidera toouse hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="0cd65-136">Assicurarsi che si utilizza sottoscrizione hello presenti tra la rete virtuale e un piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="0cd65-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="0cd65-137">oppure</span><span class="sxs-lookup"><span data-stu-id="0cd65-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="0cd65-138">Variabili usate in questo articolo</span><span class="sxs-lookup"><span data-stu-id="0cd65-138">Variables used in this article</span></span>
<span data-ttu-id="0cd65-139">i comandi toosimplify, si imposterà una **$Configuration** variabile PowerShell con configurazione specifica hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="0cd65-140">Impostare una variabile come indicato di seguito in PowerShell con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="0cd65-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="0cd65-141">percorso dell'app Hello deve essere il percorso di hello senza spazi.</span><span class="sxs-lookup"><span data-stu-id="0cd65-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="0cd65-142">Ad esempio West US, per gli Stati Uniti occidentali, sarà westus.</span><span class="sxs-lookup"><span data-stu-id="0cd65-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="0cd65-143">elemento successivo Hello è dove certificato hello deve essere scritti.</span><span class="sxs-lookup"><span data-stu-id="0cd65-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="0cd65-144">Deve essere un percorso accessibile in scrittura nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="0cd65-145">Assicurarsi che con estensione cer tooinclude alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="0cd65-146">toosee è impostato, tipo **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="0cd65-147">resto Hello di questa sezione presuppone che si disponga di una variabile creata come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0cd65-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="0cd65-148">Dichiarare hello rete virtuale toohello app</span><span class="sxs-lookup"><span data-stu-id="0cd65-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="0cd65-149">Utilizzare hello successivo comando tootell hello app che verrà utilizzato questa rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="0cd65-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="0cd65-150">In questo modo hello app toogenerate certificati necessari:</span><span class="sxs-lookup"><span data-stu-id="0cd65-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="0cd65-151">Se il comando ha esito positivo, **$vnet** deve contenere una variabile **Properties**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="0cd65-152">Hello **proprietà** variabile deve contenere sia un certificato hello e identificazione personale certificato i dati.</span><span class="sxs-lookup"><span data-stu-id="0cd65-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="0cd65-153">Caricare una rete virtuale di hello web app certificato toohello</span><span class="sxs-lookup"><span data-stu-id="0cd65-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="0cd65-154">Per ogni combinazione di sottoscrizione e rete virtuale è necessario eseguire un unico passaggio manuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="0cd65-155">Ovvero, se ci si connette l'App in una rete tooVirtual sottoscrizione, è necessario toodo questo passaggio solo una volta indipendentemente dal numero App configurato.</span><span class="sxs-lookup"><span data-stu-id="0cd65-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="0cd65-156">Se si aggiunge una nuova rete virtuale tooanother di app, occorre toodo più questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="0cd65-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="0cd65-157">motivo Hello è che viene generato un set di certificati a livello di sottoscrizione in Azure App Service e set hello viene generato una volta per ogni rete virtuale a cui si connetterà hello app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="0cd65-158">Hello certificati verranno sono già stati impostati se sono state seguite le operazioni o se è integrata con hello stessa rete virtuale tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="0cd65-159">primo passaggio Hello è file con estensione cer toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="0cd65-160">secondo passaggio Hello è rete virtuale di tooupload hello. cer file tooyour.</span><span class="sxs-lookup"><span data-stu-id="0cd65-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="0cd65-161">file con estensione cer hello toogenerate dalla chiamata all'API hello in hello passaggio precedente, eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0cd65-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="0cd65-162">certificato Hello sarà disponibile nel percorso hello che **$Configuration.GeneratedCertificatePath** specifica.</span><span class="sxs-lookup"><span data-stu-id="0cd65-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="0cd65-163">certificato hello tooupload manualmente, utilizzare hello [portale di Azure] [ azureportal] e **esplorare la rete virtuale (classico)** > **le connessioni VPN**  >  **Point-to-site** > **gestire i certificati**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="0cd65-164">A questo punto, caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="0cd65-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="0cd65-165">Ottenere il pacchetto di hello point-to-site</span><span class="sxs-lookup"><span data-stu-id="0cd65-165">Get hello point-to-site package</span></span>
<span data-ttu-id="0cd65-166">passaggio successivo di Hello nell'impostazione di una connessione di rete virtuale in un'app web è tooget hello point-to-site pacchetto e fornirlo tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="0cd65-167">Salvare i seguenti file di modello tooa chiamato GetNetworkPackageUri.json in un punto qualsiasi nel computer in uso, ad esempio, C:\Azure\Templates\GetNetworkPackageUri.json hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="0cd65-168">Impostare i parametri di input:</span><span class="sxs-lookup"><span data-stu-id="0cd65-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="0cd65-169">Chiamare hello script:</span><span class="sxs-lookup"><span data-stu-id="0cd65-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="0cd65-170">variabile Hello **$output. Outputs.packageUri** conterrà hello pacchetto URI toobe dato tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="0cd65-171">Caricare hello pacchetto point-to-site tooyour app</span><span class="sxs-lookup"><span data-stu-id="0cd65-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="0cd65-172">passaggio finale Hello è tooprovide hello app con questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0cd65-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="0cd65-173">Comando successivo hello è sufficiente eseguire:</span><span class="sxs-lookup"><span data-stu-id="0cd65-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="0cd65-174">Se un messaggio richiederà tooconfirm si sovrascrive una risorsa esistente, assicurarsi che tooallow è.</span><span class="sxs-lookup"><span data-stu-id="0cd65-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="0cd65-175">Dopo questo comando ha esito positivo, l'app dovrebbe ora essere connesso toohello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="0cd65-176">successo tooconfirm, andare console app tooyour e digitare hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0cd65-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="0cd65-177">Se è presente una variabile di ambiente denominata WEBSITE_VNETNAME con un valore che corrisponde al nome di rete virtuale di destinazione hello hello, tutte le configurazioni hanno avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="0cd65-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="0cd65-178">Aggiornare le informazioni di integrazione rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="0cd65-178">Update classic VNet integration information</span></span>
<span data-ttu-id="0cd65-179">tooupdate o risincronizzare le informazioni, ripetere semplicemente i passaggi di hello eseguiti durante la creazione di integrazione hello in primo luogo hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="0cd65-180">I passaggi sono:</span><span class="sxs-lookup"><span data-stu-id="0cd65-180">Those steps are:</span></span>

1. <span data-ttu-id="0cd65-181">Definire le informazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0cd65-181">Define your configuration information.</span></span>
2. <span data-ttu-id="0cd65-182">Dichiarare app toohello di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="0cd65-183">Ottenere il pacchetto di hello point-to-site.</span><span class="sxs-lookup"><span data-stu-id="0cd65-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="0cd65-184">Caricare hello pacchetto point-to-site tooyour app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="0cd65-185">Disconnettere l'app da una rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="0cd65-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="0cd65-186">toodisconnect hello app, è necessario hello le informazioni di configurazione è state impostate durante l'integrazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="0cd65-187">Utilizzo di tali informazioni, è quindi un comando toodisconnect l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="0cd65-188">Reti virtuali di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0cd65-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="0cd65-189">Le reti virtuali di Azure Resource Manager usano le API di Azure Resource Manager, che permettono di semplificare alcuni processi rispetto alle reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="0cd65-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="0cd65-190">Si dispone di uno script che consentirà di completare hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="0cd65-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="0cd65-191">Creare una rete virtuale di Azure Resource Manager e integrarla con l'app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="0cd65-192">Creare un gateway, configurare la connettività da punto a sito in una rete virtuale di Azure Resource Manager esistente e quindi integrarla con l'app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="0cd65-193">Integrare l'app con una rete virtuale di Azure Resource Manager esistente che abbia un gateway e la connettività da punto a sito abilitata.</span><span class="sxs-lookup"><span data-stu-id="0cd65-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="0cd65-194">Disconnettere l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="0cd65-195">Script di integrazione del servizio app della rete virtuale di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0cd65-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="0cd65-196">Copiare hello seguente script e salvarlo come file tooa.</span><span class="sxs-lookup"><span data-stu-id="0cd65-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="0cd65-197">Se non si desidera script hello toouse, ritiene toolearn disponibile da esso toosee come le operazioni tooset con una rete virtuale di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="0cd65-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="0cd65-198">Salvare una copia dello script hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-198">Save a copy of hello script.</span></span> <span data-ttu-id="0cd65-199">In questo articolo è denominato V2VnetAllinOne.ps1, ma è possibile usare un altro nome.</span><span class="sxs-lookup"><span data-stu-id="0cd65-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="0cd65-200">Non sono presenti argomenti su questo script.</span><span class="sxs-lookup"><span data-stu-id="0cd65-200">There are no arguments for this script.</span></span> <span data-ttu-id="0cd65-201">È sufficiente eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="0cd65-201">You simply run it.</span></span> <span data-ttu-id="0cd65-202">Hello in primo luogo script hello eseguirà viene chiesto toosign in.</span><span class="sxs-lookup"><span data-stu-id="0cd65-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="0cd65-203">Dopo l'accesso, script hello Ottiene i dettagli sull'account dell'utente e restituisce un elenco di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="0cd65-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="0cd65-204">Il conteggio non richiesta hello per le credenziali, l'esecuzione dello script iniziale hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd65-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="0cd65-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="0cd65-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="0cd65-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="0cd65-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="0cd65-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="0cd65-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="0cd65-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="0cd65-208">Choose an option: 3</span></span>

    <span data-ttu-id="0cd65-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="0cd65-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="0cd65-210">Immettere il gruppo di risorse dell'applicazione hello: hcdemo-rg immettere hello nome dell'App: v2vnetpowershell cosa si desidera toodo?</span><span class="sxs-lookup"><span data-stu-id="0cd65-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="0cd65-211">Aggiungere un'App di tooan nuova rete virtuale</span><span class="sxs-lookup"><span data-stu-id="0cd65-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="0cd65-212">Aggiungere un'App di tooan di rete virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="0cd65-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="0cd65-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="0cd65-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="0cd65-214">resto Hello di questa sezione viene spiegata ciascuna di queste tre opzioni.</span><span class="sxs-lookup"><span data-stu-id="0cd65-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="0cd65-215">Creare una rete virtuale di Azure Resource Manager ed eseguire l'integrazione</span><span class="sxs-lookup"><span data-stu-id="0cd65-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="0cd65-216">Selezionare una nuova rete virtuale che utilizza il modello di distribuzione di gestione risorse di hello e integrarlo con l'app, toocreate **1) aggiungere tooan una nuova rete virtuale App**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="0cd65-217">Questo verrà richiesto per il nome di rete virtuale hello hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="0cd65-218">In questo caso, come si può notare in hello seguenti impostazioni, si usa nome hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="0cd65-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="0cd65-219">script Hello fornisce informazioni dettagliate di hello sulla rete virtuale hello che viene creato.</span><span class="sxs-lookup"><span data-stu-id="0cd65-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="0cd65-220">Se desidera, è possibile modificare uno dei valori hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="0cd65-221">L'esecuzione di questo esempio, creata una rete virtuale con hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="0cd65-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="0cd65-222">Se si desidera toochange uno dei valori hello, digitare **Y** e apportare modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="0cd65-223">Quando si è soddisfatti con le impostazioni di rete virtuale hello, digitare **N** o premere INVIO quando viene richiesto di modificare le impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="0cd65-224">Da qui in fino al completamento, script hello sarà possibile conoscere alcune delle quali it' contenenti esegue fino all'avvio gateway di rete virtuale toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="0cd65-225">Questa operazione può richiedere tooan ora.</span><span class="sxs-lookup"><span data-stu-id="0cd65-225">That step can take up tooan hour.</span></span> <span data-ttu-id="0cd65-226">Durante questa fase, non esiste alcun indicatore di stato ma script hello consentono di sapere quando il gateway hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="0cd65-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="0cd65-227">Al termine dell'esecuzione dello script hello, viene indicato che **completato**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="0cd65-228">A questo punto, si avrà una rete virtuale di gestione delle risorse con nome hello e impostazioni selezionate.</span><span class="sxs-lookup"><span data-stu-id="0cd65-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="0cd65-229">La nuova rete virtuale è anche integrata con l'app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="0cd65-230">Integrare l'app con una rete di Azure Resource Manager preesistente</span><span class="sxs-lookup"><span data-stu-id="0cd65-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="0cd65-231">Quando si integra con una rete virtuale esistente, se si specifica una rete virtuale di gestione risorse che non dispone di un gateway o la connettività point-to-site, script hello imposterà che.</span><span class="sxs-lookup"><span data-stu-id="0cd65-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="0cd65-232">Se hello rete virtuale dispone già di questi aspetti, configurare, script hello passa toohello retta integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0cd65-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="0cd65-233">toostart questo processo, è sufficiente seleziona **2) aggiungere un tooan di rete virtuale esistente App**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="0cd65-234">Questa opzione funziona solo se si dispone di una rete virtuale di gestione delle risorse preesistenti in hello stessa sottoscrizione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="0cd65-235">Dopo aver selezionato l'opzione di hello, verrà visualizzato un elenco di reti virtuali di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="0cd65-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="0cd65-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="0cd65-236">v2demonetwork</span></span>
    2) <span data-ttu-id="0cd65-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="0cd65-237">v2pshell</span></span>
    3) <span data-ttu-id="0cd65-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="0cd65-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="0cd65-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="0cd65-239">v2asenetwork</span></span>
    5) <span data-ttu-id="0cd65-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="0cd65-240">v2pshell2</span></span>

    <span data-ttu-id="0cd65-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="0cd65-241">Choose an option: 5</span></span>

<span data-ttu-id="0cd65-242">Rete virtuale hello che si desidera toointegrate con, selezionare semplicemente.</span><span class="sxs-lookup"><span data-stu-id="0cd65-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="0cd65-243">Se si dispone già di un gateway che disponga della connettività point-to-site abilitata, script hello integrerà semplicemente l'app con la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd65-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="0cd65-244">Se non si dispone di un gateway, è necessario toospecify subnet del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="0cd65-245">La subnet del gateway deve trovarsi nello spazio di indirizzi della rete virtuale e non può essere in un'altra subnet.</span><span class="sxs-lookup"><span data-stu-id="0cd65-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="0cd65-246">Se si esegue questo passaggio con una rete virtuale priva di gateway, il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd65-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="0cd65-247">In questo esempio, creato un gateway di rete virtuale che dispone di hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="0cd65-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="0cd65-248">Se si desidera toochange le impostazioni, è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="0cd65-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="0cd65-249">In caso contrario, premere INVIO e script hello verrà creato il gateway e collegare la rete virtuale tooyour di app.</span><span class="sxs-lookup"><span data-stu-id="0cd65-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="0cd65-250">ora di creazione gateway Hello è ancora un'ora, tuttavia, assicurarsi che si tenere presente.</span><span class="sxs-lookup"><span data-stu-id="0cd65-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="0cd65-251">Al termine, tutti gli elementi script hello indicherà **completato**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="0cd65-252">Disconnettere l'app da una rete virtuale di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0cd65-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="0cd65-253">L'app di disconnessione dalla rete virtuale non portare offline il gateway hello o disabilitare la connettività point-to-site.</span><span class="sxs-lookup"><span data-stu-id="0cd65-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="0cd65-254">perché potrebbero essere usati da altri processi.</span><span class="sxs-lookup"><span data-stu-id="0cd65-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="0cd65-255">Inoltre non la disconnessione da qualsiasi altra App diversi da hello uno fornito.</span><span class="sxs-lookup"><span data-stu-id="0cd65-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="0cd65-256">tooperform questa azione, seleziona **3) rimuovere una rete virtuale da un'App**.</span><span class="sxs-lookup"><span data-stu-id="0cd65-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="0cd65-257">Il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd65-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="0cd65-258">Sebbene script hello delete è, significa che non elimina la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="0cd65-259">Sta rimuovendo semplicemente integrazione hello.</span><span class="sxs-lookup"><span data-stu-id="0cd65-259">It’s just removing hello integration.</span></span> <span data-ttu-id="0cd65-260">Dopo aver verificato che sia quella desiderata, toodo comando hello viene elaborato molto rapidamente e indica **True** al termine.</span><span class="sxs-lookup"><span data-stu-id="0cd65-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
