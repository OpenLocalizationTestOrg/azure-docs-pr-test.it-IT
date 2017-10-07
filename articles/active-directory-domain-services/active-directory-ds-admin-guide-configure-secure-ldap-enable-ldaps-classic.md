---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Attività 3: abilitare l'accesso LDAP sicuro per hello dominio gestito tramite il portale di Azure classico di hello
tooenable secure LDAP, eseguire hello seguendo i passaggi di configurazione:

1. Passare toohello  **[portale di Azure classico](https://manage.windowsazure.com)**.
2. Seleziona hello **Active Directory** nodo nel riquadro di sinistra hello.
3. Selezionare hello Azure Active directory (anche noto tooas 'tenant'), per cui sono stati abilitati i servizi di dominio Active Directory di Azure.

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Fare clic su hello **configura** scheda.

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Scorrere verso il basso toohello sezione **servizi di dominio**. Dovrebbe essere un'opzione denominata **LDAP sicuro (LDAPS)** come illustrato nella seguente schermata hello:

    ![Sezione per la configurazione di Servizi di dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Fare clic su hello **Configura certificato...**  toobring pulsante backup hello **Configura certificato per l'accesso LDAP sicuro** finestra di dialogo.

    ![Configura certificato per accesso LDAP sicuro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Fare clic su seguenti sull'icona di cartella hello **FILE PFX con certificato** file PFX hello toospecify, che contiene il certificato di hello da toouse per toohello di accesso LDAP sicuro gestito dominio. Anche immettere password hello specificata durante l'esportazione di file PFX del certificato toohello hello. Quindi, fare clic su Fatto pulsante nella parte inferiore di hello hello.

    ![Specificare un file PFX di accesso LDAP sicuro e la password](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hello **servizi di dominio** sezione di hello **configura** scheda deve ottenere visualizzato in grigio ed è in hello **in sospeso...**  dello stato per alcuni minuti. Durante questo periodo, certificato LDAPS hello viene verificata per verificarne l'accuratezza e la protezione di LDAP è configurato per il dominio gestito.

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Sono necessari circa 10 minuti too15 tooenable LDAP sicuro per il dominio gestito. Se hello fornito certificato LDAP sicuro non corrisponde a hello richiesto criteri, accesso LDAP sicuro non è abilitato per la directory e viene visualizzato un errore. Ad esempio, il nome di dominio hello non è corretto, certificato hello è già scaduto o scadrà a breve.
   >
   >

9. Quando l'accesso LDAP sicuro è abilitata per il dominio gestito, hello **in sospeso...**  messaggio dovrebbe essere eliminato. Verrà visualizzata l'identificazione personale hello del certificato hello visualizzato.

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Attività 4: abilitare l'accesso LDAP sicuro tramite hello internet
**Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.

Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Si noterà un'opzione troppo**hello abilitare SECURE LDAP accesso tramite INTERNET** in hello **servizi di dominio** sezione di hello **configura** pagina. Questa opzione è impostata troppo**n** per impostazione predefinita poiché toohello accesso internet gestito dominio tramite LDAP sicuro è disabilitato per impostazione predefinita.

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Attiva/disattiva **hello abilitare SECURE LDAP accesso tramite INTERNET** troppo**Sì**. Fare clic su hello **salvare** pulsante sul pannello inferiore hello.
    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hello **servizi di dominio** sezione di hello **configura** scheda deve ottenere visualizzato in grigio ed è in hello **in sospeso...**  dello stato per alcuni minuti. Dopo un po' di tempo è abilitato internet dominio gestito tooyour accesso LDAP sicuro.

    ![LDAP sicuro - In sospeso](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Sono necessari circa 10 minuti tooenable accesso a internet tramite LDAP sicuro per il dominio gestito.
   >
   >
4. Quando si tooyour di accesso LDAP sicuro dominio su hello internet è abilitata, hello **in sospeso...**  messaggio dovrebbe essere eliminato. Si dovrebbe essere indirizzo IP esterno hello possono essere utilizzati tooaccess directory over LDAPS nel campo hello **IP indirizzo per LDAPS accesso esterno**.

    ![LDAP sicuro abilitato](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Attività 5: configurare DNS tooaccess hello dominio gestito da hello internet
**Attività facoltative** : se non si prevede tooaccess hello dominio gestito utilizza LDAPS oltre hello internet, ignorare questa attività di configurazione.

Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).

Dopo aver abilitato l'accesso LDAP sicuro tramite hello internet per il dominio gestito, è necessario tooupdate DNS in modo che i computer client possano trovare il dominio gestito. Alla fine di hello di attività 4, viene visualizzato un indirizzo IP esterno in hello **configura** scheda **IP indirizzo per LDAPS accesso esterno**.

Configurare il provider DNS esterno in modo che il nome DNS di hello del hello gestiti dominio (ad esempio, ' ldaps.contoso100.com') toothis punti l'indirizzo IP esterno. In questo esempio, è necessario hello toocreate voce DNS seguenti:

    ldaps.contoso100.com  -> 52.165.38.113

La procedura è: si è ora pronto tooconnect toohello gestito hello di dominio utilizzando LDAP sicuro tramite internet.

> [!WARNING]
> Tenere presente che i computer client devono considerare attendibile correttamente autorità emittente hello di hello LDAPS certificato toobe in grado di tooconnect toohello gestiti dominio utilizzando LDAP. Se si utilizza un'autorità di certificazione o di un'autorità di certificazione attendibile pubblicamente, non è necessario toodo alcuna operazione poiché i computer client attendibile queste autorità di certificazione. Se si utilizza un certificato autofirmato, è necessario tooinstall parte pubblica di hello del certificato autofirmato hello nell'archivio certificati attendibili hello in computer client hello.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Blocco LDAPS accedere dominio gestito tooyour su hello internet
> [!NOTE]
> **Attività facoltative** : se non è stato abilitato LDAPS accesso toohello gestito dominio oltre hello internet, ignorare questa attività di configurazione.
>
>

Prima di iniziare questa attività, assicurarsi di aver completato i passaggi di hello descritti in [attività 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
