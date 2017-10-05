---
title: Personalizzare la pagina di accesso in Azure Active Directory | Microsoft Docs
description: Informazioni su come aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso di Azure
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="c6c62-103">Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6c62-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="c6c62-104">Per evitare confusione, molte aziende vogliono applicare un aspetto coerente a tutti i siti Web e servizi che gestiscono.</span><span class="sxs-lookup"><span data-stu-id="c6c62-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="c6c62-105">Azure Active Directory offre questa funzionalità consentendo di personalizzare l'aspetto delle pagine di accesso, in modo da includere il logo e le combinazioni di colori personalizzate dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="c6c62-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c6c62-106">La pagina di accesso è la pagina visualizzata quando si accede a Office 365 o ad altre applicazioni basate sul Web che usano Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c6c62-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c6c62-107">Interagire con questa pagina per immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="c6c62-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="c6c62-108">Se si vuole mostrare il marchio, i colori e altri elementi personalizzabili dell'azienda in questa pagina, vedere le immagini seguenti per capire la differenza tra le due esperienze.</span><span class="sxs-lookup"><span data-stu-id="c6c62-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="c6c62-109">Lo screenshot seguente mostra un esempio della pagina di accesso di Office 365 in un computer desktop **prima** di una personalizzazione:</span><span class="sxs-lookup"><span data-stu-id="c6c62-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Pagina di accesso di Office 365 prima della personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="c6c62-111">Lo screenshot seguente mostra un esempio della pagina di accesso di Office 365 in un computer desktop **dopo** una personalizzazione:</span><span class="sxs-lookup"><span data-stu-id="c6c62-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Pagina di accesso di Office 365 dopo la personalizzazione](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="c6c62-113">Personalizzazione della pagina di accesso</span><span class="sxs-lookup"><span data-stu-id="c6c62-113">Customizing the sign-in page</span></span>
<span data-ttu-id="c6c62-114">Di solito si usa la pagina di accesso se è necessario accedere con un browser alle app e ai servizi cloud sottoscritti dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c6c62-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="c6c62-115">Se sono state apportate modifiche alla pagina di accesso, potrebbe trascorrere fino a un'ora prima che le modifiche vengano visualizzate.</span><span class="sxs-lookup"><span data-stu-id="c6c62-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="c6c62-116">Una pagina di accesso personalizzata viene visualizzata solo quando si visita un servizio con un URL specifico del tenant, ad esempio https://outlook.com/**contoso**.com o https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="c6c62-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="c6c62-117">Quando si visita un servizio con URL non specifici del tenant (ad esempio, https://mail.office365.com), viene visualizzata una pagina di accesso non personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c6c62-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="c6c62-118">In questo caso, la personalizzazione viene visualizzata dopo avere immesso il proprio ID utente o avere selezionato un riquadro utente.</span><span class="sxs-lookup"><span data-stu-id="c6c62-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="c6c62-119">Il nome di dominio deve essere visualizzato come "Attivo" nella sezione **Domini** del portale di Azure in cui è stata configurata la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="c6c62-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="c6c62-120">Per altre informazioni, vedere l'argomento relativo all' [aggiunta di nomi di dominio personalizzati](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6c62-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="c6c62-121">La personalizzazione della pagina di accesso non si applica alla pagina di accesso degli utenti di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6c62-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="c6c62-122">Se si accede con un account Microsoft, potrebbe essere visualizzato un elenco personalizzato di riquadri utente reso disponibile da Azure AD, ma le informazioni di personalizzazione dell'organizzazione non vengono applicate alla pagina di accesso degli account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6c62-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="c6c62-123">Nella pagina di accesso, la casella di controllo **Mantieni l'accesso** consente a un utente di rimanere connesso quando chiude e riapre il browser.</span><span class="sxs-lookup"><span data-stu-id="c6c62-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="c6c62-125">Non influisce sulla durata della sessione.</span><span class="sxs-lookup"><span data-stu-id="c6c62-125">It does not effect session lifetime.</span></span> <span data-ttu-id="c6c62-126">È possibile nascondere la casella di controllo nella pagina di accesso di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6c62-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="c6c62-127">La visualizzazione della casella di controllo dipende dall'impostazione dell'opzione **Mantieni l'accesso disabilitato**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Mantieni l'accesso](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="c6c62-129">Per nascondere la casella di controllo, impostare questa opzione su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c62-130">Alcune funzionalità di SharePoint Online e di Office 2010 dipendono dalla possibilità per gli utenti di selezionare questa casella.</span><span class="sxs-lookup"><span data-stu-id="c6c62-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="c6c62-131">Se si configura questa impostazione come nascosta, gli utenti potrebbero visualizzare prompt aggiuntivi e imprevisti con una richiesta di accesso.</span><span class="sxs-lookup"><span data-stu-id="c6c62-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="c6c62-132">**Per aggiungere informazioni personalizzate distintive dell'azienda alla directory:**</span><span class="sxs-lookup"><span data-stu-id="c6c62-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="c6c62-133">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="c6c62-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c6c62-134">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="c6c62-136">Nel pannello **Utenti e gruppi** selezionare **Informazioni personalizzate distintive dell'azienda**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c6c62-137">Nel pannello **Utenti e gruppi - Informazioni personalizzate distintive dell'azienda** selezionare il comando **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Modificare le informazioni personalizzate](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="c6c62-139">Modificare gli elementi da personalizzare.</span><span class="sxs-lookup"><span data-stu-id="c6c62-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="c6c62-140">Tutti gli elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="c6c62-140">All elements are optional.</span></span>
6. <span data-ttu-id="c6c62-141">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c6c62-141">Click **Save**.</span></span>

<span data-ttu-id="c6c62-142">Può trascorrere fino a un'ora prima che qualsiasi modifica apportata per la personalizzazione della pagina di accesso venga visualizzata.</span><span class="sxs-lookup"><span data-stu-id="c6c62-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6c62-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6c62-143">Next steps</span></span>
[<span data-ttu-id="c6c62-144">Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua</span><span class="sxs-lookup"><span data-stu-id="c6c62-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
