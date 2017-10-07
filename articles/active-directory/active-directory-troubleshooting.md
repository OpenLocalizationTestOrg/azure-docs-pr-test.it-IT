---
title: "Risoluzione dei problemi: Elemento \"Active Directory\" è mancante o non disponibile | Documenti Microsoft"
description: Quali toodo quando la voce di menu Active Directory non viene visualizzato nel portale di gestione Azure hello.
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="77073-103">Risoluzione dei problemi: Voce "Active Directory" mancante o non disponibile</span><span class="sxs-lookup"><span data-stu-id="77073-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="77073-104">Molte delle istruzioni di hello per l'utilizzo di servizi e funzionalità di Azure Active Directory iniziano con "toohello portale di gestione di Azure, fare clic su **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="77073-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="77073-105">Ma cosa fare se non viene visualizzata la voce di menu o estensione di Active Directory hello o se è contrassegnato come **non disponibile**?</span><span class="sxs-lookup"><span data-stu-id="77073-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="77073-106">In questo argomento è progettato toohelp.</span><span class="sxs-lookup"><span data-stu-id="77073-106">This topic is designed toohelp.</span></span> <span data-ttu-id="77073-107">Viene descritto hello condizioni **Active Directory** non viene visualizzata o non è disponibile e viene spiegato come tooproceed.</span><span class="sxs-lookup"><span data-stu-id="77073-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="77073-108">Active Directory non disponibile</span><span class="sxs-lookup"><span data-stu-id="77073-108">Active Directory is missing</span></span>
<span data-ttu-id="77073-109">In genere, un **Active Directory** elemento viene visualizzato nel menu di navigazione sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="77073-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="77073-110">istruzioni di Hello nelle procedure di Azure Active Directory si supponga che nella visualizzazione di questo elemento.</span><span class="sxs-lookup"><span data-stu-id="77073-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Schermata: Active Directory in Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="77073-112">voce di Active Directory Hello viene visualizzata nel menu di navigazione sinistro hello quando una delle seguenti condizioni hello è true.</span><span class="sxs-lookup"><span data-stu-id="77073-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="77073-113">In caso contrario, non viene visualizzato elemento hello.</span><span class="sxs-lookup"><span data-stu-id="77073-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="77073-114">utente corrente Hello l'accesso con un account Microsoft (precedentemente noto come Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="77073-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="77073-115">OPPURE</span><span class="sxs-lookup"><span data-stu-id="77073-115">OR</span></span>
* <span data-ttu-id="77073-116">Hello tenant di Azure dispone di una directory e account di hello corrente sia un amministratore di directory.</span><span class="sxs-lookup"><span data-stu-id="77073-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="77073-117">OPPURE</span><span class="sxs-lookup"><span data-stu-id="77073-117">OR</span></span>
* <span data-ttu-id="77073-118">Hello tenant di Azure ha almeno uno spazio dei nomi di Azure AD Access Control (ACS).</span><span class="sxs-lookup"><span data-stu-id="77073-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="77073-119">Per altre informazioni, vedere [Spazio dei nomi di Access Control](https://msdn.microsoft.com/library/azure/gg185908.aspx)</span><span class="sxs-lookup"><span data-stu-id="77073-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="77073-120">OPPURE</span><span class="sxs-lookup"><span data-stu-id="77073-120">OR</span></span>
* <span data-ttu-id="77073-121">Hello tenant di Azure ha almeno un provider di Azure multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="77073-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="77073-122">Per altre informazioni, vedere [Amministrazione dei provider di Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="77073-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="77073-123">toocreate uno spazio dei nomi di controllo di accesso o un provider di multi-Factor Authentication, fare clic su **+ nuovo** > **servizi App** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77073-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="77073-124">directory di tooa tooget diritti amministrativi, hanno un amministratore di assegnare a un amministratore tooyour account membro del ruolo.</span><span class="sxs-lookup"><span data-stu-id="77073-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="77073-125">Per informazioni dettagliate, vedere [Assegnazione dei ruoli di amministratore in Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="77073-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="77073-126">Active Directory non è disponibile</span><span class="sxs-lookup"><span data-stu-id="77073-126">Active Directory is not available</span></span>
<span data-ttu-id="77073-127">Quando si fa clic su **+Nuovo** > **Servizi app**, viene visualizzata la voce **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77073-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="77073-128">In particolare, voce di Active Directory hello viene visualizzata quando si verifica una delle funzionalità di Active Directory hello, ad esempio Directory, il controllo di accesso o Provider di multi-Factor Authentication, utente corrente toohello disponibili.</span><span class="sxs-lookup"><span data-stu-id="77073-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="77073-129">Tuttavia, durante il caricamento pagina hello, elemento hello è visualizzata in grigio e viene contrassegnato **non disponibile**.</span><span class="sxs-lookup"><span data-stu-id="77073-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="77073-130">Questo stato è temporaneo.</span><span class="sxs-lookup"><span data-stu-id="77073-130">This is a temporary state.</span></span> <span data-ttu-id="77073-131">Attendere alcuni secondi, l'elemento hello diventa disponibile.</span><span class="sxs-lookup"><span data-stu-id="77073-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="77073-132">Se hello ritardo è prolungato, l'aggiornamento della pagina web di hello consente spesso di risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="77073-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Schermata: Active Directory non disponibile](./media/active-directory-troubleshooting/not-available.png)

