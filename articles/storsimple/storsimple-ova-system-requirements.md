---
title: requisiti di sistema di Azure StorSimple Virtual Array aaaMicrosoft | Documenti Microsoft
description: Informazioni sui requisiti software e rete hello, per l'Array virtuale StorSimple
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>Requisiti di sistema StorSimple Virtual Array
## <a name="overview"></a>Panoramica
Questo articolo descrive i requisiti di sistema importanti hello per l'Array virtuale di Microsoft Azure StorSimple e per i client di archiviazione hello accesso hello matrice. È consigliabile rivedere attentamente le informazioni di hello prima di distribuire il sistema di StorSimple, quindi fare riferimento tooit come necessarie durante la distribuzione e l'operazione successiva.

i requisiti di sistema Hello includono:

* **Requisiti software per client di archiviazione** -descrive piattaforme di virtualizzazione hello è supportato, web browser, gli iniziatori iSCSI, i client SMB, i requisiti minimi del dispositivo virtuale ed eventuali requisiti aggiuntivi per questi sistemi operativi.
* **Requisiti di rete per il dispositivo StorSimple hello** -fornisce informazioni sulle porte hello toobe che è necessario aprire in tooallow il firewall per il traffico iSCSI, cloud o di gestione.

requisiti di sistema StorSimple Hello informazioni pubblicate in questo articolo si applica solo matrici virtuale tooStorSimple.

