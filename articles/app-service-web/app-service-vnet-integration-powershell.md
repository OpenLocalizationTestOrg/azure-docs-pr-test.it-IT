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
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>La connessione di rete virtuale tooyour app tramite PowerShell
## <a name="overview"></a>Panoramica
Nel servizio App di Azure, è possibile connettere l'app (web, mobili o API) tooan rete virtuale di Azure (VNet) nella sottoscrizione. Questa funzionalità è detta integrazione rete virtuale. funzionalità di integrazione della rete virtuale Hello non deve essere confuso con la funzionalità dell'ambiente del servizio App di hello, che permette toorun un'istanza di servizio App di Azure nella rete virtuale.

la funzionalità di integrazione della rete virtuale Hello ha un'interfaccia utente (UI) nel nuovo portale di hello che è possibile utilizzare toointegrate con le reti virtuali che vengono distribuite tramite il modello di distribuzione classica hello o modello di distribuzione Azure Resource Manager hello. Per ulteriori informazioni sulla funzionalità hello toolearn, vedere [integrare l'app con una rete virtuale di Azure](web-sites-integrate-with-vnet.md).

In questo articolo è non sulla modalità toouse hello dell'interfaccia utente, ma piuttosto sull'integrazione tooenable tramite PowerShell. Poiché i comandi di hello per ogni modello di distribuzione sono diversi, in questo articolo contiene una sezione per ogni modello di distribuzione.  

Prima di continuare con l'articolo, verificare la disponibilità di quanto segue:

* Hello che più recente di Azure PowerShell SDK installato. È possibile installarlo con hello installazione guidata piattaforma Web.
* Un'app nel servizio app di Azure in esecuzione all'interno di uno SKU Standard o Premium.

## <a name="classic-virtual-networks"></a>Reti virtuali classiche
Questa sezione vengono illustrate tre attività per le reti virtuali che utilizzano il modello di distribuzione classica hello:

1. Connettere l'app tooa preesistenti rete virtuale che dispone di un gateway ed è configurata per la connettività point-to-site.
2. Aggiornare le informazioni di integrazione della rete virtuale per l'app
3. Disconnettere l'app dalla rete virtuale.

### <a name="connect-an-app-tooa-classic-vnet"></a>Connettersi a un'app tooa classico rete virtuale
tooconnect una rete virtuale tooa app, seguire questi tre passaggi:

1. Dichiarare toohello web app che verrà aggiunta una rete virtuale specifica. app Hello genererà un certificato che verrà assegnato toohello di rete virtuale per la connettività point-to-site.
2. Caricamento di rete virtuale di hello web app certificato toohello e quindi recuperare l'URI del pacchetto VPN point-to-site hello.
3. Aggiornare la connessione di rete virtuale dell'applicazione web hello con l'URI del pacchetto hello point-to-site.

Hello primo e il terzi passaggi sono interamente configurabile tramite script, ma secondo passaggio hello richiede un'azione manuale monouso tramite il portale di hello o accesso tooperform **inserire** o **PATCH** azioni nella rete virtuale hello Endpoint di gestione risorse di Azure. Contattare questo abilitato toohave supporto tecnico di Azure. Prima di iniziare, assicurarsi che sia già abilitata una rete virtuale classica con connettività da punto a sito e che sia disponibile un gateway distribuito. toocreate hello gateway e abilitare point-to-site connettività, è necessario portale hello toouse come descritto in [creazione di un gateway VPN][createvpngateway].

rete virtuale classica Hello deve toobe in hello stessa sottoscrizione del servizio App del piano che si sta integrando con app hello contiene.

##### <a name="set-up-azure-powershell-sdk"></a>Configurare Azure PowerShell SDK
Aprire una finestra di PowerShell e configurare l'account e la sottoscrizione di Azure con:

    Login-AzureRmAccount

Tale comando consente di aprire un prompt dei comandi tooget le credenziali di Azure. Dopo l'accesso, utilizzare uno dei seguenti sottoscrizione hello tooselect di comandi che si desidera toouse hello. Assicurarsi che si utilizza sottoscrizione hello presenti tra la rete virtuale e un piano di servizio App.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

oppure

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variabili usate in questo articolo
i comandi toosimplify, si imposterà una **$Configuration** variabile PowerShell con configurazione specifica hello.

Impostare una variabile come indicato di seguito in PowerShell con hello seguenti parametri:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

percorso dell'app Hello deve essere il percorso di hello senza spazi. Ad esempio West US, per gli Stati Uniti occidentali, sarà westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

elemento successivo Hello è dove certificato hello deve essere scritti. Deve essere un percorso accessibile in scrittura nel computer locale. Assicurarsi che con estensione cer tooinclude alla fine di hello.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee è impostato, tipo **$Configuration**.

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

