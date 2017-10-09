---
title: aaaCreate PHP-MySQL web app in Azure App Service e la distribuzione usando Git
description: Un'esercitazione che illustra come toocreate PHP web app che archivia i dati di MySQL e utilizzare tooAzure distribuzione Git.
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="889b0-103">Creazione di un'app Web PHP-MySQL in Servizio app di Azure e distribuzione tramite Git</span><span class="sxs-lookup"><span data-stu-id="889b0-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="889b0-104">Questa esercitazione Mostra l'app web toocreate PHP, MySQL e la modalità toodeploy è troppo[servizio App](http://go.microsoft.com/fwlink/?LinkId=529714) tramite Git.</span><span class="sxs-lookup"><span data-stu-id="889b0-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="889b0-105">Si utilizzerà [PHP][install-php], lo strumento da riga di comando di MySQL hello (parte di [MySQL][install-mysql]), e [Git] [ install-git] installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="889b0-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="889b0-106">istruzioni di Hello in questa esercitazione possono essere seguite su qualsiasi sistema operativo, tra cui Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="889b0-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="889b0-107">Dopo aver completato questa guida, si disporrà dell'app Web PHP/MySQL in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="889b0-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="889b0-108">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="889b0-108">You will learn:</span></span>

* <span data-ttu-id="889b0-109">Come toocreate un'app web e MySQL database utilizzando hello [portale Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="889b0-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="889b0-110">Perché PHP è abilitata in [App del servizio Web App](http://go.microsoft.com/fwlink/?LinkId=529714) per impostazione predefinita, niente di speciale è obbligatorio toorun codice PHP.</span><span class="sxs-lookup"><span data-stu-id="889b0-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="889b0-111">Come toopublish e pubblicare nuovamente l'applicazione tooAzure tramite Git.</span><span class="sxs-lookup"><span data-stu-id="889b0-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="889b0-112">Modalità tooenable hello Composer estensione tooautomate Composer attività in ogni `git push`.</span><span class="sxs-lookup"><span data-stu-id="889b0-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="889b0-113">Seguendo questa esercitazione, verrà creata una semplice app Web di registrazione in PHP,</span><span class="sxs-lookup"><span data-stu-id="889b0-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="889b0-114">verrà ospitata l'applicazione Hello nelle App Web.</span><span class="sxs-lookup"><span data-stu-id="889b0-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="889b0-115">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="889b0-115">A screenshot of hello completed application is below:</span></span>

![Sito Web PHP di Azure][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="889b0-117">Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="889b0-117">Set up hello development environment</span></span>
<span data-ttu-id="889b0-118">Questa esercitazione presuppone l'esistenza [PHP][install-php], hello lo strumento da riga di comando di MySQL (parte di [MySQL][install-mysql]), e [Git] [ install-git] installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="889b0-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="889b0-119">Creare un'app Web e configurare la pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="889b0-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="889b0-120">Seguire questi passaggi toocreate un'app web e un database MySQL:</span><span class="sxs-lookup"><span data-stu-id="889b0-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="889b0-121">Account di accesso toohello [portale Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="889b0-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="889b0-122">Fare clic su hello **New** icona.</span><span class="sxs-lookup"><span data-stu-id="889b0-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="889b0-123">Fare clic su **vedere tutti** Avanti troppo**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="889b0-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="889b0-124">Fare clic su **Web e dispositivi mobili**, quindi su **App Web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="889b0-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="889b0-125">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="889b0-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="889b0-126">Immettere un nome valido per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="889b0-126">Enter a valid name for your resource group.</span></span>
   
    ![Gruppo di risorse denominato ADF.][resource-group]
6. <span data-ttu-id="889b0-128">Immettere i valori per la nuova app Web.</span><span class="sxs-lookup"><span data-stu-id="889b0-128">Enter values for your new web app.</span></span>
   
    ![Crea app Web][new-web-app]
7. <span data-ttu-id="889b0-130">Immettere i valori per il nuovo database, tra cui accettano toohello legali.</span><span class="sxs-lookup"><span data-stu-id="889b0-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Creazione di un nuovo database MySQL][new-mysql-db]
8. <span data-ttu-id="889b0-132">Quando hello web app è stata creata, verrà visualizzato il pannello nuova web app hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="889b0-133">In **Impostazioni** fare clic su **Distribuzione continua**, poi fare clic su *Configura le impostazioni necessarie*.</span><span class="sxs-lookup"><span data-stu-id="889b0-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configurazione della pubblicazione Git][setup-publishing]
10. <span data-ttu-id="889b0-135">Selezionare **Git Repository locale** per origine hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Impostare i repository Git][setup-repository]
11. <span data-ttu-id="889b0-137">tooenable Git pubblicazione, è necessario fornire un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="889b0-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="889b0-138">Prendere nota del nome utente hello e la password creata.</span><span class="sxs-lookup"><span data-stu-id="889b0-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="889b0-139">Se è stato configurato un repository Git in precedenza, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="889b0-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Creazione di credenziali di pubblicazione][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="889b0-141">Recupero di informazioni sulla connessione remota a MySQL</span><span class="sxs-lookup"><span data-stu-id="889b0-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="889b0-142">database MySQL tooconnect toohello in cui è in esecuzione in applicazioni Web, sarà necessario hello informazioni di connessione.</span><span class="sxs-lookup"><span data-stu-id="889b0-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="889b0-143">tooget informazioni di connessione MySQL, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="889b0-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="889b0-144">Il gruppo di risorse, fare clic su database hello:</span><span class="sxs-lookup"><span data-stu-id="889b0-144">From your resource group, click hello database:</span></span>
   
    ![Selezionare il database][select-database]
2. <span data-ttu-id="889b0-146">Da database hello **impostazioni**selezionare **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="889b0-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Selezionare le proprietà][select-properties]
3. <span data-ttu-id="889b0-148">Prendere nota dei valori di hello per `Database`, `Host`, `User Id`, e `Password`.</span><span class="sxs-lookup"><span data-stu-id="889b0-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Proprietà nota][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="889b0-150">Creare e verificare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="889b0-150">Build and test your app locally</span></span>
<span data-ttu-id="889b0-151">Una volta creata l'app Web, è possibile sviluppare localmente l'applicazione, quindi distribuirla dopo il test.</span><span class="sxs-lookup"><span data-stu-id="889b0-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="889b0-152">applicazione di registrazione Hello è una semplice applicazione PHP che consente di tooregister per un evento, fornendo il nome e l'indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="889b0-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="889b0-153">Le informazioni sui registranti precedenti vengono visualizzate in una tabella.</span><span class="sxs-lookup"><span data-stu-id="889b0-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="889b0-154">Le informazioni sulle registrazioni vengono archiviate in un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="889b0-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="889b0-155">un'applicazione Hello è costituito da un file (copiare e incollare codice riportato di seguito):</span><span class="sxs-lookup"><span data-stu-id="889b0-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="889b0-156">**index.php**: consente di visualizzare un modulo per la registrazione e una tabella contenente informazioni sui registranti.</span><span class="sxs-lookup"><span data-stu-id="889b0-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="889b0-157">toobuild e in locale, un'applicazione hello esecuzione procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="889b0-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="889b0-158">Si noti che questi passaggi presuppongono che si dispone di hello PHP e MySQL strumento della riga di comando (parte di MySQL) impostare sul computer locale, e che è stata attivata hello [estensione PDO per MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="889b0-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="889b0-159">Connettersi toohello MySQL server remoto, utilizzando il valore di hello per `Data Source`, `User Id`, `Password`, e `Database` recuperato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="889b0-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="889b0-160">verranno visualizzati prompt dei comandi di Hello MySQL:</span><span class="sxs-lookup"><span data-stu-id="889b0-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="889b0-161">Incolla in seguito hello `CREATE TABLE` comando toocreate hello `registration_tbl` tabella del database:</span><span class="sxs-lookup"><span data-stu-id="889b0-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="889b0-162">Nella directory radice della cartella dell'applicazione locale hello creare **index.php** file.</span><span class="sxs-lookup"><span data-stu-id="889b0-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="889b0-163">Aprire hello **index.php** file in un editor di testo o un IDE e aggiungere hello seguente di codice e le modifiche necessarie hello completa è contrassegnato con `//TODO:` commenti.</span><span class="sxs-lookup"><span data-stu-id="889b0-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="889b0-164">In un terminal tooyour passare applicazione cartella e il tipo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="889b0-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="889b0-165">È possibile cercare troppo**http://localhost:8000/servicemodelsamples/Service /** tootest un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="889b0-166">Pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="889b0-166">Publish your app</span></span>
<span data-ttu-id="889b0-167">Dopo aver testato l'app localmente, è possibile pubblicare le app tooWeb tramite Git.</span><span class="sxs-lookup"><span data-stu-id="889b0-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="889b0-168">Verrà inizializzare il repository Git locale e pubblicare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="889b0-169">Questi sono hello stessi passaggi illustrati in hello Set e il portale di Azure alla fine hello hello crea un'app web di pubblicazione Git sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="889b0-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="889b0-170">(Facoltativo)  Se è stato dimenticato o erroneamente posizionato l'URL remoto repostitory Git, è possibile passare toohello proprietà dell'app web nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="889b0-171">Aprire GitBash (o un terminale, se si trova in Git il `PATH`), modificare le directory toohello radice directory dell'applicazione ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="889b0-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="889b0-172">Verrà richiesto di hello password creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="889b0-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![TooAzure Push iniziale tramite Git][git-initial-push]
3. <span data-ttu-id="889b0-174">Sfoglia troppo**http://[site name].azurewebsites.net/index.php** toobegin utilizzando un'applicazione hello (queste informazioni verranno archiviate nel dashboard account):</span><span class="sxs-lookup"><span data-stu-id="889b0-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Sito Web PHP di Azure][running-app]

<span data-ttu-id="889b0-176">Dopo aver pubblicato l'applicazione, è possibile iniziare a creare tooit modifiche e utilizzare Git toopublish li.</span><span class="sxs-lookup"><span data-stu-id="889b0-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="889b0-177">Pubblicare app tooyour modifiche</span><span class="sxs-lookup"><span data-stu-id="889b0-177">Publish changes tooyour app</span></span>
<span data-ttu-id="889b0-178">toopublish modifiche tooyour app, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="889b0-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="889b0-179">Rendere l'app tooyour modifiche localmente.</span><span class="sxs-lookup"><span data-stu-id="889b0-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="889b0-180">Aprire GitBash (o un terminale, it Git è il `PATH`), modificare le directory toohello radice directory dell'app ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="889b0-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="889b0-181">Verrà richiesto di hello password creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="889b0-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Push tooAzure di modifiche del sito tramite Git][git-change-push]
3. <span data-ttu-id="889b0-183">Sfoglia troppo**http://[site name].azurewebsites.net/index.php** toosee l'app e le eventuali modifiche apportate:</span><span class="sxs-lookup"><span data-stu-id="889b0-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Sito Web PHP di Azure][running-app]

> [!NOTE]
> <span data-ttu-id="889b0-185">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="889b0-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="889b0-186">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="889b0-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="889b0-187">Abilitare l'automazione Composer con estensione Composer hello</span><span class="sxs-lookup"><span data-stu-id="889b0-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="889b0-188">Per impostazione predefinita, processo di distribuzione git hello nel servizio App non esegue alcuna operazione con composer.json, se presente nel progetto PHP.</span><span class="sxs-lookup"><span data-stu-id="889b0-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="889b0-189">È possibile abilitare composer.json durante l'elaborazione di `git push` abilitando l'estensione Composer hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="889b0-190">Nel PHP web pannello dell'app in hello [portale di Azure][management-portal], fare clic su **strumenti** > **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="889b0-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Impostazioni dell'estensione Compositore][composer-extension-settings]
2. <span data-ttu-id="889b0-192">Fare clic su **Aggiungi**, quindi su **Compositore**.</span><span class="sxs-lookup"><span data-stu-id="889b0-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Aggiunta dell'estensione Compositore][composer-extension-add]
3. <span data-ttu-id="889b0-194">Fare clic su **OK** tooaccept legali.</span><span class="sxs-lookup"><span data-stu-id="889b0-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="889b0-195">Fare clic su **OK** nuovamente tooadd estensione di hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="889b0-196">Hello **estensioni installate** pannello verrà visualizzati estensione Composer hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="889b0-197">![Visualizzazione dell'estensione Compositore][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="889b0-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="889b0-198">A questo punto, eseguire `git add`, `git commit`, e `git push` come nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="889b0-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="889b0-199">Si noterà che ora Composer installa le dipendenze definite in composer.json.</span><span class="sxs-lookup"><span data-stu-id="889b0-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Estensione Compositore - Esito positivo][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="889b0-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="889b0-201">Next steps</span></span>
<span data-ttu-id="889b0-202">Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="889b0-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
