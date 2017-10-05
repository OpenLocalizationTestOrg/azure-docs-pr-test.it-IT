---
title: Modificare l'algoritmo hash della firma relativo al trust della relying party di Office 365 | Microsoft Docs
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="de234-104">Modificare l'algoritmo hash della firma relativo al trust della relying party di Office 365</span><span class="sxs-lookup"><span data-stu-id="de234-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="de234-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="de234-105">Overview</span></span>
<span data-ttu-id="de234-106">Azure Active Directory Federation Services (AD FS) esegue la firma dei token per Microsoft Azure Active Directory per evitare che possano essere alterati.</span><span class="sxs-lookup"><span data-stu-id="de234-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="de234-107">Questa firma può essere basata sull'algoritmo SHA1 o SHA256.</span><span class="sxs-lookup"><span data-stu-id="de234-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="de234-108">Azure Active Directory ora supporta i token firmati con un algoritmo SHA256, quindi è consigliabile impostare l'algoritmo per la firma di token su SHA256 per garantire il massimo livello di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="de234-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="de234-109">Questo articolo descrive i passaggi necessari per impostare l'algoritmo per la firma di token sul più sicuro livello SHA256.</span><span class="sxs-lookup"><span data-stu-id="de234-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="de234-110">Microsoft consiglia di usare SHA256 come algoritmo per la firma dei token poiché è più sicuro rispetto a SHA1 ma SHA1 rimane comunque un'opzione supportata.</span><span class="sxs-lookup"><span data-stu-id="de234-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="de234-111">Modificare l'algoritmo per la firma di token</span><span class="sxs-lookup"><span data-stu-id="de234-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="de234-112">Dopo avere impostato l'algoritmo di firma con uno dei due processi seguenti, AD FS firma i token per il trust della relying party di Office 365 con SHA256.</span><span class="sxs-lookup"><span data-stu-id="de234-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="de234-113">Non è necessario apportare modifiche di configurazione aggiuntive e questa modifica non incide sulla possibilità di accedere a Office 365 o altre applicazioni Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de234-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="de234-114">Console di gestione di AD FS</span><span class="sxs-lookup"><span data-stu-id="de234-114">AD FS management console</span></span>
1. <span data-ttu-id="de234-115">Aprire la console di gestione di AD FS nel server AD FS primario.</span><span class="sxs-lookup"><span data-stu-id="de234-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="de234-116">Espandere il nodo AD FS e fare clic su **Trust relying party**.</span><span class="sxs-lookup"><span data-stu-id="de234-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="de234-117">Fare clic con il pulsante destro del mouse sul trust della relying party di Office 365/Azure e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="de234-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="de234-118">Nella scheda **Avanzate** selezionare SHA256 come algoritmo hash sicuro.</span><span class="sxs-lookup"><span data-stu-id="de234-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="de234-119">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="de234-119">Click **OK**.</span></span>

![Algoritmo di firma SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="de234-121">Cmdlet di AD FS PowerShell</span><span class="sxs-lookup"><span data-stu-id="de234-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="de234-122">Aprire PowerShell da qualsiasi server AD FS con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="de234-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="de234-123">Impostare l'algoritmo hash sicuro con il cmdlet **Set-AdfsRelyingPartyTrust** .</span><span class="sxs-lookup"><span data-stu-id="de234-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="de234-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="de234-124">Also read</span></span>
* [<span data-ttu-id="de234-125">Ripristinare il trust di Office 365 con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="de234-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

