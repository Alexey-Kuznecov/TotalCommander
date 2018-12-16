NTLinksMaker tool for Total Commander
-------------------------------------
(information in English is below)

������� ��� �������� NTFS-������ ���� �����:
+ �������� ����� ����������, ������� ������, � ����� ������������� ������
+ ����������� ������������ ���������� ������� ��������� �������� ����������
+ ����������� ���������� �������� ��������� (��� �������� �� ������ ���������)
+ ������ ��������� ��� ��������, ��������� ���� ��������������
+ ����������� ������ ��� ����������� ���������� ����
+ ��������� ������� � ������� �����


1. ���� ������ � NTFS

����� ���������� ��������� - ��� ��������������, ������ ������� ������������ ������� ���������� ���������� ������� ���������, �������� ����� �������� ���. ��������� ������ ������������, ������� ������������ ����� ������ �� ����. ������ ��������� (������� ��������� � Windows XP) �� �������� �� �� ������� ��������� � ��� �������� ������ ������� ��� ����� ������ �������� ��������, ������� ����� ������� �� �� ��. �������������� � Windows 2000.

������� ������ ������ - ��� ������������ ������, ����������� �� ����� ���������� �����. ����� ����� ��������� ����� � ���������� � ������ ��������� � �������� ������ ����. ��������� ���������, ���� ������� ��� ����������� ����� ����� �� ��� �������� ��� ����. ��� ��������� ����� ����� ���� ������ ��������� ����� ���������� ���������� ���������� ����������, ���� ���� �� ����� ������ ����� ���. ���������� ����� �������� �� �����, ���� ���� ���� �� ���� ������� ������ �� ����. �������������� � Windows 2000.

������������� ������ ��������� - ������, ������� �� ����� ����������, �� ����������� ������������� � ������� ����. ��� � � ������ ����� ����������, ������ ��������� ����� ��� �������� ������ ������� ���������� �������� ��������. �������������� � Windows Vista, ��� �������� ����� ����� ��������������.

������������� ������ ������ - �����������, ����������� ���������� � ����������� ������� ������ � �������� ���. ��� �� ���������� ������� (�� ������ �������) � ��������� �������� ����� (���� ����������� ������ ����� ���� �������� ������). �������������� � Windows Vista, ��� �������� ����� ����� ��������������.


2. ���������� ����

� ���� ����� �������� ���� � �����, � ������� ����� ������� ������, � ��� ����������� ������. ���� �������� ������ ������, ���������� � �������� ����� ��������� *.* ��� ����� ������� ����� (��������, *_z.* ��������� � ������ ��������� "_z", � ��������� * ����������� ����������).
����� ����� ��������� ��������� �������� ������, ����� ��� ������� ������� ��� ���������� ��������� ������������ �������� (��. ����� /r), ���������� ������� ��������� ��� ������� �������� (��. ����� /l) � ���� ����������� ������.


3. ��������� ������

��������� �������� � ����������� ������� � ���������� ��������� ��������. �� ������ �������� �������� ������ � ��������� ���������, ���������� ������� ������ ��� ��� ����������� ������� � ��������. ����� �� ������ ��������� �������� � ����������� �������� ������� ������ ��� �������� �������.

��� ������� ������ ������� �������� ��� ����������� �������� ����������� �� ����� ��������������.

��� ������� � ����� ������ ��� ������ ����� ������������, ����� �������������� �� �������������.


4. ��������� ������

� ��������� ������ �������� �������� �������, ��� ������� ���������� ������� ������, ������� ����������, � ����� ��������� ��������� �������� ������ � ��������� ���������. ���������:

NTLinksMaker[.exe] [<parameters>] {<src_file>|@<src_list_utf16>} <dst_path>

