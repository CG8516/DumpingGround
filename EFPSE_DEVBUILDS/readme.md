## Use these builds at your own risk!
##### Due to the high chance of bugs/issues, you run a much greater risk of corrupting your project.
##### Always backup your projects before trying a new development build.

### WARNING: THE LATEST UPDATES WILL MAKE YOUR MAP FILES INCOMPATIBLE WITH OLDER VERSIONS OF EFPSE.
#### Maps will be automatically backed-up to 'Maps/mapname.eem_BeforeFormatUpdate' before conversion, but I still recommend that you backup your project first.

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
