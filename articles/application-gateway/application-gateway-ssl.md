---
title: aaaConfigure SSL offload classica - Gateway applicazione Azure - PowerShell | Documenti Microsoft
description: In questo articolo vengono fornite istruzioni toocreate eseguire l'offload usando un gateway applicazione con SSL hello modello di distribuzione classico di Azure.
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
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="a0b01-103">Configurare un gateway applicazione per l'offload SSL utilizzando il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0b01-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a0b01-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="a0b01-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a0b01-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="a0b01-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="a0b01-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="a0b01-107">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a0b01-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="a0b01-108">Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="a0b01-109">Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a0b01-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a0b01-110">Before you begin</span></span>

1. <span data-ttu-id="a0b01-111">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="a0b01-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="a0b01-112">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a0b01-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a0b01-113">Assicurarsi di avere una rete virtuale funzionante con una subnet valida.</span><span class="sxs-lookup"><span data-stu-id="a0b01-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="a0b01-114">Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="a0b01-115">gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a0b01-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="a0b01-116">deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a0b01-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="a0b01-117">tooconfigure SSL offload su un gateway applicazione, hello in ordine di hello elencati come segue:</span><span class="sxs-lookup"><span data-stu-id="a0b01-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="a0b01-118">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a0b01-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="a0b01-119">Caricare i certificati SSL</span><span class="sxs-lookup"><span data-stu-id="a0b01-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="a0b01-120">Configurare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="a0b01-121">Configurazione del gateway hello set</span><span class="sxs-lookup"><span data-stu-id="a0b01-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="a0b01-122">Avviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="a0b01-123">Verificare lo stato del gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="a0b01-124">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="a0b01-124">Create an application gateway</span></span>

<span data-ttu-id="a0b01-125">gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a0b01-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="a0b01-126">La fatturazione per il gateway hello non inizia a questo punto.</span><span class="sxs-lookup"><span data-stu-id="a0b01-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="a0b01-127">La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="a0b01-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="a0b01-128">toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0b01-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="a0b01-129">Nell'esempio hello *descrizione*, *InstanceCount*, e *GatewaySize* sono parametri facoltativi.</span><span class="sxs-lookup"><span data-stu-id="a0b01-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="a0b01-130">il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="a0b01-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a0b01-131">il valore predefinito per Hello *GatewaySize* è Medium.</span><span class="sxs-lookup"><span data-stu-id="a0b01-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a0b01-132">Small e Large sono altri valori disponibili.</span><span class="sxs-lookup"><span data-stu-id="a0b01-132">Small and Large are other available values.</span></span> <span data-ttu-id="a0b01-133">*Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="a0b01-134">Questi valori vengono creati una volta hello gateway si trova in stato di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="a0b01-135">Caricare i certificati SSL</span><span class="sxs-lookup"><span data-stu-id="a0b01-135">Upload SSL certificates</span></span>

<span data-ttu-id="a0b01-136">Utilizzare `Add-AzureApplicationGatewaySslCertificate` tooupload hello certificato del server *pfx* gateway applicazione toohello di formato.</span><span class="sxs-lookup"><span data-stu-id="a0b01-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="a0b01-137">nome del certificato Hello è un nome scelti dall'utente e deve essere univoco all'interno di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="a0b01-138">Questo certificato è tooby di cui si fa riferimento questo nome in tutte le operazioni di gestione di certificati su gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="a0b01-139">L'esempio seguente mostra i cmdlet di hello, sostituire i valori di hello nell'esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a0b01-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="a0b01-140">Successivamente, convalidare il caricamento di certificati hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="a0b01-141">Hello utilizzare `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0b01-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="a0b01-142">In questo esempio viene illustrato il cmdlet hello hello della prima riga, seguito dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

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
> <span data-ttu-id="a0b01-143">password del certificato Hello è toobe tra 4 too12 caratteri, lettere o numeri.</span><span class="sxs-lookup"><span data-stu-id="a0b01-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="a0b01-144">Non sono ammessi caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="a0b01-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="a0b01-145">Configurare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-145">Configure hello gateway</span></span>

<span data-ttu-id="a0b01-146">La configurazione di un gateway applicazione è costituita da più valori.</span><span class="sxs-lookup"><span data-stu-id="a0b01-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="a0b01-147">possono essere associati i valori Hello configurazione hello tooconstruct insieme.</span><span class="sxs-lookup"><span data-stu-id="a0b01-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="a0b01-148">i valori Hello sono:</span><span class="sxs-lookup"><span data-stu-id="a0b01-148">hello values are:</span></span>