* Per i dispositivi 8000 serie, andare troppo[requisiti di sistema per il dispositivo StorSimple serie 8000](storsimple-system-requirements.md).
* Per i dispositivi 7000 serie, andare troppo[requisiti di sistema per il dispositivo serie 7000 di 5000 StorSimple](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Requisiti software
i requisiti software di Hello includono informazioni hello nei browser web hello è supportato, versioni SMB, piattaforme di virtualizzazione e i requisiti minimi del dispositivo virtuale hello.

### <a name="supported-virtualization-platforms"></a>Piattaforme di virtualizzazione supportate
| **Hypervisor** | **Versione** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 e versioni successive |
| VMware ESXi |5.5 e versioni successive |

### <a name="virtual-device-requirements"></a>Requisiti del dispositivo virtuale
| **Componente** | **Requisito** |
| --- | --- |
| Numero minimo di processori virtuali (memorie centrali) |4 |
| Memoria minima (RAM) |8 GB <br> Per un file server, 8 GB per meno di 2 milioni di file e 16 GB per 2 - 4 milioni di file|
| Spazio su disco<sup>1</sup> |Disco sistema operativo: 80 GB  <br></br>Disco dati - 500 GB too8 TB |
| Numero minimo di interfaccia o interfacce di rete |1 |
| Larghezza di banda Internet minima<sup>2</sup> |5 Mbps |

<sup>1</sup> : thin provisioning

<sup>2</sup> -i requisiti di rete possono variare a seconda della frequenza di modifica dei dati giornaliera hello. Ad esempio, se un dispositivo deve tooback 10 GB o più modifiche durante un giorno, quindi hello backup giornaliero su una connessione Mbps 5 potrebbe richiedere ore too4.25 (se dati hello potrebbero non essere compressi o deduplicati).

### <a name="supported-web-browsers"></a>Web browser supportati
| **Componente** | **Versione** | **Requisiti aggiuntivi/note** |
| --- | --- | --- |
| Microsoft Edge |Versione più recente | |
| Internet Explorer |Versione più recente |Testato con Internet Explorer 11 |
| Google Chrome |Versione più recente |Testato con Chrome 46 |

### <a name="supported-storage-clients"></a>Client di archiviazione supportati
Hello requisiti software seguenti è per gli iniziatori iSCSI hello accedere l'Array virtuale StorSimple (configurato come server iSCSI).

| **Sistemi operativi supportati** | **Versione richiesta** | **Requisiti aggiuntivi/note** |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012 R2 |StorSimple consente di creare volumi di thin provisioning o di provisioning completo. Non è possibile creare volumi con provisioning parziale. I volumi iSCSI StorSimple sono supportati solo nei seguenti casi:  <ul><li>Volumi semplici su dischi di base Windows.</li><li>NTFS Windows per la formattazione di un volume.</li> |

Hello requisiti software seguenti è per hello client SMB che accedono all'Array virtuale StorSimple (configurato come un file server).

| **Versione SMB** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Non copiare o archiviare i file protetti da file server di Windows Encrypting File System (EFS) toohello Array virtuale StorSimple; Ciò determina una configurazione non supportata. 
> 

### <a name="supported-storage-format"></a>Formati di archiviazione supportati
È supportato solo hello archivio blob in blocchi di Azure. I BLOB di pagine non sono supportati. Altre informazioni [sui BLOB in blocchi e i BLOB di pagine](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Requisiti di rete
Hello nella tabella seguente elenca le porte hello necessarie toobe aperto in tooallow il firewall per iSCSI, SMB, cloud o il traffico di gestione. In questa tabella, *in* o *in ingresso* fa riferimento toohello direzione da cui le richieste client in ingresso accesso al dispositivo. *Out* o *in uscita* fa riferimento toohello direzione in cui il dispositivo StorSimple invia i dati all'esterno, oltre distribuzione hello: ad esempio, in uscita toohello Internet.

| **Numero porta<sup>1</sup>** | **In ingresso/In uscita** | **Ambito porta** | **Obbligatorio** | **Note** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |In uscita |WAN |No |Porta in uscita viene utilizzata per gli aggiornamenti di tooretrieve accesso Internet. <br></br>proxy web in uscita Hello è configurabile dall'utente. |
| TCP 443 (HTTPS) |In uscita |WAN |Sì |Porta in uscita viene utilizzata per l'accesso ai dati nel cloud hello. <br></br>proxy web in uscita Hello è configurabile dall'utente. |
| UDP 53 (DNS) |In uscita |WAN |In alcuni casi; vedere le note. |Questa porta è obbligatoria solo se si usa un server DNS basato su Internet. <br></br> Nota: se si distribuisce un file server, si consiglia l'uso del server DNS locale. |
| UDP 123 (NTP) |In uscita |WAN |In alcuni casi; vedere le note. |Questa porta è obbligatoria solo se si usa un server NTP basato su Internet.<br></br> Nota: se si distribuisce un file server, si consiglia di sincronizzare l'ora con i controller di dominio di Active Directory. |
| TCP 80 (HTTP) |In ingresso |LAN |Sì |Questo è hello porta in ingresso per l'interfaccia utente locale nel dispositivo StorSimple hello per la gestione locale. <br></br> Si noti che l'accesso a hello locale dell'interfaccia utente tramite HTTP verrà reindirizzata automaticamente tooHTTPS. |
| TCP 443 (HTTPS) |In ingresso |LAN |Sì |Questo è hello porta in ingresso per l'interfaccia utente locale nel dispositivo StorSimple hello per la gestione locale. |
| TCP 3260 (iSCSI) |In ingresso |LAN |No |Questa porta è tooaccess utilizzati dati tramite iSCSI. |

<sup>1</sup> alcuna porta in ingresso non necessario toobe aperto su hello rete Internet pubblica.

> [!IMPORTANT]
> Verificare che il firewall hello non modificare o decrittografare tutto il traffico SSL tra il dispositivo di StorSimple hello e Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Modelli URL per le regole del firewall
Gli amministratori di rete spesso possono configurare un firewall avanzato regole basate su hello toofilter modelli di hello URL in ingresso e hello il traffico in uscita. L'array virtuale e servizio di gestione di dispositivi StorSimple hello dipendono da altre applicazioni di Microsoft, ad esempio Azure Service Bus, Access Control di Azure Active Directory, gli account di archiviazione e server di Microsoft Update. pattern di URL Hello associati a queste applicazioni può essere utilizzato tooconfigure regole del firewall. È importante toounderstand che è possono modificare i modelli di URL hello associati a queste applicazioni. Ciò a sua volta è necessario toomonitor amministratore di rete hello e aggiornare le regole del firewall per StorSimple come e quando richiesto. 

È consigliabile impostare le regole del firewall per il traffico in uscita, liberamente nella maggior parte dei casi, in base agli indirizzi IP StorSimple. Tuttavia, è possibile utilizzare informazioni hello sotto tooset avanzate regole del firewall che sono gli ambienti protetti toocreate necessari.

> [!NOTE]
> 
> * dispositivo Hello (origine) gli indirizzi IP deve essere sempre impostato le interfacce di rete abilitata per il cloud di tooall hello. 
> * destinazione Hello gli indirizzi IP devono essere impostato troppo[intervalli IP Data Center di Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| Modello URL | Componente/funzionalità |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Servizio Gestione dispositivi StorSimple<br>Servizio di controllo di accesso<br>Bus di servizio di Azure |
| `http://*.backup.windowsazure.com` |Registrazione del dispositivo |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revoca del certificato |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Account di archiviazione di Azure e monitoraggio |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Server di Microsoft Update<br> |
| `http://*.deploy.akamaitechnologies.com` |Rete CDN di Akamai |
| `https://*.partners.extranet.microsoft.com/*` |Pacchetto di supporto |
| `http://*.data.microsoft.com ` |Servizio di telemetria in Windows, vedere hello [aggiornamento per l'analisi e telemetria sulla diagnostica](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Passaggio successivo
* [Preparare toodeploy portale hello l'Array virtuale StorSimple](storsimple-virtual-array-deploy1-portal-prep.md)

