---
title: Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git
description: Un'esercitazione in cui viene illustrato come creare un'app Web PHP che archivia i dati in MySQL e come utilizzare la distribuzione Git in Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="ca3f6-103">Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git</span><span class="sxs-lookup"><span data-stu-id="ca3f6-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="ca3f6-104">In questa esercitazione viene illustrato come creare un'app Web PHP-MySQL e come distribuirla in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tramite Git.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="ca3f6-105">Si useranno [PHP][install-php], lo strumento da riga di comando MySQL (che fa parte di [MySQL][install-mysql]) e [Git][install-git] installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="ca3f6-106">Le istruzioni di questa esercitazione possono essere eseguite in qualsiasi sistema operativo, tra cui Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="ca3f6-107">Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="ca3f6-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-108">You will learn:</span></span>

* <span data-ttu-id="ca3f6-109">Come creare un'app Web e un database MySQL mediante il [portale di Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="ca3f6-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="ca3f6-110">Poiché PHP è abilitato nelle [app Web di Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) per impostazione predefinita, non è necessario effettuare operazioni particolari per eseguire il codice PHP.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="ca3f6-111">Pubblicare e ripubblicare l'applicazione in Azure tramite Git.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="ca3f6-112">Come abilitare l'estensione Compositore e automatizzarne le attività per ogni `git push`.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="ca3f6-113">Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="ca3f6-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="ca3f6-114">che verrà ospitata nelle app Web.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="ca3f6-115">Di seguito è riportata una schermata dell'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-115">A screenshot of the completed application is below:</span></span>

