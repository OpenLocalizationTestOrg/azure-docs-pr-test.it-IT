---
title: i domini aaaCustom Proxy dell'applicazione Azure AD | Documenti Microsoft
description: "Gestire i domini personalizzati in Azure AD applicazione Proxy in modo tale URL hello per app hello è hello uguali indipendentemente dal fatto in cui gli utenti diritti di accesso."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="00252-103">Utilizzo di domini personalizzati nel Proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="00252-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="00252-104">Quando si pubblica un'applicazione tramite il Proxy di applicazione Azure Active Directory, si crea un URL esterno per il toowhen toogo utenti che lavorano in remoto.</span><span class="sxs-lookup"><span data-stu-id="00252-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="00252-105">Questo URL Ottiene dominio predefinito hello *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="00252-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="00252-106">Ad esempio, se è stato pubblicato un'app denominata spese per il tenant è denominato Contoso, quindi URL esterno hello sarebbe https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="00252-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="00252-107">Se si desidera toouse il nome di dominio, configurare un dominio personalizzato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="00252-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="00252-108">È consigliabile configurare domini personalizzati per le applicazioni ogni volta che è possibile.</span><span class="sxs-lookup"><span data-stu-id="00252-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="00252-109">Alcuni dei vantaggi di hello di domini personalizzati:</span><span class="sxs-lookup"><span data-stu-id="00252-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="00252-110">Gli utenti possono usare l'applicazione toohello con hello stesso URL, se si lavora all'interno o all'esterno della rete.</span><span class="sxs-lookup"><span data-stu-id="00252-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="00252-111">Se tutte le applicazioni hanno hello stesso URL interni ed esterni, i collegamenti in un'applicazione che puntano tooanother continuano toowork anche all'esterno delle rete aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="00252-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="00252-112">Si controllano la personalizzazione e creare URL hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="00252-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="00252-113">Configurare un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="00252-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="00252-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00252-114">Prerequisites</span></span>

<span data-ttu-id="00252-115">Prima di configurare un dominio personalizzato, assicurarsi di aver hello preparati requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="00252-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="00252-116">Oggetto [tooAzure Active Directory di aggiunta dominio verificato](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="00252-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="00252-117">Un certificato personalizzato per il dominio di hello, sotto forma di hello di un file PFX.</span><span class="sxs-lookup"><span data-stu-id="00252-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="00252-118">Un'app locale [pubblicata tramite il proxy di applicazione](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="00252-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="00252-119">Configurare il dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="00252-119">Configure your custom domain</span></span>

