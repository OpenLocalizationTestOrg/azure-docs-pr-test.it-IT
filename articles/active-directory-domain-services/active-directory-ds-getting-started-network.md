---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)


## <a name="before-you-begin"></a>Prima di iniziare
Fare riferimento troppo[considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Attività 2: configurare le impostazioni di rete
attività di configurazione successiva Hello è toocreate una rete virtuale di Azure e una subnet dedicata all'interno di esso. Abilitare Azure Active Directory Domain Services in questa subnet all'interno della rete virtuale. È anche possibile selezionare una rete virtuale esistente e creare subnet hello dedicata all'interno di esso.

1. Fare clic su **rete virtuale** tooselect una rete virtuale.
2. In hello **rete virtuale scegliere** pannello viene visualizzato di tutte le reti virtuali esistenti. Viene visualizzato solo hello reti virtuali che appartengono al gruppo di risorse toohello e località di Azure selezionato nell'hello **nozioni di base** pagina della procedura guidata.

3. Scegliere hello di rete virtuale in cui i servizi di dominio Active Directory di Azure devono essere abilitati. Fare clic su **Crea nuovo**, se si preferisce toocreate una nuova rete virtuale. È consigliabile l'utilizzo di una subnet dedicata per Azure AD Domain Services. Se si seleziona una rete virtuale esistente, [creare una subnet dedicata con estensione reti virtuali hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , quindi selezionare la subnet. 

    ![Selezionare una rete virtuale](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Fare clic su **Subnet** toopick hello subnet dedicata in questa rete virtuale, all'interno delle quali tooenable nuova gestiti dominio. In hello **creare subnet** pannello, specificare un nome per la subnet hello e fare clic su **OK** al termine. Ad esempio, creare una subnet con nome hello 'DomainServices', consentendo agli altri amministratori toounderstand ciò che viene distribuito all'interno di subnet hello.

    ![Selezionare subnet all'interno di rete virtuale hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Linee guida per la selezione di una subnet**
  > 1. Usare una subnet dedicata per Azure AD Domain Services. Non distribuire qualsiasi altra subnet toothis di macchine virtuali. Questa configurazione consente tooconfigure rete sicurezza gruppi per le macchine virtuali o i carichi di lavoro senza interromperne il dominio gestito. Per i dettagli vedere [Considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Non selezionare subnet del Gateway hello per la distribuzione di servizi di dominio Active Directory di Azure, perché non è una configurazione supportata.
  3. Verificare che tale subnet hello selezionata dispone di sufficiente spazio degli indirizzi disponibile - indirizzi IP disponibili almeno 3-5.
  >

5. Al termine, fare clic su **OK** toomove su toohello **gruppo amministratore** pagina della procedura guidata hello.


## <a name="next-step"></a>Passaggio successivo
[Attività 3: configurare un gruppo amministrativo e abilitare Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
