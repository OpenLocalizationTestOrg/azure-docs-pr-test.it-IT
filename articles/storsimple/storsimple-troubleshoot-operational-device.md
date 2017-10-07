---
title: un dispositivo StorSimple distribuito aaaTroubleshoot | Documenti Microsoft
description: "Viene descritto come toodiagnose e correggere gli errori che si verificano in un dispositivo StorSimple è attualmente distribuito e operativo."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Risoluzione dei problemi relativi a un dispositivo StorSimple operativo
## <a name="overview"></a>Panoramica
Questo articolo fornisce utili indicazioni sulla risoluzione dei problemi riguardo la configurazione che possono verificarsi dopo che il dispositivo StorSimple è distribuito e operativo. Vengono descritti i problemi comuni, possibili cause e toohelp di procedure consigliate che risolvere i problemi che potrebbero verificarsi durante l'esecuzione di Microsoft Azure StorSimple. Queste informazioni si applicano dispositivo fisico locale tooboth hello StorSimple e dispositivo virtuale StorSimple hello.

Alla fine di hello di questo articolo che è possibile trovare un elenco dei codici di errore che potrebbero verificarsi durante l'operazione di Microsoft Azure StorSimple, nonché i passaggi da eseguire errori hello tooresolve. 

## <a name="setup-wizard-process-for-operational-devices"></a>Procedura di configurazione guidata per i dispositivi operativi
Utilizzare Installazione guidata di hello ([Invoke-HcsSetupWizard][1]) toocheck hello configurazione del dispositivo e adottare misure correttive se necessario.

Quando si esegue l'installazione guidata di hello in un dispositivo precedentemente configurato e operativo, hello flusso del processo è diverso. È possibile modificare solo hello seguenti voci:

* Indirizzo IP, subnet mask e gateway
* Server DNS primario
* Server NTP primario
* Configurazione del proxy Web facoltativa

non esegue l'installazione guidata di Hello hello operazioni toopassword correlati insieme e registrazione del dispositivo.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Errori che si verificano durante le esecuzioni successive dell'installazione guidata di hello
alcune possibili cause di errori di hello e le azioni consigliate tooresolve li Hello nella tabella seguente vengono descritti gli errori di hello che potrebbero verificarsi quando si esegue l'installazione guidata di hello in un dispositivo operativo. 

| No. | Messaggio di errore o condizione | Possibili cause | Azione consigliata |
|:--- |:--- |:--- |:--- |
| 1 |Errore 350032: il dispositivo è già stato disattivato. |Questo errore si verifica se si esegue l'installazione guidata di hello in un dispositivo disattivato. |[Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per i passaggi successivi. Un dispositivo disattivato non può essere messo in servizio. Ripristino delle impostazioni predefinite potrebbe essere necessario prima di poter attivare il dispositivo hello nuovamente. |
| 2 |Invoke-HcsSetupWizard: ERROR_INVALID_FUNCTION (eccezione da HRESULT: 0x80070001) |aggiornamento del server DNS Hello non riesce. Le impostazioni DNS sono impostazioni globali e vengono applicate a tutte le interfacce di rete hello abilitato. |Abilitare hello interfaccia e applicare nuovamente le impostazioni DNS hello. Ciò potrebbe interferire con la rete hello per le altre interfacce abilitate poiché queste impostazioni sono globali. |
| 3 |dispositivo Hello sembra toobe online nel portale del servizio StorSimple Manager hello, ma quando si tenta l'installazione minima di toocomplete hello e salvare la configurazione di hello, hello operazione non riesce. |Durante l'installazione iniziale, hello web proxy non è stato configurato, anche se si è verificato un server proxy effettivo sul posto. |Hello utilizzare [cmdlet Test-HcsmConnection] [ 2] errore hello toolocate. [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) in caso di problema hello toocorrect non è possibile. |
| 4 |Invoke-HcsSetupWizard: Valore non compreso nell'intervallo di hello previsto. |L'errore viene generato da una subnet mask non corretta. Le possibili cause sono:  <ul><li> Hello subnet mask è mancante o vuoto.</li><li>formato di prefisso Ipv6 Hello è corretto.</li><li>interfaccia Hello è abilitata per il cloud, ma gateway hello è mancante o non corretto.</li></ul>Si noti che DATA 0 è automaticamente abilitata per il cloud se configurata tramite installazione guidata di hello. |problema di hello toodetermine, usare la subnet 0.0.0.0 o 256.256.256.256 e quindi osservare output di hello. Immettere i valori corretti per hello subnet mask, gateway e il prefisso Ipv6, in base alle esigenze. |

## <a name="error-codes"></a>Codici di errore
Gli errori sono elencati in ordine numerico.

| Numero di errore | Testo o descrizione dell’errore | Azione consigliata per l’utente |
|:--- |:--- |:--- |
| 10502 |Si è verificato un errore durante l'accesso all'account di archiviazione. |Attendere alcuni minuti e ripetere l'operazione. Se hello errore persiste, è possibile, contattare il supporto tecnico Microsoft per i passaggi successivi. |
| 40017 |un volume specificato nel criterio di backup hello non è stato trovato nel dispositivo di hello, l'operazione di backup Hello non è riuscita. |Ripetere l'operazione di backup hello, se hello l'errore persiste, contattare il supporto Microsoft. per conoscere le fasi successive. |
| 40018 |operazione di backup Hello non riuscita perché nessuno dei volumi hello specificati nei criteri di backup hello sono stati trovati nel dispositivo hello. |Ripetere l'operazione di backup hello, se hello l'errore persiste, contattare il supporto Microsoft. per conoscere le fasi successive. |
| 390061 |sistema di Hello è occupato o non disponibile. |Attendere alcuni minuti e ripetere l'operazione. Se hello errore persiste, è possibile, contattare il supporto tecnico Microsoft per i passaggi successivi. |
| 390143 |Si è verificato un errore con codice di errore 390143. (Errore sconosciuto). |Se hello errore persiste, contattare il supporto Microsoft per i passaggi successivi. |

## <a name="next-steps"></a>Passaggi successivi
In caso di problema hello tooresolve non è possibile, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per assistenza. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
