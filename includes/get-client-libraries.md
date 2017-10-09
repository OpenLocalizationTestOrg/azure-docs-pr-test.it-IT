### <a name="install-via-composer"></a><span data-ttu-id="592cd-101">Installazione tramite Composer</span><span class="sxs-lookup"><span data-stu-id="592cd-101">Install via Composer</span></span>
1. <span data-ttu-id="592cd-102">[Installare Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="592cd-102">[Install Git][install-git].</span></span> <span data-ttu-id="592cd-103">Si noti che in Windows, è necessario aggiungere anche variabile di ambiente PATH tooyour eseguibile hello Git.</span><span class="sxs-lookup"><span data-stu-id="592cd-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="592cd-104">Creare un file denominato **composer.json** in hello radice del progetto e aggiungere hello tooit di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="592cd-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="592cd-105">Scaricare **[composer.phar][composer-phar]** nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="592cd-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="592cd-106">Aprire un prompt dei comandi ed eseguire hello seguente comando nella radice del progetto</span><span class="sxs-lookup"><span data-stu-id="592cd-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