���������:
	/l=0
		���������� �������, �� ������� �������� ����� �������������� ��� ������� ��������, ������ ������� ����� ��������� �������� ������. �� ��������� ������ ����� ������� ��������-������.
	/s[?]
		���� ���� �� ������, ��� ��������� ��������� ����� ����������, � ��� ������ - ������� ������. ���� ������ ���� /s, ��� ������ � ��������� ��������� ������������� ������. ���� ������ ���� /s?, �� ������������� ������ ��������� ������ ��� ��� ��������, ��� ������� ���� ��� ������ ������� ���������� (��������, ��� ������ � ������� ���� ��� ������� �����).
	/r=<path>
		������ ����� ��������� ��������� ������ ��� �������� � ����������� �� ��������� ������������. ��� ������� ������� ������������ � ������������ ��������� ��������� ������������ ���������� �������� ��������.
	/b
		����������� ���� �� ��� ����������� ������� ������� (��� � ��� ������� �������� ��).
	/n
		���� ���������� ���������, ���� ������� ���� �������� ��� ������ (� �� ������ ���� � �����, ��� � ����� �������).
	/q
		�������� ����� �����, � ������� �� ����� ������ ������� �� ����� �������� ������� ���������� ���� � ��������. ����� ������� ��������, ������� �������� �������, � ��������� ��� ���������� (���������, ���� ���� ������).

����� ������ ���������� ����������� ���� � ��������� ����� ��� �������� (��� �� ���� � �����-������ � ��������� UTF-16 � ��������� @) � ���� � �������� ����������.


������� �������:

������� ������ �� D:\TEMP � ����� C:\TEST (� ������������ ����������� ����):
NTLinksMaker.exe "D:\TEMP" "C:\TEST\"

������� ������ �� D:\TEMP � ����� C:\TEST � ������ TEMPORARY (� ����� ������):
NTLinksMaker.exe /q /n "D:\TEMP" "C:\TEST\TEMPORARY"

������� ������������� ������ ��� �������� �� �����-������ D:\list.txt � ����� C:\TEST (� ����� ������, ����� ����� ��������������):
NTLinksMaker.exe /q /s "@D:\list.txt" "C:\TEST\"


5. ���� ������������

���������������� ���� ������ ���������� � ����� ������� � ����� ����� �� ��� �����, �� ���������� INI.

��������� ������ [NTLinks Maker]:

	FontName
		�������� ������ ����������� ����;
	FontSize
		������ ������ ����������� ����. ������ ����� �� ������ ��������� ����. ����� �������������� ��� �������� FontName;
	Language
		��� ���������� ����� ����� ��������� (��� ���� � ����������).


6. ���������� � ��

����� ������������ ������� ������ � ��, ����� ������� ������ �� ������ ������������ ��� ���������������� ������� (����� ����� ����� �������� ������� � ������� ���� ��� ��������� ���������� ������). � ���� ���������� ������������� ��������� ���������: /q- /b /r="%P" "@%WL" "%T". ����� ����, ����� �������� ��������� ��������� ����� ������� � ������� ������ /l � /s. ����� ���� ������� �� ���������� ��� ������� �������, ����� ����� ���������� �� ������� "..", ����� �������� ���� /q � ���� �������: "NTLinksMaker.exe" /q.


���������� �� ����������� ������������� ������: http://forum.wincmd.ru/viewtopic.php?t=13191



NTLinksMaker tool for Total Commander
-------------------------------------
(English section)

Tool for NTFS links creation:
+ supports junctions, hardlinks and symbolic links
+ allows duplicating first levels with regular folders
+ allows keeping directory structure (for objects from multiple dirs)
+ elevation request when admin rights needed
+ supports silent mode w/o any windows
+ Unicode and long paths support


1. NTFS link types

Junctions - pseudo-folders that show contents of some target folders and allow modifying it. They are similar to mount points that link to volumes. Old programs (including Explorer in Windows XP) treat them as regular folders and erase all target folder contents when you delete link, so it is better to delete them from TC. Supported since Windows 2000.

File hardlinks - equivalent links to the same file contents. Such links may have different names and located in different folders within same volume. You can change file attributes or contents via any of them, and other ones may show old attributes until you open file via them. File contents is kept on disk while at least one hardlink exists. Supported since Windows 2000.

Symbolic folder links - links similar to junctions but allowing relative and UNC paths. As for junctions, old programs may erase all target folder contents when you delete link. Supported since Windows Vista, administrator rights required for creation.

Symbilic file links - pseudo-files providing access to target file contents. Such links don't show file size (it is always zero) and attributes (modification date is always the same as link creation date). Supported since Windows Vista, administrator rights required for creation.


2. Dialog

