# Intelli J

## Config : File / Settings / Appearance&B / System Settings / HTTP Proxy

Manual proxy : localhost, port 3128
Exclusions see Wiki

## Config : File / Project Structure / Platform Settings

- Platform SDKs


## Per project (check after every import)

Use also the Default settings ('default' project)

### Config : File / Project Structure / Platform Settings

- Project SDK
- Project language level (is usually 6 instead of 7 with a JDK 7)

### Config : File / Settings / ... / Maven

- Maven Home directory (or set it with M2_HOME): C:\Daten\P\maven3
- User settings file: C:\Daten\P\maven3\conf\settings.xml

### Niceties

Switch on Tool Buttons and Status Bar



## Import Maven project

### Settings

- [x] Import maven projects automatically
- Automatically download : [x] Sources

### import application as project, libraries as modules

### modules have ugly names like adapter (1) (com.six-group.ao.tfo.atm.conkey)

You can rename them (Refactor / Rename) to something unique


## IntelliJ and Eclipse

### Eclipse Code Formatter plugin

http://plugins.jetbrains.com/plugin/6546

- Download it manually
- Settings / Plugins / Install plugin from disk
- Restart IntelliJ
- Settings / Other Settings / Eclipse Code Formatter :
  - use `cdfa-formatter.xml` from SVN as config file
  - use `cdfa.importorder` from SVN for import order

### For eclipse users

- Settings / IDE Settings / Keymap : Eclipse
  - Switch to unit test (Navigate/Test) : Shift-Alt-T
- Settings / IDE Settings / File Types / Ignore Files and Folders : add ";.settings;.project;.classpath"


## Key Bindings

- create Test (Alt-Enter) / create new test (Shift-Ctrl-T)
- run Test Shift-Ctrl-F10
- duplicate line: Ctrl-D
- move text selection: Shift-Alt-Up/Down
- move statement/method etc.: Shift-Ctrl-Up/Down

## Navigating the source

Instead of Eclipse's Ctrl-T, use the gutter icons (left of the declaration)


## JBoss config

- Run / Edit configurations
- Add Configuration / JBoss Server / Local
- c:\Daten\P\Java\jboss-eap-6.3\
- Configure logs: Server Log, c:\Daten\P\Java\jboss-eap-6.3\standalone\log\server.log
- Deployment: add the EARs
