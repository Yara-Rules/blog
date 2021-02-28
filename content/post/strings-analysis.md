+++
title = "Yara Rules Strings: Statistical study"

author = "Maite Moreno (@mmorenog)"
date = "2017-04-06"

draft = false

categories = ["Analysis"]
tags = ["strings", "study", "statistic", "rules"]
+++

As all Yara users know, Yara rules are based on "strings"; which are basically descriptions of patterns-based malware families. We can find simple rules like the following, [for example](https://github.com/Yara-Rules/rules/blob/master/malware/APT_APT1.yar):

```
rule LIGHTDART_APT1
{
    meta:
        author = "AlienVault Labs"
        info = "CommentCrew-threat-apt1"

    strings:
        $s1 = "ret.log" wide ascii
        $s2 = "Microsoft Internet Explorer 6.0" wide ascii
        $s3 = "szURL Fail" wide ascii
        $s4 = "szURL Successfully" wide ascii
        $s5 = "%s&sdate=%04ld-%02ld-%02ld" wide ascii

    condition:
        all of them
}
```

On the other hand, there are also more complex rules that use wild-cards, regular expressions, special operators or any other features that can be used in Yara and can be consulted in the [documentation](http://yara.readthedocs.io/en/v3.5.0/).

Starting with our [Yara rules compilation](https://github.com/Yara-Rules/rules) and with help of [YaGo](http://yara-rules.github.io/blog/2017/03/27/yago-converting-yara-rules-into-json-files/), I decided to carry out the experiment to study all the strings together collected from the compilation and we’d like to want to show the results. At the time of the experiment our repository had _11784_ signatures with _15554_ different strings.

## Top 15 references to functions

We realized a research for references to functions. We sorted the top 15 decrecently and we came up with the next:

```
1.  GetProcAddress
2.  Sleep
3.  VirtualAlloc
4.  WriteFile
5.  VirtualProtect
6.  ServiceMain
7.  WriteProcessMemory
8.  CreateThread
9.  AdjustTokenPrivileges
10. Getcommandline
11. WSAStartup
12. VirtualFree
13. LoadLibraryA
14. ExitProcess
15. DllRegisterServer
```

The result of our strings study looks very similar to this Binary Networks [study](https://www.bnxnet.com/top-maliciously-used-apis/), which it’s being used by pestudio on one of its reputation lists (specifically at functions.xml file).

## Referenced file extensions

Among the strings of Yara analyzed so far we found that rules refer up to 16 different file extensions, where which stand out _.exe_, _.dll_, _.txt_, _.dat_, or _.pdb_ as more significant in number of occurrences. A small chart below.

![Extension pie chart](/post/strings-analysis/1.png)

Analyzing in depth which _dll_ and _exe_ files are more time referenced in our strings, we reach the following conclusion (I show simply top 15 and from highest to lowest number of occurrences):

### Top 15 referenced DLL files

```
1.  kernel32.dll
2.  wsock32.dll
3.  Ws2_32.dll
4.  CI.dll
5.  WININET.dll
6.  user32.dll
7.  urlmon.dll
8.  advapi32.dll
9.  svchostdllserver.dll
10. imagehlp.dll
11. HAL.dll
12. dnsapi.dll
13. Crypt32.dll
14. BypassUacDLL.dll
15. Advapi32.dll
```

### Top 15 Referenced EXE files

```
1.  cmd.exe
2.  svchost.exe
3.  rundll32.exe
4.  Explorer.exe
5.  wmiprvse.exe
6.  ntoskrnl.exe
7.  sysprep.exe
8.  lsass.exe
9.  mshtaex.exe
10. xsiff.exe
11. regsvr32.exe
12. ISUN32.EXE
13. net.exe
14. Inetinfo.exe
15. mimikatz.exe
```

## Common folder variables

Malware often uses a variable folder when it tries to access, change, or create files and folders on your PC so we have also included a study of the occurrences that referred to any of these variables and the result obtained is as follows:

![Common folder pie chart](/post/strings-analysis/2.png)

### User-Agents

To conclude, we have compiled a list of user-agent that are used in the strings, and we’ve got the following list:

```
Mozilla/4.0 (compatible; MSIE 6.0;Windows NT 5.0; .NET CLR 1.1.4322)
Mozilla
Mozilla/4.0
Mozilla/4.0 (compatible; )
Mozilla/4.0 (compatible; MSI 6.0;
Mozilla/4.0 (compatible; MSIE 4.01; Windows NT)
Mozilla/4.0 (compatible; MSIE 5.00; Windows 98) KSMM
Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)
Mozilla/4.0 (Compatible; MSIE 6.0;)
Mozilla/4.0 (compatible; MSIE 6.0; Win32)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0; .NET CLR 1.1.4322)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SP Q%%d)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)
Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.; SV1)
Mozilla/4.0 (compatible; MSIE 6.1; Windows NT 5.1; SV1)
Mozilla/4.0 (compatible; MSIE 7.0;)
Mozilla/4.0 ( compatible; MSIE 7.0; AOL 8.0 )
Mozilla4.0 (compatible; MSIE 7.0; Win32)
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; SV1)
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; .NET CLR 1.1.4322; .NET CLR 2.0.503l3; .NET CLR 3.0.4506.2152; .NET CLR 3.5.30729; MSOffice 12)
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.2; .NET CLR 1.1.4322
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.2; SV1)
Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3
Mozilla/4.0 (compatible; MSIE 8.0; Win32)
Mozilla/4.0 (compatible; MSIE 8.0; Windows NT
Mozilla/4.0 (compatible; MSIE8.0; Windows NT 5.1)
Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727.42)
Mozilla/4.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/4.0;)
Mozilla/4.0 (compatible; MSIE %d.0;
Mozilla/4.0 (compatible; Windows NT 5.1; MSIE 7.0)
Mozilla/4.0 (compatible; Windows NT 5.1; MSIE 7.0; Trident/4.0)
Mozilla/4.0 (compatible; Windows NT 5.1; MSIE 7.0; Trident/4.0; %s.%s)
Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; MALC)
Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36
Mozilla/5.0 (Windows NT 6.2; WOW64; rv:20.0) Gecko/20100101 Firefox/
Mozilla/5.0 (Windows NT 6.3; WOW64; rv:28.0) Gecko/20100101 Firefox/28.0
Mozilla/5.0 (Windows NT 6.; WOW64; rv:20.0) Gecko/20100101 Firefox/2
Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-CN; rv:1.7.6)
Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-EN; rv:1.7.12) Gecko/200
Mozilla/5.0 (Windows; U; Windows NT 5.1; zh-EN; rv:1.7.12) Gecko/20100719 Firefox/1.0.7
Mozilla/5.0 (Windows; Windows NT 5.1; en-US; rv:1.8.0.12) Firefox/1.5.0.12
Mozilla5.1 (compatible; MSIE 8.0; Win32)
Shockwave Flash
SJZJ (compatible; MSIE 6.0; Win32)
Netscape
```

As conclusion to this strings study, we suggest that creating a Yara rule with all these strings will be very interesting. It will be worth to rate the analysis in a global way, because it would be good reputation IoC. On the other hand, whether Yara rule matches only some of these strings couldn't be enough to decide if it is a malware or not.

If you find it useful and you would like to have these lists updated we can do this analysis periodically or we could add a section in www.yara-rules.github.io/blog with the statistical data of the strings so that they will be updated in real time or periodically. We look forward to see your feedback.
