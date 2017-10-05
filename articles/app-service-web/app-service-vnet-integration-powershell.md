---
title: Connettere l'app alla rete virtuale tramite PowerShell
description: Istruzioni sulla connessione e l'uso di reti virtuali con PowerShell
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
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="39dee-103">Connettere l'app alla rete virtuale tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="39dee-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="39dee-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="39dee-104">Overview</span></span>
<span data-ttu-id="39dee-105">Nel servizio app di Azure è possibile connettere l'app Web, l'app per dispositivi mobili o l'app per le API a una rete virtuale (VNet) di Azure nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="39dee-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="39dee-106">Questa funzionalità è detta integrazione rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="39dee-107">La funzionalità di integrazione rete virtuale non deve essere confusa con la funzionalità Ambiente del servizio app, che consente di eseguire un'istanza del servizio app di Azure nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="39dee-108">La funzionalità di integrazione rete virtuale ha un'interfaccia utente nel nuovo portale che può essere usata per l'integrazione con le reti virtuali che vengono distribuite tramite il modello di distribuzione classica o il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39dee-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="39dee-109">Per altre informazioni sulla funzionalità, vedere [Integrare un'app in una rete virtuale di Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="39dee-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="39dee-110">Questo articolo non illustra l'uso dell'interfaccia utente, ma piuttosto come abilitare l'integrazione usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39dee-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="39dee-111">Poiché ogni modello di distribuzione ha comandi diversi, questo articolo contiene una sezione per ogni modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="39dee-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="39dee-112">Prima di continuare con l'articolo, verificare la disponibilità di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="39dee-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="39dee-113">SDK di Azure PowerShell più recente.</span><span class="sxs-lookup"><span data-stu-id="39dee-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="39dee-114">Per installarlo, è possibile usare l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="39dee-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="39dee-115">Un'app nel servizio app di Azure in esecuzione all'interno di uno SKU Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="39dee-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="39dee-116">Reti virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="39dee-116">Classic virtual networks</span></span>
<span data-ttu-id="39dee-117">Questa sezione illustra tre attività per le reti virtuali che usano il modello di distribuzione classica:</span><span class="sxs-lookup"><span data-stu-id="39dee-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="39dee-118">Collegare l'app a una rete virtuale preesistente dotata di gateway e configurata per la connettività da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="39dee-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="39dee-119">Aggiornare le informazioni di integrazione della rete virtuale per l'app</span><span class="sxs-lookup"><span data-stu-id="39dee-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="39dee-120">Disconnettere l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="39dee-121">Connettere un'app a una rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="39dee-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="39dee-122">Per connettere un'app a una rete virtuale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="39dee-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="39dee-123">Dichiarare all'app Web l'aggiunta a una rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="39dee-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="39dee-124">L'app genera un certificato che viene trasmesso alla rete virtuale per la connettività da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="39dee-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="39dee-125">Caricare il certificato dell'app Web nella rete virtuale e quindi recuperare l'URI del pacchetto VPN da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="39dee-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="39dee-126">Aggiornare la connessione alla rete virtuale dell'app Web con l'URI del pacchetto da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="39dee-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="39dee-127">Il primo e il terzo passaggio sono completamente configurabili tramite script, mentre il secondo passaggio richiede un'unica azione manuale tramite il portale o l'accesso per eseguire azioni **PUT** o **PATCH** sull'endpoint di Azure Resource Manager della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="39dee-128">Contattare il supporto di Azure per questa opzione.</span><span class="sxs-lookup"><span data-stu-id="39dee-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="39dee-129">Prima di iniziare, assicurarsi che sia già abilitata una rete virtuale classica con connettività da punto a sito e che sia disponibile un gateway distribuito.</span><span class="sxs-lookup"><span data-stu-id="39dee-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="39dee-130">Per creare il gateway e abilitare la connettività da punto a sito, è necessario usare il portale, come descritto in [Creazione di un gateway VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="39dee-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="39dee-131">La rete virtuale classica deve essere nella stessa sottoscrizione del piano di servizio app che contiene l'app con cui si sta eseguendo l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="39dee-132">Configurare Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="39dee-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="39dee-133">Aprire una finestra di PowerShell e configurare l'account e la sottoscrizione di Azure con:</span><span class="sxs-lookup"><span data-stu-id="39dee-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="39dee-134">Il comando consente di aprire un prompt per ricevere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="39dee-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="39dee-135">Dopo l'accesso, usare uno dei comandi seguenti per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="39dee-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="39dee-136">Assicurarsi di usare la sottoscrizione che include la rete virtuale e il piano di servizio app usati.</span><span class="sxs-lookup"><span data-stu-id="39dee-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="39dee-137">oppure</span><span class="sxs-lookup"><span data-stu-id="39dee-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="39dee-138">Variabili usate in questo articolo</span><span class="sxs-lookup"><span data-stu-id="39dee-138">Variables used in this article</span></span>
<span data-ttu-id="39dee-139">Per semplificare i comandi, verrà impostata una variabile **$Configuration** di PowerShell con la configurazione specifica.</span><span class="sxs-lookup"><span data-stu-id="39dee-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="39dee-140">Impostare la variabile in PowerShell secondo la procedura riportata di seguito, usare i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="39dee-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="39dee-141">La località dell'app non deve contenere spazi.</span><span class="sxs-lookup"><span data-stu-id="39dee-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="39dee-142">Ad esempio West US, per gli Stati Uniti occidentali, sarà westus.</span><span class="sxs-lookup"><span data-stu-id="39dee-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="39dee-143">Il prossimo elemento identifica il percorso in cui deve essere scritto il certificato.</span><span class="sxs-lookup"><span data-stu-id="39dee-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="39dee-144">Deve essere un percorso accessibile in scrittura nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="39dee-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="39dee-145">Assicurarsi di includere .cer alla fine.</span><span class="sxs-lookup"><span data-stu-id="39dee-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="39dee-146">Per verificare le impostazioni applicate, digitare **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="39dee-146">To see what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="39dee-147">Nella parte restante di questa sezione si presuppone che sia stata creata una variabile come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="39dee-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="39dee-148">Dichiarare la rete virtuale all'app</span><span class="sxs-lookup"><span data-stu-id="39dee-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="39dee-149">Usare il comando seguente per indicare all'app che verrà usata questa rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="39dee-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="39dee-150">In questo modo l'app genererà i certificati necessari:</span><span class="sxs-lookup"><span data-stu-id="39dee-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="39dee-151">Se il comando ha esito positivo, **$vnet** deve contenere una variabile **Properties**.</span><span class="sxs-lookup"><span data-stu-id="39dee-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="39dee-152">La variabile **Properties** deve contenere sia un'identificazione personale del certificato che i dati del certificato.</span><span class="sxs-lookup"><span data-stu-id="39dee-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="39dee-153">Caricare il certificato dell'app Web nella rete virtuale</span><span class="sxs-lookup"><span data-stu-id="39dee-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="39dee-154">Per ogni combinazione di sottoscrizione e rete virtuale è necessario eseguire un unico passaggio manuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="39dee-155">Se, ad esempio, si connettono le app della Sottoscrizione A alla Rete virtuale A, è necessario eseguire questo passaggio solo una volta, indipendentemente dal numero di app da configurare.</span><span class="sxs-lookup"><span data-stu-id="39dee-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="39dee-156">Se si aggiunge una nuova app a un'altra rete virtuale, sarà necessario ripetere l'operazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="39dee-157">Il motivo è che il set di certificati generato a livello di sottoscrizione nel servizio app di Azure viene generato una sola volta per ogni rete virtuale a cui le app si devono connettere.</span><span class="sxs-lookup"><span data-stu-id="39dee-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="39dee-158">Se è stata seguita la procedura oppure è stata eseguita l'integrazione con la stessa rete virtuale tramite il portale, i certificati sono già impostati.</span><span class="sxs-lookup"><span data-stu-id="39dee-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="39dee-159">Il primo passaggio consiste nel generare il file con estensione .cer.</span><span class="sxs-lookup"><span data-stu-id="39dee-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="39dee-160">Il secondo passaggio consiste nel caricare il file CER nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="39dee-161">Per generare il file. cer dalla chiamata dell'API descritta nel passaggio precedente, eseguire i comandi riportati in basso.</span><span class="sxs-lookup"><span data-stu-id="39dee-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="39dee-162">Il certificato si trova nel percorso specificato da **$Configuration.GeneratedCertificatePath** .</span><span class="sxs-lookup"><span data-stu-id="39dee-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="39dee-163">Per caricare il certificato manualmente, usare il [portale di Azure][azureportal] e selezionare **Esplora > Rete virtuale (versione classica)** > **Connessioni VPN** > **Da punto a sito** > **Gestisci certificati**.</span><span class="sxs-lookup"><span data-stu-id="39dee-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="39dee-164">A questo punto, caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="39dee-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="39dee-165">Ottenere il pacchetto da punto a sito</span><span class="sxs-lookup"><span data-stu-id="39dee-165">Get the point-to-site package</span></span>
<span data-ttu-id="39dee-166">Il passaggio successivo nella configurazione di una connessione di rete virtuale in un'app Web consiste nell'ottenere il pacchetto da punto a sito per fornirlo all'app Web.</span><span class="sxs-lookup"><span data-stu-id="39dee-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="39dee-167">Salvare il modello seguente in un file denominato GetNetworkPackageUri.json in un percorso nel computer, ad esempio in C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="39dee-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="39dee-168">Impostare i parametri di input:</span><span class="sxs-lookup"><span data-stu-id="39dee-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="39dee-169">Chiamare lo script:</span><span class="sxs-lookup"><span data-stu-id="39dee-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="39dee-170">La variabile **$output.Outputs.packageUri** contiene ora il pacchetto URI da fornire all'app Web.</span><span class="sxs-lookup"><span data-stu-id="39dee-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="39dee-171">Caricare il pacchetto da punto a sito nell'app</span><span class="sxs-lookup"><span data-stu-id="39dee-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="39dee-172">Il passaggio finale consiste nell'assegnazione del pacchetto all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="39dee-173">È sufficiente eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="39dee-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="39dee-174">Potrebbe essere visualizzato un messaggio che richiede la conferma della sovrascrittura di una risorsa esistente. Confermare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="39dee-175">Se il comando ha esito positivo, l'app dovrebbe essere connessa alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="39dee-176">Verificare passando alla console dell'app e digitando quanto segue:</span><span class="sxs-lookup"><span data-stu-id="39dee-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="39dee-177">Se è presente una variabile di ambiente denominata WEBSITE_VNETNAME con un valore corrispondente al nome della rete virtuale di destinazione, tutte le configurazioni sono state completate.</span><span class="sxs-lookup"><span data-stu-id="39dee-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="39dee-178">Aggiornare le informazioni di integrazione rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="39dee-178">Update classic VNet integration information</span></span>
<span data-ttu-id="39dee-179">Per aggiornare o risincronizzare le informazioni è sufficiente ripetere i passaggi seguiti per la creazione dell'integrazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="39dee-180">I passaggi sono:</span><span class="sxs-lookup"><span data-stu-id="39dee-180">Those steps are:</span></span>

1. <span data-ttu-id="39dee-181">Definire le informazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-181">Define your configuration information.</span></span>
2. <span data-ttu-id="39dee-182">Dichiarare la rete virtuale all'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="39dee-183">Ottenere il pacchetto da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="39dee-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="39dee-184">Caricare il pacchetto da punto a sito nell'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="39dee-185">Disconnettere l'app da una rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="39dee-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="39dee-186">Per disconnettere l'app sono necessarie le informazioni di configurazione impostate durante l'integrazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="39dee-187">Con tali informazioni, è possibile usare un unico comando per disconnettere l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="39dee-188">Reti virtuali di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39dee-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="39dee-189">Le reti virtuali di Azure Resource Manager usano le API di Azure Resource Manager, che permettono di semplificare alcuni processi rispetto alle reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="39dee-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="39dee-190">È disponibile uno script che consente completare le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="39dee-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="39dee-191">Creare una rete virtuale di Azure Resource Manager e integrarla con l'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="39dee-192">Creare un gateway, configurare la connettività da punto a sito in una rete virtuale di Azure Resource Manager esistente e quindi integrarla con l'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="39dee-193">Integrare l'app con una rete virtuale di Azure Resource Manager esistente che abbia un gateway e la connettività da punto a sito abilitata.</span><span class="sxs-lookup"><span data-stu-id="39dee-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="39dee-194">Disconnettere l'app dalla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="39dee-195">Script di integrazione del servizio app della rete virtuale di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39dee-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="39dee-196">Copiare lo script seguente e salvarlo in un file.</span><span class="sxs-lookup"><span data-stu-id="39dee-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="39dee-197">Se si preferisce non usare lo script, è comunque possibile prenderne spunto per la configurazione di una rete virtuale di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39dee-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
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
            Write-Host "Currently, I will create a VNET with the following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
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
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
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

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
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
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
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

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

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

<span data-ttu-id="39dee-198">Salvare una copia dello script.</span><span class="sxs-lookup"><span data-stu-id="39dee-198">Save a copy of the script.</span></span> <span data-ttu-id="39dee-199">In questo articolo è denominato V2VnetAllinOne.ps1, ma è possibile usare un altro nome.</span><span class="sxs-lookup"><span data-stu-id="39dee-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="39dee-200">Non sono presenti argomenti su questo script.</span><span class="sxs-lookup"><span data-stu-id="39dee-200">There are no arguments for this script.</span></span> <span data-ttu-id="39dee-201">È sufficiente eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="39dee-201">You simply run it.</span></span> <span data-ttu-id="39dee-202">La prima azione eseguita dallo script è la richiesta di accesso.</span><span class="sxs-lookup"><span data-stu-id="39dee-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="39dee-203">Dopo l'accesso, lo script ottiene i dettagli sull'account dell'utente e restituisce un elenco di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="39dee-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="39dee-204">Senza la richiesta di credenziali, l'esecuzione dello script iniziale è simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="39dee-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="39dee-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="39dee-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="39dee-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="39dee-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="39dee-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="39dee-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="39dee-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="39dee-208">Choose an option: 3</span></span>

    <span data-ttu-id="39dee-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="39dee-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="39dee-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span><span class="sxs-lookup"><span data-stu-id="39dee-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="39dee-211">Add a NEW Virtual Network to an App</span><span class="sxs-lookup"><span data-stu-id="39dee-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="39dee-212">Add an EXISTING Virtual Network to an App</span><span class="sxs-lookup"><span data-stu-id="39dee-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="39dee-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="39dee-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="39dee-214">La parte restante di questa sezione illustra ognuna delle tre opzioni.</span><span class="sxs-lookup"><span data-stu-id="39dee-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="39dee-215">Creare una rete virtuale di Azure Resource Manager ed eseguire l'integrazione</span><span class="sxs-lookup"><span data-stu-id="39dee-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="39dee-216">Per creare una nuova rete virtuale che usa il modello di distribuzione Azure Resource Manager e integrarla con l'app, selezionare l'opzione **1) Add a NEW Virtual Network to an App**.</span><span class="sxs-lookup"><span data-stu-id="39dee-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="39dee-217">Verrà richiesto il nome della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="39dee-218">In questo caso è stato usato il nome v2pshell, come risulta nelle impostazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="39dee-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="39dee-219">Lo script restituisce i dettagli della rete virtuale che si sta creando.</span><span class="sxs-lookup"><span data-stu-id="39dee-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="39dee-220">Se si desidera, è possibile modificare qualsiasi valori.</span><span class="sxs-lookup"><span data-stu-id="39dee-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="39dee-221">In questo esempio è stata creata una rete virtuale con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="39dee-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="39dee-222">Per modificare uno dei valori, digitare **Y** e apportare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="39dee-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="39dee-223">Dopo aver configurato tutte le impostazioni della rete virtuale, digitare **N** o premere INVIO quando viene richiesto di modificare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="39dee-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="39dee-224">Da quel punto in poi, lo script indicherà alcune delle attività in esecuzione fino alla creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="39dee-225">Questo passaggio può richiedere fino a un'ora.</span><span class="sxs-lookup"><span data-stu-id="39dee-225">That step can take up to an hour.</span></span> <span data-ttu-id="39dee-226">In questa fase non è disponibile un indicatore di stato, ma verrà comunicata l'avvenuta creazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="39dee-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="39dee-227">Al termine dell'operazione, lo script visualizza il messaggio **Finished**.</span><span class="sxs-lookup"><span data-stu-id="39dee-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="39dee-228">A questo punto è disponibile una rete virtuale di Azure Resource Manager con il nome e le impostazioni selezionate.</span><span class="sxs-lookup"><span data-stu-id="39dee-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="39dee-229">La nuova rete virtuale è anche integrata con l'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="39dee-230">Integrare l'app con una rete di Azure Resource Manager preesistente</span><span class="sxs-lookup"><span data-stu-id="39dee-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="39dee-231">Quando si esegue l'integrazione specificando una rete virtuale di Azure Resource Manager esistente priva di gateway e connettività da punto a sito, questi vengono impostati dallo script.</span><span class="sxs-lookup"><span data-stu-id="39dee-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="39dee-232">Se la rete virtuale ha già queste impostazioni, lo script passa direttamente all'integrazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="39dee-233">Per avviare il processo è sufficiente selezionare l'opzione **2) Add an EXISTING Virtual Network to an App**.</span><span class="sxs-lookup"><span data-stu-id="39dee-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="39dee-234">Questa opzione funziona solo se la rete virtuale di Azure Resource Manager preesistente è nella stessa sottoscrizione dell'app.</span><span class="sxs-lookup"><span data-stu-id="39dee-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="39dee-235">Dopo aver selezionato l'opzione, viene visualizzato un elenco delle reti virtuali di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39dee-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="39dee-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="39dee-236">v2demonetwork</span></span>
    2) <span data-ttu-id="39dee-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="39dee-237">v2pshell</span></span>
    3) <span data-ttu-id="39dee-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="39dee-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="39dee-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="39dee-239">v2asenetwork</span></span>
    5) <span data-ttu-id="39dee-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="39dee-240">v2pshell2</span></span>

    <span data-ttu-id="39dee-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="39dee-241">Choose an option: 5</span></span>

