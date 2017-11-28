---
title: ruoli di servizi Cloud aaaAzure domande frequenti | Documenti Microsoft
description: Domande frequenti su Servizi cloud di Azure. L'articolo contiene risposte ad alcune domande frequenti su certificati, ruoli Web e ruoli di lavoro.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="9ddda-104">Domande frequenti sui servizi cloud</span><span class="sxs-lookup"><span data-stu-id="9ddda-104">Cloud Services FAQ</span></span>
<span data-ttu-id="9ddda-105">Questo articolo risponde ad alcune domande frequenti sui servizi cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9ddda-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="9ddda-106">È inoltre possibile visitare hello [domande frequenti su Azure supporta](http://go.microsoft.com/fwlink/?LinkID=185083) per informazioni generali su Azure prezzi e supporto.</span><span class="sxs-lookup"><span data-stu-id="9ddda-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="9ddda-107">È anche possibile consultare hello [pagina dimensione di macchina virtuale di servizi Cloud](cloud-services-sizes-specs.md) per informazioni sulle dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9ddda-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="9ddda-108">Certificati</span><span class="sxs-lookup"><span data-stu-id="9ddda-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="9ddda-109">Dove deve essere installato il certificato?</span><span class="sxs-lookup"><span data-stu-id="9ddda-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="9ddda-110">**My**</span><span class="sxs-lookup"><span data-stu-id="9ddda-110">**My**</span></span>  
  <span data-ttu-id="9ddda-111">Certificato dell'applicazione con chiave privata (con estensione \*pfx, \*p12).</span><span class="sxs-lookup"><span data-stu-id="9ddda-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="9ddda-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="9ddda-112">**CA**</span></span>  
  <span data-ttu-id="9ddda-113">Tutti i certificati intermedi, come CA secondari e criteri, vanno in questo archivio.</span><span class="sxs-lookup"><span data-stu-id="9ddda-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="9ddda-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="9ddda-114">**ROOT**</span></span>  
  <span data-ttu-id="9ddda-115">autorità di certificazione radice Hello store, il certificato della CA radice deve fare clic qui.</span><span class="sxs-lookup"><span data-stu-id="9ddda-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="9ddda-116">Non è possibile rimuovere un certificato scaduto</span><span class="sxs-lookup"><span data-stu-id="9ddda-116">I can't remove expired certificate</span></span>
<span data-ttu-id="9ddda-117">Azure impedisce la rimozione di un certificato mentre viene usato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="9ddda-118">È necessario tooeither delete hello che utilizza il certificato di hello oppure aggiornamento hello distribuzione con un certificato diverso o rinnovato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="9ddda-119">Eliminare un certificato scaduto</span><span class="sxs-lookup"><span data-stu-id="9ddda-119">Delete an expired certificate</span></span>
<span data-ttu-id="9ddda-120">Come certificato hello non è in uso, è possibile utilizzare hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove cmdlet PowerShell un certificato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="9ddda-121">Sono presenti certificati scaduti denominati Gestione dei servizi Microsoft Azure per le estensioni</span><span class="sxs-lookup"><span data-stu-id="9ddda-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="9ddda-122">Questi certificati vengono creati ogni volta che si aggiunge il servizio cloud toohello, ad esempio hello estensione Desktop remoto di un'estensione.</span><span class="sxs-lookup"><span data-stu-id="9ddda-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="9ddda-123">Questi certificati vengono utilizzati solo per la crittografia e decrittografia configurazione privata di hello dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="9ddda-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="9ddda-124">Non è un problema se questi certificati scadono,</span><span class="sxs-lookup"><span data-stu-id="9ddda-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="9ddda-125">Data di scadenza Hello non è selezionata.</span><span class="sxs-lookup"><span data-stu-id="9ddda-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="9ddda-126">I certificati eliminati continuano a riapparire</span><span class="sxs-lookup"><span data-stu-id="9ddda-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="9ddda-127">Molto probabilmente questi certificati continuano a ricomparire a causa di uno strumento che si sta usando, ad esempio Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ddda-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="9ddda-128">Ogni volta che si riconnette con uno strumento che utilizza un certificato, verrà nuovamente tooAzure caricato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="9ddda-129">I certificati continuano a scomparire</span><span class="sxs-lookup"><span data-stu-id="9ddda-129">My certificates keep disappearing</span></span>
<span data-ttu-id="9ddda-130">Quando l'istanza di macchina virtuale hello viene riciclato, tutte le modifiche locali vengono perse.</span><span class="sxs-lookup"><span data-stu-id="9ddda-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="9ddda-131">Utilizzare un [attività di avvio](cloud-services-startup-tasks.md) macchina virtuale di tooinstall certificati toohello ogni ora hello avviato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="9ddda-132">Non è possibile trovare i certificati di gestione nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="9ddda-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="9ddda-133">[I certificati di gestione](../azure-api-management-certs.md) sono disponibili solo in hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ddda-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="9ddda-134">portale di Azure corrente Hello non utilizza i certificati di gestione.</span><span class="sxs-lookup"><span data-stu-id="9ddda-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="9ddda-135">Come è possibile disabilitare un certificato di gestione?</span><span class="sxs-lookup"><span data-stu-id="9ddda-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="9ddda-136">[certificati di gestione](../azure-api-management-certs.md) non possono essere disabilitati.</span><span class="sxs-lookup"><span data-stu-id="9ddda-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="9ddda-137">È eliminarli tramite hello portale di Azure classico quando non si desidera toobe più utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9ddda-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="9ddda-138">Come è possibile creare un certificato SSL per un indirizzo IP specifico?</span><span class="sxs-lookup"><span data-stu-id="9ddda-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="9ddda-139">Seguire le direzioni di hello in hello [creare un'esercitazione certificato](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="9ddda-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="9ddda-140">Utilizzare l'indirizzo IP hello come hello nome DNS.</span><span class="sxs-lookup"><span data-stu-id="9ddda-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="9ddda-141">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="9ddda-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="9ddda-142">Disabilitare SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="9ddda-142">Disable SSL 3.0</span></span>
<span data-ttu-id="9ddda-143">toodisable SSL 3.0 e TLS utilizzo, protezione, creare un'attività di avvio è documentata in questo post di blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="9ddda-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="9ddda-144">Aggiungere **nosniff** sito Web tooyour</span><span class="sxs-lookup"><span data-stu-id="9ddda-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="9ddda-145">i client tooprevent dall'analisi dei tipi MIME hello, aggiungere un'impostazione nel *Web. config* file.</span><span class="sxs-lookup"><span data-stu-id="9ddda-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="9ddda-146">È possibile aggiungerla anche come impostazione in IIS.</span><span class="sxs-lookup"><span data-stu-id="9ddda-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="9ddda-147">Comando che segue hello di utilizzo con hello [comuni attività di avvio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) articolo.</span><span class="sxs-lookup"><span data-stu-id="9ddda-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="9ddda-148">Personalizzare IIS per un ruolo Web</span><span class="sxs-lookup"><span data-stu-id="9ddda-148">Customize IIS for a web role</span></span>
<span data-ttu-id="9ddda-149">Utilizzare lo script di avvio IIS hello da hello [comuni attività di avvio](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) articolo.</span><span class="sxs-lookup"><span data-stu-id="9ddda-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="9ddda-150">Ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="9ddda-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="9ddda-151">Impossibile eseguire la scalabilità per un numero di istanze superiore a X</span><span class="sxs-lookup"><span data-stu-id="9ddda-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="9ddda-152">La sottoscrizione di Azure ha un limite sul numero di hello di core, che è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="9ddda-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="9ddda-153">Il ridimensionamento non funzionerà se sono stati utilizzati tutti i core hello è disponibili.</span><span class="sxs-lookup"><span data-stu-id="9ddda-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="9ddda-154">Ad esempio, se si dispone di un limite di 100 memorie centrali, vuol dire che è possibile avere 100 istanze di macchina virtuale con dimensioni A1 per il servizio cloud o 50 istanze di macchine virtuali con dimensioni A2.</span><span class="sxs-lookup"><span data-stu-id="9ddda-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="9ddda-155">Rete</span><span class="sxs-lookup"><span data-stu-id="9ddda-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="9ddda-156">Non è possibile riservare un indirizzo IP in un servizio cloud con più indirizzi VIP</span><span class="sxs-lookup"><span data-stu-id="9ddda-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="9ddda-157">Innanzitutto, assicurarsi che tale istanza di macchina virtuale hello che si sta tentando di IP hello tooreserve per sia attivata.</span><span class="sxs-lookup"><span data-stu-id="9ddda-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="9ddda-158">In secondo luogo, verificare che si usi IP riservati per le distribuzioni di gestione temporanea e produzione hello integra.</span><span class="sxs-lookup"><span data-stu-id="9ddda-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="9ddda-159">**Non** modificare le impostazioni di hello durante l'aggiornamento di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9ddda-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="9ddda-160">Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="9ddda-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="9ddda-161">Come si usa Desktop remoto quando si ha un gruppo di sicurezza di rete?</span><span class="sxs-lookup"><span data-stu-id="9ddda-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="9ddda-162">Aggiungere regole toohello NSG che consentano il traffico sulle porte **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="9ddda-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="9ddda-163">Desktop remoto usa la porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="9ddda-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="9ddda-164">Le istanze del servizio cloud sono con carico bilanciato, pertanto non è possibile controllare direttamente quale tooconnect istanza di.</span><span class="sxs-lookup"><span data-stu-id="9ddda-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="9ddda-165">Hello *RemoteForwarder* e *RemoteAccess* gli agenti di gestire il traffico RDP e consentire hello client toosend un cookie RDP e specificare tooconnect una singola istanza di.</span><span class="sxs-lookup"><span data-stu-id="9ddda-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="9ddda-166">Hello *RemoteForwarder* e *RemoteAccess* agenti richiedono tale porta **20000*** aperto, che può essere bloccato se si dispone di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="9ddda-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
