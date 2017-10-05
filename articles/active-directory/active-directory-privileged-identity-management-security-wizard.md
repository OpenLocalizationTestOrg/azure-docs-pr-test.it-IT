---
title: Procedura guidata relativa alla sicurezza di Azure AD Privileged Identity Management
description: Quando si usa l'estensione Azure Active Directory Privileged Identity Management per la prima volta, viene visualizzata una procedura guidata sulla sicurezza. Questo articolo descrive i passaggi della procedura guidata.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="7cf9a-104">Uso della procedura guidata relativa alla sicurezza di Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="7cf9a-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="7cf9a-105">Se si è il primo utente a eseguire Azure Privileged Identity Management (PIM) per l'organizzazione, viene visualizzata una procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="7cf9a-106">La procedura guidata offre informazioni sui rischi di sicurezza delle identità con privilegi e su come usare PIM per ridurre tali rischi.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="7cf9a-107">Se si vuole farlo in seguito, non è necessario apportare modifiche alle assegnazioni dei ruoli esistenti nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="7cf9a-108">Cosa aspettarsi</span><span class="sxs-lookup"><span data-stu-id="7cf9a-108">What to expect</span></span>
<span data-ttu-id="7cf9a-109">Prima che l'organizzazione inizi a usare PIM, tutte le assegnazioni dei ruoli sono permanenti, ovvero gli utenti sono sempre presenti nei ruoli anche se in quel momento non necessitano dei privilegi del ruolo.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="7cf9a-110">Il primo passaggio della procedura guidata visualizza un elenco dei ruoli con privilegi elevati e il numero di utenti attualmente presenti in tali ruoli.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="7cf9a-111">È possibile visualizzare i dettagli di un ruolo particolare per visualizzare altre informazioni sugli utenti nel caso in cui uno o più utenti non siano noti.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="7cf9a-112">Il secondo passaggio della procedura guidata offre la possibilità di modificare le assegnazioni dei ruoli di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="7cf9a-113">È importante che siano presenti almeno un amministratore globale e più amministratori dei ruoli con privilegi con account aziendali e non account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="7cf9a-114">Se è presente un solo amministratore dei ruoli con privilegi, l'organizzazione non sarà in grado di gestire PIM se tale account viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="7cf9a-115">Mantenere inoltre assegnazioni permanenti di ruoli se l'utente dispone di un account Microsoft (usato per accedere a servizi Microsoft come Skype e Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="7cf9a-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="7cf9a-116">Se si prevede di richiedere l'autenticazione MFA per l'attivazione di questo ruolo, l'utente verrà bloccato.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="7cf9a-117">Dopo aver apportato le modifiche, la procedura guidata non verrà più visualizzata.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="7cf9a-118">Al successivo uso di PIM, anche da parte di un altro amministratore dei ruoli con privilegi, verrà visualizzato il dashboard di PIM.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="7cf9a-119">Se si vuole aggiungere o rimuovere utenti dai ruoli o modificare le assegnazioni da permanenti a idonee, vedere [Come aggiungere o rimuovere un ruolo utente](active-directory-privileged-identity-management-how-to-add-role-to-user.md)per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7cf9a-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="7cf9a-120">Per concedere a più utenti l'accesso per la gestione di PIM, vedere l'articolo [Come concedere l'accesso per la gestione di Azure AD Privileged Identity Management](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="7cf9a-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cf9a-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cf9a-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

