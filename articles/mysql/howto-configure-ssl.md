---
title: "Configurare la connettività SSL per la connessione sicura a Database di Azure per MySQL | Microsoft Docs"
description: Istruzioni per la configurazione di Database di Azure per MySQL e delle applicazioni associate per usare correttamente le connessioni SSL
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 77e1b6266a2cf47949fa06358ec003f6b6b38065
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ssl-connectivity-in-your-application-to-securely-connect-to-azure-database-for-mysql"></a><span data-ttu-id="85173-103">Configurare la connettività SSL nell'applicazione per la connessione sicura a Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="85173-103">Configure SSL connectivity in your application to securely connect to Azure Database for MySQL</span></span>
<span data-ttu-id="85173-104">Database di Azure per il server MySQL supporta la connessione alle applicazioni client tramite Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="85173-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="85173-105">L'applicazione delle connessioni SSL tra il server di database e le applicazioni client aiuta a proteggersi dagli attacchi "man in the middle" crittografando il flusso di dati tra il server e l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="85173-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="85173-106">Passaggio 1: ottenere un certificato SSL</span><span class="sxs-lookup"><span data-stu-id="85173-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="85173-107">Scaricare il certificato necessario per comunicare tramite SSL con Database di Azure per il server MySQL da [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) e salvare il file del certificato nel disco locale (in questa esercitazione, abbiamo usato c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="85173-107">Download the certificate needed to communicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save the certificate file to your local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="85173-108">**Per Microsoft Internet Explorer e Microsoft Edge:** una volta completato il download, rinominare il certificato in BaltimoreCyberTrustRoot.crt.pem.</span><span class="sxs-lookup"><span data-stu-id="85173-108">**For Microsoft Internet Explorer and Microsoft Edge:** After the download has completed, rename the certificate to BaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="85173-109">Passaggio 2: eseguire il binding SSL</span><span class="sxs-lookup"><span data-stu-id="85173-109">Step 2: Bind SSL</span></span>
### <a name="connecting-to-server-using-the-mysql-workbench-over-ssl"></a><span data-ttu-id="85173-110">Connessione al server con MySQL Workbench tramite SSL</span><span class="sxs-lookup"><span data-stu-id="85173-110">Connecting to server using the MySQL Workbench over SSL</span></span>
<span data-ttu-id="85173-111">Configurare MySQL Workbench per connettersi in modo sicuro tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="85173-111">Configure MySQL Workbench to connect securely over SSL.</span></span> <span data-ttu-id="85173-112">Passare alla scheda **SSL** nella finestra di dialogo Setup New Connection (Configura nuova connessione) di MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="85173-112">Navigate to the **SSL** tab in the MySQL Workbench on the Setup New Connection dialogue.</span></span> <span data-ttu-id="85173-113">Immettere il percorso del file **BaltimoreCyberTrustRoot.crt.pem** nel campo **SSL CA File:** (File CA SSL:).</span><span class="sxs-lookup"><span data-stu-id="85173-113">Enter the file location of the **BaltimoreCyberTrustRoot.crt.pem** in the **SSL CA File:** field.</span></span>
<span data-ttu-id="85173-114">![Salvare un riquadro personalizzato](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="85173-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-to-server-using-the-mysql-cli-over-ssl"></a><span data-ttu-id="85173-115">Connessione al server con l'interfaccia della riga di comando di MySQL tramite SSL</span><span class="sxs-lookup"><span data-stu-id="85173-115">Connecting to server using the MySQL CLI over SSL</span></span>
<span data-ttu-id="85173-116">Usando l'interfaccia della riga di comando di MySQL, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="85173-116">Using the MySQL command-line interface, execute the following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="85173-117">Passaggio 3: applicazione delle connessioni SSL in Azure</span><span class="sxs-lookup"><span data-stu-id="85173-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="85173-118">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="85173-118">Using Azure portal</span></span>
<span data-ttu-id="85173-119">Usando il portale di Azure, passare all'istanza di Database di Azure per il server MySQL e fare clic su **Sicurezza delle connessioni**.</span><span class="sxs-lookup"><span data-stu-id="85173-119">Using the Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="85173-120">Usare l'interruttore per abilitare o disabilitare l'impostazione **Imponi connessione SSL**.</span><span class="sxs-lookup"><span data-stu-id="85173-120">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="85173-121">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="85173-121">Then click **Save**.</span></span> <span data-ttu-id="85173-122">Microsoft consiglia di abilitare sempre l'impostazione **Imponi connessione SSL** per maggiore sicurezza.</span><span class="sxs-lookup"><span data-stu-id="85173-122">Microsoft recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="85173-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="85173-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="85173-124">Utilizzare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="85173-124">Using Azure CLI</span></span>
<span data-ttu-id="85173-125">È possibile abilitare o disabilitare il parametro **ssl-enforcement** usando rispettivamente i valori Enabled o Disabled nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="85173-125">You can enable or disable the **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="85173-126">Passaggio 4: verificare la connessione SSL</span><span class="sxs-lookup"><span data-stu-id="85173-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="85173-127">Eseguire il comando mysql **status** per verificare di essere connessi al server MySQL tramite SSL:</span><span class="sxs-lookup"><span data-stu-id="85173-127">Execute the mysql **status** command to verify that you have connected to your MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="85173-128">Verificare che la connessione sia crittografata esaminando l'output.</span><span class="sxs-lookup"><span data-stu-id="85173-128">Confirm the connection is encrypted by reviewing the output.</span></span> <span data-ttu-id="85173-129">Dovrebbe mostrare: **SSL: Cipher in use is AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="85173-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="85173-130">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="85173-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="85173-131">PHP</span><span class="sxs-lookup"><span data-stu-id="85173-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="85173-132">Python</span><span class="sxs-lookup"><span data-stu-id="85173-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="85173-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85173-133">Next steps</span></span>
<span data-ttu-id="85173-134">Esaminare varie opzioni di connettività dell'applicazione in [Raccolte di connessioni per Database di Azure per MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="85173-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
