#Tips for Using Eagle CAD

Tips, tricks, and reminders for doing stuff in Eagle.

##Authors Notes 
Having just learnt eagle I wanted a place to gather the tips and tricks I'm discovering.

###Making Parts 

#####Process
- Make symbol
- Make Package 
- Make Device 

Quickest way is often to edit existing elements rather that builing from scratch.  Fist I gather all the devices that I want to copy from in a new project library. Then I proceed to edit and rename things.


**Copying an element and nenaming in using command on the command line.**
```
copy existing.pac@yourlibname new.pac
```
*substitue package , symbol, or device names as appropriate. 

**Renaming elements using the commandcommand line**
*first open your library.
On the command line type: 
```
RENAME old.pac new.pac
```
The above is renaming a package (**xxx.pac**) though you can do the same for **.dev**(devices) and **.sym** (symbols)

##Updating Library Parts 
As you work with a board layout or schematic there I've found the need to tweek or change library symbols or packages.  This can be done by editing in the Library window and saving the library again.  This does not update the parts in your designs though. To do that you need to either:
```
hit update all under the menu->library
```
or for just the specific libray
```
choose the library from menu->library->update
```




##### Unanswered Questions.
Connector Pads.  Should they be laid as pads or made simply with rectangles in copper? I think pads may be best as not all boards will have a ground plain and its a good idea to connect these to ground.
