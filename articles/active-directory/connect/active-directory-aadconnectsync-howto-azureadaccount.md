---
title: 'Servizio di sincronizzazione Azure Active Directory Connect: come gestire l''account del servizio Azure Active Directory | Microsoft Docs'
description: Questo argomento illustra come ripristinare l'account del servizio Azure AD.
services: active-directory
keywords: AADSTS70002, AADSTS50054, Come reimpostare la password dell'account del servizio di sincronizzazione Azure AD Connect
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="dd6ba-104">Servizio di sincronizzazione Azure Active Directory Connect: come gestire l'account del servizio Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd6ba-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="dd6ba-105">L'account di servizio utilizzato da Azure Active Directory Connector è progettato per non richiedere manutenzione.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="dd6ba-106">Questo argomento descrive come reimpostare le credenziali in caso di necessità,</span><span class="sxs-lookup"><span data-stu-id="dd6ba-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="dd6ba-107">ad esempio se un amministratore globale ha erroneamente reimpostato la password dell'account del servizio con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="dd6ba-108">Reimpostazione delle credenziali</span><span class="sxs-lookup"><span data-stu-id="dd6ba-108">Reset the credentials</span></span>
<span data-ttu-id="dd6ba-109">Se l'account del servizio definito in Azure Active Directory Connector non riesce a contattare Azure Active Directory a causa di problemi di autenticazione, è possibile reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="dd6ba-110">Effettuare l'accesso al server di sincronizzazione Azure AD Connect e avviare PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="dd6ba-111">Eseguire `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="dd6ba-112">![Cmdlet PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="dd6ba-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="dd6ba-113">Fornire le credenziali di amministratore globale di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="dd6ba-114">Questo cmdlet reimposta la password dell'account del servizio e la aggiorna sia in Azure AD, sia nel motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="dd6ba-115">Problemi noti che possono essere risolti con questi passaggi</span><span class="sxs-lookup"><span data-stu-id="dd6ba-115">Known issues these steps can solve</span></span>
<span data-ttu-id="dd6ba-116">Questa sezione riporta un elenco di errori segnalati dai clienti che sono stati corretti reimpostando le credenziali nell'account del servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="dd6ba-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="dd6ba-117">Event 6900</span></span>  
<span data-ttu-id="dd6ba-118">Il server ha rilevato un errore imprevisto durante l'elaborazione di una notifica di modifica password:</span><span class="sxs-lookup"><span data-stu-id="dd6ba-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="dd6ba-119">AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="dd6ba-120">AADSTS50054: Per l'autenticazione verrà usata la password precedente.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="dd6ba-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="dd6ba-121">Event 659</span></span>  
<span data-ttu-id="dd6ba-122">Errore durante il recupero della configurazione della sincronizzazione dei criteri password.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="dd6ba-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="dd6ba-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="dd6ba-124">AADSTS70002: Errore di convalida delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="dd6ba-125">AADSTS50054: Per l'autenticazione verrà usata la password precedente.</span><span class="sxs-lookup"><span data-stu-id="dd6ba-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd6ba-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd6ba-126">Next steps</span></span>
<span data-ttu-id="dd6ba-127">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="dd6ba-127">**Overview topics**</span></span>

* [<span data-ttu-id="dd6ba-128">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="dd6ba-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="dd6ba-129">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd6ba-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

