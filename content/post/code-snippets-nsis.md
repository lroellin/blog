+++
date = "2014-08-22T23:42:26+02:00"
title = "Code Snippets: NSIS"
+++


NSIS is an installer framework you can use to create your own installer. If you've never seen NSIS: yes, it's old and looks like Assembler. But it works...

# Syntax

```nsis
/* Functions */
Function "Hello World"
	MessageBox MB_ICONINFORMATION "Hello World"
FunctionEnd

/* Macros */
!macro "Hello" UserName UserAge
	MessageBox MB_ICONINFORMATION "Hello ${USERNAME}"
	MessageBox MB_ICONINFORMATION "You are ${USERAGE} years old"
!macroend

!insertmacro "Hello" "John" "99"; Hello John/You are 99 years old

/* Control Statements */
!include "LogicLib.nsh"
If|IfNot|Unless..{ElseIf|ElseIfNot|ElseUnless}..[Else]..EndIf|EndUnless
AndIf|AndIfNot|AndUnless|OrIf|OrIfNot|OrUnless
Select..{Case[2|3|4|5]}..[CaseElse|Default]..EndSelect ; ${Break} needed

${IfNot} $cmdfw == '0'
${AndIfNot} $cmdfw == '1'
${AndIfNot} $cmdfw == ''
	MessageBox MB_ICONEXCLAMATION "Your arguments for the /SETFW-parameter are not valid, use /? to check for syntax."
	Quit
${EndIf}

${Unless} $CMDFW == ''
	StrCpy $FW $CMDFW
${Else}
	StrCpy $FW $GUIFW
${EndIf}

/* Loops */
While..{ExitWhile|Continue|Break}..EndWhile
For[Each]..{ExitFor|Continue|Break}..Next
Var i
${ForEach} $i 10 0 - 2
	MessageBox MB_OK $i
${Next}

/* Conditions */
a==b	// equal to
a!=b	// not equal to

/* Sections */
Section "" ; install section
SectionEnd

Section "Uninstall" ; uninstall section
SectionEnd

/* Read CLI parameters */
${GetParameters} "$CMD_ARGS"
${GetOptions} "$CMD_ARGS" "/PARAMETER" $variable

/* nsDialogs */
 /* Create and save handle */
${NSD_CreateText} 0u 11u 142u 11u ""
Pop $handle

 /* Set text or state on handle */
${NSD_SetText} $handle "Text"
${NSD_SetState} $handle "1|0"

/* Enable/disable control */
EnableWindow $handle 0

/* Get values (in Leave-function) */
${NSD_GetText} $handle $variable
${NSD_GetState} $handle $variable

/* Variables */
Var /GLOBAL variable ; create
StrCpy $variable "Moep" ; set

/* Misc. */
; Messagebox
; Default answer (Silent): No
; On IDYES: jump to continuemultiple
MessageBox MB_ICONEXCLAMATION|MB_YESNO "There is already an installation in progress or has crashed$r$nDo you want to install anyway?" /SD IDNO IDYES continuemultiple

; Test Messagebox with LogicLib
${If} ${Cmd} 'MessageBox MB_YESNO "Do you want to reuse your settings of the last installation?" IDYES'
	StrCpy $ReuseGUISettings "1"
${Else}
	StrCpy $ReuseGUISettings "0"
${EndIf}

/* Comments */
; Inline
# Inline
/* Multi-
line */
```

# Template

