## Purpose
DefenderAV is a collection of useful powershell scripts relating to Defender AV (local client)

## DefenderSettings.ps1 (Checks common Defender settings, and outputs to a file with Microsoft Related URLS for info/config options)

    In the default configuration, you can see lines #2-4 sets variables, and these can be modified to suit your needs:

    $systemname 
    uses the environment variable hostname to uniquely identify what machine log this file belongs too

    $fileoutputdir
    Defines what directory to output this file too. This is a customizable output, by default it logs to "C:\Windows\Temp" directory
    However, you can change the variable to use a network file share, such as $fileoutputdir = "\\insertUNC\directory"

    $filename 
    Defines what you want the filename to be called, currently it outputs the filename as $systemname$filename, but this can also be configured, for example if you have            already have a directory that identifies what the script relates too, you can remove the $filename variable such as below:
    Write-Output "-------------------------------------------" >> $fileoutputdir\$systemname
    You will want to do CTRL + F most likely in a text editor and replace all the occurences since these variables are frequently called

    Lines 10-18 will check if the script is running as admin, if it's not it will log following warning in the beginning of the log file:
    WARNING! WARNING! WARNING! WARNING! WARNING!
    YOU DID NOT RUN THIS SCRIPT AS ADMINISTRATOR. FOR ACCURATE RESULTS WITH MAPS CONNECTIVITY PLEASE RUN SCRIPT AGAIN AS ADMIN

    ## What settings is the script checking?
    The powershell script uses the get-mppreference and get-mpcomputerstatus cmdlets to check the following:
    - Is Defender AV enabled?
    - Is real-time protection enabled?
    - Is Behavior monitoring enabled?
    - Is Ioav protection enabled?
    - Is On-access protection enabled?
    - Is network inspection service enabled?
    - Is your defender settings tamper protected?
    - Is MAPS enabled to get cloud-delivered protection?
    - Is the MAPS setting and sample submission set to basic, or advanced / submit safe samples or all samples
    - What block level of cloud protetction do I have enforced?
    - Is my machine able to talk to MAPS?
    - IS Block at first site enabled? (BAFS)
    - Is my signature defintions updating?
    - How often are they updating in days?
    - How many times are they updating within that day?
    - What source are the updates coming from?
    - What type of scan is running?
    - How often are scans running?
    - What time of the day is the scan running?