<span data-ttu-id="00252-120">Quando si dispone di questi tre requisiti pronti, seguire questi passaggi tooset il dominio personalizzato:</span><span class="sxs-lookup"><span data-stu-id="00252-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="00252-121">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00252-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00252-122">Passare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni** e scegliere l'applicazione hello desiderato toomanage.</span><span class="sxs-lookup"><span data-stu-id="00252-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="00252-123">Selezionare **Proxy dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="00252-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="00252-124">Nel campo URL esterno hello, utilizzare tooselect elenco a discesa di hello del dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="00252-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="00252-125">Se non viene visualizzato il dominio nell'elenco di hello, quindi non è stata verificata ancora.</span><span class="sxs-lookup"><span data-stu-id="00252-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="00252-126">Selezionare **Salva**</span><span class="sxs-lookup"><span data-stu-id="00252-126">Select **Save**</span></span>
5. <span data-ttu-id="00252-127">Hello **certificato** risulta abilitata campo che è stata disabilitata.</span><span class="sxs-lookup"><span data-stu-id="00252-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="00252-128">Selezionare questo campo.</span><span class="sxs-lookup"><span data-stu-id="00252-128">Select this field.</span></span> 

   ![Fare clic su un certificato tooupload](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="00252-130">Se è già caricato un certificato per questo dominio, il campo certificato hello Visualizza informazioni sul certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="00252-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="00252-131">Caricare un certificato PFX hello e immettere la password di hello per certificato hello.</span><span class="sxs-lookup"><span data-stu-id="00252-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="00252-132">Selezionare **salvare** toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="00252-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="00252-133">Aggiungere un [record DNS](../dns/dns-operations-recordsets-portal.md) che reindirizzamenti hello nuovo msappproxy.net dominio toohello URL esterno.</span><span class="sxs-lookup"><span data-stu-id="00252-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="00252-134">È sufficiente un certificato di tooupload per ogni dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="00252-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="00252-135">Dopo aver caricato un certificato, è possibile scegliere dominio personalizzato hello quando si pubblica una nuova app e dispone di configurazione aggiuntive di toodo ad eccezione dei record DNS hello.</span><span class="sxs-lookup"><span data-stu-id="00252-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="00252-136">Gestire i certificati</span><span class="sxs-lookup"><span data-stu-id="00252-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="00252-137">Formato del certificato</span><span class="sxs-lookup"><span data-stu-id="00252-137">Certificate format</span></span>
<span data-ttu-id="00252-138">Non vi è alcuna restrizione sui metodi di firma certificato hello.</span><span class="sxs-lookup"><span data-stu-id="00252-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="00252-139">Sono supportati certificati ECC (Curve Cryptography), SAN (Subject Alternative Name) e altri tipi comuni di certificato.</span><span class="sxs-lookup"><span data-stu-id="00252-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="00252-140">È possibile utilizzare un certificato con caratteri jolly come carattere jolly hello corrisponde hello desiderato di URL esterno.</span><span class="sxs-lookup"><span data-stu-id="00252-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="00252-141">È anche possibile usare certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="00252-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="00252-142">Se si utilizza un'autorità di certificazione privata, hello CDP (punto di distribuzione punto revoca di certificato) per il certificato di hello debba essere pubblico.</span><span class="sxs-lookup"><span data-stu-id="00252-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="00252-143">Modificare il dominio hello</span><span class="sxs-lookup"><span data-stu-id="00252-143">Changing hello domain</span></span>
<span data-ttu-id="00252-144">Tutti i domini verificati vengono visualizzati nell'elenco a discesa URL esterno di hello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="00252-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="00252-145">toochange hello dominio solo aggiornamento tale campo per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00252-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="00252-146">Se non è il dominio hello desiderato nell'elenco di hello, [aggiungerlo come un dominio verificato](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="00252-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="00252-147">Se si seleziona un dominio che non dispone ancora di un certificato associato, seguire i certificati di hello tooadd passaggi da 5 a 7.</span><span class="sxs-lookup"><span data-stu-id="00252-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="00252-148">Quindi, assicurarsi di aggiornare hello tooredirect di record DNS da hello nuovo URL esterno.</span><span class="sxs-lookup"><span data-stu-id="00252-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="00252-149">Gestione dei certificati</span><span class="sxs-lookup"><span data-stu-id="00252-149">Certificate management</span></span>
<span data-ttu-id="00252-150">È possibile utilizzare hello che stesso certificato per più applicazioni, a meno che le applicazioni di hello condividono un host esterno.</span><span class="sxs-lookup"><span data-stu-id="00252-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="00252-151">Viene visualizzato un avviso quando un certificato scade, indicante che tooupload un altro certificato tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="00252-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="00252-152">Se hello certificato revocato, gli utenti possono vedere un avviso di sicurezza quando si accede a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00252-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="00252-153">Non vengono eseguiti controlli delle revoche dei certificati.</span><span class="sxs-lookup"><span data-stu-id="00252-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="00252-154">certificato hello tooupdate per una determinata applicazione, passare toohello applicazione e seguire i passaggi da 5 a 7 per la configurazione di domini personalizzati in tooupload applicazioni pubblicate un nuovo certificato.</span><span class="sxs-lookup"><span data-stu-id="00252-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="00252-155">Se il certificato precedente hello non utilizzato da altre applicazioni, viene eliminato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="00252-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="00252-156">Tutta la gestione dei certificati è attualmente attraverso pagine dell'applicazione singoli è sono necessari i certificati toomanage nel contesto di hello di applicazioni pertinente hello.</span><span class="sxs-lookup"><span data-stu-id="00252-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="00252-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00252-157">Next steps</span></span>
* <span data-ttu-id="00252-158">[Abilita single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour pubblicati App con autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00252-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="00252-159">[Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md) tooyour App pubblicate.</span><span class="sxs-lookup"><span data-stu-id="00252-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="00252-160">Aggiungere il tooAzure nome di dominio personalizzato AD</span><span class="sxs-lookup"><span data-stu-id="00252-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


