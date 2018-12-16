ChooseEditor V2.10 Copyright 2016 Wolfgang Morgeneier

General:
The program is a tool for filemanager TotalCommander.
Its purpose is to simplify the handling of several editors.
It consists of two parts:
The file Editors.exe is used to choose an editor for a file to be edited.
The file ChooseEditor.exe is the configuration program for Editors.exe.
For the configuration program the runtime version of NET 2.0 is necessary.
The program is freeware and can be freely used.  But only the original unchanged package may be forwarded to others.
As the author I take no warranty for any damages caused by the program.  But I would be glad to hear about bugs of the program.


Installation:
The files must be copied into a directory, the user has write access.
If this is not possible, move the files Editors.ini and ChooseEditor.ini into directory <%USERPROFILE%\Appdata\Roaming\ChooseEditor>.
Pick file Editors.exe with full path as editor for F4 in program TotalCommander.
Thereby the program Editors.exe will be called for each edit command within TotalComander and an editor can be selected.


Usage of Editors.exe:
The program can be called with the following parameters:
-T: Editor.exe as topmost window
-t: Editor.exe not as topmost window
-m: <Show main Editors> is checked 
-e: <Show extended Editors> is checked
-a: <Show all Editors> is checked
-C: <Close program after calling Editor> is checked
-c: <Close program after calling Editor> is not checked
-x: if <Show main Editors> is checked and there exists a default editor, this editor will be called at once 
The file to be edited must be the last parameter.
The program parameters have a higher priority than the adjustments in the file Editors.ini
Example: editors.exe -T -m file

After start of the program a list shows all editors, which are defined for the file extension of the file to be edited.
With a douple click on an editor this editor will be started with the respective file.
Furthermore, you can select an editor and start it by pushing the button <Call Editor> or by pushing the return key.
By pushing the button <Cancel> or the escape key the program will be ended and nothing will be done.
With <Edit Defs> the configuration program will be started.  This button can be made hidden using the configuration program.
If <Close program after calling Editor> is checked (default setting), the program ends immediately after an editor is called.  If it is not checked, the program will get minimized and runs until 
the called editor will be closed.  With this it is possible to edit a file in an archive and save the modified file back into the archive.
The editors to be displayed can be selected by 3 option buttons.
<Show main Editors>: This is the default option, which is selected at start of the program.  Only the editors are displayed which are fully usable for the file with the file extension to be edited
according to definition.  These are all editors with the file extension indicated in the list of main extensions.
In this list the default editor for the respective file extension is always selected at the beginning.  
If you choose another editor by double click on this editor this preselection will not be changed for next time.  However if you push the button <Call Editor> preselection will be changed. 
<Show extended Editors>: By selecting this option all editors are displayed which are fully or partly usable for the file with the file extension to be edited according to definition.
These are all editors with the file extension indicated in the list of extended extensions.  No editor is selected.
<Show all Editors>: All available editors are displayed.  No editor is selected.


Usage of ChooseEditor.exe:
This is the configuration program for the editors.
The window is devided into 3 parts.  In the upper part there are general adjustments, in the middle there is the list of editors and in the lower part there are the buttons.

General adjustments:
- Total number of editors: This shows the number of editors (cannot be changed).
- Text field <Left corner of dialog Editors.exe>: distance of dialog window of editors.exe from left edge of monitor in pixel.
- Text field <Top corner of dialog Editors.exe>: distance of dialog window of editors.exe from top edge of monitor in pixel.
- Path of file editors.ini: path of file editors.ini, which will be edited in the moment (cannot be changed).
- Check box <Editors.exe as Topmost window>: If this is checked, the dialog window of editors.exe will be opened on top of all other windows.
- Check box <Hide edit defs button>: If this is checked, the button <Edit Defs> in dialog window of editors.exe is hidden.
- Check box <Close program deactivated>: If this is checked, <Close program after calling Editor> in Editors.exe will not be checked (this means Editors.exe will shut down immediately after start of an editor)
  If this is not checked, <Close program after calling Editor> in Editors.exe will be checked (this means Editors.exe will not shut down after start of an editor)
  If the check box is in "Tristate" condition, the program decides to check or not to check <Close program after calling Editor> depending on the path of the file to be edited.
  If the file is in directory <%Temp%\_tc> (normally this file is a temporary file from an archive), <Close program after calling Editor> will not be checked.
  Otherwise <Close program after calling Editor> will be checked.
- Option box <Show main Editors>: In program Editors.exe <Show main Editors> is checked.
- Option box <Show extended Editors>: In program Editors.exe <Show extended Editors> is checked.
- Option box <Show all Editors>: In program Editors.exe <Show all Editors> is checked.

