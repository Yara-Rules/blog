+++
title = "YaraRules now on GitHub"

author = "Yara-Rules"
date = "2015-04-27T00:00:00+01:00"

draft = false

categories = ["news"]
tags = ["github", "rules"]
+++

If you’re interested in sharing your Yara rules with us and the Security Community, you can [join our Telegram Group](https://t.me/joinchat/ALAD2UZ1HxA0M37D94oeag "YaraRules Telegram Group"), [send a message to our Twitter account @YaraRules](https://twitter.com/yararules "YaraRules' Twitter Account"), or [submit a pull request on our Github Repository](https://github.com/Yara-Rules/rules/ "YaraRules Github Repository").

We have divided our ruleset in five categories, each one of them represented by a file: AntiDebug, Crypto, Malicious Document, Packer and Malware. Also, the malware category is split in a per malware family basis.

Also, we want all the new rules to follow some guidelines. First of all, submitting rules with this template will make it easier for us to organize and sort all the rules you send:

```
rule rule_name : tag1 tag2 tag3
{
    meta:
        author      = "author's name and (if possible) link to profile"
        date        = "yyyy/mm/dd"
        description = "What does the rule do"
        reference/source = "Link to the blog, paper, ..."
        sample      = "file hashes"
   strings:
        XXXX
   condition:
        XXXX
}
```
To continue, we would like to establish a set of prefixes on the rule name to make them easily identifiable. A rule name should contain the following parts:

The category name abbreviated in 2 letters: MW (Malware), AD (AntiDebug), CR (Crypto), MD (Malicious Document) or PA (Packer) for each one of the defined categories.
A subcategory or MW family name.
A unique name that fully identifies the rule.
<Category (2 letters)>_<Subcategory/Family>_<unique name>

Besides this, adding tags to the rule can make it easier for other people to identify and keep track of rules.

For a better management of the GitHub Pull Requests it would be great if you created different PR to add, modify or delete rules, instead of mixing additions, updates or deletions in a single PR. Also, giving reasons on why you want to modify or delete some rules will definitely help us introducing the changes to the ruleset.

If you send us a new malware family, please send it on a new file so we can attach to the structure we mentioned before.

Finally, we suggest you to have in mind [this series of guidelines](https://gist.github.com/Neo23x0/e3d4e316d7441d9143c7 "Yara Performance Guidelines") when creating your signature for getting the most out of them.

Our Yara ruleset is under the [GNU-GPLv2](http://www.gnu.org/licenses/gpl-2.0.html "GNU GPL License v2") license. It’s open to any user or organization, as long as you use it under this license.

The [YaraRules](https://twitter.com/yararules) team.
