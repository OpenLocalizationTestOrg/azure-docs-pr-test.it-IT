### <a name="create-a-nodejs-application"></a><span data-ttu-id="d50fa-101">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="d50fa-101">Create a Node.js application</span></span>

<span data-ttu-id="d50fa-102">Creare un nuovo file JavaScript denominato `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="d50fa-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="d50fa-103">Aggiungere il pacchetto NPM inoltro hello</span><span class="sxs-lookup"><span data-stu-id="d50fa-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="d50fa-104">Eseguire `npm install hyco-ws` dal prompt dei comandi di Node nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="d50fa-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="d50fa-105">Scrivere codice tooreceive messaggi</span><span class="sxs-lookup"><span data-stu-id="d50fa-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="d50fa-106">Aggiungere hello seguente toohello costante cima hello `listener.js` file.</span><span class="sxs-lookup"><span data-stu-id="d50fa-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="d50fa-107">Aggiungere hello seguenti costanti toohello `listener.js` file per i dettagli della connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="d50fa-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="d50fa-108">Sostituire i segnaposto hello tra parentesi quadre con valori di hello ottenuto al momento della creazione connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="d50fa-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="d50fa-109">`const ns`-hello inoltro dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="d50fa-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="d50fa-110">Nome completo dello spazio dei nomi di hello che toouse; ad esempio, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="d50fa-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="d50fa-111">`const path`-nome hello della connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="d50fa-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="d50fa-112">`const keyrule`-nome hello della chiave di firma di accesso condiviso di hello.</span><span class="sxs-lookup"><span data-stu-id="d50fa-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="d50fa-113">`const key`-hello valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="d50fa-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="d50fa-114">Aggiungere i seguenti toohello codice hello `listener.js` file:</span><span class="sxs-lookup"><span data-stu-id="d50fa-114">Add hello following code toohello `listener.js` file:</span></span>
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    <span data-ttu-id="d50fa-115">Il file listener.js sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d50fa-115">Here is what your listener.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