```nsis
/* Settings */
Name "Installer name"
!define VERSION "Product version"
!define RELEASE "Installer version"
!define /utcdate TIMESTAMP "%Y-%m-%d_%H-%M-%S"
!define INSTALLATIONNAME "name_with_underscores" ; technical name
!define FANCYNAME "Name written for humans" ; technical name
!define FILEDIR "src" ; where to get the files from
!define ARP "SoftwareMicrosoftWindowsCurrentVersionUninstall${INSTALLATIONNAME}" ; Registry path for Add/Remove programs
!define INSTALLER "${INSTALLATIONNAME}-${VERSION}-${RELEASE}" ; define file name
InstallDir "$PROGRAMFILES${INSTALLATIONNAME}"
OutFile "bin${INSTALLER}-setup.exe"

; ============================================================
/* Environment settings */
!define MULTIUSER_EXECUTIONLEVEL Admin
!define MULTIUSER_INIT_TEXT_ADMINREQUIRED "You need to have administrative privileges to run this setup"

; ============================================================
/* Include directories */
!addincludedir include ; include files
!addplugindir include ; plugins

; ============================================================
/* Compiler settings */
SetCompressor /SOLID lzma ; this is the best compression most of the time
!verbose 2 ; do not show the script and all default plugins on compile time (only on error)

; ============================================================
/* Header files needed for functions */
!include "MUI2.nsh"; UI
!include "LogicLib.nsh"; Flow control
!include "FileFunc.nsh"; File size
!include "WinVer.nsh"; Windows version handling
!include "nsDialogs.nsh"; Dialogs
!include "MultiUser.nsh"; Admin privileges

; ============================================================
/* Icon */
!define ICON "${FILEDIR}icon.ico"
!define MUI_ICON "${ICON}"
!define MUI_UNICON "${ICON}"

; ============================================================
/* Branding */
BrandingText "${BRANDING}"

; ============================================================
/* Pages */
!insertmacro MUI_PAGE_LICENSE "${FILEDIR}license.txt"
Page custom FunctionName FunctionNameLeave
!insertmacro MUI_PAGE_DIRECTORY
!insertmacro MUI_PAGE_INSTFILES

!insertmacro MUI_UNPAGE_CONFIRM
!insertmacro MUI_UNPAGE_INSTFILES

; ============================================================
/* Language */
!insertmacro MUI_LANGUAGE "English"

; ============================================================
/* Functions */

/* Helper functions */
Function "CheckRunning"
	System::Call 'kernel32::CreateMutexA(i 0, i 0, t "${INSTALLER}") ?e'
	Pop $R0
	${IfNot} $R0 == '0'
		${If} ${Cmd} 'MessageBox MB_ICONEXCLAMATION|MB_YESNO "There is already an installation in progress or has crashed$r$nDo you want to install anyway?" /SD IDNO IDNO'
			Quit
		${EndIf}
	${EndIf}
FunctionEnd

/* First functions called */
/* Functions to be called in silent mode either have to be placed in here or in the install section */
Function ".onInit"
	Call "CheckRunning" ; check if the installation is already running
	!insertmacro MULTIUSER_INIT ; is the user an Administrator (before Vista)?
FunctionEnd

; ============================================================
/* Install */
Section ""
	w7tbp::Start ; start progress bar in Taskbar (visible on Windows 6.1 or better)
	SetOutPath "$INSTDIR"
		File "${FILEDIR}README.txt"
	Call "GetSize" ; get and write the installation size
	WriteUninstaller "$INSTDIRuninstall.exe"
	/* Write the values to the registry, so CheckMK Agent shows up in the list of removable programs and to give some help for users */
	WriteRegStr HKLM "${ARP}" "DisplayName" "${FANCYNAME}"
	WriteRegStr HKLM "${ARP}" "DisplayVersion" "${VERSION}"
	WriteRegStr HKLM "${ARP}" "Publisher" "Publisher name"
	WriteRegStr HKLM "${ARP}" "URLInfoAbout" "URL"
	WriteRegStr HKLM "${ARP}" "Readme" "$INSTDIRREADME.txt"
	WriteRegStr HKLM "${ARP}" "DisplayIcon" "$INSTDIRicon.ico"
	WriteRegStr HKLM "${ARP}" "InstallLocation" "$INSTDIR"
	WriteRegStr HKLM "${ARP}" "UninstallString" "$INSTDIRuninstall.exe"
	WriteRegDWORD HKLM "${ARP}" "NoModify" 1
	WriteRegDWORD HKLM "${ARP}" "NoRepair" 1
SectionEnd

; ============================================================
/* Uninstall Functions */

/* First functions called */
/* Functions to be called in silent mode either have to be placed in here or in the uninstall section */
Function "un.onInit"
	!insertmacro MULTIUSER_UNINIT ; is the user an Administrator (before Vista)?
FunctionEnd

; ============================================================
/* Uninstall */

Section "Uninstall"
	DeleteRegKey HKLM "${ARP}"
	RMDir /r "$INSTDIR"
SectionEnd
```
