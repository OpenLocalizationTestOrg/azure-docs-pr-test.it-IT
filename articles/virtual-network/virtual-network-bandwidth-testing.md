---
title: "velocità effettiva della rete di macchina virtuale di Azure aaaTesting | Documenti Microsoft"
description: "Informazioni su come macchina virtuale di Azure tootest rete velocità effettiva."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Test della larghezza di banda/velocità effettiva (NTTTCP)

Durante il test delle prestazioni di velocità effettiva di rete in Azure, è uno strumento che ha come destinazione rete hello per il test e riduce al minimo hello uso di altre risorse che può influire sulle prestazioni di toouse migliore. È consigliabile usare NTTTCP.

Copiare lo strumento di hello tootwo macchine virtuali di Azure di hello stessa dimensione. Una macchina virtuale funziona come mittente e altri come ricevitore hello.

#### <a name="deploying-vms-for-testing"></a>Distribuzione di macchine virtuali per i test
Ai fini di hello di questo test, hello due macchine virtuali devono trovarsi in hello nello stesso servizio Cloud o hello stesso Set di disponibilità in modo che è possibile usare l'IP interno e l'esclusione bilanciamenti del carico hello test hello. È possibile tootest con hello VIP, ma questo tipo di test si trova fuori ambito hello di questo documento.
 
Prendere nota dell'indirizzo IP del ricevitore hello. In questo esempio verrà definito "a.b.c.r."

Prendere nota del numero di hello di core nella macchina virtuale hello. In questo esempio sarà "\#num\_cores"
 
Eseguire hello NTTTCP di test per 300 secondi (o 5 minuti) sul mittente hello macchina virtuale e il destinatario macchina virtuale.

Suggerimento: Quando si imposta questo test per hello prima volta, è possibile provare un più breve periodo tooget risultati dei test più rapidamente. Una volta hello strumento funziona come previsto, è possibile estendere secondi too300 periodo di prova hello per ottenere risultati più accurati hello.

> [!NOTE]
> mittente Hello **e** ricevitore deve specificare **hello stesso** test parametro di durata (-t).

tootest un singolo flusso TCP per 10 secondi:

Parametri ricevitore: ntttcp -r -t 10 -P 1

Parametri mittente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> Hello precedente esempio deve essere solo tooconfirm utilizzata la configurazione. Alcuni esempi di test effettivi vengono trattati più avanti in questo documento.

## <a name="testing-vms-running-windows"></a>Test di macchine virtuali che eseguono WINDOWS:

#### <a name="get-ntttcp-onto-hello-vms"></a>Ottenere NTTTCP su hello macchine virtuali.

Scaricare la versione più recente di hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

O cercarla se spostata: <https://www.bing.com/search?q=ntttcp+download>\<. Generalmente sarà il primo risultato ottenuto

È consigliabile inserire NTTTCP in una cartella separata, ad esempio, ad esempio c:\\strumenti

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Consente di NTTTCP attraverso il firewall di Windows hello
Sul ricevitore hello, creare una regola di assenso in hello Windows Firewall tooallow il tooarrive traffico NTTTCP. È più semplice tooallow hello intero NTTTCP programma in base al nome anziché tooallow specifiche porte TCP in ingresso.

Consenti ntttcp tramite hello Windows Firewall simile al seguente:

netsh advfirewall firewall add rule program=\<PERCORSO\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

Ad esempio, se è stato copiato ntttcp.exe toohello "c:\\strumenti" cartella, potrebbe essere il comando hello: 

netsh advfirewall firewall add rule program=c:\\strumenti\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>Esecuzione di test NTTTCP

Avviare NTTTCP su hello ricevitore (**eseguire da CMD**, ma non da PowerShell):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Se hello macchina virtuale dispone di quattro core e un indirizzo IP di 10.0.0.4, avrà un aspetto simile al seguente:

ntttcp -r –m 8,\*,10.0.0.4 -t 300


Avviare NTTTCP su hello mittente (**eseguire da CMD**, ma non da PowerShell):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Attendere i risultati di hello.


## <a name="testing-vms-running-linux"></a>Test di macchine virtuali che eseguono LINUX:

Usare nttcp-for-linux, disponibile all'indirizzo <https://github.com/Microsoft/ntttcp-for-linux>

In hello le macchine virtuali Linux (mittente e ricevitore), eseguire questi comandi per preparare ntttcp per linux su macchine virtuali:

CentOS - Installare Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Installare Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Verificare e installare in entrambie le macchine virtuali:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Come esempio di Windows hello, si presuppone il che indirizzo IP del ricevitore di hello Linux è 10.0.0.4

Avviare NTTTCP per Linux hello ricevitore:

``` bash
ntttcp -r -t 300
```

E in hello mittente, eseguire:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Test lunghezza predefinite too60 secondi se nessun parametro di tipo ora viene assegnato

## <a name="testing-between-vms-running-windows-and-linux"></a>Test tra macchine virtuali che eseguono Windows e LINUX:

Sugli scenari di questo è necessario abilitare la modalità nosync hello che consentono di eseguire il test di hello. Questa operazione viene eseguita tramite hello **-N flag** per Linux e **flag -ns** per Windows.

#### <a name="from-linux-toowindows"></a>Da tooWindows Linux:

Ricevitore <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Mittente <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Da Windows tooLinux:

Ricevitore <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Mittente <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Passaggi successivi
* A seconda dei risultati, potrebbe esserci spazio troppo[ottimizzare macchine di velocità effettiva di rete](virtual-network-optimize-network-bandwidth.md) per lo scenario.
* Ulteriori informazioni sono disponibili nell'articolo [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md)
