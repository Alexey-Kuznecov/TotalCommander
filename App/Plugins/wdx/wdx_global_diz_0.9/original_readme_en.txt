GlobalDiz Content Plugin for Total Commander 6.50+ 
Version: 0.8b
Author: Pavel Dubrovsky aka D1P
English readme file by Sergeich.

Description:
Plugin allows assign files and directories to user groups, create user columns and store descriptions for files in global file.

Installation:
Instruction is given for TC 6.50 En.
Unpack archive into folder (for example: c:\tc\plugins\wdx\global_diz).
In TC go to menu -> Configuration -> Plugins -> Content Plugins (.WDX) -> Configure -> Add 
Then browse for file c:\tc\plugins\wdx\global_diz\global_diz.wdx 
Press OK, OK and OK :)

Configuration:
In plugin folder you can find ini-file (global_diz.ini) with default plugin settings.
This file must be stored in plugin folder or by filepath stored in registry
(HKEY_CURRENT_USER\Software\Legion\GlobalDiz, key "IniFileName").

Usage:
Adding files to group, descriptions for files can be done via separate program add_diz.exe. 
This program can works with command line parameters:

/? - Show help screen with short description of command-line parameters.
Sample:
add_diz.exe /?

/O - show plugin configuration window.
Sample:
add_diz.exe /o

/G or /GUI - start program in GUI-mode. If file name is missing, 'Open file' dialog will be shown
Sample: 
add_diz.exe c:\some\file.txt /g

/C or /CLEAR - clear base from dead entries.
Sample:
add_diz.exe /c

/DIZ=<description> - add description for file. Option can be used with /GROUP or /USER options or separate.
Sample:
add_diz.exe /diz="My description for file" c:\some\file.txt
add_diz.exe /diz=? c:\some\file.txt - ask description in dialog mode.

/GROUP=<group> - add file to group.
Sample:
add_diz.exe /group=WORK c:\some\file.txt

/USER=<user column> - add file to user columns. 
User column must be specified as filename (column name will be shown as filename without extension).
Sample:
add_diz.exe /user=ColName.diz /diz="Report" c:\some\file.txt

If specified column not exists, TC must be restarted and configured for showing this column.

/D or /DELETE - delete file from group or user column. 
Sample:
add_diz.exe /delete c:\some\file.txt - delete group assignment for file c:\some\file.txt

add_diz.exe /delete /user=ColName.diz c:\some\file.txt - delete file c:\some\file.txt from user column ColName

add_diz.exe /delete /list=c:\file.tmp - delete all group assignments for files listed in file c:\file.tmp

File or listfile can be recognized automatically. 
But if you have troubles with recognition - following specials options can be used:

/FILE=c:\some\file.txt - specify file for operation.

/LIST=c:\some\file.tmp - specify list-file (for example created with %L parameter in TC) for operation.

Options order and lettercase doesn't matter. 

If incompatible options (for example /user and /group) was given - latest option will be used. 
For specifing values with spaces quotes must be used (e.g.: /DIZ="Description with spaces").

Comments and suggestions are always welcomed!
To contact me, use the following address: no_spam@students.ru.

Special thanks:
Christian Ghisler,
Ergo,
CyberPilgrim,
all forum.wincmd.ru users.