resto Hello di questa sezione presuppone che si disponga di una variabile creata come descritto in precedenza.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Dichiarare hello rete virtuale toohello app
Utilizzare hello successivo comando tootell hello app che verrà utilizzato questa rete virtuale specifica. In questo modo hello app toogenerate certificati necessari:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Se il comando ha esito positivo, **$vnet** deve contenere una variabile **Properties**. Hello **proprietà** variabile deve contenere sia un certificato hello e identificazione personale certificato i dati.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Caricare una rete virtuale di hello web app certificato toohello
Per ogni combinazione di sottoscrizione e rete virtuale è necessario eseguire un unico passaggio manuale. Ovvero, se ci si connette l'App in una rete tooVirtual sottoscrizione, è necessario toodo questo passaggio solo una volta indipendentemente dal numero App configurato. Se si aggiunge una nuova rete virtuale tooanother di app, occorre toodo più questo messaggio. motivo Hello è che viene generato un set di certificati a livello di sottoscrizione in Azure App Service e set hello viene generato una volta per ogni rete virtuale a cui si connetterà hello app.

Hello certificati verranno sono già stati impostati se sono state seguite le operazioni o se è integrata con hello stessa rete virtuale tramite il portale di hello.

primo passaggio Hello è file con estensione cer toogenerate hello. secondo passaggio Hello è rete virtuale di tooupload hello. cer file tooyour. file con estensione cer hello toogenerate dalla chiamata all'API hello in hello passaggio precedente, eseguire hello i comandi seguenti.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certificato Hello sarà disponibile nel percorso hello che **$Configuration.GeneratedCertificatePath** specifica.

certificato hello tooupload manualmente, utilizzare hello [portale di Azure] [ azureportal] e **esplorare la rete virtuale (classico)** > **le connessioni VPN**  >  **Point-to-site** > **gestire i certificati**. A questo punto, caricare il certificato.

##### <a name="get-hello-point-to-site-package"></a>Ottenere il pacchetto di hello point-to-site
passaggio successivo di Hello nell'impostazione di una connessione di rete virtuale in un'app web è tooget hello point-to-site pacchetto e fornirlo tooyour web app.

Salvare i seguenti file di modello tooa chiamato GetNetworkPackageUri.json in un punto qualsiasi nel computer in uso, ad esempio, C:\Azure\Templates\GetNetworkPackageUri.json hello.

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


Impostare i parametri di input:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Chiamare hello script:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


variabile Hello **$output. Outputs.packageUri** conterrà hello pacchetto URI toobe dato tooyour web app.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Caricare hello pacchetto point-to-site tooyour app
passaggio finale Hello è tooprovide hello app con questo pacchetto. Comando successivo hello è sufficiente eseguire:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Se un messaggio richiederà tooconfirm si sovrascrive una risorsa esistente, assicurarsi che tooallow è.

Dopo questo comando ha esito positivo, l'app dovrebbe ora essere connesso toohello rete virtuale. successo tooconfirm, andare console app tooyour e digitare hello riportato di seguito:

    SET WEBSITE_

Se è presente una variabile di ambiente denominata WEBSITE_VNETNAME con un valore che corrisponde al nome di rete virtuale di destinazione hello hello, tutte le configurazioni hanno avuto esito positivo.

### <a name="update-classic-vnet-integration-information"></a>Aggiornare le informazioni di integrazione rete virtuale classica
tooupdate o risincronizzare le informazioni, ripetere semplicemente i passaggi di hello eseguiti durante la creazione di integrazione hello in primo luogo hello. I passaggi sono:

1. Definire le informazioni di configurazione.
2. Dichiarare app toohello di hello rete virtuale.
3. Ottenere il pacchetto di hello point-to-site.
4. Caricare hello pacchetto point-to-site tooyour app.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Disconnettere l'app da una rete virtuale classica
toodisconnect hello app, è necessario hello le informazioni di configurazione è state impostate durante l'integrazione della rete virtuale. Utilizzo di tali informazioni, è quindi un comando toodisconnect l'app dalla rete virtuale.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Reti virtuali di Azure Resource Manager
Le reti virtuali di Azure Resource Manager usano le API di Azure Resource Manager, che permettono di semplificare alcuni processi rispetto alle reti virtuali classiche. Si dispone di uno script che consentirà di completare hello seguenti attività:

* Creare una rete virtuale di Azure Resource Manager e integrarla con l'app.
* Creare un gateway, configurare la connettività da punto a sito in una rete virtuale di Azure Resource Manager esistente e quindi integrarla con l'app.
* Integrare l'app con una rete virtuale di Azure Resource Manager esistente che abbia un gateway e la connettività da punto a sito abilitata.
* Disconnettere l'app dalla rete virtuale.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script di integrazione del servizio app della rete virtuale di Azure Resource Manager
Copiare hello seguente script e salvarlo come file tooa. Se non si desidera script hello toouse, ritiene toolearn disponibile da esso toosee come le operazioni tooset con una rete virtuale di gestione risorse.

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

