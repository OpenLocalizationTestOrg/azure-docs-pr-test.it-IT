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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="a621b-103">Configurare SSL connettività in toosecurely l'applicazione connessione tooAzure Database MySQL</span><span class="sxs-lookup"><span data-stu-id="a621b-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="a621b-104">Il Database di Azure per MySQL supporta la connessione al Database di Azure per le applicazioni tooclient di MySQL server usando Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="a621b-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="a621b-105">Le connessioni SSL tra il server di database e applicazioni client di imposizione consente di proteggere da attacchi "man in intermedio hello" crittografando il flusso di dati hello tra server hello e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a621b-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="a621b-106">Passaggio 1: ottenere un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="a621b-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="a621b-107">Scaricare hello certificato necessario toocommunicate tramite SSL con il Database di Azure per il server MySQL da [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) e salvare hello tooyour file di certificato locale unità (in questa esercitazione, abbiamo utilizzato c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="a621b-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="a621b-108">**Per Microsoft Internet Explorer e Microsoft Edge:** dopo avere completato il download di hello, rinominare tooBaltimoreCyberTrustRoot.crt.pem certificato hello.</span><span class="sxs-lookup"><span data-stu-id="a621b-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="a621b-109">Passaggio 2: eseguire il binding SSL</span><span class="sxs-lookup"><span data-stu-id="a621b-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="a621b-110">Connessione tooserver utilizzando hello MySQL Workbench tramite SSL</span><span class="sxs-lookup"><span data-stu-id="a621b-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="a621b-111">Configurare tooconnect Workbench di MySQL in modo sicuro tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="a621b-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="a621b-112">Passare toohello **SSL** scheda hello Workbench di MySQL in hello finestra di dialogo di connessione di nuovo il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="a621b-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="a621b-113">Immettere il percorso di file hello di hello **BaltimoreCyberTrustRoot.crt.pem** in hello **File autorità di certificazione SSL:** campo.</span><span class="sxs-lookup"><span data-stu-id="a621b-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="a621b-114">![Salvare un riquadro personalizzato](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="a621b-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="a621b-115">Connessione tooserver utilizzo hello MySQL CLI su SSL</span><span class="sxs-lookup"><span data-stu-id="a621b-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="a621b-116">Utilizzando l'interfaccia della riga di comando di MySQL hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a621b-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="a621b-117">Passaggio 3: applicazione delle connessioni SSL in Azure</span><span class="sxs-lookup"><span data-stu-id="a621b-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="a621b-118">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a621b-118">Using Azure portal</span></span>
<span data-ttu-id="a621b-119">Utilizzando hello portale di Azure, visitare il Database di Azure per il server MySQL fare clic su **sicurezza della connessione**.</span><span class="sxs-lookup"><span data-stu-id="a621b-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="a621b-120">Utilizzare hello Attiva/Disattiva pulsante tooenable o disabilitare hello **connessione SSL applicare** impostazione.</span><span class="sxs-lookup"><span data-stu-id="a621b-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="a621b-121">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a621b-121">Then click **Save**.</span></span> <span data-ttu-id="a621b-122">Microsoft consiglia di abilitare tooalways **connessione SSL applicare** impostazione per una maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a621b-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="a621b-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="a621b-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="a621b-124">Utilizzare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a621b-124">Using Azure CLI</span></span>
<span data-ttu-id="a621b-125">È possibile abilitare o disabilitare hello **ssl imposizione** parametro con valori Enabled o Disabled rispettivamente in CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a621b-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="a621b-126">Passaggio 4: verificare la connessione SSL</span><span class="sxs-lookup"><span data-stu-id="a621b-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="a621b-127">Eseguire hello mysql **stato** tooverify comando che si è connessi tooyour MySQL server mediante SSL:</span><span class="sxs-lookup"><span data-stu-id="a621b-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="a621b-128">Verificare la connessione di hello è crittografata esaminando l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="a621b-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="a621b-129">Dovrebbe mostrare: **SSL: Cipher in use is AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="a621b-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="a621b-130">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="a621b-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="a621b-131">PHP</span><span class="sxs-lookup"><span data-stu-id="a621b-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="a621b-132">Python</span><span class="sxs-lookup"><span data-stu-id="a621b-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="a621b-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a621b-133">Next steps</span></span>
<span data-ttu-id="a621b-134">Esaminare varie opzioni di connettività dell'applicazione in [Raccolte di connessioni per Database di Azure per MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a621b-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
