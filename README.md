# Mem
A memory library for Windows in C++.

There is an internal (MemIn.h", "MemIn.cpp") and an external ("MemEx.h", "MemEx.cpp") version, both use similar interfaces so you can easily port an external application to internal and vice-versa.

# FAQ
- Which files do I have to include in my project?
  - If you want to interact with another process, use `MemEx.h` and `MemEx.cpp`. If you want to interact with the virtual address space that your code is running on, use `MemIn.h` and `MemIn.cpp`.  You can even use both at the same time!
  
# Features
**[EX]** = Function is only available on the external version
 - x86-32 & x86-64 support
 - Unicode & Multibyte support
 - MD5Hash()
 - Hook, Unhook()
 - Call() **[EX]**
 - GetInstructionLength()
 - Inject() **[EX]**
 - ValueScan()
 - FindCodeCave(), FindCodeCaveBatch()
 - PatternScan(), AOBScan()
 - AOBToPattern()
 - ReadMultiLevelPointer()
 - Read(), Write(), Patch()
 - Nop(), Restore()
 - Copy(), Set(), Compare()
 - GetProcessIdByName(), GetProcessIdByWindow()
 - GetModuleBase()
 - EnumModules()
 - Open(), OpenByWindow() **[EX]**
 - WaitOpen(), WaitOpenByWindow() **[EX]**
 - Close(), IsOpened() **[EX]**
 - GetProcess(), GetPid() **[EX]**
 - AllocateSharedMemory(), CreateSharedMemory() **[EX]**
 - MapLocalViewOfFile(), UnmapLocalViewOfFile() **[EX]**
 - MapRemoteViewOfFile(), UnmapRemoteViewOfFile **[EX]**

# Example
```C++
#include "MemEx.h"

int main()
{
  MemEx m;
  m.WaitOpen("target.exe");
  
  uintptr_t address = m.AOBScan("64 A1 ?? ?? ?? ?? BA 08 28 7A 77 8B 48 ??", ScanBoundaries(SCAN_BOUNDARIES::MODULE, "some_module.dll"));
  m.Patch(address, "\x8B\x15", 2);
  
  return 0;
}
```