<span data-ttu-id="39dee-242">Selezionare la rete virtuale con cui si vuole eseguire l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="39dee-243">Se è già disponibile un gateway con la connettività da punto a sito abilitata, lo script procede direttamente all'integrazione dell'app con la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="39dee-244">Se non è disponibile un gateway, è necessario specificare la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="39dee-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="39dee-245">La subnet del gateway deve trovarsi nello spazio di indirizzi della rete virtuale e non può essere in un'altra subnet.</span><span class="sxs-lookup"><span data-stu-id="39dee-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="39dee-246">Se si esegue questo passaggio con una rete virtuale priva di gateway, il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="39dee-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="39dee-247">In questo esempio è stato creato un gateway di rete virtuale con le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="39dee-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="39dee-248">Le impostazioni possono essere modificate in base alle preferenze.</span><span class="sxs-lookup"><span data-stu-id="39dee-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="39dee-249">In caso contrario, premere INVIO. Lo script creerà il gateway e collegherà l'app alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="39dee-250">Tenere presente che il tempo necessario per la creazione del gateway è un'ora.</span><span class="sxs-lookup"><span data-stu-id="39dee-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="39dee-251">Al termine di tutte le operazioni, lo script visualizza il messaggio **Finished**.</span><span class="sxs-lookup"><span data-stu-id="39dee-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="39dee-252">Disconnettere l'app da una rete virtuale di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="39dee-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="39dee-253">La disconnessione dell'app dalla rete virtuale non provoca l'arresto del gateway e non disabilita la connettività da punto a sito,</span><span class="sxs-lookup"><span data-stu-id="39dee-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="39dee-254">perché potrebbero essere usati da altri processi.</span><span class="sxs-lookup"><span data-stu-id="39dee-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="39dee-255">La rete virtuale viene disconnessa unicamente dall'app specificata e da nessun'altra app.</span><span class="sxs-lookup"><span data-stu-id="39dee-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="39dee-256">Per eseguire questa operazione, selezionare l'opzione **3) Remove a Virtual Network from an App**.</span><span class="sxs-lookup"><span data-stu-id="39dee-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="39dee-257">Il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="39dee-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="39dee-258">Anche se lo script usa il termine "delete", non elimina effettivamente la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="39dee-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="39dee-259">Rimuove solo l'integrazione.</span><span class="sxs-lookup"><span data-stu-id="39dee-259">It’s just removing the integration.</span></span> <span data-ttu-id="39dee-260">Dopo la conferma dell'utente, il comando viene elaborato molto rapidamente e al termine restituisce **True** .</span><span class="sxs-lookup"><span data-stu-id="39dee-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
