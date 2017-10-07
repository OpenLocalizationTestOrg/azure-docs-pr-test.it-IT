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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)


## <a name="task-3-configure-administrative-group"></a>Attività 3: Configurare un gruppo amministrativo
In questa attività di configurazione si crea un gruppo amministrativo nella directory di Azure AD. Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*. Membri di questo gruppo vengono concesse le autorizzazioni amministrative nei computer di dominio gestiti toohello appartenenti a un dominio. In computer appartenenti a un dominio, questo gruppo viene aggiunto il gruppo di amministratori toohello. Inoltre, i membri di questo gruppo è possono utilizzare Desktop remoto tooconnect in modalità remota toodomain computer appartenenti a un.

> [!NOTE]
> Non si dispone delle autorizzazioni di amministratore dell'organizzazione o di amministratore di dominio nel dominio gestito hello creato tramite Azure Active Directory Domain Services. Nei domini gestiti, queste autorizzazioni sono riservate dal servizio hello e non vengono resi disponibili toousers nel tenant di hello. Tuttavia, è possibile utilizzare gruppo amministrativo di hello speciale creato in questa tooperform di attività di configurazione alcune operazioni privilegiate. Tali operazioni includono l'aggiunta a dominio toohello computer appartenenti toohello gruppo di amministrazione nei computer appartenenti a un dominio e la configurazione dei criteri di gruppo.
>

procedura guidata di Hello crea automaticamente il gruppo amministrativo di hello nella directory di Azure AD. Il gruppo viene chiamato "Amministratori di AAD DC". Se si dispone di un gruppo esistente con lo stesso nome nella directory di Azure AD, la procedura guidata hello seleziona questo gruppo. È possibile configurare l'appartenenza al gruppo usando hello **gruppo amministratore** pagina della procedura guidata.

1. l'appartenenza al gruppo tooconfigure, fare clic su **gli amministratori di controller di dominio di AAD**.

    ![Configurare l'appartenenza al gruppo](./media/getting-started/domain-services-blade-admingroup.png)

2. Fare clic su hello **aggiungere membri** pulsante tooadd gli utenti del gruppo dell'amministratore toohello directory Azure AD.

3. Al termine, fare clic su **OK** toomove su toohello **riepilogo** pagina della procedura guidata hello.

4. In hello **riepilogo** pagina della procedura guidata hello, rivedere le impostazioni di configurazione di hello per il dominio gestito hello. È possibile tornare tooany passaggio delle modifiche di toomake hello procedura guidata, se necessario. Al termine, fare clic su **OK** toocreate hello gestiti nuovo dominio.

    ![Riepilogo](./media/getting-started/domain-services-blade-summary.png)

5. Viene visualizzata una notifica che mostra lo stato di avanzamento hello della distribuzione di servizi di dominio Active Directory di Azure. Fare clic su notifica hello toosee dettagliate per la distribuzione di hello lo stato di avanzamento.

    ![Notifica - Distribuzione in corso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Effettuare il provisioning del dominio gestito
Hello processo di provisioning del dominio gestito può richiedere tooan ora.

1. Durante la distribuzione è in corso, è possibile cercare "servizi di dominio' in hello **individuare risorse** casella di ricerca. Selezionare **servizi di dominio Active Directory di Azure** dai risultati di ricerca hello. Hello **servizi di dominio Active Directory di Azure** pannello elenca hello un dominio gestito che viene eseguito il provisioning.

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Fare clic su nome hello di hello gestito dominio (ad esempio, ' contoso100.com') toosee ulteriori dettagli su dominio hello.

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. Hello **Panoramica** scheda Mostra il dominio hello è attualmente in corso il provisioning. È possibile configurare dominio gestito hello fino a quando non è completamente disponibile. Potrebbe richiedere fino a ora tooan per toobe il dominio gestito eseguito il provisioning completo.

    ![Servizi di dominio - scheda Panoramica durante hello lo stato di provisioning ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Quando è stato effettuato il provisioning dominio gestito hello, hello **Panoramica** scheda Mostra stato dominio hello come **esecuzione**.

    ![Domain Services - Scheda Panoramica al termine del provisioning](./media/getting-started/domain-services-provisioned.png)

5. In hello **proprietà** scheda, viene visualizzato due indirizzi IP del dominio sono disponibili per la rete virtuale hello controller.

    ![Domain Services - Scheda Proprietà al termine del provisioning](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Passaggio successivo
[Attività 4: aggiornare le impostazioni DNS di hello per hello rete virtuale di Azure](active-directory-ds-getting-started-dns.md)