* <span data-ttu-id="a0b01-149">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="a0b01-150">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a0b01-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a0b01-151">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="a0b01-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a0b01-152">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="a0b01-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="a0b01-153">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="a0b01-154">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="a0b01-155">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="a0b01-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a0b01-156">**Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="a0b01-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="a0b01-157">Attualmente, solo hello *base* regola supportata.</span><span class="sxs-lookup"><span data-stu-id="a0b01-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="a0b01-158">Hello *base* regola è una distribuzione del carico round robin.</span><span class="sxs-lookup"><span data-stu-id="a0b01-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="a0b01-159">**Note aggiuntive sulla configurazione**</span><span class="sxs-lookup"><span data-stu-id="a0b01-159">**Additional configuration notes**</span></span>

<span data-ttu-id="a0b01-160">Per la configurazione di certificati SSL, hello protocollo **HttpListener** deve modificare troppo*Https* (maiuscole / minuscole).</span><span class="sxs-lookup"><span data-stu-id="a0b01-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="a0b01-161">Hello **SslCert** elemento viene aggiunto troppo**HttpListener** con hello impostato toohello stesso nome utilizzato per il caricamento di hello della precedente sezione relativa ai certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="a0b01-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="a0b01-162">porta front-end di Hello deve essere aggiornato too443.</span><span class="sxs-lookup"><span data-stu-id="a0b01-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="a0b01-163">**affinità basato su cookie tooenable**: un gateway applicazione può essere configurato tooensure che una richiesta da una sessione client è sempre toohello diretto stessa macchina virtuale nella farm web hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="a0b01-164">Questo scenario viene eseguito dall'inserimento di un cookie di sessione che consenta il traffico di toodirect di hello gateway in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="a0b01-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="a0b01-165">impostata l'affinità basato su cookie tooenable, **CookieBasedAffinity** troppo*abilitato* in hello **BackendHttpSettings** elemento.</span><span class="sxs-lookup"><span data-stu-id="a0b01-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="a0b01-166">È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a0b01-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="a0b01-167">Utilizzare la configurazione utilizzando una file XML di configurazione tooconstruct hello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="a0b01-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="a0b01-168">**Esempio di file XML di configurazione**</span><span class="sxs-lookup"><span data-stu-id="a0b01-168">**Configuration XML sample**</span></span>

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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="a0b01-169">Configurazione del gateway hello set</span><span class="sxs-lookup"><span data-stu-id="a0b01-169">Set hello gateway configuration</span></span>

<span data-ttu-id="a0b01-170">È quindi possibile impostare gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="a0b01-171">È possibile utilizzare hello `Set-AzureApplicationGatewayConfig` cmdlet con un oggetto di configurazione o con un file XML di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a0b01-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="a0b01-172">Avviare il gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-172">Start hello gateway</span></span>

<span data-ttu-id="a0b01-173">Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0b01-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="a0b01-174">La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="a0b01-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b01-175">Hello `Start-AzureApplicationGateway` cmdlet può richiedere toofinish too15-20 minuti.</span><span class="sxs-lookup"><span data-stu-id="a0b01-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="a0b01-176">Verificare lo stato del gateway hello</span><span class="sxs-lookup"><span data-stu-id="a0b01-176">Verify hello gateway status</span></span>

<span data-ttu-id="a0b01-177">Hello utilizzare `Get-AzureApplicationGateway` cmdlet toocheck hello stato gateway hello.</span><span class="sxs-lookup"><span data-stu-id="a0b01-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="a0b01-178">Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello *stato* deve essere in esecuzione, e *gli IP virtuali* e *DnsName* dovrebbero avere voci valide.</span><span class="sxs-lookup"><span data-stu-id="a0b01-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="a0b01-179">Questo esempio viene illustrato un gateway di applicazione, in esecuzione, ed è pronto tootake traffico.</span><span class="sxs-lookup"><span data-stu-id="a0b01-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a0b01-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0b01-180">Next steps</span></span>

<span data-ttu-id="a0b01-181">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="a0b01-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a0b01-182">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="a0b01-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a0b01-183">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="a0b01-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

