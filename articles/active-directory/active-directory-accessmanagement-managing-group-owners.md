---
title: Passaggi successivi per la gestione dell'accesso mediante i gruppi | Documentazione Microsoft
description: Procedura avanzata per la gestione dei gruppi di sicurezza e l'uso di questi gruppi per gestire l'accesso a una risorsa.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="6e7fa-103">Gestione dei proprietari di un gruppo</span><span class="sxs-lookup"><span data-stu-id="6e7fa-103">Managing owners for a group</span></span>
<span data-ttu-id="6e7fa-104">Quando il proprietario delle risorse ha assegnato l'accesso a una risorsa a un gruppo di Azure AD, l'appartenenza al gruppo viene gestita dal proprietario del gruppo.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="6e7fa-105">Il proprietario della risorsa delega in modo efficace l'autorizzazione ad assegnare agli utenti la loro risorsa al proprietario del gruppo.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e7fa-106">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="6e7fa-107">Assegnare la proprietà del gruppo</span><span class="sxs-lookup"><span data-stu-id="6e7fa-107">Assigning group ownership</span></span>
<span data-ttu-id="6e7fa-108">**Per Aggiungere un proprietario a un gruppo**</span><span class="sxs-lookup"><span data-stu-id="6e7fa-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="6e7fa-109">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="6e7fa-110">Selezionare la scheda **Gruppi** e aprire il gruppo a cui si desiderano aggiungere proprietari.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="6e7fa-111">Selezionare **Aggiungi proprietari**.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="6e7fa-112">Nella pagina **Aggiungi proprietari** selezionare l'utente che si desidera aggiungere come proprietario del gruppo e verificare che questo nome venga aggiunto al riquadro **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="6e7fa-113">**Per rimuovere un proprietario da un gruppo**</span><span class="sxs-lookup"><span data-stu-id="6e7fa-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="6e7fa-114">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="6e7fa-115">Selezionare la scheda **Gruppi** e aprire il gruppo da cui si desidera rimuovere un proprietario.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="6e7fa-116">Selezionare la scheda **Proprietari** .</span><span class="sxs-lookup"><span data-stu-id="6e7fa-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="6e7fa-117">Selezionare il proprietario da rimuovere dal gruppo e quindi scegliere **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="6e7fa-118">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6e7fa-118">Additional information</span></span>
<span data-ttu-id="6e7fa-119">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6e7fa-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="6e7fa-120">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e7fa-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="6e7fa-121">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="6e7fa-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="6e7fa-122">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e7fa-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6e7fa-123">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e7fa-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="6e7fa-124">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e7fa-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
