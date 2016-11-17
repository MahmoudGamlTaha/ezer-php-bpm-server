###Installation instructions

Get the code

You can download the code using the downloads page, or you can check it out using the instructions in the source page.
Install the code

Once you have the code, just throw it under any folder you choose, e.g. C:\My\Ezer\Server or /opt/ezer/server.
Configuring the server

    Create your own application folder need the server folder we created already, e.g. C:\My\Ezer\App or /opt/ezer/app.
    Copy the content of one of the examples from the examples folder to your application folder, e.g.
        xcopy /Y /S /R C:\My\Ezer\Server\examples\syncProcess1`*` C:\My\Ezer\App
        rsync -avC /opt/ezer/server/examples/syncProcess1/ /opt/ezer/app
    Edit the bootstrap.php to verify that the require_once statement is pointing to the correct path of engine/infra/Ezer_Autoloader.php file.
    Make sure that the Ezer_Autoloader::setClassMapFilePath is pointing to existing folder.
    Create XML configuration file:
        For XML persistence:

<config>

<phpExe>

                C:\xampp\php\php.exe // path to the php exec

</phpExe>

<logicPath>

                logic // path (could be relative) to the folder where the logic XML files are saved.

</logicPath>

<instancePath>

                instance // path (could be relative) to the folder where the case results XML files are saved.

</instancePath>

<casesPath>

                cases // path (could be relative) to the folder where the case XML files are saved.

</casesPath>

</config>

* For **Propel** (DB) persistence:

<config>

<phpExe>

C:\xampp\php\php.exe

</phpExe>

<database>

<datasources default="ezer">

<ezer adapter="mysql">

                            user="root" password="root" dsn="mysql:host=localhost;dbname=ezer;user=root;password=root;" />

</ezer>

<log ident="ezer" level="7" />

</datasources>

</database>

</config>

    Create run.php script that includes:
        ini_set('max_execution_time', 0); // Enable the script to run forever.
        require_once 'bootstrap.php'; // Loads the classes auto loader
        $config = Ezer_Config::createFromPath('config.xml'); // Loads the configuration file
        $server = new Ezer_BusinessProcessServer(...); // Instantiate new server
        $server->addCasePersistance(...);
        $server->run();
    Run the server from command line: php run.php
