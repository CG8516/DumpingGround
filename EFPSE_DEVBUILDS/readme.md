## Use these builds at your own risk!
##### Due to the high chance of bugs/issues, you run a much greater risk of corrupting your project.
##### Always backup your projects before trying a new development build.

### WARNING: THE LATEST UPDATES WILL MAKE YOUR MAP FILES INCOMPATIBLE WITH OLDER VERSIONS OF EFPSE.
#### Maps will be automatically backed-up to 'Maps/mapname.eem_BeforeFormatUpdate' before conversion, but I still recommend that you backup your project first.

## [2025-07-14_1655](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-07-14_1655.exe) : (1.11 alpha 46)

### Changes:
- Temporarily disabled the auto-backup feature, as it causes too much editor slow-down and instability right now
- Holding 't' or 'g' in build mode will now quickly scroll the entity list

### Performance improvements:
- Enemy/weapon raycasts are now faster when shooting down
- Decals and particles perform better now

### Fixes:
- Removed secret x-ray vision feature when changing screen resolution
- Weapon movement animations were 'jumpy'
- Enabling 'player turn 1' could buffer mouse inputs and then cause the player to rotate when 'player turn 0' was called later
- Having many lights could cause weapon flickering
- Muzzleflash would still show with an alpha set to 0
- Weapons would show their muzzleflash colour while the flashlight was enabled
- Tilt direction was inverted when using a controller
- Improved depth sorting for transparent 3d models
- Transparent particles could cause rendering issues with transparent tiles
- Weapons wouldn't enter custom "DRAW" state if the previous weapon had a "HOLSTER" state
- Weapons wouldn't play the draw sound (aka "Pull out" or "Cock" ;) when switching from a weapon with a custom "HOLSTER" state
- Editor would crash while importing a trigger sound if the 'Voices' folder was missing
- Potential editor crash when trying to load language files
- 3D decoration models weren't shown in build mode unless the level had one of the models already placed
- There was an added delay when using map next/goto/start
- 'player check rotation' during a sequence would return the sequence camera's rotation rather than the player's rotation
- A potential failure during build/pack
- A performance issue + memory leak when loading sounds in a loop script (kept loading new sounds every frame instead of re-using the old ones)
- Improved enemy collisions with ceilings when spawned with an upward velocity

(A few new requested features will be coming in the next build, I wanted to prioritise stability first before adding anything new)



## [2025-07-10_2120](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-07-10_2120.exe) : (1.11 alpha 45)

All saves made in alpha 44 should be compatible with this build, and any 'broken' saves which crashed in alpha 44 should now load without crashing.  
There are a couple of potentially-breaking changes, so make sure you read those and do some testing prior to release.  
I recommend waiting at least a week to see if additional alpha builds get released, as it's possible some new bugs were introduced.  

### Potentially breaking changes:
- CHECKPOS no longer returns a negative y-axis. (you will need to adjust any fsm/script that used variables from this, as manually inverting the y-axis is no longer required)
- FSM has been fixed so it no longer skip actions when the frame time is lower than 1/fps (eg if running at 60fps: 1/60 = 0.0166, so fsm frames quicker than 0.0166 could be skipped). If you have an existing FSM which was affected by this issue, it may behave differently now. Frame delays of 0 are also now possible.

### New Features:
- Added a per-map option for baking placed lights into vertex colours. This avoids visual errors for maps with many dense lights, without the performance penalty of increasing lighting quality. It doesn't affect lights placed with scripts. This requires an update to PixelLighting.frag and PixelLighting.vert, you may need to manually delete these files if the update isn't applied automatically.
- Added 'player bobspeed [speed]' command, allowing you to override the viewbob speed (use it after 'player speed', otherwise it will be overwritten).
- Added 'invertx' and 'inverty' checkbox options to menu.script and config.ini, allowing mouse x/y to be inverted (create a new project to get the new menu.script)
- Added optional automatic backups to the editor. If enabled, this will create incremental backups every 5 minutes and whenever a project is opened, if any files have been changed since the last backup.  
A new button in the project list will allow you to restore to any previous backup.
- Added buttons to duplicate and rotate custom modifiers

