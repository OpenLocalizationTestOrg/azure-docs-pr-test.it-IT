---
title: problemi di attivazione aaaTroubleshoot Windows macchina virtuale in Azure | Documenti Microsoft
description: Fornisce hello risolvere i passaggi per la risoluzione dei problemi di attivazione di Windows macchina virtuale in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Risolvere i problemi di attivazione della macchina virtuale Windows di Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se si verificano problemi durante l'attivazione della macchina virtuale Windows Azure (VM) che viene creato da un'immagine personalizzata, è possibile utilizzare le informazioni di hello fornite in questo numero di documento tootroubleshoot hello. 

## <a name="symptom"></a>Sintomo

Quando si tenta di tooactivate una macchina virtuale Windows Azure, viene visualizzato un errore simile a quello riportato hello seguente esempio:

**Errore: hello 0xC004F074 LicensingService Software segnalato che non è possibile attivare i computer hello. Impossibile contattare un servizio di gestione delle chiavi. Vedere hello registro eventi dell'applicazione per ulteriori informazioni.**

## <a name="cause"></a>Causa
In genere, i problemi di attivazione di macchina virtuale di Azure verificano se hello macchina virtuale di Windows non è configurata per utilizzando hello chiave di configurazione client KMS appropriato, o macchina virtuale di Windows hello è un toohello problema di connettività del servizio di gestione delle CHIAVI di Azure (kms.core.windows.net, porta 1668). 

## <a name="solution"></a>Soluzione

>[!NOTE]
>Se si utilizza una VPN da sito a sito e, tunneling forzato vedere [utilizzare Azure personalizzato instrada tooenable KMS activation con il tunneling forzato](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Se si usa ExpressRoute e dispone di una route predefinita pubblicati, vedere [macchina virtuale di Azure potrebbe non riuscire tooactivate expressroute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Passaggio 1 Configura hello KMS client setup chiave appropriata (per Windows Server 2016 e Windows Server 2012 R2)

Per hello macchina virtuale creata da un'immagine personalizzata di Windows Server 2016 o Windows Server 2012 R2, è necessario configurare hello KMS client setup chiave appropriata per hello macchina virtuale.

Questo passaggio non è applicabile tooWindows 2012 o Windows 2008 R2. Usa la funzionalità di automazione macchina virtuale di attivazione hello, che è supportata solo in Windows Server 2016 e Windows Server 2012 R2.

1. Eseguire **slmgr.vbs /dlv** in un prompt dei comandi con privilegi elevati. Controllare il valore di descrizione nell'output di hello hello e quindi determinare se è stato creato da (canale di vendita al dettaglio) delle vendite al dettaglio o un supporto licenza volume (VOLUME_KMSCLIENT):
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Se **slmgr.vbs /dlv** Mostra canale di vendita al dettaglio, eseguire hello seguente hello tooset comandi [chiave di configurazione client KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) per la versione di hello del Server di Windows in uso e forza tooretry attivazione: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Ad esempio, per Data Center di Windows Server 2016, eseguire hello comando seguente:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Passaggio 2 verificare la connettività hello tra hello macchina virtuale e servizio di gestione delle CHIAVI di Azure

1. Scaricare ed estrarre hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) strumento tooa locale cartella hello macchina virtuale che non attiva. 

2. Passare tooStart, eseguire una ricerca in Windows PowerShell, fare doppio clic su Windows PowerShell e quindi scegliere Esegui come amministratore.

3. Verificare che tale hello che macchina virtuale è configurata server di gestione delle CHIAVI di Azure toouse hello corretto. toodo questa operazione, eseguire il comando seguente:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    comando Hello deve restituire: nome computer del servizio di gestione chiave imposta tookms.core.windows.net:1688 correttamente.

4. Verificare tramite Psping che si disponga della connettività toohello KMS server. Passare toohello cartella in cui è stato estratto download Pstools.zip hello e quindi eseguire hello seguente:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Nella riga di secondo penultima hello dell'output di hello, verificare che sia visualizzato: inviati = 4, ricevuti = 4, Lost = 0 (0% persi).

  Se Lost è maggiore di 0 (zero), hello macchina virtuale non dispone di server di gestione delle CHIAVI toohello di connettività. In questo caso, se hello macchina virtuale si trova in una rete virtuale e dispone di un server DNS personalizzato, è necessario assicurarsi che il server DNS è in grado di tooresolve kms.core.windows.net. In alternativa, è possibile modificare hello DNS server tooone risolti kms.core.windows.net.

  Tenere presente che, se si rimuovono tutti i server DNS da una rete virtuale, le VM usano il servizio DNS interno di Azure. Questo servizio può risolvere kms.core.windows.net.
  
Verificare inoltre che il firewall hello guest non è stato configurato in modo che blocca i tentativi di attivazione.

5. Dopo aver verificato la connettività tookms.core.windows.net, eseguire hello seguente comando al prompt Windows PowerShell con privilegi elevati. Questo comando tenta l'attivazione più volte.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

L'attivazione restituisce informazioni che è simile al seguente hello:

**Attivazione di Windows(R), Server Datacenter Edition (12345678-1234-1234-1234-12345678) in corso… Attivazione prodotto completata.**

## <a name="faq"></a>domande frequenti 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Hello Windows Server 2016 è stata creata da Azure Marketplace. È necessario tooconfigure codice Product key per l'attivazione di Windows Server 2016 hello? 
 
No. immagine di Hello in Azure Marketplace è hello KMS client setup chiave appropriata già configurato. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Lavoro attivazione di Windows hello stesso modo indipendentemente dal se hello VM utilizza Azure ibrida utilizzare vantaggio (HUB) o non? 
 
Sì. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Che cosa succede se il periodo di attivazione di Windows scade? 
 
Se è scaduto il periodo di tolleranza hello e ancora non è attivato Windows, Windows Server 2008 R2 e versioni successive di Windows mostrerà ulteriori notifiche sull'attivazione. sfondo del desktop Hello rimane nero e Windows Update installerà sicurezza e gli aggiornamenti critici, ma gli aggiornamenti non è facoltativi. Vedere le notifiche di hello hello ultima sezione di hello [condizioni di licenza](http://technet.microsoft.com/en-us/library/ff793403.aspx) pagina.   

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
