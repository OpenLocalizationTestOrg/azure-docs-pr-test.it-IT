---
title: Configurazione della sicurezza del servizio di divisione e unione | Documentazione Microsoft
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="76b10-103">Configurazione della sicurezza del servizio di divisione e unione</span><span class="sxs-lookup"><span data-stu-id="76b10-103">Split-merge security configuration</span></span>
<span data-ttu-id="76b10-104">Per usare il servizio di "split and merge", è necessario configurare correttamente le impostazioni sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="76b10-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="76b10-105">Il servizio rientra nella funzionalità Scalabilità elastica di database SQL di Microsoft Azur.</span><span class="sxs-lookup"><span data-stu-id="76b10-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="76b10-106">Per altre informazioni, vedere [Esercitazione relativa allo strumento divisione-unione del database elastico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="76b10-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="76b10-107">Configurazione dei certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-107">Configuring certificates</span></span>
<span data-ttu-id="76b10-108">I certificati vengono configurati in due modi.</span><span class="sxs-lookup"><span data-stu-id="76b10-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="76b10-109">Per configurare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="76b10-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="76b10-110">Per configurare i certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="76b10-111">Per ottenere i certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-111">To obtain certificates</span></span>
<span data-ttu-id="76b10-112">È possibile ottenere i certificati da Autorità di certificazione (CA) pubbliche o dal [servizio certificati di Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="76b10-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="76b10-113">Questi sono i metodi consigliati per ottenere i certificati.</span><span class="sxs-lookup"><span data-stu-id="76b10-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="76b10-114">Se tali opzioni non sono disponibili, è possibile generare **certificati autofirmati**.</span><span class="sxs-lookup"><span data-stu-id="76b10-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="76b10-115">Strumenti per generare i certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="76b10-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="76b10-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="76b10-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="76b10-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="76b10-118">Per eseguire gli strumenti</span><span class="sxs-lookup"><span data-stu-id="76b10-118">To run the tools</span></span>
* <span data-ttu-id="76b10-119">Da un Prompt dei comandi per gli sviluppatori per Visual Studio, vedere l'articolo relativo al [prompt dei comandi di Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="76b10-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="76b10-120">Se installato, passare a:</span><span class="sxs-lookup"><span data-stu-id="76b10-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="76b10-121">Ottenere il WDK da [Windows 8.1: download di kit e strumenti](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="76b10-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="76b10-122">Per configurare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="76b10-122">To configure the SSL certificate</span></span>
<span data-ttu-id="76b10-123">Un certificato SSL è necessario per crittografare la comunicazione e autenticare il server.</span><span class="sxs-lookup"><span data-stu-id="76b10-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="76b10-124">Scegliere il più appropriato dei tre seguenti scenari ed eseguirne tutti i passaggi:</span><span class="sxs-lookup"><span data-stu-id="76b10-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="76b10-125">Creare un nuovo certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="76b10-126">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="76b10-127">Creare un file PFX per il certificato SSL autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="76b10-128">Caricare il certificato SSL nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="76b10-129">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="76b10-130">Importare l'Autorità di certificazione SSL</span><span class="sxs-lookup"><span data-stu-id="76b10-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="76b10-131">Per usare un certificato esistente dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="76b10-132">Esportare il certificato SSL dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="76b10-133">Caricare il certificato SSL nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="76b10-134">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="76b10-135">Per usare un certificato esistente in un file con estensione pfx</span><span class="sxs-lookup"><span data-stu-id="76b10-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="76b10-136">Caricare il certificato SSL nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="76b10-137">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="76b10-138">Per configurare i certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-138">To configure client certificates</span></span>
<span data-ttu-id="76b10-139">I certificati client sono necessari per autenticare le richieste al servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="76b10-140">Scegliere il più appropriato dei tre seguenti scenari ed eseguirne tutti i passaggi:</span><span class="sxs-lookup"><span data-stu-id="76b10-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="76b10-141">Disabilitare i certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="76b10-142">Disabilitare l'autenticazione basata su certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="76b10-143">Rilasciare nuovi certificati autofirmati</span><span class="sxs-lookup"><span data-stu-id="76b10-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="76b10-144">Creare un'autorità di certificazione autofirmata</span><span class="sxs-lookup"><span data-stu-id="76b10-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="76b10-145">Caricare un certificato della CA nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="76b10-146">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="76b10-147">Rilasciare certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="76b10-148">Creare file PFX per i certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="76b10-149">Importare il certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="76b10-150">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="76b10-151">Configurare i client consentiti nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="76b10-152">Usare i certificati client esistenti</span><span class="sxs-lookup"><span data-stu-id="76b10-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="76b10-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="76b10-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="76b10-154">Caricare un certificato della CA nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="76b10-155">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="76b10-156">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="76b10-157">Configurare i client consentiti nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="76b10-158">Configurare il controllo della revoca del certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="76b10-159">Indirizzi IP consentiti</span><span class="sxs-lookup"><span data-stu-id="76b10-159">Allowed IP addresses</span></span>
<span data-ttu-id="76b10-160">L'accesso agli endpoint del servizio può essere limitato a intervalli specifici di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="76b10-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="76b10-161">Per configurare la crittografia per l'archivio</span><span class="sxs-lookup"><span data-stu-id="76b10-161">To configure encryption for the store</span></span>
<span data-ttu-id="76b10-162">È necessario un certificato per crittografare le credenziali archiviate nell'archivio di metadati.</span><span class="sxs-lookup"><span data-stu-id="76b10-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="76b10-163">Scegliere il più appropriato dei tre seguenti scenari ed eseguirne tutti i passaggi:</span><span class="sxs-lookup"><span data-stu-id="76b10-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="76b10-164">Usare un nuovo certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="76b10-165">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="76b10-166">Creare un file PFX per il certificato di crittografia autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="76b10-167">Caricare il certificato di crittografia nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="76b10-168">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="76b10-169">Usare un certificato esistente dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="76b10-170">Esportare il certificato di crittografia dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="76b10-171">Caricare il certificato di crittografia nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="76b10-172">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="76b10-173">Usare un certificato esistente in un file PFX</span><span class="sxs-lookup"><span data-stu-id="76b10-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="76b10-174">Caricare il certificato di crittografia nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="76b10-175">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="76b10-176">Configurazione predefinita</span><span class="sxs-lookup"><span data-stu-id="76b10-176">The default configuration</span></span>
<span data-ttu-id="76b10-177">La configurazione predefinita nega qualunque accesso all'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="76b10-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="76b10-178">Questa è l'impostazione consigliata, in quanto le richieste inviate a tali endpoint posso includere dati sensibili come le credenziali di database.</span><span class="sxs-lookup"><span data-stu-id="76b10-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="76b10-179">La configurazione predefinita consente qualunque accesso all'endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="76b10-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="76b10-180">Tale impostazione può essere limitata ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="76b10-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="76b10-181">Modifica della configurazione</span><span class="sxs-lookup"><span data-stu-id="76b10-181">Changing the Configuration</span></span>
<span data-ttu-id="76b10-182">Il gruppo di regole di controllo di accesso applicabili a un endpoint viene configurato nella sezione **<EndpointAcls>** del **file di configurazione del servizio**.</span><span class="sxs-lookup"><span data-stu-id="76b10-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="76b10-183">Le regole incluse in un gruppo di controllo di accesso vengono configurate in una sezione <AccessControl name=""> del file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="76b10-184">Il formato è illustrato nella documentazione relativa agli elenchi di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="76b10-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="76b10-185">Ad esempio, per consentire l'accesso all'endpoint HTTPS solo per gli indirizzi IP compresi nell'intervallo da 100.100.0.0 a 100.100.255.255, le regole saranno simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="76b10-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="76b10-186">Prevenzione di attacchi Denial of Service</span><span class="sxs-lookup"><span data-stu-id="76b10-186">Denial of service prevention</span></span>
<span data-ttu-id="76b10-187">Per rilevare e impedire attacchi Denial of Service sono supportati due diversi meccanismi:</span><span class="sxs-lookup"><span data-stu-id="76b10-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="76b10-188">Limitare il numero di richieste simultanee per host remoto (opzione disattivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="76b10-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="76b10-189">Limitare la frequenza di accesso per host remoto (opzione attivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="76b10-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="76b10-190">Questi meccanismi si basano sulle funzionalità illustrate più estesamente nella documentazione relativa alla sicurezza degli IP dinamici in IIS.</span><span class="sxs-lookup"><span data-stu-id="76b10-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="76b10-191">Quando si modifica questa configurazione, prestare attenzione ai seguenti fattori:</span><span class="sxs-lookup"><span data-stu-id="76b10-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="76b10-192">Comportamento del proxy e dei dispositivi NAT (Network Address Translation)rispetto alle informazioni sull'host remoto.</span><span class="sxs-lookup"><span data-stu-id="76b10-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="76b10-193">Viene considerata ogni richiesta a qualsiasi risorsa nel ruolo Web (ad esempio, caricamento di script, immagini e così via).</span><span class="sxs-lookup"><span data-stu-id="76b10-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="76b10-194">Limitazione del numero di accessi simultanei</span><span class="sxs-lookup"><span data-stu-id="76b10-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="76b10-195">Le impostazioni che configurano questo comportamento sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="76b10-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="76b10-196">Impostare DynamicIpRestrictionDenyByConcurrentRequests su true per abilitare questa protezione.</span><span class="sxs-lookup"><span data-stu-id="76b10-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="76b10-197">Limitazione della frequenza di accesso</span><span class="sxs-lookup"><span data-stu-id="76b10-197">Restricting rate of access</span></span>
<span data-ttu-id="76b10-198">Le impostazioni che configurano questo comportamento sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="76b10-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="76b10-199">Configurazione della risposta a una richiesta negata</span><span class="sxs-lookup"><span data-stu-id="76b10-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="76b10-200">La seguente impostazione configura la risposta a una richiesta negata:</span><span class="sxs-lookup"><span data-stu-id="76b10-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="76b10-201">Per altri valori supportati, vedere la documentazione relativa alla sicurezza degli IP dinamici in IIS.</span><span class="sxs-lookup"><span data-stu-id="76b10-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="76b10-202">Operazioni per la configurazione dei certificati di servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="76b10-203">Questo argomento è solo per riferimento.</span><span class="sxs-lookup"><span data-stu-id="76b10-203">This topic is for reference only.</span></span> <span data-ttu-id="76b10-204">Attenersi alla procedura di configurazione riportata in:</span><span class="sxs-lookup"><span data-stu-id="76b10-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="76b10-205">Configurare il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="76b10-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="76b10-206">Configurare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="76b10-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="76b10-207">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-207">Create a self-signed certificate</span></span>
<span data-ttu-id="76b10-208">Eseguire:</span><span class="sxs-lookup"><span data-stu-id="76b10-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="76b10-209">Per personalizzare:</span><span class="sxs-lookup"><span data-stu-id="76b10-209">To customize:</span></span>

* <span data-ttu-id="76b10-210">-n con l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-210">-n with the service URL.</span></span> <span data-ttu-id="76b10-211">Sono supportati caratteri jolly ("CN=*.cloudapp.net") e nomi alternativi ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="76b10-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="76b10-212">-e con la data di scadenza del certificato creare una password complessa e specificarla quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="76b10-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="76b10-213">Creare un file PFX per il certificato SSL autofirmato</span><span class="sxs-lookup"><span data-stu-id="76b10-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="76b10-214">Eseguire:</span><span class="sxs-lookup"><span data-stu-id="76b10-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="76b10-215">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76b10-216">Sì, esporta la chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b10-216">Yes, export the private key</span></span>
* <span data-ttu-id="76b10-217">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76b10-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="76b10-218">Esportare il certificato SSL dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="76b10-219">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-219">Find certificate</span></span>
* <span data-ttu-id="76b10-220">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76b10-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76b10-221">Esportare il certificato in un file PFX con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="76b10-222">Sì, esporta la chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b10-222">Yes, export the private key</span></span>
  * <span data-ttu-id="76b10-223">Se possibile, includere tutti i certificati nel percorso della certificazione *Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76b10-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="76b10-224">Caricare il certificato SSL nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="76b10-225">Caricare il certificato con il file PFX esistente o generato con la coppia di chiavi SSL:</span><span class="sxs-lookup"><span data-stu-id="76b10-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="76b10-226">Immettere la password che protegge le informazioni sulla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b10-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="76b10-227">Aggiornare il certificato SSL nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="76b10-228">Aggiornare il valore di identificazione personale della seguente impostazione nel file di configurazione del servizio con l'identificazione personale del certificato caricato nel servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="76b10-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="76b10-229">Importare l'Autorità di certificazione SSL</span><span class="sxs-lookup"><span data-stu-id="76b10-229">Import SSL certification authority</span></span>
<span data-ttu-id="76b10-230">Seguire questa procedura in tutti gli account o i computer che comunicheranno con il servizio:</span><span class="sxs-lookup"><span data-stu-id="76b10-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="76b10-231">Fare doppio clic sul file con estensione CER in Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="76b10-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="76b10-232">Nella finestra di dialogo Certificato fare clic su Installa certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="76b10-233">Importare il certificato nell'archivio delle Autorità di certificazione radice disponibili nell'elenco locale.</span><span class="sxs-lookup"><span data-stu-id="76b10-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="76b10-234">Disabilitare l'autenticazione basata su certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="76b10-235">È supportata solo autenticazione basata su certificati client. Se viene disabilitata, consentirà l'accesso pubblico agli endpoint del servizio, a meno che siano implementati altri meccanismi (ad esempio, Rete virtuale di Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="76b10-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="76b10-236">Per disabilitare la funzionalità, modificare queste impostazioni specificando false nel file di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="76b10-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="76b10-237">Copiare quindi la stessa identificazione personale del certificato SSL nell'impostazione del certificato della CA:</span><span class="sxs-lookup"><span data-stu-id="76b10-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="76b10-238">Creare un'autorità di certificazione autofirmata</span><span class="sxs-lookup"><span data-stu-id="76b10-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="76b10-239">Per creare un certificato autofirmato che funga da autorità di certificazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76b10-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="76b10-240">Per personalizzarlo</span><span class="sxs-lookup"><span data-stu-id="76b10-240">To customize it</span></span>

* <span data-ttu-id="76b10-241">-e con la data di scadenza del certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="76b10-242">Trovare la chiave pubblica CA</span><span class="sxs-lookup"><span data-stu-id="76b10-242">Find CA public key</span></span>
<span data-ttu-id="76b10-243">Tutti i certificati client devono essere rilasciati da un'autorità di certificazione considerata attendibile dal servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="76b10-244">Trovare la chiave pubblica all'autorità di certificazione che ha rilasciato i certificati client da usare per l'autenticazione per caricarla nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="76b10-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="76b10-245">Se il file con la chiave pubblica non è disponibile, esportarlo dall'archivio certificati:</span><span class="sxs-lookup"><span data-stu-id="76b10-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="76b10-246">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-246">Find certificate</span></span>
  * <span data-ttu-id="76b10-247">Cercare un certificato client rilasciato dalla stessa autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="76b10-248">Fare doppio clic sul certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-248">Double-click the certificate.</span></span>
* <span data-ttu-id="76b10-249">Selezionare la scheda Percorso certificazione nella finestra di dialogo Certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="76b10-250">Fare doppio clic sulla voce relativa alla CA inclusa nel percorso.</span><span class="sxs-lookup"><span data-stu-id="76b10-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="76b10-251">Prendere nota delle proprietà del certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="76b10-252">Chiudere la finestra di dialogo **Certificato** .</span><span class="sxs-lookup"><span data-stu-id="76b10-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="76b10-253">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-253">Find certificate</span></span>
  * <span data-ttu-id="76b10-254">Cercare la CA annotata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="76b10-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="76b10-255">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76b10-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76b10-256">Esportare il certificato in un file con estensione CER con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="76b10-257">**No, non esportare la chiave privata**</span><span class="sxs-lookup"><span data-stu-id="76b10-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="76b10-258">Se possibile, includi tutti i certificati nel percorso certificazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="76b10-259">Esportare tutte le proprietà estese.</span><span class="sxs-lookup"><span data-stu-id="76b10-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="76b10-260">Caricare un certificato della CA nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="76b10-261">Caricare il certificato con il file PFX esistente o generato con la coppia di chiavi SSL.</span><span class="sxs-lookup"><span data-stu-id="76b10-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="76b10-262">Aggiornare il certificato della CA nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="76b10-263">Aggiornare il valore di identificazione personale della seguente impostazione nel file di configurazione del servizio con l'identificazione personale del certificato caricato nel servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="76b10-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="76b10-264">Aggiornare il valore della seguente impostazione con la stessa identificazione personale:</span><span class="sxs-lookup"><span data-stu-id="76b10-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="76b10-265">Rilasciare certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-265">Issue client certificates</span></span>
<span data-ttu-id="76b10-266">Ogni utente con l'autorizzazione di accesso al servizio deve avere un certificato client rilasciato per proprio uso esclusivo e scegliere una propria password complessa per proteggere la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b10-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="76b10-267">Seguire questa procedura nello stesso computer in cui è stato generato e archiviato il certificato CA autofirmato:</span><span class="sxs-lookup"><span data-stu-id="76b10-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="76b10-268">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76b10-268">Customizing:</span></span>

* <span data-ttu-id="76b10-269">-n con un ID per il client che verrà autenticato con il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="76b10-270">-e con la data di scadenza del certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="76b10-271">MyID.pvk e MyID.cer con nomi file univoci per il certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="76b10-272">Questo comando richiederà la creazione di una password che verrà quindi usata una sola volta.</span><span class="sxs-lookup"><span data-stu-id="76b10-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="76b10-273">Usare una password complessa.</span><span class="sxs-lookup"><span data-stu-id="76b10-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="76b10-274">Creare file PFX per i certificati client</span><span class="sxs-lookup"><span data-stu-id="76b10-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="76b10-275">Per ogni certificato client generato, eseguire:</span><span class="sxs-lookup"><span data-stu-id="76b10-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="76b10-276">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76b10-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="76b10-277">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76b10-278">Sì, esporta la chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b10-278">Yes, export the private key</span></span>
* <span data-ttu-id="76b10-279">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76b10-279">Export all extended properties</span></span>
* <span data-ttu-id="76b10-280">L'utente a cui viene rilasciato il certificato deve scegliere la password di esportazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="76b10-281">Importare il certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-281">Import client certificate</span></span>
<span data-ttu-id="76b10-282">Ogni utente per il quale è stato rilasciato un certificato client dovrà importare la coppia di chiavi nei computer che userà per comunicare con il servizio:</span><span class="sxs-lookup"><span data-stu-id="76b10-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="76b10-283">Fare doppio clic sul file con estensione CER in Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="76b10-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="76b10-284">Importare il certificato nell'archivio personale con selezionata almeno questa opzione:</span><span class="sxs-lookup"><span data-stu-id="76b10-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="76b10-285">Includi tutte le proprietà estese.</span><span class="sxs-lookup"><span data-stu-id="76b10-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="76b10-286">Copiare le identificazioni personali del certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="76b10-287">Ogni utente per il quale è stato rilasciato un certificato client dovrà seguire questa procedura per ottenere l'identificazione personale del proprio certificato, che verrà aggiunto al file di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="76b10-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="76b10-288">Eseguire certmgr.exe.</span><span class="sxs-lookup"><span data-stu-id="76b10-288">Run certmgr.exe</span></span>
* <span data-ttu-id="76b10-289">Selezionare la scheda Personale.</span><span class="sxs-lookup"><span data-stu-id="76b10-289">Select the Personal tab</span></span>
* <span data-ttu-id="76b10-290">Fare doppio clic sul certificato client da usare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="76b10-291">Nella finestra di dialogo Certificato visualizzata selezionare la scheda Dettagli.</span><span class="sxs-lookup"><span data-stu-id="76b10-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="76b10-292">Assicurarsi che in Mostra sia visualizzato Tutti.</span><span class="sxs-lookup"><span data-stu-id="76b10-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="76b10-293">Nell'elenco selezionare il campo denominato Identificazione personale.</span><span class="sxs-lookup"><span data-stu-id="76b10-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="76b10-294">Copiare il valore dell'identificazione personale ** Eliminare i caratteri Unicode non visibili davanti alla prima cifra ** Eliminare tutti gli spazi</span><span class="sxs-lookup"><span data-stu-id="76b10-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="76b10-295">Configurare i client consentiti nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="76b10-296">Aggiornare il valore della seguente impostazione nel file di configurazione del servizio con un elenco delimitato da virgole delle identificazioni personali dei certificati client a cui è consentito accedere al servizio:</span><span class="sxs-lookup"><span data-stu-id="76b10-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="76b10-297">Configurare il controllo della revoca del certificato client</span><span class="sxs-lookup"><span data-stu-id="76b10-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="76b10-298">Per impostazione predefinita,lo stato della revoca del certificato non viene verificato con l'Autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="76b10-299">Per abilitare i controlli, se l'Autorità di certificazione che ha rilasciato i certificati client li supporta, modificare la seguente impostazione con uno dei valori definiti nell'enumerazione X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="76b10-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="76b10-300">Creare un file PFX per certificati di crittografia autofirmati</span><span class="sxs-lookup"><span data-stu-id="76b10-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="76b10-301">Per un certificato di crittografia eseguire:</span><span class="sxs-lookup"><span data-stu-id="76b10-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="76b10-302">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="76b10-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="76b10-303">Immettere la password e quindi esportare il certificato con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="76b10-304">Sì, esporta la chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b10-304">Yes, export the private key</span></span>
* <span data-ttu-id="76b10-305">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76b10-305">Export all extended properties</span></span>
* <span data-ttu-id="76b10-306">Quando si carica il certificato nel servizio cloud, sarà necessaria la password.</span><span class="sxs-lookup"><span data-stu-id="76b10-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="76b10-307">Esportare il certificato di crittografia dall'archivio certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="76b10-308">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-308">Find certificate</span></span>
* <span data-ttu-id="76b10-309">Fare clic su Azioni -> Tutte le attività -> Esporta.</span><span class="sxs-lookup"><span data-stu-id="76b10-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="76b10-310">Esportare il certificato in un file PFX con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="76b10-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="76b10-311">Sì, esporta la chiave privata</span><span class="sxs-lookup"><span data-stu-id="76b10-311">Yes, export the private key</span></span>
  * <span data-ttu-id="76b10-312">Se possibile, includi tutti i certificati nel percorso certificazione</span><span class="sxs-lookup"><span data-stu-id="76b10-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="76b10-313">Esporta tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="76b10-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="76b10-314">Caricare il certificato di crittografia nel servizio cloud</span><span class="sxs-lookup"><span data-stu-id="76b10-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="76b10-315">Caricare il certificato con il file PFX esistente o generato con la coppia di chiavi di crittografia:</span><span class="sxs-lookup"><span data-stu-id="76b10-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="76b10-316">Immettere la password che protegge le informazioni sulla chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b10-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="76b10-317">Aggiornare il certificato di crittografia nel file di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="76b10-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="76b10-318">Aggiornare il valore di identificazione personale della seguente impostazione nel file di configurazione del servizio con l'identificazione personale del certificato caricato nel servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="76b10-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="76b10-319">Operazioni comuni relative ai certificati</span><span class="sxs-lookup"><span data-stu-id="76b10-319">Common certificate operations</span></span>
* <span data-ttu-id="76b10-320">Configurare il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="76b10-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="76b10-321">Configurare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="76b10-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="76b10-322">Trovare il certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-322">Find certificate</span></span>
<span data-ttu-id="76b10-323">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="76b10-323">Follow these steps:</span></span>

1. <span data-ttu-id="76b10-324">Eseguire mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="76b10-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="76b10-325">File -> Aggiungi/Rimuovi snap-in.</span><span class="sxs-lookup"><span data-stu-id="76b10-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="76b10-326">Selezionare **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="76b10-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="76b10-327">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="76b10-327">Click **Add**.</span></span>
5. <span data-ttu-id="76b10-328">Scegliere il percorso dell'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="76b10-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="76b10-329">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76b10-329">Click **Finish**.</span></span>
7. <span data-ttu-id="76b10-330">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76b10-330">Click **OK**.</span></span>
8. <span data-ttu-id="76b10-331">Espandere **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="76b10-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="76b10-332">Espandere il nodo dell'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="76b10-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="76b10-333">Espandere il nodo figlio Certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="76b10-334">Selezionare un certificato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="76b10-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="76b10-335">Esportare il certificato</span><span class="sxs-lookup"><span data-stu-id="76b10-335">Export certificate</span></span>
<span data-ttu-id="76b10-336">In **Esportazione guidata certificati**:</span><span class="sxs-lookup"><span data-stu-id="76b10-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="76b10-337">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76b10-337">Click **Next**.</span></span>
2. <span data-ttu-id="76b10-338">Selezionare **Sì** e quindi **Esporta la chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="76b10-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="76b10-339">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76b10-339">Click **Next**.</span></span>
4. <span data-ttu-id="76b10-340">Selezionare il formato del file di output desiderato.</span><span class="sxs-lookup"><span data-stu-id="76b10-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="76b10-341">Controllare le opzioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="76b10-341">Check the desired options.</span></span>
6. <span data-ttu-id="76b10-342">Selezionare **Password**.</span><span class="sxs-lookup"><span data-stu-id="76b10-342">Check **Password**.</span></span>
7. <span data-ttu-id="76b10-343">Immettere una password complessa e confermarla.</span><span class="sxs-lookup"><span data-stu-id="76b10-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="76b10-344">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76b10-344">Click **Next**.</span></span>
9. <span data-ttu-id="76b10-345">Digitare o cercare un nome file in cui archiviare il certificato (usare un'estensione PFX).</span><span class="sxs-lookup"><span data-stu-id="76b10-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="76b10-346">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76b10-346">Click **Next**.</span></span>
11. <span data-ttu-id="76b10-347">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76b10-347">Click **Finish**.</span></span>
12. <span data-ttu-id="76b10-348">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="76b10-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="76b10-349">Importare il certificato</span><span class="sxs-lookup"><span data-stu-id="76b10-349">Import certificate</span></span>
<span data-ttu-id="76b10-350">In Esportazione guidata certificati:</span><span class="sxs-lookup"><span data-stu-id="76b10-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="76b10-351">Selezionare il percorso dell'archivio.</span><span class="sxs-lookup"><span data-stu-id="76b10-351">Select the store location.</span></span>
   
   * <span data-ttu-id="76b10-352">Selezionare **Utente corrente** se solo i processi eseguiti dall'utente corrente accederanno al servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="76b10-353">Selezionare **Computer locale** se altri processi nel computer accederanno al servizio.</span><span class="sxs-lookup"><span data-stu-id="76b10-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="76b10-354">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="76b10-354">Click **Next**.</span></span>
3. <span data-ttu-id="76b10-355">Se l'importazione viene effettuata da un file, verificare il percorso del file.</span><span class="sxs-lookup"><span data-stu-id="76b10-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="76b10-356">Se si importa un file PFX:</span><span class="sxs-lookup"><span data-stu-id="76b10-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="76b10-357">Immettere la password che protegge la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b10-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="76b10-358">Selezionare le opzioni di importazione.</span><span class="sxs-lookup"><span data-stu-id="76b10-358">Select import options</span></span>
5. <span data-ttu-id="76b10-359">Selezionare "Colloca" tutti i certificati nel seguente archivio.</span><span class="sxs-lookup"><span data-stu-id="76b10-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="76b10-360">Fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="76b10-360">Click **Browse**.</span></span>
7. <span data-ttu-id="76b10-361">Selezionare l'archivio da usare.</span><span class="sxs-lookup"><span data-stu-id="76b10-361">Select the desired store.</span></span>
8. <span data-ttu-id="76b10-362">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76b10-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="76b10-363">Se è stato scelto l'archivio dell'autorità di certificazione radice attendibile, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="76b10-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="76b10-364">Fare clic su **OK** in tutte le finestre di dialogo.</span><span class="sxs-lookup"><span data-stu-id="76b10-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="76b10-365">Caricamento del certificato</span><span class="sxs-lookup"><span data-stu-id="76b10-365">Upload certificate</span></span>
<span data-ttu-id="76b10-366">Nel [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="76b10-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="76b10-367">Selezionare **Servizi cloud**.</span><span class="sxs-lookup"><span data-stu-id="76b10-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="76b10-368">Selezionare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="76b10-368">Select the cloud service.</span></span>
3. <span data-ttu-id="76b10-369">Nel menu superiore fare clic su **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="76b10-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="76b10-370">Nella barra inferiore fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="76b10-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="76b10-371">Selezionare il file del certificato.</span><span class="sxs-lookup"><span data-stu-id="76b10-371">Select the certificate file.</span></span>
6. <span data-ttu-id="76b10-372">Se è un file con estensione PFX, immettere la password per la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="76b10-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="76b10-373">Una volta completata l'operazione, copiare l'identificazione personale del certificato dalla nuova voce nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="76b10-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="76b10-374">Altre considerazioni sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="76b10-374">Other security considerations</span></span>
<span data-ttu-id="76b10-375">Le impostazioni SSL descritte in questo documento crittografano le comunicazioni tra il servizio e i relativi client quando si usa l'endpoint HTTPS.</span><span class="sxs-lookup"><span data-stu-id="76b10-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="76b10-376">Questo aspetto è importante perché nella comunicazione sono contenute le credenziali per l'accesso al database e potenzialmente altre informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="76b10-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="76b10-377">Si noti che il servizio mantiene lo stato interno, incluse le credenziali, nelle relative tabelle interne del database SQL di Microsoft Azure fornite per l'archiviazione dei metadati nella sottoscrizione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="76b10-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="76b10-378">Tale database è stato definito come parte della seguente impostazione nel file di configurazione del servizio (file CSCFG):</span><span class="sxs-lookup"><span data-stu-id="76b10-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="76b10-379">Le credenziali archiviate in questo database vengono crittografate.</span><span class="sxs-lookup"><span data-stu-id="76b10-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="76b10-380">Come procedura consigliata è opportuno verificare tuttavia che i ruoli Web e di lavoro delle distribuzioni del servizio siano sempre aggiornati e protetti, in quanto dispongono dell'accesso al database di metadati e al certificato usati per la crittografia e decrittografia delle credenziali archiviate.</span><span class="sxs-lookup"><span data-stu-id="76b10-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

