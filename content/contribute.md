+++
date = "2015-02-25T00:00:00+01:00"
title = "Contribute"
+++

If you’re interested in sharing your Yara rules with us and the Security Community, you can [join our Telegram group](https://t.me/joinchat/ALAD2UZ1HxA0M37D94oeag "YaraRules Feedback Telegram Group"), [send a message to our Twitter account @YaraRules](https://twitter.com/yararules "YaraRules' Twitter Account"), or [submit a pull request on our Github Repository](https://github.com/Yara-Rules/rules/ "YaraRules Github Repository").

We have divided our ruleset in nine main categories, each one of them represented by a file: AntiDebug, CVE, Crypto, Exploit Kits, Malicious Document, Malware, Mobile Malware, Packer and Webshells. Most of the categories are split in a per family basis.

We also have two auxiliary categories, email and utils, that have simple rules to work with emails and regular IoC (IP, domains, URL, ...).

We want all the new rules to follow some guidelines. First of all, we would like to have some common metadata fields to better identify every rule. Author, date, brief description, sources, references or sample hashes are some of the most interesting fields for us.

Submitting rules with this template will make it easier for us to organize and sort all the rules you send:

```yara
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

Also, we would like to establish a set of prefixes on the rule name to make them easily identifiable. A rule name should contain the following parts:

The category name abbreviated in 2 letters: MW (Malware), AD (AntiDebug), CR (Crypto), MD (Malicious Document) or PA (Packer) for each one of the defined categories.
A subcategory or MW family name.
A unique name that fully identifies the rule.

```html
<Category (2 letters)>_<Subcategory/Family>_<unique name>
```

Besides this, adding tags to the rule can make it easier for other people to identify and keep track of rules.

For a better management of the GitHub Pull Requests it would be great if you created different PR to add, modify or delete rules for a single category/family, instead of mixing modifications on different rules/families in a single PR. Also, giving reasons on why you want to modify or delete some rules will definitely help us introducing the changes to the ruleset.

If you send us a new malware family, please send it on a new file so we can attach to the structure we mentioned before.

Finally, we suggest you to have in mind [this series of guidelines](https://gist.github.com/Neo23x0/e3d4e316d7441d9143c7 "Yara Performance Guidelines") when creating your signature for getting the most out of them.

Our Yara ruleset is under the [GNU-GPLv2](http://www.gnu.org/licenses/gpl-2.0.html "GNU GPL License v2") license. It’s open to any user or organization, as long as you use it under this license.

The [YaraRules](https://twitter.com/yararules) team.
