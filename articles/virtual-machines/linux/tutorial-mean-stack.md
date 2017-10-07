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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Creare uno stack MongoDB, Express, AngularJS e Node.js (MEAN) in una VM Linux in Azure

Questa esercitazione viene illustrato come Node.js (Media), Express, AngularJS e tooimplement un MongoDB dello stack in una VM Linux in Azure. stack Hello medio creato consente l'aggiunta, eliminazione e l'elenco di libri in un database. Si apprenderà come:

> [!div class="checklist"]
> * Creare una macchina virtuale Linux
> * Installare Node.js
> * MongoDB di installare e configurare server hello
> * Installare Express e configurare le route toohello server
> * Route di hello accesso con AngularJS
> * Eseguire un'applicazione hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Creare una macchina virtuale Linux

Creare un gruppo di risorse con hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando e creare una VM Linux con hello [creare vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.

esempio Hello utilizza hello Azure CLI toocreate un gruppo di risorse denominato *myResourceGroupMEAN* in hello *eastus* percorso. Viene creata una VM denominata *myVM* con le chiavi SSH se non esistono già in una posizione predefinita. toouse un set specifico di chiavi, utilizzare hello - opzione ssh-chiave-valore.

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

Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente: 

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
Prendere nota di hello `publicIpAddress`. Questo indirizzo è utilizzato tooaccess hello macchina virtuale.

Comando che segue di hello utilizzare toocreate una sessione SSH con hello macchina virtuale. Assicurarsi che toouse hello corretto indirizzo IP pubblico. Nell'esempio riportato sopra l'indirizzo IP era 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Installare Node.js

[Node.js](https://nodejs.org/en/) è un runtime JavaScript basato sul motore V8 JavaScript di Chrome. Node.js è utilizzato in questa esercitazione tooset hello che instrada Express e il controller AngularJS.

Nella macchina virtuale con shell bash hello che è stato aperto con SSH, hello installare Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>MongoDB di installare e configurare server hello
[MongoDB](http://www.mongodb.com) archivia i dati in documenti flessibili simili a JSON. I campi in un database possono variare da toodocument documento e struttura dei dati può essere modificata nel tempo. Per l'applicazione di esempio, si aggiungono book record tooMongoDB che contengono il nome libro, numero isbn, autore e numero di pagine. 

1. Nel hello macchina virtuale con shell bash hello che è stato aperto con SSH, impostare la chiave di MongoDB hello.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Aggiornare Gestione pacchetti hello con chiave hello.
  
    ```bash
    sudo apt-get update
    ```

3. Installare MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Avviare server hello.

    ```bash
    sudo service mongodb start
    ```

5. È anche necessario hello tooinstall [corpo parser](https://www.npmjs.com/package/body-parser-json) toohelp pacchetto ci elaborare hello JSON passato server toohello richieste.

    Installare la gestione pacchetti npm hello.

    ```bash
    sudo apt-get install npm
    ```

    Installare il pacchetto di hello corpo parser.
    
    ```bash
    sudo npm install body-parser
    ```

6. Creare una cartella denominata *documentazione* e aggiungere tooit un file denominato *server.js* che contiene la configurazione di hello per server web hello.

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

## <a name="install-express-and-set-up-routes-toohello-server"></a>Installare Express e configurare le route toohello server

[Express](https://expressjs.com) è un framework applicazione Web Node.js minimo e flessibile che fornisce funzionalità per le applicazioni Web e per dispositivi mobili. Express viene utilizzato questo tooand di informazioni toopass esercitazione libro dal database MongoDB. [Mongoose](http://mongoosejs.com) fornisce una soluzione semplice e basata sullo schema di toomodel i dati dell'applicazione. Mongoose viene utilizzata in questa esercitazione tooprovide uno schema del libro per database hello.

1. Installare Express e Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. In hello *documentazione* cartella, creare una cartella denominata *app* e aggiungere un file denominato *routes.js* con hello express route definite.

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

3. In hello *app* cartella, creare una cartella denominata *modelli* e aggiungere un file denominato *book.js* con configurazione del modello di libro hello definito.  

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

## <a name="access-hello-routes-with-angularjs"></a>Route di hello accesso con AngularJS

[AngularJS](https://angularjs.org) fornisce un framework Web per creare visualizzazioni dinamiche nelle applicazioni Web. In questa esercitazione è utilizzare la pagina web di AngularJS tooconnect con Express e le azioni eseguibili dal database di libro.

1. Modificare anche le directory hello backup*documentazione* (`cd ../..`), quindi creare una cartella denominata *pubblica* e aggiungere un file denominato *js* con controller hello configurazione definita.

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
    
2. In hello *pubblica* cartella, creare un file denominato *index.html* con una pagina web hello definito.

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

##  <a name="run-hello-application"></a>Eseguire un'applicazione hello

1. Modificare anche le directory hello backup*documentazione* (`cd ..`) e avviare il server di hello eseguendo questo comando:

    ```bash
    nodejs server.js
    ```

2. Aprire un browser toohello indirizzo registrato per hello macchina virtuale. Ad esempio: *http://13.72.77.9:3300*. Dovrebbe essere simile al seguente hello pagina seguente:

    ![Record del libro](media/tutorial-mean/meanstack-init.png)

3. Immettere i dati in caselle di testo hello e fare clic su **Aggiungi**. ad esempio:

    ![Aggiungere il record di un libro](media/tutorial-mean/meanstack-add.png)

4. Dopo l'aggiornamento pagina hello, dovrebbe essere simile a questa pagina:

    ![Elencare i record dei libro](media/tutorial-mean/meanstack-list.png)

5. È possibile fare clic **eliminare** e rimuovere i record della Rubrica hello dal database hello.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è creata un'applicazione Web che tiene traccia dei record dei libri usando uno stack MEAN in una VM Linux. Si è appreso come:

> [!div class="checklist"]
> * Creare una macchina virtuale Linux
> * Installare Node.js
> * MongoDB di installare e configurare server hello
> * Installare Express e configurare le route toohello server
> * Route di hello accesso con AngularJS
> * Eseguire un'applicazione hello

Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.

> [!div class="nextstepaction"]
> [Secure web server with SSL (Proteggere il server Web con SSL)](tutorial-secure-web-server.md)
