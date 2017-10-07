---
title: una media aaaCreate dello stack in una VM Linux di Azure | Documenti Microsoft
description: Informazioni su come Node.js (Media), Express, AngularJS e toocreate un MongoDB dello stack in una VM Linux in Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="cdd7c-103">Creare uno stack MongoDB, Express, AngularJS e Node.js (MEAN) in una VM Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="cdd7c-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="cdd7c-104">Questa esercitazione viene illustrato come Node.js (Media), Express, AngularJS e tooimplement un MongoDB dello stack in una VM Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="cdd7c-105">stack Hello medio creato consente l'aggiunta, eliminazione e l'elenco di libri in un database.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="cdd7c-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdd7c-107">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="cdd7c-107">Create a Linux VM</span></span>
> * <span data-ttu-id="cdd7c-108">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="cdd7c-108">Install Node.js</span></span>
> * <span data-ttu-id="cdd7c-109">MongoDB di installare e configurare server hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="cdd7c-110">Installare Express e configurare le route toohello server</span><span class="sxs-lookup"><span data-stu-id="cdd7c-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="cdd7c-111">Route di hello accesso con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cdd7c-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="cdd7c-112">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cdd7c-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cdd7c-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cdd7c-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cdd7c-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="cdd7c-116">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="cdd7c-116">Create a Linux VM</span></span>

<span data-ttu-id="cdd7c-117">Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando e creare una VM Linux con hello [creare vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="cdd7c-118">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="cdd7c-119">esempio Hello utilizza hello Azure CLI toocreate un gruppo di risorse denominato *myResourceGroupMEAN* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="cdd7c-120">Viene creata una VM denominata *myVM* con le chiavi SSH se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="cdd7c-121">toouse un set specifico di chiavi, utilizzare hello - opzione ssh-chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="cdd7c-122">Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="cdd7c-123">Prendere nota di hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="cdd7c-124">Questo indirizzo è utilizzato tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="cdd7c-125">Comando che segue di hello utilizzare toocreate una sessione SSH con hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="cdd7c-126">Assicurarsi che toouse hello corretto indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="cdd7c-127">Nell'esempio riportato sopra l'indirizzo IP era 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="cdd7c-128">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="cdd7c-128">Install Node.js</span></span>

<span data-ttu-id="cdd7c-129">[Node.js](https://nodejs.org/en/) è un runtime JavaScript basato sul motore V8 JavaScript di Chrome.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="cdd7c-130">Node.js è utilizzato in questa esercitazione tooset hello che instrada Express e il controller AngularJS.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="cdd7c-131">Nella macchina virtuale con shell bash hello che è stato aperto con SSH, hello installare Node.js.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="cdd7c-132">MongoDB di installare e configurare server hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="cdd7c-133">[MongoDB](http://www.mongodb.com) archivia i dati in documenti flessibili simili a JSON.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="cdd7c-134">I campi in un database possono variare da toodocument documento e struttura dei dati può essere modificata nel tempo.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="cdd7c-135">Per l'applicazione di esempio, si aggiungono book record tooMongoDB che contengono il nome libro, numero isbn, autore e numero di pagine.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="cdd7c-136">Nel hello macchina virtuale con shell bash hello che è stato aperto con SSH, impostare la chiave di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="cdd7c-137">Aggiornare Gestione pacchetti hello con chiave hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="cdd7c-138">Installare MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="cdd7c-139">Avviare server hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="cdd7c-140">È anche necessario hello tooinstall [corpo parser](https://www.npmjs.com/package/body-parser-json) toohelp pacchetto ci elaborare hello JSON passato server toohello richieste.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="cdd7c-141">Installare la gestione pacchetti npm hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="cdd7c-142">Installare il pacchetto di hello corpo parser.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="cdd7c-143">Creare una cartella denominata *documentazione* e aggiungere tooit un file denominato *server.js* che contiene la configurazione di hello per server web hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="cdd7c-144">Installare Express e configurare le route toohello server</span><span class="sxs-lookup"><span data-stu-id="cdd7c-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="cdd7c-145">[Express](https://expressjs.com) è un framework applicazione Web Node.js minimo e flessibile che fornisce funzionalità per le applicazioni Web e per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="cdd7c-146">Express viene utilizzato questo tooand di informazioni toopass esercitazione libro dal database MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="cdd7c-147">[Mongoose](http://mongoosejs.com) fornisce una soluzione semplice e basata sullo schema di toomodel i dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="cdd7c-148">Mongoose viene utilizzata in questa esercitazione tooprovide uno schema del libro per database hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="cdd7c-149">Installare Express e Mongoose.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="cdd7c-150">In hello *documentazione* cartella, creare una cartella denominata *app* e aggiungere un file denominato *routes.js* con hello express route definite.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="cdd7c-151">In hello *app* cartella, creare una cartella denominata *modelli* e aggiungere un file denominato *book.js* con configurazione del modello di libro hello definito.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="cdd7c-152">Route di hello accesso con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cdd7c-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="cdd7c-153">[AngularJS](https://angularjs.org) fornisce un framework Web per creare visualizzazioni dinamiche nelle applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="cdd7c-154">In questa esercitazione è utilizzare la pagina web di AngularJS tooconnect con Express e le azioni eseguibili dal database di libro.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="cdd7c-155">Modificare anche le directory hello backup*documentazione* (`cd ../..`), quindi creare una cartella denominata *pubblica* e aggiungere un file denominato *js* con controller hello configurazione definita.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="cdd7c-156">In hello *pubblica* cartella, creare un file denominato *index.html* con una pagina web hello definito.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="cdd7c-157">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-157">Run hello application</span></span>

1. <span data-ttu-id="cdd7c-158">Modificare anche le directory hello backup*documentazione* (`cd ..`) e avviare il server di hello eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="cdd7c-159">Aprire un browser toohello indirizzo registrato per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="cdd7c-160">Ad esempio: *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="cdd7c-161">Dovrebbe essere simile al seguente hello pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-161">You should see something like hello following page:</span></span>

    ![Record del libro](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="cdd7c-163">Immettere i dati in caselle di testo hello e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="cdd7c-164">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-164">For example:</span></span>

    ![Aggiungere il record di un libro](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="cdd7c-166">Dopo l'aggiornamento pagina hello, dovrebbe essere simile a questa pagina:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Elencare i record dei libro](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="cdd7c-168">È possibile fare clic **eliminare** e rimuovere i record della Rubrica hello dal database hello.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdd7c-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdd7c-169">Next steps</span></span>

<span data-ttu-id="cdd7c-170">In questa esercitazione si è creata un'applicazione Web che tiene traccia dei record dei libri usando uno stack MEAN in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="cdd7c-171">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="cdd7c-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cdd7c-172">Creare una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="cdd7c-172">Create a Linux VM</span></span>
> * <span data-ttu-id="cdd7c-173">Installare Node.js</span><span class="sxs-lookup"><span data-stu-id="cdd7c-173">Install Node.js</span></span>
> * <span data-ttu-id="cdd7c-174">MongoDB di installare e configurare server hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="cdd7c-175">Installare Express e configurare le route toohello server</span><span class="sxs-lookup"><span data-stu-id="cdd7c-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="cdd7c-176">Route di hello accesso con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cdd7c-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="cdd7c-177">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="cdd7c-177">Run hello application</span></span>

<span data-ttu-id="cdd7c-178">Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="cdd7c-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cdd7c-179">Secure web server with SSL (Proteggere il server Web con SSL)</span><span class="sxs-lookup"><span data-stu-id="cdd7c-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
