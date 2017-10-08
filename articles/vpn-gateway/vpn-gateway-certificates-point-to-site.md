---
title: 'Generare ed esportare certificati autofirmati per connessioni da punto a sito: PowerShell: Azure | Microsoft Docs'
description: In questo articolo contiene passaggi toocreate un certificato radice autofirmato, esportare la chiave pubblica hello e generare i certificati client tramite PowerShell in Windows 10.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="2e56e-103">Generare ed esportare i certificati per le connessioni da punto a sito usando PowerShell su Windows 10</span><span class="sxs-lookup"><span data-stu-id="2e56e-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="2e56e-104">Le connessioni Point-to-Site, utilizzano tooauthenticate certificati.</span><span class="sxs-lookup"><span data-stu-id="2e56e-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="2e56e-105">In questo articolo viene illustrato come certificato radice toocreate a autofirmato e generare i certificati client tramite PowerShell in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2e56e-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="2e56e-106">Se si sta cercando i passaggi di configurazione da punto a sito, ad esempio come elenco di certificati radice tooupload, selezionare uno degli articoli hello ' Configure Point-to-Site' di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e56e-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="2e56e-107">[Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)</span><span class="sxs-lookup"><span data-stu-id="2e56e-107">[Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md)</span></span>
> * [<span data-ttu-id="2e56e-108">Creare certificati autofirmati - MakeCert</span><span class="sxs-lookup"><span data-stu-id="2e56e-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * <span data-ttu-id="2e56e-109">[Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="2e56e-109">[Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)</span></span>
> * [<span data-ttu-id="2e56e-110">Configurazione da punto a sito - Gestione risorse - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e56e-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * <span data-ttu-id="2e56e-111">[Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="2e56e-111">[Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)</span></span>
> 
> 


<span data-ttu-id="2e56e-112">In questo articolo in un computer che eseguono Windows 10, è necessario eseguire passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="2e56e-113">i cmdlet di PowerShell Hello utilizzare certificati toogenerate fanno parte del sistema operativo Windows 10 hello e non funzionano nelle altre versioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="2e56e-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="2e56e-114">computer Windows 10 Hello è solo necessario toogenerate hello certificati.</span><span class="sxs-lookup"><span data-stu-id="2e56e-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="2e56e-115">Una volta generati certificati hello, è possibile caricarli o installarli in qualsiasi sistema operativo client supportato.</span><span class="sxs-lookup"><span data-stu-id="2e56e-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="2e56e-116">Se non si dispone di computer Windows 10 tooa di accesso, è possibile utilizzare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificati.</span><span class="sxs-lookup"><span data-stu-id="2e56e-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="2e56e-117">Hello certificati generati usando dei metodi possono essere installati su qualsiasi [supportati](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo client.</span><span class="sxs-lookup"><span data-stu-id="2e56e-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="2e56e-118"><a name="rootcert"></a>Creare un certificato radice autofirmato</span><span class="sxs-lookup"><span data-stu-id="2e56e-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="2e56e-119">Utilizzare toocreate di cmdlet New-SelfSignedCertificate hello un certificato radice autofirmato.</span><span class="sxs-lookup"><span data-stu-id="2e56e-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="2e56e-120">Per altre informazioni sui parametri, vedere [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="2e56e-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="2e56e-121">Da un computer che esegue Windows 10 aprire una console di Windows PowerShell con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="2e56e-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="2e56e-122">Utilizzare hello certificato radice autofirmato hello toocreate di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="2e56e-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="2e56e-123">Hello seguente viene creato un certificato radice autofirmato denominato 'P2SRootCert' che viene installato automaticamente in 'Corrente\Personale\Certificati certificati'.</span><span class="sxs-lookup"><span data-stu-id="2e56e-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="2e56e-124">È possibile visualizzare il certificato di hello aprendo *certmgr.msc*, o *gestire i certificati utente*.</span><span class="sxs-lookup"><span data-stu-id="2e56e-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="2e56e-125"><a name="cer"></a>Esportare la chiave pubblica hello (con estensione cer)</span><span class="sxs-lookup"><span data-stu-id="2e56e-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="2e56e-126">file exported.cer Hello deve essere caricato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2e56e-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="2e56e-127">Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="2e56e-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="2e56e-128">un certificato radice attendibile, tooadd [in questa sezione](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="2e56e-129">Esporta certificato radice autofirmato hello e toostore chiave pubblica è (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="2e56e-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="2e56e-130">È opportuno tooexport hello certificato radice autofirmato e archiviarlo in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="2e56e-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="2e56e-131">Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer.</span><span class="sxs-lookup"><span data-stu-id="2e56e-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="2e56e-132">hello tooexport autofirmato certificato radice come una con estensione pfx, un certificato radice hello selezionare e usare hello stessi passaggi, come descritto in [esportare un certificato client](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="2e56e-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="2e56e-133"><a name="clientcert"></a>Generazione di un certificato client</span><span class="sxs-lookup"><span data-stu-id="2e56e-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="2e56e-134">Ogni computer client che si connette tooa virtuale usando Point-to-Site deve avere installato un certificato client.</span><span class="sxs-lookup"><span data-stu-id="2e56e-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="2e56e-135">Genera un certificato client dal certificato radice autofirmato hello e quindi esportare e installare il certificato client hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="2e56e-136">Se non è stato installato il certificato client hello, l'autenticazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2e56e-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="2e56e-137">Hello passaggi seguenti consentono di eseguire la generazione di un certificato client da un certificato radice autofirmato.</span><span class="sxs-lookup"><span data-stu-id="2e56e-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="2e56e-138">È possibile generare più certificati client da hello stesso certificato radice.</span><span class="sxs-lookup"><span data-stu-id="2e56e-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="2e56e-139">Quando si generano i certificati client con passaggi hello riportati di seguito, certificato hello del client viene installato automaticamente nel computer di hello utilizzato certificato hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="2e56e-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="2e56e-140">Se si desidera tooinstall un certificato client in un altro computer client, è possibile esportare il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="2e56e-141">esempi di Hello utilizzano toogenerate di cmdlet New-SelfSignedCertificate hello un certificato client che scade dopo un anno.</span><span class="sxs-lookup"><span data-stu-id="2e56e-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="2e56e-142">Per informazioni aggiuntive sui parametri, ad esempio l'impostazione di un valore di scadenza diversa per il certificato client hello, vedere [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="2e56e-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="2e56e-143">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="2e56e-143">Example 1</span></span>

<span data-ttu-id="2e56e-144">Questo esempio Usa hello dichiarata la variabile '$cert' dalla sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="2e56e-145">Se si chiude la console di PowerShell hello dopo la creazione di hello certificato radice autofirmato o sta creando i certificati client aggiuntive in una nuova sessione di console di PowerShell, utilizzare i passaggi di hello in [esempio 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="2e56e-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="2e56e-146">Modificare ed eseguire toogenerate esempio hello un certificato client.</span><span class="sxs-lookup"><span data-stu-id="2e56e-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="2e56e-147">Se si esegue l'esempio seguente senza modificarla hello, il risultato di hello è un certificato client denominato 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="2e56e-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="2e56e-148">Se si desidera certificato figlio hello tooname con un altro, modificare il valore CN hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="2e56e-149">Non modificare hello TextExtension quando si esegue questo esempio.</span><span class="sxs-lookup"><span data-stu-id="2e56e-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="2e56e-150">certificato client Hello generato viene installato automaticamente in 'Certificati - corrente\Personale\Certificati' nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2e56e-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="2e56e-151"><a name="ex2"></a>Esempio 2</span><span class="sxs-lookup"><span data-stu-id="2e56e-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="2e56e-152">Se si sta creando i certificati client aggiuntive o sono non utilizza hello stessa sessione di PowerShell utilizzato toocreate il certificato radice autofirmato, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e56e-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="2e56e-153">Identificare certificato radice autofirmato hello installata nel computer di hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="2e56e-154">Questo cmdlet restituisce un elenco dei certificati installati nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2e56e-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="2e56e-155">Individuare il nome soggetto hello da hello restituito l'elenco, quindi l'identificazione personale hello copia che si trova il testo successivo tooa tooit file.</span><span class="sxs-lookup"><span data-stu-id="2e56e-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="2e56e-156">Nell'esempio seguente di hello, esistono due certificati.</span><span class="sxs-lookup"><span data-stu-id="2e56e-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="2e56e-157">nome CN Hello è hello del certificato radice autofirmato hello da cui si desidera toogenerate un certificato figlio.</span><span class="sxs-lookup"><span data-stu-id="2e56e-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="2e56e-158">In questo caso "P2SRootCert".</span><span class="sxs-lookup"><span data-stu-id="2e56e-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="2e56e-159">Dichiarare una variabile per il certificato radice hello con identificazione personale hello dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="2e56e-160">Sostituire l'identificazione personale con identificazione personale hello del certificato radice hello da cui si desidera toogenerate un certificato figlio.</span><span class="sxs-lookup"><span data-stu-id="2e56e-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="2e56e-161">Ad esempio, con identificazione personale hello per P2SRootCert nel passaggio precedente hello, variabile hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2e56e-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="2e56e-162">Modificare ed eseguire toogenerate esempio hello un certificato client.</span><span class="sxs-lookup"><span data-stu-id="2e56e-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="2e56e-163">Se si esegue l'esempio seguente senza modificarla hello, il risultato di hello è un certificato client denominato 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="2e56e-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="2e56e-164">Se si desidera certificato figlio hello tooname con un altro, modificare il valore CN hello.</span><span class="sxs-lookup"><span data-stu-id="2e56e-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="2e56e-165">Non modificare hello TextExtension quando si esegue questo esempio.</span><span class="sxs-lookup"><span data-stu-id="2e56e-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="2e56e-166">certificato client Hello generato viene installato automaticamente in 'Certificati - corrente\Personale\Certificati' nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2e56e-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="2e56e-167"><a name="clientexport"></a>Esportare un certificato client</span><span class="sxs-lookup"><span data-stu-id="2e56e-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="2e56e-168"><a name="install"></a>Installare un certificato client esportato</span><span class="sxs-lookup"><span data-stu-id="2e56e-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2e56e-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e56e-169">Next steps</span></span>

<span data-ttu-id="2e56e-170">Continuare con la configurazione da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="2e56e-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="2e56e-171">Per **Gestione risorse** passaggi di distribuzione del modello, vedere [configurare un tooa connessione Point-to-Site rete virtuale](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e56e-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="2e56e-172">Per **classico** passaggi di distribuzione del modello, vedere [configurare tooa di connessione tra reti virtuali (classico) un VPN Point-to-Site](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e56e-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
