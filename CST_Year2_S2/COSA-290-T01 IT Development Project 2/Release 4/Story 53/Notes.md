# Story 53 - Tagging
- Need to add `Notes` and `Exclude` properties to `PatientEvaluation`
- Tags can be included in `Notes` with `#` (Ex. `"Patient was #sick and was unable to perform basic tasks"`) which depending on the tag can set the `Notes` property to true.
- Aron recommended [this](https://pub.dev/packages/fluttertagger) flutter tagging package

## ATP
- Need test for list of tags
- Spaces in the tags - **If I have a set list I just won't include ones with spaces**
- tag that isn't in the list

## Tag List
- sick
- tired
- injured
- unwell
- uncooperative
- weather
- pain
- medication
- seizure
- other
