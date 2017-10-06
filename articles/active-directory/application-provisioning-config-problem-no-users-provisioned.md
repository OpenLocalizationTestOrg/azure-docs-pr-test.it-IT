---
title: gli utenti aaaNo vengono applicazione raccolta tooan provisioning Azure AD | Documenti Microsoft
description: "Come i problemi comuni tootroubleshoot riscontrate quando non vengono visualizzati gli utenti visualizzati in una Azure Active Directory dell'applicazione di raccolta è stato configurato per il provisioning utente con Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Nessun utente vengono applicazione raccolta tooan provisioning Azure AD

Il provisioning automatico di una volta configurato per un'applicazione (inclusa la verifica che le credenziali di app hello fornito AD tooAzure tooconnect toohello app sono validi). Gli utenti e/o i gruppi sono app toohello provisioning ed è determinato dal hello seguenti operazioni:

-   Cui utenti e gruppi sono state **assegnato** toohello applicazione. Per ulteriori informazioni sull'assegnazione, vedere [assegnare un'applicazione aziendale tooan utente o gruppo in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   O meno **attributo mapping** sono gli attributi validi toosync abilitato e configurato da Azure AD toohello app. Per altre informazioni sui mapping degli attributi, vedere [Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Presenza o meno di un **filtro per la definizione dell'ambito** che filtri gli utenti in base a specifici valori di attributo. Per altre informazioni sui filtri di ambito, vedere [Provisioning dell'applicazione basato su attributi con filtri per la definizione dell'ambito](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Quando si osserva che gli utenti non provisioning in corso, consultare i log di controllo hello in Azure AD e cercare le voci di log per un utente specifico.

Hello provisioning i log di controllo sono accessibili nel portale di Azure in hello hello **Azure Active Directory &gt; le app aziendali &gt; \[nome applicazione\] &gt; log di controllo**scheda. Hello filtro accede hello **Provisioning Account** tooonly categoria vedere hello provisioning gli eventi per tale applicazione. È possibile cercare utenti basati su hello "corrispondenti all'ID" che è stato configurato per tali mapping degli attributi di hello. Ad esempio, se è stato configurato hello "nome dell'entità utente" o "indirizzo di posta elettronica" come hello corrispondenti all'attributo sul lato di hello Azure AD, e non da il provisioning degli utenti hello ha un valore di "audrey@contoso.com". Quindi eseguire ricerche nei log di controllo hello per "audrey@contoso.com" e rivedere quindi voci restituite.

Hello provisioning controllo Registra record di che tutte le operazioni eseguite dal servizio di provisioning di hello, inclusi l'interrogazione di Azure AD per gli utenti assegnati che rientrano nell'ambito per il provisioning, applicazione di destinazione hello esistenza hello di tali utenti l'esecuzione di query, il confronto hello di hello oggetti utente tra il sistema hello. Aggiungere, aggiornare o disabilitare l'account utente di hello nel sistema di destinazione hello in base a confronto hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Aree problematiche generali relativi al Provisioning tooconsider

Di seguito è riportato un elenco di hello aree di problemi generali che è possibile analizzare se si dispone di un'idea toostart.

* [Provisioning del servizio non viene visualizzato toostart](#provisioning-service-does-not-appear-to-start)
* [I log di controllo indicano che gli utenti vengono ignorati e non sottoposti a provisioning, anche se assegnati](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Provisioning del servizio non viene visualizzato toostart

Se si imposta hello **lo stato di Provisioning** toobe **su** in hello **Azure Active Directory &gt; le app aziendali &gt; \[nomedell'applicazione\] &gt;Provisioning** sezione di hello portale di Azure. Tuttavia nessun altro stato dettagli vengono visualizzati nella pagina dopo Ricarica successive, è probabile che il servizio di hello è in esecuzione ma non è stata completata una sincronizzazione iniziale è ancora. Controllare hello **log di controllo** descritto in precedenza toodetermine sta eseguendo il tipo di servizio operazioni hello e se sono presenti errori.

>[!NOTE]
>Una sincronizzazione iniziale può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello della directory di Azure AD hello e il numero di hello di utenti nell'ambito per il provisioning. Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello sono più veloci, come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale di hello. migliorando le prestazioni delle sincronizzazioni successive.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>I log di controllo indicano che gli utenti vengono ignorati e non sottoposti a provisioning, anche se assegnati

Quando un utente viene visualizzata come "ignorato" nei log di controllo di hello, è molto importante tooread hello dettagli nel motivo di hello log messaggio toodetermine hello estesi. Di seguito sono elencati i motivi e le risoluzioni comuni:

-   **È stato configurato un filtro di ambito** **che impediscano l'utente hello basata su un valore di attributo**. Per altre informazioni sui filtri di definizione dell'ambito, vedere <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **utente Hello è "non in modo efficace il diritto".** Se viene visualizzato questo messaggio di errore specifico, è perché si è verificato un problema con record di hello assegnazione utente archiviati in Azure AD. toofix questo problema, annullare l'assegnazione hello (utente o gruppo) da app hello e riassegnarlo nuovamente. Per altre informazioni sull'assegnazione, vedere <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Attributo obbligatorio mancante o non popolato per un utente.** Tooconsider una cosa importante quando l'impostazione di provisioning essere tooreview e configurare i mapping degli attributi hello e flussi di lavoro che definiscono quale flusso di proprietà utente (o gruppo) dall'applicazione toohello Azure AD. Ciò include l'impostazione di hello "proprietà corrispondente" che toouniquely utilizzati da identificare e corrisponde agli utenti o i gruppi tra i sistemi di hello due. Per altre informazioni su questo importante processo, vedere [Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Attributo di mapping per i gruppi:** Provisioning di hello gruppo dettagli nomi e gruppi, membri toohello inoltre, se supportato per alcune applicazioni. È possibile abilitare o disabilitare questa funzionalità abilitando o disabilitando hello **Mapping** per oggetti di gruppo visualizzati nelle hello **Provisioning** scheda. Se è abilitato il provisioning di gruppi, prestare attenzione tooreview hello attributo mapping tooensure un campo appropriato viene utilizzato per hello "corrispondente di ID". Può trattarsi di alias di posta elettronica o nome visualizzato hello), come gruppo hello e i relativi membri non eseguirne il provisioning se hello corrispondente alla proprietà è vuoto o non è popolata per un gruppo in Azure AD.

## <a name="next-steps"></a>Passaggi successivi
[Servizio di sincronizzazione Azure AD Connect: informazioni sul provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

