---
title: rilevato da Azure Active Directory Identity Protection aaaVulnerabilities | Documenti Microsoft
description: "Panoramica di vulnerabilità hello rilevate da Azure Active Directory Identity Protection."
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
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="eda71-104">Vulnerabilità rilevate da Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="eda71-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="eda71-105">Le vulnerabilità sono punti deboli in un ambiente che possono essere sfruttati da un utente malintenzionato.</span><span class="sxs-lookup"><span data-stu-id="eda71-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="eda71-106">È consigliabile risolvere tali condizioni di sicurezza hello tooimprove vulnerabilità dell'organizzazione e di impedire ai pirati informatici sfrutti li.</span><span class="sxs-lookup"><span data-stu-id="eda71-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="eda71-107">![vulnerabilità](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilità")</span><span class="sxs-lookup"><span data-stu-id="eda71-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="eda71-108">Hello nelle sezioni seguenti forniscono una panoramica delle vulnerabilità hello segnalati da Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="eda71-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="eda71-109">Registrazione per l'autenticazione a più fattori non configurata</span><span class="sxs-lookup"><span data-stu-id="eda71-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="eda71-110">Questa vulnerabilità contribuisce di controllare la distribuzione di hello Azure multi-Factor Authentication all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eda71-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="eda71-111">Azure multi-factor authentication fornisce un secondo livello toouser di autenticazione di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="eda71-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="eda71-112">Consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo.</span><span class="sxs-lookup"><span data-stu-id="eda71-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="eda71-113">Offre autenticazione avanzata tramite una gamma di semplici opzioni di verifica, ad esempio una telefonata, un SMS, una notifica dell'app mobile o un codice di verifica e token OATH di terze parti.</span><span class="sxs-lookup"><span data-stu-id="eda71-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="eda71-114">È consigliabile richiedere l'autenticazione a più fattori di Azure per l'accesso degli utenti. L'autenticazione a più fattori svolge un ruolo chiave nei criteri di accesso condizionale basati sul rischio disponibili tramite Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="eda71-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="eda71-115">Per altre informazioni, vedere [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="eda71-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="eda71-116">App per cloud non gestite</span><span class="sxs-lookup"><span data-stu-id="eda71-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="eda71-117">Questa vulnerabilità consente di identificare le app per cloud non gestite all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eda71-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="eda71-118">Nelle aziende moderne i reparti IT spesso sono consapevoli tutte le applicazioni cloud hello che gli utenti dell'organizzazione utilizzando toodo il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="eda71-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="eda71-119">È facile toosee perché gli amministratori avranno preoccupazioni dati toocorporate di accesso non autorizzato, perdita di dati e altri rischi di protezione.</span><span class="sxs-lookup"><span data-stu-id="eda71-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="eda71-120">È consigliabile l'organizzazione di distribuire le applicazioni cloud di Cloud App Discovery toodiscover non gestita e toomanage queste applicazioni con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eda71-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="eda71-121">Per altre informazioni, vedere [Ricerca di applicazioni cloud non gestite con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eda71-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="eda71-122">Avvisi di sicurezza di Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="eda71-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="eda71-123">Questa vulnerabilità permette di identificare e risolvere gli avvisi sulle identità con privilegi all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eda71-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="eda71-124">tooenable utenti toocarry operazioni privilegiate, le organizzazioni devono toogrant utenti di accesso con privilegi temporanei o permanente in Azure AD, le risorse di Azure o Office 365 o altre applicazioni SaaS.</span><span class="sxs-lookup"><span data-stu-id="eda71-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="eda71-125">Ognuno di questi privilegi superficie di attacco hello aumenta gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="eda71-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="eda71-126">Questa vulnerabilità consente di identificare gli utenti con accesso con privilegi non necessario e richiedere l'azione appropriata tooreduce o eliminare il rischio di hello che comportano.</span><span class="sxs-lookup"><span data-stu-id="eda71-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="eda71-127">È consigliabile che l'organizzazione utilizza Azure AD Privileged Identity Management toomanage, controllo e le identità di monitoraggio privilegiato e tooresources loro accesso in Azure AD, nonché altri Microsoft online services quali Office 365 o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="eda71-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="eda71-128">Per altre informazioni, vedere [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="eda71-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="eda71-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="eda71-129">See also</span></span>
* [<span data-ttu-id="eda71-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="eda71-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

