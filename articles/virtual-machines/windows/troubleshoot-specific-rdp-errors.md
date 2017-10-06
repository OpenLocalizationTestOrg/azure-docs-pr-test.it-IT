---
title: messaggi di errore aaaSpecific RDP per le macchine virtuali di Azure | Documenti Microsoft
description: Comprendere i messaggi di errore specifici che possono essere visualizzati durante il tentativo di utilizzo macchina virtuale di Windows tooa connessione Desktop remoto in Azure
keywords: "Errore di desktop remoto, errore di connessione desktop remoto, non è possibile connettersi tooVM, risoluzione dei desktop remoto"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Risoluzione dei problemi specifico tooa i messaggi di errore RDP macchina virtuale Windows in Azure
Si potrebbe ricevere un messaggio di errore specifico quando si utilizza una macchina virtuale di Windows tooa connessione Desktop remoto (VM) in Azure. Questo articolo presenta alcuni dei messaggi di errore più comuni rilevati, insieme a tooresolve passaggi di risoluzione dei problemi di hello li. Se si verificano problemi di connessione tooyour macchina virtuale tramite RDP senza non si verifica un messaggio di errore specifico, vedere hello [risoluzione dei problemi di Guida per il Desktop remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Per informazioni sui messaggi di errore specifico, vedere l'esempio hello:

* [la sessione remota di Hello è stata disconnessa perché sono non presenti una licenza tooprovide disponibili server licenze di Desktop remoto](#rdplicense).
* [Desktop remoto non è possibile trovare hello "nome computer"](#rdpname).
* [Si è verificato un errore di autenticazione. Hello autorità di protezione locale non può essere contattato](#rdpauth).
* [Errore di sicurezza di Windows: Le credenziali specificate non funzionano](#wincred).
* [Impossibile connettersi computer remoto toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>la sessione remota di Hello è stata disconnessa perché non esistono alcun tooprovide disponibile una licenza di server licenze di Desktop remoto.
Causa: hello 120 giorni periodo di prova per il ruolo di Server di Desktop remoto hello è scaduto e necessario tooinstall licenze.

In alternativa, salvare una copia locale del file RDP hello dal portale hello ed eseguire questo comando in un tooconnect prompt dei comandi di PowerShell. Questo passaggio disabilita la licenza solo per la connessione in oggetto:

        mstsc <File name>.RDP /admin

Se non è effettivamente necessario più di due toohello di connessioni di Desktop remoto VM simultanee, è possibile utilizzare ruolo di Server Manager tooremove hello Server Desktop remoto.

Per ulteriori informazioni, vedere hello post di blog [macchina virtuale di Azure ha esito negativo con "Nessun server Desktop remoti licenza disponibile"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Desktop remoto non è possibile trovare il computer di hello "name".
Causa: il client Desktop remoto hello nel computer in uso non è possibile risolvere il nome di hello del computer di hello nelle impostazioni di hello del file RDP hello.

Possibili soluzioni:

* Se si è nella intranet dell'organizzazione, assicurarsi che il computer dispone di server proxy di accesso toohello e può inviare tooit il traffico HTTPS.
* Se si utilizza un file RDP archiviato localmente, provare a utilizzare hello uno, viene generato dal portale hello. Questo passaggio consente di disporre di nome DNS corretto hello per macchina virtuale hello, o servizio cloud hello e porta dell'endpoint hello di hello macchina virtuale. Ecco un file RDP di esempio generato dal portale hello:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

è parte dell'indirizzo Hello del file RDP:

* Hello nome dominio completo del servizio cloud hello contenente hello VM ("tailspin-azdatatier.cloudapp.net" in questo esempio).
* porta TCP esterna Hello dell'endpoint di hello per il traffico di Desktop remoto (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Si è verificato un errore di autenticazione. Impossibile contattare Hello autorità di sicurezza locale.
Causa: destinazione hello VM non è possibile individuare autorità di sicurezza hello nella parte del nome utente hello delle credenziali.

Quando il nome utente è nel formato hello *SecurityAuthority*\\*UserName* (esempio: CORP\User1), hello *SecurityAuthority* parte è entrambi hello VM nome del computer (per l'autorità di sicurezza locale hello) o un nome di dominio Active Directory.

Possibili soluzioni:

* Se hello account locale toohello macchina virtuale, verificare che il nome della macchina virtuale hello sia stato digitato correttamente.
* Se l'account di hello si trova in un dominio Active Directory, controllare l'ortografia di hello hello del nome di dominio.
* Se si tratta di un account di dominio Active Directory e nome di dominio hello sia stato digitato correttamente, verificare che sia disponibile un controller di dominio nel dominio. Nelle reti virtuali di Azure che contengono controller di dominio, è un problema comune che un controller di dominio non sia disponibile perché non è stato avviato. Per risolvere il problema, è possibile usare un account amministratore locale anziché un account di dominio.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Errore di sicurezza di Windows: Le credenziali specificate non funzionano.
Causa: la destinazione hello VM non è possibile convalidare il nome dell'account e la password.

Un computer basato su Windows possa convalidare le credenziali di hello di un account locale o un account di dominio.

* Per gli account locali, utilizzare hello *ComputerName*\\*UserName* sintassi (esempio: SQL1\Admin4798).
* Per gli account di dominio, utilizzare hello *DomainName*\\*UserName* sintassi (esempio: CONTOSO\peterodman).

Se averlo alzato di livello il controller di dominio tooa macchina virtuale in una nuova foresta di Active Directory, l'account administrator locale hello è effettuato l'accesso viene convertito equivalente tooan account con hello stessa password in hello nuova foresta e del dominio. account locale Hello viene quindi eliminato.

Ad esempio, se è effettuato l'accesso con account locale hello DC1\DCAdmin e quindi alzare di livello macchina virtuale hello come un controller di dominio in una nuova foresta per il dominio corp.contoso.com hello, hello DC1\DCAdmin Ottiene eliminare l'account locale e un nuovo account di dominio (CORP\DCAdmin ) viene creato con hello stessa password.

Verificare che il nome account hello è un nome macchina virtuale hello è possibile verificare come un account valido e hello password non è corretto.

Se è necessario password hello toochange dell'account amministratore locale hello, vedere [come tooreset una password o hello Desktop remoto il servizio per le macchine virtuali Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Impossibile connettersi toohello computer remoto.
Causa: account hello tooconnect utilizzato non dispone di diritti di accesso Desktop remoto.

Ogni computer Windows è un gruppo locale di utenti Desktop remoto, che contiene account hello e i gruppi che possono accedere in remoto al suo interno. I membri del gruppo administrators locale hello dispongono di accesso, anche se tali account non elencati nel gruppo locale utenti Desktop remoto di hello. Per i computer appartenenti a un dominio, il gruppo di amministratori locali hello contiene anche gli amministratori di dominio hello per dominio hello.

Assicurarsi che si sta utilizzando tooconnect con account di hello disponga dei diritti di accesso Desktop remoto. In alternativa, utilizzare un dominio o tooconnect account amministratore locale tramite Desktop remoto. tooadd hello gruppo locale utenti Desktop remoto toohello account desiderato, utilizzare lo snap-in Microsoft Management Console hello (**sistema strumenti > utenti e gruppi locali > gruppi > utenti Desktop remoto**).

## <a name="next-steps"></a>Passaggi successivi
Se nessuno di questi errori si sono verificati e si verifica un problema sconosciuto con la connessione tramite RDP, vedere hello [risoluzione dei problemi di Guida per il Desktop remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Per la risoluzione dei problemi nell'accesso alle applicazioni in esecuzione in una macchina virtuale, vedere [applicazione tooan accesso di risoluzione dei problemi in esecuzione in una macchina virtuale di Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Se si sono verificati problemi di utilizzo di Secure Shell (SSH) tooconnect tooa VM Linux in Azure, vedere [tooa connessioni risolvere SSH VM Linux di Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

