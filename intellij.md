# Intelli J

## Config : File / Settings / Appearance&B / System Settings / HTTP Proxy

Manual proxy : localhost, port 3128
Exclusions see Wiki

## Config : File / Other Settings / Default Settings / ... / Maven

- Maven Home directory (or set it with M2_HOME): C:\Daten\P\maven3
- User settings file: C:\Daten\P\maven3\conf\settings.xml

## Config : File / Other Settings / Default Settings

- Editor / Spelling / Dictionaries: add ao/tools/intellij folder


## Config : File / Project Structure / Platform Settings

- Platform SDKs


## Per project (check after every import)

Use also the Default settings ('default' project)

### Config : File / Project Structure / Platform Settings

- Project SDK
- Project language level (is usually 6 instead of 7 with a JDK 7)

### Niceties

Enable Tool Buttons and Status Bar
Change Settings | Editor | Editor Tabs | Tab limit to a bigger number (e.g. 40)


### Issues

Comment Block (Ctrl-/) works only with the / on the numpad (https://youtrack.jetbrains.com/issue/IDEA-16116)


## File Saving

- Settings / Editor / General / Editor Tab / Mark Modified tabs with asterisk (does not seem to work)


## Import Maven project

Consider just opening the project?


### Settings

- [x] Import maven projects automatically
- Automatically download : [x] Sources

### import application as project, libraries as modules

### modules have ugly names like adapter (1) (com.six-group.ao.tfo.atm.conkey)

You can rename them (Refactor / Rename) to something unique


## Using IntelliJ

- Use the Packages View instead of the Project View

### Favourites

Ctrl-Alt-V (extract variable) = introduce local variable
Alt-Q (view context info) = display current method


### Quick Doc window can't be dismissed

Unpin the window ("restore popup"), as "Tool Window" it is much more difficult to dismiss...


### Tips unsorted

From https://www.youtube.com/watch?v=h8wRC7Qkcb8

double Shift = Search Anywhere (Goto Anything in Sublime?)
Disable Navigation Bar and use Alt-Left : popup navigation bar
Disable Tabs
Cmd-E : recent files (UNterschied zu Ctrl-Tab?)
S-C-i ähnlich wie Cmd-Q, aber zeigt Source in Popup

Navigate forward/backward (Ctrl-ALt-l/r): ähnlich wie Ctrl-Tab?
S-Cmd-F12 : maximize Editor
S-C-P : Presentation Mode
S-F4 Extract Window (to move it on 2nd screen)
Extend Selection (Ctrl-W on Windows, Mac?)

"Multi Caret" is the only thing in IJ that you must use the mouse
What is the key to introduce local variable?
Smart completino (e.g. something inheriting) Shift-Ctrl-Space
Completion: e.g. notnull introduces if(x!=null) ...
colored box upper right (green when no problems in file...): right-click it; together with Shift-F2? (Navigate next)
Use Ctrl-T for Refactorings?
Inspections can be run separately (via Find Action?)
Structural Search, e.g. to find empty catch blocks
chronon plugin to step back in time in the debugger
Quick Switch Scheme Shortcut? (Ctrl-` not possible with swiss german keyboard)-> for pair programming
Custom Menus: "Quick Lists"
Alt-F12 : Terminal
Restful client (find via Find Action)
Productivity Guide (Help Menu)



## Building

### IntelliJ 'make project'

- <kbd>Ctrl-F9</kbd> : Make Project
- <kbd>Shift-Ctrl-F9</kbd> : Compile <compilation_scope> (current project/module/package etc)
- difference 'make project' and 'compile project' :
  - compile : all files in scope
  - make : only changed files and dependent files

### Problems

- The Project Tool Window has a dropdown containing 'problems'


### Cleanup

- maven clean
- File / Invalidate Caches


## IntelliJ and Eclipse

### Eclipse Code Formatter plugin

http://plugins.jetbrains.com/plugin/6546

- Download it manually
- Settings / Plugins / Install plugin from disk
- Restart IntelliJ
- Settings / Other Settings / Eclipse Code Formatter :
  - use `cdfa-formatter.xml` from SVN as config file
  - use `cdfa.importorder` from SVN for import order

- Settings / Editor / General / Auto Import
  - Optimize imports on the fly
  - Add unambiguous imports on the fly
- Settings / Editor / Code Style / Java / Imports
  - Class count to use import with '*' : 50
  - Names count to use static import with '*' : 10


### Eclipse formatting w/o plugin

- Import order: http://stackoverflow.com/a/17194980/3686


### For eclipse users

- Settings / Keymap : Eclipse
  - Switch to unit test (Navigate/Test) : Shift-Alt-T
- Settings / Editor / File Types / Ignore Files and Folders : add ";.settings;.project;.classpath"

#### Javadoc

- create/update Javadoc
  - regular: just type /** and the Enter
  - Assign Alt-Shift-D to action *Fix doc comment* (Settings / Keymap)
- Javadoc mouse hover: Settings / Editor / General / Show quick documentation on mouse move


#### Navigation

Quick Hierarchy: Hierarchy Tool Window (Alt-8), appears only after Hierarchy has been created (Navigate / Type Hierarchy)


## Plugins

### Settings Repository

Stores settings on GitHub (or elsewhere), using access token

https://plugins.jetbrains.com/plugin/7566
https://github.com/develar/settings-repository

- local git repo clone: %idea.config.path%/config/settingsRepository/repository/.git
  (idea.config.path = %HOME%/.IntelliJIdea14 or ~/Library/Preferences/IntelliJIdeaXX)

=> does not work well across operating systems or multiple machines
=> manually managing the config directory with git is more flexible

### Presentation Assistant

- Displays other keyboard bindings
- good for pair programming

### Lines Sorter (org.sylfra.idea.plugins.linessorter)

- Default Binding: Alt-Shift-L (Edit / Sort Lines)

### Grep Console

Good for Maven Console etc.

https://plugins.jetbrains.com/plugin/?idea&pluginId=7125

### Markdown

The Markdown Navigator Plugin (com.vladsch.idea.multimarkdown) seems to have more features

### ASM Bytecode Outline
### CamelCase (de.netnexus.camelcaseplugin)
### Docker Integration
### Save Actions (com.dubreuia)
### SonarLint (org.sonarlint.idea)
### String Manipulation


## Key Bindings

- create Test (Alt-Enter) / create new test (Shift-Ctrl-T)
- run Test Shift-Ctrl-F10
- duplicate line: Ctrl-D
- move text selection: Shift-Alt-Up/Down
- move statement/method etc.: Shift-Ctrl-Up/Down
- Navigate Class (Eclipse Shift-Ctrl-T): Ctrl-N
- Display definition
- Reformat Ctrl-Alt-L / Reindent Ctrl-Alt-I

### debugging

F7 : step into
Alt-Shift-F7 : force step into
F8 : step over
Shift-F8 : step out
F9 : resume
Ctrl-F5 : rerun
Ctrl-F2 : stop
Shift-F9 : debug
Shift-F10 : run


### missing key bindings

Define them in Settings / Keymap; the first is the 'action')

- Fix doc comment : Alt-Shift-D


## Navigating the source

Instead of Eclipse's Ctrl-T, use the gutter icons (left of the declaration)

## JVM config

- for JUnit tests: Run/Debug Configurations / Default / JUnit / VM Options
  -Xms1000M -Xmx1000M -XX:MaxPermSize=512M

## JBoss config

- Run / Edit configurations
- Add Configuration / JBoss Server / Local
- c:\Daten\P\Java\jboss-eap-6.4\
- Configure logs: Alias "Server Log", Location: c:\Daten\P\Java\jboss-eap-6.4\standalone\log\server.log
- Deployment: add the EARs

## Datasource

- Tool Window Database, add datasource, Oracle (driver must be loaded first)

