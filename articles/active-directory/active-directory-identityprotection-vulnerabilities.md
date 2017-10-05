---
title: "Vulnerabilità rilevate da Azure Active Directory Identity Protection | Documentazione Microsoft"
description: "Panoramica delle vulnerabilità rilevate da Azure Active Directory Identity Protection"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="3f5fb-104">Vulnerabilità rilevate da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3f5fb-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="3f5fb-105">Le vulnerabilità sono punti deboli in un ambiente che possono essere sfruttati da un utente malintenzionato.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="3f5fb-106">È consigliabile risolvere le vulnerabilità per migliorare le condizioni di sicurezza dell'organizzazione e impedire che vengano sfruttate da utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="3f5fb-107">![vulnerabilità](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilità")</span><span class="sxs-lookup"><span data-stu-id="3f5fb-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="3f5fb-108">Le sezioni seguenti presentano una panoramica delle vulnerabilità segnalate da Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="3f5fb-109">Registrazione per l'autenticazione a più fattori non configurata</span><span class="sxs-lookup"><span data-stu-id="3f5fb-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="3f5fb-110">Questa vulnerabilità consente di controllare la distribuzione di Azure Multi-Factor Authentication all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="3f5fb-111">L'autenticazione a più fattori di Azure fornisce un secondo livello di sicurezza per l'autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="3f5fb-112">Consente di proteggere l'accesso ai dati e alle applicazioni dell'utente, garantendo al tempo stesso una procedura di accesso semplice.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="3f5fb-113">Offre autenticazione avanzata tramite una gamma di semplici opzioni di verifica, ad esempio una telefonata, un SMS, una notifica dell'app mobile o un codice di verifica e token OATH di terze parti.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="3f5fb-114">È consigliabile richiedere l'autenticazione a più fattori di Azure per l'accesso degli utenti.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="3f5fb-115">L'autenticazione a più fattori svolge un ruolo chiave nei criteri di accesso condizionale basati sul rischio disponibili tramite Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="3f5fb-116">Per altre informazioni, vedere [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3f5fb-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="3f5fb-117">App per cloud non gestite</span><span class="sxs-lookup"><span data-stu-id="3f5fb-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="3f5fb-118">Questa vulnerabilità consente di identificare le app per cloud non gestite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="3f5fb-119">Nelle aziende moderne, i reparti IT spesso non sono a conoscenza di tutte le applicazioni cloud usate per lavoro dagli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="3f5fb-120">L'accesso non autorizzato ai dati aziendali, le possibili perdite di dati e altri rischi di sicurezza rappresentano una preoccupazione per gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="3f5fb-121">È consigliabile distribuire Cloud App Discovery per identificare le applicazioni cloud non gestite dell'organizzazione e gestirle con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="3f5fb-122">Per altre informazioni, vedere [Ricerca di applicazioni cloud non gestite con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f5fb-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="3f5fb-123">Avvisi di sicurezza di Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="3f5fb-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="3f5fb-124">Questa vulnerabilità permette di identificare e risolvere gli avvisi sulle identità con privilegi all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="3f5fb-125">Per consentire agli utenti di eseguire operazioni con privilegi, le organizzazioni devono concedere agli utenti accessi con privilegi temporanei o permanenti in Azure AD, per le risorse di Azure o Office 365 o per altre app SaaS.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="3f5fb-126">Ognuno di questi utenti con privilegi aumenta la superficie di attacco dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="3f5fb-127">Questa vulnerabilità consente di identificare gli utenti che hanno un accesso con privilegi non necessario e di intraprendere le azioni appropriate per ridurre o eliminare il rischio.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="3f5fb-128">È consigliabile usare Azure AD Privileged Identity Management nell'organizzazione per gestire, controllare e monitorare le identità con privilegi e il relativo accesso alle risorse in Azure AD e in altri Microsoft Online Services, ad esempio Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="3f5fb-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="3f5fb-129">Per altre informazioni, vedere [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3f5fb-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="3f5fb-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3f5fb-130">See also</span></span>
* [<span data-ttu-id="3f5fb-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3f5fb-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

