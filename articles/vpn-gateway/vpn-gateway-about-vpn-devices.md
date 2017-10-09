---
title: i dispositivi VPN aaaAbout per le connessioni di Azure cross-premise | Documenti Microsoft
description: Questo articolo illustra i dispositivi VPN e i parametri IPsec per connessioni cross-premise del Gateway VPN da sito a sito. Vengono forniti collegamenti tooconfiguration istruzioni ed esempi.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>Informazioni sui dispositivi VPN e sui parametri IPsec/IKE per connessioni del Gateway VPN da sito a sito

Un dispositivo VPN è necessario tooconfigure una connessione VPN di più sedi locali da sito a sito (S2S) tramite un gateway VPN. Le connessioni da sito a sito possono essere utilizzato toocreate una soluzione ibrida o se si desidera proteggere le connessioni tra le reti locali e le reti virtuali. Questo documento offre un elenco di dispositivi VPN convalidati e un elenco di parametri IPsec/IKE per i gateway VPN.

> [!IMPORTANT]
> Se si verificano problemi di connettività tra i dispositivi VPN locali e i gateway VPN, fare riferimento troppo[noti problemi di compatibilità dei dispositivi](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Elementi toonote durante la visualizzazione tabelle hello:

* È stata eseguita una modifica della terminologia per i Gateway VPN di Azure. Solo i nomi di hello sono stati modificati. Le funzionalità rimangono invariate.
  * Routing statico = PolicyBased
  * Routing dinamico = RouteBased
* Specifiche per i gateway VPN HighPerformance e gateway VPN RouteBased sono hello stesso, se non diversamente specificato. Ad esempio, i dispositivi VPN convalidato hello compatibili con gateway VPN RouteBased anche sono compatibili con gateway VPN HighPerformance hello.

## <a name="devicetable"></a>Dispositivi VPN convalidati e guide di configurazione per dispositivi

> [!NOTE]
> Quando si configura una connessione da sito a sito, è necessario un indirizzo IP IPv4 pubblico per il dispositivo VPN.
>

In collaborazione con i fornitori di dispositivi, è stato approvato un set di dispositivi VPN standard. Tutti i dispositivi hello in famiglie di dispositivi hello nel seguente elenco hello dovrebbero funzionare con gateway VPN. Vedere [sulle impostazioni del Gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand hello VPN digitare use (basato su criteri o tipo RouteBased) per una soluzione Gateway VPN da tooconfigure hello.

toohelp configurare il dispositivo VPN, fare riferimento i collegamenti toohello corrispondenti tooappropriate il gruppo di dispositivi. vengono fornite istruzioni di tooconfiguration collegamenti di Hello con cadenza principio del best effort. Per il supporto ai dispositivi VPN, contattare il produttore del dispositivo.

|**Fornitore**          |**Famiglia di dispositivi**     |**Versione minima del sistema operativo** |**Istruzioni di configurazione di tipo PolicyBased** |**Istruzioni di configurazione di tipo RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Non compatibile  |[Guida alla configurazione](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Router VPN serie AR |2.9.2                  |Presto disponibile     |Non compatibile  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-series |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Guida alla configurazione](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Guida alla configurazione](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-series |Barracuda Firewall 6.5 |[Guida alla configurazione](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Non compatibile |
| Brocade            |Vyatta 5400 vRouter   |Virtual Router 6.6R3 GA|[Guida alla configurazione](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Non compatibile |
| Punto di controllo |Gateway di protezione |R77.30 |[Guida alla configurazione](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Guida alla configurazione](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Non compatibile |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Esempi di configurazione*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 e versioni successive |[Guida alla configurazione](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Non compatibile |
| F5 |Serie BIG-IP |12.0 |[Guida alla configurazione](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Guida alla configurazione](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Guida alla configurazione](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Serie SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Guida alla configurazione](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Non compatibile |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Serie J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Esempi di configurazione](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Routing and Remote Access Service |Windows Server 2012 |Non compatibile |[Esempi di configurazione](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Gateway |N/D |[Guida alla configurazione](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Non compatibile |
| Openswan |Openswan |2.6.32 |(Presto disponibile) |Non compatibile |
| Palo Alto Networks |Tutti i dispositivi che eseguono PAN-OS |PAN-OS<br>PolicyBased: 6.1.5 o versione successiva<br>RouteBased: 7.1.4 |[Guida alla configurazione](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Guida alla configurazione](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWALL |Serie TZ, serie NSA<br>Serie SuperMassive<br>Serie NSA classe E |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Guida alla configurazione di SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guida alla configurazione di SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Guida alla configurazione di SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guida alla configurazione di SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Tutti |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Guida alla configurazione](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Guida alla configurazione](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) I router serie ISR 7200 supportano solo VPN PolicyBased.

## <a name="additionaldevices"></a>Dispositivi VPN non convalidati

Se non viene visualizzato il dispositivo elencato nella tabella di dispositivi VPN convalidati hello, il dispositivo può funzionare anche in una connessione Site-to-Site. Contattare il produttore del dispositivo per assistenza e istruzioni di configurazione.

## <a name="editing"></a>Modifica degli esempi di configurazione di dispositivo

Dopo aver scaricato l'esempio di configurazione del dispositivo VPN hello fornito, sarà necessario tooreplace alcuni hello valori impostazioni hello tooreflect per l'ambiente.

### <a name="tooedit-a-sample"></a>tooedit un esempio:

1. Aprire l'esempio hello utilizzando blocco note.
2. Cercare e sostituire tutte <*testo*> stringhe con valori hello pertinenti tooyour ambiente. Essere certi tooinclude < e >. Quando viene specificato un nome, nome hello selezionato deve essere univoco. Se un comando non funziona, consultare la documentazione del produttore del dispositivo.

| **Testo di esempio** | **Modificare in** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Nome scelto per questo oggetto. Esempio: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |Nome scelto per questo oggetto. Esempio: myAzureNetwork |
| &lt;RP_AccessList&gt; |Nome scelto per questo oggetto. Esempio: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |Nome scelto per questo oggetto. Esempio: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |Nome scelto per questo oggetto. Esempio: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Specificare l'intervallo. Esempio: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Specificare la subnet mask. Esempio: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Specificare l'intervallo in locale. Esempio: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Specificare la subnet mask locale. Esempio: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Questa rete virtuale tooyour specifici di informazioni e si trova nel portale di gestione di hello come **indirizzo IP del Gateway**. |
| &lt;SP_PresharedKey&gt; |Queste informazioni sono specifiche tooyour rete virtuale e si trovano nel portale di gestione come gestire chiave hello. |

## <a name="ipsec"></a>Parametri IPsec/IKE

> [!NOTE]
> Anche se i valori hello elencati nella tabella seguente hello sono supportati attualmente dal gateway VPN di hello, non vi è alcun meccanismo per toospecify o selezionare una combinazione di algoritmi o i parametri specifica da gateway VPN hello. È necessario specificare tutti i vincoli dal dispositivo VPN locale di hello. È inoltre necessario limitare **MSS** a **1350**.
> 
>

In hello le tabelle seguenti:

* SA = associazione di sicurezza
* La Fase 1 di IKE viene definita anche "Modalità principale"
* La Fase 2 di IKE viene definita anche "Modalità rapida"

### <a name="ike-phase-1-main-mode-parameters"></a>Parametri della Fase 1 di IKE (Modalità principale)

| **Proprietà**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Versione IKE           |IKEv1              |IKEv2              |
| Diffie-Hellman Group  |Gruppo 2 (1024 bit) |Gruppo 2 (1024 bit) |
| Metodo di autenticazione |Chiave precondivisa     |Chiave precondivisa     |
| Algoritmi di crittografia e di hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Durata dell'associazione di sicurezza           |28.800 secondi     |28.800 secondi     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Parametri della Fase 2 di IKE (Modalità rapida)

| **Proprietà**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Versione IKE                   |IKEv1          |IKEv2                                        |
| Algoritmi di crittografia e di hash |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Offerte per associazioni di sicurezza QM basate su route](#RouteBasedOffers) |
| Durata dell'associazione di sicurezza (tempo)            |3.600 secondi  |27.000 secondi                                |
| Durata dell'associazione di sicurezza (byte)           |102.400.000 KB | -                                           |
| Perfect Forward Secrecy (PFS) |No             |[Offerte per associazioni di sicurezza QM basate su route](#RouteBasedOffers) |
| Rilevamento peer inattivo     |Non supportate  |Supportato                                    |


### <a name ="RouteBasedOffers"></a>Offerte per associazioni di sicurezza IPsec VPN basate su route (associazione di sicurezza IKE Modalità rapida)

Hello nella tabella seguente sono elencati offerte SA IPsec (IKE in modalità rapida). Offerte sono ordine hello elencati di preferenza dell'offerta hello presentazione o accettazione.

#### <a name="azure-gateway-as-initiator"></a>Gateway Azure come iniziatore

|-  |**Crittografia**|**Autenticazione**|**Gruppo PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |

#### <a name="azure-gateway-as-responder"></a>Gateway Azure come risponditore

|-  |**Crittografia**|**Autenticazione**|**Gruppo PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |None         |
| 2 |AES256        |SHA1              |None         |
| 3 |3DES          |SHA1              |None         |
| 4 |AES256        |SHA256            |None         |
| 5 |AES128        |SHA1              |None         |
| 6 |3DES          |SHA256            |None         |
| 7 |DES           |SHA1              |None         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |None         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* È possibile specificare la crittografia NULL ESP IPsec con gateway VPN RouteBased e con prestazioni elevate. Crittografia basata su null non fornisce protezione toodata in transito e deve essere utilizzata solo quando massima velocità effettiva e minimo la latenza è obbligatorio. I client possono scegliere toouse questa in scenari di comunicazione di rete virtuale a oppure durante la crittografia viene applicata in un' posizione nella soluzione hello.
* Per la connettività cross-premise tramite hello Internet, utilizzare impostazioni del gateway VPN di Azure predefinito hello con la crittografia e algoritmi di hash elencati nelle tabelle di hello sopra tooensure sicurezza delle comunicazioni critiche.

## <a name="known"></a>Problemi noti di compatibilità del dispositivo

> [!IMPORTANT]
> Questi sono hello problemi di compatibilità noti tra i dispositivi VPN di terze parti e i gateway VPN di Azure. Hello team di Azure è attivamente impegnata con fornitori di hello tooaddress hello problemi elencati di seguito. Dopo aver risolti i problemi di hello, questa pagina verrà aggiornata con le informazioni più aggiornate hello. Controllarla periodicamente.
>
>

### <a name="feb-16-2017"></a>16 febbraio 2017

**Dispositivi Palo Alto Networks con versione precedente too7.1.4** per VPN basate su route Azure: se si usano i dispositivi VPN da reti Palo Alto con PAN-OS versione preliminare too7.1.4 e verifica connettività problemi tooAzure gateway VPN basate su route, eseguire hello alla procedura seguente:

1. Controllo versione di hello del firmware del dispositivo Palo Alto Networks. Se la versione PAN-OS è meno recente 7.1.4, eseguire l'aggiornamento too7.1.4.
2. Nel dispositivo Palo Alto Networks hello, cambiare hello fase 2 SA (o SA modalità rapida) durata too28, 800 secondi (8 ore) quando la connessione gateway VPN di Azure toohello.
3. Se si verificano ancora problemi di connettività, aprire una richiesta di supporto da hello portale di Azure.
