---
title: Notifiche relative al provisioning dell'account | Documentazione Microsoft
description: Come assicurarsi di ricevere notifiche relative ai problemi di provisioning utente che richiedono l'attenzione dell'utente abilitando le notifiche di provisioning dell'account.
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
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="8dd04-103">Notifiche relative al provisioning dell'account</span><span class="sxs-lookup"><span data-stu-id="8dd04-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="8dd04-104">Con il provisioning utente, è possibile automatizzare il processo di gestione degli utenti nelle applicazioni SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8dd04-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="8dd04-105">Anche se si tratta di un processo automatizzato, l'interazione con questo processo è richiesta di tanto in tanto.</span><span class="sxs-lookup"><span data-stu-id="8dd04-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="8dd04-106">È il caso, ad esempio, quando scade la password dell'account configurato per lo scambio dei dati con un'applicazione SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8dd04-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="8dd04-107">Abilitando le notifiche di provisioning dell'account è possibile assicurarsi di ricevere notifiche relative ai problemi di provisioning utente che richiedono l'attenzione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8dd04-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="8dd04-108">È possibile attivare o disattivare le notifiche di provisioning dell'account come parte della configurazione del provisioning utenti per un'applicazione SaaS di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8dd04-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Provisioning utente][1] 

<span data-ttu-id="8dd04-110">Per attivare le notifiche di provisioning dell'account, selezionare la casella di controllo relativa nella finestra di dialogo **Conferma** e quindi digitare l'alias di posta elettronica del destinatario.</span><span class="sxs-lookup"><span data-stu-id="8dd04-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Notifiche relative al provisioning dell'account][2]

<span data-ttu-id="8dd04-112">È possibile immettere un elenco di distribuzione come destinatario; tuttavia, è importante notare che l'e-mail di notifica contiene collegamenti ai report che sono accessibili solo agli amministratori di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dd04-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="8dd04-113">Se sono state abilitate le notifiche di provisioning dell'account si riceveranno e-mail riguardo problemi di importanza critica correlati al provisioning utente.</span><span class="sxs-lookup"><span data-stu-id="8dd04-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="8dd04-114">Tuttavia, per evitare un sovraccarico di posta elettronica, si riceverà un solo messaggio di notifica al giorno per ogni applicazione SaaS per cui sono abilitate le notifiche.</span><span class="sxs-lookup"><span data-stu-id="8dd04-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="8dd04-115">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="8dd04-115">Related Articles</span></span>
* [<span data-ttu-id="8dd04-116">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dd04-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8dd04-117">Automatizzare il provisioning e il deprovisioning utenti in app SaaS</span><span class="sxs-lookup"><span data-stu-id="8dd04-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="8dd04-118">Personalizzazione dei mapping degli attributi per il Provisioning dell’utente</span><span class="sxs-lookup"><span data-stu-id="8dd04-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="8dd04-119">Scrittura di espressioni per i mapping degli attributi</span><span class="sxs-lookup"><span data-stu-id="8dd04-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="8dd04-120">Ambito dei filtri per il Provisioning utente</span><span class="sxs-lookup"><span data-stu-id="8dd04-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="8dd04-121">Uso di SCIM per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="8dd04-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="8dd04-122">Elenco di esercitazioni pratiche sulla procedura di integrazione delle applicazioni SaaS</span><span class="sxs-lookup"><span data-stu-id="8dd04-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
