Automatic linking of daily and ticket notes
__
__
```js
async function createNoteFromTemplate(templateName, newNoteName) {
    // Get the file from the vault
    const templateFile = app.vault.getAbstractFileByPath("obsidian_templates/" + templateName + ".md");
    var newNoteFile = app.vault.getAbstractFileByPath(newNoteName + ".md");

    // Check if the template file exists
    if (templateFile) {
        // Read the content of the template file
        const templateContent = await app.vault.read(templateFile);
        // Check if new note file exists.
        if (newNoteFile){
            console.log("Note exists");
        } else {
            // Create the new note with the template content
            console.log("Creating " + newNoteName);
            await app.vault.create(newNoteName + ".md", templateContent);
            newNoteFile = app.vault.getAbstractFileByPath(newNoteName + ".md");
            console.log(`Created new note: ${newNoteName}`);
        }
    } else {
        console.error(`Template file not found: ${templateFile}`);
    }
    var today = new Date();
    const cmd = "/opt/homebrew/bin/gsed -i 's/^## Notes:/## Notes:\r- " + String(today.toISOString().slice(0, 10)) + ": " + $3 + "/' " +  newNoteFile.name;
    console.log("Running " + cmd);
    runExternal(cmd);
    return newNoteName;
}

async function insertNote(noteName, sectionName = null) {
    console.log(sectionName);
    var noteFile = app.vault.getAbstractFileByPath(noteName + ".md");
    if (noteFile) {
        // Read the content of the note file
        console.log("Note exists");
        var noteContent = await app.vault.read(noteFile);
        if (sectionName){
            // Add section matching here
            const re = new RegExp("## " + sectionName);
            var keptLines = [];
            var foundSection = 0;
            for (const line of noteContent.split("\n")){
                if (foundSection){
                    if (line.match(/## /)){
                        break;
                    } else {
                        keptLines.push(line);
                    }
                } else if (line.match(re)){
                    keptLines.push(line);
                    foundSection = 1;
                } 
            }
            console.log(keptLines);
            noteContent = keptLines.join("\n");
        }
        return "\n" + noteContent.replace(/^/gm, "> ");
    } else {
        console.log("Note doesn't exist");
        return null;
    }
}
```
__
__

```
^\[\[(SCTASK|INC|CHG)([0-9]{7})\]\] (?!--)(.*)$
```
__
```js
return "[[" + await createNoteFromTemplate($1, $1 + $2) + "]]: " + $3;
```
__
<ticket number> <text>


__
```
^\[\[(\S+)\]\] --text ?(|.*)$
```
__
```js
console.log($2);
return "[[" + $1 + "]]: " + await insertNote($1, $2);
```
__
<note name> --text [Heading]

