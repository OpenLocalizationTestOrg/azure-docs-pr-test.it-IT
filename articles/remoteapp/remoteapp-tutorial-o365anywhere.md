---
title: aaaGet hello stessa esperienza di Office 365 su qualsiasi dispositivo con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooshare qualsiasi app di Office 365 con gli utenti con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello stessa esperienza di Office 365 su qualsiasi dispositivo con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

In questo articolo illustra come toodeploy Office 365 su qualsiasi dispositivo nell'azienda. Gli utenti possono usare hello stesse funzionalità e di esperienza dell'interfaccia utente in Windows, Android e Apple.

A questo scopo, si userà Azure RemoteApp mediante l’hosting di Office 365 in macchine virtuali scalabili di Azure a cui gli utenti possono connettersi. Questo set di macchine virtuali è detto "raccolta nel cloud".

## <a name="create-a-cloud-collection"></a>Creare una raccolta nel cloud
Dopo aver creato un account Azure, passare troppo**RemoteApp** facendo clic sul collegamento hello hello lato sinistro.
![Con Azure RemoteApp nel portale di Azure hello](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Procedere quindi alla **nuova** nella parte inferiore di hello e "Creazione rapida" una raccolta. Specificare un nome area hello, sottoscrizione hello, piano hello e immagine hello "Proffesional Office 2013" fornito da Microsoft.
![Finestra di dialogo Crea](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Al termine processo di creazione di hello modulo hello raccolta deve iniziare. Questa operazione potrebbe richiedere ore tooan o meno.

![Waiting](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Al termine il processo di hello, sarà simile al seguente. Se si fa clic su **Pubblicazione** , si noterà che la maggior parte delle applicazioni di Office è già stata pubblicata.
![Raccolta creata](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![App pubblicate](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

A questo punto è anche possibile aggiungere più utenti che hanno accesso toothis raccolta facendo **accesso utente**.
![Configurare l'accesso utente](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Ora si proverà timeout connessione tooOffice 365!

## <a name="connect-toooffice-365"></a>Connettersi tooOffice 365
Si sarà head su troppo[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scorrere verso il basso e fare clic su **scaricare i client** client di Azure RemoteApp hello tooinstall sul dispositivo hello ci si trova. Hello schermate riportate di seguito sono per Windows.

Una volta avviata un'applicazione hello chiesto toosign con l'account Microsoft (precedentemente denominato "Live ID"), utilizzare hello corrisponde a quello dell'account di Azure per il momento. Dopo avere eseguito l'accesso dovrebbe essere visualizzata una notifica relativa a nuovi inviti. Fare clic sulla notifica per visualizzare un elenco come il seguente. Accettare l'invito hello corrispondente della posta elettronica del proprietario di account di Azure.

![Nuovo invito](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Ecco come appare la schermata quando sono presenti nuovi inviti.

![Accettare un'applicazione](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Dopo avere accettato l'invito hello dovrebbe tutte le app di Office hello nel client di Azure RemoteApp hello.

![Elenco di app](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Quando si sceglie uno di tali applicazioni, hello devono iniziare in hello macchina virtuale di Azure e dovrebbe essere tutto a posto. Buon lavoro.

![Avvio](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

