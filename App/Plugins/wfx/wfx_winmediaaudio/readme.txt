Windows Media Audio 2 plugin v1.2
====================================
Copyright (C) 2011-2013 Christian Ghisler, Ghisler Software GmbH
This plugin is free software released under a BSD-Style licence.

Description:
============
This plugin uses the Windows Portable Devices interface to access media
players and some other devices like Android tablets.

Requirements:
=============
Windows Media Player 10 or newer

Installation:
=============
Just double click on the plugin archive to install it in Total Commander.

Usage:
======
This plugin is showing up in Network Neighborhood as "MediaAudio2".

History
=======
20131001 Release v1.2
20131001 Fixed: The plugin could delete the wrong files when there were more than 128 in a directory
20130701 Release v1.1
20130701 Fixed: Folders were recognized as files when the file system returned a size for them
20130701 Added: Let the user choose via Alt+Enter on the device name whether it sends time stamps as local time or UTC
20111230 Release v1.0
20111230 Release v0.7 beta
20111230 Fixed: The plugin didn't return the "friendly name" when more than 1 device was connected at the same time
20111229 Added: Copy cover art with audio files (untested, please report any errors shown in the log!)
20111229 Added: Set the OBJECT_NAME of uploaded audio files to the music title instead of the file name
20111219 Release v0.6 beta
20111219 Fixed: Metadata was not sent correctly
20111219 Fixed: Remove any name from the cache when it's renamed, deleted or uploaded, because the ID may change on some devices
20111219 Fixed: When uploading, we need to set the size of the uploaded file before sending the data
20111215 Initial Release v0.5 beta
