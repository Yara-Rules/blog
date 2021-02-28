---
title: "YaraRET"
author: "Joan Soriano (@w0lfvan)"
date: 2018-10-30T22:43:54+01:00
keywords: ["yara", "radare2", "forensics", "go"]
tags: ["yara", "radare2", "forensics", "go"]
draft: false
---

For this forensics cases which are based in unreliable evidences, we decided to carry out the development of a carving tool for getting files from a raw disk using IoC detection. 
 
YaraRET it’s based in Radare2 and Yara, and  it provides 58 magic number's rules for detecting 58 types of files.
This tool relies on the idea of a first stage detecting files using its magic numbers and a second stage, selecting or discarding those detected files using Yara, IoCs or its entropy value. After that, we can generate the hash, the ssdeep to check it over another files or upload the structure to VirusTotal.

YaraRET can be used as a oneliner or in a shell mode.

## Oneliner

If you want to run a fast scan over a disk, you can execute YaraRET in oneliner mode.

In this case, YaraRET runs the ruleset marked as yarafile and, if some rule has a match, YaraRET will look for magic numbers for detecting file structures around this match. If some result has been found, YaraRET will dump this file.

```
$  ./yaraRET yara myYaraRule rawdisk myRaw maxsize maxsizeValue 
```

In the following example, YaraRET has searched for files related to TRISIS malware and a pyc file has been found.

Like with yara rules, YaraRET can parse a file with domains or IPs in it, for look for them in a raw disk.

```
$ ./yaraRET ioc ./myIOC.stix rawdisk myRaw maxsize maxsizeValue
```

## Shell Mode

For running a complex analysis, YaraRET adds a shell mode which allows selection of file structures based in Yara or IoC detection or its entropy. Also, provides a flexible way for footer assignment.

```
$ ./yaraRET rawdisk myRaw shell
```

## Features

YaraRET also includes the following features:

* Run Radare2 commands
* Ssdeep distance checking
* VirusTotal API integration
* Scripting
* YaraForensics ruleset
* Entropy

You can find all the documentation about YaraRET in the following link: https://github.com/wolfvan/YaraRET/blob/master/docs/readTheDocs.md

An stable version of code could be found in our Github repository.
