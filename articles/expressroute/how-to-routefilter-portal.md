---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: Portale | Microsoft Docs'
description: In questo articolo viene descritto come tooconfigure i filtri di route per l'utilizzo di Peering Microsoft hello portale di Azure
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Configurare i filtri di route per il peering Microsoft

I filtri di route sono tooconsume un modo un sottoinsieme di servizi supportati tramite il peering Microsoft. Hello passaggi in questo articolo consentono configurare e gestire i filtri di route per i circuiti ExpressRoute.

Dynamics 365 servizi e i servizi di Office 365, ad esempio Exchange Online, SharePoint Online e Skype for Business, sono accessibili tramite il peering Microsoft hello. Quando Microsoft peering è configurato in un circuito ExpressRoute, tutti i servizi correlati toothese prefissi sono annunciati tramite sessioni BGP hello stabilite. Un valore di community BGP è collegato tooevery prefisso tooidentify hello servizio verrà offerti attraverso prefisso hello. Per un elenco di valori di community hello BGP e i servizi di hello viene eseguito il mapping, vedere [community BGP](expressroute-routing.md#bgp).

Se si richiedono servizi di integrazione applicativa tooall, un numero elevato di prefissi venga pubblicato tramite BGP. Ciò aumenta significativamente il dimensioni hello hello di tabelle di route gestita da router all'interno della rete. Se si prevede solo un sottoinsieme di servizi offerti tramite il peering Microsoft tooconsume, è possibile ridurre le dimensioni di hello delle tabelle di route in due modi. È possibile:

- Escludere i prefissi indesiderati applicando filtri di route alle community BGP. Si tratta di una procedura di rete standard usata comunemente in molte reti.

- Definire i filtri di route e applicarli circuito ExpressRoute tooyour. Un filtro di route è una nuova risorsa, che consente di selezionare l'elenco di hello dei servizi è pianificare tooconsume tramite il peering Microsoft. Router di ExpressRoute inviare solo elenco hello di prefissi che appartengono a servizi toohello individuati nel filtro di route hello.

### <a name="about"></a>Informazioni sui filtri di route

Quando Microsoft peering è configurato il circuito ExpressRoute, router perimetrali dei Microsoft hello stabilisce una coppia di sessioni BGP con il router perimetrali hello (il proprio o il provider di connettività). Nessuna route sono rete tooyour annunciato. rete di tooyour gli annunci di route tooenable, è necessario associare un filtro di route.

Un filtro di route consente di identificare i servizi desiderati tooconsume tramite il peering Microsoft del circuito di ExpressRoute. È essenzialmente un elenco vuoto di tutti i valori della community di hello BGP. Una volta una risorsa di filtro di route è definita e collegata tooan circuito ExpressRoute, tutti i prefissi che mappa i valori della community BGP toohello sono rete tooyour annunciato.

filtri di route in grado di tooattach toobe con servizi di Office 365 su di essi, è necessario disporre di servizi di Office 365 tooconsume autorizzazione tramite ExpressRoute. Se non si è autorizzati tooconsume Office 365 services tramite ExpressRoute, filtri di route tooattach hello operazione ha esito negativo. Per ulteriori informazioni sul processo di autorizzazione hello, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Servizi di integrazione applicativa tooDynamics 365 non richiede alcuna autorizzazione precedente.

> [!IMPORTANT]
> Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite Microsoft peering, anche se non sono definiti i filtri di route. Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.
> 
> 

### <a name="workflow"></a>Flusso di lavoro

toobe toosuccessfully in grado di connettersi tooservices tramite il peering Microsoft, è necessario completare hello seguendo i passaggi di configurazione:

- È necessario avere un circuito ExpressRoute attivo, per cui è stato effettuato il provisioning del peering Microsoft. È possibile utilizzare hello seguendo le istruzioni tooaccomplish queste attività:
  - [Creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.
  - [Creare il peering Microsoft](expressroute-howto-routing-portal-resource-manager.md) se si Gestione sessione BGP di hello direttamente. In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.

-  È necessario creare e configurare un filtro di route.
    - Identificare hello è servizi con tooconsume tramite il peering Microsoft
    - Identificare hello elenco di valori di community BGP associati ai servizi hello
    - Creare un regola tooallow hello prefisso elenco corrispondente hello valori community BGP

-  È necessario collegare il circuito ExpressRoute toohello di hello route filtro.

## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare la configurazione, assicurarsi che siano soddisfatti hello seguenti criteri:

 - Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

 - È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.

 - È necessario disporre di un peering Microsoft attivo. Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-howto-routing-portal-resource-manager.md).


## <a name="prefixes"></a>Passaggio 1. Ottenere un elenco di prefissi e di valori di community BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Ottenere un elenco dei valori di community BGP

I valori della community BGP associati a servizi accessibili tramite il peering Microsoft è disponibile in hello [requisiti di routing ExpressRoute](expressroute-routing.md) pagina.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Creare un elenco di valori hello che si desidera toouse

Creare un elenco dei valori di community BGP da toouse nel filtro di route hello. Ad esempio, il valore di community BGP per servizi di Dynamics 365 hello è 12076:5040.

## <a name="filter"></a>Passaggio 2. Creare un filtro di route e una regola di filtro

Un filtro di route può avere solo una regola e hello regola deve essere di tipo 'Consenti'. A questa regola può essere associato un elenco di valori di community BGP.

### <a name="1-create-a-route-filter"></a>1. Creare un filtro di route
È possibile creare un filtro di route selezionando hello opzione toocreate una nuova risorsa. Fare clic su **New** > **rete** > **RouteFilter**, come illustrato nella seguente immagine hello:

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

È necessario inserire il filtro di route hello in un gruppo di risorse. 

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Creare una regola di filtro

È possibile aggiungere e gestire di regole di aggiornamento selezionando hello scheda regola per il filtro di route.

![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


È possibile selezionare hello servizi desiderati tooconnect toofrom hello nell'elenco a discesa e salvare la regola di hello al termine.

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Passaggio 3. Collegare il circuito ExpressRoute hello route filtro tooan

È possibile collegare tooa circuito di hello route filtro selezionando pulsante "Aggiungi circuito" hello e selezionando il circuito ExpressRoute hello hello nell'elenco a discesa.

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>proprietà hello tooget di un filtro di route

Quando si apre risorse hello nel portale di hello, è possibile visualizzare le proprietà di un filtro di route.

![Creare un filtro di route](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>proprietà hello tooupdate di un filtro di route

È possibile aggiornare l'elenco di hello del circuito BGP community valori collegati tooa selezionando pulsante hello "Gestisci"regola.


![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach un filtro di route da un circuito ExpressRoute

toodetach un circuito dal filtro di route hello, fare clic con il pulsante destro sul circuito hello e fare clic su "dissociare".

![Creare un filtro di route](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete un filtro di route

È possibile eliminare un filtro di route selezionando pulsante Elimina hello. 

![Creare un filtro di route](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
