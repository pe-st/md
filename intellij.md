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


## Key Bindings

- create Test (Alt-Enter) / create new test (Shift-Ctrl-T)
- run Test Shift-Ctrl-F10
- duplicate line: Ctrl-D
- move text selection: Shift-Alt-Up/Down
- move statement/method etc.: Shift-Ctrl-Up/Down
- Navigate Class (Eclipse Shift-Ctrl-T): Ctrl-N
- Display definition
- Reformat Ctrl-Alt-L / Reindent Ctrl-Alt-I

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

