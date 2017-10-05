---
title: Uso di un gateway applicazione di Azure con un servizio di bilanciamento del carico interno | Documentazione Microsoft
description: Questa pagina fornisce le istruzioni per configurare un servizio Gateway applicazione di Azure con un endpoint con carico bilanciato interno
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="3a978-103">Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB)</span><span class="sxs-lookup"><span data-stu-id="3a978-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a978-104">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="3a978-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="3a978-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a978-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="3a978-106">Il gateway applicazione può essere configurato con un indirizzo IP virtuale con connessione Internet o con un endpoint interno non esposto a Internet, detto anche endpoint di bilanciamento del carico interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="3a978-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="3a978-107">Configurare il gateway con un ILB è utile per le applicazioni line-of-business interne non esposte a Internet.</span><span class="sxs-lookup"><span data-stu-id="3a978-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="3a978-108">È utile anche per i servizi o i livelli in un'applicazione multilivello che si trova entro un limite di sicurezza non esposto a Internet, ma che richiede la distribuzione del carico round robin, la persistenza delle sessioni o la terminazione SSL.</span><span class="sxs-lookup"><span data-stu-id="3a978-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="3a978-109">Questo articolo illustra la procedura per configurare un gateway applicazione con un ILB.</span><span class="sxs-lookup"><span data-stu-id="3a978-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a978-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3a978-110">Before you begin</span></span>

1. <span data-ttu-id="3a978-111">Installare la versione più recente dei cmdlet di Azure PowerShell mediante l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="3a978-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="3a978-112">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3a978-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="3a978-113">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="3a978-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="3a978-114">Assicurasi di avere server back-end nella rete virtuale o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="3a978-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="3a978-115">Per creare un nuovo gateway applicazione, eseguire i passaggi seguenti nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="3a978-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="3a978-116">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3a978-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="3a978-117">Configurare il gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="3a978-118">Definire la configurazione del gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="3a978-119">Avviare il gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="3a978-120">Verificare il gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="3a978-121">Creare un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="3a978-121">Create an application gateway:</span></span>

<span data-ttu-id="3a978-122">**Per creare il gateway**, usare il cmdlet `New-AzureApplicationGateway` sostituendo i valori correnti con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="3a978-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="3a978-123">Si noti che la fatturazione per il gateway non viene applicata a partire da questo punto.</span><span class="sxs-lookup"><span data-stu-id="3a978-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="3a978-124">La fatturazione viene applicata a partire da un passaggio successivo, dopo l'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="3a978-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="3a978-125">**Per confermare** l'avvenuta creazione del gateway è possibile usare il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="3a978-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="3a978-126">Nell'esempio *Description*, *InstanceCount* e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="3a978-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="3a978-127">Il valore predefinito per *InstanceCount* è 2, con un valore massimo pari a 10.</span><span class="sxs-lookup"><span data-stu-id="3a978-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="3a978-128">Il valore predefinito per *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="3a978-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="3a978-129">Small e Large sono altri valori disponibili.</span><span class="sxs-lookup"><span data-stu-id="3a978-129">Small and Large are other available values.</span></span> <span data-ttu-id="3a978-130">*Indirizzo VIP* e *DnsName* vengono visualizzati come campi vuoti, perché il gateway non si è ancora avviato.</span><span class="sxs-lookup"><span data-stu-id="3a978-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="3a978-131">Questi valori vengono creati quando il gateway è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3a978-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="3a978-132">Configurare il gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-132">Configure the gateway</span></span>
<span data-ttu-id="3a978-133">La configurazione di un gateway applicazione è costituita da più valori.</span><span class="sxs-lookup"><span data-stu-id="3a978-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="3a978-134">È possibile collegare tra loro tali valori per creare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a978-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="3a978-135">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="3a978-135">The values are:</span></span>

