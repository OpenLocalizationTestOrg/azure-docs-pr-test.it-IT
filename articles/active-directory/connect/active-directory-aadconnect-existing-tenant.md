---
title: "Azure AD Connect: Quando è già presente Azure AD | Documentazione Microsoft"
description: Questo argomento viene descritto come toouse connettersi quando si dispone di un tenant Azure AD.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect con un tenant esistente
La maggior parte degli argomenti sulle hello come Azure AD Connect toouse si presuppone che si avvia con Azure un nuovo tenant di Active Directory e che nessun utente o gli altri oggetti. Ma se è stata avviata con un tenant di Azure AD viene popolato con gli utenti e altri oggetti e si decide toouse Connetti, quindi in questo argomento viene automaticamente.

## <a name="hello-basics"></a>Nozioni di base Hello
Un oggetto in Azure AD è essere controllato in locale o cloud hello (Azure AD). Per un singolo oggetto non è possibile gestire alcuni attributi in locale e altri attributi in Azure AD. Ogni oggetto dispone di un flag che indica dove hello oggetto gestito.

È possibile gestire alcuni utenti locali e altri in cloud hello. Uno scenario comune per questa configurazione è un'azienda con una combinazione di contabili e addetti alla vendita. Hello lavoratori accounting dispongano di un locale non sono account di Active Directory, ma i lavoratori vendita hello, hanno un account di Azure AD. Alcuni utenti verranno gestiti in locale, alcuni in Azure AD.

Se è stata avviata toomanage utenti in Azure AD che sono presenti anche in AD locale e successivamente si desidera toouse Connetti, quindi sono disponibili alcuni altri problemi, che è necessario tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Eseguire la sincronizzazione con gli utenti esistenti in Azure AD
Quando si installa Azure AD Connect e si avvia la sincronizzazione, hello servizio di sincronizzazione di Azure AD (in Azure AD) esegue un controllo per ogni nuovo oggetto e tentare toofind un toomatch oggetto esistente. Vengono usati tre attributi per questo processo: **userPrincipalName**, **proxyAddresses** e **sourceAnchor**/**immutableID**. Una corrispondenza per **userPrincipalName** e **proxyAddresses** è nota come **corrispondenza flessibile**. Una corrispondenza per **sourceAnchor** è nota come **corrispondenza rigida**. Per hello **proxyAddresses** solo hello valore con attributo **SMTP:**, che è l'indirizzo di posta elettronica primario hello, viene utilizzato per la valutazione di hello.

corrispondenza Hello viene valutata solo per i nuovi oggetti provenienti da Connect. Se si modifica un oggetto esistente in modo che corrisponda a uno di questi attributi, verrà visualizzato un errore.

Se AD Azure rileva un oggetto in cui i valori di attributo hello sono hello lo stesso per un oggetto provenienti dalla connessione e che è già presente in Azure AD, quindi hello oggetto in Azure AD viene preso in carico da Connect. Hello in precedenza oggetto gestito cloud viene contrassegnata come gestite in locale. Tutti gli attributi in Azure AD con un valore in locale Active Directory vengono sovrascritti con valore locale hello. Hello eccezione è quando un attributo dispone di un **NULL** valore locale. In questo caso, il valore di hello in Azure AD continuerà, ma può comunque modificarla solo locale toosomething else.

> [!WARNING]
> Poiché tutti gli attributi in Azure Active Directory vengono sovrascritti dal valore locale hello toobe, assicurarsi di avere dei dati in locale. Se ad esempio un indirizzo e-mail è stato gestito solo in Office 365, ma non è stato aggiornato nell'istanza di Active Directory Domain Services locale, i valori di Azure AD/Office 365 non presenti in Active Directory Domain Services andranno persi.

> [!IMPORTANT]
> Se si usa la sincronizzazione delle password, che viene sempre utilizzata dalle impostazioni express, quindi password hello in Azure AD viene sovrascritto con password hello in locale Active Directory. Se gli utenti sono utilizzati toomanage password diverse, è necessario tooinform dopo aver installato Connect che devono usare hello password locale.

la sezione precedente di hello e di avviso da considerare nella pianificazione. Se sono state apportate numerose modifiche in Azure AD non verranno aggiornate locale di dominio Active Directory, è necessario tooplan per la modalità di dominio Active Directory con hello toopopulate i valori aggiornati prima di sincronizzare gli oggetti con Azure AD Connect.

Se gli oggetti con una corrispondenza di soft corrisposto hello **sourceAnchor** viene aggiunto un oggetto toohello in Azure AD una disco rigida corrispondenza può essere utilizzato in un secondo momento.

### <a name="hard-match-vs-soft-match"></a>Differenza tra corrispondenza rigida e corrispondenza flessibile
Per una nuova installazione di Connect, non esiste alcuna differenza pratica tra corrispondenza flessibile e corrispondenza rigida. differenza Hello è in una situazione di ripristino di emergenza. Se si è perso il server con Azure AD Connect, è possibile reinstallare una nuova istanza senza perdere i dati. Un oggetto con un attributo sourceAnchor viene inviato tooConnect durante l'installazione iniziale. Hello corrispondenza può quindi essere valutata dal client di hello (Azure AD Connect), che è molto più veloce rispetto a tale stesso hello in Azure AD. Una corrispondenza rigida viene valutata sia da Connect che da Azure AD. Una corrispondenza flessibile viene valutata solo da Azure AD.

### <a name="other-objects-than-users"></a>Oggetti diversi dagli utenti
Gli utenti dispongono in genere userPrincipalName sia proxyAddresses, semplificando la corrispondenza di hello. Altri oggetti, ad esempio i gruppi di sicurezza, non hanno tuttavia questi attributi. In questo caso, può trovare solo in caso di corrispondenza di disco rigida utilizzando hello sourceAnchor. Hello sourceAnchor è sempre hello Base64 convertito **objectGUID** locale, pertanto è necessario aggiornare il valore di hello in Azure AD quando è necessario toomatch di due oggetti. Hello sourceAnchor o immutableID può essere aggiornata solo con PowerShell e non tramite i portali di hello.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Creare una nuova istanza di Active Directory locale dai dati di Azure AD
Alcuni clienti iniziano con una soluzione solo cloud con Azure AD e non hanno un'istanza di AD locale. In un secondo momento si desidera tooconsume alle risorse locali e toobuild un locale di Active Directory in base ai dati di Azure AD. Azure AD Connect non potrà essere utile per questo scenario. Non è possibile creare gli utenti locali e non dispone di qualsiasi toohello di possibilità tooset hello password locale corrisponde a quella di Azure AD.

Se l'unico motivo hello perché si prevede di tooadd locale AD è toosupport LOB (Line-of-Business apps), quindi considerare forse toouse [servizi di dominio di Azure AD](../../active-directory-domain-services/index.md) invece.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
