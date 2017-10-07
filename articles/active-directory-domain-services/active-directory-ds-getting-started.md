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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)
Questo articolo illustra come tooenable Azure Active Directory servizi di dominio (Azure AD DS) tramite hello portale di Azure.


hello toolaunch **servizi di dominio Active Directory di Azure attiva** hello procedura guidata, completo alla procedura seguente:

1. Passare toohello [portale di Azure](https://portal.azure.com).
2. Nel riquadro di sinistra hello, fare clic su **New**.
3. In hello **New** blade, tipo **servizi di dominio** nella barra di ricerca hello.

    ![Ricerca di Domain Services](./media/getting-started/search-domain-services.png)

4. Fare clic su tooselect **servizi di dominio Active Directory di Azure** elenco hello dei suggerimenti di ricerca. In hello **servizi di dominio Active Directory di Azure** pannello, fare clic su hello **crea** pulsante.

    ![Pannello Domain Services](./media/getting-started/domain-services-blade.png)

5. Hello **servizi di dominio Active Directory di Azure attiva** procedura guidata viene avviata.


## <a name="task-1-configure-basic-settings"></a>Attività 1: Configurare le impostazioni di base
In hello **nozioni di base** pagina della procedura guidata hello, è possibile specificare nome di dominio DNS hello per il dominio gestito hello. È anche possibile scegliere il gruppo di risorse hello e dominio gestito di Azure percorso toowhich hello deve essere distribuito.

![Configurare le informazioni di base](./media/getting-started/domain-services-blade-basics.png)

1. Scegliere hello **nome di dominio DNS** per il dominio gestito.

   * nome di dominio Hello predefinito della directory hello (con un **. c o m** suffisso) viene specificato per impostazione predefinita.

   * È anche possibile immettere un nome di dominio personalizzato. In questo esempio, è il nome di dominio personalizzato hello *contoso100.com*.

     > [!WARNING]
     > prefisso Hello del nome del dominio specificato (ad esempio, *contoso100* in hello *contoso100.com* nome di dominio) deve contenere meno di 15 caratteri. Non è possibile creare un dominio gestito con un prefisso più lungo di 15 caratteri.
     >
     >

2. Verificare il nome di dominio DNS hello che scelto per hello gestito dominio non esiste già nella rete virtuale hello. In particolare, verificare se:

   * Si dispone già di un dominio con hello stesso nome di dominio DNS nella rete virtuale hello.

   * rete virtuale di Hello in cui si prevede di dominio gestiti di hello tooenable stabilita una connessione VPN alla rete locale. In questo scenario, verificare che non si dispone di un dominio con hello stesso nome di dominio DNS nella rete locale.

   * È un servizio cloud esistente con lo stesso nome nella rete virtuale hello.

3. Scegliere hello **tipo di rete virtuale**. Per impostazione predefinita, hello **Gestione risorse** viene selezionato il tipo di rete virtuale. È consigliabile usare questo tipo di rete virtuale per tutti i nuovi domini gestiti creati.

4. Seleziona hello Azure **sottoscrizione** nel quale si desidera toocreate hello gestito dominio.

5. Seleziona hello **gruppo di risorse** toowhich hello gestito dominio deve appartenere. È possibile scegliere entrambi hello **Crea nuovo** o **utilizzare esistente** gruppo di risorse hello tooselect opzioni.

6. Scegliere hello Azure **percorso** in cui hello deve essere creato un dominio gestito. In hello **rete** pagina della procedura guidata hello, vedrai le reti virtuali solo appartenenti toohello percorso selezionato.

7. Al termine, fare clic su **OK** toomove su toohello **rete** pagina della procedura guidata hello.


## <a name="next-step"></a>Passaggio successivo
[Attività 2: Configurare le impostazioni di rete](active-directory-ds-getting-started-network.md)
