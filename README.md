# scarpet
Public Repository of scarpet apps for Minecraft.
Check https://gnembon.github.io/scarpet/ for full language docs.
Obtain scarpet through carpet mod: https://github.com/gnembon/fabric-carpet/releases

## Changelog

### v1.5
 - added ability for apps to keep their persistent state using `load_app_data` and `store_app_data` functions
 - added maps via `m()` function
 - added proper nbt support via `nbt()` function
 - all containers (lists, maps and nbts) now have unified api via `get`, `has`, `put` and `delete` functions
 - added L-value behaviour to certain functions and operators, like `get`, `has`, `put`, `delete`, `=`, `+=`
 - new `:` operator - highest priority - to access containers elements, alias for `get` function
 - changed priority of `~` match operator to match `:`
 - numbers have to start because of that with a number, so `.123` won't float anymore, use `0.123` instead
 - added `in_dimension(dimension, expr)` to change the execution context for the subexpression, for instance to place blocks in the nether while running a script in the overworld
 - added carpet mod setting `/carpet scriptsAutoload` to automatically load scarpet packages from disk on server / game start which works even with `/script` command fully disabled. However, scipts to stay loaded need to return proper app config by defining `__config()` function. See `/script load` section for details.
 - added `entity_event` to add functions to be called when certain events happen for an entity
 - added four more general use events: `player_releases_item` (bows, aborting actions, controlled client side), `player_finishes_using_item` (item consumed, eating etc. server controlled), `player_drops_item` for single item dropped, and `player_drops_stack` for dropping entire stack.

### v1.4
 - `top` to get the top block at position now requires full block coordinates, but Y value is ignored.
 - Inventories of blocks and entities got their API as well. Check `stack_limit`, `inventory_size`, `inventory_get`, `inventory_set`, `inventory_find`, `inventory_remove` and `drop_item` functions.
 - scripts loaded from disk (via /script load/unload command) will operate in each player space by default, unless loaded with `shared` option.
 - the newline markers for 'in-commandblock' type scripts are now fully parsed, meaning you can have `$` in strings. `$` markers are supported only with in-game cases.
 - support for comments via `//` in scripts loaded from world files. Comments are only allowed in external file scripts.
 - tab completion for typing programs in commands manually (in /script command)
 - unloading/reloading a module removes all event callbacks from that module
 - `return`, `throw`, `exit`, as well as the 'catch' expression of `try` can be omitted, assuming `null`
 - if with no `else` expression will 'else' to `null`
 - `element(list,index)` has been deprecated, and replaced with `get(value,address)`, working on lists as well as nbt constructs
 - there is a new `nbt` type, that behave like string, but can be queried with get more efficiently
 - primitive types of nbt are now converted to primitive scarpet types when queried. This doesn't apply to compound nbts
 - iterators, like `range`, `rect`, can be reused and moved about in a variable.
 - added `type` function to recognized held variable type.
 - `str` format arguments can now be passed in a single list
 - block values now properly handle block entity data, meaning `set`-ting a chest from another location will retain its content.
 - therefore set can also accept custom BE tag?
 - `place_item` to replicate the action of  a player placing a block of item
 - `set_biome` to sets permanently a custom biome at a position. For those missing a custom command to do that in carpet, just use `/script scan 0 0 0 x1 0 z1 x2 0 z2 set_biome(_,'swamp')` for the same effect
 - `block_properties` lists all available block properties at position
 - `block_data` returns nbt of a block at position
 - `property` makes sure all value comes out lowercased.
 - `spawn` function to spawn entities like /summon command but retaining access to them.
 - `entity ~ 'look'` will return a look vector of an entity. No need to math yaw pitch here.
 - `entity ~ 'selected_slot'` to return current selected slot for players
 - `entity ~ 'facing'` returns a facing order of a player
 - `entity ~ 'trace'` ca be used to ray trace blocks, liquids and entities
 - entity `~` sugar can now support 
 - fixed `modify(e,'custom_name',null)` to actually clear custom name
 - `create_marker` and `remove_all_markers` for easy marking I guess
 - fixed 'double evaluation' caused by print function
 - setting various entities motions and positions should update properly to the clients
 - fixed `thoughts too dope` when trying to compare list to a number

### v1.3
 - Added 1.14 specific structures to plop for 1.14 (fabric-carpet)
 - added `destroy` and `harvest` functions for other valid methods of breaking blocks
 - added `schedule` to delay execution of user defined functions for later ticks
 - scarpet now allows to intercept most important user actions related events. Check `utilities\event_test.sc` and load via `/script load event_test` to test event handling.

### v1.2
 - fixes to lists handling
 - fixed issue with running 'run' command in functions
 - scripts can now be loaded from files in /scripts/ folder inside world directory. These also can be edited normally, without extra $ to indicate new lines.
 - each file represents a package and is run independently from others.
 - /script load/unload <package>
 - /script in <package> run/invoke etc...
 - script modules loaded from scripts / bundled with carpetmod can make new commands. details - later.

### v1.1
 - `put` function to modify lists content
 - `_` in loop functions can be used to change content of sublists
 - minor performance improvements
 - scripting engine will reset with world loading
 -  typos with gragon eggs
 - player movement is much smoother when controlled with `modify` function
 - `loaded` and `loaded_ep` won't load the points, lol
 - if executed as `/execute as @p script run... ` print will output to players chat, not system log
 - no need to disable commandBlockOutput - scripts will no longer output results of intermediate results.
 
 ### v1.0
  - everything
