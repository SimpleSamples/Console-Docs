---
title: GetConsoleMode function
description: Retrieves the current input mode of a console's input buffer or the current output mode of a console screen buffer.
author: bitcrazed
ms.author: richturn
ms.topic: article
ms.prod: console
keywords: console, character mode applications, command line applications, terminal applications, console api
MS-HAID:
- '\_win32\_getconsolemode'
- 'base.getconsolemode'
- 'consoles.getconsolemode'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/desktop'
ms.assetid: 49adf618-196d-4490-93ca-cd177807f58e

topic_type:
- apiref
api_name:
- GetConsoleMode
api_location:
- Kernel32.dll
- API-MS-Win-Core-Console-l1-1-0.dll
- KernelBase.dll
- API-MS-Win-DownLevel-Kernel32-l1-1-0.dll
- MinKernelBase.dll
api_type:
- DllExport
---

# GetConsoleMode function


Retrieves the current input mode of a console's input buffer or the current output mode of a console screen buffer.

Syntax
------

```ManagedCPlusPlus
BOOL WINAPI GetConsoleMode(
  _In_  HANDLE  hConsoleHandle,
  _Out_ LPDWORD lpMode
);
```

Parameters
----------

*hConsoleHandle* \[in\]  
A handle to the console input buffer or the console screen buffer. The handle must have the **GENERIC\_READ** access right. For more information, see [Console Buffer Security and Access Rights](console-buffer-security-and-access-rights.md).

*lpMode* \[out\]  
A pointer to a variable that receives the current mode of the specified buffer.

