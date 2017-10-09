---
title: aaaFind out quando un utente specifico saranno in grado di tooaccess un'applicazione | Documenti Microsoft
description: Come toofind out quando un utente di estremamente importante essere in grado di tooaccess un'applicazione sono stati configurati per il provisioning utente con Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="4a189-103">Sapere quando un utente specifico sarà in grado di tooaccess un'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a189-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="4a189-104">Quando si usa il provisioning utenti automatico con un'applicazione, Azure AD esegue automaticamente il provisioning e aggiorna gli account utente in un'app in base ad alcuni elementi, ad esempio l'[assegnazione di utenti e gruppi](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), a intervalli regolari pianificati, in genere ogni 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="4a189-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="4a189-105">Quanto tempo occorre?</span><span class="sxs-lookup"><span data-stu-id="4a189-105">How long does it take?</span></span>

<span data-ttu-id="4a189-106">Hello tempo richiesto per toobe un determinato utente provisioning dipende principalmente dal è già stata eseguita o meno una sincronizzazione iniziale "full".</span><span class="sxs-lookup"><span data-stu-id="4a189-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="4a189-107">Hello prima sincronizzazione tra Azure AD e un'app può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello di hello Azure Active directory e il numero di hello degli utenti in ambito per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="4a189-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="4a189-108">Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello risultare più veloce (ad esempio all'interno di 10 minuti), come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale hello, migliorando le prestazioni di sincronizzazioni successive.</span><span class="sxs-lookup"><span data-stu-id="4a189-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="4a189-109">Come toocheck hello lo stato di un utente</span><span class="sxs-lookup"><span data-stu-id="4a189-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="4a189-110">stato di provisioning hello toosee per un utente selezionato, consultare hello i log di controllo di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a189-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="4a189-111">Hello provisioning i log di controllo sono accessibili nel portale di Azure in hello hello **Azure Active Directory &gt; le app aziendali &gt; \[nome applicazione\] &gt; log di controllo**scheda. Hello filtro accede hello **Provisioning Account** tooonly categoria vedere hello provisioning gli eventi per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a189-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="4a189-112">È possibile cercare utenti basati su hello "corrispondenti all'ID" che è stato configurato per tali mapping degli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="4a189-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="4a189-113">Ad esempio, se è stato configurato hello "nome dell'entità utente" o "indirizzo di posta elettronica" come hello corrispondenti all'attributo sul lato di hello Azure AD, e non da il provisioning degli utenti hello ha un valore di "audrey@contoso.com", quindi di log di controllo di hello ricerca per"audrey@contoso.com" e quindi esaminare le voci restituite.</span><span class="sxs-lookup"><span data-stu-id="4a189-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="4a189-114">Hello provisioning controllo Registra record tutti hello le operazioni eseguite da hello provisioning del servizio, tra cui:</span><span class="sxs-lookup"><span data-stu-id="4a189-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="4a189-115">Esecuzione in Azure AD di query sugli utenti assegnati che rientrano nell'ambito del provisioning</span><span class="sxs-lookup"><span data-stu-id="4a189-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="4a189-116">Applicazione di destinazione hello esistenza hello di tali utenti l'esecuzione di query</span><span class="sxs-lookup"><span data-stu-id="4a189-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="4a189-117">Confronto di oggetti utente hello tra sistema hello</span><span class="sxs-lookup"><span data-stu-id="4a189-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="4a189-118">Aggiunta, aggiornamento o la disattivazione di account utente di hello nel sistema di destinazione hello in base a confronto hello</span><span class="sxs-lookup"><span data-stu-id="4a189-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a189-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a189-119">Next steps</span></span>
<span data-ttu-id="4a189-120">[Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'</span><span class="sxs-lookup"><span data-stu-id="4a189-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
