---
title: procedura guidata di protezione di aaaThe Azure AD Privileged Identity Management
description: "Hello prima volta che si utilizza l'estensione di Azure Active Directory Privileged Identity Management hello, verrà visualizzata una procedura guidata di protezione. Questo articolo descrive i passaggi di hello per utilizzare la procedura guidata hello."
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
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9b866-104">Utilizzando la procedura guidata protezione hello in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9b866-104">Using hello security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="9b866-105">Se si hello prima persona toorun Azure Privileged Identity Management (PIM) per l'organizzazione, verrà visualizzata una procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="9b866-105">If you're hello first person toorun Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="9b866-106">procedura guidata Hello consente di comprendere i rischi di sicurezza hello delle identità con privilegi e come toouse PIM tooreduce tali rischi.</span><span class="sxs-lookup"><span data-stu-id="9b866-106">hello wizard helps you understand hello security risks of privileged identities and how toouse PIM tooreduce those risks.</span></span> <span data-ttu-id="9b866-107">Non è necessario toomake le assegnazioni di ruolo tooexisting eventuali modifiche nella procedura guidata hello, se si preferisce toodo posticipato.</span><span class="sxs-lookup"><span data-stu-id="9b866-107">You don't need toomake any changes tooexisting role assignments in hello wizard, if you prefer toodo it later.</span></span>

## <a name="what-tooexpect"></a><span data-ttu-id="9b866-108">Quali tooexpect</span><span class="sxs-lookup"><span data-stu-id="9b866-108">What tooexpect</span></span>
<span data-ttu-id="9b866-109">Prima che l'organizzazione inizia a usare PIM, tutte le assegnazioni di ruolo sono permanenti: gli utenti di hello sono sempre a questi ruoli, anche se non è necessario attualmente i propri privilegi.</span><span class="sxs-lookup"><span data-stu-id="9b866-109">Before your organization starts using PIM, all role assignments are permanent: hello users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="9b866-110">innanzitutto Hello della procedura guidata hello Mostra un elenco di ruoli con privilegi elevati e il numero di utenti è attualmente in tali ruoli.</span><span class="sxs-lookup"><span data-stu-id="9b866-110">hello first step of hello wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="9b866-111">È possibile analizzare in tooa particolare ruolo toolearn ulteriori informazioni su utenti, se uno o più di esse si ha dimestichezza.</span><span class="sxs-lookup"><span data-stu-id="9b866-111">You can drill in tooa particular role toolearn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="9b866-112">secondo passaggio di Hello della procedura guidata hello offre le assegnazioni di ruolo dell'amministratore toochange opportunità.</span><span class="sxs-lookup"><span data-stu-id="9b866-112">hello second step of hello wizard gives you an opportunity toochange administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="9b866-113">È importante che siano presenti almeno un amministratore globale e più amministratori dei ruoli con privilegi con account aziendali e non account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9b866-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="9b866-114">Se è presente solo un amministratore del ruolo con privilegi, organizzazione hello non sarà in grado di toomanage PIM se tale account viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="9b866-114">If there is only one privileged role administrator, hello organization will not be able toomanage PIM if that account is deleted.</span></span>
> <span data-ttu-id="9b866-115">Tenere inoltre le assegnazioni di ruolo permanente se un utente dispone di un account Microsoft (account utilizzano toosign in servizi tooMicrosoft Skype e Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="9b866-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use toosign in tooMicrosoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="9b866-116">Se si prevede di toorequire autenticazione a più fattori per l'attivazione per tale ruolo, tale utente verrà bloccato.</span><span class="sxs-lookup"><span data-stu-id="9b866-116">If you plan toorequire MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="9b866-117">Dopo avere apportato modifiche, la procedura guidata hello non mostrerà più.</span><span class="sxs-lookup"><span data-stu-id="9b866-117">After you have made changes, hello wizard will no longer show up.</span></span> <span data-ttu-id="9b866-118">Hello successivo utilizzo di un ruolo con privilegi amministratore PIM, verrà visualizzato il dashboard PIM hello.</span><span class="sxs-lookup"><span data-stu-id="9b866-118">hello next time you or another privileged role administrator use PIM, you will see hello PIM dashboard.</span></span>  

* <span data-ttu-id="9b866-119">Se si sarebbe ad esempio tooadd o rimuovere utenti dai ruoli o modificare le assegnazioni da tooeligible permanente, leggere informazioni, vedere [come tooadd o rimuovere un ruolo utente](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="9b866-119">If you would like tooadd or remove users from roles or change assignments from permanent tooeligible, read more at [how tooadd or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="9b866-120">Se si desidera toogive toomanage PIM, accedano a più utenti di leggere informazioni, vedere [modalità di accesso toomanage in PIM toogive](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="9b866-120">If you would like toogive more users access toomanage PIM, read more at [how toogive access toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b866-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b866-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

