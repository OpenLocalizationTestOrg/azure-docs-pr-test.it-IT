---
title: Configurare l'offload SSL - Gateway applicazione di Azure - PowerShell versione classica | Documentazione Microsoft
description: Questo articolo fornisce istruzioni per la creazione di un gateway applicazione con offload SSL tramite il modello di distribuzione classica di Azure.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="d2799-103">Configurare un gateway applicazione per l'offload SSL tramite il modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="d2799-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2799-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d2799-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="d2799-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2799-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="d2799-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="d2799-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="d2799-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d2799-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="d2799-108">Il gateway applicazione di Azure può essere configurato per terminare la sessione Secure Sockets Layer (SSL) nel gateway ed evitare costose attività di decrittografia SSL nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="d2799-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="d2799-109">L'offload SSL semplifica anche la configurazione e la gestione del server front-end dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d2799-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d2799-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d2799-110">Before you begin</span></span>

1. <span data-ttu-id="d2799-111">Installare la versione più recente dei cmdlet di Azure PowerShell usando l'Installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="d2799-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="d2799-112">È possibile scaricare e installare la versione più recente dalla sezione **Windows PowerShell** della [Pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d2799-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d2799-113">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="d2799-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="d2799-114">Assicurarsi che nessuna macchina virtuale o distribuzione cloud stia usando la subnet.</span><span class="sxs-lookup"><span data-stu-id="d2799-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="d2799-115">Il gateway applicazione deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d2799-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d2799-116">È necessario che i server configurati per l'uso del gateway applicazione esistano oppure che i relativi endpoint siano stati creati nella rete virtuale o con un indirizzo IP/VIP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="d2799-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="d2799-117">Per configurare l'offload SSL in un gateway applicazione, eseguire i passaggi seguenti nell'ordine elencato.</span><span class="sxs-lookup"><span data-stu-id="d2799-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="d2799-118">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="d2799-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="d2799-119">Caricare i certificati SSL</span><span class="sxs-lookup"><span data-stu-id="d2799-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="d2799-120">Configurare il gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="d2799-121">Definire la configurazione del gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="d2799-122">Avviare il gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="d2799-123">Verificare lo stato del gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="d2799-124">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="d2799-124">Create an application gateway</span></span>

<span data-ttu-id="d2799-125">Per creare il gateway, usare il cmdlet `New-AzureApplicationGateway`, sostituendo i valori esistenti con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="d2799-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="d2799-126">La fatturazione per il gateway non viene applicata a partire da questo punto.</span><span class="sxs-lookup"><span data-stu-id="d2799-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="d2799-127">La fatturazione viene applicata a partire da un passaggio successivo, dopo l'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="d2799-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="d2799-128">Per convalidare la creazione del gateway, è possibile usare il cmdlet `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="d2799-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="d2799-129">In questo esempio *Description*, *InstanceCount* e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="d2799-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="d2799-130">Il valore predefinito per *InstanceCount* è 2, con un valore massimo pari a 10.</span><span class="sxs-lookup"><span data-stu-id="d2799-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d2799-131">Il valore predefinito per *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="d2799-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d2799-132">Small e Large sono altri valori disponibili.</span><span class="sxs-lookup"><span data-stu-id="d2799-132">Small and Large are other available values.</span></span> <span data-ttu-id="d2799-133">*VirtualIPs* e *DnsName* vengono visualizzati vuoti perché il gateway non è stato ancora avviato.</span><span class="sxs-lookup"><span data-stu-id="d2799-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="d2799-134">Questi valori vengono creati quando il gateway è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d2799-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="d2799-135">Caricare i certificati SSL</span><span class="sxs-lookup"><span data-stu-id="d2799-135">Upload SSL certificates</span></span>

<span data-ttu-id="d2799-136">Usare `Add-AzureApplicationGatewaySslCertificate` per caricare il certificato del server in formato *pfx* nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="d2799-137">Il nome del certificato è un nome scelto dall'utente e deve essere univoco all'interno del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="d2799-138">Il certificato viene identificato da questo nome in tutte le operazioni di gestione del certificato nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="d2799-139">L'esempio seguente illustra il cmdlet. Sostituire i valori dell'esempio con i propri.</span><span class="sxs-lookup"><span data-stu-id="d2799-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="d2799-140">Successivamente, convalidare il caricamento del certificato.</span><span class="sxs-lookup"><span data-stu-id="d2799-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="d2799-141">Utilizzare il cmdlet `Get-AzureApplicationGatewayCertificate` .</span><span class="sxs-lookup"><span data-stu-id="d2799-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="d2799-142">Questo esempio illustra il cmdlet nella prima riga seguito dall'output.</span><span class="sxs-lookup"><span data-stu-id="d2799-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="d2799-143">La password del certificato deve contenere da 4 a 12 caratteri, lettere o numeri.</span><span class="sxs-lookup"><span data-stu-id="d2799-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="d2799-144">Non sono ammessi caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="d2799-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="d2799-145">Configurare il gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-145">Configure the gateway</span></span>

