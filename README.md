# install-earlierOfficeVersionperGPO
Installation einer vorherigen Office-Version per GPO


:: Script erstellt am 13.01.2025 von Amihanua90
::
::
:: Changelog
::
::
::
::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::aktuelle Office Version als Dateiname (ohne Endung) hier eintragen:
set curversion=18227.20162

::Abfrage nach Steuerdatei und installierten Komponenten
if exist "C:\Steuerdateien\Steuerdatei_Office_%curversion%.txt" goto exit

:Installationsdateien-auf-Client-kopieren
if not exist "C:\Steuerdateien" md "C:\Steuerdateien"
ping -n 2 127.0.0.1
if not exist "C:\Steuerdateien\Installationsdateien" md "C:\Steuerdateien\Installationsdateien"
ping -n 2 127.0.0.1
::if not exist "C:\Steuerdateien\Installationsdateien\Office" md "C:\Steuerdateien\Installationsdateien\Office"
::ping -n 2 127.0.0.1
::if exist "C:\Program Files\Microsoft Office\root\Office16" goto exit
::ping -n 2 127.0.0.1

goto Installation

:Installation
echo >>"\\[SERVER]\Softwareverteilung\Office\install_log.txt" %username% ; %date% ; %time% ; Office Client Installation gestartet
"C:\Program Files\Common Files\Microsoft shared\ClickToRun\officec2rclient.exe"/update user updatetoversion=16.0.18227.20162

::if %errorlevel% EQU 0 goto exit3
::if %errorlevel% NEQ 0 goto exit4
::goto exit1

goto Steuerdatei-schreiben

:Steuerdatei-schreiben

echo >>"c:\Steuerdateien\Steuerdatei_Office_%curversion%.txt"
echo >>"\\[SERVER]\Softwareverteilung\Office\install_log.txt" %username% ; %date% ; %time% ; Office Installation wurde erfolgreich abgeschlossen
exit

:exit
exit