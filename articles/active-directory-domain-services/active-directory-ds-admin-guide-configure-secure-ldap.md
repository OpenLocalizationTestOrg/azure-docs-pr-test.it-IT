---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services
Questo articolo illustra come abilitare l'accesso LDAPS (Secure Lightweight Directory Access Protocol) per il dominio gestito di Servizi di dominio Azure AD. L'accesso LDAP sicuro è noto anche come LDAP (Lightweight Directory Access Protocol) su SSL (Secure Sockets Layer) / TLS (Transport Layer Security).

## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).
4. Oggetto **tooenable toobe utilizzato certificato secure LDAP**.

   * È **consigliabile** ottenere un certificato da un'autorità di certificazione pubblica attendibile. Questa opzione di configurazione è più sicura.
   * In alternativa, è possibile anche scegliere troppo[creare un certificato autofirmato](#task-1---obtain-a-certificate-for-secure-ldap) come illustrato più avanti in questo articolo.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Requisiti di certificato LDAP sicuro hello
Acquisire un certificato valido per hello seguendo le istruzioni, prima di abilitare accesso LDAP sicuro. Si verificano errori, se si tenta di tooenable LDAP sicuro per il dominio gestito con un certificato non valido o corretto.

1. **Autorità emittente attendibile** -hello certificato deve essere emesso da un'autorità attendibile dai computer che si connettono toohello dominio gestito utilizzando il protocollo LDAP sicuro. L'autorità può essere un'autorità di certificazione pubblica considerata attendibile da questi computer.
2. **Durata** -hello certificato deve essere valido per almeno hello Avanti 3-6 mesi. Scadenza del certificato hello, accesso LDAP sicuro tooyour una dominio gestito non è disponibile.
3. **Nome del soggetto** -nome del soggetto hello certificato hello deve essere un carattere jolly per il dominio gestito. Ad esempio, se il dominio è denominato 'contoso100.com', nome del soggetto del certificato hello deve essere ' *. contoso100.com'. Impostare il nome di carattere jolly toothis hello DNS nome (nome alternativo soggetto).
4. **Utilizzo chiave** - hello certificato deve essere configurato per hello seguente utilizza - firme digitali e crittografia chiave.
5. **Scopo del certificato** -hello certificato deve essere valido per l'autenticazione server SSL.

> [!NOTE]
> **Autorità di certificazione globali (enterprise):** Azure AD Domain Services non supporta l'uso di certificati LDAP sicuri rilasciati dall'autorità di certificazione globale (enterprise) dell'organizzazione. Questa restrizione è perché il servizio di hello non considera attendibile la CA come autorità di certificazione radice dell'organizzazione. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Attività 1: Ottenere un certificato per l'accesso LDAP sicuro
Hello prima attività comporta l'acquisizione di un certificato utilizzato per l'accesso LDAP sicuro toohello una dominio gestito. Sono disponibili due opzioni:

* Ottenere un certificato da un'autorità di certificazione. autorità Hello potrebbe essere un'autorità di certificazione pubblica.
* Creare un certificato autofirmato.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Opzione A (scelta consigliata): ottenere un certificato LDAP sicuro da un'autorità di certificazione
Se l'organizzazione Ottiene i certificati da un'autorità di certificazione pubblica, è necessario certificati secure LDAP tooobtain hello da tale autorità di certificazione pubblica.

Quando viene richiesto un certificato, assicurarsi che siano soddisfatti tutti i requisiti di hello descritti [requisiti di certificato LDAP sicuro hello](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Computer client che devono tooconnect toohello dominio gestito utilizzando il protocollo LDAP sicuro deve emittente hello del certificato LDAP sicuro hello.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Opzione B: creare un certificato autofirmato per l'accesso LDAP sicuro
Se non si prevede di toouse un certificato da un'autorità di certificazione pubblica, è possibile scegliere toocreate un certificato autofirmato per l'accesso LDAP sicuro.

**Creare un certificato autofirmato con PowerShell**

Nel computer Windows, aprire una nuova finestra di PowerShell come **amministratore** e hello tipo seguendo i comandi, toocreate un nuovo certificato autofirmato.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

Nel precedente esempio di hello, sostituire "*. contoso100.com' con nome di dominio DNS hello del dominio gestito. Ad esempio, se è stato creato un dominio gestito chiamato 'contoso100.onmicrosoft.com', sostituire "*. contoso100.com' in hello di sopra di script con ' *. contoso100.onmicrosoft.com').

![Selezionare una directory di Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

certificato autofirmato Hello appena creato viene inserito nell'archivio certificati del computer locale hello.


## <a name="next-step"></a>Passaggio successivo
[Attività 2: esportare hello sicura LDAP certificato tooa. File PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
