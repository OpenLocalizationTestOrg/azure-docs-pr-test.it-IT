---
title: aaaChoose tra server o cloud di Azure MFA | Documenti Microsoft
description: "Scegliere una soluzione di sicurezza di multi-factor authentication hello è adatta alle proprie esigenze richiedendo, quali am si sta tentando di toosecure e dove sono gli utenti si trova.  Scegliere quindi cloud, Server di autenticazione a più fattori o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Scegliere una soluzione di Azure multi-Factor Authentication hello automaticamente
Poiché sono presenti diverse versioni di Azure multi-Factor Authentication (MFA), è necessario rispondere alcune domande toofigure, la versione è uno toouse appropriato hello.  Le domande sono:

* [Cosa sto cercando toosecure](#what-am-i-trying-to-secure)
* [Dove si trovano gli utenti di hello](#where-are-the-users-located)
* [Quali funzionalità sono necessarie?](#what-featured-do-i-need)

Hello nelle sezioni seguenti forniscono istruzioni su come determinare ognuna di queste risposte.

## <a name="what-am-i-trying-toosecure"></a>Cosa sto cercando toosecure?
soluzione di verifica in due passaggi corretta hello toodetermine, innanzitutto è necessario rispondere alla domanda hello di quali sono si toosecure durante il tentativo con un secondo metodo di autenticazione.  Si tratta di un'applicazione in Azure?  Oppure di un sistema di accesso remoto?  Mediante la determinazione di ciò che si sta tentando toosecure, possiamo rispondere alla domanda hello in cui multi-Factor Authentication deve toobe abilitato.  

| Quali sono toosecure durante il tentativo | Autenticazione a più fattori nel cloud hello | Server MFA |
| --- |:---:|:---:|
| App prodotte direttamente da Microsoft |● |● |
| App SaaS nella raccolta di app hello |● |  |
| Applicazioni Web pubblicate tramite il proxy di applicazione di Azure AD |● |  |
| Le applicazioni IIS non pubblicate tramite proxy app per Azure AD | |● |
| Accesso remoto, ad esempio VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Dove si trovano gli utenti di hello
Successivamente, analizzando in cui si trovano gli utenti consente di toodetermine hello soluzione corretta toouse, se nel cloud di hello o in locale con hello Server MFA.

| Ubicazione degli utenti | Autenticazione a più fattori nel cloud hello | Server MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD e AD locale usando la federazione con AD FS |● |● |
| Azure AD e AD locale con DirSync, Azure AD Sync, Azure AD Connect, senza sincronizzazione di password |● |● |
| Azure AD e AD locale con DirSync, Azure AD Sync, Azure AD Connect, con sincronizzazione di password |● | |
| Active Directory locale | |● |

## <a name="what-features-do-i-need"></a>Quali funzionalità sono necessarie?
Hello nella tabella seguente vengono confrontate hello funzionalità disponibili con multi-Factor Authentication nel cloud hello e hello Server multi-Factor Authentication.

| Funzionalità | Autenticazione a più fattori nel cloud hello | Server MFA |
| --- |:---:|:---:|
| Notifica dell'app per dispositivi mobili come secondo fattore | ● | ● |
| Codice di verifica dell'app per dispositivi mobili come secondo fattore | ● | ● |
| Chiamata telefonica come secondo fattore | ● | ● |
| SMS unidirezionale come secondo fattore | ● | ● |
| SMS bidirezionale come secondo fattore | | ● |
| Token hardware come secondo fattore | | ● |
| Password di app per i client Office 365 che non supportano MFA | ● | |
| Controllo amministrazione sui metodi di autenticazione | ● | ● |
| Modalità PIN | | ● |
| Avviso di illecito |● | ● |
| Report MFA |● | ● |
| Bypass monouso | | ● |
| Messaggi di saluto personalizzati per le telefonate | ● | ● |
| ID chiamante personalizzabile per le telefonate | ● | ● |
| IP attendibili | ● | ● |
| Memorizzazione di MFA per dispositivi attendibili | ● | |
| Accesso condizionale | ● | ● |
| Cache |  | ● |

## <a name="next-steps"></a>Passaggi successivi

Ora che abbiamo determinato se toouse cloud multi-factor authentication o hello Server MFA locale, è possibile iniziare a configurare e tramite Azure multi-Factor Authentication. **Selezionare l'icona di hello che rappresenti lo scenario**

<center>




[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
