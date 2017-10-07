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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Abilitare Azure Active Directory Domain Services (anteprima)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Attività 4: aggiornare le impostazioni DNS per hello rete virtuale di Azure
In hello precedenti attività di configurazione, si attiva Azure Active Directory Domain Services per la directory. attività successiva Hello è tooensure che i computer in rete virtuale hello possono connettersi e utilizzare tali servizi. In questo articolo, aggiornare le impostazioni del server DNS hello per il rete virtuale toopoint toohello due indirizzi IP in Azure Active Directory Domain Services è disponibile nella rete virtuale hello.

tooupdate hello impostazioni del server DNS per la rete virtuale di hello in cui è stato abilitato Azure Active Directory Domain Services hello completo alla procedura seguente:

1. Hello **Panoramica** scheda Elenca un set di **necessari passaggi di configurazione** toobe eseguita dopo che il dominio gestito viene eseguito il provisioning completo. primo passaggio di configurazione Hello è **impostazioni del server DNS di aggiornamento per la rete virtuale**.

    ![Domain Services - Scheda Panoramica al termine del provisioning](./media/getting-started/domain-services-provisioned-overview.png)

2. Quando il provisioning del dominio è stato completato, in questo riquadro vengono visualizzati due indirizzi IP. Ogni indirizzo IP rappresenta un controller di dominio per il dominio gestito.

3. primo indirizzo IP hello toocopy indirizzo tooclipboard, fare clic su hello copia pulsante Avanti tooit. Quindi fare clic su hello **server configurare DNS** pulsante.

4. Incollare l'indirizzo IP prima hello hello **server DNS aggiungere** casella di testo in hello **server DNS** blade. Scorrere orizzontalmente toohello toocopy hello secondo indirizzo IP a sinistra e incollarlo in hello **server DNS aggiungere** casella di testo.

    ![Domain Services - Aggiornamento di DNS](./media/getting-started/domain-services-update-dns.png)

5. Fare clic su **salvare** una volta completate i server DNS per la rete virtuale hello tooupdate hello.

> [!NOTE]
> Macchine virtuali nella rete hello ottenere solo le nuove impostazioni DNS di hello dopo un riavvio. Se sono necessarie le impostazioni DNS di tooget hello aggiornato immediatamente, attivare un riavvio di un portale hello, PowerShell o hello CLI.
>
>

## <a name="next-step"></a>Passaggio successivo
[Attività 5: abilitare la sincronizzazione di password tooAzure servizi di dominio Active Directory](active-directory-ds-getting-started-password-sync.md)
