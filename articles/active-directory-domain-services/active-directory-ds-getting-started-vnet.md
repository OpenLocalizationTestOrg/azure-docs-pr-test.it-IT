---
title: 'Azure Active Directory Domain Services: creare o selezionare una rete virtuale | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>Creare o selezionare una rete virtuale per Azure Active Directory Domain Services
## <a name="before-you-begin"></a>Prima di iniziare
Fare riferimento troppo[considerazioni sulla rete per Azure Active Directory Domain Services](active-directory-ds-networking.md).

## <a name="task-2-create-an-azure-virtual-network"></a>Attività 2: Creare una rete virtuale di Azure
attività di configurazione successiva Hello è toocreate una rete virtuale di Azure e una subnet all'interno di esso. Abilitare Azure Active Directory Domain Services in questa subnet all'interno della rete virtuale. Se si dispone di una rete virtuale esistente che si preferisce toouse, è possibile ignorare questo passaggio.

> [!NOTE]
> Verificare che tale rete virtuale di Azure creare o scegliere toouse con Azure Active Directory Domain Services appartiene tooan area di Azure è supportato da Azure Active Directory Domain Services hello. tooascertain hello aree di Azure in cui sono disponibili servizi di dominio di Azure Active Directory, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).
>
>Annotare il nome di hello di hello tooensure di rete virtuale selezionare la rete virtuale a destra di hello quando si abilita Azure Active Directory Domain Services in un passaggio di configurazione successive.


toocreate una rete virtuale di Azure in cui si desidera tooenable Azure Active Directory Domain Services, seguire queste istruzioni di configurazione:

1. Passare toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nel riquadro sinistro hello selezionare **reti**.

    ![Nodi di reti](./media/active-directory-domain-services-getting-started/networks-node.png)  
    Hello **reti virtuali** verrà visualizzata la finestra.
3. Nel riquadro delle attività hello nella parte inferiore di hello della finestra hello, fare clic su **New**.

    ![Finestra delle reti virtuali](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. Fare clic su **Servizi di rete**, quindi selezionare **Rete virtuale**.

    ![Rete virtuale - creazione rapida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. Fare clic su una rete virtuale, toocreate **creazione rapida**.

6. Specificare un **nome** per la macchina di rete e provare a eseguire operazioni hello seguenti:
    * È possibile scegliere tooconfigure **lo spazio degli indirizzi** o **numero massimo VM** per la rete.
    * È possibile lasciare hello **server DNS** impostando come **Nessuno** per ora. È possibile aggiornare l'impostazione di hello dopo aver abilitato Servizi di dominio di Azure Active Directory.
7. In hello **percorso** elenco a discesa selezionare una regione di Azure supportata.  
    tooascertain hello aree di Azure in cui sono disponibili servizi di dominio di Azure Active Directory, vedere [servizi di Azure dall'area](https://azure.microsoft.com/regions/#services/).
8. toocreate la rete virtuale, fare clic su **creare una rete virtuale**.

    ![Creare una rete virtuale per Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. Dopo aver creato una rete virtuale, selezionare il nome di rete virtuale hello hello e quindi fare clic su hello **configura** scheda.

    ![Creare una subnet](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. In **spazi di indirizzi della rete virtuale**, fare clic su **aggiungere subnet**, quindi specificare una subnet con nome hello **AaddsSubnet**.

    ![Creare una subnet per Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate hello subnet, fare clic su **salvare**.


## <a name="next-step"></a>Passaggio successivo
[Attività 3: Abilitare Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
