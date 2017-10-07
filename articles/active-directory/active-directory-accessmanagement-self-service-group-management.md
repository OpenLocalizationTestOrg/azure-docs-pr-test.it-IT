---
title: aaaSetting backup di Azure Active Directory per la gestione di accesso di applicazioni self-service | Documenti Microsoft
description: "Gestione dei gruppi self-service consente agli utenti toocreate e gestire gruppi di protezione o gruppi di Office 365 in Azure Active Directory e gruppo di sicurezza toorequest hello possibilità offerte utenti o l'appartenenza ai gruppi di Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Configurazione di Azure Active Directory per la gestione self-service dei gruppi
Gestione dei gruppi self-service consente agli utenti toocreate e gestire gruppi di protezione o gruppi di Office 365 in Azure Active Directory (Azure AD). Gli utenti possono inoltre richiedere appartenenze a gruppi di Office 365 o di gruppo di sicurezza e quindi hello proprietario del gruppo di hello può approvare o rifiutare l'appartenenza. In questo modo, il controllo giornaliero dell'appartenenza al gruppo può essere delegata toopeople che conoscono il contesto business hello per tale appartenenza. Le funzionalità di gestione self-service dei gruppi sono disponibili solo per i gruppi di sicurezza e i gruppi di Office 365, ma non per i gruppi di protezione abilitati alla posta o le liste di distribuzione.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo.

La gestione self-service dei gruppi comprende attualmente due scenari principali, ovvero gestione delegata e gestione self-service.

* **Gestione gruppi delegata** un esempio è un amministratore che gestisce l'applicazione SaaS di tooa accesso società hello è in uso. Gestione dei diritti di accesso diventa più onerosa, l'amministratore chiede hello business proprietario toocreate un nuovo gruppo. messaggio per l'amministratore assegna l'accesso per il nuovo gruppo di hello applicazione toohello e aggiunge toohello gruppo tutti gli utenti che già accedono toohello applicazione. i proprietari aziendali Hello quindi possono aggiungere più utenti e gli utenti sono automaticamente provisioning toohello applicazione. i proprietari aziendali Hello non deve necessariamente toowait per l'accesso toomanage hello amministratore per gli utenti. Se viene concessa dall'amministratore di hello hello nella stessa gestione tooa autorizzazione in un gruppo aziendale diverso, quindi che l'utente può anche gestire l'accesso per i propri utenti. I proprietari aziendali hello né manager hello è possibile visualizzare o gestire gli utenti di altro. amministratore Hello è comunque possibile visualizzare tutti gli utenti che dispongono di accesso toohello applicazione e blocco dei diritti di accesso se necessario.
* **Gestione self-service dei gruppi** Un esempio di questo scenario è costituito da due utenti che hanno entrambi siti di SharePoint Online configurati in modo indipendente Ogni di altro team di accedere ai siti tootheir toogive desiderati. tooaccomplish, è possibile creare un gruppo in Azure AD e in SharePoint Online ognuno di essi Seleziona che i siti tootheir tooprovide accesso gruppo. Se qualcuno desidera accedere, effettua la richiesta dal Pannello di accesso hello e dopo l'approvazione, può accedere ai siti SharePoint Online tooboth automaticamente. In un secondo momento, uno di essi decide che tutti gli utenti che accedono sito hello devono inoltre ottenere accesso tooa particolare applicazione SaaS. messaggio per l'amministratore di hello applicazione SaaS possa aggiungere diritti di accesso per sito di SharePoint Online toohello applicazione hello. Tutte le richieste che un'approvazione in poi, offre un accesso toohello due siti SharePoint Online e anche toothis applicazione SaaS.

## <a name="making-a-group-available-for-end-user-self-service"></a>Rendere un gruppo disponibile per la modalità self-service per gli utenti finali
1. In hello [portale di Azure classico](https://manage.windowsazure.com), aprire la directory di Azure AD.
2. In hello **configura** scheda, impostare **Gestione gruppi delegata** tooEnabled.
3. Impostare **gli utenti possono creare gruppi di sicurezza** o **gli utenti possono creare gruppi di Office** tooEnabled.

Quando **gli utenti possono creare gruppi di sicurezza** è abilitata, tutti gli utenti nella directory sono consentiti toocreate nuovi gruppi di sicurezza e aggiungere gruppi di membri toothese. Questi nuovi gruppi sono visibili in hello Pannello di accesso per tutti gli altri utenti. Se l'impostazione di criteri di hello in gruppo hello lo consente, ad altri utenti possono creare richieste toojoin questi gruppi. Se l'opzione **Gli utenti possono creare gruppi di sicurezza** è disabilitata, gli utenti non possono creare gruppi né modificare i gruppi esistenti di cui sono proprietari. Tuttavia, possono tuttavia gestire hello appartenenze a tali gruppi e approvare le richieste di toojoin altri utenti ai gruppi.

È inoltre possibile utilizzare **utenti che possono usare Self-Service per i gruppi di sicurezza** tooachieve un controllo di accesso con granularità fine su gestione dei gruppi self-service per gli utenti. Quando **gli utenti possono creare gruppi** è abilitata, tutti gli utenti nella directory sono consentiti toocreate nuovi gruppi e aggiungere gruppi di membri toothese. Impostando anche **utenti che possono usare Self-Service per i gruppi di sicurezza** tooSome, si limiterà gruppo Gestione tooonly un gruppo di utenti limitato. Quando questa opzione è impostata tooSome, è necessario aggiungere gli utenti toohello gruppo SSGMSecurityGroupsUsers prima di poter creare nuovi gruppi e aggiungere membri toothem. Impostando **utenti che possono usare Self-Service per i gruppi di sicurezza** tooAll, si attiva tutti gli utenti nei gruppi toocreate nuova directory.

È inoltre possibile utilizzare hello **gruppi che possono usare Self-Service per i gruppi di sicurezza** casella toospecify un nome personalizzato per un gruppo i cui membri possono usare Self-Service.

## <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
