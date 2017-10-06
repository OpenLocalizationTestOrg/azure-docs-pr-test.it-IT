---
title: algoritmo hash della firma aaaChange per Office 365 trust della relying party | Documenti Microsoft
description: Questa pagina fornisce le linee guida per la modifica dell'algoritmo SHA per il trust federativo con Office 365
keywords: SHA1,SHA256,O365,federazione,aadconnect,adfs,ad fs,modifica algoritmo hash della firma,trust federativo,trust della relying party
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="0db85-104">Modificare l'algoritmo hash della firma relativo al trust della relying party di Office 365</span><span class="sxs-lookup"><span data-stu-id="0db85-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="0db85-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0db85-105">Overview</span></span>
<span data-ttu-id="0db85-106">Active Directory Federation Services (ADFS) firma relativo tooensure di Azure Active Directory tooMicrosoft i token che non possa essere manomessa.</span><span class="sxs-lookup"><span data-stu-id="0db85-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="0db85-107">Questa firma può essere basata sull'algoritmo SHA1 o SHA256.</span><span class="sxs-lookup"><span data-stu-id="0db85-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="0db85-108">Azure Active Directory supporta ora i token firmati con un algoritmo SHA256, ed è consigliabile impostare hello tooSHA256 algoritmo di firma di token per il livello più alto di hello di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="0db85-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="0db85-109">Questo articolo descrive i passaggi di hello necessari toohello di algoritmo di firma di token hello tooset più sicuro il livello SHA256.</span><span class="sxs-lookup"><span data-stu-id="0db85-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="0db85-110">Microsoft consiglia l'utilizzo di SHA256 come algoritmo di hello per la firma di token è più sicuro rispetto a SHA1 ma SHA1 rimane comunque un'opzione supportata.</span><span class="sxs-lookup"><span data-stu-id="0db85-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="0db85-111">Modificare l'algoritmo di firma di token hello</span><span class="sxs-lookup"><span data-stu-id="0db85-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="0db85-112">Dopo aver impostato l'algoritmo di firma hello con uno dei hello due processi, AD FS firma token hello per Office 365 trust della relying party con SHA256.</span><span class="sxs-lookup"><span data-stu-id="0db85-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="0db85-113">Non è necessario di tutte le modifiche di configurazione aggiuntive toomake e questa modifica non ha alcun impatto sul tooaccess possibilità Office 365 o di altre applicazioni di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0db85-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="0db85-114">Console di gestione di AD FS</span><span class="sxs-lookup"><span data-stu-id="0db85-114">AD FS management console</span></span>
1. <span data-ttu-id="0db85-115">Aprire console di gestione di hello AD ADFS nel server di hello primario AD FS.</span><span class="sxs-lookup"><span data-stu-id="0db85-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="0db85-116">Espandere il nodo di hello AD FS e fare clic su **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="0db85-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0db85-117">Fare clic con il pulsante destro del mouse sul trust della relying party di Office 365/Azure e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0db85-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="0db85-118">Seleziona hello **avanzate** scheda e l'algoritmo hash protetto hello selezionare SHA256.</span><span class="sxs-lookup"><span data-stu-id="0db85-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="0db85-119">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0db85-119">Click **OK**.</span></span>

![Algoritmo di firma SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="0db85-121">Cmdlet di AD FS PowerShell</span><span class="sxs-lookup"><span data-stu-id="0db85-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="0db85-122">Aprire PowerShell da qualsiasi server AD FS con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="0db85-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="0db85-123">Algoritmo hash protetto di hello set tramite hello **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0db85-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="0db85-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0db85-124">Also read</span></span>
* [<span data-ttu-id="0db85-125">Ripristinare il trust di Office 365 con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0db85-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

