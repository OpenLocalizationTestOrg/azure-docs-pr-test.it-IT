---
title: 'Azure Active Directory Domain Services: Aggiornare le impostazioni DNS per hello rete virtuale di Azure | Documenti Microsoft'
description: Introduzione a Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Aggiornare le impostazioni DNS per hello rete virtuale di Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Attività 4: Aggiornare le impostazioni DNS per hello rete virtuale di Azure
In hello precedenti attività di configurazione, si attiva Azure Active Directory Domain Services per la directory. attività successiva Hello è tooensure che i computer in rete virtuale hello possono connettersi e utilizzare tali servizi. In questo articolo, aggiornare le impostazioni del server DNS hello per il rete virtuale toopoint toohello due indirizzi IP in Azure Active Directory Domain Services è disponibile nella rete virtuale hello.

> [!NOTE]
> Dopo aver abilitato Azure Active Directory Domain Services per la directory di hello, annotare gli indirizzi IP hello per Azure Active Directory Domain Services visualizzate in hello **configura** della directory.
>
>

tooupdate hello impostazioni del server DNS per la rete virtuale di hello in cui è stato abilitato Azure Active Directory Domain Services hello completo alla procedura seguente:

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro sinistro hello selezionare **reti**.  
    Hello **reti** verrà visualizzata la finestra.

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. In hello **reti virtuali** scheda, rete virtuale di hello select in cui è abilitato Azure Active Directory Domain Services tooview le relative proprietà.
4. Fare clic su hello **configura** scheda.

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. In hello **server DNS** immettere entrambi indirizzi IP hello che sono stati visualizzati in hello **servizi di dominio** sezione hello **configura** della directory.
6. Fare clic su impostazioni del server DNS hello toosave per la rete virtuale, nel riquadro attività hello nella parte inferiore di hello della finestra hello **salvare**.

   ![Aggiornare le impostazioni del server per la rete virtuale hello hello DNS](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Macchine virtuali nella rete hello ottenere solo le nuove impostazioni DNS di hello dopo un riavvio. Se sono necessarie le impostazioni DNS di tooget hello aggiornato immediatamente, attivare un riavvio di un portale hello, PowerShell o hello CLI.
>
>

## <a name="next-steps"></a>Passaggi successivi
Attività 5: [abilitare tooAzure di sincronizzazione password servizi di dominio Active Directory](active-directory-ds-getting-started-password-sync.md)
