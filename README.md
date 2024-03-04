# nls_933w_dll

```
Small note: sometimes named
- nls_933w_dll
- nls_933w.dll

Just as fanny.bmp is sometimes named "fanny_bmp" and "fanny.bmp"

Refs:
- https://github.com/Yara-Rules/rules/blob/master/malware/APT_Equation.yar
- https://securelist.com/inside-the-equationdrug-espionage-platform/69203/
- https://www.antiy.net/p/a-trojan-that-can-modify-the-hard-disk-firmware/
- https://www.antiy.net/wp-content/uploads/A_TROJAN_THAT_CAN_MODIFY_THE_HARD_DISK_FIRMWARE.pdf

```



```
$ for ALGO in {md5sum,sha1sum,sha224sum,sha256sum,sha384sum,sha512sum}; do $ALGO nls_933w.dll; done 11fb08b9126cdb4668b3f5135cf7a6c5  nls_933w.dll
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

