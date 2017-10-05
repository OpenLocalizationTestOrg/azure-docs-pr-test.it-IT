---
title: Creare, avviare o eliminare un gateway applicazione | Documentazione Microsoft
description: Questa pagina fornisce istruzioni per la creazione, la configurazione, l'avvio e l'eliminazione di un gateway applicazione di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: c4932096229b1941e0966e7f3e97de39c6931392
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="4b1d2-103">Creare, avviare o eliminare un gateway applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b1d2-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b1d2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d2-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="4b1d2-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b1d2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="4b1d2-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="4b1d2-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="4b1d2-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b1d2-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="4b1d2-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d2-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="4b1d2-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="4b1d2-110">Fornisce richieste HTTP con routing delle prestazioni e failover tra server diversi, sia nel cloud che in locale.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="4b1d2-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="4b1d2-112">Per un elenco completo delle funzionalità supportate, vedere [Panoramica del gateway applicazione](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4b1d2-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="4b1d2-113">Questo articolo illustra in dettaglio i passaggi necessari per creare e configurare, avviare ed eliminare un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4b1d2-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4b1d2-114">Before you begin</span></span>

1. <span data-ttu-id="4b1d2-115">Installare la versione più recente dei cmdlet di Azure PowerShell usando l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="4b1d2-116">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [pagina Download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="4b1d2-117">Se si ha una rete virtuale esistente, selezionare una subnet vuota esistente oppure creare una nuova subnet nella rete virtuale esclusivamente per l'uso da parte del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="4b1d2-118">Non è possibile distribuire il gateway applicazione in una rete virtuale diversa da quella delle risorse da distribuire dietro il gateway applicazione a meno che non venga usato il peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="4b1d2-119">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4b1d2-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="4b1d2-120">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="4b1d2-121">Assicurarsi che nessuna macchina virtuale o distribuzione cloud stia usando la subnet.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="4b1d2-122">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="4b1d2-123">È necessario che i server configurati per l'uso del gateway applicazione esistano oppure che i relativi endpoint siano stati creati nella rete virtuale o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="4b1d2-124">Elementi necessari per creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="4b1d2-125">Quando si usa il comando `New-AzureApplicationGateway` per creare il gateway applicazione, non è ancora stata impostata alcuna configurazione e la risorsa appena creata viene configurata usando XML o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="4b1d2-126">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="4b1d2-126">The values are:</span></span>

* <span data-ttu-id="4b1d2-127">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="4b1d2-128">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4b1d2-129">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4b1d2-130">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="4b1d2-131">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="4b1d2-132">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="4b1d2-133">**Listener** : ha una porta front-end, un protocollo (Http o Https, con distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4b1d2-134">**Regola** : associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="4b1d2-135">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-135">Create an application gateway</span></span>

<span data-ttu-id="4b1d2-136">Per creare un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="4b1d2-136">To create an application gateway:</span></span>

1. <span data-ttu-id="4b1d2-137">Creare una risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="4b1d2-138">Creare un file XML di configurazione o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="4b1d2-139">Eseguire il commit della configurazione nella risorsa del gateway applicazione appena creata.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="4b1d2-140">Se è necessario configurare un probe personalizzato per il gateway applicazione, vedere [Creare un probe personalizzato per il gateway applicazione di Azure con PowerShell per Azure Resource Manager](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-140">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="4b1d2-141">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="4b1d2-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Esempio dello scenario][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="4b1d2-143">Creare una risorsa del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-143">Create an application gateway resource</span></span>

<span data-ttu-id="4b1d2-144">Per creare il gateway, usare il cmdlet `New-AzureApplicationGateway`, sostituendo i valori esistenti con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="4b1d2-145">La fatturazione per il gateway non viene applicata a partire da questo punto.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="4b1d2-146">La fatturazione viene applicata a partire da un passaggio successivo, dopo l'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="4b1d2-147">L'esempio seguente mostra come creare un gateway applicazione usando una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="4b1d2-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="4b1d2-148">*Description*, *InstanceCount* e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="4b1d2-149">Per convalidare la creazione del gateway, è possibile usare il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="4b1d2-150">Il valore predefinito per *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-150">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4b1d2-151">Il valore predefinito per *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-151">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4b1d2-152">È possibile scegliere tra Small, Medium e Large.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="4b1d2-153">*VirtualIPs* e *DnsName* vengono visualizzati vuoti perché il gateway non è stato ancora avviato.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="4b1d2-154">Questi valori vengono creati quando il gateway è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="4b1d2-155">Configurare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-155">Configure the application gateway</span></span>

<span data-ttu-id="4b1d2-156">È possibile configurare il gateway applicazione usando XML o un oggetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="4b1d2-157">Configurare il gateway applicazione usando XML</span><span class="sxs-lookup"><span data-stu-id="4b1d2-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="4b1d2-158">Nell'esempio seguente viene usato un file XML per configurare tutte le impostazioni del gateway applicazione ed eseguirne il commit nella risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="4b1d2-159">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4b1d2-159">Step 1</span></span>

<span data-ttu-id="4b1d2-160">Copiare il testo seguente in Blocco note.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="4b1d2-161">Modificare i valori tra parentesi per gli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="4b1d2-162">Salvare il file con estensione XML.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b1d2-163">L'elemento del protocollo HTTP o HTTPS deve rispettare la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-163">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="4b1d2-164">L'esempio seguente mostra come usare un file di configurazione per configurare il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="4b1d2-165">L'esempio bilancia il carico del traffico HTTP sulla porta pubblica 80 e invia il traffico di rete alla porta back-end 80 tra i due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="4b1d2-166">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4b1d2-166">Step 2</span></span>

<span data-ttu-id="4b1d2-167">Configurare ora il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-167">Next, set the application gateway.</span></span> <span data-ttu-id="4b1d2-168">Usare il cmdlet `Set-AzureApplicationGatewayConfig` con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="4b1d2-169">Configurare il gateway applicazione usando un oggetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="4b1d2-170">L'esempio seguente mostra come configurare il gateway applicazione usando oggetti di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="4b1d2-171">Tutti gli elementi di configurazione devono essere configurati singolarmente e quindi aggiunti a un oggetto di configurazione del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="4b1d2-172">Dopo avere creato l'oggetto di configurazione, usare il comando `Set-AzureApplicationGateway` per eseguire il commit della configurazione nella risorsa per il gateway applicazione creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="4b1d2-173">Prima di assegnare un valore a ogni oggetto di configurazione, è necessario dichiarare quale tipologia di oggetto verrà usato da PowerShell per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-173">Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="4b1d2-174">La prima riga per creare i singoli elementi definisce cosa `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` viene usato.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-174">The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="4b1d2-175">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4b1d2-175">Step 1</span></span>

<span data-ttu-id="4b1d2-176">Creare tutti i singoli elementi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-176">Create all individual configuration items.</span></span>

<span data-ttu-id="4b1d2-177">Creare l'IP front-end, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="4b1d2-178">Creare la porta front-end, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="4b1d2-179">Creare il pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-179">Create the back-end server pool.</span></span>

<span data-ttu-id="4b1d2-180">Definire gli indirizzi IP che vengono aggiunti al pool di server back-end, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="4b1d2-181">Usare l'oggetto $server per aggiungere i valori all'oggetto pool back-end ($pool).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="4b1d2-182">Creare l'impostazione del pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="4b1d2-183">Creare il listener.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="4b1d2-184">Creare la regola.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="4b1d2-185">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4b1d2-185">Step 2</span></span>

<span data-ttu-id="4b1d2-186">Assegnare tutti i singoli elementi di configurazione a un oggetto di configurazione del gateway applicazione ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="4b1d2-187">Aggiungere l'IP front-end alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="4b1d2-188">Aggiungere la porta front-end alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="4b1d2-189">Aggiungere il pool di server back-end alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="4b1d2-190">Aggiungere l'impostazione del pool back-end alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="4b1d2-191">Aggiungere il listener alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="4b1d2-192">Aggiungere la regola alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="4b1d2-193">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="4b1d2-193">Step 3</span></span>
<span data-ttu-id="4b1d2-194">Eseguire il commit dell'oggetto di configurazione nella risorsa per il gateway applicazione usando `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="4b1d2-195">Avviare il gateway</span><span class="sxs-lookup"><span data-stu-id="4b1d2-195">Start the gateway</span></span>

<span data-ttu-id="4b1d2-196">Dopo la configurazione del gateway, usare il cmdlet `Start-AzureApplicationGateway` per avviarlo.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="4b1d2-197">La fatturazione per un gateway applicazione verrà applicata a partire dall'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="4b1d2-198">Il completamento del cmdlet `Start-AzureApplicationGateway` potrebbe richiedere fino a 15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-198">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="4b1d2-199">Verificare lo stato del gateway</span><span class="sxs-lookup"><span data-stu-id="4b1d2-199">Verify the gateway status</span></span>

<span data-ttu-id="4b1d2-200">Usare il cmdlet `Get-AzureApplicationGateway` per verificare lo stato del gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="4b1d2-201">Se nel passaggio precedente l'operazione `Start-AzureApplicationGateway` è riuscita, assumerà lo *stato* In esecuzione e i valori in *Vip* e *DnsName* saranno validi.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="4b1d2-202">L'esempio seguente illustra un gateway applicazione attivo, in esecuzione e pronto per accettare il traffico destinato a `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="4b1d2-203">Eliminare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="4b1d2-203">Delete the application gateway</span></span>

<span data-ttu-id="4b1d2-204">Per eliminare il gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="4b1d2-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="4b1d2-205">Usare il cmdlet `Stop-AzureApplicationGateway` per arrestare il gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="4b1d2-206">Usare il cmdlet `Remove-AzureApplicationGateway` per rimuovere il gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="4b1d2-207">Assicurarsi che il gateway sia stato rimosso usando il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="4b1d2-208">L'esempio seguente mostra il cmdlet `Stop-AzureApplicationGateway` sulla prima riga seguito dall'output.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="4b1d2-209">Quando il gateway applicazione si trova in stato di interruzione, usare il cmdlet `Remove-AzureApplicationGateway` per rimuovere il servizio.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="4b1d2-210">Per verificare che il servizio sia stato rimosso, è possibile usare il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="4b1d2-211">Questo passaggio non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="4b1d2-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="4b1d2-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b1d2-212">Next steps</span></span>

<span data-ttu-id="4b1d2-213">Per configurare l'offload SSL, vedere [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="4b1d2-214">Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, vedere [Creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="4b1d2-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4b1d2-215">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="4b1d2-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4b1d2-216">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d2-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4b1d2-217">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="4b1d2-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
