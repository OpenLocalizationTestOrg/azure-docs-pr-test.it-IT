---
title: un nome di dominio personalizzato in servizi Cloud aaaConfigure | Documenti Microsoft
description: Informazioni su come tooexpose applicazione Azure o ai dati in un dominio personalizzato, configurare le impostazioni DNS.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="16232-103">Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="16232-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16232-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="16232-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="16232-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="16232-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="16232-106">Quando si crea un servizio Cloud, Azure assegna tooa sottodominio di cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="16232-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="16232-107">Ad esempio, se il servizio Cloud denominato "contoso", gli utenti verranno essere in grado di tooaccess l'applicazione in un URL come http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="16232-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="16232-108">Azure assegna anche un indirizzo IP virtuale.</span><span class="sxs-lookup"><span data-stu-id="16232-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="16232-109">È tuttavia possibile esporre l'applicazione in un nome di dominio personalizzato, ad esempio contoso.com. Questo articolo viene illustrato come tooreserve o configurare un nome di dominio personalizzato per i ruoli web del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="16232-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="16232-110">Se si conoscono già i record CNAME e A,</span><span class="sxs-lookup"><span data-stu-id="16232-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="16232-111">[Jump oltre hello spiegazione](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="16232-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="16232-112">Per velocizzare le operazioni,</span><span class="sxs-lookup"><span data-stu-id="16232-112">Get going faster!</span></span> <span data-ttu-id="16232-113">Hello utilizzare Azure [interattiva procedura dettagliata](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="16232-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="16232-114">Grazie alla procedura guidata, è facile associare un nome di dominio personalizzato e proteggere le comunicazioni (SSL) con i Servizi cloud di Azure o Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="16232-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="16232-115">procedure Hello in questa attività si applicano i servizi Cloud tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16232-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="16232-116">Per Servizi app, vedere [questo articolo](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="16232-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="16232-117">Per gli account di archiviazione, vedere [questo articolo](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="16232-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="16232-118">Informazioni sui record CNAME e A</span><span class="sxs-lookup"><span data-stu-id="16232-118">Understand CNAME and A records</span></span>
<span data-ttu-id="16232-119">CNAME (o record di alias) e un record sia consentono tooassociate un nome di dominio con un server specifico (o del servizio in questo caso,) tuttavia funzionano in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="16232-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="16232-120">Esistono inoltre alcune considerazioni specifiche quando si utilizza un record con i servizi Cloud di Azure che è necessario considerare prima di decidere quale toouse.</span><span class="sxs-lookup"><span data-stu-id="16232-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="16232-121">Record CNAME o Alias</span><span class="sxs-lookup"><span data-stu-id="16232-121">CNAME or Alias record</span></span>
<span data-ttu-id="16232-122">Esegue il mapping di un record CNAME un *specifico* dominio, ad esempio **contoso.com** o **www.contoso.com**, il nome di dominio canonico tooa.</span><span class="sxs-lookup"><span data-stu-id="16232-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="16232-123">In questo caso, il nome di dominio canonico hello è hello **.cloudapp [myapp] .net** applicazione host del dominio di Azure.</span><span class="sxs-lookup"><span data-stu-id="16232-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="16232-124">Una volta creato, hello CNAME crea un alias per hello **.cloudapp [myapp] .net**.</span><span class="sxs-lookup"><span data-stu-id="16232-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="16232-125">Hello voce CNAME risolverà l'indirizzo IP del toohello il **.cloudapp [myapp] .net** service automaticamente, se l'indirizzo IP di hello del servizio cloud hello viene modificato, non è tootake alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="16232-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="16232-126">Alcuni Registrar consentono solo i sottodomini toomap quando si utilizza un record CNAME, ad esempio www.contoso.com e non i nomi radice, ad esempio contoso.com. Per ulteriori informazioni sui record CNAME, vedere la documentazione di hello fornita dal registrar, [hello di Wikipedia sul record CNAME](http://en.wikipedia.org/wiki/CNAME_record), o hello [i nomi di dominio IETF - implementazione e specifiche](http://tools.ietf.org/html/rfc1035) documento.</span><span class="sxs-lookup"><span data-stu-id="16232-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="16232-127">Record A</span><span class="sxs-lookup"><span data-stu-id="16232-127">A record</span></span>
<span data-ttu-id="16232-128">Esegue il mapping, ad esempio un record A un dominio, **contoso.com** o **www.contoso.com**, *o in un dominio con caratteri jolly* , ad esempio  **\*. contoso.com**, indirizzo IP tooan.</span><span class="sxs-lookup"><span data-stu-id="16232-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="16232-129">Nel caso di hello di un servizio Cloud di Azure, hello IP virtuale del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="16232-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="16232-130">Vantaggio principale di hello di un record in un record CNAME è che è possibile avere una voce che utilizza un carattere jolly, ad esempio \* **. contoso.com**, che si gestisce le richieste per più sottodomini, ad esempio  **Mail.contoso.com**, **login.contoso.com**, o **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="16232-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="16232-131">Poiché viene eseguito il mapping di un record di indirizzo IP statico tooa, in grado di risolvere automaticamente le modifiche toohello IP indirizzo del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="16232-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="16232-132">indirizzo IP di Hello utilizzato dal servizio Cloud viene allocato hello prima volta che si distribuisce tooan slot vuoto (produzione o gestione temporanea.) Se si elimina la distribuzione di hello per slot hello, indirizzo IP di hello viene rilasciato da Azure e qualsiasi slot toohello distribuzioni future può essere assegnato un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="16232-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="16232-133">Per praticità, indirizzo IP hello di uno slot di distribuzione specificata (produzione o gestione temporanea) viene mantenuto quando si passa tra l'esecuzione di un aggiornamento sul posto di una distribuzione esistente e le distribuzioni di produzione o gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="16232-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="16232-134">Per ulteriori informazioni sull'esecuzione di queste azioni, vedere [come servizi cloud toomanage](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="16232-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="16232-135">Aggiunta di un record CNAME per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="16232-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="16232-136">toocreate un record CNAME, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite strumenti hello forniti dal registrar.</span><span class="sxs-lookup"><span data-stu-id="16232-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="16232-137">Ogni autorità di registrazione è un metodo simile, ma leggermente diverso per specificare un record CNAME, ma hello concetti sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="16232-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="16232-138">Utilizzare uno di questi hello toofind metodi **. cloudapp.net** nome di dominio del servizio cloud tooyour assegnato.</span><span class="sxs-lookup"><span data-stu-id="16232-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="16232-139">Account di accesso toohello [portale di Azure classico], selezionare il servizio cloud, **Dashboard**e quindi individuare hello **URL del sito** voce hello **riepilogo rapido**  sezione.</span><span class="sxs-lookup"><span data-stu-id="16232-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![sezione di riepilogo rapido che mostra l'URL del sito hello][csurl]
     
       <span data-ttu-id="16232-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="16232-141">**OR**</span></span>  
   * <span data-ttu-id="16232-142">Installare e configurare [Azure Powershell](/powershell/azure/overview), e quindi utilizzare hello finestra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="16232-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="16232-143">Salvare il nome di dominio hello utilizzato nell'URL di hello restituito da dei metodi, perché sarà necessaria quando si crea un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="16232-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="16232-144">Accedere al sito Web del registrar DNS tooyour e toohello pagina per la gestione DNS passare.</span><span class="sxs-lookup"><span data-stu-id="16232-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="16232-145">Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**.</span><span class="sxs-lookup"><span data-stu-id="16232-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="16232-146">Trovare la sezione in cui è possibile selezionare o immettere CNAME.</span><span class="sxs-lookup"><span data-stu-id="16232-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="16232-147">Potrebbe essere record hello tooselect digitare un elenco a discesa oppure passare tooan pagina Impostazioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="16232-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="16232-148">È consigliabile cercare parole hello **CNAME**, **Alias**, o **sottodomini**.</span><span class="sxs-lookup"><span data-stu-id="16232-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="16232-149">È inoltre necessario specificare hello dominio o sottodominio di alias per hello CNAME, ad esempio **www** se si desidera toocreate un alias per **www.customdomain.com**. Se si desidera toocreate un alias per il dominio radice hello, potrebbe essere elencato come hello '**@**' simbolo negli strumenti DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="16232-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="16232-150">A questo punto, occorre fornire un nome host canonico, che in questo caso corrisponde al dominio **cloudapp.net** .</span><span class="sxs-lookup"><span data-stu-id="16232-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="16232-151">Ad esempio, hello seguente record CNAME inoltra tutto il traffico da **www.contoso.com** troppo**contoso.cloudapp.net**, il nome di dominio personalizzato hello dell'applicazione distribuita:</span><span class="sxs-lookup"><span data-stu-id="16232-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="16232-152">Alias/Nome host/Sottodominio</span><span class="sxs-lookup"><span data-stu-id="16232-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="16232-153">Dominio canonico</span><span class="sxs-lookup"><span data-stu-id="16232-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="16232-154">www</span><span class="sxs-lookup"><span data-stu-id="16232-154">www</span></span> |<span data-ttu-id="16232-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="16232-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="16232-156">Un visitatore di **www.contoso.com** non vedranno mai host true hello (contoso.cloudapp.net), in modo hello processo di inoltro è l'utente finale toothe invisibile.</span><span class="sxs-lookup"><span data-stu-id="16232-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="16232-157">Hello esempio precedente si applica solo tootraffic in hello **www** sottodominio.</span><span class="sxs-lookup"><span data-stu-id="16232-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="16232-158">Poiché non è possibile usare caratteri jolly con i record CNAME, è necessario crearne uno per ogni dominio/sottodominio.</span><span class="sxs-lookup"><span data-stu-id="16232-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="16232-159">Se si desidera che il traffico toodirect da sottodomini, ad esempio \*. contoso.com, l'indirizzo di cloudapp.net tooyour, è possibile configurare un **Reindirizzamento URL** o **URL rollforward** voce nelle impostazioni DNS, o creare un record A.</span><span class="sxs-lookup"><span data-stu-id="16232-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="16232-160">Aggiungere un record A per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="16232-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="16232-161">toocreate un record, è necessario trovare indirizzi IP virtuali hello del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16232-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="16232-162">Aggiungere quindi una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite strumenti hello forniti dal registrar.</span><span class="sxs-lookup"><span data-stu-id="16232-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="16232-163">Ogni autorità di registrazione è un metodo simile, ma leggermente diverso della specifica di un record A, ma hello concetti sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="16232-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="16232-164">Utilizzare uno dei seguenti metodi tooget hello indirizzo del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="16232-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="16232-165">account di accesso toohello [portale di Azure classico], selezionare il servizio cloud, **Dashboard**e quindi individuare hello **indirizzo IP virtuale pubblico (VIP)** voce hello **riepilogo rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="16232-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![sezione di riepilogo rapido che illustra hello VIP][vip]
     
       <span data-ttu-id="16232-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="16232-167">**OR**</span></span>  
   * <span data-ttu-id="16232-168">Installare e configurare [Azure Powershell](/powershell/azure/overview), e quindi utilizzare hello finestra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="16232-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="16232-169">Se si dispone di più endpoint associati al servizio cloud, si riceverà più le righe contenenti l'indirizzo IP di hello, ma tutti deve essere visualizzato hello stesso indirizzo.</span><span class="sxs-lookup"><span data-stu-id="16232-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="16232-170">Salva l'indirizzo IP di hello, perché sarà necessaria quando si crea un record A.</span><span class="sxs-lookup"><span data-stu-id="16232-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="16232-171">Accedere al sito Web del registrar DNS tooyour e toohello pagina per la gestione DNS passare.</span><span class="sxs-lookup"><span data-stu-id="16232-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="16232-172">Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**.</span><span class="sxs-lookup"><span data-stu-id="16232-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="16232-173">Trovare la sezione in cui è possibile selezionare o immettere i record A.</span><span class="sxs-lookup"><span data-stu-id="16232-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="16232-174">Potrebbe essere record hello tooselect digitare un elenco a discesa oppure passare tooan pagina Impostazioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="16232-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="16232-175">Selezionare o immettere il dominio di hello o un sottodominio che verrà utilizzato il record A.</span><span class="sxs-lookup"><span data-stu-id="16232-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="16232-176">Ad esempio, selezionare **www** se si desidera toocreate un alias per **www.customdomain.com**. Se si desidera toocreate una voce con caratteri jolly per tutti i sottodomini, immettere '__*__'.</span><span class="sxs-lookup"><span data-stu-id="16232-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="16232-177">In questo modo verranno inclusi tutti i sottodomini, ad esempio **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="16232-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="16232-178">Se si desidera toocreate un record per il dominio radice hello, potrebbe essere elencato come hello '**@**' simbolo negli strumenti DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="16232-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="16232-179">Immettere l'indirizzo IP di hello del servizio cloud nel campo fornito hello.</span><span class="sxs-lookup"><span data-stu-id="16232-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="16232-180">In questo modo viene voce di dominio hello utilizzata nel record A hello con indirizzo IP hello la distribuzione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="16232-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="16232-181">Ad esempio, dopo un record di hello inoltra tutto il traffico da **contoso.com** troppo**137.135.70.239**, hello indirizzo IP dell'applicazione distribuita:</span><span class="sxs-lookup"><span data-stu-id="16232-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="16232-182">Nome host/Sottodominio</span><span class="sxs-lookup"><span data-stu-id="16232-182">Host name/Subdomain</span></span> | <span data-ttu-id="16232-183">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="16232-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="16232-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="16232-184">137.135.70.239</span></span> |

<span data-ttu-id="16232-185">In questo esempio viene illustrata la creazione di un record A per il dominio radice hello.</span><span class="sxs-lookup"><span data-stu-id="16232-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="16232-186">Se si desidera toocreate un toocover voce jolly tutti i sottodomini, immettere '__*__' come sottodominio hello.</span><span class="sxs-lookup"><span data-stu-id="16232-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="16232-187">Gli indirizzi IP in Azure sono dinamici per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="16232-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="16232-188">Probabilmente si desidererà toouse un [degli indirizzi IP riservati](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure che l'indirizzo IP non cambia.</span><span class="sxs-lookup"><span data-stu-id="16232-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="16232-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16232-189">Next steps</span></span>
* [<span data-ttu-id="16232-190">Come tooManage dei servizi Cloud</span><span class="sxs-lookup"><span data-stu-id="16232-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="16232-191">Come tooMap CDN contenuto tooa dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="16232-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="16232-192">[Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="16232-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="16232-193">Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="16232-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="16232-194">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="16232-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portale di Azure classico]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
