### Author: ###

stevpan@gmail.com

XFileDialog is a Java wrapper class built upon Windows CFileDialog/IFileDialog and JNI. With xfiledialog, a Java Swing app can easily access several frequently-used functions of Windows native Filedialog (multi-selection, thumbnail view-mode, folder-selection).  On other platforms (MAC, LINUX) or DLL loading failure, XFileDialog will switch back to JFileChooser automatically.



**Stable: 0.63**
http://xfiledialog.googlecode.com/files/xfiledialog0.63.zip

The native C code was compiled with Visual C++ 2008.
XFileDialog is based on XP's CFileDialog and Vista's IFileDialog (Common Item Dialog).

## Changelog: ##

Ver.  0.63

  1. A bug in folder dialog under Windows XP 64 bit was fixed.
  1. Applet deployment of XFileDialog was improved.
  1. The XFileDialog interface was revised.

  * A new public method String getSaveFile() was provided for SaveFileDialog only.

  * Some unnecessary or misleading methods were removed,
> > e.g.  setMode(), getFilters(), setMultipleEnabled()

  * Actually, XFileDialog determines its internal native mode according the five top-level functions:
    * getFile();  (single-selection, LOAD mode)
    * getFilkes();(multi-selection, LOAD mode)
    * getFolder();(single-selection, folder only, LOAD mode)
    * getFolders(); (multi-selection, folder only, LOAD mode)
    * getSaveFile();(single-selection, SAVE mode)


  * The setFilters() method was replaced with two new methods:
> > addFilters(), resetFilters().


> See details in the sample "helloworld.java"

### What you can get from xfiledialog under Windows ###
  * faster startup
> > I shortened my Java program's startup time about 0.8 second by replacing JFileChooser with xfiledialog (Two customized JFileChoosers were initialized during startup in my old code).
  * Vista style dialog (in Vista/Win7)
  * Setting thumbnail view mode as default in Windows FileDialog
  * multi-selection
  * filename extension filter
  * small dll code size (about 100k bytes after compression)
> > It's more convenient and efficient than calling SWT filedialog from Swing.

### Some other features ###
  * Support for unicode filename
  * Support for applet deployment
  * Platforms supported:
    * Windows XP (32bit) + J2SE 6 (32bit)
    * Windows XP (64bit) + J2SE 6 (64bit)
    * Windows Vista (32bit) + J2SE 6 (32bit)
    * Windows 7 (32bit) + J2SE 6 (32bit)
    * Windows 7 X64 (64bit) + J2SE 6 (32bit)
    * Windows 7 X64 (64bit) + J2SE 6 (64bit)
    * Windows 7 X64 (64bit) + IE (64bit) + J2SE 6 (64bit)

  * J2SE 7
    * tested successfully in  early-access (b76) + Windows XP (32 bit)



### Interface: ###

To select multiple files, three new methods were added:
```
    * void addFilters(ExtensionsFilter... filter); 
     Note:  details can be found in helloworld.java 

    * void resetFilters(); 
        
    * String[] getFiles(); 
      Return:  relative filenames 
      Note: You can call getDirectory() to get the current directory and create your File objects.  

```
To select folders,  two new methods were added:
```
    * String getFolder(); 
      Return: absolute (full) path name

    * String[] getFolders(); 
      Return: absolute (full) path names

```
To set Thumbnail List as the default view mode for graphic apps
```
    * void setThumbnail(boolean val); 
    Note:  val=true will force the native Windows dialog to thumbnail view mode. 
           val=false does not mean to disasble the thumbnail viewmode. It will let the
           filedilog determine its view mode. In Vista, the filedialog can remember the
            view mode of your last visit. 

```

To turn off debug info (val=0)
```
    * void setTraceLevel(int val); 
```

On Cancel

> It will return NULL.

### How to use it ###

How to use xfiledialog :
http://code.google.com/p/xfiledialog/wiki/how_to_use_xfiledialog

How to compile xfiledialog:
http://code.google.com/p/xfiledialog/wiki/How_to_compile_xfiledialog

How to use xfiledialog in applet:  http://code.google.com/p/xfiledialog/wiki/How_to_use_xfiledialog_in_applet

### Usage: ###

  * This software is released into the public domain.
  * This software is provided "as is" with no expressed or implied warranty.


### Why ###

> Several serious restrictions of Java/Swing prevent Java from being adopted in modern Windows desktop apps. A well-known restriction is Java's File dialog.

Both of the two default filedialog classes in Java/Swing have serious limitations:

  * JFileChooser takes too long time to initialize. It's an important factor for sluggish Java startup.
  * No thumbnail preview mode in JFileChooser.
  * No multi-selection in AWT's FileDialog.
  * No implementation of filename filters in AWT's Filedialog under Windows.

> IMHO, a native Windows FileDialog that supports multi-selection and thumbnail preview mode is definitely required for desktop apps, especially graphic apps.

### Implementation and Credits: ###

Read the this page if you wish to modify the code and recompile it yourself.

> http://code.google.com/p/xfiledialog/wiki/The_implementation_of_XFileDialog

contributions:
> ExtensionsFilter in XFileDialog and  WinXP/X64 testing  were done by
> Jose Getino.

### Software projects which use xfiledialog ###

> Maple slideshow builder:  http://sites.google.com/site/jtvmaker/

> Email me if you know some projects using xfiledialog.



## Donation or Help: ##

  * A small donation is welcome if you are using it in commercial products.

> Donation Link: https://sites.google.com/site/jtvmaker/Home/xfiledialog-online-demo

  * For freeware, Open-source, or private software developers, you could help me in another product of mine (Maple slideshow builder) if you are interested in graphic apps.  It still needs testing, correcting English syntax errors, advice or some promotion.

> Maple Java slideshow builder: http://sites.google.com/site/jtvmaker/

> Email me if you wish to help.

> stevpan@gmail.com