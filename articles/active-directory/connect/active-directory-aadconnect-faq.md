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
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Domande frequenti su Azure Active Directory Connect

## <a name="general-installation"></a>Installazione generale
**D: installazione funzioneranno se hello amministratore globale di Azure AD ha 2FA abilitato?**  
Con le compilazioni hello da febbraio 2016, questa è supportata.

**D: è presente un tooinstall modo Azure AD Connect automatica?**  
È solo supportati tooinstall Azure AD Connect hello installazione guidata. L'installazione automatica e invisibile all'utente non è supportata.

**D: Ho una foresta in cui un dominio non può essere contattato. Come installare Azure AD Connect?**  
Con le compilazioni hello da febbraio 2016, questa è supportata.

**D: hello lavoro agente di integrità di dominio Active Directory in server core?**  
Sì. Dopo aver installato l'agente di hello, è possibile completare il processo di registrazione hello utilizzando hello cmdlet di PowerShell seguente: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Rete
**D: ho un firewall, il dispositivo di rete o un'altra caratteristica che limita le connessioni di tempo massimo di hello può rimanere aperta sulla rete. Quanto deve durare la soglia di timeout lato client quando si utilizza Connetti AD Azure?**  
Tutti i software di rete, dispositivi fisici o altri elementi che i limiti di tempo massimo di hello connessioni possono rimanere aperte deve utilizzare una soglia di almeno 5 minuti (300 secondi) per la connettività tra hello server in cui hello client di Azure AD Connect è installato e Azure Active Directory. Questo vale anche gli strumenti di sincronizzazione di Microsoft Identity tooall rilasciate in precedenza.

**D: I domini SDL sono supportati?**  
No, Azure AD Connect non supporta foreste/domini in locale mediante i domini SLD.

**D: Gli elementi denominati NetBios con "punti" sono supportati?**  
No, Azure AD Connect non supporta locale foreste o domini in cui il nome NetBios hello contiene un punto "." nel nome hello.

## <a name="federation"></a>Federazione
**D: cosa fare se viene visualizzato un messaggio di posta elettronica che chiedere toorenew certificato Office 365**  
Utilizzare le linee guida hello descritta in hello [rinnovare i certificati](active-directory-aadconnect-o365-certs.md) argomento su come toorenew hello certificato.

**D: L'opzione di aggiornamento automatico della relying party è impostata per la relying party Office 365. È necessario tootake alcuna azione quando il certificato di firma automaticamente il token rollover?**  
Utilizzare le linee guida hello descritta nell'articolo hello [rinnovare i certificati](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Environment
**D: è supportato it toorename hello server dopo l'installazione di Azure AD Connect?**  
No. Modifica del nome di server hello causa hello sincronizzazione motore toonot sarà in grado di tooconnect toohello SQL database e il servizio di hello non sarà in grado di toostart.

## <a name="identity-data"></a>Dati di identità
**D: hello l'attributo UPN (userPrincipalName) in Azure AD non corrisponde hello UPN locale - perché?**  
Vedere i seguenti articoli:

* [I nomi utente non corrispondono in Office 365, Azure o Intune hello UPN locale o ID di accesso alternativo](https://support.microsoft.com/en-us/kb/2523192)
* [Le modifiche non sono sincronizzate dallo strumento di sincronizzazione di Azure Active Directory hello dopo aver modificato hello UPN di un toouse di account utente diverso dominio federato](https://support.microsoft.com/en-us/kb/2669550)

È inoltre possibile configurare Azure AD tooallow hello sincronizzazione motore tooupdate hello userPrincipalName come descritto in [funzionalità servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**D: sono supportato it toosoft corrispondenza locale oggetti di gruppo o contatto di Active Directory con gli oggetti di Azure AD/contatto del gruppo esistente?**  
No, attualmente non è supportata.

**D: è supportato it toomanually impostare l'attributo ImmutableId in Azure AD gruppo o contatto esistente toohard oggetti corrispondenti tooon locale oggetti gruppo di Active Directory/contatto?**  
No, attualmente non è supportata.



## <a name="custom-configuration"></a>Configurazione personalizzata
**D: dove sono hello i cmdlet di PowerShell per Azure AD Connect documentato?**  
Con l'eccezione di hello dei cmdlet hello documentati in questo sito, altri cmdlet di PowerShell trovato in Azure AD Connect non sono supportati per l'utilizzo di cliente.

**D: è possibile utilizzare "Server di esportazione/importazione Server" trovato nel *Synchronization Service Manager* toomove configurazione tra i server?**  
No. Questa opzione non recupererà tutte le impostazioni di configurazione e non deve essere utilizzata. È necessario invece utilizzare configurazione base hello toocreate guidata hello nel secondo server hello e hello editor di regola di sincronizzazione toogenerate toomove di script di PowerShell qualsiasi regola personalizzata tra i server. Vedere [Migrazione swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**D: è possibile password essere memorizzati nella cache per la pagina hello Accedi Azure e questo è possibile evitare poiché contiene un elemento input di password con completamento automatico hello = "false" attributo?**</br>
Attualmente non è supportata la modifica degli attributi HTML hello del campo di immissione Password hello, inclusi i tag di completamento automatico hello. Sono attualmente una funzionalità che consentono di Javascript personalizzato che consentirà tooadd tutti i campi password toohello attributo. Dovrebbe essere disponibile più avanti nel 2017.

**D: in hello Azure nella pagina di accesso, vengono visualizzati i nomi utente per gli utenti che hanno già effettuato l'accesso correttamente.  Questo comportamento può essere disattivato?**</br>
Attualmente non è supportata la modifica degli attributi HTML hello di hello nella pagina di accesso. Sono attualmente una funzionalità che consentono di Javascript personalizzato che consentirà tooadd tutti i campi password toohello attributo. Dovrebbe essere disponibile più avanti nel 2017.

**D: è un modo tooprevent sessioni simultanee?**</br>
No.



## <a name="troubleshooting"></a>Risoluzione dei problemi
**D: Come è possibile ottenere informazioni su Azure AD Connect?**

[Hello ricerca Microsoft Knowledge Base (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Hello di ricerca Microsoft Knowledge Base (KB) per i problemi di riparazione toocommon soluzioni ai problemi tecnici sul supporto per Azure AD Connect.

[Forum di Microsoft Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* È possibile cercare e visualizzare per la technical domande e risposte dalla community di hello o porre una domanda facendo [qui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Assistenza clienti per Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Usare questo supporto tooget collegamento tramite hello portale di Azure.

