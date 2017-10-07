---
title: aaaCustomize accesso pagina hello Azure Active Directory | Documenti Microsoft
description: Informazioni su come tooadd una pagina toohello Accedi Azure branding aziendale
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="da2f4-103">Aggiungere informazioni personalizzate distintive tooyour nella pagina di accesso in hello Azure Active Directory della società</span><span class="sxs-lookup"><span data-stu-id="da2f4-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="da2f4-104">tooavoid confusione, molte società desidera tooapply un aspetto coerente in tutti i siti Web di hello e i servizi gestiti.</span><span class="sxs-lookup"><span data-stu-id="da2f4-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="da2f4-105">Azure Active Directory fornisce questa funzionalità, consentendo l'aspetto di hello toocustomize di hello nella pagina di accesso con il logo della società e combinazioni di colori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="da2f4-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="da2f4-106">pagina di accesso Hello è hello pagina viene visualizzata quando si accede tooOffice 365 o altre applicazioni basate su web che usano Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="da2f4-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="da2f4-107">Si interagiscono con tooenter questa pagina delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="da2f4-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="da2f4-108">Se si desidera tooshow il marchio dell'azienda, colori e altri elementi personalizzabili in questa pagina, vedere hello seguenti immagini toounderstand hello differenza due esperienze hello.</span><span class="sxs-lookup"><span data-stu-id="da2f4-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="da2f4-109">Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **prima** una personalizzazione:</span><span class="sxs-lookup"><span data-stu-id="da2f4-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Pagina di accesso di Office 365 prima della personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="da2f4-111">Hello illustrato nella schermata e di esempio per Office 365 hello nella pagina di accesso in un computer desktop seguenti **dopo** una personalizzazione:</span><span class="sxs-lookup"><span data-stu-id="da2f4-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Pagina di accesso di Office 365 dopo la personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="da2f4-113">Personalizzazione pagina di accesso hello</span><span class="sxs-lookup"><span data-stu-id="da2f4-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="da2f4-114">In genere, se è necessario l'accesso basato su browser tooyour cloud App e servizi sottoscritti dall'organizzazione, utilizzare hello nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="da2f4-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="da2f4-115">Se è stato applicato le modifiche tooyour nella pagina di accesso, può richiedere tooan orari per tooappear modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="da2f4-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="da2f4-116">Una pagina di accesso personalizzata viene visualizzata solo quando si visita un servizio con un URL specifico del tenant, ad esempio https://outlook.com/**contoso**.com o https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="da2f4-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="da2f4-117">Quando si visita un servizio con URL non specifici del tenant (ad esempio, https://mail.office365.com), viene visualizzata una pagina di accesso non personalizzata.</span><span class="sxs-lookup"><span data-stu-id="da2f4-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="da2f4-118">In questo caso, la personalizzazione viene visualizzata dopo avere immesso il proprio ID utente o avere selezionato un riquadro utente.</span><span class="sxs-lookup"><span data-stu-id="da2f4-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="da2f4-119">Il nome di dominio deve risultare "Attivo" nella hello **domini** hello di parte del portale di Azure in cui è stata configurata la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="da2f4-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="da2f4-120">Per altre informazioni, vedere l'argomento relativo all' [aggiunta di nomi di dominio personalizzati](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="da2f4-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="da2f4-121">Personalizzazione pagina di accesso non si estende su toohello consumer firmare nella pagina di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da2f4-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="da2f4-122">Se si accede con un account Microsoft, si potrebbe visualizzare un elenco personalizzato di sezioni utente sottoposto a rendering da Azure AD, ma hello personalizzazione dell'organizzazione non è applicabile toohello Microsoft account-pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="da2f4-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="da2f4-123">Nella pagina accesso hello **Mantieni l'accesso** casella di controllo permette tooremain un utente connesso quando viene chiuso e riaprire il browser.</span><span class="sxs-lookup"><span data-stu-id="da2f4-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="da2f4-125">Non influisce sulla durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="da2f4-125">It does not effect session lifetime.</span></span> <span data-ttu-id="da2f4-126">È possibile nascondere una casella di controllo hello hello Azure Active Directory nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="da2f4-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="da2f4-127">Se non viene visualizzata la casella hello dipende dall'impostazione di hello di **Mantieni l'accesso disabilitato**.</span><span class="sxs-lookup"><span data-stu-id="da2f4-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="da2f4-129">toohide hello casella di controllo, configurare questa impostazione troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="da2f4-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="da2f4-130">Alcune funzionalità di SharePoint Online e Office 2010 dipendono dagli utenti in grado di toocheck questa casella.</span><span class="sxs-lookup"><span data-stu-id="da2f4-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="da2f4-131">Se si configura questa impostazione toohidden, gli utenti potrebbero notare aggiuntive e impreviste prompt toosign-in.</span><span class="sxs-lookup"><span data-stu-id="da2f4-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="da2f4-132">**directory tooadd aziendale personalizzazione tooyour:**</span><span class="sxs-lookup"><span data-stu-id="da2f4-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="da2f4-133">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="da2f4-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="da2f4-134">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="da2f4-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="da2f4-136">In hello **utenti e gruppi** pannello seleziona **personalizzazione specifica della società**.</span><span class="sxs-lookup"><span data-stu-id="da2f4-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="da2f4-137">In hello **utenti e gruppi - personalizzazione specifica della società** blade, seleziona hello **modifica** comando.</span><span class="sxs-lookup"><span data-stu-id="da2f4-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Modificare le informazioni personalizzate](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="da2f4-139">Modificare gli elementi di hello desiderati toocustomize.</span><span class="sxs-lookup"><span data-stu-id="da2f4-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="da2f4-140">Tutti gli elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="da2f4-140">All elements are optional.</span></span>
6. <span data-ttu-id="da2f4-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="da2f4-141">Click **Save**.</span></span>

<span data-ttu-id="da2f4-142">Potrebbe essere necessaria fino tooan ora per tutte le modifiche apportate toohello Accedi pagina tooappear personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="da2f4-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da2f4-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da2f4-143">Next steps</span></span>
[<span data-ttu-id="da2f4-144">Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua</span><span class="sxs-lookup"><span data-stu-id="da2f4-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