If the *hConsoleHandle* parameter is an input handle, the mode can be one or more of the following values. When a console is created, all input modes except **ENABLE\_WINDOW\_INPUT** are enabled by default.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="ENABLE_ECHO_INPUT"></span><span id="enable_echo_input"></span>
<strong>ENABLE_ECHO_INPUT</strong>
0x0004</td>
<td><p>Characters read by the [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md) function are written to the active screen buffer as they are read. This mode can be used only if the <strong>ENABLE_LINE_INPUT</strong> mode is also enabled.</p></td>
</tr>
<tr class="even">
<td><span id="ENABLE_INSERT_MODE"></span><span id="enable_insert_mode"></span>
<strong>ENABLE_INSERT_MODE</strong>
0x0020</td>
<td><p>When enabled, text entered in a console window will be inserted at the current cursor location and all text following that location will not be overwritten. When disabled, all following text will be overwritten.</p></td>
</tr>
<tr class="odd">
<td><span id="ENABLE_LINE_INPUT"></span><span id="enable_line_input"></span>
<strong>ENABLE_LINE_INPUT</strong>
0x0002</td>
<td><p>The [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md) function returns only when a carriage return character is read. If this mode is disabled, the functions return when one or more characters are available.</p></td>
</tr>
<tr class="even">
<td><span id="ENABLE_MOUSE_INPUT"></span><span id="enable_mouse_input"></span>
<strong>ENABLE_MOUSE_INPUT</strong>
0x0010</td>
<td><p>If the mouse pointer is within the borders of the console window and the window has the keyboard focus, mouse events generated by mouse movement and button presses are placed in the input buffer. These events are discarded by [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md), even when this mode is enabled.</p></td>
</tr>
<tr class="odd">
<td><span id="ENABLE_PROCESSED_INPUT"></span><span id="enable_processed_input"></span>
<strong>ENABLE_PROCESSED_INPUT</strong>
0x0001</td>
<td><p>CTRL+C is processed by the system and is not placed in the input buffer. If the input buffer is being read by [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md), other control keys are processed by the system and are not returned in the <strong>ReadFile</strong> or <strong>ReadConsole</strong> buffer. If the <strong>ENABLE_LINE_INPUT</strong> mode is also enabled, backspace, carriage return, and line feed characters are handled by the system.</p></td>
</tr>
<tr class="even">
<td><span id="ENABLE_QUICK_EDIT_MODE"></span><span id="enable_quick_edit_mode"></span>
<strong>ENABLE_QUICK_EDIT_MODE</strong>
0x0040</td>
<td><p>This flag enables the user to use the mouse to select and edit text.</p>
<p>To enable this mode, use <code>ENABLE_QUICK_EDIT_MODE | ENABLE_EXTENDED_FLAGS</code>. To disable this mode, use <strong>ENABLE_EXTENDED_FLAGS</strong> without this flag.</p></td>
</tr>
<tr class="odd">
<td><span id="ENABLE_WINDOW_INPUT"></span><span id="enable_window_input"></span>
<strong>ENABLE_WINDOW_INPUT</strong>
0x0008</td>
<td><p>User interactions that change the size of the console screen buffer are reported in the console's input buffer. Information about these events can be read from the input buffer by applications using the [<strong>ReadConsoleInput</strong>](readconsoleinput.md) function, but not by those using [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md).</p></td>
</tr>
<tr class="even">
<td><span id="ENABLE_VIRTUAL_TERMINAL_INPUT"></span><span id="enable_virtual_terminal_input"></span>
<strong>ENABLE_VIRTUAL_TERMINAL_INPUT</strong>
0x0200</td>
<td><p>Setting this flag directs the Virtual Terminal processing engine to convert user input received by the console window into [Console Virtual Terminal Sequences](console-virtual-terminal-sequences.md) that can be retrieved by a supporting application through [<strong>WriteFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [<strong>WriteConsole</strong>](writeconsole.md) functions.</p>
<p>The typical usage of this flag is intended in conjunction with ENABLE_VIRTUAL_TERMINAL_PROCESSING on the output handle to connect to an application that communicates exclusively via virtual terminal sequences.</p></td>
</tr>
<tr class="odd">
</tr>
<tr class="even">
</tr>
<tr class="odd">
</tr>
<tr class="even">
</tr>
<tr class="odd">
</tr>
<tr class="even">
</tr>
</tbody>
</table>

 

If the *hConsoleHandle* parameter is a screen buffer handle, the mode can be one or more of the following values. When a screen buffer is created, both output modes are enabled by default.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>Meaning</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><span id="ENABLE_PROCESSED_OUTPUT"></span><span id="enable_processed_output"></span>
<strong>ENABLE_PROCESSED_OUTPUT</strong>
0x0001</td>
<td><p>Characters written by the [<strong>WriteFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [<strong>WriteConsole</strong>](writeconsole.md) function or echoed by the [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md) function are parsed for ASCII control sequences, and the correct action is performed. Backspace, tab, bell, carriage return, and line feed characters are processed.</p></td>
</tr>
<tr class="even">
<td><span id="ENABLE_WRAP_AT_EOL_OUTPUT"></span><span id="enable_wrap_at_eol_output"></span>
<strong>ENABLE_WRAP_AT_EOL_OUTPUT</strong>
0x0002</td>
<td><p>When writing with [<strong>WriteFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [<strong>WriteConsole</strong>](writeconsole.md) or echoing with [<strong>ReadFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [<strong>ReadConsole</strong>](readconsole.md), the cursor moves to the beginning of the next row when it reaches the end of the current row. This causes the rows displayed in the console window to scroll up automatically when the cursor advances beyond the last row in the window. It also causes the contents of the console screen buffer to scroll up (discarding the top row of the console screen buffer) when the cursor advances beyond the last row in the console screen buffer. If this mode is disabled, the last character in the row is overwritten with any subsequent characters.</p></td>
</tr>
<tr class="odd">
<td><span id="ENABLE_VIRTUAL_TERMINAL_PROCESSING"></span><span id="enable_virtual_terminal_processing"></span>
<strong>ENABLE_VIRTUAL_TERMINAL_PROCESSING</strong>
0x0004</td>
<td><p>When writing with [<strong>WriteFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [<strong>WriteConsole</strong>](writeconsole.md), characters are parsed for VT100 and similar control character sequences that control cursor movement, color/font mode, and other operations that can also be performed via the existing Console APIs. For more information, see [Console Virtual Terminal Sequences](console-virtual-terminal-sequences.md).</p></td>
</tr>
<tr class="even">
<td><span id="DISABLE_NEWLINE_AUTO_RETURN"></span><span id="disable_newline_auto_return"></span>
<strong>DISABLE_NEWLINE_AUTO_RETURN</strong>
0x0008</td>
<td><p>When writing with [<strong>WriteFile</strong>](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [<strong>WriteConsole</strong>](writeconsole.md), this adds an additional state to end-of-line wrapping that can delay the cursor move and buffer scroll operations.</p>
<p>Normally when ENABLE_WRAP_AT_EOL_OUTPUT is set and text reaches the end of the line, the cursor will immediately move to the next line and the contents of the buffer will scroll up by one line. In contrast with this flag set, the scroll operation and cursor move is delayed until the next character arrives. The written character will be printed in the final position on the line and the cursor will remain above this character as if ENABLE_WRAP_AT_EOL_OUTPUT was off, but the next printable character will be printed as if ENABLE_WRAP_AT_EOL_OUTPUT is on. No overwrite will occur. Specifically, the cursor quickly advances down to the following line, a scroll is performed if necessary, the character is printed, and the cursor advances one more position.</p>
<p>The typical usage of this flag is intended in conjunction with setting ENABLE_VIRTUAL_TERMINAL_PROCESSING to better emulate a terminal emulator where writing the final character on the screen (in the bottom right corner) without triggering an immediate scroll is the desired behavior.</p></td>
</tr>
<tr class="odd">
<td><span id="ENABLE_LVB_GRID_WORLDWIDE"></span><span id="enable_lvb_grid_worldwide"></span>
<strong>ENABLE_LVB_GRID_WORLDWIDE</strong>
0x0010</td>
<td><p>The APIs for writing character attributes including [<strong>WriteConsoleOutput</strong>](writeconsoleoutput.md) and [<strong>WriteConsoleOutputAttribute</strong>](writeconsoleoutputattribute.md) allow the usage of flags from [character attributes](https://msdn.microsoft.com/library/windows/desktop/ms682088.aspx#_win32_font_attributes) to adjust the color of the foreground and background of text. Additionally, a range of DBCS flags was specified with the COMMON_LVB prefix. Historically, these flags only functioned in DBCS code pages for Chinese, Japanese, and Korean languages. With exception of the leading byte and trailing byte flags, the remaining flags describing line drawing and reverse video (swap foreground and background colors) can be useful for other languages to emphasize portions of output.</p>
<p>With exception of the leading byte and trailing byte flags, the remaining flags describing line drawing and reverse video (swap foreground and background colors) can be useful for other languages to emphasize portions of output.</p>
<p>Setting this console mode flag will allow these attributes to be used in every code page on every language.</p>
<p>It is off by default to maintain compatibility with known applications that have historically taken advantage of the console ignoring these flags on non-CJK machines to store bits in these fields for their own purposes or by accident.</p>
<p>Note that using the ENABLE_VIRTUAL_TERMINAL_PROCESSING mode can result in LVB grid and reverse video flags being set while this flag is still off if the attached application requests underlining or inverse video via [Console Virtual Terminal Sequences](console-virtual-terminal-sequences.md).</p></td>
</tr>
<tr class="even">
</tr>
<tr class="odd">
</tr>
<tr class="even">
</tr>
</tbody>
</table>

 

Return value
------------

If the function succeeds, the return value is nonzero.

If the function fails, the return value is zero. To get extended error information, call [**GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360).

Remarks
-------

A console consists of an input buffer and one or more screen buffers. The mode of a console buffer determines how the console behaves during input or output (I/O) operations. One set of flag constants is used with input handles, and another set is used with screen buffer (output) handles. Setting the output modes of one screen buffer does not affect the output modes of other screen buffers.

The **ENABLE\_LINE\_INPUT** and **ENABLE\_ECHO\_INPUT** modes only affect processes that use [**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [**ReadConsole**](readconsole.md) to read from the console's input buffer. Similarly, the **ENABLE\_PROCESSED\_INPUT** mode primarily affects **ReadFile** and **ReadConsole** users, except that it also determines whether CTRL+C input is reported in the input buffer (to be read by the [**ReadConsoleInput**](readconsoleinput.md) function) or is passed to a function defined by the application.

The **ENABLE\_WINDOW\_INPUT** and **ENABLE\_MOUSE\_INPUT** modes determine whether user interactions involving window resizing and mouse actions are reported in the input buffer or discarded. These events can be read by [**ReadConsoleInput**](readconsoleinput.md), but they are always filtered by [**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467) and [**ReadConsole**](readconsole.md).

The **ENABLE\_PROCESSED\_OUTPUT** and **ENABLE\_WRAP\_AT\_EOL\_OUTPUT** modes only affect processes using [**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467) or [**ReadConsole**](readconsole.md) and [**WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747) or [**WriteConsole**](writeconsole.md).

To change a console's I/O modes, call [**SetConsoleMode**](setconsolemode.md) function.

Examples
--------

For an example, see [Reading Input Buffer Events](reading-input-buffer-events.md).

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Minimum supported client</p></td>
<td><p>Windows 2000 Professional [desktop apps only]</p></td>
</tr>
<tr class="even">
<td><p>Minimum supported server</p></td>
<td><p>Windows 2000 Server [desktop apps only]</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wincon.h (include Windows.h)</td>
</tr>
<tr class="even">
<td><p>Library</p></td>
<td>Kernel32.lib</td>
</tr>
<tr class="odd">
<td><p>DLL</p></td>
<td>Kernel32.dll</td>
</tr>
<tr class="even">
</tr>
<tr class="odd">
</tr>
<tr class="even">
</tr>
</tbody>
</table>

## <span id="see_also"></span>See also


[Console Functions](console-functions.md)

[Console Modes](console-modes.md)

[**ReadConsole**](readconsole.md)

[**ReadConsoleInput**](readconsoleinput.md)

[**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467)

[**SetConsoleMode**](setconsolemode.md)

[**WriteConsole**](writeconsole.md)

[**WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747)

 

 




