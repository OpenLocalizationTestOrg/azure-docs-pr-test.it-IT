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
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services

## <a name="before-you-begin"></a>Prima di iniziare
Assicurarsi di aver completato [attività 2 - esportazione hello sicura LDAP certificato tooa. Il file PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Scegliere se toouse hello anteprima esperienza del portale Azure oppure hello Azure toocomplete portale classico di questa attività.
> [!div class="op_single_selector"]
> * **Il portale di Azure (anteprima)**: [Enable secure LDAP utilizzando hello portale di Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portale di Azure classico**: [Enable secure LDAP utilizzando il portale di Azure classico di hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Attività 3: abilitare l'accesso LDAP sicuro per hello dominio gestito utilizzando hello del portale di Azure (anteprima)
tooenable secure LDAP, eseguire hello seguendo i passaggi di configurazione:

1. Passare toohello  **[portale di Azure](https://portal.azure.com)**.

2. Ricerca di "servizi di dominio' in hello **individuare risorse** casella di ricerca. Selezionare **servizi di dominio Active Directory di Azure** dai risultati di ricerca hello. Hello **servizi di dominio Active Directory di Azure** pannello elenca il dominio gestito.

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Fare clic su nome hello di hello gestito dominio (ad esempio, ' contoso100.com') toosee ulteriori dettagli su dominio hello.

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. Fare clic su **Secure LDAP** nel riquadro di spostamento hello.

    ![Domain Services - Pannello LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Per impostazione predefinita, l'accesso LDAP sicuro tooyour una dominio gestito è disabilitata. Attiva/disattiva **Secure LDAP** troppo**abilitare**.

    ![Abilitare LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Per impostazione predefinita, tooyour di accesso LDAP sicuro gestiti dominio tramite hello che Internet è disabilitato. Attiva/disattiva **Consenti l'accesso LDAP sicuro su internet di hello** troppo**abilitare**, se necessario. 

6. Fare clic su seguenti sull'icona di cartella hello **. Il file PFX con certificato LDAP sicuro**. Specificare file PFX di hello percorso toohello con certificato hello per accesso LDAP sicuro toohello una dominio gestita.

7. Specificare hello **toodecrypt Password. Il file PFX**. Fornire hello stessa password usata per l'esportazione di file PFX del certificato toohello hello.

8. Al termine, fare clic su hello **salvare** pulsante.

9. Viene visualizzata una notifica che informa l'utente che viene configurato per il dominio gestito hello LDAP sicuro. Fino a quando questa operazione è stata completata, è possibile modificare altre impostazioni per il dominio hello.

    ![Configurare il protocollo LDAP sicuro per il dominio gestito hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Sono necessari circa 10 minuti too15 tooenable LDAP sicuro per il dominio gestito. Se hello fornito certificato LDAP sicuro non corrisponde a hello richiesto criteri, accesso LDAP sicuro non è abilitato per la directory e viene visualizzato un errore. Ad esempio, il nome di dominio hello non è corretto, certificato hello è già scaduto o scadrà a breve. In questo caso, riprovare con un certificato valido.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Attività 4: configurare DNS tooaccess hello dominio gestito da hello internet
> [!NOTE]
> **Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.
>
>

Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Dopo aver abilitato l'accesso LDAP sicuro tramite hello internet per il dominio gestito, è necessario tooupdate DNS in modo che i computer client possano trovare il dominio gestito. Alla fine di hello di attività 3, viene visualizzato un indirizzo IP esterno in hello **proprietà** pannello in **IP indirizzo per LDAPS accesso esterno**.

Configurare il provider DNS esterno in modo che il nome DNS di hello del hello gestiti dominio (ad esempio, ' ldaps.contoso100.com') toothis punti l'indirizzo IP esterno. In questo esempio, è necessario hello toocreate voce DNS seguenti:

    ldaps.contoso100.com  -> 52.165.38.113

La procedura è: si è ora pronto tooconnect toohello gestito hello di dominio utilizzando LDAP sicuro tramite internet.

> [!WARNING]
> Tenere presente che i computer client devono considerare attendibile correttamente autorità emittente hello di hello LDAPS certificato toobe in grado di tooconnect toohello gestiti dominio utilizzando LDAP. Se si utilizza un'autorità di certificazione attendibile pubblicamente, non è necessario toodo alcuna operazione poiché i computer client attendibile queste autorità di certificazione. Se si utilizza un certificato autofirmato, è possibile installare parte pubblica di hello del certificato autofirmato hello nell'archivio certificati attendibili hello in computer client hello.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Attività 5 - blocco LDAPS accesso tooyour gestiti hello di dominio tramite internet
> [!NOTE]
> **Attività facoltative** : se non è stato abilitato LDAPS accesso toohello gestito dominio oltre hello internet, ignorare questa attività di configurazione.
>
>

Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Esporre il dominio gestito per l'accesso LDAPS su hello internet rappresenta una minaccia alla sicurezza. Hello dominio gestito è raggiungibile da hello internet hello porta utilizzata per l'accesso LDAP sicuro (ovvero, la porta 636). Pertanto, è possibile scegliere toorestrict accesso toohello gestito dominio toospecific noti gli indirizzi IP. Per migliorare la sicurezza, creare un gruppo di sicurezza di rete (gruppo) e associarlo a subnet hello in cui sono abilitati i servizi di dominio Active Directory di Azure.

Hello tabella seguente viene illustrato un esempio di gruppo è possibile configurare, toolock verso il basso l'accesso LDAP sicuro tramite hello internet. Hello gruppo contiene un set di regole che consentono l'accesso LDAPS in ingresso sulla porta TCP 636 solo da un set specificato di indirizzi IP. Hello predefinito 'DenyAll' regola verrà applicata tooall il traffico in ingresso di hello internet. Hello NSG regola tooallow LDAPS tramite hello internet da indirizzi IP specificati ha una priorità maggiore hello regola DenyAll NSG.

![Esempio NSG toosecure LDAPS tramite hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Altre informazioni** - [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)

<br>

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Amministrare i Criteri di gruppo in un dominio gestito da Azure AD Domain Services)
* [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)
* [Creare un gruppo di sicurezza di rete](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
