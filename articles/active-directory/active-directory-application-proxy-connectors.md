---
title: connettori Proxy di Azure AD App del portale aaaClassic | Documenti Microsoft
description: Include informazioni su come toocreate e gestire gruppi di connettori Proxy di applicazione di Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Pubblicare applicazioni in reti e posizioni separate tramite i gruppi di connettori
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portale di Azure classico](active-directory-application-proxy-connectors.md)
>
>

I gruppi di connettori sono utili in varie situazioni, ad esempio:

* Siti con più data center interconnessi. In questo caso, si desidera tookeep come quantità di traffico in Data Center di hello possibile poiché i collegamenti tra Data Center sono lente e costoso. È possibile distribuire i connettori in ogni Data Center tooserve solo hello le applicazioni che risiedono all'interno di hello datacenter. Questo approccio riduce al minimo i collegamenti tra Data Center e offre un'esperienza completamente trasparente agli utenti di tooyour.
* La gestione delle applicazioni installate in reti isolate che non fanno parte della rete aziendale principale hello. È possibile utilizzare i connettori di connettore gruppi tooinstall dedicato nella rete di toohello reti isolate tooalso isolare le applicazioni.
* Per le applicazioni installate in IaaS per l'accesso cloud, i gruppi di connettori forniscono un servizio toosecure hello accesso tooall hello le applicazioni comuni. Gruppi di connettori non creare una dipendenza aggiuntiva nella rete aziendale, o frammento esperienza app hello. I connettori possono essere installati in ogni data center nel cloud e gestire solo le applicazioni che si trovano nella rete. È possibile installare i diversi connettori tooachieve la disponibilità elevata.
* Supporto per gli ambienti con più foreste in cui i connettori specifici possono essere distribuiti per ogni foresta e impostare tooserve specifiche applicazioni.
* Connettore gruppi possono essere utilizzati nei siti di ripristino di emergenza tooeither rileva il failover o come backup per hello principale sito.
* Gruppi di connettori possono inoltre essere utilizzati tooserve più società da un singolo tenant.

## <a name="prerequisite-create-your-connectors"></a>Prerequisito: creare i connettori
toogroup i connettori, [installare più connettori](active-directory-application-proxy-enable.md), quindi assegnare un nome e li raggruppa. Infine è tooassign li toospecific app.

## <a name="step-1-create-connector-groups"></a>Passaggio 1: Creare gruppi di connettori
È possibile creare tutti i gruppi di connettori desiderati. Mediante la creazione del connettore gruppo hello portale di Azure classico.

1. Selezionare la directory e fare clic su **Configura**.  
    ![Schermata di configurazione del proxy dell'applicazione: fare clic su Gestisci gruppi di connettori](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. Proxy dell'applicazione, selezionare **gestire gruppi di connettori** e creare un gruppo di connettori, assegnando un nome di gruppo hello.  
    ![Screenshot dei gruppi del connettore del proxy dell'applicazione: assegnare un nome al gruppo](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Passaggio 2: Assegnare connettori tooyour gruppi
Una volta creati i gruppi di connettori hello, Sposta gruppo appropriato di hello connettori toohello.

1. In **Proxy dell'applicazione** fare clic su **Gestisci connettori**.
2. In **gruppo**, selezionare il gruppo di hello desiderato per ogni connettore. Connettori hello backup too10 minuti toobecome potrebbe richiedere attivi nel nuovo gruppo di hello.  
    ![Screenshot dei connettori proxy dell'applicazione: selezionare il gruppo dal menu a discesa](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Passaggio 3: Assegnare gruppi di connettori tooyour le applicazioni
ultimo passaggio Hello è tooset ogni gruppo di connettori toohello applicazione che gestisce.

1. Nel portale di Azure classico, nella directory, hello selezionare hello applicazione che si desidera tooassign toohello gruppo e fare clic su **configura**.
2. In **gruppo connettore**, selezionare il gruppo di hello desiderato hello toouse applicazione. Questa modifica viene applicata immediatamente.  
    ![Screenshot dei gruppi del connettore proxy dell'applicazione: selezionare il gruppo dal menu a discesa](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Vedere anche
* [Abilitare il proxy dell'applicazione](active-directory-application-proxy-enable.md)
* [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
* [Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md)
* [Risolvere i problemi che si verificano con il proxy di applicazione](active-directory-application-proxy-troubleshoot.md)

Per informazioni più recenti hello e gli aggiornamenti, consultare hello [blog del Proxy dell'applicazione](http://blogs.technet.com/b/applicationproxyblog/)
