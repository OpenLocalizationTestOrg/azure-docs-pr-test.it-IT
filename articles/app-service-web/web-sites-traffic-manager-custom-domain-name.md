---
title: Configurare un nome di dominio personalizzato per un'app Web nel servizio app di Azure che usa Gestione traffico per il bilanciamento del carico.
description: Usare un nome di dominio personalizzato per un'app Web nel servizio app di Azure che usa Gestione traffico per il bilanciamento del carico.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="10fd8-103">Configurazione di un nome di dominio personalizzato per un'app Web nel servizio app di Azure con Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="10fd8-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="10fd8-104">Questo articolo fornisce istruzioni generiche sull'uso di un nome di dominio personalizzato con il servizio app di Azure in cui viene usato Gestione traffico per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="10fd8-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="10fd8-105">Informazioni sui record DNS</span><span class="sxs-lookup"><span data-stu-id="10fd8-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="10fd8-106">Configurare le app Web per la modalità standard</span><span class="sxs-lookup"><span data-stu-id="10fd8-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="10fd8-107">Aggiunta di un record DNS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="10fd8-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="10fd8-108">Se si è acquistato un dominio tramite App Web del servizio app di Azure, ignorare i passaggi seguenti e fare riferimento all'ultimo passaggio dell'articolo [Acquistare un dominio per app Web](custom-dns-web-site-buydomains-web-app.md) .</span><span class="sxs-lookup"><span data-stu-id="10fd8-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="10fd8-109">Per associare il dominio personalizzato a un'app Web nel servizio app di Azure, è necessario aggiungere nella tabella DNS una nuova voce per il dominio personalizzato usando gli strumenti forniti dal registrar da cui è stato acquistato il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="10fd8-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="10fd8-110">Per individuare e utilizzare gli strumenti DNS, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="10fd8-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="10fd8-111">Accedere all'account presso il registrar e cercare la pagina in cui gestire i record DNS.</span><span class="sxs-lookup"><span data-stu-id="10fd8-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="10fd8-112">Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="10fd8-113">Un collegamento a questa pagina è spesso disponibile nelle informazioni dell'account, cercando una voce simile a **My domains**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="10fd8-114">Dopo aver trovato la pagina di gestione del nome di dominio, cercare un collegamento che consenta di modificare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="10fd8-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="10fd8-115">Questo collegamento può essere denominato **Zone file** o **DNS Records** oppure figurare come collegamento di configurazione in **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="10fd8-116">La pagina conterrà molto probabilmente alcuni record già creati, ad esempio una voce per associare '**@**' o '\*' a una pagina di registrazione semplice.</span><span class="sxs-lookup"><span data-stu-id="10fd8-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="10fd8-117">Può anche contenere record per sottodomini comuni, ad esempio **www**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="10fd8-118">Nella pagina saranno presenti voci per record **CNAME**oppure verrà visualizzato un elenco a discesa per selezionare il tipo di record.</span><span class="sxs-lookup"><span data-stu-id="10fd8-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="10fd8-119">È anche possibile che siano presenti voci per altri record, ad esempio **record A** e **record MX**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="10fd8-120">In alcuni casi, i record CNAME avranno una denominazione diversa, come ad esempio nel caso dei record **Alias**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="10fd8-121">La pagina conterrà inoltre campi che consentono di eseguire il **mapping** da un **nome host** o da un **nome di dominio** a un altro nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="10fd8-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="10fd8-122">Anche se le specifiche di ogni registrar possono variare, in genere viene eseguito il mapping *dal* nome di dominio personalizzato, ad esempio **contoso.com**, *al* nome di dominio di Gestione traffico (**contoso.trafficmanager.net**) usato per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="10fd8-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10fd8-123">In alternativa, se un record è già in uso ed è necessario associare le app in modalità preemptive, è possibile creare un altro record CNAME.</span><span class="sxs-lookup"><span data-stu-id="10fd8-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="10fd8-124">Ad esempio, per associare **www.contoso.com** all'app Web in modalità preemptive, creare un record CNAME da **awverify.www** a **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="10fd8-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="10fd8-125">Aggiungere quindi "www.contoso.com" all'app Web senza modificare il record CNAME "www".</span><span class="sxs-lookup"><span data-stu-id="10fd8-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="10fd8-126">Per altre informazioni, vedere [Creare record DNS per un'app Web in un dominio personalizzato][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="10fd8-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="10fd8-127">Dopo aver completato l'aggiunta o la modifica di record DNS presso il registrar, salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="10fd8-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="10fd8-128">Abilitare Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="10fd8-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="10fd8-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10fd8-129">Next steps</span></span>
<span data-ttu-id="10fd8-130">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="10fd8-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
