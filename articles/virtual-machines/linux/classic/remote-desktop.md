---
title: aaaRemote Desktop tooa VM Linux | Documenti Microsoft
description: Informazioni su come tooinstall e configurare Desktop remoto tooconnect tooa VM Linux di Microsoft Azure per modello di distribuzione classica hello
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Utilizzo di Desktop remoto tooconnect tooa VM Linux di Microsoft Azure
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per hello aggiornata la versione di gestione risorse di questo articolo, vedere [qui](../use-remote-desktop.md).

## <a name="overview"></a>Panoramica
Il protocollo RDP (Remote Desktop Protocol) è un protocollo proprietario utilizzato per Windows. Come possiamo usare RDP tooconnect tooa VM Linux (macchina virtuale) in modalità remota?

Questa Guida verrà fornite risposte hello! Questo risulterà utile xrdp tooinstall e file di configurazione nella macchina virtuale Linux di Microsoft Azure, che consente di connettersi tooit con Desktop remoto da un computer Windows. Si utilizzerà VM Linux in esecuzione Ubuntu o OpenSUSE come esempio hello in questa Guida.

strumento xrdp Hello è open source server RDP che consente di tooconnect server Linux con Desktop remoto da un computer Windows. RDP offre prestazioni migliori di VNC (Virtual Network Computing). VNC esegue il rendering usando una grafica di qualità JPEG e può risultare lento, mentre RDP è veloce e nitido.

> [!NOTE]
> È necessario disporre di una macchina virtuale di Microsoft Azure che esegue Linux. toocreate e impostare una VM Linux, vedere hello [esercitazione VM Linux di Azure](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Creare un endpoint per Desktop remoto
Si utilizzerà l'endpoint predefinito hello 3389 per Desktop remoto in questo documento. Configurare un endpoint 3389 come `Remote Desktop` tooyour VM Linux come il seguente:

![immagine](./media/remote-desktop/endpoint-for-linux-server.png)

Se non si conosce tooset un endpoint per la macchina virtuale, vedere [questa Guida](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Installare Gnome Desktop
Tooyour VM Linux di connettersi tramite `putty`e installare `Gnome Desktop`.

Per Ubuntu, utilizzare:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Per OpenSUSE, usare:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Installare xrdp
Per Ubuntu, utilizzare:

    #sudo apt-get install xrdp

Per OpenSUSE, usare:

> [!NOTE]
> Aggiornare versione OpenSUSE hello con la versione di hello utilizzate nel comando seguente hello. esempio Hello seguente riguarda `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Avviare xrdp e impostare il servizio xdrp all'avvio
Per OpenSUSE, usare:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Per Ubuntu, xrdp verrà avviato e abilitato automaticamente al momento dell'avvio dopo l'installazione.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Uso di xfce se si usa una versione di Ubuntu successiva a Ubuntu 12.04LTS
Poiché hello versione corrente di xrdp non supporta Desktop Gnome per Ubuntu versioni successiva Ubuntu 12.04LTS, si utilizzerà `xfce` Desktop invece.

tooinstall `xfce`, utilizzare questo comando:

    #sudo apt-get install xubuntu-desktop

Quindi abilitare `xfce` usando questo comando:

    #echo xfce4-session >~/.xsession

Modificare il file di configurazione di hello `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Aggiungere la riga hello `xfce4-session` prima riga hello `/etc/X11/Xsession`.

toorestart hello xrdp servizio, usare questa opzione:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Connettersi alla macchina virtuale Linux da un computer Windows
In un computer Windows, avviare il client Desktop remoto hello e il nome DNS VM Linux di input. O toohello Dashboard della macchina virtuale nel portale di Azure hello, fare clic su `Connect` tooconnect VM Linux. In tal caso, si vedere la finestra di accesso hello:

![immagine](./media/remote-desktop/no2.png)

Accedere con il nome di utente hello e la password della VM Linux.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso di xrdp, vedere [http://www.xrdp.org/](http://www.xrdp.org/).
