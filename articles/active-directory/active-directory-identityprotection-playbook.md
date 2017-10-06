---
title: "playbook la protezione dell'identità di Active Directory aaaAzure | Documenti Microsoft"
description: "Informazioni su come Azure AD Identity Protection consenta il possibilità hello toolimit di un tooexploit malintenzionato un'identità compromessa o il dispositivo e toosecure un'identità o un dispositivo che in precedenza era noto o sospetta toobe compromesso."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Studio sulla protezione delle identità di Azure Active Directory
Questo studio consente di:

* Popolare i dati nell'ambiente di protezione dell'identità hello da simulare eventi di rischio e vulnerabilità
* Impostare i criteri di accesso condizionale basati sui rischi e hello impatto di questi criteri di test

## <a name="simulating-risk-events"></a>Simulazione di eventi di rischio
Questa sezione fornisce passaggi per la simulazione hello seguenti tipi di eventi di rischio:

* Accessi da indirizzi IP anonimi (facile)
* Accessi da posizioni non note (intermedio)
* Impossibile tooatypical corsa (complesso)

Non è possibile simulare altri eventi di rischio in modo sicuro.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Accessi da indirizzi IP anonimi
Questo tipo di evento di rischio identifica gli utenti che hanno eseguito l'accesso da un indirizzo IP riconosciuto come un indirizzo IP proxy anonimo. Questi proxy vengono utilizzati dagli utenti che desiderano toohide indirizzo IP del dispositivo in uso e possono essere utilizzate per fini dannosi.

**toosimulate sign-in da un IP anonimo, eseguire operazioni hello**:

1. Scaricare hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).
2. Utilizzando hello Tor Browser, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Immettere le credenziali di hello di account di hello si vuole tooappear in hello **accessi da indirizzi IP anonimi** report.

Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 5 minuti. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Accessi da posizioni non note
rischio posizioni non familiari Hello è un meccanismo di valutazione dell'accesso in tempo reale che prende in considerazione oltre i percorsi di accesso (IP, latitudine / longitudine e ASN) toodetermine nuovo / familiarità percorsi. sistema Hello archivia gli indirizzi IP precedente, latitudine / longitudine e ASN di un utente e considera questi percorsi familiarità toobe. Un percorso di accesso viene considerato non familiare se hello posizione di accesso non corrisponde a nessuno dei percorsi familiarità esistente hello.

Azure Active Directory Identity Protection:  

* ha un periodo di apprendimento iniziale di 14 giorni, durante i quali le nuove posizioni non vengono contrassegnate come posizioni non note.
* Ignora accessi da dispositivi familiarità e percorsi di posizione familiare esistente tooan geograficamente Chiudi.

posizioni non familiari toosimulate, aver toosign in un percorso e un dispositivo che account hello ha non eseguito l'accesso dalla prima. 

**toosimulate sign-in da una posizione familiarità, eseguire hello alla procedura seguente**:

1. Scegliere un account che abbia una cronologia di accesso di almeno 14 giorni. 
2. È possibile procedere in due modi:
   
   a. Quando si utilizza una connessione VPN, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com) e immettere le credenziali di hello di account di hello si vuole toosimulate hello rischio relativo.
   
   b. Chiedere a un collega in toosign un percorso diverso utilizzando le credenziali dell'account hello (scelta non consigliate).

Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 5 minuti.

### <a name="impossible-travel-tooatypical-location"></a>Impossibile tooatypical viaggio.
Simulazione di condizione di comunicazione Impossibile: hello è difficile perché l'algoritmo hello Usa machine learning tooweed out falsi positivi, ad esempio viaggio Impossibile da dispositivi familiari o accessi da connessioni VPN che vengono utilizzati da altri utenti nella directory hello. Algoritmo hello richiede inoltre una cronologia di accesso di 3 giorni too14 per utente hello prima di avviare la generazione di eventi di rischio.

**toosimulate un impossibili tooatypical viaggio, eseguire hello alla procedura seguente**:

