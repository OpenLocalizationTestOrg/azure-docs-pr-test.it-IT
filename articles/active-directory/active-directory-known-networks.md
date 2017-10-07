---
title: Reti aaaKnown nel portale di Azure classico hello | Documenti Microsoft
description: "Quando si configurano reti note, è possibile evitare gli indirizzi IP che sono di proprietà dell'organizzazione incluso in hello accessi da più aree geografiche e accessi da indirizzi IP con attività sospetta report."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Reti note

> [!div class="op_single_selector"]
> * [Portale di Azure classico](active-directory-known-networks.md)
> * [Portale di Azure](active-directory-known-networks-azure-portal.md)
> 
> 


È possibile utilizzare l'accesso di Azure Active Directory e utilizzo report toogain visibilità hello integrità e sicurezza della directory dell'organizzazione. Con queste informazioni, un amministratore di directory possa meglio stabilire l'origine di possibili rischi per la sicurezza in modo da poter adeguatamente pianificare toomitigate tali rischi.

È possibile che hello "*accessi da più aree geografiche*"e"*accessi da indirizzi IP con attività sospetta*" report flag in modo errato gli indirizzi IP che sono effettivamente di proprietà del organizzazione. 

Questo può avvenire, ad esempio, nei casi seguenti: 

* Un utente nel proprio ufficio Boston ha effettuato l'accesso in modalità remota tooyour centro dati San Francisco trigger hello report "Accessi da più aree geografiche" 
* Un utente dell'organizzazione tenta toosign su più volte con un hello trigger password non corretta per il report "Accessi da indirizzi IP con attività sospetta" 

tooprevent questi casi protezione fuorviante la generazione del report, è consigliabile aggiungere note intervalli toohello elenco di indirizzi IP dell'indirizzo IP pubblico dell'organizzazione.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>gli intervalli di tooadd indirizzo IP pubblico dell'organizzazione, eseguire hello alla procedura seguente:

1. Sign-on toohello [portale di gestione di Azure](https://manage.windowsazure.com).

2. Nel riquadro di sinistra hello, fare clic su **Active Directory**. 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-01.png)

3. In hello **Directory** scheda, selezionare la directory.

4. Scegliere dal menu hello in primo piano hello **configura**. 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-02.png)

5. Nella scheda Configura hello, andare troppo**gli intervalli di indirizzi IP pubblici organizzazioni** 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-03.png)

6. Fare clic su **Aggiungi intervalli di indirizzi IP noti**.

7. Aggiungere gli intervalli di indirizzi nella finestra di dialogo hello visualizzata e quindi fare clic su pulsante di controllo hello al termine. 

    ![Reti note](./media/active-directory-known-networks/known-netwoks-04.png)

**Risorse aggiuntive:**

* [Visualizzare i report di accesso e utilizzo](active-directory-view-access-usage-reports.md)
* [Accessi da indirizzi IP con attività sospetta](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Accessi da più aree geografiche](active-directory-reporting-sign-ins-from-multiple-geographies.md)

