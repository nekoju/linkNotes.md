# linkNotes.md
And Obsidian plugin (sub-plugin?) to create an internal CLI for creating and linking note contents

# Installation
- Get inlineScripts obsidian plugin and enable external commands.
- Install `gnu-sed` if you're on Mac
- Put in `<obsidian-vault>/support/inlineScripts` and follow inlineScripts script installation instructions.

# Usage
Commands are defined by a pattern. ;;...:: triggers any script

`[[<ticket-no>]] <text>`
- Creates a note for `<ticket-no>` if it does not exist. "`<date>: <text>`" will be appended under the `## Notes` heading in any event. Text will expand to `[[<ticket-no>]]: <text>` in-place.

`[[<note-title>]] --text [<heading>]`
- Will expand to `[[<note-title>]]\n<note-text>`. If `<heading>` argument is given, `<note-text>` will only be the text under `<heading>` (`##` level)
