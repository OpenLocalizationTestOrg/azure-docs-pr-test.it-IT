---
title: aaaConfigure un nome di dominio personalizzato per un'app web in Azure App Service che Usa gestione traffico per il bilanciamento del carico.
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
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="c08fd-103">Configurazione di un nome di dominio personalizzato per un'app Web nel servizio app di Azure con Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="c08fd-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="c08fd-104">Questo articolo fornisce istruzioni generiche sull'uso di un nome di dominio personalizzato con il servizio app di Azure in cui viene usato Gestione traffico per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="c08fd-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="c08fd-105">Informazioni sui record DNS</span><span class="sxs-lookup"><span data-stu-id="c08fd-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="c08fd-106">Configurare le app Web per la modalità standard</span><span class="sxs-lookup"><span data-stu-id="c08fd-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="c08fd-107">Aggiunta di un record DNS per il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="c08fd-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="c08fd-108">Se si hanno acquistato dominio tramite l'App Web di servizio App di Azure quindi passare alla procedura seguente fanno riferimento toohello passaggio finale della [acquistare dominio per le app Web](custom-dns-web-site-buydomains-web-app.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="c08fd-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="c08fd-109">tooassociate il dominio personalizzato con un'app web nel servizio App di Azure, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite gli strumenti forniti da hello registrar che è stato acquistato il nome del dominio.</span><span class="sxs-lookup"><span data-stu-id="c08fd-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="c08fd-110">Utilizzare i seguenti passaggi toolocate hello e utilizzare gli strumenti per DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c08fd-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="c08fd-111">Eseguire l'accesso account tooyour presso un registrar di dominio e cercare una pagina di gestione dei record DNS.</span><span class="sxs-lookup"><span data-stu-id="c08fd-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="c08fd-112">Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="c08fd-113">Spesso un collegamento toothis pagina sono disponibili da visualizzare le informazioni sull'account e quindi cercando, ad esempio un collegamento **My domains**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="c08fd-114">Dopo aver trovato la pagina di gestione hello del nome di dominio, cercare un collegamento che consente i record DNS di tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="c08fd-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="c08fd-115">Questo collegamento può essere denominato **Zone file** o **DNS Records** oppure figurare come collegamento di configurazione in **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="c08fd-116">pagina Hello più probabile che abbiano già creato, ad esempio un'associazione di voce di alcuni record '**@**'o'\*' con una pagina 'parcheggio dominio'.</span><span class="sxs-lookup"><span data-stu-id="c08fd-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="c08fd-117">Può anche contenere record per sottodomini comuni, ad esempio **www**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="c08fd-118">pagina Hello verrà menzionato **record CNAME**, o fornire un elenco a discesa tooselect un tipo di record.</span><span class="sxs-lookup"><span data-stu-id="c08fd-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="c08fd-119">È anche possibile che siano presenti voci per altri record, ad esempio **record A** e **record MX**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="c08fd-120">In alcuni casi, i record CNAME avranno una denominazione diversa, come ad esempio nel caso dei record **Alias**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="c08fd-121">pagina Hello disporrà di campi che consentono di troppo**mappa** da un **nome Host** o **nome di dominio** tooanother nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="c08fd-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="c08fd-122">Mentre specifiche hello di ogni registrar variano, in genere si esegue il mapping *da* nome di dominio personalizzato (ad esempio **contoso.com**,) *a* nome di dominio di Traffic Manager hello (**contoso.trafficmanager.net**) che viene utilizzato per l'app web.</span><span class="sxs-lookup"><span data-stu-id="c08fd-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c08fd-123">In alternativa, se un record è già in uso ed è necessario toopreemptively associare tooit l'App, è possibile creare un record CNAME aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="c08fd-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="c08fd-124">Ad esempio, l'associazione toopreemptively **www.contoso.com** tooyour app web, creare un record CNAME da **awverify.www** troppo**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="c08fd-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="c08fd-125">È quindi possibile aggiungere tooyour "www.contoso.com" App Web senza modificare i record CNAME di hello "www".</span><span class="sxs-lookup"><span data-stu-id="c08fd-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="c08fd-126">Per altre informazioni, vedere [Creare record DNS per un'app Web in un dominio personalizzato][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="c08fd-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="c08fd-127">Una volta completata l'aggiunta o la modifica di record DNS nel registrar, salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="c08fd-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="c08fd-128">Abilitare Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="c08fd-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="c08fd-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c08fd-129">Next steps</span></span>
<span data-ttu-id="c08fd-130">Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="c08fd-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
