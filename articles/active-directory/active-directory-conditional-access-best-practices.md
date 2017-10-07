---
title: aaaBest procedure consigliate per l'accesso condizionale in Azure Active Directory | Documenti Microsoft
description: "Informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale."
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Procedure consigliate per l'accesso condizionale in Azure Active Directory

Questo argomento fornisce informazioni sugli aspetti da conoscere e su ciò che è consigliabile evitare quando si configurano i criteri di accesso condizionale. Prima di leggere questo argomento, è consigliabile acquisire familiarità con concetti hello e terminologia hello descritte nella [accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Informazioni utili

### <a name="whats-required-toomake-a-policy-work"></a>Le impostazioni necessarie toomake un lavoro criteri?

Quando si crea un nuovo criterio, non sono selezionti utenti, gruppi, app o controlli di accesso.

![App cloud](./media/active-directory-conditional-access-best-practices/02.png)


i criteri di toomake lavoro, è necessario configurare l'esempio hello:


|Cosa           | Come                                  | Motivo|
|:--            | :--                                  | :-- |
|**App cloud** |È necessario tooselect una o più app.  | obiettivo di Hello di criteri di accesso condizionale è tooenable è ottimizzare toofine come gli utenti autorizzati possono accedere le applicazioni.|
| **Utenti e gruppi** | È necessario tooselect almeno un utente o gruppo che è autorizzato tooaccess hello cloud App è stata selezionata. | Un criterio di accesso condizionale a cui non sono assegnati utenti e gruppi non viene mai attivato. |
| **Controlli di accesso** | È necessario tooselect almeno un controllo di accesso. | Il processore di criteri deve tooknow quali toodo se vengono soddisfatte le condizioni.|


Aggiunta toothese base dei requisiti, in molti casi, è necessario configurare anche una condizione. Mentre un criterio funzionerebbe anche senza una condizione configurata, le condizioni sono un fattore determinante per l'ottimizzazione di accesso tooyour App hello.


![App cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Come vengono valutate le assegnazioni?

Tutte le assegnazioni vengono collegate logicamente con l'operatore **AND**. Se si dispone di più di un'assegnazione configurata, tootrigger un criterio, tutte le assegnazioni devono essere soddisfatta.  

Se è necessario tooconfigure una condizione di percorso che applica le connessioni tooall effettuate all'esterno della rete aziendale, è possibile farlo da:

- Includere **Tutte le località**
- Escludere **Tutti gli indirizzi IP attendibili**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>Cosa accade se si dispone di criteri nel portale di Azure classico hello e portale di Azure configurato.  
Entrambi i criteri vengono applicati da Azure Active Directory e hello utente ottiene l'accesso solo quando tutti i requisiti.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Cosa accade se si dispone di criteri nel portale Silverlight di Intune hello e hello portale di Azure?
Entrambi i criteri vengono applicati da Azure Active Directory e hello utente ottiene l'accesso solo quando tutti i requisiti.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>Cosa accade se si dispone di più criteri per hello configurato dall'utente stesso.  
Per ogni accesso, Azure Active Directory restituisce tutti i criteri e assicura che tutti i requisiti siano soddisfatti prima che l'utente di toohello concesso l'accesso.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>L'accesso condizionale funziona con Exchange ActiveSync?

Sì, è possibile usare Exchange ActiveSync in criteri di accesso condizionale.


## <a name="what-you-should-avoid-doing"></a>Azioni da evitare

il framework di accesso condizionale Hello offre la flessibilità di una configurazione ottimale. Tuttavia, una grande flessibilità significa anche che è opportuno esaminare attentamente ogni criterio di configurazione precedente tooreleasing è tooavoid di risultati non desiderabili. In questo contesto, è necessario prestare particolare attenzione tooassignments che interessano un set completo, ad esempio **tutti gli utenti / gruppi / App cloud**.

Nell'ambiente in uso, è necessario evitare hello seguenti configurazioni:


**Per tutti gli utenti e tutte le applicazioni cloud:**

- **Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.

- **Richiede un dispositivo conforme** - per gli utenti che non hanno registrato i dispositivi ancora, questo criterio blocca tutti gli accessi inclusi accesso toohello Intune portale. Se si è un amministratore senza un dispositivo registrato, questo criterio verrà bloccata dal rimettersi in Criteri di hello hello toochange portale Azure.

- **Richiedere l'aggiunta a dominio** : questo blocco criteri accesso ha inoltre hello potenziali tooblock accesso per tutti gli utenti nell'organizzazione se non si dispone ancora di un dispositivo aggiunto al dominio.


**Per tutti gli utenti, tutte le applicazioni cloud e tutte le piattaforme per dispositivi:**

- **Blocca accesso**: questa configurazione consente di bloccare l'intera organizzazione. Un'idea chiaramente non buona.


## <a name="common-scenarios"></a>Scenari comuni

### <a name="requiring-multi-factor-authentication-for-apps"></a>Richiesta dell'autenticazione a più fattori per le app

Molti ambienti dispongono di applicazioni che richiedono un livello di protezione maggiore rispetto a hello ad altri utenti.
Questo accade, ad esempio, hello per le applicazioni che dispongono di accesso toosensitive dati.
Se si desidera tooadd un ulteriore livello di protezione toothese App, è possibile configurare un criterio di accesso condizionale che richiede l'autenticazione a più fattori quando gli utenti accedono a tali app.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Richiesta dell'autenticazione a più fattori per l'accesso da reti non considerate attendibili

Questo scenario consente simile toohello precedente perché aggiunge un requisito per l'autenticazione a più fattori.
Tuttavia, la differenza principale hello è condizione hello per questo requisito.  
Durante lo stato attivo hello dello scenario precedente hello per le app con accesso ai dati toosensitve, hello di questo scenario è attiva percorsi attendibili.  
In altre parole, è possibile avere un requisito per l'autenticazione a più fattori se un'app è accessibile a un utente da una rete non considerata attendibile.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Solo i dispositivi attendibili possono accedere ai servizi di Office 365

Se si usa Intune nel proprio ambiente, è possibile avviare immediatamente usando l'interfaccia di criteri di accesso condizionale hello nella console di Azure hello.

Molti clienti di Intune usano tooensure di accesso condizionale che solo i dispositivi attendibili possono accedere ai servizi di Office 365. Ciò significa che i dispositivi mobili registrati con Intune e che soddisfano i requisiti di conformità e che i PC Windows sono dominio locale tooan unita in join. Dei miglioramenti principali è che non sia tooset hello stesso criterio per ognuno dei servizi di Office 365 hello.  Quando si crea un nuovo criterio, è possibile configurare hello Cloud App tooinclude ogni delle app di Office 365 hello che si desidera tooprotect con accesso condizionale.

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooknow tooconfigure criteri di accesso condizionale, vedere [iniziare con l'accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
