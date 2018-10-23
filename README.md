# changelog-level-script
A bash script which creates a multi-level changelog based on an annotated GIT commit history

## Usage: 
```
    ./changelog.sh [-t|--anchor_tag <arg>] [-f|--output_file <arg>] [-h|--help] <changelog_lvl>
	<changelog_lvl>: threshold for generating changelogs
	-t,--anchor_tag: tag from which the changelog should be generated (default: '@^')
	-f,--output_file: the file into the changelog is written (default: 'CHANGELOG.md')
	-h,--help: Prints help
````

This script assumes that **HEAD is on a tag** and the git commit history is annotated with the changelog information formatted as follows:

```
<beta>[Changelog message goes here]</beta>
<rc>[Changelog message goes here]</rc>
<release>[Changelog message goes here]</release>
```

The idea behind this is that this way an automated changelog for different target groups can be generated, for example a change which introduces a new feature should be visible in all three levels of the changelog and put into the <release> tag. Changes which should be communicated to external testers but not shown in the final release log is put into <rc> tags. Changes which is important information for internal testers but not external testers or releases is put into <beta> tags and is shown there. 

### The script generates the following changelog:

<changelog_lvl> = beta

```
Version:
[Tagname]

Internal testing changes:
- [Changelog message]

External testing changes:
- [Changelog message]

Release changes:
- [Changelog message]
```

---

<changelog_lvl> = rc

```
Version:
[Tagname]

External testing changes:
- [Changelog message]

Release changes:
- [Changelog message]
```

---

<changelog_lvl> = release

```
Version:
[Tagname]

Release changes:
- [Changelog message]
```