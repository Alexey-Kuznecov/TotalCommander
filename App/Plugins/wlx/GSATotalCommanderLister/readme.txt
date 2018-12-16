
 ***************************************************************************
 *				GSATotalCommanderLister v.1.02.2
 *   				--------------------------------
 *   begin			: Jan 22, 2006
 *   copyright		: (C) 2006 GSA (Attila Gerendi)
 *   homepage		: http://sourceforge.net/projects/gsalister
 *   email			: darkz.gsa@gmail.com
 *
 *
 *   This program is free software; you can redistribute it and/or modify
 *   it under the terms of the GNU General Public License as published by
 *   the Free Software Foundation; either version 2 of the License, or
 *   (at your option) any later version.
 *	
 *   THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
 *   ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
 *   WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
 *   IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT,
 *   INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
 *   (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
 *   LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
 *   ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
 *   OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
 *   OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 *
 ***************************************************************************
 
Description:
----------------
 Lister plugin for the Total Commander File Manager. This plugin is a source code viewer with highlighting and some minimal editing features. It is based on scintilla and delphisci delphi component. The  GSATotalCommanderLister is Free Software , but if you find it useful, you can support its development :)
 
Installation:
----------------
Use Total Commander  automated installation from within zip.
 

Build Dependencies:
--------------------
- Delphi Scintilla Interface Components v.>=0.23 (delphisci.sourceforge.net)
- PCRE import unit for Delphi 7 and PCRE Wrapper for Delphi 7 (http://www.renatomancuso.com/software/dpcre/dpcre.htm)
- Delphi Fundamentals (http://fundementals.sourceforge.net/index.html)
- GSAScintillaConector (GSAScintillaConector.pas)


History:
--------
- v.1.02.2 (bugfix release) / December 04, 2007
1. The lister can now open already locked files

- v.1.02.1 (bugfix release) / June 14, 2007
1. implementing the p.3. feature in v.1.02 trashed the incremental search ability to search for those letters (1,2,3,4,5,6,7). Fixed.

- v.1.02
1. Now for installation can be done using Total Commander  automated installation from within zip.
2. The lister now try to load the dpcre45.dll and SciLexer.dll first from the plugin directory.
3. Added/forwarded shortcuts:
	- F2 			reload file
	- 1,2,3,4,5,6,7		(only forwarded when the file is in Read Only state)

- v.1.01.1 (bugfix release)
1. Quick fix. (Save buton remain always disabled)

- v.1.01

What's new:
============
1. Added shortcuts (p.9,p.1)
	- CTRL+N		- incremental search, search next
	- CTRL+P 		- incremental search, search previous
	- CTRL+SHIFT+R 	- incremental search, search with regex (toggle)
	- CTRL+SHIFT+H 	- incremental search, highlight search (toggle)
	- CTRL+O 		- open file
	- CTRL+S 		- save file (if not readonly)
	- CTRL+SHIFT+W 	- editor word wrap (toggle)
	- CTRL+R 		- readonly (toggle)
	- F6 			- emulate show/hide cursor total commander lister feature (partial)
	- F7,F3 		- find (Total Commander style)
	- F5 			- find/find next (Total Commander style)
2. Space now scroll down the document if document is readonly (p.4)
3. Added "Highlighter settings" (p.7,p.8) Note: loading external highlighter settings will increase the plugin load time, so if no user settings is needed just delete or rename the "highlighter.cnf" file and consider this feature inexistent.
4. Renamed "pcre.dll" to "dpcre45.dll" to avoid conflicts.
5. Removed debug informations from GSALister.


Suggestion points received on Total Commander forum (no particular order):
============================================================================
1. "Editing is possible only when opening a file from an already opened Lister window. Wouldn't be a better solution to implement a hot-key (F4) that toggles editing on/off?"
2. "Make it possible to turn the text cursor off, so that pressing cursor arrow keys scrolled the whole document instead of just moving the cursor" 
4. "scroll page down with space, just as lister does"
5. "Question: Your pcre conflicts with the one I use. Can I use not modded pcre 6.4 instead of yours? "
6. "Suggestion: you have a lot of unused things inside this plugin (Resources for sure. Also debug info. I think that also some code). Could you please clean it up before the final release?"
7. "Add customizations - at least, for fonts and colors."
8. "extendable highlighters set"
9. "in search, shortcut for moving to the next match" 

- v.1.00 - first public release

Todo:
--------
- complete emulate show/hide cursor total commander lister feature

Etc:
----
- I am curious if someone found this component useful, have suggestions to give and/or contribute with code, so feel free to email me regarding the program.


