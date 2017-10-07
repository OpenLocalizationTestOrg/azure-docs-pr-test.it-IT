---
title: "identità aaaAuthenticating privi di password tramite Windows Hello for Business e Azure AD | Documenti Microsoft"
description: Contiene una panoramica di Windows Hello for Business e altre informazioni sulla distribuzione di Windows Hello for Business.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Autenticazione delle identità senza password con Windows Hello for Business
metodi di Hello correnti di autenticazione con password solo non sono sufficienti agli utenti di tookeep-safe. Gli utenti riutilizzano e dimenticano le password. Le password sono breachable, phishable, soggetta a toocracks e identificabili. Ricevono inoltre difficile tooremember e soggetta a tooattacks come "[passare hash hello](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>Informazioni su Windows Hello for Business
Windows Hello for Business è un approccio di autenticazione basato su certificato o su chiave privata/pubblica disponibile per organizzazioni e utenti grazie al quale non è più necessario usare password. Questo tipo di autenticazione si basa su credenziali coppia di chiavi che possono sostituire le password e toobreaches vengano interrotte, furti e phishing.

 Windows Hello per le aziende consente di autenticare l'account Microsoft tooa, un account di Windows Server Active Directory, un account di Microsoft Azure Active Directory (Azure AD) o un servizio non Microsoft che supporta l'autenticazione Fast identità Online (FIDO). Dopo una verifica in due passaggi iniziali durante Windows Hello per la registrazione di Business, Windows Hello for Business è configurato nel dispositivo dell'utente hello e utente hello imposta un'azione, che può essere Windows Hello o un PIN. utente Hello fornisce hello movimenti tooverify la propria identità. Windows, quindi, utilizza Windows Hello per gli utenti aziendali tooauthenticate hello e aiutarli a servizi e le risorse protette tooaccess.

la chiave privata di Hello è disponibile esclusivamente tramite un movimento"utente" come un PIN, biometrica o un dispositivo remoto come una smart card che hello utente utilizza toosign toohello dispositivo. Queste informazioni sono collegati tooa certificato o una coppia di chiavi asimmetrica. la chiave privata di Hello è hardware attestata se hello dispositivo dispone di un chip di modulo TPM (Trusted Platform). la chiave privata di Hello non lascia mai il dispositivo di hello.

la chiave pubblica di Hello è registrata con Azure Active Directory e Windows Server Active Directory (per locale). Il provider di identità (IDPs) convalida utente hello dalla chiave pubblica hello di mapping della chiave privata di hello utente toohello e fornisce informazioni di accesso tramite una volta Password (OTP), PhoneFactor o un meccanismo di notifica diversi.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Perché alle aziende conviene scegliere Windows Hello for Business?
L'abilitazione di Windows Hello for Business consente alle aziende di aumentare la protezione delle proprie risorse mediante:

* Configurazione di Windows Hello for Business con l'opzione preferita dall'hardware. Ciò significa che le chiavi verranno generate su TPM 1.2 o TPM 2.0, se disponibile. Quando il TPM non è disponibile, software genera chiave hello.
* Definizione hello complessità e la lunghezza di hello PIN e attivazione dell'utilizzo di Hello all'interno dell'organizzazione.
* Configurazione Windows Hello per scenari di utilizzo delle smart card simile toosupport tramite trust basata sui certificati.

## <a name="how-windows-hello-for-business-works"></a>Come funziona Windows Hello for Business
1. Vengono generate chiavi hardware hello TPM o software. Molti dispositivi presentano un chip TPM incorporato che protegge hardware hello integrando le chiavi di crittografia ai dispositivi. TPM 1.2 o TPM 2.0 genera chiavi o certificati creati dalle chiavi hello generato.
2. Hello TPM attesta queste chiavi hardware associato.
3. Un movimento unlock singolo Sblocca dispositivo hello. Questa azione consente toomultiple di accedere alle risorse se il dispositivo di hello è dominio o di Azure fanno parte di Active Directory.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Funzionamento di hello Windows Hello per ciclo di vita di Business
![Ciclo di vita di Windows Hello for Business](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Hello diagramma precedente illustra coppia di chiavi pubblica/privata hello e convalida hello dal provider di identità hello. Ognuno di questi passaggi è illustrato in dettaglio di seguito:

1. utente Hello dimostra la propria identità tramite più metodi correzione predefiniti (movimenti, smart card fisiche, multi-factor authentication) e invia questo tooan informazioni del Provider di identità (IDP) come Azure Active Directory o Active Directory locale.
2. dispositivo Hello quindi Crea chiave hello, attesta chiave hello, accetta parte pubblica di hello di questa chiave, viene associato con le istruzioni di stazione, accede e Invia chiave di hello tooregister toohello IDP.
3. Non appena hello IDP registra parte pubblica di hello della chiave di hello, sfide IDP hello hello toosign dispositivo con una parte di chiave hello privata hello.
4. viene quindi convalidato Hello IDP e problemi hello token di autenticazione che consente di utente hello e hello dispositivo accedere hello protetto alle risorse. IDPs scrivere App multipiattaforma o utilizzare toocreate supporto (tramite le API JavaScript/Webcrypto) del browser e usare Windows Hello per le credenziali aziendali per i propri utenti.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Hello requisiti di distribuzione per Windows Hello for Business
### <a name="at-hello-enterprise-level"></a>Livello di organizzazione hello
* enterprise Hello ha una sottoscrizione Azure.

### <a name="at-hello-user-level"></a>A livello di utente hello
* computer dell'utente Hello viene eseguito Windows 10 Professional o Enterprise.

Per istruzioni dettagliate sulla distribuzione, vedere [abilitare Windows Hello for Business organizzazione hello](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Informazioni aggiuntive
* [Windows 10 per enterprise hello: i dispositivi toouse modi per lavoro](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Scenari di utilizzo per Aggiunta ad Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connettersi tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurare Aggiunta di Azure AD](active-directory-azureadjoin-setup.md)

