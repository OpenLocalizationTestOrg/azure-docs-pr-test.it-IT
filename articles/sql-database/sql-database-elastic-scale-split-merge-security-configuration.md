---
title: configurazione della sicurezza di tipo merge aaaSplit | Documenti Microsoft
description: Impostazione dei certificati 409 per la crittografia
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="76a88-103">Configurazione della sicurezza del servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="76a88-103">Split-merge security configuration</span></span>
<span data-ttu-id="76a88-104">servizio di suddivisione/unione hello toouse, è necessario configurare correttamente sicurezza.</span><span class="sxs-lookup"><span data-stu-id="76a88-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="76a88-105">servizio Hello fa parte della funzionalità di scalabilità elastica hello di Database SQL di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="76a88-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="76a88-106">Per altre informazioni, vedere [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="76a88-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="76a88-107">Configurazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-107">Configuring certificates</span></span>
<span data-ttu-id="76a88-108">I certificati vengono configurati in due modi.</span><span class="sxs-lookup"><span data-stu-id="76a88-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="76a88-109">hello tooConfigure certificato SSL</span><span class="sxs-lookup"><span data-stu-id="76a88-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="76a88-110">tooConfigure i certificati Client</span><span class="sxs-lookup"><span data-stu-id="76a88-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="76a88-111">certificati tooobtain</span><span class="sxs-lookup"><span data-stu-id="76a88-111">tooobtain certificates</span></span>
<span data-ttu-id="76a88-112">Certificati possono essere ottenuti da una autorità di certificazione (CA) pubblica o da hello [servizio certificato Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="76a88-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="76a88-113">Questi sono hello preferito metodi tooobtain certificati.</span><span class="sxs-lookup"><span data-stu-id="76a88-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="76a88-114">Se tali opzioni non sono disponibili, è possibile generare **certificati autofirmati**.</span><span class="sxs-lookup"><span data-stu-id="76a88-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="76a88-115">Certificati toogenerate strumenti</span><span class="sxs-lookup"><span data-stu-id="76a88-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="76a88-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="76a88-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="76a88-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="76a88-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="76a88-118">strumenti di hello toorun</span><span class="sxs-lookup"><span data-stu-id="76a88-118">toorun hello tools</span></span>
* <span data-ttu-id="76a88-119">Da un Prompt dei comandi per gli sviluppatori per Visual Studio, vedere l'articolo relativo al [prompt dei comandi di Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="76a88-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="76a88-120">Se installato, passare a:</span><span class="sxs-lookup"><span data-stu-id="76a88-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="76a88-121">Ottenere hello WDK da [Windows 8.1: Download di Kit e strumenti](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="76a88-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="76a88-122">certificato SSL di hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="76a88-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="76a88-123">Un certificato SSL è obbligatorio tooencrypt hello comunicazione e l'autenticazione server hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="76a88-124">Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:</span><span class="sxs-lookup"><span data-stu-id="76a88-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="76a88-125">Creare un nuovo certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="76a88-126">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="76a88-127">Creare un file PFX per il certificato SSL autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="76a88-128">Caricare il certificato SSL tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="76a88-129">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="76a88-130">Importare l'Autorità di certificazione SSL</span><span class="sxs-lookup"><span data-stu-id="76a88-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="76a88-131">archiviare un certificato esistente dal certificato hello toouse</span><span class="sxs-lookup"><span data-stu-id="76a88-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="76a88-132">Esportare il certificato SSL dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="76a88-133">Caricare il certificato SSL tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="76a88-134">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="76a88-135">toouse un certificato esistente in un file PFX</span><span class="sxs-lookup"><span data-stu-id="76a88-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="76a88-136">Caricare il certificato SSL tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="76a88-137">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="76a88-138">certificati client tooconfigure</span><span class="sxs-lookup"><span data-stu-id="76a88-138">tooconfigure client certificates</span></span>
<span data-ttu-id="76a88-139">In ordine tooauthenticate richieste toohello service sono richiesti certificati client.</span><span class="sxs-lookup"><span data-stu-id="76a88-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="76a88-140">Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:</span><span class="sxs-lookup"><span data-stu-id="76a88-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="76a88-141">Disabilitare i certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="76a88-142">Disabilitare l'autenticazione basata su certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="76a88-143">Rilasciare nuovi certificati autofirmati</span><span class="sxs-lookup"><span data-stu-id="76a88-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="76a88-144">Creare un'autorità di certificazione autofirmata</span><span class="sxs-lookup"><span data-stu-id="76a88-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="76a88-145">Carica certificato della CA tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="76a88-146">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="76a88-147">Rilasciare certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="76a88-148">Creare file PFX per i certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="76a88-149">Importare il certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="76a88-150">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="76a88-151">Configurare i client consentiti in File di configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="76a88-152">Usare i certificati client esistenti</span><span class="sxs-lookup"><span data-stu-id="76a88-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="76a88-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="76a88-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="76a88-154">Carica certificato della CA tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="76a88-155">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="76a88-156">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="76a88-157">Configurare i client consentiti in File di configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="76a88-158">Configurare il controllo della revoca del certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="76a88-159">Indirizzi IP consentiti</span><span class="sxs-lookup"><span data-stu-id="76a88-159">Allowed IP addresses</span></span>
<span data-ttu-id="76a88-160">Endpoint di servizio di accesso toohello può essere limitato toospecific intervalli di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="76a88-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="76a88-161">crittografia tooconfigure per archivio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="76a88-162">Le credenziali di hello tooencrypt obbligatorio archiviate nell'archivio dei metadati hello è un certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="76a88-163">Scegliere hello più applicabile di hello tre scenari seguenti ed eseguire tutti i relativi passaggi:</span><span class="sxs-lookup"><span data-stu-id="76a88-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="76a88-164">Usare un nuovo certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="76a88-165">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="76a88-166">Creare un file PFX per il certificato di crittografia autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="76a88-167">Caricare il certificato di crittografia tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="76a88-168">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="76a88-169">Usare un certificato esistente dall'archivio certificati hello</span><span class="sxs-lookup"><span data-stu-id="76a88-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="76a88-170">Esportare il certificato di crittografia dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="76a88-171">Caricare il certificato di crittografia tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="76a88-172">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="76a88-173">Usare un certificato esistente in un file PFX</span><span class="sxs-lookup"><span data-stu-id="76a88-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="76a88-174">Caricare il certificato di crittografia tooCloud servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="76a88-175">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="76a88-176">configurazione predefinita di Hello</span><span class="sxs-lookup"><span data-stu-id="76a88-176">hello default configuration</span></span>
<span data-ttu-id="76a88-177">configurazione predefinita di Hello Nega tutte endpoint HTTP toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="76a88-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="76a88-178">Si tratta di hello impostazione, consigliata poiché hello richieste toothese endpoint potrebbe contenere informazioni riservate come le credenziali del database.</span><span class="sxs-lookup"><span data-stu-id="76a88-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="76a88-179">configurazione predefinita di Hello consente tutti endpoint HTTPS toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="76a88-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="76a88-180">Tale impostazione può essere limitata ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="76a88-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="76a88-181">Modifica configurazione hello</span><span class="sxs-lookup"><span data-stu-id="76a88-181">Changing hello Configuration</span></span>
<span data-ttu-id="76a88-182">Hello gruppo di regole di controllo di accesso che si applicano tooand endpoint sono configurati in hello  **<EndpointAcls>**  sezione hello **file di configurazione del servizio**.</span><span class="sxs-lookup"><span data-stu-id="76a88-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="76a88-183">le regole di Hello in un gruppo di controllo di accesso vengono configurate un <AccessControl name=""> sezione del file di configurazione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="76a88-184">formato di Hello è illustrato nella documentazione relativa a elenchi di controllo di accesso rete.</span><span class="sxs-lookup"><span data-stu-id="76a88-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="76a88-185">Ad esempio, tooallow solo indirizzi IP in hello 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint di intervallo, le regole di hello sono analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="76a88-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="76a88-186">Prevenzione di attacchi Denial of Service</span><span class="sxs-lookup"><span data-stu-id="76a88-186">Denial of service prevention</span></span>
<span data-ttu-id="76a88-187">Esistono due diversi meccanismi supportati toodetect e impediscono attacchi Denial of Service:</span><span class="sxs-lookup"><span data-stu-id="76a88-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="76a88-188">Limitare il numero di richieste simultanee per host remoto (opzione disattivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="76a88-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="76a88-189">Limitare la frequenza di accesso per host remoto (opzione attivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="76a88-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="76a88-190">Questi sono basati sulle funzionalità di hello documentata in sicurezza IP dinamica in IIS.</span><span class="sxs-lookup"><span data-stu-id="76a88-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="76a88-191">Quando la modifica di questa configurazione prestare attenzione al hello seguenti fattori:</span><span class="sxs-lookup"><span data-stu-id="76a88-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="76a88-192">comportamento di Hello di proxy e i dispositivi NAT sulle informazioni relative a host remoto hello</span><span class="sxs-lookup"><span data-stu-id="76a88-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="76a88-193">Ogni risorsa tooany richiesta nel ruolo web hello è considerato (ad esempio, il caricamento di script, immagini e così via)</span><span class="sxs-lookup"><span data-stu-id="76a88-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="76a88-194">Limitazione del numero di accessi simultanei</span><span class="sxs-lookup"><span data-stu-id="76a88-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="76a88-195">Hello impostazioni che consentono di configurare questo comportamento sono:</span><span class="sxs-lookup"><span data-stu-id="76a88-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="76a88-196">Modificare DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable questa protezione.</span><span class="sxs-lookup"><span data-stu-id="76a88-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="76a88-197">Limitazione della frequenza di accesso</span><span class="sxs-lookup"><span data-stu-id="76a88-197">Restricting rate of access</span></span>
<span data-ttu-id="76a88-198">Hello impostazioni che consentono di configurare questo comportamento sono:</span><span class="sxs-lookup"><span data-stu-id="76a88-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="76a88-199">Configurazione hello risposta tooa ha negato la richiesta</span><span class="sxs-lookup"><span data-stu-id="76a88-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="76a88-200">Hello seguente consente di configurare hello risposta tooa ha negato la richiesta:</span><span class="sxs-lookup"><span data-stu-id="76a88-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="76a88-201">Per altri valori supportati, consultare la documentazione di toohello per la sicurezza IP dinamica in IIS.</span><span class="sxs-lookup"><span data-stu-id="76a88-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="76a88-202">Operazioni per la configurazione dei certificati di servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="76a88-203">Questo argomento è solo per riferimento.</span><span class="sxs-lookup"><span data-stu-id="76a88-203">This topic is for reference only.</span></span> <span data-ttu-id="76a88-204">Eseguire le operazioni di configurazione hello descritte in:</span><span class="sxs-lookup"><span data-stu-id="76a88-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="76a88-205">Configurare il certificato SSL hello</span><span class="sxs-lookup"><span data-stu-id="76a88-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="76a88-206">Configurare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="76a88-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="76a88-207">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-207">Create a self-signed certificate</span></span>
<span data-ttu-id="76a88-208">Eseguire:</span><span class="sxs-lookup"><span data-stu-id="76a88-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="76a88-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="76a88-209">toocustomize:</span></span>

* <span data-ttu-id="76a88-210">URL del servizio - n con hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-210">-n with hello service URL.</span></span> <span data-ttu-id="76a88-211">Sono supportati caratteri jolly ("CN=*.cloudapp.net") e nomi alternativi ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="76a88-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="76a88-212">-e con data di scadenza certificato hello creare una password complessa e specificarlo quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="76a88-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="76a88-213">Creare un file PFX per il certificato SSL autofirmato</span><span class="sxs-lookup"><span data-stu-id="76a88-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="76a88-214">Eseguire:</span><span class="sxs-lookup"><span data-stu-id="76a88-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="76a88-215">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76a88-216">Sì, Esporta la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-216">Yes, export hello private key</span></span>
* <span data-ttu-id="76a88-217">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76a88-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="76a88-218">Esportare il certificato SSL dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="76a88-219">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-219">Find certificate</span></span>
* <span data-ttu-id="76a88-220">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76a88-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76a88-221">Esportare il certificato in un file PFX con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="76a88-222">Sì, Esporta la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="76a88-223">Se possibile, Includi tutti i certificati nel percorso certificazione hello * esportare tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76a88-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="76a88-224">Caricare il servizio toocloud certificato SSL</span><span class="sxs-lookup"><span data-stu-id="76a88-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="76a88-225">Caricamento del certificato con hello esistente o generati. File PFX con hello coppia di chiavi SSL:</span><span class="sxs-lookup"><span data-stu-id="76a88-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="76a88-226">Immettere la password di hello la protezione delle informazioni sulla chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="76a88-227">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="76a88-228">Aggiornare il valore di identificazione personale hello di hello impostazione nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76a88-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="76a88-229">Importare l'Autorità di certificazione SSL</span><span class="sxs-lookup"><span data-stu-id="76a88-229">Import SSL certification authority</span></span>
<span data-ttu-id="76a88-230">Seguire questi passaggi nell'account/macchina tutti che comunicherà con il servizio hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="76a88-231">Fare doppio clic su hello. File CER in Esplora risorse</span><span class="sxs-lookup"><span data-stu-id="76a88-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="76a88-232">Nella finestra di dialogo certificato hello, fare clic su Installa certificato...</span><span class="sxs-lookup"><span data-stu-id="76a88-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="76a88-233">Importare certificato nell'archivio Autorità di certificazione radice attendibili hello</span><span class="sxs-lookup"><span data-stu-id="76a88-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="76a88-234">Disabilitare l'autenticazione basata su certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="76a88-235">Solo autenticazione basata sui certificati client è supportata e disabilitarlo consentirà l'accesso pubblico toohello gli endpoint del servizio, a meno che non esistono altri meccanismi sono disponibili (ad esempio Microsoft rete virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="76a88-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="76a88-236">Modificare queste impostazioni toofalse in funzionalità del servizio configurazione file tooturn hello hello off:</span><span class="sxs-lookup"><span data-stu-id="76a88-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="76a88-237">Nell'impostazione del certificato CA hello, copiare hello hello SSL stessa identificazione digitale certificato:</span><span class="sxs-lookup"><span data-stu-id="76a88-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="76a88-238">Creare un'autorità di certificazione autofirmata</span><span class="sxs-lookup"><span data-stu-id="76a88-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="76a88-239">Eseguire i seguenti passaggi toocreate tooact un certificato autofirmato come autorità di certificazione hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="76a88-240">toocustomize,</span><span class="sxs-lookup"><span data-stu-id="76a88-240">toocustomize it</span></span>

* <span data-ttu-id="76a88-241">-e con la data di scadenza certificazione hello</span><span class="sxs-lookup"><span data-stu-id="76a88-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="76a88-242">Trovare la chiave pubblica CA</span><span class="sxs-lookup"><span data-stu-id="76a88-242">Find CA public key</span></span>
<span data-ttu-id="76a88-243">Tutti i certificati client devono essere stati rilasciati da un'autorità di certificazione attendibile per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="76a88-244">Trovare toohello chiave pubblica hello autorità di certificazione che ha emesso i certificati client hello che verranno toobe utilizzata per l'autenticazione in tooupload ordine servizio cloud toohello.</span><span class="sxs-lookup"><span data-stu-id="76a88-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="76a88-245">Se il file hello con chiave pubblica hello non è disponibile, è possibile esportarlo dall'archivio certificati hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="76a88-246">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-246">Find certificate</span></span>
  * <span data-ttu-id="76a88-247">Ricerca di un certificato client emesso da hello stessa autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="76a88-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="76a88-248">Fare doppio clic sul certificato hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="76a88-249">Selezionare scheda Percorso certificazione hello nella finestra di dialogo certificato hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="76a88-250">Fare doppio clic sulla voce di autorità di certificazione hello nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="76a88-251">Annotare le proprietà del certificato hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="76a88-252">Chiude hello **certificato** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="76a88-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="76a88-253">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-253">Find certificate</span></span>
  * <span data-ttu-id="76a88-254">Ricerca di hello CA indicata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="76a88-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="76a88-255">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76a88-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76a88-256">Esportare il certificato in un file con estensione CER con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="76a88-257">**No, non esportare la chiave privata di hello**</span><span class="sxs-lookup"><span data-stu-id="76a88-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="76a88-258">Se possibile, Includi tutti i certificati nel percorso certificazione hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="76a88-259">Esportare tutte le proprietà estese.</span><span class="sxs-lookup"><span data-stu-id="76a88-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="76a88-260">Autorità di certificazione certificato toocloud servizio di caricamento</span><span class="sxs-lookup"><span data-stu-id="76a88-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="76a88-261">Caricamento del certificato con hello esistente o generati. File CER con chiave pubblica hello autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="76a88-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="76a88-262">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="76a88-263">Aggiornare il valore di identificazione personale hello di hello impostazione nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76a88-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="76a88-264">Aggiornare il valore di hello di hello dopo l'impostazione con hello stessa identificazione personale:</span><span class="sxs-lookup"><span data-stu-id="76a88-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="76a88-265">Rilasciare certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-265">Issue client certificates</span></span>
<span data-ttu-id="76a88-266">Ogni servizio di hello singoli tooaccess autorizzato deve avere un certificato client emesso per his/hers esclusivo usare e deve scegliere che una password complessa tooprotect his/hers proprietari relativa chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76a88-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="76a88-267">Hello alla procedura seguente deve essere eseguito in hello nello stesso computer in cui hello autorità di certificazione certificato autofirmato è stato generato e archiviato:</span><span class="sxs-lookup"><span data-stu-id="76a88-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="76a88-268">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76a88-268">Customizing:</span></span>

* <span data-ttu-id="76a88-269">-n con un ID per il client toohello che verrà autenticata con il certificato</span><span class="sxs-lookup"><span data-stu-id="76a88-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="76a88-270">-e con data di scadenza certificato hello</span><span class="sxs-lookup"><span data-stu-id="76a88-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="76a88-271">MyID.pvk e MyID.cer con nomi file univoci per il certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="76a88-272">Questo comando richiederà una password toobe creata e quindi utilizzata una sola volta.</span><span class="sxs-lookup"><span data-stu-id="76a88-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="76a88-273">Usare una password complessa.</span><span class="sxs-lookup"><span data-stu-id="76a88-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="76a88-274">Creare file PFX per i certificati client</span><span class="sxs-lookup"><span data-stu-id="76a88-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="76a88-275">Per ogni certificato client generato, eseguire:</span><span class="sxs-lookup"><span data-stu-id="76a88-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="76a88-276">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76a88-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="76a88-277">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76a88-278">Sì, Esporta la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-278">Yes, export hello private key</span></span>
* <span data-ttu-id="76a88-279">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76a88-279">Export all extended properties</span></span>
* <span data-ttu-id="76a88-280">Questo certificato viene emessa la toowhom singoli Hello deve scegliere password esportazione hello</span><span class="sxs-lookup"><span data-stu-id="76a88-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="76a88-281">Importare il certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-281">Import client certificate</span></span>
<span data-ttu-id="76a88-282">Ogni singolo per il quale è stato emesso un certificato client deve importare una coppia di chiavi hello in macchine hello potrà utilizzerà toocommunicate con servizio hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="76a88-283">Fare doppio clic su hello. File PFX in Esplora risorse</span><span class="sxs-lookup"><span data-stu-id="76a88-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="76a88-284">Importare certificati in hello personale archiviare con almeno questa opzione:</span><span class="sxs-lookup"><span data-stu-id="76a88-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="76a88-285">Includi tutte le proprietà estese.</span><span class="sxs-lookup"><span data-stu-id="76a88-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="76a88-286">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="76a88-287">Ogni singolo per il quale è stato emesso un certificato client è necessario seguire questi passaggi nell'identificazione personale hello tooobtain di ordine di his/hers certificato che verrà aggiunto il file di configurazione servizio toohello:</span><span class="sxs-lookup"><span data-stu-id="76a88-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="76a88-288">Eseguire certmgr.exe.</span><span class="sxs-lookup"><span data-stu-id="76a88-288">Run certmgr.exe</span></span>
* <span data-ttu-id="76a88-289">Selezionare la scheda personale hello</span><span class="sxs-lookup"><span data-stu-id="76a88-289">Select hello Personal tab</span></span>
* <span data-ttu-id="76a88-290">Fare doppio clic sul certificato client hello toobe utilizzato per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="76a88-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="76a88-291">In hello certificato finestra di dialogo visualizzata, selezionare scheda Dettagli hello</span><span class="sxs-lookup"><span data-stu-id="76a88-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="76a88-292">Assicurarsi che in Mostra sia visualizzato Tutti.</span><span class="sxs-lookup"><span data-stu-id="76a88-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="76a88-293">Campo di selezione hello denominato identificazione personale nell'elenco di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="76a88-294">Copiare il valore di hello dell'identificazione digitale hello * * eliminare i caratteri Unicode non visibili davanti prima cifra hello * * eliminare tutti gli spazi</span><span class="sxs-lookup"><span data-stu-id="76a88-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="76a88-295">Configurare i client consentiti in file di configurazione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="76a88-296">Aggiornare il valore di hello di hello seguente impostazione nel file di configurazione del servizio hello con un elenco delimitato da virgole di identificazioni personali di hello dei certificati client hello consentiti l'accesso toohello servizio:</span><span class="sxs-lookup"><span data-stu-id="76a88-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="76a88-297">Configurare il controllo della revoca del certificato client</span><span class="sxs-lookup"><span data-stu-id="76a88-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="76a88-298">impostazione predefinita Hello non verifica con hello autorità di certificazione per lo stato di revoca dei certificati client.</span><span class="sxs-lookup"><span data-stu-id="76a88-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="76a88-299">tooturn su hello controlla se l'autorità di certificazione che ha rilasciato i certificati client hello hello supporta tali controlli, modificare hello seguente impostazione con uno dei valori hello definiti nell'enumerazione X509RevocationMode hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="76a88-300">Creare un file PFX per certificati di crittografia autofirmati</span><span class="sxs-lookup"><span data-stu-id="76a88-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="76a88-301">Per un certificato di crittografia eseguire:</span><span class="sxs-lookup"><span data-stu-id="76a88-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="76a88-302">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76a88-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="76a88-303">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76a88-304">Sì, Esporta la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-304">Yes, export hello private key</span></span>
* <span data-ttu-id="76a88-305">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76a88-305">Export all extended properties</span></span>
* <span data-ttu-id="76a88-306">Quando si carica il servizio cloud di hello certificato toohello, sarà necessario password hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="76a88-307">Esportare il certificato di crittografia dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="76a88-308">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-308">Find certificate</span></span>
* <span data-ttu-id="76a88-309">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76a88-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76a88-310">Esportare il certificato in un file PFX con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76a88-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="76a88-311">Sì, Esporta la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="76a88-312">Se possibile, Includi tutti i certificati nel percorso certificazione hello</span><span class="sxs-lookup"><span data-stu-id="76a88-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="76a88-313">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76a88-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="76a88-314">Servizio di crittografia certificato toocloud di caricamento</span><span class="sxs-lookup"><span data-stu-id="76a88-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="76a88-315">Caricamento del certificato con hello esistente o generati. File PFX con una coppia di chiavi di crittografia hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="76a88-316">Immettere la password di hello la protezione delle informazioni sulla chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="76a88-317">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76a88-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="76a88-318">Aggiornare il valore di identificazione personale hello di hello impostazioni nel file di configurazione del servizio hello con identificazione personale hello del servizio cloud di hello certificato caricato toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76a88-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="76a88-319">Operazioni comuni relative ai certificati</span><span class="sxs-lookup"><span data-stu-id="76a88-319">Common certificate operations</span></span>
* <span data-ttu-id="76a88-320">Configurare il certificato SSL hello</span><span class="sxs-lookup"><span data-stu-id="76a88-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="76a88-321">Configurare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="76a88-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="76a88-322">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-322">Find certificate</span></span>
<span data-ttu-id="76a88-323">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76a88-323">Follow these steps:</span></span>

1. <span data-ttu-id="76a88-324">Eseguire mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="76a88-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="76a88-325">File -> Aggiungi/Rimuovi snap-in.</span><span class="sxs-lookup"><span data-stu-id="76a88-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="76a88-326">Selezionare **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="76a88-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="76a88-327">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="76a88-327">Click **Add**.</span></span>
5. <span data-ttu-id="76a88-328">Scegliere percorso dell'archivio certificati hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="76a88-329">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76a88-329">Click **Finish**.</span></span>
7. <span data-ttu-id="76a88-330">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76a88-330">Click **OK**.</span></span>
8. <span data-ttu-id="76a88-331">Espandere **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="76a88-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="76a88-332">Espandere il nodo di archivio certificato hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="76a88-333">Espandere il nodo figlio di hello certificato.</span><span class="sxs-lookup"><span data-stu-id="76a88-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="76a88-334">Selezionare un certificato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="76a88-335">Esportare il certificato</span><span class="sxs-lookup"><span data-stu-id="76a88-335">Export certificate</span></span>
<span data-ttu-id="76a88-336">In hello **esportazione guidata certificati**:</span><span class="sxs-lookup"><span data-stu-id="76a88-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="76a88-337">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76a88-337">Click **Next**.</span></span>
2. <span data-ttu-id="76a88-338">Selezionare **Sì**, quindi **Esporta chiave privata di hello**.</span><span class="sxs-lookup"><span data-stu-id="76a88-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="76a88-339">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76a88-339">Click **Next**.</span></span>
4. <span data-ttu-id="76a88-340">Selezionare il formato di file di hello output desiderato.</span><span class="sxs-lookup"><span data-stu-id="76a88-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="76a88-341">Controllare le opzioni di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="76a88-341">Check hello desired options.</span></span>
6. <span data-ttu-id="76a88-342">Selezionare **Password**.</span><span class="sxs-lookup"><span data-stu-id="76a88-342">Check **Password**.</span></span>
7. <span data-ttu-id="76a88-343">Immettere una password complessa e confermarla.</span><span class="sxs-lookup"><span data-stu-id="76a88-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="76a88-344">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76a88-344">Click **Next**.</span></span>
9. <span data-ttu-id="76a88-345">Digitare o selezionare un nome di file in cui toostore hello certificato (usare una. Con estensione PFX).</span><span class="sxs-lookup"><span data-stu-id="76a88-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="76a88-346">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76a88-346">Click **Next**.</span></span>
11. <span data-ttu-id="76a88-347">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76a88-347">Click **Finish**.</span></span>
12. <span data-ttu-id="76a88-348">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76a88-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="76a88-349">Importare il certificato</span><span class="sxs-lookup"><span data-stu-id="76a88-349">Import certificate</span></span>
<span data-ttu-id="76a88-350">In Importazione guidata certificati hello:</span><span class="sxs-lookup"><span data-stu-id="76a88-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="76a88-351">Selezionare il percorso di archivio hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="76a88-352">Selezionare **utente corrente** se solo i processi in esecuzione in utente corrente avrà accesso servizio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="76a88-353">Selezionare **computer locale** se altri processi nel computer avrà accesso servizio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="76a88-354">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76a88-354">Click **Next**.</span></span>
3. <span data-ttu-id="76a88-355">Se l'importazione da un file, confermare il percorso del file hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="76a88-356">Se si importa un file PFX:</span><span class="sxs-lookup"><span data-stu-id="76a88-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="76a88-357">Immettere la password di hello protegge la chiave privata di hello</span><span class="sxs-lookup"><span data-stu-id="76a88-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="76a88-358">Selezionare le opzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="76a88-358">Select import options</span></span>
5. <span data-ttu-id="76a88-359">Selezionare i certificati di "Posto" nel seguente archivio hello</span><span class="sxs-lookup"><span data-stu-id="76a88-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="76a88-360">Fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="76a88-360">Click **Browse**.</span></span>
7. <span data-ttu-id="76a88-361">Selezionare l'archivio di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="76a88-361">Select hello desired store.</span></span>
8. <span data-ttu-id="76a88-362">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76a88-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="76a88-363">Se è stato scelto l'archivio di autorità di certificazione radice attendibili hello, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="76a88-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="76a88-364">Fare clic su **OK** in tutte le finestre di dialogo.</span><span class="sxs-lookup"><span data-stu-id="76a88-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="76a88-365">Caricamento del certificato</span><span class="sxs-lookup"><span data-stu-id="76a88-365">Upload certificate</span></span>
<span data-ttu-id="76a88-366">In hello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="76a88-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="76a88-367">Selezionare **Servizi cloud**.</span><span class="sxs-lookup"><span data-stu-id="76a88-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="76a88-368">Selezionare servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="76a88-369">Scegliere dal menu superiore hello **certificati**.</span><span class="sxs-lookup"><span data-stu-id="76a88-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="76a88-370">Nella barra inferiore hello, fare clic su **caricare**.</span><span class="sxs-lookup"><span data-stu-id="76a88-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="76a88-371">Selezionare il file di certificato hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="76a88-372">Se si tratta di una. PFX file, immettere la password di hello per la chiave privata di hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="76a88-373">Al termine, copiare l'identificazione personale del certificato hello da hello nuova voce di elenco hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="76a88-374">Altre considerazioni sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="76a88-374">Other security considerations</span></span>
<span data-ttu-id="76a88-375">le impostazioni SSL Hello descritte in questo documento crittografare le comunicazioni tra il servizio hello e i relativi client quando viene utilizzato l'endpoint HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="76a88-376">Questo aspetto è importante perché le credenziali per l'accesso al database e altri potenziali informazioni riservate contenute nella comunicazione hello.</span><span class="sxs-lookup"><span data-stu-id="76a88-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="76a88-377">Si noti tuttavia che il servizio hello mantiene lo stato interno, incluse le credenziali, in tabelle interne nel database SQL di Microsoft Azure hello fornito per l'archiviazione dei metadati nella sottoscrizione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="76a88-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="76a88-378">Il database è stato definito come parte di hello seguente impostazione nel file di configurazione del servizio (. File CSCFG):</span><span class="sxs-lookup"><span data-stu-id="76a88-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="76a88-379">Le credenziali archiviate in questo database vengono crittografate.</span><span class="sxs-lookup"><span data-stu-id="76a88-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="76a88-380">Tuttavia, come procedura consigliata, assicurarsi che i ruoli web e di lavoro delle distribuzioni del servizio vengono conservati backup toodate e sicura man mano che prevedono toohello metadati del database e hello certificato di accesso utilizzato per la crittografia e decrittografia di credenziali archiviate.</span><span class="sxs-lookup"><span data-stu-id="76a88-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

