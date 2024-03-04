# nls_933w.dll
# WIN32M.SYS

Note.
*WIN32M.SYS was extracted from nls_933.dll*

![image](https://github.com/loneicewolf/nls_933w_dll/assets/68499986/027d162a-bbd8-43dc-8d77-898060bb7998)


```
Small note: sometimes named
- nls_933w_dll
- nls_933w.dll

- WIN32M_SYS
- WIN32M.SYS

Just as fanny.bmp is sometimes named "fanny_bmp" and "fanny.bmp"

Refs:
- https://github.com/Yara-Rules/rules/blob/master/malware/APT_Equation.yar
- https://securelist.com/inside-the-equationdrug-espionage-platform/69203/
- https://www.antiy.net/p/a-trojan-that-can-modify-the-hard-disk-firmware/
- https://www.antiy.net/wp-content/uploads/A_TROJAN_THAT_CAN_MODIFY_THE_HARD_DISK_FIRMWARE.pdf

```



```
$ file nls_933w.dll 
nls_933w.dll: PE32 executable (DLL) (GUI) Intel 80386, for MS Windows

$ for ALGO in {md5sum,sha1sum,sha224sum,sha256sum,sha384sum,sha512sum}; do $ALGO nls_933w.dll; done
$ SUMS
ff2b50f371eb26f22eb8a2118e9ab0e015081500  nls_933w.dll
a67ecb844ca20ae3c934ebb1683190376f3aca1c9d72b7d37b57eee2  nls_933w.dll
83d14ce2dcfc852791d20cd78066ba5a2b39eb503e12e33f2ef0b1a46c68de73  nls_933w.dll
2046f8a25abc661a805f202a3052b2d19a9a97eb66d94e6f8736b9b2b8f3640e6d8b5f73a87eb5e23432253ab4abc71c  nls_933w.dll
b82aae750e138199cbd61586a033a106a9aa2b4d626d9b7d9028a753205505c8261f9457b23bf24d7ac7306d89e95dfbbcffbce7f0269ce8c15af9ea37b9a786  nls_933w.dll


$ rabin2 -E nls_933w.dll
# normal output

[Exports]
nth paddr      vaddr      bind   type size lib          name      demangled
―――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
1   0x000007f4 0x100013f4 GLOBAL FUNC 0    nls_933w.dll Ordinal_1
1   0x000007dd 0x100013dd GLOBAL FUNC 0    nls_933w.dll Ordinal_2
1   0x000007f0 0x100013f0 GLOBAL FUNC 0    nls_933w.dll Ordinal_3
1   0x00000808 0x10001408 GLOBAL FUNC 0    nls_933w.dll Ordinal_4
1   0x00000825 0x10001425 GLOBAL FUNC 0    nls_933w.dll Ordinal_5


$ rabin2 -qqE nls_933w.dll
$ # or, cleaner output:
$ # basically this is (often) for rundll32, e.g rundll32.exe <DLL_FILE.dll>, _Start@(), or rundll32.exe <DLL_FILE.dll>, Ordinal_3
Ordinal_1
Ordinal_2
Ordinal_3
Ordinal_4
Ordinal_5


$ rabin2 -I nls_933w.dll
arch     x86
baddr    0x10000000
binsz    212480
bintype  pe
bits     32
canary   true
injprot  false
retguard false
class    PE32
cmp.csum 0x000369ba
compiled Tue Jun 15 18:23:37 2010
crypto   false
endian   little
havecode true
hdr.csum 0x00000000
laddr    0x0
lang     msvc
linenum  true
lsyms    true
machine  i386
nx       false
os       windows
overlay  false
cc       cdecl
pic      false
relocs   false
signed   false
sanitize false
static   false
stripped false
subsys   Windows GUI
va       true


$ rabin2 -R nls_933w.dll 
[Relocations]
vaddr      paddr      type   name
―――――――――――――――――――――――――――――――――
0x0002dbbc 0x00028898 SET_32 MSVCRT.dll_strlen
0x0002dbc6 0x000288b8 SET_32 MSVCRT.dll_strncat
0x0002dbd0 0x000288b4 SET_32 MSVCRT.dll__except_handler3
0x0002dbe4 0x000288b0 SET_32 MSVCRT.dll_memcpy
0x0002dbee 0x000288ac SET_32 MSVCRT.dll___CxxFrameHandler
0x0002dc02 0x000288a8 SET_32 MSVCRT.dll_strncpy
0x0002dc0c 0x000288a4 SET_32 MSVCRT.dll__purecall
0x0002dc18 0x000288a0 SET_32 MSVCRT.dll_memset
0x0002dc22 0x0002889c SET_32 MSVCRT.dll_free
0x0002dc36 0x00028894 SET_32 MSVCRT.dll__initterm
0x0002dc42 0x00028890 SET_32 MSVCRT.dll_malloc
0x0002dc4c 0x0002888c SET_32 MSVCRT.dll__adjust_fdiv
0x0002dc5c 0x0002883c SET_32 KERNEL32.dll_GetSystemDirectoryA
0x0002dc72 0x00028840 SET_32 KERNEL32.dll_DeleteFileA
0x0002dc80 0x00028844 SET_32 KERNEL32.dll_CloseHandle
0x0002dc8e 0x00028848 SET_32 KERNEL32.dll_WriteFile
0x0002dc9a 0x0002884c SET_32 KERNEL32.dll_CreateFileA
0x0002dca8 0x00028850 SET_32 KERNEL32.dll_SizeofResource
0x0002dcba 0x00028854 SET_32 KERNEL32.dll_LockResource
0x0002dcca 0x00028858 SET_32 KERNEL32.dll_LoadResource
0x0002dcda 0x0002885c SET_32 KERNEL32.dll_FindResourceA
0x0002dcea 0x00028860 SET_32 KERNEL32.dll_LocalAlloc
0x0002dcf8 0x00028864 SET_32 KERNEL32.dll_LocalFree
0x0002dd04 0x00028868 SET_32 KERNEL32.dll_LocalReAlloc
0x0002dd14 0x0002886c SET_32 KERNEL32.dll_GetLastError
0x0002dd32 0x0002893c SET_32 SHLWAPI.dll_SHDeleteKeyA
0x0002dd4e 0x00028934 SET_32 SETUPAPI.dll_SetupDiDestroyDeviceInfoList
0x0002dd6e 0x00028930 SET_32 SETUPAPI.dll_SetupDiEnumDeviceInfo
0x0002dd86 0x0002892c SET_32 SETUPAPI.dll_SetupDiGetClassDevsA
0x0002dd9e 0x00028928 SET_32 SETUPAPI.dll_SetupDiClassGuidsFromNameA
0x0002ddbc 0x00028924 SET_32 SETUPAPI.dll_CM_Free_Log_Conf_Handle
0x0002ddd6 0x00028920 SET_32 SETUPAPI.dll_CM_Free_Res_Des_Handle
0x0002ddf0 0x0002891c SET_32 SETUPAPI.dll_CM_Get_Next_Res_Des
0x0002de06 0x00028918 SET_32 SETUPAPI.dll_CM_Get_First_Log_Conf
0x0002de1e 0x00028914 SET_32 SETUPAPI.dll_CM_Get_Res_Des_Data
0x0002de34 0x00028910 SET_32 SETUPAPI.dll_CM_Get_Res_Des_Data_Size
0x0002de50 0x0002890c SET_32 SETUPAPI.dll_SetupDiGetDeviceRegistryPropertyA
0x0002de82 0x0002880c SET_32 ADVAPI32.dll_AdjustTokenPrivileges
0x0002de9a 0x00028818 SET_32 ADVAPI32.dll_LookupPrivilegeValueA
0x0002deb2 0x00028814 SET_32 ADVAPI32.dll_OpenProcessToken
0x0002dec6 0x00028810 SET_32 ADVAPI32.dll_RegCloseKey
0x0002ded4 0x00028800 SET_32 ADVAPI32.dll_RegSetValueExA
0x0002dee6 0x00028808 SET_32 ADVAPI32.dll_RegCreateKeyExA
0x0002def8 0x00028804 SET_32 ADVAPI32.dll_RegOpenKeyExA
0x0002df16 0x000288bc SET_32 MSVCRT.dll_??2@YAPAXI@Z
0x0002df26 0x000288c0 SET_32 MSVCRT.dll_fwrite
0x0002df30 0x000288c4 SET_32 MSVCRT.dll_remove
0x0002df3a 0x000288c8 SET_32 MSVCRT.dll_fclose
0x0002df44 0x000288cc SET_32 MSVCRT.dll_fopen
0x0002df4c 0x000288d0 SET_32 MSVCRT.dll_fread
0x0002df54 0x000288d4 SET_32 MSVCRT.dll__stat
0x0002df5c 0x000288d8 SET_32 MSVCRT.dll_strstr
0x0002df66 0x000288dc SET_32 MSVCRT.dll_time
0x0002df6e 0x000288e0 SET_32 MSVCRT.dll_memmove
0x0002df78 0x000288e4 SET_32 MSVCRT.dll_realloc
0x0002df82 0x000288e8 SET_32 MSVCRT.dll_strncmp
0x0002df8c 0x000288ec SET_32 MSVCRT.dll_calloc
0x0002df96 0x000288f0 SET_32 MSVCRT.dll_wcslen
0x0002dfa0 0x000288f4 SET_32 MSVCRT.dll_memchr
0x0002dfaa 0x000288f8 SET_32 MSVCRT.dll_isdigit
0x0002dfb4 0x000288fc SET_32 MSVCRT.dll_toupper
0x0002dfbe 0x00028900 SET_32 MSVCRT.dll_isspace
0x0002dfc8 0x00028904 SET_32 MSVCRT.dll_isgraph
0x0002dfd2 0x00028884 SET_32 KERNEL32.dll_GetCurrentProcess
0x0002dfe6 0x00028824 SET_32 KERNEL32.dll_GetProcAddress
0x0002dff8 0x00028828 SET_32 KERNEL32.dll_GetModuleHandleA
0x0002e00c 0x0002882c SET_32 KERNEL32.dll_DeviceIoControl
0x0002e01e 0x00028830 SET_32 KERNEL32.dll_GetSystemInfo
0x0002e02e 0x00028834 SET_32 KERNEL32.dll_GetVersionExA
0x0002e03e 0x00028838 SET_32 KERNEL32.dll_LoadLibraryA
0x0002e04e 0x00028880 SET_32 KERNEL32.dll_WideCharToMultiByte
0x0002e064 0x0002887c SET_32 KERNEL32.dll_MultiByteToWideChar
0x0002e07a 0x00028878 SET_32 KERNEL32.dll_LCMapStringA
0x0002e08a 0x00028874 SET_32 KERNEL32.dll_LCMapStringW
0x0002e09a 0x00028870 SET_32 KERNEL32.dll_GetStringTypeA
0x0002e0ac 0x00028820 SET_32 KERNEL32.dll_GetStringTypeW

76 relocations


$ rabin2 -S nls_933w.dll 
[Sections]
nth paddr          size vaddr         vsize perm type name
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
0   0x00000400  0x28400 0x10001000  0x29000 -r-x ---- .text
1   0x00028800   0x4200 0x1002a000   0x5000 -r-- ---- .rdata
2   0x0002ca00    0x800 0x1002f000   0x1000 -rw- ---- .data
3   0x0002d200   0x4e00 0x10030000   0x5000 -r-- ---- .rsrc
4   0x00032000   0x1e00 0x10035000   0x2000 -r-- ---- .reloc
```


```
$ file WIN32M.SYS 
WIN32M.SYS: PE32 executable (native) Intel 80386, for MS Windows

$ for ALGO in {md5sum,sha1sum,sha224sum,sha256sum,sha384sum,sha512sum}; do $ALGO WIN32M.SYS; done
2b444ac5209a8b4140dd6b747a996653  WIN32M.SYS
645678c4ed9bbdd641c4ff4dcb1825c262b2d879  WIN32M.SYS
22baf875e4f2182ded216fae1c58e9554d2728f4998b53c2c5214fc3  WIN32M.SYS
07fc80ecaa8f12f0d57fbf9627d5505b8f969a84fc3907c31dd68f5022edf643  WIN32M.SYS
a84b4c03775a94f2e4288a2337078a66f27929a80977a744d1bb00afaf6b5a605d68435eb204948deab64c82f94cd297  WIN32M.SYS
9adf7d3e218110323f2a5930cb2bfaf2b948b45947ad951ac43619b1440031b77bd61c43719a00085bae0337746458b6e9e6729885503e8a5295086f15b3a362  WIN32M.SYS




$ rabin2 -g WIN32M.SYS
ERROR: Missing bin header main
ERROR: Missing bin header dwarf
[Sections]

nth paddr         size vaddr        vsize perm type name
――――――――――――――――――――――――――――――――――――――――――――――――――――――――
0   0x00000300  0x3b80 0x00010300  0x3b80 -r-x ---- .text
1   0x00003e80   0x200 0x00013e80   0x200 -r-- ---- .rdata
2   0x00004080   0x100 0x00014080   0x100 -rw- ---- .data
3   0x00004180   0x780 0x00014180   0x780 -rwx ---- INIT
4   0x00004900   0x300 0x00014900   0x300 -r-- ---- .reloc

[Segments]

nth paddr  size vaddr  vsize perm type name
―――――――――――――――――――――――――――――――――――――――――――

[Entrypoints]
vaddr=0x00010812 paddr=0x00000812 haddr=0x000000f0 type=program

1 entrypoints
[Constructors]

0 entrypoints
[Imports]
nth vaddr      bind type lib          name
――――――――――――――――――――――――――――――――――――――――――
1   0x00013ed0 NONE FUNC ntoskrnl.exe KeSetEvent
2   0x00013ed4 NONE FUNC ntoskrnl.exe KeWaitForMultipleObjects
3   0x00013ed8 NONE FUNC ntoskrnl.exe _allmul
4   0x00013edc NONE FUNC ntoskrnl.exe ZwSetInformationThread
5   0x00013ee0 NONE FUNC ntoskrnl.exe PsTerminateSystemThread
6   0x00013ee4 NONE FUNC ntoskrnl.exe KeSetPriorityThread
7   0x00013ee8 NONE FUNC ntoskrnl.exe KeGetCurrentThread
8   0x00013eec NONE FUNC ntoskrnl.exe ZwClose
9   0x00013ef0 NONE FUNC ntoskrnl.exe PsCreateSystemThread
10  0x00013ef4 NONE FUNC ntoskrnl.exe KeInitializeEvent
11  0x00013ef8 NONE FUNC ntoskrnl.exe KeWaitForSingleObject
12  0x00013efc NONE FUNC ntoskrnl.exe KeInitializeMutex
13  0x00013f00 NONE FUNC ntoskrnl.exe IoAcquireCancelSpinLock
14  0x00013f04 NONE FUNC ntoskrnl.exe READ_REGISTER_UCHAR
15  0x00013f08 NONE FUNC ntoskrnl.exe WRITE_REGISTER_UCHAR
16  0x00013f0c NONE FUNC ntoskrnl.exe WRITE_REGISTER_BUFFER_USHORT
17  0x00013f10 NONE FUNC ntoskrnl.exe READ_REGISTER_BUFFER_USHORT
18  0x00013f14 NONE FUNC ntoskrnl.exe READ_REGISTER_ULONG
19  0x00013f18 NONE FUNC ntoskrnl.exe WRITE_REGISTER_ULONG
20  0x00013f1c NONE FUNC ntoskrnl.exe MmGetPhysicalAddress
21  0x00013f20 NONE FUNC ntoskrnl.exe MmAllocateContiguousMemorySpecifyCache
22  0x00013f24 NONE FUNC ntoskrnl.exe MmFreeContiguousMemorySpecifyCache
23  0x00013f28 NONE FUNC ntoskrnl.exe MmAllocateNonCachedMemory
24  0x00013f2c NONE FUNC ntoskrnl.exe MmFreeNonCachedMemory
25  0x00013f30 NONE FUNC ntoskrnl.exe READ_REGISTER_USHORT
26  0x00013f34 NONE FUNC ntoskrnl.exe WRITE_REGISTER_USHORT
27  0x00013f38 NONE FUNC ntoskrnl.exe MmMapIoSpace
28  0x00013f3c NONE FUNC ntoskrnl.exe MmUnmapIoSpace
29  0x00013f40 NONE FUNC ntoskrnl.exe KeInsertQueueDpc
30  0x00013f44 NONE FUNC ntoskrnl.exe KeSetTargetProcessorDpc
31  0x00013f48 NONE FUNC ntoskrnl.exe IoReleaseCancelSpinLock
32  0x00013f4c NONE FUNC ntoskrnl.exe KeInitializeSpinLock
33  0x00013f50 NONE FUNC ntoskrnl.exe IoCreateDevice
34  0x00013f54 NONE FUNC ntoskrnl.exe IoCreateSymbolicLink
35  0x00013f58 NONE FUNC ntoskrnl.exe ExAllocatePoolWithTag
36  0x00013f5c NONE FUNC ntoskrnl.exe RtlCopyUnicodeString
37  0x00013f60 NONE FUNC ntoskrnl.exe IofCompleteRequest
38  0x00013f64 NONE FUNC ntoskrnl.exe ExFreePoolWithTag
39  0x00013f68 NONE FUNC ntoskrnl.exe RtlInitUnicodeString
40  0x00013f6c NONE FUNC ntoskrnl.exe IoDeleteSymbolicLink
41  0x00013f70 NONE FUNC ntoskrnl.exe IoDeleteDevice
42  0x00013f74 NONE FUNC ntoskrnl.exe KeNumberProcessors
43  0x00013f78 NONE FUNC ntoskrnl.exe KeCancelTimer
44  0x00013f7c NONE FUNC ntoskrnl.exe KeInitializeDpc
45  0x00013f80 NONE FUNC ntoskrnl.exe KeInitializeTimerEx
46  0x00013f84 NONE FUNC ntoskrnl.exe KeReleaseMutex
47  0x00013f88 NONE FUNC ntoskrnl.exe KeSetTimerEx
1   0x00013e80 NONE FUNC HAL.dll      KeRaiseIrqlToDpcLevel
2   0x00013e84 NONE FUNC HAL.dll      KfRaiseIrql
3   0x00013e88 NONE FUNC HAL.dll      HalGetBusData
4   0x00013e8c NONE FUNC HAL.dll      HalGetBusDataByOffset
5   0x00013e90 NONE FUNC HAL.dll      HalSetBusDataByOffset
6   0x00013e94 NONE FUNC HAL.dll      KeGetCurrentIrql
7   0x00013e98 NONE FUNC HAL.dll      WRITE_PORT_ULONG
8   0x00013e9c NONE FUNC HAL.dll      WRITE_PORT_USHORT
9   0x00013ea0 NONE FUNC HAL.dll      READ_PORT_USHORT
10  0x00013ea4 NONE FUNC HAL.dll      READ_PORT_ULONG
11  0x00013ea8 NONE FUNC HAL.dll      READ_PORT_BUFFER_USHORT
12  0x00013eac NONE FUNC HAL.dll      WRITE_PORT_BUFFER_USHORT
13  0x00013eb0 NONE FUNC HAL.dll      KeStallExecutionProcessor
14  0x00013eb4 NONE FUNC HAL.dll      WRITE_PORT_UCHAR
15  0x00013eb8 NONE FUNC HAL.dll      READ_PORT_UCHAR
16  0x00013ebc NONE FUNC HAL.dll      HalGetInterruptVector
17  0x00013ec0 NONE FUNC HAL.dll      KfAcquireSpinLock
18  0x00013ec4 NONE FUNC HAL.dll      KfReleaseSpinLock
19  0x00013ec8 NONE FUNC HAL.dll      KfLowerIrql

[Symbols]
nth paddr      vaddr      bind type size lib          name                                       demangled
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
1   0x00003ed0 0x00013ed0 NONE FUNC 0    ntoskrnl.exe imp.KeSetEvent
2   0x00003ed4 0x00013ed4 NONE FUNC 0    ntoskrnl.exe imp.KeWaitForMultipleObjects
3   0x00003ed8 0x00013ed8 NONE FUNC 0    ntoskrnl.exe imp._allmul
4   0x00003edc 0x00013edc NONE FUNC 0    ntoskrnl.exe imp.ZwSetInformationThread
5   0x00003ee0 0x00013ee0 NONE FUNC 0    ntoskrnl.exe imp.PsTerminateSystemThread
6   0x00003ee4 0x00013ee4 NONE FUNC 0    ntoskrnl.exe imp.KeSetPriorityThread
7   0x00003ee8 0x00013ee8 NONE FUNC 0    ntoskrnl.exe imp.KeGetCurrentThread
8   0x00003eec 0x00013eec NONE FUNC 0    ntoskrnl.exe imp.ZwClose
9   0x00003ef0 0x00013ef0 NONE FUNC 0    ntoskrnl.exe imp.PsCreateSystemThread
10  0x00003ef4 0x00013ef4 NONE FUNC 0    ntoskrnl.exe imp.KeInitializeEvent
11  0x00003ef8 0x00013ef8 NONE FUNC 0    ntoskrnl.exe imp.KeWaitForSingleObject
12  0x00003efc 0x00013efc NONE FUNC 0    ntoskrnl.exe imp.KeInitializeMutex
13  0x00003f00 0x00013f00 NONE FUNC 0    ntoskrnl.exe imp.IoAcquireCancelSpinLock
14  0x00003f04 0x00013f04 NONE FUNC 0    ntoskrnl.exe imp.READ_REGISTER_UCHAR
15  0x00003f08 0x00013f08 NONE FUNC 0    ntoskrnl.exe imp.WRITE_REGISTER_UCHAR
16  0x00003f0c 0x00013f0c NONE FUNC 0    ntoskrnl.exe imp.WRITE_REGISTER_BUFFER_USHORT
17  0x00003f10 0x00013f10 NONE FUNC 0    ntoskrnl.exe imp.READ_REGISTER_BUFFER_USHORT
18  0x00003f14 0x00013f14 NONE FUNC 0    ntoskrnl.exe imp.READ_REGISTER_ULONG
19  0x00003f18 0x00013f18 NONE FUNC 0    ntoskrnl.exe imp.WRITE_REGISTER_ULONG
20  0x00003f1c 0x00013f1c NONE FUNC 0    ntoskrnl.exe imp.MmGetPhysicalAddress
21  0x00003f20 0x00013f20 NONE FUNC 0    ntoskrnl.exe imp.MmAllocateContiguousMemorySpecifyCache
22  0x00003f24 0x00013f24 NONE FUNC 0    ntoskrnl.exe imp.MmFreeContiguousMemorySpecifyCache
23  0x00003f28 0x00013f28 NONE FUNC 0    ntoskrnl.exe imp.MmAllocateNonCachedMemory
24  0x00003f2c 0x00013f2c NONE FUNC 0    ntoskrnl.exe imp.MmFreeNonCachedMemory
25  0x00003f30 0x00013f30 NONE FUNC 0    ntoskrnl.exe imp.READ_REGISTER_USHORT
26  0x00003f34 0x00013f34 NONE FUNC 0    ntoskrnl.exe imp.WRITE_REGISTER_USHORT
27  0x00003f38 0x00013f38 NONE FUNC 0    ntoskrnl.exe imp.MmMapIoSpace
28  0x00003f3c 0x00013f3c NONE FUNC 0    ntoskrnl.exe imp.MmUnmapIoSpace
29  0x00003f40 0x00013f40 NONE FUNC 0    ntoskrnl.exe imp.KeInsertQueueDpc
30  0x00003f44 0x00013f44 NONE FUNC 0    ntoskrnl.exe imp.KeSetTargetProcessorDpc
31  0x00003f48 0x00013f48 NONE FUNC 0    ntoskrnl.exe imp.IoReleaseCancelSpinLock
32  0x00003f4c 0x00013f4c NONE FUNC 0    ntoskrnl.exe imp.KeInitializeSpinLock
33  0x00003f50 0x00013f50 NONE FUNC 0    ntoskrnl.exe imp.IoCreateDevice
34  0x00003f54 0x00013f54 NONE FUNC 0    ntoskrnl.exe imp.IoCreateSymbolicLink
35  0x00003f58 0x00013f58 NONE FUNC 0    ntoskrnl.exe imp.ExAllocatePoolWithTag
36  0x00003f5c 0x00013f5c NONE FUNC 0    ntoskrnl.exe imp.RtlCopyUnicodeString
37  0x00003f60 0x00013f60 NONE FUNC 0    ntoskrnl.exe imp.IofCompleteRequest
38  0x00003f64 0x00013f64 NONE FUNC 0    ntoskrnl.exe imp.ExFreePoolWithTag
39  0x00003f68 0x00013f68 NONE FUNC 0    ntoskrnl.exe imp.RtlInitUnicodeString
40  0x00003f6c 0x00013f6c NONE FUNC 0    ntoskrnl.exe imp.IoDeleteSymbolicLink
41  0x00003f70 0x00013f70 NONE FUNC 0    ntoskrnl.exe imp.IoDeleteDevice
42  0x00003f74 0x00013f74 NONE FUNC 0    ntoskrnl.exe imp.KeNumberProcessors
43  0x00003f78 0x00013f78 NONE FUNC 0    ntoskrnl.exe imp.KeCancelTimer
44  0x00003f7c 0x00013f7c NONE FUNC 0    ntoskrnl.exe imp.KeInitializeDpc
45  0x00003f80 0x00013f80 NONE FUNC 0    ntoskrnl.exe imp.KeInitializeTimerEx
46  0x00003f84 0x00013f84 NONE FUNC 0    ntoskrnl.exe imp.KeReleaseMutex
47  0x00003f88 0x00013f88 NONE FUNC 0    ntoskrnl.exe imp.KeSetTimerEx
1   0x00003e80 0x00013e80 NONE FUNC 0    HAL.dll      imp.KeRaiseIrqlToDpcLevel
2   0x00003e84 0x00013e84 NONE FUNC 0    HAL.dll      imp.KfRaiseIrql
3   0x00003e88 0x00013e88 NONE FUNC 0    HAL.dll      imp.HalGetBusData
4   0x00003e8c 0x00013e8c NONE FUNC 0    HAL.dll      imp.HalGetBusDataByOffset
5   0x00003e90 0x00013e90 NONE FUNC 0    HAL.dll      imp.HalSetBusDataByOffset
6   0x00003e94 0x00013e94 NONE FUNC 0    HAL.dll      imp.KeGetCurrentIrql
7   0x00003e98 0x00013e98 NONE FUNC 0    HAL.dll      imp.WRITE_PORT_ULONG
8   0x00003e9c 0x00013e9c NONE FUNC 0    HAL.dll      imp.WRITE_PORT_USHORT
9   0x00003ea0 0x00013ea0 NONE FUNC 0    HAL.dll      imp.READ_PORT_USHORT
10  0x00003ea4 0x00013ea4 NONE FUNC 0    HAL.dll      imp.READ_PORT_ULONG
11  0x00003ea8 0x00013ea8 NONE FUNC 0    HAL.dll      imp.READ_PORT_BUFFER_USHORT
12  0x00003eac 0x00013eac NONE FUNC 0    HAL.dll      imp.WRITE_PORT_BUFFER_USHORT
13  0x00003eb0 0x00013eb0 NONE FUNC 0    HAL.dll      imp.KeStallExecutionProcessor
14  0x00003eb4 0x00013eb4 NONE FUNC 0    HAL.dll      imp.WRITE_PORT_UCHAR
15  0x00003eb8 0x00013eb8 NONE FUNC 0    HAL.dll      imp.READ_PORT_UCHAR
16  0x00003ebc 0x00013ebc NONE FUNC 0    HAL.dll      imp.HalGetInterruptVector
17  0x00003ec0 0x00013ec0 NONE FUNC 0    HAL.dll      imp.KfAcquireSpinLock
18  0x00003ec4 0x00013ec4 NONE FUNC 0    HAL.dll      imp.KfReleaseSpinLock
19  0x00003ec8 0x00013ec8 NONE FUNC 0    HAL.dll      imp.KfLowerIrql
[Strings]
nth paddr vaddr len size section type string
――――――――――――――――――――――――――――――――――――――――――――
arch     x86
baddr    0x10000
binsz    19456
bintype  pe
bits     32
canary   true
injprot  false
retguard false
class    PE32
cmp.csum 0x000125fe
compiled Thu Aug 23 19:03:19 2001
crypto   false
endian   little
havecode true
hdr.csum 0x000125fe
laddr    0x0
lang     c
linenum  true
lsyms    true
machine  i386
nx       false
os       native
overlay  false
cc       cdecl
pic      false
relocs   false
signed   false
sanitize false
static   false
stripped false
subsys   Native
va       true
PE file header:
IMAGE_NT_HEADERS
  Signature : 0x4550
IMAGE_FILE_HEADERS
  Machine : 0x14c
  NumberOfSections : 0x5
  TimeDateStamp : 0x3b853757
  PointerToSymbolTable : 0x0
  NumberOfSymbols : 0x0
  SizeOfOptionalHeader : 0xe0
  Characteristics : 0x10e
IMAGE_OPTIONAL_HEADERS
  Magic : 0x10b
  MajorLinkerVersion : 0x7
  MinorLinkerVersion : 0x0
  SizeOfCode : 0x4300
  SizeOfInitializedData : 0x600
  SizeOfUninitializedData : 0x0
  AddressOfEntryPoint : 0x812
  BaseOfCode : 0x300
  BaseOfData : 0x3e80
  ImageBase : 0x10000
  SectionAlignment : 0x80
  FileAlignment : 0x80
  MajorOperatingSystemVersion : 0x5
  MinorOperatingSystemVersion : 0x1
  MajorImageVersion : 0x5
  MinorImageVersion : 0x1
  MajorSubsystemVersion : 0x5
  MinorSubsystemVersion : 0x1
  Win32VersionValue : 0x0
  SizeOfImage : 0x4c00
  SizeOfHeaders : 0x300
  CheckSum : 0x125fe
  Subsystem : 0x1
  DllCharacteristics : 0x0
  SizeOfStackReserve : 0x40000
  SizeOfStackCommit : 0x1000
  SizeOfHeapReserve : 0x100000
  SizeOfHeapCommit : 0x1000
  LoaderFlags : 0x0
  NumberOfRvaAndSizes : 0x10
RICH_FIELDS
  Product: 61 Name: Linker700 Version: 9210 Times: 1
  Product: 29 Name: Utc13_CPP Version: 9178 Times: 13
  Product: 28 Name: Utc13_C Version: 9178 Times: 2
  Product: 25 Name: Implib700 Version: 9210 Times: 5
  Product: 1 Name: Import0 Version: 0 Times: 66
IMAGE_DIRECTORY_ENTRY_IMPORT
  VirtualAddress : 0x4180
  Size : 0x3c
IMAGE_DIRECTORY_ENTRY_BASERELOC
  VirtualAddress : 0x4900
  Size : 0x1e4
IMAGE_DIRECTORY_ENTRY_IAT
  VirtualAddress : 0x3e80
  Size : 0x110
IMAGE_DIRECTORY_ENTRY_DELAY_IMPORT
  VirtualAddress : 0x0
  Size : 0xffff
[Linked libraries]
ntoskrnl.exe
hal.dll

2 libraries
[Relocations]

vaddr      paddr      type   name
―――――――――――――――――――――――――――――――――
0x000042cc 0x00003f88 SET_32 ntoskrnl.exe_KeSetTimerEx
0x000042dc 0x00003f80 SET_32 ntoskrnl.exe_KeInitializeTimerEx
0x000042f2 0x00003f7c SET_32 ntoskrnl.exe_KeInitializeDpc
0x00004304 0x00003f78 SET_32 ntoskrnl.exe_KeCancelTimer
0x00004314 0x00003f74 SET_32 ntoskrnl.exe_KeNumberProcessors
0x0000432a 0x00003f70 SET_32 ntoskrnl.exe_IoDeleteDevice
0x0000433c 0x00003f6c SET_32 ntoskrnl.exe_IoDeleteSymbolicLink
0x00004354 0x00003f68 SET_32 ntoskrnl.exe_RtlInitUnicodeString
0x0000436c 0x00003f64 SET_32 ntoskrnl.exe_ExFreePoolWithTag
0x00004380 0x00003f60 SET_32 ntoskrnl.exe_IofCompleteRequest
0x00004396 0x00003f5c SET_32 ntoskrnl.exe_RtlCopyUnicodeString
0x000043ae 0x00003f58 SET_32 ntoskrnl.exe_ExAllocatePoolWithTag
0x000043c6 0x00003f54 SET_32 ntoskrnl.exe_IoCreateSymbolicLink
0x000043de 0x00003f50 SET_32 ntoskrnl.exe_IoCreateDevice
0x000043f0 0x00003f4c SET_32 ntoskrnl.exe_KeInitializeSpinLock
0x00004408 0x00003f48 SET_32 ntoskrnl.exe_IoReleaseCancelSpinLock
0x00004422 0x00003f00 SET_32 ntoskrnl.exe_IoAcquireCancelSpinLock
0x0000443c 0x00003efc SET_32 ntoskrnl.exe_KeInitializeMutex
0x00004450 0x00003ef8 SET_32 ntoskrnl.exe_KeWaitForSingleObject
0x00004468 0x00003f84 SET_32 ntoskrnl.exe_KeReleaseMutex
0x0000447a 0x00003ed0 SET_32 ntoskrnl.exe_KeSetEvent
0x00004488 0x00003ed4 SET_32 ntoskrnl.exe_KeWaitForMultipleObjects
0x000044a4 0x00003ed8 SET_32 ntoskrnl.exe__allmul
0x000044ae 0x00003edc SET_32 ntoskrnl.exe_ZwSetInformationThread
0x000044c8 0x00003ee0 SET_32 ntoskrnl.exe_PsTerminateSystemThread
0x000044e2 0x00003ee4 SET_32 ntoskrnl.exe_KeSetPriorityThread
0x000044f8 0x00003ee8 SET_32 ntoskrnl.exe_KeGetCurrentThread
0x0000450e 0x00003eec SET_32 ntoskrnl.exe_ZwClose
0x00004518 0x00003ef0 SET_32 ntoskrnl.exe_PsCreateSystemThread
0x00004530 0x00003ef4 SET_32 ntoskrnl.exe_KeInitializeEvent
0x00004552 0x00003ec4 SET_32 HAL.dll_KfReleaseSpinLock
0x00004566 0x00003ec0 SET_32 HAL.dll_KfAcquireSpinLock
0x00004582 0x00003f04 SET_32 ntoskrnl.exe_READ_REGISTER_UCHAR
0x00004598 0x00003f08 SET_32 ntoskrnl.exe_WRITE_REGISTER_UCHAR
0x000045b0 0x00003f0c SET_32 ntoskrnl.exe_WRITE_REGISTER_BUFFER_USHORT
0x000045d0 0x00003f10 SET_32 ntoskrnl.exe_READ_REGISTER_BUFFER_USHORT
0x000045ee 0x00003f14 SET_32 ntoskrnl.exe_READ_REGISTER_ULONG
0x00004604 0x00003f18 SET_32 ntoskrnl.exe_WRITE_REGISTER_ULONG
0x0000461c 0x00003f1c SET_32 ntoskrnl.exe_MmGetPhysicalAddress
0x00004634 0x00003f20 SET_32 ntoskrnl.exe_MmAllocateContiguousMemorySpecifyCache
0x0000465e 0x00003f24 SET_32 ntoskrnl.exe_MmFreeContiguousMemorySpecifyCache
0x00004684 0x00003f28 SET_32 ntoskrnl.exe_MmAllocateNonCachedMemory
0x000046a0 0x00003f2c SET_32 ntoskrnl.exe_MmFreeNonCachedMemory
0x000046b8 0x00003f30 SET_32 ntoskrnl.exe_READ_REGISTER_USHORT
0x000046d0 0x00003f34 SET_32 ntoskrnl.exe_WRITE_REGISTER_USHORT
0x000046e8 0x00003f38 SET_32 ntoskrnl.exe_MmMapIoSpace
0x000046f8 0x00003f3c SET_32 ntoskrnl.exe_MmUnmapIoSpace
0x0000470a 0x00003f40 SET_32 ntoskrnl.exe_KeInsertQueueDpc
0x0000471e 0x00003f44 SET_32 ntoskrnl.exe_KeSetTargetProcessorDpc
0x00004738 0x00003ebc SET_32 HAL.dll_HalGetInterruptVector
0x00004750 0x00003eb8 SET_32 HAL.dll_READ_PORT_UCHAR
0x00004762 0x00003eb4 SET_32 HAL.dll_WRITE_PORT_UCHAR
0x00004776 0x00003eb0 SET_32 HAL.dll_KeStallExecutionProcessor
0x00004792 0x00003eac SET_32 HAL.dll_WRITE_PORT_BUFFER_USHORT
0x000047ae 0x00003ea8 SET_32 HAL.dll_READ_PORT_BUFFER_USHORT
0x000047c8 0x00003ea4 SET_32 HAL.dll_READ_PORT_ULONG
0x000047da 0x00003ea0 SET_32 HAL.dll_READ_PORT_USHORT
0x000047ee 0x00003e9c SET_32 HAL.dll_WRITE_PORT_USHORT
0x00004802 0x00003e98 SET_32 HAL.dll_WRITE_PORT_ULONG
0x00004816 0x00003e94 SET_32 HAL.dll_KeGetCurrentIrql
0x0000482a 0x00003e90 SET_32 HAL.dll_HalSetBusDataByOffset
0x00004842 0x00003e8c SET_32 HAL.dll_HalGetBusDataByOffset
0x0000485a 0x00003e88 SET_32 HAL.dll_HalGetBusData
0x0000486a 0x00003e84 SET_32 HAL.dll_KfRaiseIrql
0x00004878 0x00003ec8 SET_32 HAL.dll_KfLowerIrql
0x00004886 0x00003e80 SET_32 HAL.dll_KeRaiseIrqlToDpcLevel


66 relocations
19456
=== VS_VERSIONINFO ===

Section to Segment mapping:
Segment Section
---------------

```



