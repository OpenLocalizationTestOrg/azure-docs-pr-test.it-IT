---
title: 'Generare ed esportare certificati autofirmati per connessioni da punto a sito: PowerShell: Azure | Microsoft Docs'
description: Questo articolo contiene i passaggi per creare un certificato radice autofirmato, esportare la chiave pubblica e generare certificati client con PowerShell in Windows 10.
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
ms.openlocfilehash: f96b9b212b9322d0677e49ff95184d0feccca2df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="b5751-103">Generare ed esportare i certificati per le connessioni da punto a sito usando PowerShell su Windows 10</span><span class="sxs-lookup"><span data-stu-id="b5751-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="b5751-104">Le connessioni da punto a sito usano certificati per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b5751-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="b5751-105">Questo articolo illustra come creare un certificato radice autofirmato e generare i certificati client usando PowerShell su Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b5751-105">This article shows you how to create a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="b5751-106">Per le procedure di configurazione da punto a sito, ad esempio come caricare i certificati radice, selezionare uno degli articoli "Configurare da punto a sito" dell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="b5751-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="b5751-107">[Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md) (Creare certificati autofirmati - PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b5751-107">[Create self-signed certificates - PowerShell](vpn-gateway-certificates-point-to-site.md)</span></span>
> * [<span data-ttu-id="b5751-108">Creare certificati autofirmati - MakeCert</span><span class="sxs-lookup"><span data-stu-id="b5751-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * <span data-ttu-id="b5751-109">[Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md) (Eseguire una configurazione da punto a sito - Resource Manager - Portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="b5751-109">[Configure Point-to-Site - Resource Manager - Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)</span></span>
> * [<span data-ttu-id="b5751-110">Configurazione da punto a sito - Gestione risorse - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5751-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * <span data-ttu-id="b5751-111">[Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md) (Eseguire una configurazione da punto a sito - Classica - Portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="b5751-111">[Configure Point-to-Site - Classic - Azure portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)</span></span>
> 
> 


<span data-ttu-id="b5751-112">È necessario eseguire i passaggi descritti in questo articolo in un computer che esegue Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b5751-112">You must perform the steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="b5751-113">I cmdlet di PowerShell usati per generare i certificati fanno parte del sistema operativo Windows 10 e non funzionano in altre versioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="b5751-113">The PowerShell cmdlets that you use to generate certificates are part of the Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="b5751-114">Il computer Windows 10 deve solo generare i certificati.</span><span class="sxs-lookup"><span data-stu-id="b5751-114">The Windows 10 computer is only needed to generate the certificates.</span></span> <span data-ttu-id="b5751-115">Dopo aver generato i certificati, è possibile caricarli o installarli in qualsiasi sistema operativo client supportato.</span><span class="sxs-lookup"><span data-stu-id="b5751-115">Once the certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="b5751-116">Se non si ha accesso a un computer con Windows 10, è possibile usare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) per generare i certificati.</span><span class="sxs-lookup"><span data-stu-id="b5751-116">If you do not have access to a Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) to generate certificates.</span></span> <span data-ttu-id="b5751-117">I certificati generati con uno dei due metodi possono essere installati in qualsiasi sistema operativo client [supportato](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq).</span><span class="sxs-lookup"><span data-stu-id="b5751-117">The certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="b5751-118"><a name="rootcert"></a>Creare un certificato radice autofirmato</span><span class="sxs-lookup"><span data-stu-id="b5751-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="b5751-119">Usare il cmdlet New-SelfSignedCertificate per creare un certificato radice autofirmato.</span><span class="sxs-lookup"><span data-stu-id="b5751-119">Use the New-SelfSignedCertificate cmdlet to create a self-signed root certificate.</span></span> <span data-ttu-id="b5751-120">Per altre informazioni sui parametri, vedere [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="b5751-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="b5751-121">Da un computer che esegue Windows 10 aprire una console di Windows PowerShell con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="b5751-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="b5751-122">Usare l'esempio seguente per creare il certificato radice autofirmato.</span><span class="sxs-lookup"><span data-stu-id="b5751-122">Use the following example to create the self-signed root certificate.</span></span> <span data-ttu-id="b5751-123">L'esempio seguente crea un certificato radice autofirmato denominato "P2SRootCert" che viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati".</span><span class="sxs-lookup"><span data-stu-id="b5751-123">The following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="b5751-124">È possibile visualizzare il certificato aprendo *certmgr.msc* o *Gestire i certificati utente*.</span><span class="sxs-lookup"><span data-stu-id="b5751-124">You can view the certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="b5751-125"><a name="cer"></a>Esportare la chiave pubblica (.cer)</span><span class="sxs-lookup"><span data-stu-id="b5751-125"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="b5751-126">Il file exported.cer deve essere caricato in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5751-126">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="b5751-127">Per istruzioni, vedere [Configurare una connessione da punto a sito](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="b5751-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="b5751-128">Per aggiungere un certificato radice attendibile aggiuntivo, vedere [questa sezione](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="b5751-128">To add an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of the article.</span></span>

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a><span data-ttu-id="b5751-129">Esportare il certificato radice autofirmato e la chiave pubblica per archiviarli (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b5751-129">Export the self-signed root certificate and public key to store it (optional)</span></span>

<span data-ttu-id="b5751-130">Si consiglia di esportare il certificato radice autofirmato e archiviarlo in un percorso sicuro.</span><span class="sxs-lookup"><span data-stu-id="b5751-130">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="b5751-131">Se necessario, in seguito è possibile installarlo su un altro computer e generare altri certificati client oppure esportare un altro file.cer.</span><span class="sxs-lookup"><span data-stu-id="b5751-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="b5751-132">Per esportare il certificato radice autofirmato come file .pfx, selezionare il certificato radice ed eseguire la stessa procedura descritta in [Esportazione di un certificato client](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="b5751-132">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="b5751-133"><a name="clientcert"></a>Generazione di un certificato client</span><span class="sxs-lookup"><span data-stu-id="b5751-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="b5751-134">Ogni computer client che si connette a una rete virtuale usando la soluzione Da punto a sito deve avere un certificato client installato.</span><span class="sxs-lookup"><span data-stu-id="b5751-134">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="b5751-135">È possibile generare un certificato client da un certificato radice autofirmato, quindi esportare e installare il certificato client.</span><span class="sxs-lookup"><span data-stu-id="b5751-135">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="b5751-136">Se il certificato client non è installato, l'autenticazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="b5751-136">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="b5751-137">I passaggi seguenti illustrano come generare un certificato client da un certificato radice autofirmato.</span><span class="sxs-lookup"><span data-stu-id="b5751-137">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="b5751-138">È possibile generare più certificati client dallo stesso certificato radice.</span><span class="sxs-lookup"><span data-stu-id="b5751-138">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="b5751-139">Quando si generano certificati client con la procedura seguente, il certificato client viene installato automaticamente nel computer che è stato usato per generare il certificato.</span><span class="sxs-lookup"><span data-stu-id="b5751-139">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="b5751-140">Se si vuole installare un certificato client in un altro computer client, è possibile esportare il certificato.</span><span class="sxs-lookup"><span data-stu-id="b5751-140">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>

<span data-ttu-id="b5751-141">Gli esempi usano il cmdlet New-SelfSignedCertificate per generare un certificato client con scadenza in un anno.</span><span class="sxs-lookup"><span data-stu-id="b5751-141">The examples use the New-SelfSignedCertificate cmdlet to generate a client certificate that expires in one year.</span></span> <span data-ttu-id="b5751-142">Per informazioni aggiuntive sui parametri, ad esempio l'impostazione di un valore di scadenza diverso per i certificati client, vedere [New SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="b5751-142">For additional parameter information, such as setting a different expiration value for the client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="b5751-143">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="b5751-143">Example 1</span></span>

<span data-ttu-id="b5751-144">Questo esempio usa la variabile dichiarata "$cert" della sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="b5751-144">This example uses the declared '$cert' variable from the previous section.</span></span> <span data-ttu-id="b5751-145">Se è stata chiusa la console di PowerShell dopo aver creato il certificato radice autofirmato o si stanno creando i certificati client aggiuntivi in una nuova sessione della console di PowerShell, attenersi alla procedura nell'[esempio 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="b5751-145">If you closed the PowerShell console after creating the self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use the steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="b5751-146">Modificare ed eseguire l'esempio per generare un certificato client.</span><span class="sxs-lookup"><span data-stu-id="b5751-146">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="b5751-147">Se si esegue l'esempio seguente senza modificarlo, il risultato è un certificato client denominato "P2SChildCert".</span><span class="sxs-lookup"><span data-stu-id="b5751-147">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="b5751-148">Se si desidera assegnare un nome diverso al certificato figlio, modificare il valore CN.</span><span class="sxs-lookup"><span data-stu-id="b5751-148">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="b5751-149">Non modificare il TextExtension quando si esegue questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b5751-149">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="b5751-150">Il certificato client generato viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati" nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b5751-150">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="b5751-151"><a name="ex2"></a>Esempio 2</span><span class="sxs-lookup"><span data-stu-id="b5751-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="b5751-152">Se si creano certificati client aggiuntivi o non si usa la stessa sessione di PowerShell utilizzata per creare il certificato radice autofirmato, usare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5751-152">If you are creating additional client certificates, or are not using the same PowerShell session that you used to create your self-signed root certificate, use the following steps:</span></span>

1. <span data-ttu-id="b5751-153">Identificare il certificato radice autofirmato che viene installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="b5751-153">Identify the self-signed root certificate that is installed on the computer.</span></span> <span data-ttu-id="b5751-154">Questo cmdlet restituisce un elenco dei certificati installati nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b5751-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="b5751-155">Individuare il nome dell'oggetto nell'elenco restituito e quindi copiare in un file di testo l'identificazione personale che si trova accanto a esso.</span><span class="sxs-lookup"><span data-stu-id="b5751-155">Locate the subject name from the returned list, then copy the thumbprint that is located next to it to a text file.</span></span> <span data-ttu-id="b5751-156">Nell'esempio seguente ci sono due certificati.</span><span class="sxs-lookup"><span data-stu-id="b5751-156">In the following example, there are two certificates.</span></span> <span data-ttu-id="b5751-157">Il nome CN è il nome del certificato radice autofirmato da cui si desidera generare un certificato figlio.</span><span class="sxs-lookup"><span data-stu-id="b5751-157">The CN name is the name of the self-signed root certificate from which you want to generate a child certificate.</span></span> <span data-ttu-id="b5751-158">In questo caso "P2SRootCert".</span><span class="sxs-lookup"><span data-stu-id="b5751-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="b5751-159">Dichiarare una variabile per il certificato radice usando l'identificazione personale del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b5751-159">Declare a variable for the root certificate using the thumbprint from the previous step.</span></span> <span data-ttu-id="b5751-160">Sostituire THUMBPRINT con l'identificazione personale del certificato radice autofirmato da cui si desidera generare un certificato figlio.</span><span class="sxs-lookup"><span data-stu-id="b5751-160">Replace THUMBPRINT with the thumbprint of the root certificate from which you want to generate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="b5751-161">Ad esempio, usando l'identificazione personale per P2SRootCert nel passaggio precedente, la variabile è simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b5751-161">For example, using the thumbprint for P2SRootCert in the previous step, the variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="b5751-162">Modificare ed eseguire l'esempio per generare un certificato client.</span><span class="sxs-lookup"><span data-stu-id="b5751-162">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="b5751-163">Se si esegue l'esempio seguente senza modificarlo, il risultato è un certificato client denominato "P2SChildCert".</span><span class="sxs-lookup"><span data-stu-id="b5751-163">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="b5751-164">Se si desidera assegnare un nome diverso al certificato figlio, modificare il valore CN.</span><span class="sxs-lookup"><span data-stu-id="b5751-164">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="b5751-165">Non modificare il TextExtension quando si esegue questo esempio.</span><span class="sxs-lookup"><span data-stu-id="b5751-165">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="b5751-166">Il certificato client generato viene installato automaticamente in "Certificati-Utente corrente\Personale\Certificati" nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b5751-166">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="b5751-167"><a name="clientexport"></a>Esportare un certificato client</span><span class="sxs-lookup"><span data-stu-id="b5751-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="b5751-168"><a name="install"></a>Installare un certificato client esportato</span><span class="sxs-lookup"><span data-stu-id="b5751-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b5751-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5751-169">Next steps</span></span>

<span data-ttu-id="b5751-170">Continuare con la configurazione da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="b5751-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="b5751-171">Per i passaggi del modello di distribuzione di **Resource Manager**, vedere l'articolo relativo a come [configurare una connessione da punto a sito a una rete VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b5751-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="b5751-172">Per i passaggi del modello di distribuzione **classico**, vedere [Configurare una connessione VPN da punto a sito a una rete virtuale (classico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b5751-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>