# Tools for token management

## Export to xwiki

Files related to the module :

libRQII\tokenPropertyManagement\exportSheetWiki.rqm
libRQII\tokenPropertyManagement\exportSheetWikiLight.rqm
libRQII\tokenPropertyManagement\openExportSheetWiki.rqm
libRQII\tokenPropertyManagement\openExportSheetWikiLight.rqm

GM\adminDebug\openExportSheetWiki.rqm
GM\adminDebug\openExportSheetWikiLight.rqm

Principle :
- select a token
- launch GM/openExportSheetWiki (or the light version)
- select all the content and copy/paste to xwiki page (in wiki edition mode)

Must be open in an html window otherwise there's an issue with the copy paste (no carriage return))

## Token Log Management

Various macros / function to enable the management of a log for some token, in order to trace event like change in HP/AP, Magic Point, etc.

Main principles are
- Logs are managed using a specific token for each player.
- This log token needs to be manually created on **_Main_AE** map. 
- It must be of type **RQ_Log** 
- It must use the naming convention : **tokenLog_**_the token name_ (ex: tokenLog_PJ_TST01)

Macros related to the feature ONLY : 
- libRQII/sheetView/showFilteredTokenLogEntry.rqm
- libRQII/sheetView/viewSheetLogs.rqm
- libRQII/tokenPropertyManagement/editTokenLogEntry.rqm
- libRQII/tokenPropertyManagement/findCurrentTokenLog.rqm
- libRQII/tokenPropertyManagement/updateTokenLogEntry.rqm

Other macros which are modified for this feature :
- libRQII/combatAction/addCombatLogEntry.rqm
- libRQII/combatAction/updateCombatProactive.rqm
- libRQII/eventHandler/onCampaignLoad.rqm
- libRQII/locHpAp/updateAPHP.rqm
- libRQII/sheetView/openSheet.rqm
- libRQII/sheetView/viewSheet.rqm

Related also to *combatLog Feature* described in cf [combat Action readme](../combatAction/README.md).
Usage is also described on the Xwiki : - https://www.inyanga.me/xwiki/bin/view/Rq/MapTool/RpTools/

Some related issue : #85