---
title: 'Collegare un circuito ExpressRoute di tooan rete virtuale: PowerShell: classico: Azure | Documenti Microsoft'
description: "Questo documento viene fornita una panoramica della modalità virtuale toolink reti circuiti tooExpressRoute (Vnet) utilizzando il modello di distribuzione classica hello e PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Connettersi a un circuito ExpressRoute tooan di rete virtuale con PowerShell (versione classica)
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-linkvnet-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-linkvnet-classic.md)
>

In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure utilizzando il modello di distribuzione classica hello e PowerShell. Reti virtuali possono essere nella stessa sottoscrizione hello o possono far parte di un'altra sottoscrizione.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Prerequisiti di configurazione
1. È necessario più recente dei moduli di Azure PowerShell hello hello. È possibile scaricare i moduli di PowerShell più recenti hello dalla sezione PowerShell di hello hello [pagina di download di Azure](https://azure.microsoft.com/downloads/). Seguire le istruzioni hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per istruzioni dettagliate su come tooconfigure i moduli di Azure PowerShell hello toouse computer.
2. È necessario hello tooreview [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
3. È necessario avere un circuito ExpressRoute attivo.
   * Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e il provider di connettività abilitare circuito hello.
   * Assicurarsi di disporre del peering privato di Azure configurato per il circuito. Vedere hello [Configura routing](expressroute-howto-routing-classic.md) articolo per le istruzioni di routing.
   * Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.
   * È necessario disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo. Seguire le istruzioni di hello troppo[configurare una rete virtuale per ExpressRoute](expressroute-howto-vnet-portal-classic.md).

È possibile collegare le reti virtuali di too10 tooan circuito ExpressRoute. Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica. È possibile collegare un maggior numero di reti virtuali tooyour circuito ExpressRoute o collegamento di reti virtuali in altre aree di natura geopolitiche se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium. Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connettere una rete virtuale in hello circuito tooa sottoscrizione
È possibile collegare un circuito ExpressRoute di tooan rete virtuale tramite hello cmdlet seguente. Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il cmdlet hello.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connettere una rete virtuale in un circuito tooa sottoscrizione diversa
È possibile condividere un circuito ExpressRoute tra più sottoscrizioni. Hello nella figura seguente illustra un semplice schema di funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.

Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione. Per distribuire i servizi, ma reparti hello possono condividere una singola ExpressRoute circuito tooconnect tooyour indietro locale rete, ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione. Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello. Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.

> [!NOTE]
> Gli addebiti di connettività e larghezza di banda per il circuito dedicato hello sarà proprietario del circuito ExpressRoute toohello applicato. Tutte le reti virtuali condividono hello stessa larghezza di banda.
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Amministrazione
Hello *proprietario del circuito* è hello amministratore/coadministrator di sottoscrizione hello in cui hello ExpressRoute viene creato il circuito. Hello proprietario del circuito può autorizzare gli amministratori/coadministrators di altre sottoscrizioni, cui viene fatto riferimento tooas *circuit utenti*, hello toouse dedicato circuito a cui sono proprietari. Gli utenti del circuito che sono autorizzati toouse hello del ExpressRoute circuito possono collegano la rete virtuale di hello nella loro toohello sottoscrizione circuito ExpressRoute dopo che sono autorizzati.

proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento. Revoca l'autorizzazione comporterà tutti i collegamenti viene eliminati dalla sottoscrizione hello il cui accesso è stato revocato.

### <a name="circuit-owner-operations"></a>Operazioni del proprietario del circuito

**Creazione di un'autorizzazione**

proprietario del circuito Hello autorizza gli amministratori di hello di altre sottoscrizioni hello toouse specificato circuito. Nell'esempio seguente di hello, messaggio per l'amministratore del circuito hello (Contoso IT) consente di messaggio per l'amministratore di un'altra sottoscrizione (Dev-Test) toolink backup circuito di toohello tootwo reti virtuali. messaggio per l'amministratore IT di Contoso ha abilitato specificando l'ID del Test di sviluppo Microsoft hello. cmdlet di Hello non invia posta elettronica toohello specificato ID Microsoft. proprietario del circuito Hello deve tooexplicitly notificare hello di altri proprietario della sottoscrizione che hello autorizzazione è stato completato.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Verifica delle autorizzazioni**

proprietario del circuito Hello è possibile esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello seguente cmdlet:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Aggiornamento delle autorizzazioni**

proprietario del circuito Hello è possibile modificare le autorizzazioni utilizzando hello seguente cmdlet:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Eliminazione delle autorizzazioni**

proprietario del circuito Hello può revocare/eliminazione utente toohello autorizzazioni eseguendo hello seguente cmdlet:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Operazioni dell'utente del circuito

**Verifica delle autorizzazioni**

utente del circuito Hello è possibile esaminare le autorizzazioni utilizzando hello seguente cmdlet:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Riscatto delle autorizzazioni dei collegamenti**

utente del circuito Hello è possibile eseguire il seguente cmdlet tooredeem hello un'autorizzazione del collegamento:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Eseguire questo comando nella sottoscrizione hello appena collegato per la rete virtuale hello:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).

