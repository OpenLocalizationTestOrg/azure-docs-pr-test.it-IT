---
title: Configurazione di un nome di dominio personalizzato nel servizio app di Azure (GoDaddy)
description: Informazioni su come usare un nome di dominio di GoDaddy con le app Web di Azure
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="73373-103">Configurare un nome di dominio personalizzato nel servizio app di Azure (acquistato direttamente da GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="73373-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="73373-104">Se si è acquistato un dominio tramite App Web del servizio app di Azure, fare riferimento all'ultimo passaggio di [Acquistare un dominio per app Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="73373-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="73373-105">Questo articolo contiene istruzioni generiche sull'uso di un nome di dominio personalizzato acquistato direttamente da [GoDaddy](https://godaddy.com) con [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="73373-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="73373-106">Informazioni sui record DNS</span><span class="sxs-lookup"><span data-stu-id="73373-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="73373-107">Aggiunta di un record DNS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="73373-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="73373-108">Per associare il dominio personalizzato a un'app Web nel servizio app, è necessario aggiungere nella tabella DNS una nuova voce per il dominio personalizzato usando gli strumenti forniti da GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="73373-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="73373-109">Per individuare gli strumenti DNS per GoDaddy.com, attenersi alla procedura seguente</span><span class="sxs-lookup"><span data-stu-id="73373-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="73373-110">Accedere al proprio account presso GoDaddy.com e selezionare **Mio account**, quindi **Gestisci i miei domini**.</span><span class="sxs-lookup"><span data-stu-id="73373-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="73373-111">Selezionare il menu a discesa relativo al nome di dominio da usare con l'app Web di Azure e selezionare **Gestisci DNS**.</span><span class="sxs-lookup"><span data-stu-id="73373-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![pagina del domino personalizzato per GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="73373-113">Nella pagina **Dettagli dominio** selezionare la scheda **DNS Zone File**.</span><span class="sxs-lookup"><span data-stu-id="73373-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="73373-114">In questa sezione è possibile aggiungere e modificare i record DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="73373-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Scheda DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="73373-116">Selezionare **Aggiungi record** a un record esistente.</span><span class="sxs-lookup"><span data-stu-id="73373-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="73373-117">Per **modificare** un record esistente, selezionare l'icona della penna e del foglio accanto al record.</span><span class="sxs-lookup"><span data-stu-id="73373-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="73373-118">Prima di aggiungere nuovi record, tenere presente che GoDaddy ha già creato i record DNS per i sottodomini più diffusi (denominati **Host** nell'editor), ad esempio **email**, **files**, **mail** e altri ancora.</span><span class="sxs-lookup"><span data-stu-id="73373-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="73373-119">Se il nome che si desidera utilizzare è già presente, modificare il record esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="73373-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="73373-120">Per aggiungere un record, è necessario innanzitutto selezionare un tipo di record.</span><span class="sxs-lookup"><span data-stu-id="73373-120">When adding a record, you must first select the record type.</span></span>
   
    ![select record type](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="73373-122">Quindi, è necessario specificare l'**Host** (il dominio o il sottodominio personalizzato) e l'opzione **Points to**.</span><span class="sxs-lookup"><span data-stu-id="73373-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![add zone record](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="73373-124">Quando si aggiunge un **record A (host)**, è necessario impostare il campo **Host** su **@** (che rappresenta il nome di dominio radice, ad esempio **contoso.com**)* (un carattere jolly per la corrispondenza di più sottodomini) o sul sottodominio da usare (ad esempio **www**). È necessario impostare il campo **Points to** (Punta a) sull'indirizzo IP dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73373-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="73373-125">Quando si aggiunge un **record CNAME (alias)**, è necessario impostare il campo **Host** sul sottodominio da usare,</span><span class="sxs-lookup"><span data-stu-id="73373-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="73373-126">ad esempio **www**.</span><span class="sxs-lookup"><span data-stu-id="73373-126">For example, **www**.</span></span> <span data-ttu-id="73373-127">È necessario impostare il campo **Points to** (Punta a) sul nome di dominio **.azurewebsites.net** dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="73373-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="73373-128">Ad esempio, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="73373-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="73373-129">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="73373-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="73373-130">Selezionare **TXT** come tipo di record, quindi specificare un valore **Host** di **@** e un valore **Points to** (Punta a) di **&lt;nomeappweb&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="73373-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="73373-131">Questo record TXT viene usato da Azure per convalidare la proprietà del dominio descritto dal record A o il primo record TXT.</span><span class="sxs-lookup"><span data-stu-id="73373-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="73373-132">Una volta eseguito il mapping del dominio all'app Web nel portale di Azure, questa voce del record TXT può essere rimossa.</span><span class="sxs-lookup"><span data-stu-id="73373-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="73373-133">Dopo avere completato l'aggiunta o la modifica dei record, fare clic su **Fine** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="73373-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="73373-134">Abilitazione del nome del dominio nell'app Web</span><span class="sxs-lookup"><span data-stu-id="73373-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="73373-135">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="73373-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="73373-136">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="73373-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="73373-137">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="73373-137">What's changed</span></span>
* <span data-ttu-id="73373-138">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="73373-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

