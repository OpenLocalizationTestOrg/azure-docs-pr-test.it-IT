---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: PowerShell | Microsoft Docs'
description: In questo articolo viene descritto come i filtri di route tooconfigure per il Peering Microsoft tramite PowerShell
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
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
  - [Creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.
  - [Creare il peering Microsoft](expressroute-circuit-peerings.md) se si Gestione sessione BGP di hello direttamente. In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.

-  È necessario creare e configurare un filtro di route.
    - Identificare hello è servizi con tooconsume tramite il peering Microsoft
    - Identificare hello elenco di valori di community BGP associati ai servizi hello
    - Creare un regola tooallow hello prefisso elenco corrispondente hello valori community BGP

-  È necessario collegare il circuito ExpressRoute toohello di hello route filtro.

## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare la configurazione, assicurarsi che siano soddisfatti hello seguenti criteri:

 - Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).

  > [!NOTE]
  > Scaricare la versione più recente di hello da hello PowerShell Gallery, anziché utilizzare hello programma di installazione. Hello Installer attualmente non supporta i cmdlet di hello necessario.
  > 

 - Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.

 - È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.

 - È necessario disporre di un peering Microsoft attivo. Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-circuit-peerings.md).

### <a name="log-in-tooyour-azure-account"></a>Accedi tooyour account Azure

Prima di iniziare questa configurazione, è necessario accedere tooyour account Azure. cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure. Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.

Aprire la console di PowerShell con privilegi elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
```

Se si dispone di più sottoscrizioni di Azure, controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

Specificare una sottoscrizione di hello che si desidera toouse.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>Passaggio 1. Ottenere un elenco di prefissi e di valori di community BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Ottenere un elenco dei valori di community BGP

Utilizzare hello dopo cmdlet tooget hello elenco dei valori di community BGP associati servizi accessibili tramite il peering Microsoft e hello elenco di prefissi associati:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Creare un elenco di valori hello che si desidera toouse

Creare un elenco dei valori di community BGP da toouse nel filtro di route hello. Ad esempio, il valore di community BGP per servizi di Dynamics 365 hello è 12076:5040.

## <a name="filter"></a>Passaggio 2. Creare un filtro di route e una regola di filtro

Un filtro di route può avere solo una regola e hello regola deve essere di tipo 'Consenti'. A questa regola può essere associato un elenco di valori di community BGP.

### <a name="1-create-a-route-filter"></a>1. Creare un filtro di route

Creare innanzitutto il filtro di route hello. comando Hello 'New-AzureRmRouteFilter' Crea solo una risorsa di filtro di route. Dopo aver creato la risorsa hello, è necessario creare una regola e collegarlo oggetto filtro di route toohello. Eseguire hello successivo comando toocreate una risorsa di filtro delle route:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Creare una regola di filtro

È possibile specificare un insieme di Comunità BGP come un elenco delimitato da virgole, come illustrato nell'esempio hello. Eseguire una nuova regola di hello successivo comando toocreate:
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Aggiungere filtri di route hello regola toohello

Eseguire hello comando tooadd hello regola toohello route filtro seguente:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>Passaggio 3. Collegare il circuito ExpressRoute hello route filtro tooan

Eseguire hello comando tooattach hello route filtro toohello circuito ExpressRoute, presupponendo che si dispone solo di peering Microsoft seguenti:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>proprietà hello tooget di un filtro di route

proprietà hello tooget di un filtro di route, usare hello alla procedura seguente:

1. Risorsa di filtro route hello tooget comando che segue di hello esecuzione:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Ottenere le regole di filtro di hello route per la risorsa di filtro di route hello eseguendo hello comando seguente:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>proprietà hello tooupdate di un filtro di route

Se è già collegato il filtro di route hello tooa circuito, elenco di aggiornamenti toohello BGP community propaga automaticamente le modifiche di annuncio prefisso appropriato tramite sessioni BGP hello stabilita. È possibile aggiornare l'elenco di community hello BGP del filtro route utilizzando hello comando seguente:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach un filtro di route da un circuito ExpressRoute

Dopo essere stato disconnesso da hello circuito ExpressRoute, un filtro di route non prefissi sono annunciati tramite sessione BGP hello. È possibile scollegare un filtro di route da un circuito ExpressRoute tramite hello comando seguente:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>toodelete un filtro di route

È possibile solo eliminare un filtro di route, se non è collegato tooany circuito. Verificare che il filtro route hello non è collegato il circuito tooany prima di tentare di toodelete è. È possibile eliminare un filtro di route utilizzando hello comando seguente:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