Salvare una copia dello script hello. In questo articolo è denominato V2VnetAllinOne.ps1, ma è possibile usare un altro nome. Non sono presenti argomenti su questo script. È sufficiente eseguirlo. Hello in primo luogo script hello eseguirà viene chiesto toosign in. Dopo l'accesso, script hello Ottiene i dettagli sull'account dell'utente e restituisce un elenco di sottoscrizioni. Il conteggio non richiesta hello per le credenziali, l'esecuzione dello script iniziale hello è simile al seguente:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Choose an option: 3

    Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47

    Immettere il gruppo di risorse dell'applicazione hello: hcdemo-rg immettere hello nome dell'App: v2vnetpowershell cosa si desidera toodo?

    1) Aggiungere un'App di tooan nuova rete virtuale
    2) Aggiungere un'App di tooan di rete virtuale esistente
    3) Remove a Virtual Network from an App

resto Hello di questa sezione viene spiegata ciascuna di queste tre opzioni.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Creare una rete virtuale di Azure Resource Manager ed eseguire l'integrazione
Selezionare una nuova rete virtuale che utilizza il modello di distribuzione di gestione risorse di hello e integrarlo con l'app, toocreate **1) aggiungere tooan una nuova rete virtuale App**. Questo verrà richiesto per il nome di rete virtuale hello hello. In questo caso, come si può notare in hello seguenti impostazioni, si usa nome hello, v2pshell.

script Hello fornisce informazioni dettagliate di hello sulla rete virtuale hello che viene creato. Se desidera, è possibile modificare uno dei valori hello. L'esecuzione di questo esempio, creata una rete virtuale con hello seguenti impostazioni:

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

Se si desidera toochange uno dei valori hello, digitare **Y** e apportare modifiche hello. Quando si è soddisfatti con le impostazioni di rete virtuale hello, digitare **N** o premere INVIO quando viene richiesto di modificare le impostazioni di hello. Da qui in fino al completamento, script hello sarà possibile conoscere alcune delle quali it' contenenti esegue fino all'avvio gateway di rete virtuale toocreate hello. Questa operazione può richiedere tooan ora. Durante questa fase, non esiste alcun indicatore di stato ma script hello consentono di sapere quando il gateway hello è stato creato.

Al termine dell'esecuzione dello script hello, viene indicato che **completato**. A questo punto, si avrà una rete virtuale di gestione delle risorse con nome hello e impostazioni selezionate. La nuova rete virtuale è anche integrata con l'app.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integrare l'app con una rete di Azure Resource Manager preesistente
Quando si integra con una rete virtuale esistente, se si specifica una rete virtuale di gestione risorse che non dispone di un gateway o la connettività point-to-site, script hello imposterà che. Se hello rete virtuale dispone già di questi aspetti, configurare, script hello passa toohello retta integrazione dell'applicazione. toostart questo processo, è sufficiente seleziona **2) aggiungere un tooan di rete virtuale esistente App**.

Questa opzione funziona solo se si dispone di una rete virtuale di gestione delle risorse preesistenti in hello stessa sottoscrizione dell'app. Dopo aver selezionato l'opzione di hello, verrà visualizzato un elenco di reti virtuali di gestione delle risorse.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Choose an option: 5

Rete virtuale hello che si desidera toointegrate con, selezionare semplicemente. Se si dispone già di un gateway che disponga della connettività point-to-site abilitata, script hello integrerà semplicemente l'app con la rete virtuale. Se non si dispone di un gateway, è necessario toospecify subnet del gateway hello. La subnet del gateway deve trovarsi nello spazio di indirizzi della rete virtuale e non può essere in un'altra subnet. Se si esegue questo passaggio con una rete virtuale priva di gateway, il risultato sarà simile al seguente:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

In questo esempio, creato un gateway di rete virtuale che dispone di hello seguenti impostazioni:

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

Se si desidera toochange le impostazioni, è possibile farlo. In caso contrario, premere INVIO e script hello verrà creato il gateway e collegare la rete virtuale tooyour di app. ora di creazione gateway Hello è ancora un'ora, tuttavia, assicurarsi che si tenere presente. Al termine, tutti gli elementi script hello indicherà **completato**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Disconnettere l'app da una rete virtuale di Azure Resource Manager
L'app di disconnessione dalla rete virtuale non portare offline il gateway hello o disabilitare la connettività point-to-site. perché potrebbero essere usati da altri processi. Inoltre non la disconnessione da qualsiasi altra App diversi da hello uno fornito. tooperform questa azione, seleziona **3) rimuovere una rete virtuale da un'App**. Il risultato sarà simile al seguente:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Sebbene script hello delete è, significa che non elimina la rete virtuale hello. Sta rimuovendo semplicemente integrazione hello. Dopo aver verificato che sia quella desiderata, toodo comando hello viene elaborato molto rapidamente e indica **True** al termine.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
