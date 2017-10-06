---
title: le notifiche di provisioning aaaAccount | Documenti Microsoft
description: Informazioni su come tooensure la notifica dei problemi correlati toouser provisioning che richiedono attenzione abilitando le notifiche di provisioning dell'account.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="b1a9e-103">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="b1a9e-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="b1a9e-104">Con il provisioning utente, è possibile automatizzare il processo di hello di gestione degli utenti nelle applicazioni SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-104">With user provisioning, you can automate hello process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="b1a9e-105">Si tratta di un processo automatizzato, l'interazione con questo processo è da tootime tempo richiesto.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-105">While this is an automated process, your interaction with this process is from time tootime required.</span></span> <br>
<span data-ttu-id="b1a9e-106">Questo accade, ad esempio hello, quando password hello dell'account hello configurato tooexchange dati con un terzo di terze parti SaaS applicazione è scaduta.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-106">This is, for example hello case, when hello password of hello account you have configured tooexchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="b1a9e-107">Abilitando le notifiche di provisioning dell'account, è possibile garantire la notifica di problemi correlati toouser provisioning che richiedono attenzione.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related toouser provisioning that require your attention.</span></span>

<span data-ttu-id="b1a9e-108">È possibile attivare o disattivare le notifiche di provisioning dell'account come parte della configurazione del provisioning utenti per un'applicazione SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Provisioning utente][1] 

<span data-ttu-id="b1a9e-110">le notifiche di provisioning dell'account tooactivate, selezionare hello casella di controllo correlato hello **conferma** nella pagina e alias del tipo di messaggio di posta elettronica hello del destinatario hello.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-110">tooactivate account provisioning notifications, select hello related checkbox on hello **Confirmation** dialog page, and then type hello email alias of hello recipient.</span></span>

![Notifiche relative al provisioning dell'account][2]

<span data-ttu-id="b1a9e-112">È possibile immettere una lista di distribuzione come destinatario. Tuttavia, è importante toonote che posta elettronica di notifica hello contiene collegamenti tooreports che accessibili solo dagli amministratori di hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-112">You can enter a distribution list as recipient; however, it is important toonote that hello notification email contains links tooreports that are only accessible by hello Azure AD administrators.</span></span>

<span data-ttu-id="b1a9e-113">Se sono abilitate le notifiche di provisioning dell'account si riceveranno e-mail riguardo problemi critici che sono correlati toouser provisioning.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related toouser provisioning.</span></span> <span data-ttu-id="b1a9e-114">Tuttavia, tooavoid un sovraccarico di posta elettronica, è solo riceverà una notifica tramite posta elettronica al giorno per ogni SaaS applicazione hello notifica tramite posta elettronica è abilitata per.</span><span class="sxs-lookup"><span data-stu-id="b1a9e-114">However, tooavoid an email overload, you will only receive one notification email per day for each SaaS application hello notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b1a9e-115">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="b1a9e-115">Related Articles</span></span>
* [<span data-ttu-id="b1a9e-116">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1a9e-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b1a9e-117">Automatizzare tooSaaS utente Provisioning o Deprovisioning App</span><span class="sxs-lookup"><span data-stu-id="b1a9e-117">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="b1a9e-118">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="b1a9e-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="b1a9e-119">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="b1a9e-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="b1a9e-120">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="b1a9e-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="b1a9e-121">Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="b1a9e-121">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="b1a9e-122">Elenco di esercitazioni sulla tooIntegrate App SaaS</span><span class="sxs-lookup"><span data-stu-id="b1a9e-122">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
