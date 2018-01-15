---
title: Clearing the Screen
description: How to clear the screen of the Windows Console using the system function or programmatically using public API functions.
author: bitcrazed
ms.author: richturn
ms.topic: article
ms.prod: console
keywords: console, character mode applications, command line applications, terminal applications, console api
MS-HAID:
- '\_win32\_clearing\_the\_screen'
- 'base.clearing\_the\_screen'
- 'consoles.clearing\_the\_screen'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/desktop'
ms.assetid: 2097cc53-13b9-4f29-9d2c-feea56a27cb8
---

# Clearing the Screen


There are two ways to clear the screen in a console application.

## <span id="Example_1"></span><span id="example_1"></span><span id="EXAMPLE_1"></span>Example 1


The first method is to use the C run-time **system** function. The **system** function invokes the **cls** command provided by the command interpreter to clear the screen. Note that this is a highly inefficient way to clear the screen.

```ManagedCPlusPlus
#include <stdlib.h>

int main( void )
{
    system("cls");
    return 0;
}
```

## <span id="Example_2"></span><span id="example_2"></span><span id="EXAMPLE_2"></span>Example 2


The second method is to write a function to programmatically clear the screen using the [**FillConsoleOutputCharacter**](fillconsoleoutputcharacter.md) and [**FillConsoleOutputAttribute**](fillconsoleoutputattribute.md) functions. The following sample code demonstrates this technique.

```ManagedCPlusPlus
#include <windows.h>

void cls( HANDLE hConsole )
{
   COORD coordScreen = { 0, 0 };    // home for the cursor 
   DWORD cCharsWritten;
   CONSOLE_SCREEN_BUFFER_INFO csbi; 
   DWORD dwConSize;

// Get the number of character cells in the current buffer. 

   if( !GetConsoleScreenBufferInfo( hConsole, &csbi ))
   {
      return;
   }

   dwConSize = csbi.dwSize.X * csbi.dwSize.Y;

   // Fill the entire screen with blanks.

   if( !FillConsoleOutputCharacter( hConsole,        // Handle to console screen buffer 
                                    (TCHAR) ' ',     // Character to write to the buffer
                                    dwConSize,       // Number of cells to write 
                                    coordScreen,     // Coordinates of first cell 
                                    &cCharsWritten ))// Receive number of characters written
   {
      return;
   }

   // Get the current text attribute.

   if( !GetConsoleScreenBufferInfo( hConsole, &csbi ))
   {
      return;
   }

   // Set the buffer's attributes accordingly.

   if( !FillConsoleOutputAttribute( hConsole,         // Handle to console screen buffer 
                                    csbi.wAttributes, // Character attributes to use
                                    dwConSize,        // Number of cells to set attribute 
                                    coordScreen,      // Coordinates of first cell 
                                    &cCharsWritten )) // Receive number of characters written
   {
      return;
   }

   // Put the cursor at its home coordinates.

   SetConsoleCursorPosition( hConsole, coordScreen );
}

int main( void )
{
    HANDLE hStdout;

    hStdout = GetStdHandle(STD_OUTPUT_HANDLE);

    cls(hStdout);
    
    return 0;
}
```

 

 




