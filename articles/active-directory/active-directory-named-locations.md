---
title: percorsi aaaNamed in Azure Active Directory | Documenti Microsoft
description: "Configurando denominato percorsi, è possibile evitare IP indirizzi che appartengono a organizzazione generano falsi positivi per il tipo di evento di rischio di hello impossibili tooatypical corsa."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Località denominate in Azure Active Directory

Con hello denominato percorsi funzionalità di Azure Active Directory, è possibile etichettare gli intervalli di indirizzi IP attendibili nell'organizzazione. Nell'ambiente in uso, è possibile utilizzare posizioni denominate contesto hello di rilevamento hello di [gli eventi di rischio](active-directory-reporting-risk-events.md). funzionalità Hello consente di ridurre il numero di hello di segnalati falsi positivi per hello *percorsi di comunicazione Impossibile tooatypical* il tipo di evento di rischio. 

## <a name="configuration"></a>Configurazione

posizione denominata tooconfigure:

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore globale.

2. Nel riquadro di sinistra hello, fare clic su **Azure Active Directory**.

    ![collegamento di Azure Active Directory Hello nel riquadro di sinistra hello](./media/active-directory-named-locations/01.png)

3. In hello **Azure Active Directory** pannello in hello **sicurezza** fare clic su **accesso condizionale**.

    ![il comando di accesso condizionale Hello](./media/active-directory-named-locations/05.png)


4. In hello **accesso condizionale** pannello in hello **Gestisci** fare clic su **posizioni denominate**.

    ![comando percorsi denominato Hello](./media/active-directory-named-locations/06.png)


5. In hello **denominato percorsi** pannello, fare clic su **nuova posizione**.

    ![Hello nuovo comando di percorso](./media/active-directory-named-locations/07.png)


6. In hello **New** pannello hello seguenti:

    ![Nuovo pannello Hello](./media/active-directory-named-locations/08.png)

    a. In hello **nome** , digitare un nome per il percorso denominato.

    b. In hello **intervalli IP** , digitare un intervallo di IP. intervallo IP Hello deve toobe in hello *Classless Interdomain Routing* formato (CIDR).  

    c. Fare clic su **Crea**.



## <a name="what-you-should-know"></a>Informazioni utili

**Aggiornamenti bulk**: quando si crea o Aggiorna ubicazioni denominate, per gli aggiornamenti bulk, è possibile caricare o scaricare un file CSV con intervalli IP hello. Un'operazione di caricamento consente di aggiungere intervalli IP hello nell'elenco di toohello hello file anziché sovrascrivere l'elenco di hello.

![Hello caricare e scaricare i collegamenti](./media/active-directory-named-locations/09.png)


**Limitazioni**: È possibile definire un massimo di 60 posizioni denominate, con tooeach di intervallo assegnato IP uno di essi. Se si dispone di una sola posizione denominata configurata, è possibile definire degli intervalli IP too500 appositamente.


## <a name="next-steps"></a>Passaggi successivi

toolearn più sugli eventi di rischio, vedere [gli eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).

