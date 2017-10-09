---
title: "connettività SSL aaaConfigure nel Database di Azure per PostgreSQL | Documenti Microsoft"
description: Le istruzioni e informazioni tooconfigure Azure Database PostgreSQL relative applicazioni associate tooproperly utilizzare connessioni SSL.
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Configurare la connettività SSL nel Database di Azure per PostgreSQL
Il Database di Azure per PostgreSQL preferenziale per la connessione il toohello di applicazioni client del servizio PostgreSQL utilizzando Secure Sockets Layer (SSL). Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.

Per impostazione predefinita, il servizio di database PostgreSQL hello è toorequire configurato SSL. Facoltativamente, è possibile disabilitare richiedere SSL per la connessione del servizio di database tooyour se l'applicazione client non supporta la connettività SSL. 

## <a name="enforcing-ssl-connections"></a>Applicazione delle connessioni SSL
Per tutti i Database di Azure per i server PostgreSQL eseguito il provisioning tramite hello portale di Azure e CLI, per impostazione predefinita è attivata l'imposizione di connessioni SSL. 

Allo stesso modo, le stringhe di connessione predefinite nelle impostazioni di "Stringhe di connessione" hello del server di hello portale di Azure includono parametri hello necessario per il server database tooyour tooconnect linguaggi comuni mediante SSL. Hello parametro SSL varia in base al connettore hello, ad esempio "ssl = true" o "sslmode = richiedono" o "sslmode = obbligatorio" e altre varianti.

## <a name="configure-enforcement-of-ssl"></a>Configurare l'applicazione di SSL
Facoltativamente, è possibile disabilitare l'applicazione della connettività SSL. Microsoft Azure si consiglia di abilitare tooalways **connessione SSL applicare** impostazione per una maggiore sicurezza.

### <a name="using-hello-azure-portal"></a>Utilizzo di hello portale di Azure
Visitare il Database di Azure per il server PostgreSQL e fare clic su **Sicurezza connessione**. Utilizzare hello Attiva/Disattiva pulsante tooenable o disabilitare hello **connessione SSL applicare** impostazione. Fare quindi clic su **Salva**. 

