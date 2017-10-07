---
title: "Porte e protocolli necessari per la soluzione ibrida di gestione delle identità | Microsoft Docs"
description: "Questa pagina è una pagina di riferimento tecnico per le porte necessarie toobe aperto per Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>Porte e protocolli necessari per la soluzione ibrida di gestione delle identità
Hello seguente documento è un riferimento tecnico su hello necessarie porte e protocolli per l'implementazione di una soluzione con identità ibrida. Fare riferimento a tabella corrispondente toohello utilizzare hello seguente illustrazione.

![Cos'è Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Tabella 1 - Azure AD Connect e AD locale
Questa tabella descrive hello porte e protocolli necessari per la comunicazione tra server di hello Azure AD Connect e Active Directory locale.

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |Ricerche DNS nella foresta di destinazione hello. |
| Kerberos |88 (TCP/UDP) |Foresta di toohello AD autenticazione Kerberos. |
| MS-RPC |135 (TCP/UDP) |Utilizzato durante la configurazione iniziale della procedura guidata di Azure AD Connect hello durante l'associazione di foresta di Active Directory toohello hello e durante la sincronizzazione delle Password. |
| LDAP |389 (TCP/UDP) |Usato per l'importazione di dati da Active Directory. I dati vengono crittografati con la firma e il sigillo Kerberos. |
| RPC | 445 (TCP/UDP) |Utilizzato toocreate SSO senza un account di computer nella foresta Active Directory hello. |
| LDAP/SSL |636 (TCP/UDP) |Usato per l'importazione di dati da Active Directory. trasferimento dati Hello viene firmato e crittografato. Usato solo se si utilizza SSL. |
| RPC |49152- 65535 (porta RPC elevata casuale)(TCP/UDP) |Utilizzato durante la configurazione iniziale di Azure AD Connect, durante l'associazione di insiemi di strutture Active Directory toohello hello e durante la sincronizzazione delle Password. Per altre informazioni, vedere gli articoli [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) e [KB224196](https://support.microsoft.com/kb/224196). |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Tabella 2 - Azure AD Connect e AD locale
La tabella seguente descrive hello porte e protocolli necessari per la comunicazione tra il server di Azure AD Connect hello e Azure AD.

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Utilizzare i certificati SSL tooverify di toodownload CRL (elenchi di revoca dei certificati). |
| HTTPS |443 (TCP/UDP) |Toosynchronize usato con Azure AD. |

Per un elenco degli URL e IP indirizzi necessari tooopen nel firewall, vedere [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Tabella 3 - Azure AD Connect e server federativi/WAP di AD FS
La tabella seguente descrive hello porte e protocolli necessari per la comunicazione tra il server di Azure AD Connect hello e server AD FS Federation/WAP.  

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Utilizzare i certificati SSL tooverify di toodownload CRL (elenchi di revoca dei certificati). |
| HTTPS |443 (TCP/UDP) |Toosynchronize usato con Azure AD. |
| WinRM |5985 |Listener di Gestione remota Windows |

## <a name="table-4---wap-and-federation-servers"></a>Tabella 4 - server federativi e WAP
La tabella seguente descrive hello porte e protocolli necessari per la comunicazione tra server federativi hello e server WAP.

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |Usato per l'autenticazione. |

## <a name="table-5---wap-and-users"></a>Tabella 5 - WAP e utenti
La tabella seguente descrive hello porte e protocolli necessari per la comunicazione tra server WAP hello e utenti.

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |Usato per l'autenticazione del dispositivo. |
| TCP |49443 (TCP) |Usato per l'autenticazione del certificato. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Tabella 6a e 6b - Autenticazione pass-through con Single Sign-On (SSO) e Sincronizzazione degli hash delle password con Single Sign-On (SSO)
Hello le tabelle seguenti vengono descritti hello porte e protocolli necessari per la comunicazione tra hello Azure AD Connect e Active Directory di Azure.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Tabella 6a - Autenticazione pass-through con SSO
|Protocol|Numero della porta|Descrizione
| --- | --- | ---
|HTTP|80|Abilitare il traffico HTTP in uscita per la convalida di sicurezza quale SSL. Anche necessari per il connettore hello aggiornamento automatico funzionalità toofunction correttamente.
|HTTPS|443| Abilitare il traffico HTTPS in uscita per operazioni quali l'abilitazione e disabilitazione della funzionalità di hello, la registrazione di connettori, il download degli aggiornamenti di connettore e gestisce tutte le richieste di utente.

Inoltre, Azure AD Connect deve toobe toomake in grado di connessioni dirette IP toohello [data center di Azure intervalli IP](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Tabella 6b - Sincronizzazione degli hash delle password con SSO

|Protocol|Numero della porta|Descrizione
| --- | --- | ---
|HTTPS|443| Abilitare la registrazione SSO (obbligatorio solo per il processo di registrazione SSO hello).

Inoltre, Azure AD Connect deve toobe toomake in grado di connessioni dirette IP toohello [data center di Azure intervalli IP](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Inoltre, questa è solo necessario per il processo di registrazione hello SSO.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabelle 7a e 7b - Agente di Azure AD Connect Health (AD FS/sincronizzazione) e Azure AD
Hello nelle tabelle seguenti vengono descritti gli endpoint di hello, porte e protocolli necessari per la comunicazione tra gli agenti di Azure AD Connect Health e Azure AD

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabella 7a - Porte e protocolli per l'agente di Azure AD Connect Health (AD FS/sincronizzazione) e Azure AD
La tabella seguente descrive hello seguenti porte in uscita e i protocolli necessari per la comunicazione tra gli agenti di hello Azure AD Connect Health e Azure AD.  

| Protocol | Porte | Descrizione |
| --- | --- | --- |
| HTTPS |443 (TCP/UDP) |In uscita |
| Bus di servizio di Azure |5671 (TCP/UDP) |In uscita |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b - Endpoint per l'agente di Azure AD Connect Health (AD FS/sincronizzazione) e Azure AD
Per un elenco di endpoint, vedere [hello sezione requisiti per l'agente di hello Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

