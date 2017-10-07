---
title: aaaManaging tooapps di accesso con Azure AD | Documenti Microsoft
description: Viene descritto come Azure Active Directory consente alle organizzazioni toospecify hello App toowhich ogni utente dispone di accesso.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>La gestione di accesso tooapps
Gestione dell'accesso in corso, la valutazione di utilizzo e creazione di report continuare toobe una sfida dopo un'app è integrata nel sistema di identità dell'organizzazione. In molti casi, gli amministratori IT o il supporto tecnico presentano tootake un ruolo attivo in corso nella gestione delle App tooyour di accesso. In alcuni casi, l'assegnazione viene eseguita da un team IT generale o di reparto. È previsto toobe toohello delegata decisore aziendale, che richiedono approvazione prima rende IT spesso decisione assegnazione hello hello assegnazione.  Altre organizzazioni investono nell'integrazione mediante sistemi automatizzati esistenti di gestione dell'accesso e dell'identità, quali il controllo degli accessi in base al ruolo (RBAC) o il controllo degli accessi in base all'attributo (ABAC). Integrazione hello sia lo sviluppo di regola tendono toobe specializzate e costosa. Il monitoraggio o la creazione di report in entrambi gli approcci di gestione è di per sé un investimento isolato, complesso e costoso.

## <a name="how-does-azure-active-directory-help"></a>Quale contributo può offrire Azure Active Directory?
 Supporta l'ampio accesso gestione di Azure Active Directory per le applicazioni configurate, consentendo alle organizzazioni tooeasily ottenere criteri di diritti di accesso hello compreso tra l'assegnazione automatica, basato su attributi (scenari ABAC o RBAC) mediante la delega e incluso gestione amministratori. Con Azure AD è possibile facilmente ottenere criteri complessi, la combinazione di più modelli di gestione per una singola applicazione e possono anche usare nuovamente le regole di gestione tra le applicazioni con hello stessi gruppi di destinatari.

* [Aggiunta di applicazioni nuove o esistenti](active-directory-sso-integrate-saas-apps.md)

 L’assegnazione dell’applicazione di Azure AD riguarda due modalità di assegnazione primaria:

* **Singola assegnazione** IT un amministratore con autorizzazioni di amministratore globale directory è possibile selezionare singoli account utente e concedere l'accesso dell'applicazione toohello.
* **L'assegnazione basata su gruppo (solo Azure AD (a pagamento)** IT un amministratore con autorizzazioni di amministratore globale directory è possibile assegnare un'applicazione toohello di gruppo. Accesso a utenti specifici è determinato dal che se sono membri del gruppo di hello in fase di hello tentano di un'applicazione hello tooaccess. In altre parole, un amministratore può in modo efficace di creare una regola di assegnazione che indica "tutti i membri del gruppo assegnato hello ha accesso toohello applicazione". Con questa opzione di assegnazione, gli amministratori possono sfruttare le opzioni di gestione dei gruppi di Azure AD, tra cui [gruppi dinamici basati sugli attributi](active-directory-accessmanagement-manage-groups.md), gruppi di sistema esterno (ad esempio, Active Directory locale o Workday), gruppi gestiti dall'amministratore o in modalità self-service. Un singolo gruppo è possibile assegnare le app toomultiple, assicurandosi che le applicazioni con affinità assegnazione possono condividere le regole di assegnazione, la riduzione hello complessità di gestione globale. Tenere presente che gruppo nidificato appartenenze non sono supportate per l'assegnazione basata su gruppo tooapplications in questo momento.

Mediante queste due modalità di assegnazione, gli amministratori possono ottenere qualsiasi approccio di gestione delle assegnazioni.

Con Azure AD, utilizzo e creazione di report di assegnazione è completamente integrato, abilitazione di amministratori tooeasily report stato di assegnazione, gli errori di assegnazione, e anche l'utilizzo.

