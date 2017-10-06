---
title: aaaNext i passaggi per la gestione di accesso mediante gruppi | Documenti Microsoft
description: "Modalità avanzate-a gestione dei gruppi di sicurezza e come toouse queste risorse tooa di gruppi toomanage accesso."
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="a808a-103">Gestione dei proprietari di un gruppo</span><span class="sxs-lookup"><span data-stu-id="a808a-103">Managing owners for a group</span></span>
<span data-ttu-id="a808a-104">Una volta un proprietario della risorsa è assegnato a gruppo di accesso tooa risorse tooan Azure AD, l'appartenenza hello del gruppo di hello è gestita dal proprietario del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="a808a-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="a808a-105">proprietario della risorsa Hello vengono delegate hello autorizzazione tooassign utenti toohello toohello proprietario della risorsa del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="a808a-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a808a-106">Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a808a-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="a808a-107">Assegnare la proprietà del gruppo</span><span class="sxs-lookup"><span data-stu-id="a808a-107">Assigning group ownership</span></span>
<span data-ttu-id="a808a-108">**un gruppo di tooa proprietario tooadd**</span><span class="sxs-lookup"><span data-stu-id="a808a-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="a808a-109">In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a808a-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a808a-110">Seleziona hello **gruppi** , scheda e un gruppo di hello quindi aperto da tooadd ai proprietari di.</span><span class="sxs-lookup"><span data-stu-id="a808a-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="a808a-111">Selezionare **Aggiungi proprietari**.</span><span class="sxs-lookup"><span data-stu-id="a808a-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="a808a-112">In hello **aggiungere proprietari** pagina, l'utente di selezionare hello vuole tooadd come proprietario di hello di questo gruppo e verificare che questo nome viene aggiunto toohello **selezionati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="a808a-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="a808a-113">**tooremove un proprietario di un gruppo**</span><span class="sxs-lookup"><span data-stu-id="a808a-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="a808a-114">In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi aprire la directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a808a-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a808a-115">Seleziona hello **gruppi** scheda e quindi aprire hello gruppo che si desidera tooremove proprietari.</span><span class="sxs-lookup"><span data-stu-id="a808a-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="a808a-116">Seleziona hello **proprietari** scheda.</span><span class="sxs-lookup"><span data-stu-id="a808a-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="a808a-117">Proprietario hello selezionare desidera tooremove da questo gruppo e quindi selezionare **rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="a808a-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="a808a-118">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a808a-118">Additional information</span></span>
<span data-ttu-id="a808a-119">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a808a-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a808a-120">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a808a-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a808a-121">Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo</span><span class="sxs-lookup"><span data-stu-id="a808a-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="a808a-122">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a808a-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a808a-123">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a808a-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a808a-124">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a808a-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