### General Improvements:
- Made mouse movement much more consistent (switched to raw input)
- Added more bindable keys, avoiding the issue of some keybinds not saving when relaunching the game.
- When a script/fsm fails to convert text into a number (eg when you use a variable without a $), the issue will be logged to startup.log and 0 will be used.
- Improved indentation support in scripts
- 'Merge with level geometry' is now unchecked by default for new models (won't affect existing models)
- Per-pixel-lighting is now enabled by default when config.ini is missing
- Config.ini for the test build is now copied to the built game folder
- Resolution changes now apply instantly, rather than requiring a restart
- Decreased default item/injury flash opacity for new games
- Decreased default map ambient brightness
- Added 'ALPHA 45' to the editor title, to make support easier
- The entire 'map properties' panel now scrolls when the screen resolution is too low to fit everything
- Improved editor compatibility with mono (generally performs better than wine on linux)

### Performance improvements:
- 'skybox texture' now caches skyboxes instead of reloading them each time it's called (animated skyboxes run decently now)
- General FSM performance improvements
- Improved performance of entity movement/collision
- Reduced performance impact of 'hud image/mask/text' commands in loop scripts
- Improved launch times for games with high-resolution weapon sprites

### Fixes:
- Many lighting issues
- Many rendering/scaling issues at resolutions/ratios other than 1280x720/16:9
- Projectiles could sometimes go through enemies
- Some 3d models wouldn't spawn when loading a save
- Cryllic text with 'status' and 'hud text'
- A crash caused by solid 3d decorations when there was a gap in decoration ID's
- JUMPIFNOAMMO, JUMPIFNOAMMOTOTAL and JUMPIFHPLESS could continue executing actions in the original state after jumping
- SETVAR AMMO and MAGAMMO didn't work
- SETVAR HP always returned MAXHP instead
- SETVAR HP/MAXHP didn't work for weapons (now returns player's hp/maxhp)
- SETYAW/ADDYAW FSM actions would crash when a variable was used instead of a number
- Mouse wasn't locked to the game window
- Bullet/projectile spread didn't work when looking directly up/down
- 'player speed' ignored viewbob scale when calculating new viewbob speed
- HP could go below 0
- Using 'map next' or 'map goto' could make the first weapon temporarily show on screen, even if the weapon wasn't owned.
- Camera could clip through floor if player died while crouched
- z-fighting when an entity spawns an item
- Config.ini with a high resolution should no longer create a window larger than the native resolution
- Spawn weapon/ammo didn't work above 9 (eg Weapon12)
- Map scripts would restart if the player spammed inputs, which could also cause the pause menu text to disappear.
- Enemies couldn't walk on invisible or barrier tiles.
- 3d weapons were using normal/emissive textures for the muzzleflash plane
- RANDOM, POWER, etc only worked with =, rather than +=,-=, etc..
- Crash when there were more hud images than masks
- Crash when a 3d FSM used a frame number higher than the number of frames in the model
- The custom modifiers list wouldn't create a scrollbar when full
- 3D Decorations/Enemies with 'merge with level geometry' were being duplicated when saving/loading.
- Inaccurate line numbers for logged script errors
- Crash when spawning a particle with a missing/invalid texture
- Spark textures weren't spread when aiming directly up/down
- Large 'spark' particle images weren't centered correctly
- -data argument was ignored when Data.pak was present
- Crash when pressing delete in the 3d model editor and no entity was selected.
- Sometimes a crash could happen when loading a save.
- Invalid startup.log entry claiming to load model "" when models.dat ended with an empty line.
- Crash when Game.exe is used with an old Data.pak which has no skybox
- Player could get stuck on floor if healed after death.
- Crash when 'skybox texture' command was used on a map which didn't have a skybox.
- Many script/fsm stability issues (Most script errors should now be logged into startup.log, and script execution will attempt to continue after an error occurs)
- Status command would show '0' if any variables in the text hadn't been assigned
- Jumping while under a circle modifier or entity caused the player's y position to be set to 0
- Editor sometimes crashed while attempting to delete old builds/folders
- Scripted sun/ambient light settings weren't saved
- Scripted weapon stats weren't saved
- Starting a new game after scripting sun/ambient light or weapon stats caused the changes to carry over to the new game.
- 2D muzzleflash for 3d weapons wouldn't work when posteffects was enabled.
- 'settings set scale' caused zoomed/skewed rendering issues
- Sequences started from a map script could cause the player jump sound to play continuously every frame after the map restarts
- 'Manual' button didn't work
- Game would freeze if the pause menu was opened while a halted VN script was running, when using 'test current map'
- Camera would be frozen if map was changed or a game was loaded while a sequence was playing
- If a game was saved near an open door, entities on the other side of the door would be invisible until the door was closed and opened again.
- Various other random issues (memory leaks, unnoticable crash while game is closing, etc..)


