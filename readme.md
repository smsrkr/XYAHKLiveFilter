## XYAHKLiveFilter
[forum](http://www.xyplorer.com/xyfc/viewtopic.php?t=12588)|[code](https://www.github.com/smsrkr/XYAHKLiveFilter) | 
[releases](https://www.github.com/smsrkr/XYAHKLiveFilter/releases)|[bugreport](https://www.github.com/smsrkr/XYAHKLiveFilter/issues)<br>

A live-filter plugin for [XYplorer](http://www.xyplorer.com), made with [AutoHotkey](https://autohotkey.com)<br>
Live-filters the file list as you type into a textbox. Uses SC `filter`, so all VF syntax is available.

###INSTALL:
* Download the [release archive](/../../releases).
* Extract the downloaded archive into `<xyscripts>` (or wherever you want).
* Next attach the following xyscript to a CTB or to a UDC Run Script item or to the Catalog.<br>
  (it simply runs [`XYAHKLiveFilter.xys`](/XYAHKLiveFilter.xys))
```php
::load "<xyscripts>\xyahklivefilter.xys";
```
* That's it! Now just click the CTB or trigger the UDC and filter away!
* You can obviously also run the `XYAHKLiveFilter.xys` script itself directly to do the same.
* (Remember to modify the path in the scripts to match the actual path of the exe and xys in your setup.)
* Don't forget to read about usage & options below.
* [XYAHKLiveFilter.ctb.txt](/XYAHKLiveFilter.ctb.txt) provides slightly better CTB integration.<br>
  Execute this script to add a CTB with that snippet: `::snippet readfile("<xyscripts>\XYAHKLiveFilter.ctb.txt");`
  The CTB right-click menu has an option to "reset" that may help if XYAHKLiveFilter doesn't open.

###USAGE:
* By default, the filterbox pops up and stays over the right edge of the AB (addressbar), enabling AB if needed.<br>
  See `$SyncToAB` in [**OPTIONS**](#options) below for more details.
* If associated with a CTB, that CTB toggles the filterbox, and any other calling method refocuses it.<br>
  See `$NextAction` in [**OPTIONS**](#options) and in [`XYAHKLiveFilter.xys`](/XYAHKLiveFilter.xys) for more details.
* Press the focus hotkey (default:<kbd>CTRL</kbd>+<kbd>\`</kbd>) to focus the filterbox and <kbd>TAB</kbd>
  to refocus main XY window. (of course mouse can be used instead too.)<br>
  See `$FocusHotkey` in [**OPTIONS**](#options) and in [`XYAHKLiveFilter.xys`](/XYAHKLiveFilter.xys) for more details.
* Press <kbd>ESCAPE</kbd> while the filterbox is focused to close it. (also quits automatically when parent XY window is closed.)
* You might get pattern errors while entering complex/RegExp patterns. In that case, check the **P** checkbox to pause livemode,
  type the pattern, then uncheck it again to submit the pattern.
* Livemode can also be toggled with <kbd>ALT</kbd>+<kbd>P</kbd>. Press <kbd>ENTER</kbd> to force filter update while paused.
* If you use the script as a UDC with a keyboard shortcut, it's best to associate the same shortcut as `$FocusHotkey`.<br>
* The filterbox uses the same font and fontsize as the addressbar, so you can be sure it'll always match the zoom level of XY.


###OPTIONS:
These options may be modified in [`XYAHKLiveFilter.xys`](/XYAHKLiveFilter.xys).
* `$FocusHotkey`: this value is passed as the shortcut code to instantly focus the filterbox. The default value <tt>^\`</tt> means
  <kbd>CTRL</kbd>+<kbd>\`</kbd>. It follows [Authotkey's hotkey definition syntax](https://autohotkey.com/docs/Hotkeys.htm).
* `$SyncToAB`: if set to 1, the filterbox is positioned over right edge the of the addressbar. This is enabled by default.
  This also forces the AB to stay visible as long as livefilter is running (reverts back to last state when the filter is closed).<br>
  If `$SyncToAB` is not 1, then the filterbox is pops up and stays at the _topright_ of XY, and does not try to modify AB visibility.
* `$ABPadding`: Adjust this value only if the filterbox doesn't horizontal-align exactly with the addressbar.<br>
  The value should be a (small) integer: 0,3,-2 etc (default is 5).<br>
  The filterbox moves up/down this many pixels. Only effective when `$SyncToAB = 1`.
* `$Quote`: Controls how the VF pattern is quoted. Use `S` for single quotes (default) or `D` for double quotes.<br>
  Any quotes inside the pattern are taken care of - you don't have to type two quotes when you want one.
  The only advantage is that XY variables in pattern are resolved when `$Quote = "D"`
* `$NextAction`: Controls what subsequent calls to start XYAHKLiveFilter do, after it's been already opened. Values: 1: focus, 2: quit.<br>
  Now you can, for example, click the CTB once to open the filterbox, and click it again to focus.
* `$NextActionCTB`: Same as `$NextAction`, but controls what happens when run with a CTB.

Each of these variables may be set as empty, eg, `$FocusHotkey = "";`

###IMPORTANT:
* To work correctly, the exe/ahk must be launched using the XYscript.
* If the filterbox doesn't open, unset the permanent variables `$p_XYAHKLiveFilter_A`,`$p_XYAHKLiveFilter_B` and try again.<br>
  (CTB integration provides an easy RESET option on right click.)
* May also fail to run if an invalid hotkey string is supplied in `$FocusHotkey`.
* Some anti-malware suites apparently flag compiled ahk scripts as infected, which is a false alarm.
  If in doubt, you can always generate the exe yourself or directly run it as an ahk script.

Well, that's about it.
_Happy filtering!_