<span data-ttu-id="d2799-146">La configurazione di un gateway applicazione è costituita da più valori.</span><span class="sxs-lookup"><span data-stu-id="d2799-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="d2799-147">È possibile collegare tra loro tali valori per creare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="d2799-148">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="d2799-148">The values are:</span></span>

* <span data-ttu-id="d2799-149">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="d2799-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="d2799-150">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="d2799-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d2799-151">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="d2799-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d2799-152">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="d2799-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="d2799-153">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="d2799-154">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="d2799-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="d2799-155">**Listener** : ha una porta front-end, un protocollo (Http o Https, con distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="d2799-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d2799-156">**Regola** : associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="d2799-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="d2799-157">È attualmente supportata solo la regola *basic* .</span><span class="sxs-lookup"><span data-stu-id="d2799-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="d2799-158">La regola *basic* è una distribuzione del carico di tipo round robin.</span><span class="sxs-lookup"><span data-stu-id="d2799-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="d2799-159">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="d2799-159">**Additional configuration notes**</span></span>

<span data-ttu-id="d2799-160">Per la configurazione dei certificati SSL, il protocollo in **HttpListener** deve essere sostituito con *Https* (distinzione tra maiuscole e minuscole).</span><span class="sxs-lookup"><span data-stu-id="d2799-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="d2799-161">L'elemento **SslCert** viene aggiunto a **HttpListener** con il valore impostato sullo stesso nome usato nella sezione precedente sul caricamento dei certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="d2799-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="d2799-162">La porta front-end deve essere impostata su 443.</span><span class="sxs-lookup"><span data-stu-id="d2799-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="d2799-163">**Per abilitare l'affinità basata sui cookie**: è possibile configurare un gateway applicazione per fare in modo che una richiesta proveniente da una sessione client sia sempre diretta alla stessa macchina virtuale nella Web farm.</span><span class="sxs-lookup"><span data-stu-id="d2799-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="d2799-164">Questo scenario viene realizzato aggiungendo un cookie di sessione che consente al gateway di indirizzare il traffico in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="d2799-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="d2799-165">Per abilitare l'affinità basata sui cookie, impostare **CookieBasedAffinity** su *Enabled* nell'elemento **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="d2799-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="d2799-166">È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="d2799-167">Per creare la configurazione con un file XML di configurazione, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d2799-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="d2799-168">**Esempio di file XML di configurazione**</span><span class="sxs-lookup"><span data-stu-id="d2799-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="d2799-169">Definire la configurazione del gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-169">Set the gateway configuration</span></span>

<span data-ttu-id="d2799-170">Viene quindi impostato il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-170">Next, you set the application gateway.</span></span> <span data-ttu-id="d2799-171">È possibile usare il cmdlet `Set-AzureApplicationGatewayConfig` con un oggetto di configurazione o con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2799-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="d2799-172">Avviare il gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-172">Start the gateway</span></span>

<span data-ttu-id="d2799-173">Dopo la configurazione del gateway, usare il cmdlet `Start-AzureApplicationGateway` per avviarlo.</span><span class="sxs-lookup"><span data-stu-id="d2799-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="d2799-174">La fatturazione per un gateway applicazione verrà applicata a partire dall'avvio corretto del gateway.</span><span class="sxs-lookup"><span data-stu-id="d2799-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="d2799-175">Il completamento del cmdlet `Start-AzureApplicationGateway` potrebbe richiedere fino a 15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="d2799-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="d2799-176">Verificare lo stato del gateway</span><span class="sxs-lookup"><span data-stu-id="d2799-176">Verify the gateway status</span></span>

<span data-ttu-id="d2799-177">Usare il cmdlet `Get-AzureApplicationGateway` per verificare lo stato del gateway.</span><span class="sxs-lookup"><span data-stu-id="d2799-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="d2799-178">Se nel passaggio precedente l'operazione `Start-AzureApplicationGateway` è riuscita, lo stato (*State*) risulterà in esecuzione (Running) e le voci *VirtualIPs* e *DnsName* saranno valide.</span><span class="sxs-lookup"><span data-stu-id="d2799-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="d2799-179">Questo esempio illustra un gateway applicazione attivo, in esecuzione e pronto per accettare il traffico</span><span class="sxs-lookup"><span data-stu-id="d2799-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="d2799-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2799-180">Next steps</span></span>

<span data-ttu-id="d2799-181">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="d2799-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="d2799-182">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="d2799-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="d2799-183">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="d2799-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