## <a name="complex-application-assignment-with-azure-ad"></a>Assegnazione di applicazioni complesse con Azure AD
Si tenga in considerazione un'applicazione come Salesforce. In molte organizzazioni, Salesforce viene principalmente utilizzato da organizzazioni di vendita e marketing hello. Spesso, i membri del team di marketing hello hanno privilegi elevati tooSalesforce di accesso, mentre i membri del team di vendita hello abbia accesso limitato. In molti casi, un ampio popolamento di information worker avere limitato accesso toohello applicazione. Le regole toothese eccezioni se non bastasse. Spesso è prerogativa hello hello marketing o di vendita leadership team toogrant un utente di accedere o modificare i ruoli in modo indipendente da queste regole generiche.

Con Azure AD, applicazioni come Salesforce possono essere preconfigurate per l'accesso Single Sign-On e il provisioning automatizzato. Dopo aver configurata un'applicazione hello, un amministratore può richiedere toocreate azione unica hello e assegnare gruppi appropriati hello. In questo esempio, un amministratore di eseguire hello seguenti assegnazioni:

* [Gruppi dinamici](active-directory-accessmanagement-manage-groups.md) può essere definito tooautomatically rappresentare tutti i membri del team di vendita e marketing di hello usando attributi quali reparto o ruolo:
  
  * Tutti i membri dei gruppi di marketing verrebbero assegnati toohello ruolo "marketing" in Salesforce
  * Tutti i membri delle vendite team gruppi verrebbe assegnato toohello ruolo "sales" in Salesforce. Un ulteriore perfezionamento è possibile utilizzare più gruppi di rappresentano i team di vendita regionali toodifferent Salesforce ruoli assegnati.
* meccanismo di eccezioni tooenable hello, per ogni ruolo è stato possibile creare un gruppo self-service. Gruppo "Marketing eccezione Salesforce" hello, ad esempio, può essere creato come gruppo self-service. gruppo di Hello può essere assegnato a un ruolo di marketing Salesforce toohello e team di leadership hello marketing possono essere eseguite proprietari. I membri del team di leadership marketing hello Impossibile aggiungere o rimuovere gli utenti, impostare un criterio di join, o anche approvare o negare toojoin le richieste di singoli utenti. Questa opzione è supportata tramite un'appropriata esperienza di un information worker che non richiede una formazione specifica per proprietari o membri.

In questo caso, tutti gli utenti assegnati sarebbe tooSalesforce automaticamente sottoposto a provisioning, come se fossero gruppi aggiunti toodifferent che l'assegnazione di ruolo verranno aggiornato in Salesforce. Gli utenti sarebbero toodiscover in grado di e accedere a Salesforce tramite il pannello di accesso dell'applicazione Microsoft hello, i client web di Office, o anche passando tootheir pagina di accesso Salesforce azienda. Gli amministratori sarebbe tooeasily in grado di visualizzare informazioni sull'utilizzo e assegnazione lo stato con Azure AD reporting.

Gli amministratori possono utilizzare [accesso condizionale di Azure AD](active-directory-conditional-access.md) tooset i criteri di accesso per ruoli specifici. Questi criteri possono includere se è consentito l'accesso all'esterno di ambiente aziendale hello e anche multi-Factor Authentication o accedere al dispositivo requisiti tooachieve in vari casi.

## <a name="how-can-i-get-started"></a>Operazioni iniziali
Innanzitutto, un amministratore IT che non usa già Azure AD:

* [Versione di valutazione](https://azure.microsoft.com/trial/get-started-active-directory/) : è possibile ottenere subito gratuitamente una versione di valutazione di 30 giorni e distribuire la prima soluzione cloud in meno di 5 minuti, usando il collegamento seguente

Le funzionalità di Azure AD che consentono la condivisione di account includono:

* [Assegnazione di gruppi](active-directory-accessmanagement-self-service-group-management.md)
* Aggiunta di applicazioni tooAzure AD
* Introduzione all'assegnazione
* Domande frequenti sull'assegnazione di applicazioni
* [Dashboard/report sull'utilizzo di app](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Altre informazioni
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Sicurezza delle app con l'accesso condizionale](active-directory-conditional-access.md)
* [Gestione di gruppi self-service/SSAA](active-directory-accessmanagement-self-service-group-management.md)