## [2024_08-27_2027](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-27_2027.exe) : (1.11 alpha 44)
- Fixed rendering issues caused by the 'fog distance' command setting an incorrect fog start position.  
- Fixed model rendering issue when 'render all geometry' is checked in the map editor.  
- Fixed 'light offset' command. (lights weren't updating for tiles, y/z were flipped, incorrect unit-scale) (light offset [tileX] [tileY] [tileZ] [offsetX] [offsetY] [offsetZ])  
- More tile rendering performance improvements.   
- Added 'entity spawn unit [entity] [unitX] [unitY] [unitZ] [rotation]'.  
- Added "CHECKPOS [varX] [varY] [varZ]" fsm action for storing the decoration/enemy position in the specified variables.  

## [2024_08_22_2010](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-22_2010.exe) : (1.11 alpha 43)
- Fixed scripted music ignoring the music volume setting.

## [2024_08_22_1842](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-22_1842.exe) : (1.11 alpha 42)
- Reverted an optimisation which was causing MODELTEXTURE to affect all model instances.
- Reverted optimisations to outline rendering, as it was causing many visual issues.

## [2024_08_22_1416](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-22_1416.exe) : (1.11 alpha 41)
- Fixed a light rendering issue.

## [2024_08_22_0136](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-22_0136.exe) : (1.11 alpha 40)
- Fixed scripts sometimes restarting during a map start/return.
- Fixed broken texture animations for the first loaded tile.
- Fixed normal/emissive maps with animated textures.
- Fixed wall tile rendering when the editor is used with WINE on linux.
- Fixed muzzleflash affecting 2d weapon sprite transparency.
- Fixed an issue that would cause some decorations to be culled, even when 'disable culling' is checked.
- Many improvements to script safety, making it harder to crash your game with a bad script file.
- Many script issues will now be logged to the startup.log file when they're encountered.
- Added various other minor improvements to the script engine (for example: 'bind w test.script' and 'bind w test' will both work now)
- Added ROTMODE 3, allowing you to set a 3d model's rotation directly, rather than just its yaw.
- Added 'cheat [cheatcode] [scriptname]' command, so you can create custom cheats. (type directly while playing, not in console)
- Added optional volume and pan parameters to 'play sound' and 'play music': 'play sound/music [soundName/musicPath] [volume] [pan]' (volume 1 = normal, 0.5 = half, etc.. Can only make sounds quieter.) (pan 0 = left, 0.5 = middle, 1 = right. Only works with mono sounds)
- Deprecated 'entity spawnat/pos' in favour of three new commands:  
&nbsp;&nbsp;&nbsp;&nbsp;entity spawn tile [entity] [x] [y] [z] [rotation]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Spawns an entity directly in the middle of a specified tile (same as 'entity spawnat')  
&nbsp;&nbsp;&nbsp;&nbsp;entity spawn precise [entity] [x] [y] [z] [rotation]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Spawns an entity at an exact tile position like: 13.2 14.5 12.91  
&nbsp;&nbsp;&nbsp;&nbsp;entity spawn relative [entity] [x] [y] [z] [rotation]  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Same as 'spawn precise', but the position is added to the position of the decoration, terminal, trigger, or player.  
- Map music will now continue where it left off if a script ends with 'map (quick)return 1/2' without any scripted music playing.
- Improved performance of layer-switching in the editor.
- Made various other performance improvements.
- Made some **huge** improvements to tile and outline rendering performance.
- ~~removed sex~~

Deprecated commands will *not* be removed, and will continue to work as expected.  
In fact, right now I'd recommend the deprecated commands over the new ones, as the new ones haven't been tested thoroughly yet.  
But when 1.11 is final, the deprecated commands will not be recommended anymore, and they will be removed from the manual.  
My goal is to unify all the commands, so that everything will use the same x/y/z units.  
I find '1.5 tiles' to be much easier to use than '96 units', and I think new users in particular will benefit from this change.  


## [2024-08-12_1147](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-12_1147.exe) : (1.11 alpha 39)
- Allow variables to be used with 'SPAWN' fsm actions.

## [2024-08-12_1015](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-08-12_1015.exe) : (1.11 alpha 38)
- Fixed MODELTEXTURE fsm action affecting other entities of the same type.
- Fixed a player shadow rendering issue.
- Fixed a crash when a video is used for a startup title.
- Fixed title screens showing when opening the menu if the game was launched with 'test current map'.
- Fixed another crash caused by blank custom modifier names.
- Fixed 3d enemy hitboxes sometimes being sized incorrectly when spawned.
- Fixed z offset for 3d weapon FSM's.
- Fixed fps counter not showing values below 22.
- Fixed a flickering issue with per-pixel lighting. You may have to delete Shaders/PixelLighting.frag if this fix isn't applied automatically.
- Fixed issue with 3d weapon models being removed when importing a world/view/ammo model with a different name.
- Fixed normal/emissive textures on doors.
- Fixed the map floor being reset to 1 when closing some editor dialogues.
- Fixed position-based rotation for pickups.
- Fixed floor/wall textures not having spaces replaced with underscores during import.
- Fixed texture coordinates for gltf and fbx models.
- Fixed 90-degree rotation of gltf models.
- Bloom strength can now be set below 0.1.
- MODELTEXTURE fsm action can now optionally update normals and emissive textures: "MODELTEXTURE [path] [variable] [update normals? 0/1] [update emissive? 0/1]
- Added an option to allow 3d weapons to use a 2d muzzleflash without needing to add a 'muzzle' plane to the model.
- Added a 'Test Current Map' button next to the 'Test Game' button.
- Added 'hud text [name] [string] [font size] [x] [y] [r] [g] [b] [layer]' command. (use the same name to update previous text).
- Added 'hud active [0/1]' to hide/show all hud elements.
- Added game config option to disable weapon switching with the number keys.
- Added 'HEAL/HURT/SETHP [hp]' fsm actions.
- Added 'settings check/set timescale [var/value]' for adjusting gameplay and audio speed. Default is 1.
- ~~Added sex.~~

## [2024-07-30_1403](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-30_1403.exe) : (1.11 alpha 37)
- Fix crash when closing weapon pos/scale editor if an idle sprite hasn't been loaded.
- Fixed gravity not being reset when starting a new game.
- Added player jump height to save data.
- Fixed ROTMODE with multiple 3d enemies/decorations of the same type.
- Fixed inaccurate yaw offset for 3d enemies.

## [2024-07-29_2248](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-29_2248.exe) : (1.11 alpha 36)
- Fixed a scripting issue when multiple '}' are put on the same line (I'll stop now)

## [2024-07-29_2218](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-29_2218.exe) : (1.11 alpha 35)
- Fixed an issue processing 'if' statements if the '{' is placed on the next line.
- Reduced 'directional snapping' with scripted player velocities.

## [2024-07-29_2015](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-29_2015.exe) : (1.11 alpha 34)
- Fixed a crash when saving a game that doesn't use 3d enemies (not sure how I missed that...).
- Fixed rotation issue with 3d decorations.
- Limited player rotation to a 0-360 range.

## [2024-07-29_1706](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-29_1706.exe) : (1.11 alpha 33)
- 'Authors' screens will no longer show when using 'test current map' in the editor.
- Made the editor more usable at lower screen resolutions.
- Added an 'Auto fit' button to the weapon position/scale editor, making it easier to find large weapon sprites.
- The editor will automatically update pixellighting.frag if it's missing or if an older version is detected (will not overwrite it if you've made any changes to the file).
- Muzzleflash is now a colour picker instead of a checkbox and also works for melee weapons. Adjust the alpha value to adjust the flash strength.
- Loop scripts will now work while the player is dead.
- Improved 3d enemy rotation in flee/chase states.
- Added ROTMODE fsm action to override the 3d model rotation mode. 0 = normal, 1 = always face player, 2 = freeze rotation.
- Added SETYAW and ADDYAW fsm actions to override the model's yaw.
- Added hud images/masks to savedata.
- Added all fsm state info to savedata.
- Added 'saveauto' and 'loadauto' for accessing auto saves from menu.script.
- Added optional emissive textures if per-pixel lighting is enabled (TextureName_emissive.png in the same folder).
- Fixed unlit 3d decorations when per-pixel lighting is enabled.
- Fixed the flashlight flashbang when per-pixel lighting is enabled.
- Fixed 'flashlight range' when per-pixel lighting is enabled.
- Fixed depth sorting with 3d weapon muzzleflash (again...).
- Fixed the sprite/weapon scale editor not changing with the scrollwheel if the scale is near 0.
- Fixed the 'player check maxarmour' command.
- Fixed comments causing issues in state files.
- Fixed 'tab' characters causing issues in state files.
- Fixed 'bind' command causing vn-like delay when used in a normal script.
- Fixed variable copying (a=$b) not working in scripts.
- Fixed yaw being ignored for 3d enemies.
- Fixed decoration model yaw being ignored when 'always face player' is checked.
- Fixed crash when replacing the weapon's idle sprite after using the 'position and scale' editor.
- Fixed a crash caused by having a blank custom modifier name.
- Fixed a bug that could cause enemy hitboxes to shrink after loading.
- Fixed CAMSPEED not working in FSM.
- Fixed nested 'if' statements in the script engine.


## [2024-07-21_1858](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-21_1858.exe) : (1.11 alpha 32)
- Title screens can now optionally be videos (Titles/Authors1.vid instead of Titles/Authors1.png).
- Added option to make 3d models always rotate to face the player.
- Initial support for new 3d model formats: fbx, gltf/glb, dae, obj. These formats currently only support static models, as they use a different animation method to md3 files.
- Added "player jumpheight [$height]" (default is 256).
- Fixed crash when using 'map next' as a single-line console command ";map next".
- Fixed stats not transferring to next level when "map next" command is used.
- Fixed new maps not having the .eem extension.
- Fixed 3d decoration collision when using an offset with a scale other than 1.
- Fixed 3d decoration collision when spawning a decoration with fsm.
- Fixed crash when a projectile-shooting enemy is created after multiple consecutive enemies were deleted.
- Fixed a crash when loading a project after deleting a tile texture.

This will probably the last 1.11 alpha that adds new features.  
I'll be focusing on bug fixes and small improvements to the existing features to prepare for a release on itch.io.  


## [2024-07-17_0044](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-17_0044.exe) : (1.11 alpha 31)
- Fixed multi-texture model rendering if 'merge with level geometry' is checked.
- Fixed potential Enemies.dat corruption when opening a project.
- Creating a map will now ask for a map name instead of a file path (file location was ignored anyway).
- Added an option to disable fog culling (Terrible for performance, but avoids a rendering issue when using cylinder/cube skyboxes).
- Added map button tooltips to the language file.
- Fixed a crash while closing the game (maybe I should have left it in for faster closing times?).
- Fixed a culling issue when the player or entities are above the highest-placed tile.
- Added a checkbox to make a 3d model double-sided (bad for performance, but useful for thin geometry like grass).
- Fix light data not being loaded properly from savefiles.

## [2024-07-14_1111](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-14_1111.exe) : (1.11 alpha 30)
- Fixed crash when moving to the next map if there are no weapons in the game.
- Fixed an issue causing video playback to get stuck.
- Videos are now skippable.
- Added 'timeout video' command to wait until the current video has finished.
- Added lights to savedata.

## [2024-07-14_0023](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-14_0023.exe) : (1.11 alpha 29)
- Fixed map script being partially re-executed when a savefile is loaded.  
- Fixed editor crash when opening the game info configurator if the currently selected 'starting weapon' was removed.  
- Fixed invisible door collision if the game is saved/loaded while a door is open.  
- Attempt to prevent enemies getting stuck on eachother.  

## [2024-07-13_2149](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-13_2149.exe) : (1.11 alpha 28)
- Fixed crash related to enemies spawned with forward velocity.

## [2024-07-13_2123](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-13_2123.exe) : (1.11 alpha 27)
- Fixed collision with enemies which were spawned with forward velocity but don't leave the IDLE state.

## [2024-07-13_1819](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-13_1819.exe) : (1.11 alpha 26)
- Added complete door state to savefile data (open state, lock status, etc..).
- Enemies spawned with forward force from a weapon will now have collision as soon as they leave the player's radius, instead of when the velocity reaches 0.
- Enemies spawned with a forward velocity should now work properly even if their state changes (not 100% sure because I couldn't reproduce the issue).
- Fixed a crash when accessing variables from a dev console command.

## [2024-07-13_0000](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-13_0000.exe) : (1.11 alpha 25)
- Fix enemies getting stuck on tiles/decorations.
- Fixed player teleport.
- Added ability to execute single-line script commands from the console with ';' eg: ";player teleport 1 2 3".
- Moved textboxes back up to where they were before the scaling changes were added.
- Fixed rendering issue when using multiple camera actions in a sequence animation.

 ## [2024-07-11_2236](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-11_2236.exe) : (1.11 alpha 24)
- Armour amount is now transferred between levels.

 ## [2024-07-11_2043](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-11_2043.exe) : (1.11 alpha 23)
- Fixed a rendering issue when using the 'settings set scale' command.
- Improved performance of the 'settings set scale' command.
- Fixed test mode not working when the project has a space in its name.
- map start/return is now optional. Scripts will automatically insert a 'map start' or 'map return 2' at the end if you don't include your own.
- Fixed weapon mag and ammo not transferring between maps.
- Spawned 3d model rotation/scale is now restored properly when loading save data (old savefiles will not load with this version).
- Improved sprite scaling with the scrollwheel (now scales proportionally, making it more useful at both higher and lower scales).
- Added a game setting to prevent enemy stacking.
- Maps can now have more than one exit.

## [2024-07-04_2134](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-04_2134.exe) : (1.11 alpha 22)
- Fixed create/open map buttons not appearing after creating or opening an empty project (broke in last update)

## [2024-07-04_1555](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-04_1555.exe) : (1.11 alpha 21)
- Fixed broken slope and cornerslope modifiers when using negative scales/positions.
- Fixed enemies with negative forward velocity moving through walls.
- Added "settings set scale [$scale]" to set the current render scale.
- Prevent maps being created/opened without opening a project first.
- Prevent any editors/importers from being used before a project is opened.

## [2024-07-03_2015](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-03_2015.exe) : (1.11 alpha 20)
- Fixed menu checkbox flickering.
- Added 'player check aimtile [tileX] [tileY] [tileZ]'. It will store the coordinates of whatever tile the player is looking at. If the player isn't looking at a tile, all coordinates will be set to -1.
- Sounds started from triggers/scripts will no longer be interrupted if many other in-game sounds are played.
- Fixed an editor crash when using the enemy or decoration editor before creating a map.
- Fixed a crash that could occur when reloading a level.

## [2024-07-01_1553](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-07-01_1553.exe) : (1.11 alpha 19)
- Fixed videos not scaling to the game resolution when starting from a script.
- Menu checkbox text can now be changed with the 'mcheckboxstyle' command in menu.script files.  
		mcheckboxstyle "Off" "Hover Off" "Hover On" "On"  
		eg; mcheckboxstyle No -No- -Yes- Yes  
- Weapon outline scale now respects the 'outlinewidth' setting
- Fixed crash when a weapon has a 3d ammo model, but not a 3d view model
- The colour picker now matches the editor's theme
- Made 'light sun direction' align with the same xyz directions in the map editor
- Fixed crash when 'player check rotation' is used without specifying both an x and y output variable

## [2024-06-27_1436](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-27_1436.exe) : (1.11 alpha 18)
- Fixed player colliding with enemy barrier blocks (Broke in Alpha 15).
- Fixed an editor crash when dragging the rectangle-fill outside of the map bounds.
- Adjusted some editor UI elements to avoid long translation text getting cut short.
- Fixed a crash that would occur if you tried to create a decoration after your project's Sprites/Decorations folder was deleted (same for enemies, weapons, etc..)
- Added debug output when loading the pixellighting shader to startup.log
- Fixed a bug causing the player's weapons to disappear if a map script ends with 'map goto' or 'map next' instead of 'map start'

## [2024-06-23_2001](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-23_2001.exe) : (1.11 alpha 17)
- Added sfml error output to startup.log (may help with finding issues)

## [2024-06-23_0112](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-23_0112.exe) : (1.11 alpha 16)
- Fixed player collision with non-cube tiles (accidentally broke in alpha 15)

## [2024-06-23_0030](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-23_0030.exe) : (1.11 alpha 15)
- Fixed enemies spawned with a forward velocity not 'bouncing' or being affected by a collision with a wall.
- Fixed a crash that could occur if an enemy was deleted from a project.
- Fixed an editor crash when the currently-selected weapon/ammo/hp/key/armour sprite is replaced.
- Fixed a culling issue when looking up and down near large decorations.
- Fixed vn mode with looping scripts (broke in last update).
- Made it harder for swarms of enemies to push the player out of bounds.
- Creating a weapon will now create placeholder weapon and ammo sprites (instead of a decoration sprite...).
- Added a 'knockback' stat for enemies, allowing enemy attacks to push the player back.
- Added tooltips for enemies and decorations that were placed on the map.

## [2024-06-16_0119](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-16_0119.exe) : (1.11 alpha 14)
- Added speed parameter for vn textboxes (text string [r] [g] [b] [characters per second, default is 80]).
- Improved vn textbox scaling.
- Looping scripts are now executed while other scripts are running, unless vn mode is active.
- Improved projectile collision detection.
- Fixed entities spawned with forward velocity not having collision (will still go through walls if spawned in front of player when standing next to a wall)
- Fixed a crash when killing an entity spawned with forward velocity.

Just a sidenote...  
If you have a game that was built with an older version of the engine and don't have access to the project files, you can still apply the latest engine fixes.  
The engine is almost 100% backwards-compatible with all versions from around v1.5 and later, so you can replace the Game.exe from an older game with one that was exported with a later engine update, and it will have all the latest fixes applied automatically.  
Might be useful if you're hosting a game jam and want the latest fixes applied to all the games ;)  

## [2024-06-12_1110](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-12_1110.exe) : (1.11 alpha 13)
- Fixed forward velocity parameter for 'SPAWN' fsm action (wrong direction, and enemies weren't moving properly)
- Fixed a one-frame input interruption when exiting a script with 'quickreturn'
- Fixed weapon range not being saved/loaded correctly in some regions
- Fixed gaps in tile placement when drawing quickly with the mouse.
- 'import' button in weapon sound editor was incorrectly labelled as 'accept'
- Removed unused 'Game font' item from the system resources importer.

## [2024-06-08_1214](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-08_1214.exe) : (1.11 alpha 12)
- More transparent rendering fixes.
- Fixed a crash when launching a game with no weapons added.

## [2024-06-08_0025](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-08_0025.exe) : (1.11 alpha 11)
- Lots of transparent rendering fixes.

## [2024-06-07_2041](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-07_2041.exe) : (1.11 alpha 10)
- Use alpha blending instead of alpha clipping.
- Fixed collision rotation with spawned 3d decorations.

## [2024-06-07_0052](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-07_0052.exe) : (1.11 alpha 9)
- Fixed doors being stuck closed if the 'door close' command is used.
- The 'bind' command can now be used from any scripts.
- Added the 'unbind [key]' command to remove an existing keybind.
- Holding the left/right arrows in build mode will cycle through the numbers.
- The map editor is now reset properly when creating/loading projects.
- The 'console' keybind can be changed in the [input] section of config.ini. Default is: "console=tilde"
- Prevent things being spawned with the "SPAWN" fsm action moving slightly towards the player.

## [2024-06-04_2008](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-04_2008.exe) : (1.11 alpha 8)
- Added "hud autoscale [image/mask name] [stretch/width/height/off]" command.
- Added "settings check resolution [resX] [resY]" command.
- Fixed rectangle fill tool in the editor.

## [2024-06-04_1230](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-04_1230.exe) : (1.11 alpha 7)
- Hud images/masks are now scaled with screen resolution
- Added "hud rotate [image/mask name] [rotation]" (angle in degrees)
- Added "hud scale [image/mask name] [x] [y]" (1 = original size, 0.5 = half size, etc..)
- Added "hud origin [image/mask name] [x: 0 to image width] [y: 0 to image height]" (Sets point within the image where position/scaling/rotation will be based on. Default is top-left corner at 0,0)
- Fixed 3d model textures not loading correctly when 'per-pixel lighting' is disabled.

I started improving the 'sequence animator' a few updates ago but forgot to mention it.  
It's a feature that allows you to animate the camera and entities.  
JessicoChan added it a while ago but for unknown reasons never documented it publicly.  
It hasn't been tested much, but I figure it's worth documenting here for anyone who wants to try it out now.  
  
In a script file, call "sequence start [sequenceName]"  
It will search for a .seq file in the 'Sequences' folder, eg: Sequences/sequenceName.seq  
seq files have the following syntax:  

- action camera - Animate the camera.  
- action entity [x] [y] [z] - Animate an entity at the specified x,y,z coordinates.  
- start [x] [y] [z] - Position to start animation from.  
- end [x] [y] [z] - Position to end animation on.  
- rotationstart [x] [y] [z] - The rotation at the start of the sequence.  
- rotationend [x] [y] [z] - The rotation at the end of the sequence.  
- statestart [state name] - State to set the entity to when the sequence starts.  
- stateend [state name] - State to set the entity to after the sequence ends.  
- time [seconds] - How long the animation will run.  
- parallel - Allows more than one sequnce to run at the same time.  

Here's an example of a camera animation:  
> action camera  
start 7 6 0.5  
end 7 15 0.5  
rotationstart 0 0 0  
rotationend 0 360 0  
time 2  

This will animate the camera for two seconds from 7,6,0.5 to 7,15,0.5, rotating 360 degrees in the y-axis.  
Save it as Sequences/demo.seq, and call it from a script with: "sequence start demo"

## [2024-06-02_1031](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-02_1031.exe) : (1.11 alpha 6)
- Fix off-by-one error with CUSTOMPARTICLE IDs

## [2024-06-02_1013](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-02_1013.exe) : (1.11 alpha 5)
#### WARNING: THIS UPDATE WILL MAKE YOUR MAP FILES INCOMPATIBLE WITH OLDER VERSIONS OF EFPSE.
Maps will be automatically backed-up to 'Maps/mapname.eem_BeforeFormatUpdate' before conversion, but I still recommend that you backup your project first.
- Increased max floor count to 64.
- Map files are now trimmed to the highest floor with data (if your highest tile/entity is on floor 4, Only floors 1-4 will be saved).
- Reduced the editor's memory usage to roughly 1/3 of what it was.
- Added 'JUMPIFNOAMMOTOTAL' fsm action, because 'no ammo' really means 'no mag ammo'.
- Added 'AMMO' and 'MAGAMMO' as SETVAR options.
- Added the ability to toggle muzzleflash for individual weapons.
- Fixed an editor crash when decoration/enemy sprite scale is set to a negative or a non-number value.
- Fixed weapon scale not working correctly in some regions.

## [2024-06-01_1443](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-01_1443.exe) : (1.11 alpha 4)
- Added "player velocity [set/add] [x] [y] [z]" command.
- Added 'db.' variable scope. 'db' values are saved to the Saves/db.txt file, offering a form of persistent storage that isn't tied to a save file. (File writes aren't optimised yet, probably terrible in looping scripts right now).
- A 'global.deltaTime' variable will be set and automatically updated for looping scripts, providing the amount of seconds which have passed since the last frame.
- Fixed an issue that could break triggers if any of them were set to an audio file instead of a script.
- Fixed an issue that would cause meshes without a normal map to be rendered with one.
- Fixed an issue that would cause some tiles to be rendered without their normal map applied.
- Added normal map support for md3 models (modelName_normal.png, and modelName_materialName_normal.png for each material)

## [2024-06-01_1025](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-01_1025.exe) : (1.11 alpha test 3)
- Normal maps are now smoothed when texture interpolation is enabled
- Fixed cube skybox rendering height
- Added a wireframe cheat (very useful, I know)
- Weapons/sprites can now be positioned and scaled in the editor by dragging and scrolling

## [2024-05-31_1216](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-05-31_1216.exe) : (1.11 alpha test 2)  
- Added preferences menu.
- Initial support for editor translations (any .yaml files in the 'Languages' folder will be added as a language in the preferences menu).
- Started adding a dark theme (Needs work. Default theme looks different right now, and winforms adds borders to everything that aren't all easy to change).
- Testing a different spawn method for the 'SPAWN' fsm action (probably broken).
- Added checkbox in game info configurator for weapon sprite smoothing (might move to in-game graphics menu).
- Added checkbox in game info configurator for entity rotation mode.
- Added number box in game info config for vertical camera rotation limit.
- Added crouch height to the player configurator.
- Added ability to add new weapons in the editor.
- Fix distance culling issue when using cube skyboxes.


## [EasyFPSEditor_CE_DEV_2024-05-28_1605](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-05-28_1605.exe) : (1.11 alpha test 1)
- flashlight state [0/1]
- flashlight lock [0/1]
- flashlight range [range]
- flashlight colour [r] [g] [b]
- flashlight radius [radius]
- SETVAR PLAYERDISTANCE
- SETVAR PLAYERVISIBLE
- hud mask (same as hud image syntax but masks images on the same layer)
- weapon limit increased to 1024 (requires manual weapon.dat modification, editor support not complete yet)
- light ambient [r] [g] [b] [a]
- light sun colour [r] [g] [b] [a]
- light sun direction [x] [y] [z]
- skybox texture Path/To/Texture.png
- fog colour [r] [g] [b]
- fog distance [dist]
- shader texture [uniformName] [Path/To/Texture.png]
- shader bool [uniformName] [0/1 or true/false]
- shader int [uniform] [int value]
- shader float [uniform] [float value]
- shader vec2 [uniform] [x] [y]
- shader vec3 [uniform] [x] [y] [z]
- shader vec4 [uniform] [x] [y] [z] [w]
- light offset [x] [y] [z] (moves light without updating its tile position, allowing lights to be moved around without needing to recalculate the new position)
- Many advanced math commands (SIN,COS,TAN,ASIN,ACOS,ATAN,ATAN2,POWER,SQRT,ABS,FLOOT,CEIL,CLAMP,MIN,MAX,ROUND). varX=SIN($varY)
- Build mode improvements for 3d models
- Tile textures will now look for Textures/tileName_normal.png and Textures/tileName_dxnormal.png to optionally use normal maps (in opengl or directx format) on walls/floors (models to come in full release)
- Md3 models will look for modelname_material.png When loading (eg; if model 'tree' has two materials 'bark' and 'leaves', it will try to load 'tree_bark.png' and 'tree_leaves.png')
- Player y-rotation limit can be applied by modifying game.dat (editor support and script command will be in 1.11 release)
- Enemy/Decoration rotation mode can be changed by modifying game.dat (editor support coming in 1.11 release)
- Various issues have been fixed
- Various issues have been added
- Probably a bunch of things I forgot to mention

Some of these changes may be completely broken, so testers would be greatly appreciated :)  
Remaining plans for 1.11:
- ~~Editor preferences menu~~
- ~~External editor language files~~
- Editor colour schemes/themes
- Update editor to support the new features (~~weapon/floor counts,~~ flashlight adjustments, ~~rotation mode, y-rotation limit~~)
- ~~Support normal maps for md3's~~
- Add all this new data to the save file format, so the previous state is restored properly on load
- ~~Possibly some velocity commands/actions (needs investigation)~~
- ~~Potentially increase level height to 64 (need to do some performance testing)~~
- ~~Maybe a new variable scope that's always kept after death (Checkpoints, life counters, achievements, gameplay stats, etc...)~~
- More bug fixes
