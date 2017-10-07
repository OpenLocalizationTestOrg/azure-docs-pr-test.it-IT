---
title: aaaHow toouse gestione API di Azure con le reti virtuali
description: Informazioni su come toosetup una connessione tooa virtuale in Gestione API di Azure e accesso web di servizi di rete attraverso di esso.
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Come toouse gestione API di Azure con le reti virtuali
Reti virtuali di Azure (Vnet) consentono di tooplace delle risorse di Azure in una rete routeable internet non è possibile controllare l'accesso a. Queste reti possono quindi essere reti locali connesse tooyour con varie tecnologie VPN. informazioni sulle reti virtuali di Azure dispone di informazioni hello qui toolearn: [Panoramica di rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).

Gestione API di Azure possono essere distribuiti all'interno di hello rete virtuale (VNET), in modo che possa accedere a servizi di back-end in rete hello. salve portale per sviluppatori e il gateway API, può essere accessibile da Internet hello o solo all'interno di rete virtuale hello toobe configurato.

> [!NOTE]
> Gestione API di Azure supporta le reti virtuali classiche e Azure Resource Manager.
>
>

## <a name="enable-vpn"></a>Attivare la connessione VNET
> [!NOTE]
> Connettività di rete virtuale è disponibile in hello **Premium** e **Developer** livelli. tooswitch tra i livelli di hello, aprire il servizio Gestione API in hello portale di Azure e quindi hello **scala e prezzi** scheda. In hello **tariffario** sezione, selezionare il livello di Premium o lo sviluppatore hello e fare clic su Salva.
>

connettività tra reti VIRTUALI tooenable, aprire il servizio Gestione API nel portale di Azure hello e hello **rete virtuale** pagina.

![Menu della rete virtuale di Gestione API][api-management-using-vnet-menu]

Selezionare il tipo di accesso di hello desiderato:

* **Esterno**: sono accessibili dal portale di gestione API hello gateway e developer hello pubblica internet tramite un servizio di bilanciamento del carico esterno. gateway Hello possono accedere alle risorse in rete virtuale hello.

![Peering pubblico][api-management-vnet-public]

* **Interno**: portale di gestione API hello gateway e developer sono accessibili solo dall'interno di rete virtuale di hello tramite un servizio di bilanciamento del carico interno. gateway Hello possono accedere alle risorse in rete virtuale hello.

![Peering privato][api-management-vnet-private]

Verrà ora visualizzato un elenco di tutte le aree in cui viene eseguito il provisioning del servizio Gestione API. Selezionare una VNET e una subnet per ogni area. Hello elenco viene popolato con classica e reti virtuali di gestione delle risorse disponibili nelle sottoscrizioni di Azure che sono il programma di installazione nell'area di hello che si sta configurando.

> [!NOTE]
> **Endpoint del servizio** in hello diagramma include Gateway o Proxy, portale di pubblicazione, portale per sviluppatori, GIT e hello diretto dell'Endpoint di gestione.
> **Gestione Endpoint** in hello diagramma è endpoint hello ospitato nella configurazione di toomanage hello servizio tramite il portale di Azure e Powershell.
> Inoltre, si noti che, anche se il diagramma hello Mostra gli indirizzi IP per gli endpoint diversi, il servizio Gestione API **solo** risponde alla relativa i nomi host configurato.

> [!IMPORTANT]
> Quando si distribuisce un tooa di istanza VNET Gestione risorse di gestione API di Azure, servizio di hello deve essere in una subnet dedicata che non contiene altre risorse, ad eccezione delle istanze di gestione API di Azure. Se viene effettuato un tentativo di toodeploy un tooa di istanza di gestione API di Azure subnet VNET Gestione risorse che contiene altre risorse, distribuzione hello avrà esito negativo.
>
>

![Selezionare una VPN][api-management-setup-vpn-select]

Fare clic su **salvare** in alto hello hello.

> [!NOTE]
> Hello indirizzo VIP dell'istanza di gestione API hello verrà modificato ogni volta rete virtuale è abilitato o disabilitato.  
> indirizzo VIP Hello viene modificata quando Gestione API viene spostato dalla **esterno** troppo**interno** o viceversa
>


> [!IMPORTANT]
> Se si rimuove gestione API da una rete virtuale o modifica hello uno che in cui viene distribuito, hello tra reti VIRTUALI usate in precedenza possono rimanere bloccati per le ore too4. Durante questo periodo verrà non hello toodelete possibili tra reti VIRTUALI o distribuire un nuovo tooit di risorse.

