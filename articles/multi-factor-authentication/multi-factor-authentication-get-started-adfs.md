---
title: "verifica aaaTwo passaggio e AD FS - autenticazione a più fattori di Azure | Documenti Microsoft"
description: "Si tratta hello Azure multi-Factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA e AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Introduzione a Azure Multi-Factor Authentication e Active Directory Federation Services
<center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Se l'organizzazione ha federato l'istanza locale di Active Directory con Azure Active Directory tramite AD FS, sono disponibili due opzioni per l'uso di Azure Multi-Factor Authentication.

* Proteggere le risorse cloud mediante Azure Multi-Factor Authentication o Active Directory Federation Services
* Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication

Hello nella tabella seguente sono riepilogati hello esperienza di verifica della protezione delle risorse con Azure multi-Factor Authentication e AD FS

| Esperienza di verifica - App basate su browser | Esperienza di verifica - App non basate su browser |
|:--- |:--- |:--- |
| Proteggere le risorse Azure AD utilizzando Azure Multi-Factor Authentication |<li>il primo passaggio di verifica Hello viene eseguita in locale con ADFS.</li> <li>secondo passaggio Hello è un metodo basato su telefono eseguito mediante l'autenticazione cloud.</li> |
| Proteggere le risorse di Azure AD con Active Directory Federation Services |<li>il primo passaggio di verifica Hello viene eseguita in locale con ADFS.</li><li>secondo passaggio Hello viene eseguito localmente rispettando l'attestazione hello.</li> |

Avvertenze per le password dell’app rivolte agli utenti federati:

* Le password dell'app vengono verificate mediante l'autenticazione cloud e di conseguenza ignorano la federazione. La federazione viene usata attivamente solo durante l'impostazione della password dell'app.
* Le impostazioni locali di Controllo di accesso client non vengono rispettate dalle password dell'app.
* Si perde la funzionalità di registrazione dell'autenticazione locale per le password dell'app.
* Disabilitazione o eliminazione di account potrebbe richiedere ore toothree per la sincronizzazione della directory, ritardando disabilitazione o eliminazione di password di app nell'identità cloud hello.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulla configurazione di Azure multi-Factor Authentication o hello Server Azure multi-Factor Authentication con ADFS, vedere hello seguenti articoli:

* [Proteggere le risorse cloud mediante Azure Multi-Factor Authentication e ADFS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Proteggere le risorse del cloud e locali mediante Server Azure multi-Factor Authentication con ADFS Server Windows 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Proteggere le risorse del cloud e locali mediante Server Azure Multi-Factor Authentication con AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
