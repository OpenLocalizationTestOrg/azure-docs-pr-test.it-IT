---
title: aaaConfigure un nome di dominio personalizzato in Azure App Service (GoDaddy)
description: Informazioni su come assegnare un nome toouse un dominio di GoDaddy con le app Web di Azure
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="44727-103">Configurare un nome di dominio personalizzato nel servizio app di Azure (acquistato direttamente da GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="44727-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="44727-104">Se si hanno acquistato dominio tramite l'App Web di servizio App di Azure, vedere toohello passaggio finale della [acquistare dominio per le app Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="44727-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="44727-105">Questo articolo contiene istruzioni generiche sull'uso di un nome di dominio personalizzato acquistato direttamente da [GoDaddy](https://godaddy.com) con [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="44727-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="44727-106">Informazioni sui record DNS</span><span class="sxs-lookup"><span data-stu-id="44727-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="44727-107">Aggiunta di un record DNS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="44727-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="44727-108">tooassociate il dominio personalizzato con un'app web nel servizio App, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite gli strumenti forniti da GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="44727-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="44727-109">Utilizzare i seguenti strumenti DNS hello toolocate di passaggi per GoDaddy.com hello</span><span class="sxs-lookup"><span data-stu-id="44727-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="44727-110">Accesso account tooyour con GoDaddy.com e selezionare **Account personale** e quindi **Manage my domains**.</span><span class="sxs-lookup"><span data-stu-id="44727-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="44727-111">Menu di scelta rapida selezionare hello hello nome di dominio che si desidera toouse con l'app web di Azure e si seleziona **Manage DNS**.</span><span class="sxs-lookup"><span data-stu-id="44727-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![pagina del domino personalizzato per GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="44727-113">Da hello **i dettagli del dominio** pagina, scorrere toohello **File di zona DNS** scheda. Si tratta di sezione hello utilizzata per aggiungere e modificare i record DNS per il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="44727-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Scheda DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="44727-115">Selezionare **Aggiungi Record** tooadd un record esistente.</span><span class="sxs-lookup"><span data-stu-id="44727-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="44727-116">troppo**modifica** un record esistente, selezionare hello penna e carta accanto icona record hello.</span><span class="sxs-lookup"><span data-stu-id="44727-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="44727-117">Prima di aggiungere nuovi record, tenere presente che GoDaddy ha già creato i record DNS per i sottodomini più diffusi (denominati **Host** nell'editor), ad esempio **email**, **files**, **mail** e altri ancora.</span><span class="sxs-lookup"><span data-stu-id="44727-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="44727-118">Se nome hello desiderato toouse già esiste, modificare record di hello esistente anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="44727-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="44727-119">Quando si aggiunge un record, è necessario innanzitutto selezionare tipo di record di hello.</span><span class="sxs-lookup"><span data-stu-id="44727-119">When adding a record, you must first select hello record type.</span></span>
   
    ![select record type](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="44727-121">Successivamente, è necessario fornire hello **Host** (hello dominio personalizzato o sottodominio) e l'oggetto a cui **punta a**.</span><span class="sxs-lookup"><span data-stu-id="44727-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![add zone record](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="44727-123">Quando si aggiunge un **record (host)** -è necessario impostare hello **Host** campo tooeither  **@**  (rappresenta il nome di dominio radice, ad esempio  **Contoso.com**,) * (un carattere jolly per la corrispondenza più sottodomini,) o un sottodominio di hello desiderato toouse (ad esempio, **www**.) È necessario impostare hello **punta a** campo indirizzo IP toohello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="44727-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="44727-124">Quando si aggiunge un **record CNAME (alias)** -è necessario impostare hello **Host** sottodominio del toohello campo desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="44727-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="44727-125">ad esempio **www**.</span><span class="sxs-lookup"><span data-stu-id="44727-125">For example, **www**.</span></span> <span data-ttu-id="44727-126">È necessario impostare hello **punta a** campo toohello **. azurewebsites.net** nome di dominio dell'applicazione web di Azure.</span><span class="sxs-lookup"><span data-stu-id="44727-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="44727-127">Ad esempio, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="44727-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="44727-128">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="44727-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="44727-129">Selezionare **TXT** come tipo di record hello, quindi specificare un **Host** valore  **@**  e **punta a** valore  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="44727-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="44727-130">Questo record TXT viene usato da Azure toovalidate che si è proprietari di dominio hello descritto da hello un record TXT primo record o hello.</span><span class="sxs-lookup"><span data-stu-id="44727-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="44727-131">Dopo aver mappato toohello app web nel portale di Azure hello dominio hello, questa voce di record TXT può essere rimossi.</span><span class="sxs-lookup"><span data-stu-id="44727-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="44727-132">Quando si hanno completato l'aggiunta o la modifica di record, fare clic su **fine** toosave modifiche.</span><span class="sxs-lookup"><span data-stu-id="44727-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="44727-133">Abilitare il nome di dominio hello in app web</span><span class="sxs-lookup"><span data-stu-id="44727-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="44727-134">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="44727-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="44727-135">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="44727-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="44727-136">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="44727-136">What's changed</span></span>
* <span data-ttu-id="44727-137">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="44727-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

