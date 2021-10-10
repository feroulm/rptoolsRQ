# sheetManagement
rpTools Macro for RuneQuest

*Purpose* : Viewing and editing human and monster sheet

Compose of two main window
- viewSheet
- editSheet

## editSheet

Composed of sub-windows for spellManagement
### spellManagement

Logic - Mermaid diagram
```
graph TD
    A(openSheetSpellMgt) -->|tokenId, nameFilter,typeFilter| B[editSheetSpellMgt]
    B --> C1[/Update Common Spell/] 
    B --> C2[/Update Divine Spell/] 
    B --> |tokenId, nameFilter,typeFilter| C3(editAddSpells)
    C1 --> |tokenId| D(updateSpells)
    C2 --> |tokenId| D(updateSpells)
```

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBKG9wZW5TaGVldFNwZWxsTWd0KSAtLT58dG9rZW5JZCwgbmFtZUZpbHRlcix0eXBlRmlsdGVyfCBCW2VkaXRTaGVldFNwZWxsTWd0XVxuICAgIEIgLS0-IEMxWy9VcGRhdGUgQ29tbW9uIFNwZWxsL10gXG4gICAgQiAtLT4gQzJbL1VwZGF0ZSBEaXZpbmUgU3BlbGwvXSBcbiAgICBCIC0tPiB8dG9rZW5JZCwgbmFtZUZpbHRlcix0eXBlRmlsdGVyfCBDMyhlZGl0QWRkU3BlbGxzKVxuICAgIEMxIC0tPiB8dG9rZW5JZHwgRCh1cGRhdGVTcGVsbHMpXG4gICAgQzIgLS0-IHx0b2tlbklkfCBEKHVwZGF0ZVNwZWxscylcbiAiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](https://mermaid-js.github.io/mermaid-live-editor/edit#eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBKG9wZW5TaGVldFNwZWxsTWd0KSAtLT58dG9rZW5JZCwgbmFtZUZpbHRlcix0eXBlRmlsdGVyfCBCW2VkaXRTaGVldFNwZWxsTWd0XVxuICAgIEIgLS0-IEMxWy9VcGRhdGUgQ29tbW9uIFNwZWxsL10gXG4gICAgQiAtLT4gQzJbL1VwZGF0ZSBEaXZpbmUgU3BlbGwvXSBcbiAgICBCIC0tPiB8dG9rZW5JZCwgbmFtZUZpbHRlcix0eXBlRmlsdGVyfCBDMyhlZGl0QWRkU3BlbGxzKVxuICAgIEMxIC0tPiB8dG9rZW5JZHwgRCh1cGRhdGVTcGVsbHMpXG4gICAgQzIgLS0-IHx0b2tlbklkfCBEKHVwZGF0ZVNwZWxscylcbiAiLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)