The list shows all editors defined in file Editors.ini.
The following is shown in the list:
- short designation of the editor
- full path of the editor (or eventually only file name, if the editor is located in program search path)
- main file extensions, the editor can be used with (individual extensions are separated with <|>)
- extended file extensions, the editor can be used with (individual extensions are separated with <|>)
- default file extensions, the editor is preselected for (for each file extension only one editor can be preselected)

Description of the buttons:
- <New Editor>: An additional editor will be created.  The dialog "Add new/Edit Editor" will pop up.
- <Edit Editor>: The selected editor can be modified (only one editor may be selected).  The dialog "Add new/Edit Editor" will pop up.
- <Delete Editor(s)>: All selected editors will be deleted after a confirmation prompt.
- <Save to Editors.ini>: The editors with all presets will be saved to file Editors.ini after a confirmation prompt.
- <Cancel/Quit>: The program will be ended.  If there are unsafed changes, there will be a confirmation prompt.
- <New Editor with act Data>: An additional editor will be created. As a template the selected editor will be used (only one editor may be selected).  The dialog "Add new/Edit Editor" will pop up.
- <Read Editors from Reg>: The program will try to read the editors for the file extensions in the registry.  They can be edited with dialog box "Add Editors from Registry" and added to the editors to be used for the program.
The method is not failproof.  There can be wrong results and many editors can be ignored.  But the registry will only be read and not changed.
- <Reload from Editors.ini>: After a confirmation prompt all changes will be discarded and the editors will be reloaded from the prferences file.
- <Sort Editors a-z>: After a confirmation prompt the editors will be sorted according to their short designation.  Also the file extensions of the individual editors can be sorted.
- <Move Editor up>: Move the selected editor up one row (only one editor may be selected).
- <Move Editor down>: Move the selected editor down one row (only one editor may be selected).

Description of dialog "Add new/Edit Editor":
This dialog is used to edit existing editors and create new editors.
Text field <Name of editor>: This is the short designation of the editor (this text will be shown in program Editors.exe).  Each editor must have a short designation which is different to each other editor (upper and lower case is no difference).
<Set directory as name>: If there is a path in <Path of editor>, the directory of the editor will be inserted as short designation of the editor.
<Set filename as name>: If there is a path in <Path of editor>, the filename of the editor (without extension) will be inserted as short designation of the editor.
Text field <Path of editor>: This is the full path of the editor, including file name and extension.  If the file directory is included in the program search path, the directory can be omitted.
In this text field environment variables can be used (e.g. %userprofile%).
<Select editor path>: A dialog to select the editor with path is shown.
Text field <Working directory>: If the editor needs a special working directory, it must be entered here.  Normally this is not necessary.
<Select working dir>: A dialog to select a path is shown.
Text field <Parameter before file>: If there must be any additional parameter for the editor before the file to be edited, it must be entered here.  Normally this is not necessary.
Text field <Parameter after file>: If there must be any additional parameter for the editor after the file to be edited, it must be entered here.  Normally this is not necessary.
Check box <Insert file without quotes>: If the file to be edited shall not be included within quotes this box must be checked.  Normally this must be unchecked.
List <List of main extensions>: This is the list of all main file extensions, the editor can fully be used with.  Enter the file extensions without dot.  For files without file extension enter a <.> (dot).
For all file extensions enter a <*> (star).  If there is a special fixed beginning of the file extension and the remaining part is variable, enter the beginning of the file extension and a <*>.
The star represents 0 or more characters.  If a character of the file extension can be any character, enter a <?> (question mark) for this character.  A question mark represents exactly 1 character.
It is not allowed to use star and question mark together for one file extension.
List <List of extended extensions>: This is the list of all extended file extensions, the editor can fully or partially be used with.  Enter the file extensions without dot.  For files without file extension enter a <.> (dot).
For all file extensions enter a <*> (star).  If there is a special fixed beginning of the file extension and the remaining part is variable, enter the beginning of the file extension and a <*>.
The star represents 0 or more characters.  If a character of the file extension can be any character, enter a <?> (question mark) for this character.  A question mark represents exactly 1 character.
It is not allowed to use star and question mark together for one file extension.
List <Default extensions>: This is the list of all default file extensions, the editor will be preselected.  Each default file extension may only exist one time and only such file extensions may be entered,
which are included in the list of file main extensions.  Enter the file extensions without dot.  For files without file extension enter a <.> (dot).  Neither a star nor a 
question mark may be entered for this.
The entries can be edited as follows:
<New extension> or <New default>: Add an additional file extension for the editor.
<Edit extensions> or <Edit defaults>: Edit the file extensions of the editor in a comfortable manner.  The dialog "Edit extensions/Edit default extensions" will pop up.
<Delete extension> or delete default: Delete the selected file extension of the editor (without confirmation prompt).
<Move extension up> or <Move default up>: Move the selected file extension of the editor up one row.
<Move extension down> or <Move default down>: Move the selected file extension of the editor down one row.
<Copy ext to extended>: The actual selected file extension will be copied to the list of extended file extensions.
<Copy ext to main>: The actual selected file extension will be copied to the list of main file extensions.
<Copy all to extended>: All file extensions will be copied to the list of extended file extensions.
<Copy all to main>: All file extensions will be copied to the list of main file extensions.
<Copy ext to default>: The actual selected file extension will be copied to the list of default file extensions.
<Sort extensions a-z>: Sort the file extensions of the editor.
<Add extension for>: Add all file extensions of an defined file type.  Before doing this select a file type in the drop down menu at the right.  The file types are defined in file ChooseEditor.ini and can be adjusted as required.

