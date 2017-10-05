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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="e6af5-103">Domande frequenti su Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="e6af5-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="e6af5-104">Installazione generale</span><span class="sxs-lookup"><span data-stu-id="e6af5-104">General installation</span></span>
<span data-ttu-id="e6af5-105">**D: L'installazione verrà eseguita correttamente se per l'amministratore globale di Active Directory Azure è abilitata l'autenticazione a due fattori?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="e6af5-106">Questa opzione è supportata nelle build rilasciate a partire da febbraio 2016.</span><span class="sxs-lookup"><span data-stu-id="e6af5-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="e6af5-107">**D: Esiste un modo per eseguire l'installazione automatica di Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="e6af5-108">È supportata solo l'installazione di Azure AD Connect tramite l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="e6af5-109">L'installazione automatica e invisibile all'utente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="e6af5-110">**D: Ho una foresta in cui un dominio non può essere contattato. Come installare Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="e6af5-111">Questa opzione è supportata nelle build rilasciate a partire da febbraio 2016.</span><span class="sxs-lookup"><span data-stu-id="e6af5-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="e6af5-112">**D: L'agente di integrità di AD DS funziona su Server Core?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="e6af5-113">Sì.</span><span class="sxs-lookup"><span data-stu-id="e6af5-113">Yes.</span></span> <span data-ttu-id="e6af5-114">Dopo aver installato l'agente, è possibile completare il processo di registrazione con il cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="e6af5-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="e6af5-115">Rete</span><span class="sxs-lookup"><span data-stu-id="e6af5-115">Network</span></span>
<span data-ttu-id="e6af5-116">**D: Ho un firewall, un dispositivo di rete o qualcos'altro che limita il tempo massimo in cui le connessioni possono rimanere aperte sulla mia rete. Quanto deve durare la soglia di timeout lato client quando si utilizza Connetti AD Azure?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="e6af5-117">Tutti i software di rete, i dispositivi fisici o qualsiasi altra cosa che limiti il tempo massimo delle connessioni possono rimanere aperti qualora si utilizzi una soglia di almeno 5 minuti (300 secondi) per la connettività tra il server in cui è installato il client AD Azure Connect e la Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e6af5-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="e6af5-118">Questo vale anche per tutti gli strumenti di sincronizzazione Microsoft Identity rilasciati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e6af5-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="e6af5-119">**D: I domini SDL sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="e6af5-120">No, Azure AD Connect non supporta foreste/domini in locale mediante i domini SLD.</span><span class="sxs-lookup"><span data-stu-id="e6af5-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="e6af5-121">**D: Gli elementi denominati NetBios con "punti" sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="e6af5-122">No, Azure AD Connect non supporta foreste/domini in locale il cui nome NetBios contenga un periodo "." nel nome.</span><span class="sxs-lookup"><span data-stu-id="e6af5-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="e6af5-123">Federazione</span><span class="sxs-lookup"><span data-stu-id="e6af5-123">Federation</span></span>
<span data-ttu-id="e6af5-124">**D: Cosa occorre fare se si riceve un messaggio di posta elettronica che richiede il rinnovo del certificato di Office 365?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="e6af5-125">Usare le indicazioni specifiche disponibili nell'argomento che spiega come [rinnovare i certificati](active-directory-aadconnect-o365-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="e6af5-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="e6af5-126">**D: L'opzione di aggiornamento automatico della relying party è impostata per la relying party Office 365. È necessario eseguire un'azione quando il certificato per la firma di token esegue automaticamente il rollover?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="e6af5-127">Usare le linee guida descritte nell'articolo relativo al [rinnovare i certificati](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="e6af5-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="e6af5-128">Environment</span><span class="sxs-lookup"><span data-stu-id="e6af5-128">Environment</span></span>
<span data-ttu-id="e6af5-129">**D: Il fatto di rinominare il server dopo l'installazione di Azure AD Connect è supportato?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="e6af5-130">No.</span><span class="sxs-lookup"><span data-stu-id="e6af5-130">No.</span></span> <span data-ttu-id="e6af5-131">La modifica del nome del server farà sì che il motore di sincronizzazione no sia in grado di connettersi al database SQL e il servizio non riuscirà ad avviarsi.</span><span class="sxs-lookup"><span data-stu-id="e6af5-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="e6af5-132">Dati di identità</span><span class="sxs-lookup"><span data-stu-id="e6af5-132">Identity data</span></span>
<span data-ttu-id="e6af5-133">**D: Perché l'attributo UPN (userPrincipalName) in Azure AD non corrisponde con l'UPN locale?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="e6af5-134">Vedere i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="e6af5-134">See these articles:</span></span>

* [<span data-ttu-id="e6af5-135">I nomi utente in Office 365, Azure o Intune non corrispondono agli ID di accesso o alternativi dell'UPN locale</span><span class="sxs-lookup"><span data-stu-id="e6af5-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="e6af5-136">Le modifiche non sono sincronizzate dallo strumento di sincronizzazione di Azure Active Directory dopo aver modificato l'UPN di un account utente per usare un dominio federato diverso</span><span class="sxs-lookup"><span data-stu-id="e6af5-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="e6af5-137">È anche possibile configurare Azure AD per consentire al motore di sincronizzazione di aggiornare userPrincipalName come descritto in [Funzionalità del servizio di sincronizzazione di Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="e6af5-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="e6af5-138">**D: È supportata la corrispondenza flessibile degli oggetti contatto/gruppo AD locali con gli oggetti contatto/gruppo Azure AD esistenti?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="e6af5-139">No, attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-139">No, this is currently not supported.</span></span>

<span data-ttu-id="e6af5-140">**D: È supportata l'impostazione manualmente dell'attributo ImmutableId su oggetti contatto/gruppo Azure AD esistenti per farlo corrispondere a livello rigido a oggetti contatto/gruppo AD locali?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="e6af5-141">No, attualmente non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="e6af5-142">Configurazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="e6af5-142">Custom configuration</span></span>
<span data-ttu-id="e6af5-143">**D: Dove sono documentati i cmdlet PowerShell per Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="e6af5-144">Fatta eccezione per i cmdlet documentati in questo sito, gli altri cmdlet di PowerShell disponibili in Azure AD Connect di non sono supportati per l'utilizzo da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="e6af5-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="e6af5-145">**D: Si può usare l'opzione "Server export/server import" disponibile in *Synchronization Service Manager* per spostare la configurazione tra i server?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="e6af5-146">No.</span><span class="sxs-lookup"><span data-stu-id="e6af5-146">No.</span></span> <span data-ttu-id="e6af5-147">Questa opzione non recupererà tutte le impostazioni di configurazione e non deve essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="e6af5-148">Si dovrebbe invece utilizzare la procedura guidata per creare la configurazione di base sul secondo server e usare l'editor delle regole di sincronizzazione per generare script di PowerShell per spostare qualsiasi regola personalizzata tra i server.</span><span class="sxs-lookup"><span data-stu-id="e6af5-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="e6af5-149">Vedere [Migrazione swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="e6af5-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="e6af5-150">**D: Le password per la pagina di accesso di Azure possono essere memorizzate nella cache; è possibile evitare questa condizione poiché contiene un elemento di input della password impostando l'attributo della funzionalità di completamento automatico = "false"?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="e6af5-151">Attualmente la modifica degli attributi HTML del campo di input della password non è supportata, incluso il tag di completamento automatico.</span><span class="sxs-lookup"><span data-stu-id="e6af5-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="e6af5-152">Attualmente è in fase di elaborazione una funzionalità che consente un JavaScript personalizzato con cui è possibile aggiungere qualsiasi attributo al campo della password.</span><span class="sxs-lookup"><span data-stu-id="e6af5-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="e6af5-153">Dovrebbe essere disponibile più avanti nel 2017.</span><span class="sxs-lookup"><span data-stu-id="e6af5-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="e6af5-154">**D: Nella pagina di accesso di Azure vengono visualizzati i nomi utente per gli utenti che hanno già eseguito l'accesso correttamente.  Questo comportamento può essere disattivato?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="e6af5-155">Attualmente la modifica degli attributi HTML della pagina di accesso non è supportata.</span><span class="sxs-lookup"><span data-stu-id="e6af5-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="e6af5-156">Attualmente è in fase di elaborazione una funzionalità che consente un JavaScript personalizzato con cui è possibile aggiungere qualsiasi attributo al campo della password.</span><span class="sxs-lookup"><span data-stu-id="e6af5-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="e6af5-157">Dovrebbe essere disponibile più avanti nel 2017.</span><span class="sxs-lookup"><span data-stu-id="e6af5-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="e6af5-158">**D: Esiste un modo per impedire sessioni simultanee?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="e6af5-159">No.</span><span class="sxs-lookup"><span data-stu-id="e6af5-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="e6af5-160">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e6af5-160">Troubleshooting</span></span>
<span data-ttu-id="e6af5-161">**D: Come è possibile ottenere informazioni su Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="e6af5-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="e6af5-162">Ricercare nella Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="e6af5-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="e6af5-163">Cercare nella Microsoft Knowledge Base (KB) soluzioni tecniche per problemi comuni in garanzia riguardanti il supporto per Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e6af5-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="e6af5-164">Forum di Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6af5-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="e6af5-165">Per cercare e passare in rassegna domande e risposte tecniche della community o porre domande, fare clic [qui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="e6af5-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="e6af5-166">Assistenza clienti per Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="e6af5-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="e6af5-167">Usare questo collegamento per ottenere assistenza tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6af5-167">Use this link to get support through the Azure portal.</span></span>

