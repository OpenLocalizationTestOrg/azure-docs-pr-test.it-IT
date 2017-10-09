---
title: "aaaConfigure SSL connettività toosecurely la connessione tooAzure Database MySQL | Documenti Microsoft"
description: Le istruzioni per come tooproperly Configura Database di Azure per MySQL e le applicazioni associate toocorrectly utilizzano connessioni SSL
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Configurare SSL connettività in toosecurely l'applicazione connessione tooAzure Database MySQL
Il Database di Azure per MySQL supporta la connessione al Database di Azure per le applicazioni tooclient di MySQL server usando Secure Sockets Layer (SSL). Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.

## <a name="step-1-obtain-ssl-certificate"></a>Passaggio 1: ottenere un certificato SSL
Scaricare hello certificato necessario toocommunicate tramite SSL con il Database di Azure per il server MySQL da [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) e salvare hello tooyour file di certificato locale unità (in questa esercitazione, abbiamo utilizzato c:\ssl).
**Per Microsoft Internet Explorer e Microsoft Edge:** dopo avere completato il download di hello, rinominare tooBaltimoreCyberTrustRoot.crt.pem certificato hello.

## <a name="step-2-bind-ssl"></a>Passaggio 2: eseguire il binding SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Connessione tooserver utilizzando hello MySQL Workbench tramite SSL
Configurare tooconnect Workbench di MySQL in modo sicuro tramite SSL. Passare toohello **SSL** scheda hello Workbench di MySQL in hello finestra di dialogo di connessione di nuovo il programma di installazione. Immettere il percorso di file hello di hello **BaltimoreCyberTrustRoot.crt.pem** in hello **File autorità di certificazione SSL:** campo.
![Salvare un riquadro personalizzato](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Connessione tooserver utilizzo hello MySQL CLI su SSL
Utilizzando l'interfaccia della riga di comando di MySQL hello, eseguire hello comando seguente:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Passaggio 3: applicazione delle connessioni SSL in Azure 
### <a name="using-azure-portal"></a>Uso del portale di Azure
Utilizzando hello portale di Azure, visitare il Database di Azure per il server MySQL fare clic su **sicurezza della connessione**. Utilizzare hello Attiva/Disattiva pulsante tooenable o disabilitare hello **connessione SSL applicare** impostazione. Fare quindi clic su **Salva**. Microsoft consiglia di abilitare tooalways **connessione SSL applicare** impostazione per una maggiore sicurezza.
![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Utilizzare l'interfaccia della riga di comando di Azure
È possibile abilitare o disabilitare hello **ssl imposizione** parametro con valori Enabled o Disabled rispettivamente in CLI di Azure.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Passaggio 4: verificare la connessione SSL
Eseguire hello mysql **stato** tooverify comando che si è connessi tooyour MySQL server mediante SSL:
```dos
mysql> status
```
Verificare la connessione di hello è crittografata esaminando l'output di hello. Dovrebbe mostrare: **SSL: Cipher in use is AES256-SHA** 

## <a name="sample-code"></a>Codice di esempio
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Passaggi successivi
Esaminare varie opzioni di connettività dell'applicazione in [Raccolte di connessioni per Database di Azure per MySQL](concepts-connection-libraries.md)
