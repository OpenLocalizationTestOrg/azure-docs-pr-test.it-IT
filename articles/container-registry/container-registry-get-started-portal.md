---
title: aaaCreate privata Docker Registro di sistema - portale di Azure | Documenti Microsoft
description: Iniziare a creare e gestire i registri contenitore Docker privati con hello portale di Azure
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Creare un registro di sistema contenitore Docker privata mediante hello portale di Azure
Utilizzare hello toocreate portale Azure del Registro di sistema un contenitore e gestire le relative impostazioni. È anche possibile creare e gestire i registri di contenitore usando hello [comandi CLI di Azure 2.0](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).

Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Creare un registro di contenitori
1. In hello [portale di Azure](https://portal.azure.com), fare clic su **+ nuovo**.
2. Marketplace hello ricerca per **Registro di sistema di contenitore di Azure**.
3. Selezionare **Registro contenitori di Azure** pubblicato da **Microsoft**.
    ![Servizio Registro contenitori in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Fare clic su **Crea**. Hello **Registro di sistema di Azure contenitore** pannello viene visualizzato.

    ![Impostazioni di Registro contenitori](./media/container-registry-get-started-portal/container-registry-settings.png)
5. In hello **Registro di sistema di Azure contenitore** pannello, immettere le seguenti informazioni hello. Al termine dell'operazione fare clic su **Crea**.

    a. **Registry name** (Nome registro): nome di dominio di primo livello univoco globale per il registro. In questo esempio, nome del Registro di sistema hello è *myRegistry01*, ma sostituire un nome univoco del proprio. Hello nome può contenere solo lettere e numeri.

    b. **Gruppo di risorse**: selezionare un oggetto esistente [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo.

    c. **Percorso**: selezionare un Data Center di Azure posizione servizio hello [disponibile](https://azure.microsoft.com/regions/services/), ad esempio **centro-meridionali**.

    d. **L'utente amministratore**: se si desidera, attivare del Registro di sistema hello tooaccess utente amministratore. È possibile modificare questa impostazione dopo la creazione del Registro di sistema di hello.

      > [!IMPORTANT]
      > Inoltre l'accesso a tooproviding tramite un account utente di amministratore, i registri di contenitore supportano l'autenticazione supportato da entità di servizio di Azure Active Directory. Per altre informazioni e considerazioni, vedere [Authenticate with the container registry](container-registry-authentication.md) (Eseguire l'autenticazione al registro contenitori).
      >

    e. **Account di archiviazione**: utilizzare hello predefinito impostazione toocreate un [account di archiviazione](../storage/common/storage-introduction.md), oppure selezionare un account di archiviazione esistente nell'hello nello stesso percorso. Archiviazione Premium non è attualmente supportata.

## <a name="manage-registry-settings"></a>Gestire le impostazioni del registro
Dopo la creazione del Registro di sistema di hello, trovare hello le impostazioni del Registro di sistema iniziando dalla hello **contenitore registri** pannello nel portale di hello. Ad esempio, potrebbe essere necessario hello impostazioni toolog nel Registro di sistema tooyour o si potrebbe desidera tooenable o disabilitare l'utente amministratore hello.

1. In hello **contenitore registri** pannello, fare clic sul nome di hello del Registro di sistema.

    ![Pannello Container Registries (Registri dei contenitori)](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Fare clic su impostazioni di accesso toomanage, **tasto**.

    ![Accesso al registro contenitori](./media/container-registry-get-started-portal/container-registry-access.png)
3. Si noti hello seguenti impostazioni:

   * **Server di accesso** -nome completo di hello è utilizzare toolog toohello del Registro di sistema. In questo esempio si tratta di `myregistry01.azurecr.io`.
   * **L'utente amministratore** - tooenable di attivare o disattivare o disabilitare l'account amministratore del Registro di sistema di hello.
   * **Nome utente** e **Password** -hello credenziali dell'account utente di amministrazione hello (se abilitati) è possibile utilizzare toolog toohello del Registro di sistema. È facoltativamente possibile rigenerare le password hello. Le due password vengono create in modo che sia possibile gestire Registro di sistema toohello connessioni con una password, mentre si rigenera hello altre password. tooauthenticate con un'entità servizio, vedere [eseguire l'autenticazione con un registro di sistema di contenitore Docker privata](container-registry-authentication.md).

## <a name="next-steps"></a>Passaggi successivi
* [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
