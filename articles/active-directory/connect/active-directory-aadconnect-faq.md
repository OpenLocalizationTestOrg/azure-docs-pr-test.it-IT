---
title: Domande frequenti su Azure Active Directory Connect | Documentazione Microsoft
description: Questa pagina contiene le domande frequenti su Azure AD Connect.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="5bbcc-103">Domande frequenti su Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="5bbcc-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="5bbcc-104">Installazione generale</span><span class="sxs-lookup"><span data-stu-id="5bbcc-104">General installation</span></span>
<span data-ttu-id="5bbcc-105">**D: installazione funzioneranno se hello amministratore globale di Azure AD ha 2FA abilitato?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="5bbcc-106">Con le compilazioni hello da febbraio 2016, questa è supportata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="5bbcc-107">**D: è presente un tooinstall modo Azure AD Connect automatica?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="5bbcc-108">È solo supportati tooinstall Azure AD Connect hello installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="5bbcc-109">L'installazione automatica e invisibile all'utente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="5bbcc-110">**D: Ho una foresta in cui un dominio non può essere contattato. Come installare Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="5bbcc-111">Con le compilazioni hello da febbraio 2016, questa è supportata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="5bbcc-112">**D: hello lavoro agente di integrità di dominio Active Directory in server core?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="5bbcc-113">Sì.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-113">Yes.</span></span> <span data-ttu-id="5bbcc-114">Dopo aver installato l'agente di hello, è possibile completare il processo di registrazione hello utilizzando hello cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="5bbcc-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="5bbcc-115">Rete</span><span class="sxs-lookup"><span data-stu-id="5bbcc-115">Network</span></span>
<span data-ttu-id="5bbcc-116">**D: ho un firewall, il dispositivo di rete o un'altra caratteristica che limita le connessioni di tempo massimo di hello può rimanere aperta sulla rete. Quanto deve durare la soglia di timeout lato client quando si utilizza Connetti AD Azure?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="5bbcc-117">Tutti i software di rete, dispositivi fisici o altri elementi che i limiti di tempo massimo di hello connessioni possono rimanere aperte deve utilizzare una soglia di almeno 5 minuti (300 secondi) per la connettività tra hello server in cui hello client di Azure AD Connect è installato e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="5bbcc-118">Questo vale anche gli strumenti di sincronizzazione di Microsoft Identity tooall rilasciate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="5bbcc-119">**D: I domini SDL sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="5bbcc-120">No, Azure AD Connect non supporta foreste/domini in locale mediante i domini SLD.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="5bbcc-121">**D: Gli elementi denominati NetBios con "punti" sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="5bbcc-122">No, Azure AD Connect non supporta locale foreste o domini in cui il nome NetBios hello contiene un punto "." nel nome hello.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="5bbcc-123">Federazione</span><span class="sxs-lookup"><span data-stu-id="5bbcc-123">Federation</span></span>
<span data-ttu-id="5bbcc-124">**D: cosa fare se viene visualizzato un messaggio di posta elettronica che chiedere toorenew certificato Office 365**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="5bbcc-125">Utilizzare le linee guida hello descritta in hello [rinnovare i certificati](active-directory-aadconnect-o365-certs.md) argomento su come toorenew hello certificato.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="5bbcc-126">**D: L'opzione di aggiornamento automatico della relying party è impostata per la relying party Office 365. È necessario tootake alcuna azione quando il certificato di firma automaticamente il token rollover?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="5bbcc-127">Utilizzare le linee guida hello descritta nell'articolo hello [rinnovare i certificati](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="5bbcc-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="5bbcc-128">Environment</span><span class="sxs-lookup"><span data-stu-id="5bbcc-128">Environment</span></span>
<span data-ttu-id="5bbcc-129">**D: è supportato it toorename hello server dopo l'installazione di Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="5bbcc-130">No.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-130">No.</span></span> <span data-ttu-id="5bbcc-131">Modifica del nome di server hello causa hello sincronizzazione motore toonot sarà in grado di tooconnect toohello SQL database e il servizio di hello non sarà in grado di toostart.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="5bbcc-132">Dati di identità</span><span class="sxs-lookup"><span data-stu-id="5bbcc-132">Identity data</span></span>
<span data-ttu-id="5bbcc-133">**D: hello l'attributo UPN (userPrincipalName) in Azure AD non corrisponde hello UPN locale - perché?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="5bbcc-134">Vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="5bbcc-134">See these articles:</span></span>

* [<span data-ttu-id="5bbcc-135">I nomi utente non corrispondono in Office 365, Azure o Intune hello UPN locale o ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="5bbcc-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="5bbcc-136">Le modifiche non sono sincronizzate dallo strumento di sincronizzazione di Azure Active Directory hello dopo aver modificato hello UPN di un toouse di account utente diverso dominio federato</span><span class="sxs-lookup"><span data-stu-id="5bbcc-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="5bbcc-137">È inoltre possibile configurare Azure AD tooallow hello sincronizzazione motore tooupdate hello userPrincipalName come descritto in [funzionalità servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="5bbcc-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="5bbcc-138">**D: sono supportato it toosoft corrispondenza locale oggetti di gruppo o contatto di Active Directory con gli oggetti di Azure AD/contatto del gruppo esistente?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="5bbcc-139">No, attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-139">No, this is currently not supported.</span></span>

<span data-ttu-id="5bbcc-140">**D: è supportato it toomanually impostare l'attributo ImmutableId in Azure AD gruppo o contatto esistente toohard oggetti corrispondenti tooon locale oggetti gruppo di Active Directory/contatto?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="5bbcc-141">No, attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="5bbcc-142">Configurazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="5bbcc-142">Custom configuration</span></span>
<span data-ttu-id="5bbcc-143">**D: dove sono hello i cmdlet di PowerShell per Azure AD Connect documentato?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="5bbcc-144">Con l'eccezione di hello dei cmdlet hello documentati in questo sito, altri cmdlet di PowerShell trovato in Azure AD Connect non sono supportati per l'utilizzo di cliente.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="5bbcc-145">**D: è possibile utilizzare "Server di esportazione/importazione Server" trovato nel *Synchronization Service Manager* toomove configurazione tra i server?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="5bbcc-146">No.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-146">No.</span></span> <span data-ttu-id="5bbcc-147">Questa opzione non recupererà tutte le impostazioni di configurazione e non deve essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="5bbcc-148">È necessario invece utilizzare configurazione base hello toocreate guidata hello nel secondo server hello e hello editor di regola di sincronizzazione toogenerate toomove di script di PowerShell qualsiasi regola personalizzata tra i server.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="5bbcc-149">Vedere [Migrazione swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="5bbcc-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="5bbcc-150">**D: è possibile password essere memorizzati nella cache per la pagina hello Accedi Azure e questo è possibile evitare poiché contiene un elemento input di password con completamento automatico hello = "false" attributo?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="5bbcc-151">Attualmente non è supportata la modifica degli attributi HTML hello del campo di immissione Password hello, inclusi i tag di completamento automatico hello.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="5bbcc-152">Sono attualmente una funzionalità che consentono di Javascript personalizzato che consentirà tooadd tutti i campi password toohello attributo.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="5bbcc-153">Dovrebbe essere disponibile più avanti nel 2017.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="5bbcc-154">**D: in hello Azure nella pagina di accesso, vengono visualizzati i nomi utente per gli utenti che hanno già effettuato l'accesso correttamente.  Questo comportamento può essere disattivato?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="5bbcc-155">Attualmente non è supportata la modifica degli attributi HTML hello di hello nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="5bbcc-156">Sono attualmente una funzionalità che consentono di Javascript personalizzato che consentirà tooadd tutti i campi password toohello attributo.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="5bbcc-157">Dovrebbe essere disponibile più avanti nel 2017.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="5bbcc-158">**D: è un modo tooprevent sessioni simultanee?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="5bbcc-159">No.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="5bbcc-160">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="5bbcc-160">Troubleshooting</span></span>
<span data-ttu-id="5bbcc-161">**D: Come è possibile ottenere informazioni su Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="5bbcc-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="5bbcc-162">Hello ricerca Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="5bbcc-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="5bbcc-163">Hello di ricerca Microsoft Knowledge Base (KB) per i problemi di riparazione toocommon soluzioni ai problemi tecnici sul supporto per Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="5bbcc-164">Forum di Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bbcc-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="5bbcc-165">È possibile cercare e visualizzare per la technical domande e risposte dalla community di hello o porre una domanda facendo [qui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="5bbcc-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="5bbcc-166">Assistenza clienti per Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5bbcc-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="5bbcc-167">Usare questo supporto tooget collegamento tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5bbcc-167">Use this link tooget support through hello Azure portal.</span></span>

