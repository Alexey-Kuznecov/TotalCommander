GraphicConverter v 1.6.2.1 Beta

Packer plugin for Total Commander for convert from one image format to another.


*** Features ***

- read many graphic formats including camera RAW;
- save to PNG, JPEG, GIF, TIFF, BMP, ICO;
- apply embedded ICC profile;
- and some more.


*** Installing ***

TC has "auto install plugin" feature. Just enter to archive with plugin and TC ask you about plugin installing. 


*** Using ***

Select graphic files in TC, then select Files-Pack..., in combo box in Packer section panel select GraphConv.
You may change output file settings by pressing Configure button. 

Set ResetAllMetadataExtended in ini to 1 (default 0) for delete all metadata in JPEG include comment and ICC profile.
In Setup dialog option 'Reset All Metadata' must be enabled. 
Only for not "recompressed" files (if option 'Try Recompress Only if Needed' enabled).

For SVG converting plugin use rsvg-convert (from http://opensourcepack.blogspot.ru/2012/06/rsvg-convert-svg-image-conversion-tool.html).



*** License agrement ***

  This software provided "AS-IS" without warranty of any kind for non-commercial use only.


*** Changes history ***

Ver 0.9:
 * initial release.

Ver 1.2.1:
 + convert to ICO;
 * some fixes.

Ver 1.2.2:
 * Auto Adjust Orientation bug fix.

Ver 1.5 Beta:
 * graphic libraries updated;
 + basic functions for convert SVG files using RSVG converter;
 * some fixes.

Ver 1.6 Beta:
 * graphic libraries updated;
 + new parameters for enhance Camera RAW; 
 + new parameters for image sizing and JPEG save;
 * some fixes and improvements.

Ver 1.6.1 Beta:
 * graphic libraries updated;
 * improvements when convert SVG to multi icon.

Ver 1.6.2 Beta:
 * graphic libraries updated;
 + change image size in percent;
 + thumbnail size for JPEG (ThumbnailSize in ini, default 256);
 * some fixes and improvements.

Ver 1.6.2.1 Beta:
 * some fixes and improvements.


---
Suggestions, Wishes and bug reports are welcome!
ProgMan13, (ProgMan13@mail.ru)