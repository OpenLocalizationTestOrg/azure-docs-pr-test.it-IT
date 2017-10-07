---
title: aaaConnect tooSQL Database utilizzando SQL Server Management Studio in Azure RemoteApp | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come toouse SQL Server Management Studio in Azure RemoteApp per la sicurezza e le prestazioni durante la connessione di Database tooSQL
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Utilizzare SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database

> [!IMPORTANT]
> Azure RemoteApp sta per essere sospeso. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
>

## <a name="introduction"></a>Introduzione
In questa esercitazione illustra come toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database. Viene illustrato il processo di hello di configurazione di SQL Server Management Studio in Azure RemoteApp, vengono illustrati i vantaggi di hello e illustra le funzionalità di sicurezza che è possibile utilizzare in Azure Active Directory.

**Toocomplete tempo stimato:** 45 minuti

## <a name="ssms-in-azure-remoteapp"></a>SSMS in Azure RemoteApp
Azure RemoteApp è un servizio di Servizi desktop remoto di Azure che fornisce applicazioni. Per altre informazioni, vedere: [Informazioni su Azure RemoteApp](../remoteapp/remoteapp-whatis.md)

SQL Server Management Studio in esecuzione in Azure RemoteApp consente hello stessa esperienza di esecuzione in locale di SQL Server Management Studio.

![Schermata di SSMS in esecuzione in Azure RemoteApp][1]

## <a name="benefits"></a>Vantaggi
Esistono molti vantaggi toousing SSMS in Azure RemoteApp, tra cui:

* La porta 1433 sul server SQL di Azure non dispone di toobe esposta esternamente (all'esterno di Azure).
* Nessuna necessità tookeep aggiunta e rimozione di indirizzi IP in firewall hello del server SQL Azure.
* Tutte le connessioni di Azure RemoteApp avvengono tramite HTTPS sulla porta 443 con Remote Desktop Protocol crittografato.
* È multiutente e scalabile.
* È un miglioramento delle prestazioni dalla presenza di SQL Server Management Studio in hello stessa area hello Database SQL.
* È possibile controllare l'utilizzo di Azure RemoteApp con hello Premium edition di Azure Active Directory che contiene il report attività utente.
* È possibile abilitare Multi-Factor Authentication (MFA).
* Client di Azure RemoteApp di accesso SQL Server Management Studio in qualsiasi punto quando si utilizza uno di hello supportati che include iOS, Android, Mac, Windows Phone e PC Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Creare una raccolta di hello Azure RemoteApp
Di seguito è hello passaggi toocreate la raccolta RemoteApp di Azure con SQL Server Management Studio:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Creare una nuova VM Windows da immagine
Utilizzare hello immagine "Windows Server Remote Desktop sessione Host Windows Server 2012 R2" da hello raccolta toomake la nuova macchina virtuale.

### <a name="2-install-ssms-from-sql-express"></a>2. Installare SSMS da SQL Express
Andare nella nuova macchina virtuale hello e passare la pagina di download toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

È un download tooonly opzione SQL Server Management Studio. Dopo il download, passare alla directory di installazione hello ed eseguire il programma di installazione tooinstall SSMS.

È inoltre necessario tooinstall SQL Server 2014 Service Pack 1. Scaricarlo qui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 include le funzionalità essenziali per l'utilizzo del database SQL di Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Eseguire lo script di convalida e Sysprep
In hello desktop della macchina virtuale hello è uno script di PowerShell denominato convalida. Fare doppio clic sullo script per eseguirlo. Verificherà che hello macchina virtuale è pronta toobe utilizzato per l'hosting remoto di applicazioni. Quando si verifica è completa, viene chiesto di sysprep toorun - scegliere toorun è.

Al termine, sysprep viene chiuso hello macchina virtuale.

toolearn informazioni sulla creazione di un'immagine di Azure RemoteApp, vedere: [come immagine di un modello di RemoteApp toocreate in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Acquisire l'immagine
Quando hello VM ha smesso di funzionare, individuarlo nel portale corrente hello e acquisirlo.

toolearn più informazioni sull'acquisizione di un'immagine, vedere [acquisire un'immagine di una macchina virtuale Windows Azure creata con il modello di distribuzione classica hello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Aggiungere immagini modello RemoteApp tooAzure
Nella sezione di Azure RemoteApp del portale corrente hello hello, andare scheda immagini modello toohello e fare clic su Aggiungi. Nella finestra popup hello, selezionare "Importare un'immagine dalla raccolta di macchine virtuali", quindi scegliere hello immagine appena creato.

### <a name="6-create-cloud-collection"></a>6. Creare una raccolta nel cloud
Nel portale corrente hello, creare una nuova raccolta Cloud di Azure RemoteApp. Scegliere hello immagine modello appena importata con SQL Server Management Studio è installato.

![Creare una nuova raccolta nel cloud][2]

### <a name="7-publish-ssms"></a>7. Pubblicare SSMS
Nella pubblicazione di un'applicazione dalla scheda della finestra il nuovo insieme di cloud, seleziona pubblica hello hello Menu Start e quindi scegliere SQL Server Management Studio elenco hello.

![Pubblicare l'app][5]

### <a name="8-add-users"></a>8. Aggiungi utenti
Nella scheda accesso utente hello è possibile selezionare gli utenti di hello che disporranno di accesso toothis Azure RemoteApp raccolta che include solo SQL Server Management Studio.

![Aggiunta di un utente][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Installare un'applicazione client hello Azure RemoteApp
Scaricare e installare un client di Azure RemoteApp qui: [Scaricare | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configurare il server SQL di Azure
Hello configurazione necessaria è tooensure che servizi di Azure è abilitato per il firewall hello. Se si utilizza questa soluzione, quindi non è necessario tooadd qualsiasi firewall di hello tooopen gli indirizzi IP. traffico di rete Hello consentito toohello SQL Server è da altri servizi di Azure.

![Consentire Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
MFA può essere abilitata appositamente per questa applicazione. Andare nella scheda applicazioni toohello di Azure Active Directory. È disponibile una voce per Microsoft Azure RemoteApp. Se si sceglie di tale applicazione e quindi configurare, si noterà hello pagina in cui è possibile abilitare l'autenticazione a più fattori per questa applicazione.

![Abilitare MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Controllare l'attività utente con Azure Active Directory Premium
Se non è Azure AD Premium, è necessario tooturn in su hello sezione licenze della directory. Con Premium abilitato, è possibile assegnare agli utenti di livello Premium toohello.

Quando si passa tooa utente in Azure Active Directory, sarà quindi possibile passare toohello attività scheda toosee accesso informazioni tooAzure RemoteApp.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver completato tutti hello sopra passaggi, verrà client di Azure RemoteApp in grado di toorun hello e Accedi con un utente assegnato. Verrà visualizzata con SQL Server Management Studio come una delle applicazioni ed è possibile eseguire come se fosse installato in computer con accesso tooAzure a SQL server.

Per ulteriori informazioni su come toomake hello tooSQL connessione Database, vedere [connettersi tooSQL Database con SQL Server Management Studio ed eseguire una query T-SQL di esempio](sql-database-connect-query-ssms.md).

È tutto per ora. Buon lavoro.

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png