1. Utilizzando il browser standard, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Immettere le credenziali di hello di account di hello per che si vuole toogenerate un evento di rischio per la comunicazione Impossibile.
3. Modificare l'agente utente. Per modificare l'agente utente in Internet Explorer, usare Strumenti di sviluppo. Per modificare l'agente utente in Firefox o Chrome, usare un componente aggiuntivo di selezione dell'agente utente.
4. Modificare l'indirizzo IP. È possibile modificare l'indirizzo IP usando una VPN, un componente aggiuntivo Tor o avviare un nuovo computer in Azure in un altro data center.
5. Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com) utilizzando hello stesse credenziali come prima ed entro pochi minuti dopo hello precedente accesso.

Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 2-4 ore.<br>
A causa di hello complesso modelli di machine learning coinvolti, è probabile che sarà non prelevata.<br> È possibile tooreplicate questi passaggi per più account di Azure AD.

## <a name="simulating-vulnerabilities"></a>Simulazione di vulnerabilità
Le vulnerabilità sono punti deboli in un ambiente Azure AD che possono essere sfruttati da un utente malintenzionato. In Azure AD Identity Protection sono attualmente visibili 3 tipi di vulnerabilità che consentono di sfruttare altre funzionalità di Azure AD. Queste vulnerabilità verranno visualizzate nel dashboard di protezione dell'identità hello automaticamente una volta impostate queste funzionalità.

* Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Rischio di compromissione dell'utente
**tootest il rischio di manomissione di utente, eseguire operazioni hello**:

1. Accedi troppo[https://portal.azure.com](https://portal.azure.com) con credenziali di amministratore globale per il tenant.
2. Passare troppo**Identity Protection**. 
3. Nella finestra principale di hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**. 
4. In hello **le impostazioni del portale** pannello, in **regole di sicurezza**, fare clic su **il rischio di compromissione utente**. 
5. In hello **Accedi rischio** pannello, attivare **Abilita regola** off e quindi fare clic su **salvare** impostazioni.
6. Per un determinato account utente, simulare un evento di rischio IP anonimo o posizione non nota. Questo verrà elevare un livello di rischio hello utente per tale utente troppo**Media**.
7. Attendere alcuni minuti e poi verificare che il livello utente sia **Medio**.
8. Passare toohello **le impostazioni del portale** blade.
9. In hello **il rischio di compromissione utente** pannello, in **Abilita regola**selezionare **su** . 
10. Selezionare una delle seguenti opzioni hello:
    
    a. tooblock, selezionare **Media** in **blocco Accedi**.
    
    b. modifica della password sicura tooenforce, selezionare **Media** in **richiede l'autenticazione a più fattori**.
11. Fare clic su **Salva**.
12. A questo punto è possibile testare l'accesso condizionale basato sul rischio eseguendo l'accesso come un utente con un livello di rischio elevato. Se il rischio di utente hello è Media, a seconda della configurazione di hello dei criteri, l'accesso è sia bloccato o se è necessario toochange la password. 
    <br><br>
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    <br>

## <a name="sign-in-risk"></a>Rischio di accesso
**tootest Accedi rischio, eseguire hello alla procedura seguente:**

1. Accedi troppo[https://portal.azure.com ](https://portal.azure.com) con credenziali di amministratore globale per il tenant.
2. Passare troppo**Identity Protection**.
3. Nella finestra principale di hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**. 
4. In hello **le impostazioni del portale** pannello, in **regole di sicurezza**, fare clic su **Accedi rischio**.
5. In hello * * Accedi rischio * * pannello seleziona **su** in **Abilita regola**. 
6. Selezionare una delle seguenti opzioni hello:
   
   a. tooblock, selezionare **Media** in **blocco Accedi**
   
   b. modifica della password sicura tooenforce, selezionare **Media** in **richiede l'autenticazione a più fattori**.
7. tooblock, seleziona Media sotto blocco Accedi.
8. autenticazione a più fattori tooenforce, seleziona **Media** in **richiede l'autenticazione a più fattori**.
9. Fare clic su **Save**.
10. È ora possibile testare l'accesso condizionale basati sui rischi simulando posizioni non familiari hello o IP anonimo rischio eventi perché sono entrambi **Media** gli eventi di rischio.


![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")


## <a name="see-also"></a>Vedere anche
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

