---
title: Assegnare gli utenti a un dominio personalizzato in Azure Active Directory | Documentazione Microsoft
description: Come popolare un dominio personalizzato in Azure Active Directory con gli account utente.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="d756d-103">Assegnare utenti a un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="d756d-103">Assign users to a custom domain</span></span>
<span data-ttu-id="d756d-104">Dopo aver aggiunto il dominio personalizzato in Azure Active Directory, è necessario aggiungere gli account utente del dominio per poter iniziare l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="d756d-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d756d-105">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="d756d-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="d756d-106">Per informazioni su come gestire i nomi di dominio nell'interfaccia di amministrazione di Azure AD, vedere [Gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d756d-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="d756d-107">Utenti sincronizzati da una directory locale</span><span class="sxs-lookup"><span data-stu-id="d756d-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="d756d-108">Se è già stata impostata una connessione tra Active Directory locale e Azure Active Directory, la sincronizzazione può popolare gli account.</span><span class="sxs-lookup"><span data-stu-id="d756d-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="d756d-109">Per altre informazioni sulla sincronizzazione di Azure Active Directory con Active Directory locale, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d756d-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="d756d-110">Utenti aggiunti e gestiti nel cloud</span><span class="sxs-lookup"><span data-stu-id="d756d-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="d756d-111">Per modificare il dominio di un account utente esistente:</span><span class="sxs-lookup"><span data-stu-id="d756d-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="d756d-112">Aprire il portale di Azure classico usando un account amministratore globale o amministratore utenti.</span><span class="sxs-lookup"><span data-stu-id="d756d-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="d756d-113">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="d756d-113">Open your directory.</span></span>
3. <span data-ttu-id="d756d-114">Selezionare la scheda **Utenti** ,</span><span class="sxs-lookup"><span data-stu-id="d756d-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="d756d-115">Selezionare l'utente dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="d756d-115">Select the user from the list.</span></span>
5. <span data-ttu-id="d756d-116">Modificare il dominio dell'utente e quindi selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d756d-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="d756d-117">Questa operazione può essere eseguita anche usando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o l'[API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="d756d-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="d756d-118">Selezionare un dominio personalizzato durante la creazione di un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="d756d-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="d756d-119">Aprire il portale di Azure classico usando un account amministratore globale o amministratore utenti.</span><span class="sxs-lookup"><span data-stu-id="d756d-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="d756d-120">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="d756d-120">Open your directory.</span></span>
3. <span data-ttu-id="d756d-121">Selezionare la scheda **Utenti** ,</span><span class="sxs-lookup"><span data-stu-id="d756d-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="d756d-122">Sulla barra dei comandi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d756d-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="d756d-123">Quando si aggiunge il nome utente, scegliere il dominio personalizzato dall'elenco di domini.</span><span class="sxs-lookup"><span data-stu-id="d756d-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="d756d-124">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d756d-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d756d-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d756d-125">Next steps</span></span>
* [<span data-ttu-id="d756d-126">Uso di nomi di dominio personalizzati per semplificare l'esperienza di accesso degli utenti</span><span class="sxs-lookup"><span data-stu-id="d756d-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="d756d-127">Gestire i nomi di dominio personalizzati</span><span class="sxs-lookup"><span data-stu-id="d756d-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="d756d-128">Informazioni sui concetti relativi alla gestione dei domini in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d756d-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

