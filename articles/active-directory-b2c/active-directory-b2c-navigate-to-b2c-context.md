---
title: 'Azure Active Directory B2C: Passaggio a un tenant B2C | Microsoft Docs'
description: Come passare a un tenant diverso nel contesto del tenant di Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 0eb1b198-44d3-4065-9fae-16591a8d3eae
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/13/2017
ms.author: parakhj
ms.openlocfilehash: 40d8d57d974a949fbdc0a06eeceb2d06bfbaa09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="switching-to-your-azure-ad-b2c-tenant"></a><span data-ttu-id="fe963-103">Passaggio al tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fe963-103">Switching to your Azure AD B2C tenant</span></span>

<span data-ttu-id="fe963-104">Per configurare Azure AD B2C, è necessario trovarsi nel contesto del tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-104">In order to configure Azure AD B2C, you need to be in the context of your Azure AD B2C tenant.</span></span>

## <a name="log-into-azure-ad-b2c-tenant"></a><span data-ttu-id="fe963-105">Accedere al tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fe963-105">Log into Azure AD B2C tenant</span></span>

<span data-ttu-id="fe963-106">Per passare al tenant di Azure AD B2C, è necessario essere connessi al portale di Azure come amministratore globale del tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-106">To navigate to your Azure AD B2C tenant, you must be logged into the Azure portal as a global administrator of the Azure AD B2C tenant.</span></span>

1. <span data-ttu-id="fe963-107">Accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe963-107">Sign into the [Azure portal](http://portal.azure.com).</span></span>
1. <span data-ttu-id="fe963-108">Cambiare tenant facendo clic sull'indirizzo di posta elettronica o sull'immagine nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="fe963-108">Switch tenants by clicking your email address or picture in the top-right corner.</span></span>
1. <span data-ttu-id="fe963-109">Nell'elenco `Directory` visualizzato selezionare il tenant di Azure AD B2C da gestire.</span><span class="sxs-lookup"><span data-stu-id="fe963-109">In the `Directory` list that appears, select the Azure AD B2C tenant that you wish to manage.</span></span>

<span data-ttu-id="fe963-110">Il portale di Azure verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="fe963-110">The Azure Portal will refresh.</span></span>  <span data-ttu-id="fe963-111">Si è ora connessi al portale di Azure nel contesto del tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-111">Now you are signed into the Azure Portal in the context of your Azure AD B2C tenant.</span></span>

## <a name="navigate-to-the-b2c-features-blade"></a><span data-ttu-id="fe963-112">Passare al pannello delle funzionalità B2C</span><span class="sxs-lookup"><span data-stu-id="fe963-112">Navigate to the B2C features blade</span></span>

1. <span data-ttu-id="fe963-113">Fare clic su **Sfoglia** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fe963-113">Click **Browse** on the left hand navigation.</span></span>
1. <span data-ttu-id="fe963-114">Fare clic su **> Altri servizi** e quindi cercare `Azure AD B2C` nel riquadro di spostamento di sinistra.</span><span class="sxs-lookup"><span data-stu-id="fe963-114">Click **> More services** and then search for `Azure AD B2C` in the left navigation pane.</span></span>  <span data-ttu-id="fe963-115">Per aggiungerlo alla schermata iniziale di sinistra, fare clic sulla stella a sinistra di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-115">(To pin to your left-hand Startboard, click the star to the left of Azure AD B2C)</span></span>
1. <span data-ttu-id="fe963-116">Fare clic su **Azure AD B2C** per accedere al pannello delle funzionalità B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-116">Click **Azure AD B2C** to access the B2C features blade.</span></span>
   
    ![Screenshot del pannello delle funzionalità B2C](./media/active-directory-b2c-get-started/b2c-browse.png)

> [!IMPORTANT]
> <span data-ttu-id="fe963-118">È necessario avere diritti di amministratore globale del tenant B2C per poter accedere al pannello delle funzionalità B2C.</span><span class="sxs-lookup"><span data-stu-id="fe963-118">You need to be a Global Administrator of the B2C tenant to be able to access the B2C features blade.</span></span> <span data-ttu-id="fe963-119">Un amministratore globale o un utente di qualsiasi altro tenant non può accedere.</span><span class="sxs-lookup"><span data-stu-id="fe963-119">A Global Administrator from any other tenant or a user from any tenant cannot access it.</span></span>  <span data-ttu-id="fe963-120">È possibile passare al tenant B2C usando l'apposito controllo nell'angolo superiore destro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe963-120">You can switch to your B2C tenant by using the tenant switcher in the top right corner of the Azure portal.</span></span>
