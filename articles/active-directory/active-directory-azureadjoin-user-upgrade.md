---
title: aaaSet un dispositivo Windows 10 con Azure AD dalle impostazioni | Documenti Microsoft
description: Viene illustrato come gli utenti possono partecipare tooAzure AD tramite il menu di impostazioni hello.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="06453-103">Configurazione di un dispositivo Windows 10 con Azure AD da Impostazioni</span><span class="sxs-lookup"><span data-stu-id="06453-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="06453-104">Se si ha già con Windows 7 o Windows 8 e un computer o dispositivo è stato aggiornato tooWindows 10, è possibile unire tooAzure Active Directory (Azure AD) tramite il menu di impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="06453-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="06453-105">toojoin tooAzure Active Directory dal menu Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="06453-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="06453-106">Da hello **avviare** menu, fare clic su hello **impostazioni** accesso.</span><span class="sxs-lookup"><span data-stu-id="06453-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="06453-107">Da **Impostazioni** selezionare **Sistema**->**Informazioni**->**Aggiungi ad Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="06453-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="06453-108"><center>
   ![Aggiungere Azure Active Directory dal menu Impostazioni hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="06453-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="06453-109">Fare clic su **continua** nella finestra di messaggio hello aggiunta ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06453-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="06453-110"><center>
   ![Finestra di messaggio Aggiungi ad Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="06453-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="06453-111">Fornire le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="06453-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="06453-112">Questa esperienza di accesso includerà tutti i passaggi di hello che sono necessari toocomplete autenticazione.</span><span class="sxs-lookup"><span data-stu-id="06453-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="06453-113">Se si fa parte di un tenant federato, l'amministratore sarà con esperienza di federazione hello è ospitato dalla propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="06453-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="06453-114"><center>
   ![Fornire le credenziali di accesso](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span><span class="sxs-lookup"><span data-stu-id="06453-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="06453-115">Se l'organizzazione ha configurato Azure multi-Factor Authentication per l'aggiunta AD tooAzure, fornire secondo fattore di hello prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="06453-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="06453-116">Fare clic su **Accept** su hello **consentire questa toobe dispositivo gestito** dello schermo.</span><span class="sxs-lookup"><span data-stu-id="06453-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="06453-117">Verrà visualizzato il messaggio hello "il dispositivo è ora tooyour unita in join dell'organizzazione in Azure AD".</span><span class="sxs-lookup"><span data-stu-id="06453-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="06453-118">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="06453-118">Additional information</span></span>
* [<span data-ttu-id="06453-119">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="06453-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="06453-120">Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10</span><span class="sxs-lookup"><span data-stu-id="06453-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="06453-121">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="06453-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="06453-122">Autenticazione delle identità senza password con Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="06453-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