You can change destination path and link name. In case of multiple objects link name must be *.* or a more complex mask (e.g. *_z.* adds "_z" to names while lonely * strips extensions).
Also you can set link creation parameters: base path for keeping directory structure (/r option), number of folders to create directly (/l option) and link types to be created.


3. Error handling

The tool reports all errors and asks for an action. You can abort creation of links and exit, or you can skip current object or all further objects with errors. You also can fix problem and try to repeat link creation for current object.

If you ask to repeat, all further operations will be done with admin rights.

In silent mode no error messages or elevation requests will be shown.


4. Command line

Command line accepts source objects and destination path, and also optional parameters. Syntax:

NTLinksMaker[.exe] [<parameters>] {<src_file>|@<src_list_utf16>} <dst_path>

Parameters:
	/l=0
		Number of levels where folders will be duplicated as regular folders with file links inside them. Next level will be duplicated with folder links.
	/s[?]
		If not set, junctions are created for folders and hardlinks for files. Option /s causes symbolic links for both folders and files to be created. Option /s? causes symbolic links to be created only when necessary (e.g. for files from another volume or UNC paths).
	/r=<path>
		This option allows links creation with keeping directory structure. It sets base path which is used to detect and re-create relative paths for all objects.
	/b
		Block TC window when dialog is shown (as for regular copy/move TC dialogs).
	/n
		This option must be set when destination path contains also link name.
	/q
		Enable silent mode which suppresses all questions and confirmations. Only possible actions will be performed and status code returned (nonzero in case of errors).

After parameters you should specify path to a source object (or path to a UTF-16 text file with list of objects prefixed with @) and a destination path.


Examples:

Create link for D:\TEMP in C:\TEST (dialog will be shown):
NTLinksMaker.exe "D:\TEMP" "C:\TEST\"

Create link for D:\TEMP in C:\TEST with name TEMPORARY (silent mode):
NTLinksMaker.exe /q /n "D:\TEMP" "C:\TEST\TEMPORARY"

Create symbolic links for objects from list D:\list.txt in C:\TEST (silent mode, admin rights required):
NTLinksMaker.exe /q /s "@D:\list.txt" "C:\TEST\"


5. Configuration file

Configuration file must be placed near application and have same name and extension INI.

Parameters in [NTLinks Maker] section:

	FontName
		Dialog font face name;
	FontSize
		Dialog font size. Also affects size of controls. May be used without FontName;
	Language
		Current language file name (just name w/o path and extension).


6. Integration with TC

In order to use tool with TC, you should create buttonbar button or user command (this one will allow adding tool to main menu or assigning a hotkey for it). Recommended parameter field string is: /q- /b /r="%P" "@%WL" "%T". Also you can alter initial dialog options using /l and /s keys. If you don't like to see help window when ".." item is focused, you can add /q key to command field: "NTLinksMaker.exe" /q.


Discussion page on official board: http://www.ghisler.ch/board/viewtopic.php?t=23681



History:

2017-01-10	1.2.0.340
	+ wildcard filename mask support (default mask is now *.* for consistency with TC)
	+ symlinks are now created manually in Explorer-compatible form

2016-11-07	1.1.1.322
	* source/target UNC path support (long path issue)

2016-01-17	1.1.0.306
	* /l=-1 worked as /l=0

2015-10-05	1.1.0.304
	+ paths with up to 1024 characters are supported now
	* a bit better error reporting
	* fixed junctions creation for long targets

2015-07-30	1.0.5.272
	+ FontName, FontSize options added
	- Windows font detection removed

2015-02-06	1.0.5.262
	+ creates intermediate folders
	+ /r parameter with base path to cut when determining destination name
	+ /s? parameter allows symlink creation when it is impossible to create old links
	+ detects Windows font to use in dialog
	* better error handling with hardlinks and new dir creation

2014-10-08	1.0.4.170
	+ retry/skip inner files/folders in case of nonzero level number

2014-08-14	1.0.3.154
	+ ignore all button added to error dialog
	+ left/right keys goes to selection start/end in input field
	* /l=-1 is now supported

2014-02-24	1.0.2.122
	+ supports junctions/hardlinks/symlinks and folder level to duplicate
	+ asks for elevation when required
	+ is able to block TC window
	+ F5/F6 switches selection in input field (like in TC)
	* do not enter reparse points
