NL_Info, Version 1.20
  Content plugin for Total Commander, that allows to view information about hard links and
  reparse points on NTFS.

Plugin's author: Konstantin Vlasov, 2011
Homepage: http://flint-inc.ru/
E-mail:   support@flint-inc.ru

Distributed under BSD 2-Clause license. 

For writing the plugin, source code of the program Junction.exe was used.
The author of the program is Mark Russinovich (http://www.sysinternals.com/).


Description
-----------

The plugin contains the following data fields:
1. Number of Hard Links
   The hard links counter for the particular file. For usual files (and for files on
   non-NTFS partitions) this counter is 1, since the file itself is also a hard link.
   This field is available for files only.
2. Reparse Point Type
   Here is the full list of possible types of reparse points:
     Junction (type of links available in pre-Vista Windows systems)
     Mount Point (mount point for a partition)
     Symbolic Link (new type of links introduced in Windows Vista)
     Hierarchical Storage Management Reparse
     Native Structured Storage Point
     Native Structured Storage Recovery Point
     Single Instance Store Point
     Distributed File System Point
     Unknown Microsoft Reparse Point
     Third-Party Reparse Point
3. Reparse Point Type (Ext)
   This field outputs the same as the "Reparse Point Type", except for usual folders it
   outputs "Folder", and for files "File". This can be useful e.g. for searching or
   selecting all folders but not reparse points.
4. Reparse Point Target
   The object the link points to. For mount points the plugin automatically converts the
   volume identifier stored in the file system record into a common drive letter (only
   if a letter is assigned to this partition, of course).
5. Relative
   Flag telling whether the link is absolute or relative. It is applicable to Symbolic
   Link type only.
6. Valid Target
   Outputs the value Yes or No to show if the reparse point target is available or not.


System Requirements
-------------------
32-bit version:
	Windows 2000 or higher
	Total Commander 7.50–8.0 x32

64-bit version:
	Processor with 64-bit instrustion set (Intel Pentium 4, AMD Athlon 64 and higher)
	Windows XP x64 or higher
	Total Commander 8.0 x64


Version History
---------------

Version 1.20:
  1. Plugin now uses Unicode strings.
  2. Added 64-bit version.
  3. Added support for Windows Vista/7's symbolic links (files and directories).
  4. Added new field "Relative".
  5. Source code is published under the BSD license.

Version 1.11:
  1. Fixed a bug: incorrect handling of the "Reparse Point Type (Ext)" field.

Version 1.10:
  1. The field "Junction Type" is renamed into more correct "Reparse Point Type".
  2. A new field added: "Reparse Point Type (Ext)", that outputs the same values as the
     "Reparse Point Type" field, but in addition for usual folders it outputs "Folder".
  3. A new field added: "Valid Target" that outputs Yes or No to show if the reparse
     point target is available or not.
  4. Added the installation descriptions in the file pluginst.inf in Polish (Pawel
     Wawrzyszko) and Ukranian (Butsky Igor).

Version 1.03:
  1. Added German translation (Kurt Lettmaier).

Version 1.02:
  1. Fixed a small bug, which caused incorrect work of searching by field "Junction Type"
     in Total Commander 6.52.
  2. Added Polish interface translation (Pawel Wawrzyszko).
  3. Added Ukranian interface translation (Butsky Igor).

Version 1.01:
  1. Fixed a bug that did not allow to use the plugin on Win2000 systems.

Version 1.0:
  1. The first public version. Can show the number of hard links for files, and type and
     target for reparse points (junctions, mount points).