![Sito Web PHP di Azure][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="ca3f6-117">Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="ca3f6-117">Set up the development environment</span></span>
<span data-ttu-id="ca3f6-118">In questa esercitazione si presuppone che [PHP][install-php], lo strumento da riga di comando MySQL (parte di [MySQL][install-mysql]) e [Git][install-git] siano installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="ca3f6-119">Creare un'app Web e configurare la pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="ca3f6-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="ca3f6-120">Per creare un'app Web e un database MySQL, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="ca3f6-121">Eseguire l'accesso al [portale di Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="ca3f6-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="ca3f6-122">Fare clic sull'icona **Nuovo** .</span><span class="sxs-lookup"><span data-stu-id="ca3f6-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="ca3f6-123">Fare clic su **Visualizza tutto** accanto a **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="ca3f6-124">Fare clic su **Web e dispositivi mobili**, quindi su **App Web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="ca3f6-125">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="ca3f6-126">Immettere un nome valido per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-126">Enter a valid name for your resource group.</span></span>
   
    ![Gruppo di risorse denominato ADF.][resource-group]
6. <span data-ttu-id="ca3f6-128">Immettere i valori per la nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-128">Enter values for your new web app.</span></span>
   
    ![Crea app Web][new-web-app]
7. <span data-ttu-id="ca3f6-130">Immettere i valori per il nuovo database e accettare termini e condizioni.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
8. <span data-ttu-id="ca3f6-132">Una volta creata l'app Web, verrà visualizzato il pannello del nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="ca3f6-133">In **Impostazioni** fare clic su **Distribuzione continua**, poi fare clic su *Configura le impostazioni necessarie*.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configurazione della pubblicazione Git][setup-publishing]
10. <span data-ttu-id="ca3f6-135">Selezionare **Repository Git locale** per l'origine.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Impostare i repository Git][setup-repository]
11. <span data-ttu-id="ca3f6-137">Per abilitare la pubblicazione Git, è necessario specificare un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="ca3f6-138">Prendere nota del nome utente e della password creati.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="ca3f6-139">Se è stato configurato un repository Git in precedenza, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Creazione di credenziali di pubblicazione][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="ca3f6-141">Recupero di informazioni sulla connessione remota a MySQL</span><span class="sxs-lookup"><span data-stu-id="ca3f6-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="ca3f6-142">Per connettersi al database MySQL in esecuzione in App Web, saranno necessarie le informazioni sulla connessione.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="ca3f6-143">Per recuperare le informazioni sulla connessione a MySQL, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="ca3f6-144">Dal gruppo di risorse, fare clic sul database:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-144">From your resource group, click the database:</span></span>
   
    ![Selezionare il database][select-database]
2. <span data-ttu-id="ca3f6-146">Dalle **Impostazioni** del database, selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Selezionare le proprietà][select-properties]
3. <span data-ttu-id="ca3f6-148">Prendere nota dei valori di `Database`, `Host`, `User Id` e `Password`.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Proprietà nota][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="ca3f6-150">Creare e verificare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="ca3f6-150">Build and test your app locally</span></span>
<span data-ttu-id="ca3f6-151">Una volta creata l'app Web, è possibile sviluppare localmente l'applicazione, quindi distribuirla dopo il test.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="ca3f6-152">L'applicazione di registrazione è una semplice applicazione PHP che consente di registrarsi per un evento specificando il proprio nome e l'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="ca3f6-153">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="ca3f6-154">Le informazioni sulle registrazioni vengono archiviate in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="ca3f6-155">L'applicazione è costituita da un unico file (copiare e incollare il codice disponibile di seguito):</span><span class="sxs-lookup"><span data-stu-id="ca3f6-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="ca3f6-156">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="ca3f6-157">Per creare ed eseguire l'applicazione in locale, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="ca3f6-158">Si noti che per questi passaggi si presuppone che PHP e lo strumento da riga di comando MySQL (parte di MySQL) siano configurati nel computer locale e che l'[estensione PDO per MySQL][pdo-mysql] sia stata abilitata.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="ca3f6-159">Connettersi al server MySQL remoto usando i valori di `Data Source`, `User Id`, `Password` e `Database` recuperati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="ca3f6-160">Verrà visualizzato il prompt dei comandi MySQL:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="ca3f6-161">Incollare il comando `CREATE TABLE` seguente per creare la tabella `registration_tbl` nel database:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="ca3f6-162">Nella radice della cartella dell'applicazione locale creare il file **index.php** .</span><span class="sxs-lookup"><span data-stu-id="ca3f6-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="ca3f6-163">Aprire il file **index.php** in un editor di testo o in un IDE e aggiungere il codice seguente, quindi completare le necessarie modifiche contrassegnate con commenti `//TODO:`.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
            if(!empty($_POST)) {
            try {
                $name = $_POST['name'];
                $email = $_POST['email'];
                $date = date("Y-m-d");
                // Insert data
                $sql_insert = "INSERT INTO registration_tbl (name, email, date)
                           VALUES (?,?,?)";
                $stmt = $conn->prepare($sql_insert);
                $stmt->bindValue(1, $name);
                $stmt->bindValue(2, $email);
                $stmt->bindValue(3, $date);
                $stmt->execute();
            }
            catch(Exception $e) {
                die(var_dump($e));
            }
            echo "<h3>Your're registered!</h3>";
            }
            // Retrieve data
            $sql_select = "SELECT * FROM registration_tbl";
            $stmt = $conn->query($sql_select);
            $registrants = $stmt->fetchAll();
            if(count($registrants) > 0) {
                echo "<h2>People who are registered:</h2>";
                echo "<table>";
                echo "<tr><th>Name</th>";
                echo "<th>Email</th>";
                echo "<th>Date</th></tr>";
                foreach($registrants as $registrant) {
                    echo "<tr><td>".$registrant['name']."</td>";
                    echo "<td>".$registrant['email']."</td>";
                    echo "<td>".$registrant['date']."</td></tr>";
                }
                 echo "</table>";
            } else {
                echo "<h3>No one is currently registered.</h3>";
            }
        ?>
        </body>
        </html>

1. <span data-ttu-id="ca3f6-164">In un terminale passare alla cartella dell'applicazione e digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="ca3f6-165">A questo punto è possibile passare a **http://localhost:8000/** per testare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="ca3f6-166">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="ca3f6-166">Publish your app</span></span>
<span data-ttu-id="ca3f6-167">Dopo aver testato l'app in locale, è possibile pubblicarla su App Web tramite Git.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="ca3f6-168">Inizializzare l'archivio Git locale e pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ca3f6-169">Questi passaggi sono uguali a quelli illustrati nel portale di Azure alla fine della precedente sezione Creare un'app Web e configurare la pubblicazione Git.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="ca3f6-170">(Facoltativo) Se l'URL del repository remoto Git è stato dimenticato o smarrito, passare alle proprietà dell'app Web nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="ca3f6-171">Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'applicazione ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="ca3f6-172">Verrà richiesto di specificare la password creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Push iniziale in Azure tramite Git][git-initial-push]
3. <span data-ttu-id="ca3f6-174">Passare a **http://[nome sito].azurewebsites.net/index.php** per iniziare a usare l'applicazione. Queste informazioni verranno archiviate nel dashboard dell'account:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Sito Web PHP di Azure][running-app]

<span data-ttu-id="ca3f6-176">Dopo aver pubblicato l'app, è possibile iniziare ad apportarvi modifiche e ad usare Git per pubblicarle.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="ca3f6-177">Pubblicare le modifiche apportate all'app</span><span class="sxs-lookup"><span data-stu-id="ca3f6-177">Publish changes to your app</span></span>
<span data-ttu-id="ca3f6-178">Per pubblicare le modifiche appportate all'app, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="ca3f6-179">Apportare le modifiche all'app localmente.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="ca3f6-180">Aprire GitBash (o un terminale, se Git si trova in `PATH`), passare alla directory radice dell'app e eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="ca3f6-181">Verrà richiesto di specificare la password creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Push delle modifiche del sito apportate in Azure tramite Git][git-change-push]
3. <span data-ttu-id="ca3f6-183">Passare a **http://[nome sito].azurewebsites.net/index.php** per visualizzare l'app e le eventuali modifiche apportate:</span><span class="sxs-lookup"><span data-stu-id="ca3f6-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Sito Web PHP di Azure][running-app]

> [!NOTE]
> <span data-ttu-id="ca3f6-185">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ca3f6-186">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="ca3f6-187">Abilitare l'automazione Composer con l'estensione Composer</span><span class="sxs-lookup"><span data-stu-id="ca3f6-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="ca3f6-188">Per impostazione predefinita, il processo di distribuzione git nel servizio app non esegue operazioni relative a composer.json, se questo è presente nel progetto PHP.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="ca3f6-189">È possibile abilitare l'elaborazione di composer.json durante l'operazione di `git push` abilitando l'estensione Compositore.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="ca3f6-190">Nel pannello dell'app Web PHP nel [portale di Azure][management-portal] fare clic su **Strumenti** > **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Impostazioni dell'estensione Compositore][composer-extension-settings]
2. <span data-ttu-id="ca3f6-192">Fare clic su **Aggiungi**, quindi su **Compositore**.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Aggiunta dell'estensione Compositore][composer-extension-add]
3. <span data-ttu-id="ca3f6-194">Fare clic su **OK** per accettare le note legali.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="ca3f6-195">Fare di nuovo clic su **OK** per aggiungere l'estensione.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="ca3f6-196">Nel pannello **Estensioni installate** è ora visualizzata l'estensione Compositore.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="ca3f6-197">![Visualizzazione dell'estensione Compositore][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="ca3f6-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="ca3f6-198">Eseguire ora `git add`, `git commit` e `git push` come nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="ca3f6-199">Si noterà che ora Composer installa le dipendenze definite in composer.json.</span><span class="sxs-lookup"><span data-stu-id="ca3f6-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Estensione Compositore - Esito positivo][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="ca3f6-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca3f6-201">Next steps</span></span>
<span data-ttu-id="ca3f6-202">Per ulteriori informazioni, vedere il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="ca3f6-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
