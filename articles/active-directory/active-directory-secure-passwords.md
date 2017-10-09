---
title: "aaaAzure Active Directory a più livelli di protezione delle password | Documenti Microsoft"
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
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="4bef5-103">Protezione delle password tooAzure AD un approccio a più livelli</span><span class="sxs-lookup"><span data-stu-id="4bef5-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="4bef5-104">In questo articolo vengono illustrate alcune procedure consigliate è possibile seguire come un utente o un amministratore tooprotect l'Account di Microsoft o di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4bef5-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="4bef5-105">Gli amministratori di Azure AD possono reimpostare le password utente utilizzando istruzioni hello nell'articolo hello [hello di reimpostazione password per un utente in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4bef5-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="4bef5-106">Gli utenti possono reimpostare le proprie password tramite istruzioni hello nell'articolo hello [Guida ho dimenticato la password di Azure AD](active-directory-passwords-update-your-own-password.md).</span><span class="sxs-lookup"><span data-stu-id="4bef5-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="4bef5-107">Requisiti delle password</span><span class="sxs-lookup"><span data-stu-id="4bef5-107">Password requirements</span></span>

<span data-ttu-id="4bef5-108">Azure AD incorpora hello password toosecuring di approcci comuni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4bef5-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="4bef5-109">Requisiti di lunghezza delle password</span><span class="sxs-lookup"><span data-stu-id="4bef5-109">Password length requirements</span></span>
* <span data-ttu-id="4bef5-110">Requisiti di complessità delle password</span><span class="sxs-lookup"><span data-stu-id="4bef5-110">Password complexity requirements</span></span>
* <span data-ttu-id="4bef5-111">Scadenza regolare e periodica delle password</span><span class="sxs-lookup"><span data-stu-id="4bef5-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="4bef5-112">Per informazioni su reimpostare la password in Azure Active Directory, vedere l'argomento hello [AD Azure self-service la reimpostazione della password per i professionisti IT hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="4bef5-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="4bef5-113">Protezione delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4bef5-113">Azure AD password protections</span></span>

<span data-ttu-id="4bef5-114">Azure AD e sistema di Account Microsoft utilizzare settore rivelato hello si avvicina tooensure protezione sicura della password utente e amministratore, che includono:</span><span class="sxs-lookup"><span data-stu-id="4bef5-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="4bef5-115">Password vietate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="4bef5-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="4bef5-116">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="4bef5-116">Smart Password Lockout</span></span>

<span data-ttu-id="4bef5-117">Per informazioni sulla gestione delle password in base alle ricerche corrente, vedere il white paper hello [indicazioni Password](http://aka.ms/passwordguidance).</span><span class="sxs-lookup"><span data-stu-id="4bef5-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="4bef5-118">Password vietate in modo dinamico</span><span class="sxs-lookup"><span data-stu-id="4bef5-118">Dynamically banned passwords</span></span>

<span data-ttu-id="4bef5-119">Azure AD e il sistema di account Microsoft salvaguardano la protezione delle password vietando in modo dinamico le password usate comunemente.</span><span class="sxs-lookup"><span data-stu-id="4bef5-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="4bef5-120">il team di protezione dell'identità di Azure ID Hello analizza regolarmente gli elenchi di password escluso, impedendo agli utenti di selezione di password usate comunemente.</span><span class="sxs-lookup"><span data-stu-id="4bef5-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="4bef5-121">Questo servizio è disponibile tooAzure AD e clienti del servizio di Account Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="4bef5-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="4bef5-122">Durante la creazione di password, è importante per gli amministratori tooencourage utenti toochoose password frasi che includono una combinazione univoca di lettere, numeri, caratteri o parole.</span><span class="sxs-lookup"><span data-stu-id="4bef5-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="4bef5-123">Questo approccio consente le password utente toomake toobe praticamente compromesso ma più semplice per gli utenti tooremember.</span><span class="sxs-lookup"><span data-stu-id="4bef5-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="4bef5-124">Violazioni delle password</span><span class="sxs-lookup"><span data-stu-id="4bef5-124">Password breaches</span></span>

<span data-ttu-id="4bef5-125">Microsoft sta sempre toostay un unico passaggio precedono criminali informatici.</span><span class="sxs-lookup"><span data-stu-id="4bef5-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="4bef5-126">il team di Azure AD Identity Protection Hello analizza continuamente le password utilizzati di frequente.</span><span class="sxs-lookup"><span data-stu-id="4bef5-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="4bef5-127">Criminali informatici inoltre utilizzano simile strategie tooinform gli attacchi, ad esempio creazione un' [tabella arcobaleno](https://en.wikipedia.org/wiki/Rainbow_table) per violare gli hash delle password.</span><span class="sxs-lookup"><span data-stu-id="4bef5-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="4bef5-128">Microsoft analizza continuamente [violazioni dati](https://www.privacyrights.org/data-breaches) toomaintain un elenco aggiornato in modo dinamico la password da escludere, che assicura che le password vulnerabili vengono escluse prima che diventino un reale minaccia clienti tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4bef5-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="4bef5-129">Per ulteriori informazioni sull'impegno di sicurezza corrente, vedere hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="4bef5-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="4bef5-130">Smart Password Lockout</span><span class="sxs-lookup"><span data-stu-id="4bef5-130">Smart Password Lockout</span></span>

<span data-ttu-id="4bef5-131">Quando Azure Active Directory rileva una potenziale toohack durante il tentativo di informatica penali in una password utente, si blocca account utente di hello con blocco Password Smart.</span><span class="sxs-lookup"><span data-stu-id="4bef5-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="4bef5-132">Azure AD viene progettato il rischio di hello toodetermine associato alle sessioni di accesso specifico.</span><span class="sxs-lookup"><span data-stu-id="4bef5-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="4bef5-133">Quindi l'uso di dati di sicurezza più aggiornati hello, si applicano minacce cyber toostop semantica di blocco.</span><span class="sxs-lookup"><span data-stu-id="4bef5-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="4bef5-134">Se un utente è bloccato da Azure AD, la schermata appare simile toohello uno che segue:</span><span class="sxs-lookup"><span data-stu-id="4bef5-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Bloccato da Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="4bef5-136">Per gli altri account Microsoft, la schermata appare simile toohello uno che segue:</span><span class="sxs-lookup"><span data-stu-id="4bef5-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Bloccato da un account Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="4bef5-138">Per informazioni su reimpostare la password in Azure Active Directory, vedere l'argomento hello [AD Azure self-service la reimpostazione della password per i professionisti IT hello](active-directory-passwords.md).</span><span class="sxs-lookup"><span data-stu-id="4bef5-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="4bef5-139">Se si è un amministratore di Azure AD, è opportuno toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid con gli utenti di creare password tradizionali completamente.</span><span class="sxs-lookup"><span data-stu-id="4bef5-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="4bef5-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bef5-140">Next steps</span></span>

* [<span data-ttu-id="4bef5-141">Come tooupdate la propria password</span><span class="sxs-lookup"><span data-stu-id="4bef5-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="4bef5-142">Nozioni fondamentali su Hello della gestione delle identità di Azure</span><span class="sxs-lookup"><span data-stu-id="4bef5-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="4bef5-143">Rapporto sull'attività di reimpostazione password</span><span class="sxs-lookup"><span data-stu-id="4bef5-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


