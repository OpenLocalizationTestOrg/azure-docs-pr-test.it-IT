---
title: 'Azure Active Directory Domain Services: abilitare Azure Active Directory Domain Services | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Attività 3: Abilitare Azure Active Directory Domain Services
In questa attività, abilitare Servizi di dominio Active Directory Azure (Azure AD DS) per la directory effettuando hello alla procedura seguente:

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro sinistro hello selezionare hello **Active Directory** pulsante.
3. Selezionare tenant di Azure Active Directory (Azure AD) hello (directory) per il quale si desidera tooenable Azure Active Directory.

    ![Selezionare una directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. In hello **directory anteprima** pagina, fare clic su hello **configura** scheda.

    ![Scheda Configura della directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. In **servizi di dominio**, modificare hello **Abilita servizi di dominio per questa directory** opzione troppo**Sì**.  
    Ulteriori opzioni di configurazione di Azure Active Directory Domain Services visualizzati nella pagina di hello.

    ![Abilita servizi di dominio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Quando si abilita Azure Active Directory Domain Services per il tenant, Azure AD genera e archivia hello Kerberos e NTLM degli hash delle credenziali necessarie per l'autenticazione degli utenti.
   >
   >
6. Specificare hello **nome di dominio DNS di servizi di dominio**.

   * nome di dominio Hello predefinito della directory hello (con un **. c o m** suffisso) è selezionata per impostazione predefinita.

   * Hello elenco contiene tutti i domini che sono stati configurati per la directory di Azure AD, inclusi sia verificato e non verificati domini configurati nel hello **domini** scheda.

   * È inoltre possibile immettere un nome di dominio personalizzato. In questo esempio, è il nome di dominio personalizzato hello *contoso100.com*.

     > [!WARNING]
     > prefisso Hello del nome del dominio specificato (ad esempio, *contoso100* in hello *contoso100.com* nome di dominio) deve contenere meno di 15 caratteri. Non è possibile creare un dominio di Azure Active Directory Domain Services con un prefisso contenente più di 15 caratteri.
     >
     >
7. Verificare il nome di dominio DNS hello che scelto per hello gestito dominio non esiste già nella rete virtuale hello. In particolare, controllare se toosee:

   * Si dispone già di un dominio con hello stesso nome di dominio DNS nella rete virtuale hello.

   * rete virtuale selezionata Hello ha una connessione VPN alla rete locale e si dispone di un dominio con hello stesso nome di dominio DNS nella rete locale.

   * È un servizio cloud esistente con lo stesso nome nella rete virtuale hello.
8. Selezionare una rete virtuale in cui si desidera toobe di Azure Active Directory Domain Services disponibili. Selezionare la rete virtuale hello e una subnet dedicata creata in hello **toothis di rete virtuale di servizi di dominio Connetti** elenco a discesa. Considerare anche l'esempio hello:

   * Verificare che tale rete virtuale hello specificato appartiene tooan area di Azure supportati da servizi di dominio di Azure Active Directory. tooascertain hello aree di Azure in cui servizi di dominio di Azure Active Directory è disponibili, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).

   * Reti virtuali appartenenti tooa area in cui i servizi di dominio di Azure Active Directory non è supportato non vengono visualizzati nell'elenco a discesa hello.

   * Utilizzare una subnet dedicata all'interno di rete virtuale hello per servizi di dominio di Azure Active Directory. Eseguire *non* selezionare hello subnet del gateway. Vedere le [considerazioni sulla rete](active-directory-ds-networking.md).

   * Analogamente, le reti virtuali che sono state create usando Gestione risorse di Azure non vengono visualizzati nell'elenco a discesa hello. Le reti virtuali basate su Resource Manager attualmente non sono supportate da Azure Active Directory Domain Services.
9. Fare clic su tooenable Azure Active Directory Domain Services, nel riquadro attività hello nella parte inferiore di hello della pagina hello **salvare**.
    * Servizi di dominio di Azure Active Directory è abilitato per la directory, pagina hello Visualizza lo stato di *in sospeso*.

        ![Finestra Abilita Domain Services](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services garantisce un'elevata disponibilità per il dominio gestito. Dopo aver abilitato Servizi di dominio di Azure Active Directory, gli indirizzi IP di hello del dominio sono disponibili nella rete virtuale hello servizi sono visualizzati uno alla volta. secondo indirizzo IP di Hello viene visualizzato in primo luogo, poco dopo hello appena servizio hello consente una disponibilità elevata per il dominio. Quando è configurata la disponibilità elevata e attivo per il dominio, vengono visualizzati due indirizzi IP in hello **servizi di dominio** sezione di hello **configura** scheda.
        >
        >
    * Dopo circa 20 minuti too30, hello primo indirizzo IP del dominio servizi disponibili nella rete virtuale in hello **indirizzo IP** campo hello **configura** pagina.

        ![La finestra di Domain Service visualizza il primo indirizzo IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Quando la disponibilità elevata è operativa per il dominio, i due indirizzi IP vengono visualizzati nella pagina hello. Il dominio gestito è disponibile nella rete virtuale selezionata a questi due indirizzi IP.

10. Si noti due indirizzi IP di hello in modo che sia possibile aggiornare le impostazioni DNS hello per la rete virtuale. In questo modo consente alle macchine virtuali nel dominio di hello rete virtuale tooconnect toohello per operazioni quali aggiunta al dominio.

    ![La finestra di Domain Services mostra entrambi gli IP di cui è stato eseguito il provisioning](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> A seconda delle dimensioni di hello del tenant di Azure AD (ad esempio, numero hello di utenti o gruppi), dominio di sincronizzazione tooyour gestito richiede un certo tempo. Questo processo di sincronizzazione viene eseguita in background hello. Per i tenant con decine di migliaia di oggetti di grandi dimensioni, potrebbe richiedere un o due giorni per tutti gli utenti, appartenenze a gruppi e credenziali toobe sincronizzato.
>
>

## <a name="next-step"></a>Passaggio successivo
[Attività 4: aggiornare le impostazioni DNS di hello per hello rete virtuale di Azure](active-directory-ds-getting-started-update-dns.md)