<Use and return>: Save the changes and close the dialog.  If any file extension is listed only in main file extensions and not in extended file extensions, a dialog will pop up,
which allows to copy these file extensions to the extended file extensions.
<Cancel>: Close the dialog without saving changes.  If there are any changes a confirmation prompt will pop up.

Description of dialog "Edit extensions/Edit default extensions":
The dialog is used to edit main/extended file extensions and default file extensions of an editor in an easy way.
Multiline text field: This text field shows all file extensios of the editor.  Each file extension stands in one line and is terminated with the enter key.  
The text field can be edited in any way.  But you are responsible yourself for entering only meaningful inputs according to the definition above. 
<Save and close>: The file extensions will be transmitted to the dialog "Add new/Edit Editor" and the actual dialog will close.
<Cancel>: Close the dialog without saving changes.  If there are any changes a confirmation prompt will pop up.

Description of dialog "Add Editors from Registry":
The editors extacted from the registry can be edited and added as editors for the program.
<Available editors from registry>: This is the list of the editors extracted from the registry with file path and a file extension.
<Editors to save for program>: This is the list of editors which can be saved as editors for the program.  The editors must be copied from the list <Available editors from registry> to this list.
<Add all editors>: All editors of the list <Available editors from registry> will be copied to the list <Editors to save for program>.
<Add selected editor>: The selected editor (path and file extension) of the list <Available editors from registry> will be copied to the list <Editors to save for program>,
if the editor is not jet existing.  Double clicking on an editor in list <Available editors from registry> has the same result.
<Remove selected editor>: Removes the selected editor from list <Editors to save for program>.  Double clicking on an editor in list <Editors to save for program> has the same result.
<Cancel>: Close the dialog, without adding editors (there will be no confirmation prompt).
<Save and Close>: Close the dialog and add the editors of list <Editors to save for program> to the editors (main file extensions and extended file extensions) of the program.
This will be done the following way:
- If the editor path of more than one editor is the same, these editors will be combined.
- Short designation of the editors will be the filename without file extension.  
- If the short designation already exists, the character "1" will be added to the short designation as long as the result is a unique short designation.


Description of file Editors.ini:
This is the initialization file for program Editors.exe.  First the program searches for this file in program directory.  If it does not find it, it searches in directory <%USERPROFILE%\Appdata\Roaming\ChooseEditor>.
You should not manually edit this file.  It includes data for the location of the window of program Editors.exe, the filename of the configuration program and all data of the individual editors.


Description of file ChooseEditor.ini:
This is the initialization file for program ChooseEditor.exe.  First the program searches for this file in program directory.  If it does not find it, it searches in directory <%USERPROFILE%\Appdata\Roaming\ChooseEditor>.
The file ChooseEditor.ini contains (among others) the file extensions of the defined file types, which can be used in dialog "Add new/Edit Editor".  These configurations can only be changed manually.
NumberofExtensions: Number of extension types
ExtensionXName: Name of the individual file extension types
ExtensionXExt: Extensions of the individual file extension types, separated by <|>
X is the number of the individual file extension type and must start with 1 and end with NumberofExtensions.


Version history:
V1.00 first version
Changes in V1.10:
- environment variables for path
- editor.exe can be a topmost window
- button <Edit Defs> can be hidden
- smaller changes
Changes in V1.20:
- option to not immediately close program Editors.exe, but wait until the called editor is closed
- full implementation of * and ? for file extensions 
- return key in program editors.exe = Call Editor  
Changes in V2.00:
- escape key in program editors.exe = Cancel
- now the program editors.exe has 3 groups of editors for each file extension
  - main editors, which are fully usable for the file extension (main file extensions)
  - additional editors, which are partially usable for the file extension, including main editors (extended file extensions)
  - all editors
  the user is responsible for organizing the editors for each file extension
  without additional organization there is no significant change to V1.20, as during loading of an old initialization file 
  the file extensions will be included in both lists (main file extensions and extended file extensions)  
- smaller changes
Changes in V2.10:
- function <Close program after calling Editor> extended
- additional adjustments for ChooseEditor.exe
- program parameters for Editors.exe

Wolfgang Morgeneier
Email: W.Morgeneier@gmail.com
