---
title: Abilitazione di Azure Active Directory Identity Protection | Microsoft Docs
description: Informazioni su come abilitare Azure Active Directory Identity Protection.
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="d0193-104">Abilitazione di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d0193-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="d0193-105">Azure Active Directory Identity Protection è una nuova funzionalità che offre una vista consolidata delle attività di accesso sospette e delle potenziali vulnerabilità e che contribuisce a proteggere l'azienda con notifiche, raccomandazioni sulla risoluzione dei problemi e criteri basati sui rischi.</span><span class="sxs-lookup"><span data-stu-id="d0193-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="d0193-106">Il servizio rileva le attività sospette per l'utente finale e le identità con privilegi (amministratore), in base a segnali come attacchi di forza bruta, perdita di credenziali, accessi da località ignote e dispositivi infetti per offrire una protezione da queste attività in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="d0193-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="d0193-107">Ancora più importante, sulla base di queste attività sospette viene calcolato un livello di gravità dei rischi per l'utente ed è possibile configurare criteri basati sui rischi e proteggere automaticamente le identità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d0193-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="d0193-108">Per altre informazioni, vedere [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="d0193-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="d0193-109">Questo argomento illustra come abilitare Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="d0193-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="d0193-110">Passaggi per abilitare Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d0193-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="d0193-111">[Accedere](https://ms.portal.azure.com/) al portale di Azure come amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="d0193-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="d0193-112">Nel portale di Azure fare clic su **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d0193-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="d0193-113">![Creare](./media/active-directory-identityprotection-enable/01.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="d0193-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="d0193-114">Nell'elenco delle applicazioni fare clic su **Sicurezza e identità**.</span><span class="sxs-lookup"><span data-stu-id="d0193-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="d0193-115">![Creare](./media/active-directory-identityprotection-enable/02.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="d0193-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="d0193-116">Fare clic su **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="d0193-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="d0193-117">![Creare](./media/active-directory-identityprotection-enable/03.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="d0193-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="d0193-118">Nel pannello **Azure AD Identity Protection** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d0193-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="d0193-119">![Creare](./media/active-directory-identityprotection-enable/04.png "Creare")</span><span class="sxs-lookup"><span data-stu-id="d0193-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0193-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0193-120">Next Steps</span></span>
* [<span data-ttu-id="d0193-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d0193-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