* <span data-ttu-id="3a978-136">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="3a978-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="3a978-137">Gli indirizzi IP elencati devono appartenere alla subnet VNet o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="3a978-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="3a978-138">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="3a978-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="3a978-139">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="3a978-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="3a978-140">**Porta front-end:** questa porta è la porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3a978-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="3a978-141">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="3a978-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="3a978-142">**Listener:** il listener ha una porta front-end, un protocollo (Http o Https, con applicazione della distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="3a978-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="3a978-143">**Regola:** la regola associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="3a978-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="3a978-144">È attualmente supportata solo la regola *basic* .</span><span class="sxs-lookup"><span data-stu-id="3a978-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="3a978-145">La regola *basic* è una distribuzione del carico di tipo round robin.</span><span class="sxs-lookup"><span data-stu-id="3a978-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="3a978-146">È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a978-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="3a978-147">Per definire la configurazione mediante un file XML di configurazione, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3a978-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="3a978-148">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3a978-148">Note the following:</span></span>

* <span data-ttu-id="3a978-149">L'elemento *FrontendIPConfigurations* descrive i dettagli ILB pertinenti alla configurazione del gateway applicazione con un ILB.</span><span class="sxs-lookup"><span data-stu-id="3a978-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="3a978-150">L'elemento *Type* Frontend IP deve essere impostato su "Private".</span><span class="sxs-lookup"><span data-stu-id="3a978-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="3a978-151">*StaticIPAddress* deve essere impostato sull'IP interno desiderato su cui il gateway riceve il traffico.</span><span class="sxs-lookup"><span data-stu-id="3a978-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="3a978-152">Si noti che l'elemento *StaticIPAddress* è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="3a978-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="3a978-153">Se non viene impostato, viene scelto un IP interno disponibile dalla subnet distribuita.</span><span class="sxs-lookup"><span data-stu-id="3a978-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="3a978-154">Il valore dell'elemento *Name* specificato in *FrontendIPConfiguration* deve essere usato nell'elemento *FrontendIP* di HTTPListener per fare riferimento a FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="3a978-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="3a978-155">**Esempio di file XML di configurazione**</span><span class="sxs-lookup"><span data-stu-id="3a978-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="3a978-156">Definire la configurazione del gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-156">Set the gateway configuration</span></span>
<span data-ttu-id="3a978-157">Verrà quindi configurato il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3a978-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="3a978-158">È possibile usare il cmdlet `Set-AzureApplicationGatewayConfig` con un oggetto di configurazione o con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a978-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="3a978-159">Avviare il gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-159">Start the gateway</span></span>

<span data-ttu-id="3a978-160">Dopo la configurazione del gateway, usare il cmdlet `Start-AzureApplicationGateway` per avviarlo.</span><span class="sxs-lookup"><span data-stu-id="3a978-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="3a978-161">La fatturazione per un gateway applicazione verrà applicata a partire dall'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="3a978-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a978-162">La regola `Start-AzureApplicationGateway` potrebbe richiedere fino a 15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="3a978-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="3a978-163">Verificare lo stato del gateway</span><span class="sxs-lookup"><span data-stu-id="3a978-163">Verify the gateway status</span></span>

<span data-ttu-id="3a978-164">Usare il cmdlet `Get-AzureApplicationGateway` per verificare lo stato del gateway.</span><span class="sxs-lookup"><span data-stu-id="3a978-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="3a978-165">Se nel passaggio precedente l'operazione `Start-AzureApplicationGateway` è riuscita, lo stato sarà *In esecuzione* e i valori in Indirizzo VIP e DnsName saranno validi.</span><span class="sxs-lookup"><span data-stu-id="3a978-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="3a978-166">Questo esempio illustra il cmdlet nella prima riga seguito dall'output.</span><span class="sxs-lookup"><span data-stu-id="3a978-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="3a978-167">In questo esempio il gateway è in esecuzione ed è pronto per ricevere il traffico.</span><span class="sxs-lookup"><span data-stu-id="3a978-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="3a978-168">Il gateway applicazione è configurato per accettare il traffico nell'endpoint ILB configurato 10.0.0.10 di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="3a978-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="3a978-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a978-169">Next steps</span></span>
<span data-ttu-id="3a978-170">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="3a978-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="3a978-171">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="3a978-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="3a978-172">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="3a978-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

