---
title: Guida alla risoluzione dei problemi di DNS aaaAzure | Documenti Microsoft
description: "La modalità di problemi comuni di tootroubleshoot con DNS di Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Guida alla risoluzione dei problemi di DNS di Azure

Questa pagina fornisce informazioni sulla risoluzione dei problemi comuni di DNS di Azure.

Se questi passaggi non consentono di risolvere il problema, è anche possibile eseguire una ricerca o inserire una domanda nel [forum di supporto della community su MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). In alternativa, aprire una richiesta di Supporto tecnico di Azure.


## <a name="i-cant-create-a-dns-zone"></a>Non è possibile creare una zona DNS

problemi comuni tooresolve, provare a uno o più hello alla procedura seguente:

1.  Hello revisione che DNS di Azure di controllo Registra motivo dell'errore toodetermine hello.
2.  Ogni nome di zona DNS deve essere univoco all'interno del relativo gruppo di risorse, Ovvero, due zone DNS con hello stesso nome non può condividere un gruppo di risorse. Provare a usare un nome di zona o un gruppo di risorse diverso.
3.  Potrebbe essere visualizzato un errore "È stato raggiunto o superato hello il numero massimo di zone nella sottoscrizione {id sottoscrizione}." Utilizzare un'altra sottoscrizione di Azure, eliminare alcune aree oppure contattare il supporto tecnico di Azure tooraise il limite della sottoscrizione.
4.  Potrebbe essere visualizzato un errore "zona hello '{nome zona}' non è disponibile." Questo errore indica che il DNS di Azure è stato Impossibile tooallocate server dei nomi per la zona DNS. Provare a usare un nome di zona diverso. In alternativa, se si è proprietario del nome di dominio di hello, contattare il supporto tecnico di Azure, che può allocare server dei nomi per l'utente.


### <a name="recommended-documents"></a>**Documenti consigliati**

[Zone e record DNS](dns-zones-records.md)
<br>
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Non è possibile creare un record DNS

problemi comuni tooresolve, provare a uno o più hello alla procedura seguente:

1.  Hello revisione che DNS di Azure di controllo Registra motivo dell'errore toodetermine hello.
2.  Set di record hello esiste già?  DNS di Azure gestisce i record di utilizzo di record *imposta*, che sono raccolta hello dei record di hello stesso nome e hello stesso tipo. Se un record con hello stesso nome e tipo già esistente, quindi tooadd un altro record di questo tipo è consigliabile modificare hello record esistente.
3.  Si sta cercando toocreate un record al vertice di zona DNS hello (Buongiorno 'root' della zona hello)? In caso affermativo, hello convenzione DNS toouse hello ' @' carattere come nome del record di hello. Si noti inoltre che standard DNS hello non consentono i record CNAME al vertice zona hello.
4.  Si è verificato un conflitto CNAME?  standard DNS Hello non consentono un record CNAME con hello stesso nome di un record di qualsiasi altro tipo. Se si dispone di un CNAME esistente, la creazione di un record con hello stesso nome di un tipo diverso ha esito negativo.  Analogamente, la creazione di un record CNAME, ha esito negativo se hello nome corrisponde a un record esistente di un tipo diverso. Rimuovere il conflitto hello rimuovendo hello altri record o scegliere un nome di un record diverso.
5.  È stato raggiunto limite hello numero hello di set di record consentiti in una zona DNS di? Imposta il numero corrente di Hello del record e hello numero massimo di set di record viene visualizzato nel portale di Azure in hello 'proprietà' per la zona hello hello. Se si hanno raggiunto questo limite, quindi eliminare alcuni set di record o contatta tooraise supporto tecnico di Azure il limite del set di record per la zona, quindi riprovare. 


### <a name="recommended-documents"></a>**Documenti consigliati**

[Zone e record DNS](dns-zones-records.md)
<br>
[Creare una zona DNS](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Non riesco a risolvere un record DNS

La risoluzione dei nomi DNS è un processo articolato in più passaggi che può non riuscire per vari motivi. Hello passaggi seguenti consentono di analizzare perché la risoluzione DNS non riesce per un record DNS in una zona ospitata nel sistema DNS di Azure.

1.  Verificare che i record DNS hello siano stati configurati correttamente nel sistema DNS di Azure. Esaminare i record DNS hello in hello portale di Azure, verifica che nome zona hello e nome del record di tipo di record siano corretti.
2.  Verificare che i record DNS hello risolvere correttamente nel server dei nomi DNS di Azure hello.
    - Se si apportano le query DNS dal computer locale, è possibile ottenere risultati memorizzati nella cache che non riflettono lo stato corrente di hello hello server dei nomi.  Inoltre, alle reti aziendali utilizzano server proxy DNS, che impedire le query DNS indirizzate toospecific server dei nomi.  tooavoid questi problemi, utilizzare un servizio risoluzione dei nomi basato sul web, ad esempio [digwebinterface](http://digwebinterface.com).
    - Essere toospecify che server dei nomi corretto hello per la zona DNS, come illustrato nel portale di Azure hello.
    - Verificare che il nome DNS hello sia corretto (si dispone di nome completo di hello toospecify, inclusi nome della zona hello) e tipo di record hello sia corretto
3.  Verificare il nome di dominio DNS hello è stata correttamente [delega server dei nomi DNS di Azure toohello](dns-domain-delegation.md). Esistono [molti siti Web di terze parti da cui è possibile eseguire la convalida della delega DNS](https://www.bing.com/search?q=dns+check+tool). Questo test è un *zona* test di delega, deve essere immesso solo nome della zona DNS hello e non hello record nome completo.
4.  Dopo aver completato hello precedente, il record DNS debba ora risolto correttamente. tooverify, è possibile usare nuovamente [digwebinterface](http://digwebinterface.com), questa volta utilizzando le impostazioni di hello predefinite nome server.


### <a name="recommended-documents"></a>**Documenti consigliati**

[Delegato tooAzure un dominio DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Come specificare hello 'service' e 'protocollo' per un record SRV?

DNS di Azure gestisce i record DNS come set di record: hello raccolta di record con hello stesso nome e hello stesso tipo. Per un set di record SRV, servizio"hello" e "protocollo" necessario toobe specificato come parte del nome di set di record di hello. Hello SRV ('priority', 'peso', 'porta' e 'target') sono specificati altri parametri separatamente per ciascun record nel set di record di hello.

Nomi di record SRV di esempio ("sip" indica il nome del servizio, "tcp" il protocollo):

- \_SIP. \_tcp (Crea un set al vertice zona hello di record)
- \_sip.\_tcp.sipservice (crea un set di record denominato "sipservice")

### <a name="recommended-documents"></a>**Documenti consigliati**

[Zone e record DNS](dns-zones-records.md)
<br>
[Creare set di record DNS e i record utilizzando hello portale di Azure](dns-getstarted-create-recordset-portal.md)
<br>
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record) (Tipo di record SRV (Wikipedia))


## <a name="next-steps"></a>Passaggi successivi

* Informazioni sulle [zone e sui record di DNS di Azure](dns-zones-records.md)
* toostart tramite DNS di Azure, informazioni su come troppo[creare una zona DNS](dns-getstarted-create-dnszone-portal.md) e [creare record DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate una zona DNS esistente, informazioni su come troppo[importare ed esportare un file di zona DNS](dns-import-export.md).

