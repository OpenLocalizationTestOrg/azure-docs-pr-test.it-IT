---
title: Configurare un nome di dominio personalizzato nei servizi cloud | Microsoft Docs
description: Informazioni su come esporre i dati su internet o l'applicazione Azure in un dominio personalizzato configurando le impostazioni DNS.  Questi esempi utilizzano il portale di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="fd36e-104">Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="fd36e-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd36e-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fd36e-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="fd36e-106">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fd36e-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="fd36e-107">Quando si crea un servizo cloud, Azure lo assegna a un sottodominio di **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="fd36e-108">Ad esempio, se il servizio cloud è denominato "contoso", gli utenti saranno in grado di accedere all'applicazione da un URL come http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="fd36e-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="fd36e-109">Azure assegna anche un indirizzo IP virtuale.</span><span class="sxs-lookup"><span data-stu-id="fd36e-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="fd36e-110">È tuttavia possibile esporre l'applicazione in un nome di dominio personalizzato, ad esempio **contoso.com**. In questo articolo viene illustrato come riservare o configurare un nome di dominio personalizzato per i ruoli Web del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd36e-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="fd36e-111">Se si conoscono già i record CNAME e A,</span><span class="sxs-lookup"><span data-stu-id="fd36e-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="fd36e-112">[saltare la spiegazione](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="fd36e-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="fd36e-113">Le procedure in questa attività si applicano ai servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd36e-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="fd36e-114">Per Servizi app, vedere [questo articolo](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="fd36e-115">Per gli account di archiviazione, vedere [questo articolo](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="fd36e-116">Acquistare velocità: usare il NUOVO [percorso guidato](http://support.microsoft.com/kb/2990804) di Azure</span><span class="sxs-lookup"><span data-stu-id="fd36e-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="fd36e-117">Grazie al percorso guidato, è facilissimo associare un nome di dominio personalizzato E proteggere le comunicazioni (SSL) con i Servizi cloud di Azure o Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd36e-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="fd36e-118">Informazioni sui record CNAME e A</span><span class="sxs-lookup"><span data-stu-id="fd36e-118">Understand CNAME and A records</span></span>
<span data-ttu-id="fd36e-119">I record CNAME (o record Alias) e i record A consentono entrambi di associare un nome di dominio a un server specifico (o in questo caso a un servizio) tuttavia le modalità di funzionamento sono diverse.</span><span class="sxs-lookup"><span data-stu-id="fd36e-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="fd36e-120">Vi sono inoltre alcune considerazioni specifiche sull'utilizzo di record A con i servizi cloud di Azure, di cui è necessario tenere conto prima di decidere il tipo di record da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="fd36e-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="fd36e-121">Record CNAME o Alias</span><span class="sxs-lookup"><span data-stu-id="fd36e-121">CNAME or Alias record</span></span>
<span data-ttu-id="fd36e-122">Un record CNAME consente di eseguire il mapping di un dominio *specifico* , ad esempio **contoso.com** or **www.contoso.com**, a un nome di dominio canonico.</span><span class="sxs-lookup"><span data-stu-id="fd36e-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="fd36e-123">In questo caso, il nome di dominio canonico è il nome di dominio **[myapp].cloudapp.net** dell'applicazione ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd36e-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="fd36e-124">Dopo la creazione, il record CNAME crea a sua volta un alias per **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="fd36e-125">La voce CNAME viene risolta nell'indirizzo IP del servizio **[myapp].cloudapp.net** in modo automatico, pertanto se l'indirizzo IP del servizio cloud cambia non sarà necessaria alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="fd36e-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="fd36e-126">Alcuni registrar consentono di eseguire il mapping solo dei sottodomini se si usa un record CNAME, ad esempio www.contoso.com, e non dei nomi radice come contoso.com. Per altre informazioni sui record CNAME, vedere la documentazione fornita dal registrar, la [voce di Wikipedia sui record CNAME](http://en.wikipedia.org/wiki/CNAME_record) oppure il documento di IETF relativo a [implementazione e specifiche dei nomi di dominio](http://tools.ietf.org/html/rfc1035).</span><span class="sxs-lookup"><span data-stu-id="fd36e-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="fd36e-127">Record A</span><span class="sxs-lookup"><span data-stu-id="fd36e-127">A record</span></span>
<span data-ttu-id="fd36e-128">Un record *A* consente di eseguire il mapping di un dominio, ad esempio **contoso.com** o **www.contoso.com**, *o di un dominio con caratteri jolly*, ad esempio **\*.contoso.com**, a un indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="fd36e-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="fd36e-129">Nel caso di un servizio cloud di Azure, si tratta dell'IP virtuale del servizio.</span><span class="sxs-lookup"><span data-stu-id="fd36e-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="fd36e-130">Il principale vantaggio di un record A rispetto a un record CNAME consiste quindi nel fatto che un'unica voce con un carattere jolly, ad esempio \***.contoso.com**, gestirà le richieste per più sottodomini, ad esempio **mail.contoso.com**, **login.contoso.com** o **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="fd36e-131">Poiché il mapping di un record A viene eseguito a un indirizzo IP statico, il record non è in grado di risolvere automaticamente le modifiche all'indirizzo IP del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd36e-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="fd36e-132">L'indirizzo IP usato dal servizio cloud viene allocato la prima volta che si effettua una distribuzione in uno slot vuoto di produzione o di gestione temporanea. Se si elimina la distribuzione per lo slot, l'indirizzo IP viene rilasciato da Azure e le distribuzioni future in quello slot potrebbero ricevere un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="fd36e-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="fd36e-133">L'indirizzo IP di un determinato slot di distribuzione (di produzione o di gestione temporanea) viene reso permanente durante i passaggi tra distribuzioni di produzione e di gestione temporanea o durante l'esecuzione di aggiornamenti sul posto di distribuzioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="fd36e-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="fd36e-134">Per ulteriori informazioni sull'esecuzione di queste azioni, vedere [Come gestire i servizi cloud](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="fd36e-135">Aggiunta di un record CNAME per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="fd36e-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="fd36e-136">Per creare un record CNAME è necessario aggiungere una nuova voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar.</span><span class="sxs-lookup"><span data-stu-id="fd36e-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="fd36e-137">Sebbene i registrar utilizzino metodi simili per specificare un record CNAME, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.</span><span class="sxs-lookup"><span data-stu-id="fd36e-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="fd36e-138">Utilizzare uno dei metodi seguenti per trovare il nome di dominio **.cloudapp.net** assegnato al servizio cloud in questione.</span><span class="sxs-lookup"><span data-stu-id="fd36e-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="fd36e-139">Accedere al [portale di Azure], selezionare il servizio cloud, esaminare la sezione **Informazioni di base** e quindi individuare la voce **URL sito**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![Sezione quick glance in cui è visualizzato l'URL del sito][csurl]
     
       <span data-ttu-id="fd36e-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="fd36e-141">**OR**</span></span>
   * <span data-ttu-id="fd36e-142">Installare e configurare [Azure Powershell](/powershell/azure/overview), quindi eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fd36e-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="fd36e-143">Salvare il nome di dominio utilizzato nell'URL restituito da uno dei metodi, poiché sarà necessario per la creazione di un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="fd36e-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="fd36e-144">Accedere al sito Web del registrar DNS e passare alla pagina di gestione dei DNS.</span><span class="sxs-lookup"><span data-stu-id="fd36e-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="fd36e-145">Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="fd36e-146">Trovare la sezione in cui è possibile selezionare o immettere CNAME.</span><span class="sxs-lookup"><span data-stu-id="fd36e-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="fd36e-147">Può essere necessario selezionare un tipo di record in un elenco a discesa oppure passare a una pagina di impostazioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="fd36e-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="fd36e-148">Individuare i termini **CNAME**, **Alias** o **Subdomains** (Sottodomini).</span><span class="sxs-lookup"><span data-stu-id="fd36e-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="fd36e-149">È necessario fornire anche l'alias di dominio o sottodominio per CNAME, ad esempio **www**, se si vuole creare un alias per **www.customdomain.com**. Se si desidera creare un alias per il dominio radice, è possibile che sia elencato con il simbolo '**@**' negli strumenti DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="fd36e-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="fd36e-150">A questo punto, occorre fornire un nome host canonico, che in questo caso corrisponde al dominio **cloudapp.net** .</span><span class="sxs-lookup"><span data-stu-id="fd36e-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="fd36e-151">Il record CNAME seguente, ad esempio, inoltra tutto il traffico da **www.contoso.com** a **contoso.cloudapp.net**, che è il nome di dominio personalizzato dell'applicazione distribuita:</span><span class="sxs-lookup"><span data-stu-id="fd36e-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="fd36e-152">Alias/Nome host/Sottodominio</span><span class="sxs-lookup"><span data-stu-id="fd36e-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="fd36e-153">Dominio canonico</span><span class="sxs-lookup"><span data-stu-id="fd36e-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="fd36e-154">www</span><span class="sxs-lookup"><span data-stu-id="fd36e-154">www</span></span> |<span data-ttu-id="fd36e-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="fd36e-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="fd36e-156">A un visitatore di **www.contoso.com** non verrà mai visualizzato il nome dell'host reale (contoso.cloudapp.net), pertanto il processo di inoltro risulta totalmente invisibile all'utente finale.</span><span class="sxs-lookup"><span data-stu-id="fd36e-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="fd36e-157">L'esempio precedente si applica solo al sottodominio **www** .</span><span class="sxs-lookup"><span data-stu-id="fd36e-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="fd36e-158">Poiché non è possibile usare caratteri jolly con i record CNAME, è necessario crearne uno per ogni dominio/sottodominio.</span><span class="sxs-lookup"><span data-stu-id="fd36e-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="fd36e-159">Se si vuole indirizzare traffico da sottodomini, ad esempio *.contoso.com, all'indirizzo cloudapp.net in uso, è possibile configurare una voce di **reindirizzamento URL** o **inoltro URL** nelle impostazioni DNS oppure creare un record A.</span><span class="sxs-lookup"><span data-stu-id="fd36e-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="fd36e-160">Aggiungere un record A per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="fd36e-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="fd36e-161">Per creare un record A, è necessario innanzitutto trovare l'indirizzo IP virtuale del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd36e-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="fd36e-162">Si aggiunge quindi una voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar.</span><span class="sxs-lookup"><span data-stu-id="fd36e-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="fd36e-163">Sebbene i registrar utilizzino metodi simili per specificare un record A, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.</span><span class="sxs-lookup"><span data-stu-id="fd36e-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="fd36e-164">Utilizzare uno dei metodi seguenti per ottenere l'indirizzo IP del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd36e-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="fd36e-165">Accedere al [portale di Azure], selezionare il servizio cloud, esaminare la sezione **Informazioni di base** e quindi individuare la voce **Indirizzi IP pubblici**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![Sezione quick glance in cui è visualizzato l'indirizzo VIP][vip]
     
       <span data-ttu-id="fd36e-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="fd36e-167">**OR**</span></span>
   * <span data-ttu-id="fd36e-168">Installare e configurare [Azure Powershell](/powershell/azure/overview), quindi eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fd36e-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="fd36e-169">Salvare l'indirizzo IP, poiché sarà necessario per la creazione di un record A.</span><span class="sxs-lookup"><span data-stu-id="fd36e-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="fd36e-170">Accedere al sito Web del registrar DNS e passare alla pagina di gestione dei DNS.</span><span class="sxs-lookup"><span data-stu-id="fd36e-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="fd36e-171">Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="fd36e-172">Trovare la sezione in cui è possibile selezionare o immettere i record A.</span><span class="sxs-lookup"><span data-stu-id="fd36e-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="fd36e-173">Può essere necessario selezionare un tipo di record in un elenco a discesa oppure passare a una pagina di impostazioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="fd36e-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="fd36e-174">Selezionare o immettere il dominio o sottodominio che utilizzerà il record A.</span><span class="sxs-lookup"><span data-stu-id="fd36e-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="fd36e-175">Selezionare ad esempio **www** se si vuole creare un alias per **www.customdomain.com**. Se si vuole creare una voce con caratteri jolly per tutti i sottodomini, immettere '*****'.</span><span class="sxs-lookup"><span data-stu-id="fd36e-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="fd36e-176">In questo modo verranno inclusi tutti i sottodomini, ad esempio **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="fd36e-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="fd36e-177">Se si desidera creare un record A per il dominio radice, è possibile che sia elencato con il simbolo '**@**' negli strumenti DNS del registrar.</span><span class="sxs-lookup"><span data-stu-id="fd36e-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="fd36e-178">Immettere l'indirizzo IP del servizio cloud nell'apposito campo.</span><span class="sxs-lookup"><span data-stu-id="fd36e-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="fd36e-179">La voce del dominio usata nel record A verrà associata all'indirizzo IP della distribuzione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd36e-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="fd36e-180">Il record A seguente, ad esempio, inoltra tutto il traffico da **contoso.com** a **137.135.70.239**, che è l'indirizzo IP dell'applicazione distribuita:</span><span class="sxs-lookup"><span data-stu-id="fd36e-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="fd36e-181">Nome host/Sottodominio</span><span class="sxs-lookup"><span data-stu-id="fd36e-181">Host name/Subdomain</span></span> | <span data-ttu-id="fd36e-182">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="fd36e-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="fd36e-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="fd36e-183">137.135.70.239</span></span> |

<span data-ttu-id="fd36e-184">In questo esempio viene illustrata la creazione di un record A per il dominio radice.</span><span class="sxs-lookup"><span data-stu-id="fd36e-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="fd36e-185">Se si vuole creare una voce con caratteri jolly per tutti i sottodomini, immettere '*****' come sottodominio.</span><span class="sxs-lookup"><span data-stu-id="fd36e-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="fd36e-186">Gli indirizzi IP in Azure sono dinamici per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fd36e-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="fd36e-187">È possibile utilizzare un [indirizzo IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) per garantire che l'indirizzo IP non venga modificato.</span><span class="sxs-lookup"><span data-stu-id="fd36e-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fd36e-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd36e-188">Next steps</span></span>
* [<span data-ttu-id="fd36e-189">Come gestire i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="fd36e-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="fd36e-190">Come eseguire il mapping del contenuto della rete CDN a un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="fd36e-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="fd36e-191">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="fd36e-192">Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="fd36e-193">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd36e-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portale di Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