## <a name="enable-vnet-powershell"></a>Abilitare la connessione della rete virtuale usando i cmdlet di PowerShell
È inoltre possibile abilitare la connettività di rete virtuale utilizzando i cmdlet di PowerShell hello

* **Creare un servizio di gestione API all'interno di una rete virtuale**: utilizzare i cmdlet di hello [New AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate un servizio di gestione API di Azure all'interno di una rete virtuale.

* **Distribuire un servizio di gestione API esistente all'interno di una rete virtuale**: utilizzare i cmdlet di hello [aggiornamento AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove un servizio di gestione API di Azure esistente all'interno di una rete virtuale.

## <a name="connect-vnet"></a>Connettersi tooa del servizio web ospitato all'interno di una rete virtuale
Dopo aver connesso toohello rete virtuale del servizio Gestione API, l'accesso ai servizi back-end in esso contenuti è alcuna differenza rispetto all'accesso ai servizi pubblici. Digitare l'indirizzo IP locale hello o al nome di host di hello (se un server DNS è configurato per la rete virtuale hello) del servizio web in hello **URL servizio Web** campo quando si crea una nuova API o la modifica di uno esistente.

![Aggiungere un'API dalla VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"> </a>Problemi comuni di configurazione di rete
Di seguito è riportato un elenco di problemi di configurazione comuni che possono verificarsi durante la distribuzione del servizio Gestione API in una rete virtuale.

* **Installazione del server DNS personalizzato**: hello servizio Gestione API dipende da diversi servizi di Azure. Quando l'API di gestione è ospitato in una rete virtuale con un server DNS personalizzato, è necessario che i nomi host hello tooresolve di tali servizi Azure. Vedere [queste](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) informazioni aggiuntive sulla configurazione del DNS personalizzato. Vedere tabella porte hello riportata di seguito e altri requisiti di rete per riferimento.

> [!IMPORTANT]
> È consigliabile, se si utilizza un server DNS personalizzato per la rete virtuale hello, configurare che **prima** distribuzione di un servizio di gestione API al suo interno. In caso contrario è necessario troppo aggiornare il servizio di gestione API hello ogni volta che si modifica il server DNS hello (s) eseguendo hello [applicare operazioni di configurazione di rete](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Porte richieste per l'API di gestione**: il traffico in ingresso e in uscita in hello Subnet in cui viene distribuito l'API di gestione può essere controllato utilizzando [Network Security Group][Network Security Group]. Se una qualsiasi di queste porte non è disponibile, Gestione API potrebbe non funzionare correttamente e potrebbe diventare inaccessibile. Il blocco di una o più di tali porte è un problema di configurazione comune nell'uso di Gestione API in una rete virtuale.

Quando un'istanza del servizio Gestione API è ospitata in una rete virtuale, vengono utilizzate porte hello in hello nella tabella seguente.

| Porte di origine/destinazione | Direzione | Protocollo di trasporto | Scopo | Origine/Destinazione | Tipo di accesso |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |In ingresso |TCP |TooAPI di comunicazione client Management |INTERNET / VIRTUAL_NETWORK |Esterno |
| */3443 |In ingresso |TCP |Endpoint di gestione per il portale di Azure e PowerShell |INTERNET / VIRTUAL_NETWORK |Esterno e interno |
| * / 80, 443 |In uscita |TCP |Dipendenza da Archiviazione di Azure e dal bus di servizio di Azure |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| * / 1433 |In uscita |TCP |Dipendenza da SQL di Azure |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| * / 11000 - 11999 |In uscita |TCP |Dipendenza da Azure SQL V12 |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| * / 14000 - 14999 |In uscita |TCP |Dipendenza da Azure SQL V12 |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| * / 5671 |In uscita |AMQP |Dipendenze per i criteri di Hub tooEvent Log e agente di monitoraggio |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| 6381 - 6383/6381 - 6383 |In ingresso e in uscita |UDP |Dipendenza dalla cache Redis |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Esterno e interno |-
| * / 445 |In uscita |TCP |Dipendenza dalla condivisione file di Azure per GIT |VIRTUAL_NETWORK / INTERNET |Esterno e interno |
| * / * | In ingresso |TCP |Bilanciamento del carico di infrastruttura di Azure | VIRTUAL_NETWORK/AZURE_LOADBALANCER |Esterno e interno |

* **La funzionalità SSL**: certificato SSL tooenable catena servizio Gestione API hello compilazione e la convalida deve tooocsp.msocsp.com di connettività di rete in uscita, mscrl.microsoft.com e crl.microsoft.com. Questa dipendenza non è necessaria se qualsiasi certificato caricato tooAPI Management contenga radice toohello autorità di certificazione di hello catena completa.

* **Accesso a DNS**: l'accesso in uscita sulla porta 53 è necessario per la comunicazione con i server DNS. Se un server DNS personalizzato esiste in hello altra entità finale di un gateway VPN, server DNS hello deve essere raggiungibile dalla subnet hello gestione API di hosting.

* **Monitoraggio dell'integrità e le metriche**: in uscita connettività tooAzure monitoraggio gli endpoint di rete, quale risolto in hello seguenti domini: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Express Route installazione**: una configurazione personalizzata comune è toodefine i propri route predefinita (0.0.0.0/0) impone in uscita Internet traffico tooinstead flusso locale. Questo flusso di traffico indubbiamente a interruzioni di connettività con gestione API di Azure perché il traffico in uscita hello è bloccato in locale o NAT certificati tooan Impossibile riconoscere gli indirizzi che non funzionano con vari endpoint di Azure. soluzione hello è route definite dall'utente toodefine (più) ([UDRs][UDRs]) nella subnet hello contenente hello gestione API di Azure. Un UDR definisce le route di subnet specifiche che verranno utilizzato il valore anziché route predefinita hello.
  Se possibile, è consigliabile hello toouse seguente configurazione:
 * configurazione di ExpressRoute Hello annuncia 0.0.0.0/0 e per impostazione predefinita force tunnel tutto il traffico in uscita in locale.
 * Hello UDR applicato toohello subnet contenente hello gestione API di Azure definisce 0.0.0.0/0 con un tipo di hop successivo di Internet.
 Hello effetto combinato di questi passaggi è che il livello di subnet hello UDR ha la precedenza su hello garantendo l'accesso a Internet in uscita da hello gestione API di Azure, tunneling forzato ExpressRoute.

>[!WARNING]  
>Gestione API di Azure non è supportato con ExpressRoute configurazioni che **in modo non corretto tra-annunciare le route da hello peering percorso toohello privata percorso di peering pubblico**. Le configurazioni di ExpressRoute che dispongono di peering pubblico configurato, riceveranno gli annunci di route da Microsoft per un elevato numero di intervalli di indirizzi IP di Microsoft Azure. Se questi intervalli di indirizzi in modo non corretto tra annunciati nel percorso di peering privato hello, risultato finale hello è che tutti i pacchetti di rete in uscita dalla subnet dell'istanza di hello gestione API di Azure sono di rete locale del cliente in modo errato il tunneling forzato tooa infrastruttura. Questo flusso di rete interromperà il servizio Gestione API di Azure. problema di toothis soluzione hello è toostop le route tra annunci hello peering percorso toohello privata percorso di peering pubblico.


## <a name="troubleshooting"> </a>Risoluzione dei problemi
Quando si effettua rete tooyour modifiche, fare riferimento troppo[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate se hello servizio Gestione API non ha perso l'accesso tooany di hello risorse critiche che dipende. stato della connettività Hello deve essere aggiornato ogni 15 minuti.

## <a name="limitations"></a>Limitazioni
* Una subnet contenente le istanze di Gestione API non può contenere altri tipi di risorse di Azure.
* subnet Hello e hello API Gestione servizio deve essere in hello stessa sottoscrizione.
* Una subnet contenente le istanze di gestione API non può essere spostata da una sottoscrizione all'altra.
* Quando si utilizza una rete virtuale interna, solo un indirizzo IP interno saranno disponibile indicato l'intervallo di hello [RFC 1918](https://tools.ietf.org/html/rfc1918), non può essere fornito un indirizzo IP pubblico.
* Per le distribuzioni di gestione API di più aree, con le reti virtuali interne configurate, gli utenti sono responsabili per la gestione dei propri come possiedono hello DNS di bilanciamento del carico.


## <a name="related-content"></a>Contenuti correlati
* [Connessione toobackend una rete virtuale tramite il Vpn Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Connessione di una rete virtuale da modelli di distribuzione differenti](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Modalità toouse hello tootrace API controllo chiama in Gestione API di Azure](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
