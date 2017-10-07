---
title: aaaUse gruppi toomanage accesso tooresources in Azure Active Directory | Documenti Microsoft
description: Gruppi di toouse utente toomanage Azure Active Directory come accedere a risorse e le applicazioni cloud e locali tooon.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Gestire accesso tooresources con gruppi di Azure Active Directory
Azure Active Directory (Azure AD) è una completa soluzione di gestione di identità e accessi che fornisce un set affidabile di funzionalità toomanage accesso tooon locale e le applicazioni cloud e risorse, tra cui Microsoft online services quali Office 365 e moltissime applicazioni SaaS non Microsoft. In questo articolo viene fornita una panoramica, ma se si desidera ora gruppi di toostart mediante Azure AD, seguire le istruzioni hello [la gestione di gruppi di sicurezza di Azure AD](active-directory-accessmanagement-manage-groups.md). Se si desidera toosee come è possibile utilizzare PowerShell toomanage i gruppi in Azure Active directory, è possibile leggere ulteriori [cmdlet di Azure Active Directory per la gestione di gruppo](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Azure Active Directory, è necessario un account di Azure. Se non si dispone di un account, è possibile [iscriversi per un account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/).
>
>

All'interno di Azure AD, una delle funzionalità principali di hello è hello possibilità toomanage accesso tooresources. Queste risorse possono far parte della directory di hello, come nel caso di hello oggetti toomanage autorizzazioni tramite ruoli nella directory hello o risorse che sono directory toohello esterno, ad esempio applicazioni SaaS, servizi di Azure e siti di SharePoint o in locale risorse. Sono disponibili quattro modi che un utente può essere assegnato come risorsa tooa diritti di accesso:

1. Assegnazione diretta

    Gli utenti possono essere assegnati direttamente tooa risorsa dal proprietario hello di tale risorsa.
2. Appartenenza al gruppo

    Un gruppo può essere assegnato tooa risorsa dal proprietario della risorsa hello e in tal modo, i membri di tale risorsa del gruppo di accesso toohello hello concessione. Appartenenza al gruppo hello possa essere gestito dal proprietario hello del gruppo di hello. In effetti, i delegati proprietario risorsa hello hello autorizzazione tooassign utenti tootheir toohello proprietario della risorsa del gruppo di hello.
3. Basato su regole

    proprietario della risorsa Hello è possibile utilizzare una regola tooexpress gli utenti a cui devono essere assegnati l'accesso tooa risorse. risultato Hello della regola hello dipende da attributi di hello usati in tale regola e i relativi valori per utenti specifici, e in questo modo, proprietario della risorsa hello delegati in modo efficace hello toomanage destra accesso tootheir risorse toohello origine autorevole per hello attributi utilizzati nella regola hello. proprietario della risorsa Hello ancora gestisce regola hello stessa e determina quali attributi e valori di forniscono accesso tootheir risorse.
4. Autorità esterna

    risorse di tooa accesso Hello sono derivata da un'origine esterna. ad esempio, un gruppo che verrà sincronizzato da un'origine attendibile, ad esempio una directory locale o di un'applicazione SaaS, ad esempio giorno lavorativo. proprietario della risorsa Hello viene assegnata hello gruppo tooprovide accesso toohello e origine esterna hello gestisce i membri del gruppo di hello hello.

   ![Panoramica del diagramma di gestione dell’accesso](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Video che illustra la gestione dell'accesso
È possibile guardare un breve video che fornisce ulteriori spiegazioni su questo:

**Azure AD: Appartenenza toodynamic introduzione per i gruppi**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Come funziona la gestione dell'accesso in Azure Active Directory?
In hello centro della soluzione di gestione di Azure AD access hello è il gruppo di sicurezza di hello. Utilizzo di un accesso tooresources di sicurezza gruppo toomanage è un paradigma noto, che consente di una risorsa di tooa accesso tooprovide modo flessibile e facilmente comprensibile per il gruppo di hello previsto di utenti. proprietario della risorsa Hello (o messaggio per l'amministratore della directory hello) possibile assegnare tooprovide un gruppo una determinate risorse di destra toohello accesso che sono proprietari. i membri del gruppo di hello Hello verranno forniti accesso hello e proprietario della risorsa hello possibile delegare l'elenco dei membri hello toomanage destra hello di un altro, ad esempio un responsabile del reparto o un amministratore di help desk toosomeone di gruppo.

![Diagramma di gestione dell’accesso di Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

Hello proprietario di un gruppo può inoltre rendere tale gruppo disponibili per le richieste self-service. In questo modo, un utente finale può cercare e trovare il gruppo di hello. toojoin una richiesta, ricerca in modo efficace le risorse di hello tooaccess autorizzazione gestiti tramite il gruppo di hello il proprietario di Hello del gruppo di hello possibile impostare il gruppo di hello in modo che le richieste di join vengono approvate automaticamente o richiedono l'approvazione dal proprietario hello del gruppo di hello. Quando un utente apporta toojoin una richiesta di un gruppo, la richiesta di join hello viene inoltrata toohello proprietari del gruppo di hello. Se uno dei proprietari di hello Approva richiesta di hello, riceve una notifica utente richiedente hello e utente hello toohello aggiunti a un gruppo. Se uno dei proprietari di hello Nega richiesta hello, richiedente hello riceve una notifica, ma non aggiunti a un gruppo toohello.

## <a name="getting-started-with-access-management"></a>Introduzione alla gestione dell’accesso
Tooget pronto iniziare? È consigliabile provare alcune delle attività di base hello che è possibile eseguire con i gruppi di Azure AD. Utilizzare queste tooprovide funzionalità specializzate access toodifferent gruppi di utenti per diverse risorse nell'organizzazione. Un elenco di passaggi di base sono elencati di seguito.

* [Creazione di una semplice regola tooconfigure appartenenze dinamiche per un gruppo](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Utilizzo di applicazioni di tooSaaS un gruppo toomanage accesso](active-directory-accessmanagement-group-saasapps.md)
* [Rendere la modalità self-service disponibile a un gruppo di utenti](active-directory-accessmanagement-self-service-group-management.md)
* [La sincronizzazione di un tooAzure di gruppo locali con Azure AD Connect](active-directory-aadconnect.md)
* [Gestione dei proprietari di un gruppo](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Passaggi successivi
Ora che avere compreso i concetti di base di hello gestione dell'accesso, ecco alcune funzionalità avanzate aggiuntive disponibili in Azure Active Directory per la gestione delle applicazioni di accesso tooyour e risorse.

* [Utilizzando attributi toocreate regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Gestire i gruppi di sicurezza in Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Impostare gruppi dedicati in Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Informazioni di riferimento all'API Graph per gruppi](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
