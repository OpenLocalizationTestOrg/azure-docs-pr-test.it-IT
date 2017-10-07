---
title: 'Sincronizzazione di Azure AD Connect: come account del servizio toomanage hello Azure AD | Documenti Microsoft'
description: Questo argomento vengono documentate come account del servizio toorestore hello Azure AD.
services: active-directory
keywords: AADSTS70002, AADSTS50054, come tooreset hello password per hello sincronizzazione di Azure AD Connect account del servizio del connettore
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="a2d4c-104">Sincronizzazione di Azure AD Connect: come account del servizio toomanage hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2d4c-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="a2d4c-105">account di servizio Hello utilizzato dal connettore Azure AD hello dovrebbe toobe servizio gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="a2d4c-106">Se è necessario tooreset le sue credenziali, in questo argomento è per l'utente.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="a2d4c-107">Ad esempio, se dispone di un amministratore globale per errore reimpostazione hello password nell'account di servizio hello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="a2d4c-108">Reimpostare le credenziali di hello</span><span class="sxs-lookup"><span data-stu-id="a2d4c-108">Reset hello credentials</span></span>
<span data-ttu-id="a2d4c-109">Se l'account del servizio hello definito in hello Azure Active Directory Connector non riesce a contattare Azure Active Directory a causa di problemi di tooauthentication, è possibile reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="a2d4c-110">Accedi a server di sincronizzazione di Azure AD Connect toohello e avviare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="a2d4c-111">Eseguire `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="a2d4c-112">![Cmdlet PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="a2d4c-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="a2d4c-113">Fornire le credenziali di amministratore globale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="a2d4c-114">Questo cmdlet Reimposta password hello dell'account del servizio hello e aggiornarlo in Azure AD e nel motore di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="a2d4c-115">Problemi noti che possono essere risolti con questi passaggi</span><span class="sxs-lookup"><span data-stu-id="a2d4c-115">Known issues these steps can solve</span></span>
<span data-ttu-id="a2d4c-116">In questa sezione è un elenco di errori segnalati dai clienti che sono stati corretti in delle credenziali predefinite nel hello account del servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="a2d4c-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="a2d4c-117">Event 6900</span></span>  
<span data-ttu-id="a2d4c-118">server di Hello ha rilevato un errore imprevisto durante l'elaborazione di una notifica di modifica password:</span><span class="sxs-lookup"><span data-stu-id="a2d4c-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="a2d4c-119">AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="a2d4c-120">AADSTS50054: Per l'autenticazione verrà usata la password precedente.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="a2d4c-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="a2d4c-121">Event 659</span></span>  
<span data-ttu-id="a2d4c-122">Errore durante il recupero della configurazione della sincronizzazione dei criteri password.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="a2d4c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="a2d4c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="a2d4c-124">AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="a2d4c-125">AADSTS50054: Per l'autenticazione verrà usata la password precedente.</span><span class="sxs-lookup"><span data-stu-id="a2d4c-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2d4c-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2d4c-126">Next steps</span></span>
<span data-ttu-id="a2d4c-127">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="a2d4c-127">**Overview topics**</span></span>

* [<span data-ttu-id="a2d4c-128">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="a2d4c-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="a2d4c-129">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2d4c-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

