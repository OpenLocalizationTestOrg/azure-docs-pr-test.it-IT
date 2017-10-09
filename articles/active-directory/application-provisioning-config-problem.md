---
title: configurazione applicazione raccolta tooan Azure AD di provisioning dell'utente aaaProblem | Documenti Microsoft
description: "Come i problemi comuni tootroubleshoot riscontrate durante la configurazione dell'applicazione tooan già nella raccolta di applicazioni hello Azure AD di provisioning dell'utente"
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Problema con la configurazione dell'applicazione raccolta tooan Azure AD di provisioning dell'utente

Configurazione [il provisioning utente automatico](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) per un'app (se supportato), richiede che un'applicazione hello tooprepare seguiti per il provisioning automatico istruzioni specifiche. È quindi possibile utilizzare hello tooconfigure portale Azure hello provisioning applicazione toohello gli account di servizio toosynchronize utente.

È sempre consigliabile iniziare cercando hello installazione esercitazione specifico toosetting di provisioning per l'applicazione. Seguire quindi tooconfigure tali passaggi entrambi app hello e Azure AD toocreate hello connessione provisioning. Un elenco di esercitazioni di app è reperibile in [elenco di esercitazioni sulla procedura tooIntegrate App SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Funzionamento toosee se il provisioning 

Una volta configurato il servizio di hello, la maggior parte delle informazioni dettagliate sui operazione hello del servizio hello possono essere recuperate dal due posizioni:

-   **Log di controllo** : hello provisioning record di log di controllo tutte le operazioni hello eseguite da hello provisioning del servizio, tra cui Azure AD per l'esecuzione di query assegnato agli utenti che si trovano nell'ambito per il provisioning. Applicazione di destinazione query hello esistenza hello di tali utenti, il confronto di oggetti utente hello tra sistema hello. Aggiungere, aggiornare o disabilitare l'account utente di hello nel sistema di destinazione hello in base a confronto hello. Hello provisioning i log di controllo sono accessibili nel portale di Azure in hello hello **Azure Active Directory &gt; le app aziendali &gt; \[nome applicazione\] &gt; log di controllo**scheda. Hello filtro accede hello **Provisioning Account** tooonly categoria vedere hello provisioning gli eventi per tale applicazione.

-   **Stato: provisioning** un riepilogo di provisioning ultimo hello di esecuzione per un'applicazione specificata è visibile nel hello **Azure Active Directory &gt; le app aziendali &gt; \[nome applicazione\] &gt; Provisioning** alla sezione, hello parte inferiore della schermata di hello in impostazioni di servizio hello. In questa sezione vengono riepilogati quanti utenti (e/o gruppi) siano eseguendo la sincronizzazione tra hello due sistemi, e se sono presenti errori. I dettagli dell'errore essere nei log di controllo hello. Si noti che lo stato di provisioning hello non popolato fino a quando non è stata completata una sincronizzazione iniziale completa tra Azure AD e app hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Problemi generali relativi al provisioning tooconsider

Di seguito è riportato un elenco di hello aree di problemi generali che è possibile analizzare se si dispone di un'idea toostart.

* [Provisioning del servizio non viene visualizzato toostart](#provisioning-service-does-not-appear-to-start)
* [Impossibile salvare la configurazione a causa di credenziali tooapp non funziona](#can’t-save-configuration-due-to-app-credentials-not-working)
* [I log di controllo indicano che gli utenti vengono "ignorati" e non sottoposti a provisioning, anche se assegnati](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Provisioning del servizio non viene visualizzato toostart

Se si imposta hello **lo stato di Provisioning** toobe **su** in hello **Azure Active Directory &gt; le app aziendali &gt; \[nomedell'applicazione\] &gt;Provisioning** sezione di hello portale di Azure. ma in seguito a successivi ricaricamenti non vengono visualizzati altri dettagli nella pagina, È probabile che il servizio di hello è in esecuzione ma non è stata completata una sincronizzazione iniziale ancora. Controllare hello **log di controllo** descritto in precedenza toodetermine sta eseguendo il tipo di servizio operazioni hello e se sono presenti errori.

>[!NOTE]
>Una sincronizzazione iniziale può richiedere ore tooseveral 20 minuti, a seconda delle dimensioni di hello della directory di Azure AD hello e il numero di hello di utenti nell'ambito per il provisioning. Le sincronizzazioni successive dopo la sincronizzazione iniziale di hello risultare più veloce, come hello provisioning servizio archivia le soglie che rappresentano lo stato di hello di entrambi i sistemi dopo la sincronizzazione iniziale hello, migliorando le prestazioni di sincronizzazioni successive.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Impossibile salvare la configurazione a causa di credenziali tooapp non funziona

Affinché toowork provisioning, Azure AD richiede credenziali valide che consentono la gestione degli utenti tooa tooconnect API fornite da tale app. Se queste credenziali non funzionano o non si conosce wat che sono, rivedere l'esercitazione hello per la configurazione di questa app, descritta in precedenza.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>I log di controllo indicano che gli utenti vengono ignorati e non sottoposti a provisioning, anche se assegnati

Quando un utente viene visualizzata come "ignorato" nei log di controllo di hello, è molto importante tooread hello dettagli nel motivo di hello log messaggio toodetermine hello estesi. Di seguito sono elencati i motivi e le risoluzioni comuni:

-   **È stato configurato un filtro di ambito** **che impediscano l'utente hello basata su un valore di attributo**. Per altre informazioni sui filtri di definizione dell'ambito, vedere <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **utente Hello è "non in modo efficace il diritto".** Se viene visualizzato questo messaggio di errore specifico, è perché si è verificato un problema con record di hello assegnazione utente archiviati in Azure AD. toofix questo problema, annullare l'assegnazione hello (utente o gruppo) da app hello e riassegnarlo nuovamente. Per altre informazioni sull'assegnazione, vedere <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Attributo obbligatorio mancante o non popolato per un utente.** Tooconsider una cosa importante quando l'impostazione di provisioning essere tooreview e configurare i mapping degli attributi hello e flussi di lavoro che definiscono quale flusso di proprietà utente (o gruppo) dall'applicazione toohello Azure AD. Ciò include l'impostazione di hello "proprietà corrispondente" che toouniquely utilizzati da identificare e corrisponde agli utenti o i gruppi tra i sistemi di hello due. Per altre informazioni su questo importante processo, vedere <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Attributo di mapping per i gruppi:** Provisioning di hello gruppo dettagli nomi e gruppi, membri toohello inoltre, se supportato per alcune applicazioni. È possibile abilitare o disabilitare questa funzionalità abilitando o disabilitando hello **Mapping** per oggetti di gruppo visualizzati nelle hello **Provisioning** scheda. Se è abilitato il provisioning di gruppi, prestare attenzione tooreview hello attributo mapping tooensure un campo appropriato viene utilizzato per hello "corrispondente di ID". Può trattarsi di alias di posta elettronica o nome visualizzato hello), come gruppo hello e i relativi membri non eseguirne il provisioning se hello corrispondente alla proprietà è vuoto o non è popolata per un gruppo in Azure AD.

#<a name="next-steps"></a>Passaggi successivi
[Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md)
