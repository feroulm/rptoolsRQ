# rptoolsRQ
rpTools Macro for RuneQuest

*Purpose* : I just discover the amazing job of the [RPTools team](https://www.rptools.net/)  thanks to them ! Now i want to try it on my current Runequest[^1] campaign, so time for me to learn development and immerse myself in the rptools macro world...
Hoping Lhankor Mhy will share a few drops of its knowldge to help me during this heroquest to achieve something useful.

(!) *Still under dev, below is not yet a guide mainly cryptic notes that make sense for me at this stage*

## Token Macro - libRQII
### pnjSheet
Display a simplified sheet with useful information for Melee mode, mainly :
- combat skill , Hit Point & Armour Point
- melee and missile weapon
Token creation process: 
- Create your pnj using macroGen/pnjSheet.xls
- The sheet generate the necessary macro command (tab *TokenMacro*) needed to init you PNJ Token in maptool
- Create you token in maptool, use the config RQ_Human (using template campaing/tokenTypeProp_RQ_Human.txt)
- Impersonate the token and copy/paste the macros

### monsterSheet
Display a simplified sheet with useful information for Melee mode, mainly :
- enable multiples location for monster with too much heads, legs and arms ;)
- combat skill , Hit Point & Armour Point
Token creation process: 
- Create your monster using macroGen/monsterSheet.xls
- The sheet generate the necessary macro command (tab *TokenMacro*) needed to init you PNJ Token in maptool
- Create you token in maptool, use the config RQ_Human (using template campaing/tokenTypeProp_RQ_Monster.txt)
- Impersonate the token and copy/paste the macros

### combatAction
*Manage Combat Action for all the token added to the Initiative List*

During a combat , the current CA can be different from its base value (modified by of a spell, a magic weapon, etc..)
- the form unable to define a such a specific CA (ccCA) for each member
- it also enable to reset counter using base value or specific value (this as to be done each MR)

### combatAction
*Manage Combat Action for all the token added to the Initiative List*

During a combat , the current CA can be different from its base value (modified by of a spell, a magic weapon, etc..)
- the form unable to define a such a specific CA (ccCA) for each member
- it also enable to reset counter using base value or specific value (this as to be done each MR)

## Notepad++
Set up specific UDL for rptools macro : Language > User Defined Language > Define your language
Then import : rpToolsMacroUDL.xml


[^1]: &trade;,&copy;,&reg;  Runequest and Glorantha are property , copyright, trademark of Chaosium Inc and/or   Moon Design Publications

