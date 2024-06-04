## Use these builds at your own risk!
##### Due to the high chance of bugs/issues, you run a much greater risk of corrupting your project.
##### Always backup your projects before trying a new development build.

### WARNING: THE LATEST UPDATES WILL MAKE YOUR MAP FILES INCOMPATIBLE WITH OLDER VERSIONS OF EFPSE.
#### Maps will be automatically backed-up to 'Maps/mapname.eem_BeforeFormatUpdate' before conversion, but I still recommend that you backup your project first.

## [2024-06-04_1230](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2024-06-04_1230.exe) : (1.11 alpha 7)
- Hud images/masks are now scaled with screen resolution
- Added "hud rotate [image/mask name] [rotation]" (angle in degrees)
- Added "hud scale [image/mask name] [x] [y]" (1 = original size, 0.5 = half size, etc..)
- Added "hud origin [image/mask name] [x: 0-1] [y: 0-1]" (Sets point within the image where position/scaling/rotation will be based on. Default is top-left corner at 0,0)
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
- flashligh colour [r] [g] [b]
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
- Update editor to support the new features (~~weapon~~/floor counts, flashlight adjustments, ~~rotation mode, y-rotation limit~~)
- ~~Support normal maps for md3's~~
- Add all this new data to the save file format, so the previous state is restored properly on load
- ~~Possibly some velocity commands/actions (needs investigation)~~
- Potentially increase level height to 64 (need to do some performance testing)
- ~~Maybe a new variable scope that's always kept after death (Checkpoints, life counters, achievements, gameplay stats, etc...)~~
- More bug fixes
