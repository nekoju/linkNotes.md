
```
                       .-') _ .-. .-')       .-') _               .-') _     ('-.    .-')      _   .-')    _ .-') _   
                      ( OO ) )\  ( OO )     ( OO ) )             (  OO) )  _(  OO)  ( OO ).   ( '.( OO )_ ( (  OO) )  
 ,--.      ,-.-') ,--./ ,--,' ,--. ,--. ,--./ ,--,'  .-'),-----. /     '._(,------.(_)---\_)   ,--.   ,--.)\     .'_  
 |  |.-')  |  |OO)|   \ |  |\ |  .'   / |   \ |  |\ ( OO'  .-.  '|'--...__)|  .---'/    _ |    |   `.'   | ,`'--..._) 
 |  | OO ) |  |  \|    \|  | )|      /, |    \|  | )/   |  | |  |'--.  .--'|  |    \  :` `.    |         | |  |  \  ' 
 |  |`-' | |  |(_/|  .     |/ |     ' _)|  .     |/ \_) |  |\|  |   |  |  (|  '--.  '..`''.)   |  |'.'|  | |  |   ' | 
(|  '---.',|  |_.'|  |\    |  |  .   \  |  |\    |    \ |  | |  |   |  |   |  .--' .-._)   \   |  |   |  | |  |   / : 
 |      |(_|  |   |  | \   |  |  |\   \ |  | \   |     `'  '-'  '   |  |   |  `---.\       /.-.|  |   |  | |  '--'  / 
 `------'  `--'   `--'  `--'  `--' '--' `--'  `--'       `-----'    `--'   `------' `-----' `-'`--'   `--' `-------'  
 ```

# linkNotes.md
And Obsidian plugin (sub-plugin?) to create an internal CLI for creating and linking note contents

# Installation
- Get inlineScripts obsidian plugin and enable external commands.
- Install `gnu-sed` if you're on Mac
- Put in `<obsidian-vault>/support/inlineScripts` and follow inlineScripts script installation instructions. If you're on Linux, change the path for the `sed` executable. If you're on Windows, good luck and namaste.
- Create required templates. Generally, each template must have relevant sections delineated by `## ` and ticket templates must include a `## Notes:` heading.

# Usage
Commands are defined by a pattern. `;;...::` triggers any script

`<ticket-link> <text>`
- Creates a note for `<ticket-no>` if it does not exist. "`<date>: <text>`" will be appended under the `## Notes` heading in any event. Text will expand to `[[<ticket-no>]]: <text>` in-place.
- This requires you to make templates for `SCTASK`, `INC`, `CHG` and add them to obsidian accordingly (see Templates core plugin docs).

`<note-link> --text [<heading>]`
- Will expand to `<note-link>\n<blockquote(note-text)>`. If `<heading>` argument is given, `<note-text>` will only be the text under `<heading>` (`##` level)