![Sicurezza connessione - Disabilitare l'applicazione di SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

È possibile verificare l'impostazione di hello visualizzando hello **Panoramica** hello toosee pagina **SSL applicare stato** indicatore.

### <a name="using-azure-cli"></a>Utilizzare l'interfaccia della riga di comando di Azure
È possibile abilitare o disabilitare hello **ssl imposizione** parametro utilizzando `Enabled` o `Disabled` valori rispettivamente in CLI di Azure.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Verificare che le connessioni SSL siano supportate dall'applicazione o dal framework
Per impostazione predefinita, molti framework di applicazione comuni che usano i servizi PostgreSQL per database, quali Drupal e Django, non abilitano SSL durante l'installazione. Abilitazione della connettività SSL devono essere eseguita dopo l'installazione o tramite l'applicazione di toohello specifici comandi CLI. Se il server PostgreSQL consiste nell'imporre le connessioni SSL e un'applicazione hello associata non è configurata correttamente, un'applicazione hello potrebbe non riuscire a tooconnect tooyour server di database. Consultare toolearn documentazione dell'applicazione, come le connessioni SSL tooenable.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Applicazioni che richiedono la verifica del certificato per la connettività SSL
In alcuni casi, le applicazioni richiedono un file di certificato locale generato da un tooconnect (. cer) di certificati Autorità di certificazione (CA) attendibili in modo sicuro. Vedere i seguenti passaggi tooobtain hello. cer file hello, decodificare certificato hello e associarlo tooyour applicazione.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Scaricare il file di certificato hello da hello autorità di certificazione (CA) 
Hello certificato richiesto toocommunicate tramite SSL con il Database di Azure per cui si trova il server PostgreSQL [qui](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Scaricare i file del certificato hello localmente.

### <a name="download-and-install-openssl-on-your-machine"></a>Scaricare e installare OpenSSL sul computer 
file di certificato hello toodecode necessarie in modo sicuro per l'applicazione tooconnect tooyour server di database, è necessario tooinstall OpenSSL sul computer locale.

#### <a name="for-linux-os-x-or-unix"></a>Per Linux, OS X o Unix
librerie OpenSSL Hello vengono fornite nel codice sorgente direttamente da hello [OpenSSL Software Foundation](http://www.openssl.org). Hello istruzioni seguenti consentono di eseguire hello passaggi necessari tooinstall OpenSSL sul computer Linux. In questo articolo Usa comandi noti toowork in Ubuntu 12.04 e versioni successive.

Aprire una sessione terminal e installare OpenSSL
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Estrarre i file hello dal pacchetto di download hello
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Immettere la directory hello in cui sono stati estratti i file hello. Per impostazione predefinita, deve essere come segue.

```bash
cd openssl-1.1.0e
```
Configurare OpenSSL eseguendo hello comando seguente. Se si desidera file hello in una cartella diversa /usr/local/openssl, assicurarsi che toochange hello seguenti come appropriato.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Ora che OpenSSL sia configurato correttamente, è necessario toocompile è tooconvert il certificato. toocompile, eseguire hello comando seguente:

```bash
make
```
Una volta completata la compilazione, si è pronti tooinstall OpenSSL come eseguibile eseguendo hello comando seguente:
```bash
make install
```
tooconfirm che OpenSSL è stato installato correttamente nel sistema, comando hello esecuzione seguente, verificare che si ottiene hello toomake stesso output.

```bash
/usr/local/openssl/bin/openssl version
```
Se ha esito positivo dovrebbe segue messaggio hello.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Per Windows
L'installazione di OpenSSL nei PC Windows può essere eseguita in hello seguenti modi:
1. **(Scelta consigliata)**  Utilizzando hello funzionalità incorporata di barra rovesciata per Windows 10 finestra e versioni successive, OpenSSL è installato per impostazione predefinita. Istruzioni su come tooenable funzionalità Bash per Windows in Windows 10 è reperibile [qui](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. Tramite il download di un'applicazione Win32/64 bit fornita dalla community di hello. Mentre hello OpenSSL Software Foundation non fornisce né avalla eventuali programmi di installazione di Windows specifici, forniscono un elenco di programmi di installazione disponibili [qui](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Decodificare il file del certificato
Hello scaricati autorità di certificazione radice file è in formato crittografato. Utilizzare i file del certificato hello toodecode OpenSSL. toodo in tal caso, eseguire il comando OpenSSL:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>Per la connessione per PostgreSQL tooAzure Database con l'autenticazione del certificato SSL
Ora che si è decodificati correttamente il certificato, è ora possibile connettere il server di database tooyour a in modo sicuro tramite SSL. verifica del certificato server tooallow, hello certificato deve essere collocato in ~/.postgresql/root.crt file hello nella home directory dell'utente hello. (File di Microsoft Windows hello è denominato % APPDATA%\postgresql\root.crt.). esempio Hello vengono fornite istruzioni per la connessione di Database tooAzure per PostgreSQL.

> [!NOTE]
> Attualmente, è presente un problema noto se si utilizza "sslmode = verificare-full" in servizio, toohello connessione connessione hello avrà esito negativo con il seguente errore hello: _certificato server per "&lt;area&gt;. Control.database.Windows.NET"(e 7 altri nomi) non corrispondano il nome host"&lt;servername&gt;. postgres.database.azure.com "._
> Se "sslmode = verificare-full" è necessario, utilizzare convenzione di denominazione hello  **&lt;servername&gt;. database.windows.net** come nome host di stringa di connessione. Prevediamo tooremove questa limitazione in hello future. Le connessioni che utilizzano altri [modalità SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) deve continuare convenzione di denominazione host hello preferito toouse  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Uso dell'utilità della riga di comando PSQL
Hello di esempio seguente vengono illustrate le modalità di connessione tooyour PostgreSQL server utilizzando l'utilità della riga di comando di hello psql toosuccessfully. Hello utilizzare `root.crt` file creato e hello `sslmode=verify-ca` o `sslmode=verify-full` opzione.

Utilizzando l'interfaccia della riga di comando di hello PostgreSQL, eseguire hello comando seguente:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
Se ha esito positivo, verrà visualizzato hello seguente output:
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a>Uso dello strumento GUI pgAdmin
Per configurare tooconnect pgAdmin 4 in modo sicuro tramite SSL è necessario hello tooset `SSL mode = Verify-CA` o `SSL mode = Verify-Full` come indicato di seguito:

![Schermata di pgAdmin - connessione - modalità SSL richiesta](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Passaggi successivi
Esaminare varie opzioni di connettività dell'applicazione secondo [Raccolte connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)
