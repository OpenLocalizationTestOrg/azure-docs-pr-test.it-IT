---
title: "Sicurezza delle password a più livelli di Azure AD | Microsoft Docs"
description: Questo articolo spiega in che modo Azure AD applica le password complesse e protegge le password degli utenti dai criminali informatici.
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="ac17a-103">Approccio multilivello alla sicurezza delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac17a-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="ac17a-104">Questo articolo illustra alcune procedure consigliate che è possibile seguire come utente o amministratore per proteggere il proprio account Azure Active Directory (Azure AD) o Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac17a-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="ac17a-105">Gli amministratori di Azure Active Directory possono reimpostare le password degli utenti seguendo le indicazioni fornite nell'articolo [Reimpostare la password per un utente in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac17a-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="ac17a-106">Gli utenti possono reimpostare la propria password seguendo le indicazioni fornite nell'articolo [Password di Azure AD dimenticata](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="ac17a-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="ac17a-107">Requisiti delle password</span><span class="sxs-lookup"><span data-stu-id="ac17a-107">Password requirements</span></span>

<span data-ttu-id="ac17a-108">Azure AD adotta i seguenti approcci comuni per la protezione delle password:</span><span class="sxs-lookup"><span data-stu-id="ac17a-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="ac17a-109">Requisiti di lunghezza delle password</span><span class="sxs-lookup"><span data-stu-id="ac17a-109">Password length requirements</span></span>
* <span data-ttu-id="ac17a-110">Requisiti di complessità delle password</span><span class="sxs-lookup"><span data-stu-id="ac17a-110">Password complexity requirements</span></span>
* <span data-ttu-id="ac17a-111">Scadenza regolare e periodica delle password</span><span class="sxs-lookup"><span data-stu-id="ac17a-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="ac17a-112">Per informazioni sulla reimpostazione delle password in Azure Active Directory, vedere l'argomento [Reimpostazione self-service delle password di Azure AD per i professionisti IT](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="ac17a-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="ac17a-113">Protezione delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac17a-113">Azure AD password protections</span></span>

<span data-ttu-id="ac17a-114">Azure AD e il sistema di account Microsoft usano approcci di settore comprovati per assicurare la protezione delle password di utenti e amministratori, tra cui:</span><span class="sxs-lookup"><span data-stu-id="ac17a-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="ac17a-115">Password vietate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="ac17a-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="ac17a-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="ac17a-116">Smart Password Lockout</span></span>

<span data-ttu-id="ac17a-117">Per informazioni sulla gestione delle password in base alla ricerca corrente, vedere il white paper contenente le [indicazioni sulle password](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="ac17a-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="ac17a-118">Password vietate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="ac17a-118">Dynamically banned passwords</span></span>

<span data-ttu-id="ac17a-119">Azure AD e il sistema di account Microsoft salvaguardano la protezione delle password vietando in modo dinamico le password usate comunemente.</span><span class="sxs-lookup"><span data-stu-id="ac17a-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="ac17a-120">Il team di Azure AD Identity Protection analizza periodicamente gli elenchi delle password vietate, impedendo agli utenti di selezionare le password usate comunemente.</span><span class="sxs-lookup"><span data-stu-id="ac17a-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="ac17a-121">Questo servizio è disponibile in Azure AD e per i clienti del servizio account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac17a-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="ac17a-122">Quando si creano password, è importante che gli amministratori invitino gli utenti a scegliere passphrase che includano una combinazione univoca di lettere, numeri, caratteri o parole.</span><span class="sxs-lookup"><span data-stu-id="ac17a-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="ac17a-123">Questo approccio contribuisce a rendere quasi impossibile il rischio di compromissione delle password degli utenti e allo stesso tempo le rende più facili da ricordare.</span><span class="sxs-lookup"><span data-stu-id="ac17a-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="ac17a-124">Violazioni delle password</span><span class="sxs-lookup"><span data-stu-id="ac17a-124">Password breaches</span></span>

<span data-ttu-id="ac17a-125">Microsoft cerca sempre di anticipare le mosse dei criminali informatici.</span><span class="sxs-lookup"><span data-stu-id="ac17a-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="ac17a-126">Il team di Azure AD Identity Protection analizza costantemente le password più comuni.</span><span class="sxs-lookup"><span data-stu-id="ac17a-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="ac17a-127">Anche i criminali informatici usano strategie simili per gli attacchi, ad esempio creando un [tabella arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table) per violare gli hash delle password.</span><span class="sxs-lookup"><span data-stu-id="ac17a-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="ac17a-128">Microsoft analizza continuamente le [violazioni di dati](https://www.privacyrights.org/data-breaches) per mantenere un elenco di password da vietare aggiornato in modo dinamico che assicura l'esclusione delle password vulnerabili prima che diventino una minaccia reale per i clienti di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac17a-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="ac17a-129">Per altre informazioni sulle attività volte a garantire la sicurezza, vedere il [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac17a-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="ac17a-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="ac17a-130">Smart Password Lockout</span></span>

<span data-ttu-id="ac17a-131">Quando Azure AD rileva un potenziale criminale informatico che prova a violare una password utente, l'account utente viene bloccato con Smart Password Lockout.</span><span class="sxs-lookup"><span data-stu-id="ac17a-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="ac17a-132">Azure AD è progettato per determinare i rischi associati a sessioni di accesso specifiche.</span><span class="sxs-lookup"><span data-stu-id="ac17a-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="ac17a-133">Usando i dati di sicurezza più aggiornati, Microsoft applica quindi la semantica di blocco alle minacce informatiche.</span><span class="sxs-lookup"><span data-stu-id="ac17a-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="ac17a-134">Se un utente viene bloccato da Azure AD, la schermata sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="ac17a-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Bloccato da Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="ac17a-136">Per altri account Microsoft, la schermata sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="ac17a-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Bloccato da un account Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="ac17a-138">Per informazioni sulla reimpostazione delle password in Azure Active Directory, vedere l'argomento [Reimpostazione self-service delle password di Azure AD per i professionisti IT](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="ac17a-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="ac17a-139">Se si è amministratori di Azure AD è consigliabile usare [Windows Hello](https://www.microsoft.com/windows/windows-hello) per evitare che gli utenti creino password tradizionali.</span><span class="sxs-lookup"><span data-stu-id="ac17a-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="ac17a-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac17a-140">Next steps</span></span>

* [<span data-ttu-id="ac17a-141">Come aggiornare la password</span><span class="sxs-lookup"><span data-stu-id="ac17a-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="ac17a-142">Concetti fondamentali sulla gestione delle identità di Azure</span><span class="sxs-lookup"><span data-stu-id="ac17a-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="ac17a-143">Rapporto sull'attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="ac17a-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


