+++
title = "YaGo, converting Yara rules into JSON files"

author = "Jaume Martin (@Xumeiquer)"
date = "2017-03-27"

draft = false

categories = ["tools"]
tags = ["yara", "rules", "yago", "json"]
+++

**NOTE**
Yago project is archived and no longer maintained.

Yara-Rules project is proud to anounce YaGo. YaGo is a tool that converts Yara rules into JSON files, that's it, simple.

Yara has a great comunity that use it and use a lot of rules, but sometimes it is hard to manage all of them, it is difficult to get a bird's eye view of your rule set so we thought coverting the rules in json format will help.

YaGo can be used as a standalone application or you can embed it on your own application. In adition, we haved licensed YaGo using Apache License v2 so you can use it as you want in your projects. In any way, we hope you to colaborate with us improving YaGo and Yara-Rules in general.

Using YaGo is really simple, for example this is its command line options.

```md
./yago
  yago fileName <fileName> [ --validJSON ]
  yago dirName <dirName> [ --validJSON ]
  yago indexFile <indexFile> [ cwd <path> ] [ --validJSON ]
  yago inputFile <inputFile> outputDir <outputDir> [ --overwrite ] [ --validJSON ]
  yago inputFile <inputFile> outputFile <outputFile> [ --overwrite ] [ --validJSON ]
  yago -h | --help
  yago --version
```

The easyest execution is:

```json
yago fileName test/EK_Zeus.yar

{"file_name":"EK_Zeus.yar","imports":null,"rules":[{"name":"zeus_js","global":false,"private":false,"tags":["EK"],"meta":{"author":"Josh Berry","date":"2016-06-26","description":"Zeus Exploit Kit Detection","hash0":"c87ac7a25168df49a64564afb04dc961","sample_filetype":"js-html","yaragenerator":"https://github.com/Xen0ph0n/YaraGenerator"},"strings":[{"name":"$string0","value":"var jsmLastMenu ","modifers":null,"type":1},{"name":"$string1","value":"position:absolute; z-index:99' ","modifers":null,"type":1},{"name":"$string2","value":" -1)jsmSetDisplayStyle('popupmenu' ","modifers":null,"type":1},{"name":"$string3","value":" '\u003ctr\u003e\u003ctd\u003e\u003ca href","modifers":null,"type":1},{"name":"$string4","value":"  jsmLastMenu ","modifers":null,"type":1},{"name":"$string5","value":"  var ids ","modifers":null,"type":1},{"name":"$string6","value":"this.target","modifers":null,"type":1},{"name":"$string7","value":" jsmPrevMenu, 'none');","modifers":null,"type":1},{"name":"$string8","value":"  if(jsmPrevMenu ","modifers":null,"type":1},{"name":"$string9","value":")if(MenuData[i])","modifers":null,"type":1},{"name":"$string10","value":" '\u003cdiv style","modifers":null,"type":1},{"name":"$string11","value":"popupmenu","modifers":null,"type":1},{"name":"$string12","value":"  jsmSetDisplayStyle('popupmenu' ","modifers":null,"type":1},{"name":"$string13","value":"function jsmHideLastMenu()","modifers":null,"type":1},{"name":"$string14","value":" MenuData.length; i","modifers":null,"type":1}],"condition":"14 of them"}]}
```

You can use `jq` to see the output much clear.

```json
yago fileName test/EK_Zeus.yar | jq .
{
  "file_name": "EK_Zeus.yar",
  "imports": null,
  "rules": [
    {
      "name": "zeus_js",
      "global": false,
      "private": false,
      "tags": [
        "EK"
      ],
      "meta": {
        "author": "Josh Berry",
        "date": "2016-06-26",
        "description": "Zeus Exploit Kit Detection",
        "hash0": "c87ac7a25168df49a64564afb04dc961",
        "sample_filetype": "js-html",
        "yaragenerator": "https://github.com/Xen0ph0n/YaraGenerator"
      },
      "strings": [
        {
          "name": "$string0",
          "value": "var jsmLastMenu ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string1",
          "value": "position:absolute; z-index:99' ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string2",
          "value": " -1)jsmSetDisplayStyle('popupmenu' ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string3",
          "value": " '<tr><td><a href",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string4",
          "value": "  jsmLastMenu ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string5",
          "value": "  var ids ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string6",
          "value": "this.target",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string7",
          "value": " jsmPrevMenu, 'none');",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string8",
          "value": "  if(jsmPrevMenu ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string9",
          "value": ")if(MenuData[i])",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string10",
          "value": " '<div style",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string11",
          "value": "popupmenu",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string12",
          "value": "  jsmSetDisplayStyle('popupmenu' ",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string13",
          "value": "function jsmHideLastMenu()",
          "modifers": null,
          "type": 1
        },
        {
          "name": "$string14",
          "value": " MenuData.length; i",
          "modifers": null,
          "type": 1
        }
      ],
      "condition": "14 of them"
    }
  ]
}
```

You can use mongo or a ELK stack to store and organize your rules as well as manage your own rule set. By default YaGo prints out the rules in a way to be able to import them into mongo o logstash.

For example:

```
yago dirName rules_dir | mongoimport --db yararules --collection rules --type json
```

Or
```
mongoexport --db yararules --collection rules --type json > rules.json ; yago inputFile rules.json outputFile rules.yar
```

If you want to get more of YaGo go to https://github.com/Yara-Rules/yago and start playing with it. There is documentation in the repo as wll as a full list of examples.


