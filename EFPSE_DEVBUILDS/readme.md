## Use these builds at your own risk!
##### Due to the high chance of bugs/issues, you run a much greater risk of corrupting your project.
##### Always backup your projects before trying a new development build.

### WARNING: THE LATEST UPDATES WILL MAKE YOUR MAP FILES INCOMPATIBLE WITH OLDER VERSIONS OF EFPSE.
#### Maps will be automatically backed-up to 'Maps/mapname.eem_BeforeFormatUpdate' before conversion, but I still recommend that you backup your project first.

## [bugtest](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_bugtest.exe) : (1.11 bugtest)
There's *many* fixes, some changes, and a few QoL improvements.  
To make things interesting (and to try and get people to thoroughly test/check every part of the engine), some of the changes and additions are a secret!  
Consider this a very late easter egg hunt :)  

There are some changes you should definitely know about though, because they could cause issues with existing games:
- Terminal decorations now use the decoration's collider more accurately, so you may need to adjust the radius/scale of some terminal decorations to make them interactable again. (colliders cheat now shows terminal decoration colliders properly, which should help).
- Setmaxhp/setmaxarmour commands now apply limits instantly, and will reduce hp/armour if it's above the max. (one game I tested had 'player setmaxhp 0' in a script, which now kills the player).
- Hud images/text with a layer below 0 will now be rendered behind the default hud elements (hp, status, background, etc..).
- 'light move', 'light offset' and 'light status' commands now affect 'all' lights in the specified tile. Previously it only affected the first light it found in the tile, which could change unpredictably each time the script was used.
- 'light sun colour' now uses 0-255 rgb values instead of 0-1, improving consistency across commands.
- Enemies would enter CHASE automatically, even if there was no jump to it. If you have an enemy with a custom fsm that's no longer chasing the player, make sure you have a jump to CHASE in it (eg 'state SEE CHASE 0').
- mpeg1 .vid files now have working audio, so you may now have audio-doubling if you were playing an audio track at the same time as your video.

And to make things a bit easier, here are some additions that I think probably wouldn't have been found:
- The bind and unbind script commands now work with controller buttons (button names: c_dpadup, c_dpaddown, c_dpadleft, c_dpadright, c_start, c_select, c_a, c_b, c_x, c_y, c_l1, c_l2, c_l3, c_r1, c_r2, c_r3. a/b/x/y uses xbox layout)
- SETTARGET fsm action, allowing you to set where an enemy should move towards (CHASE/HURT/FLEE will overwrite this) SETTARGET [x] [y] [z] [stop at target: 0/1, default = 1] [speed: default = enemy speed]
- STOP fsm action, to stop entity movement from a custom state, without needing to jump to idle/hurt/dead.

I'll leave the rest up to you to find :)  
Have fun, and always make a backup before trying any new builds!

Fixes:
- Enemy blob shadows work again.
- Potential crash when "shader set texture" was used with an invalid path/file.
- Fixed scripts ending after using a #include
- Crash when loading a game which contains a weapon/entity with an empty .states files.
- Potential crash when loading a savefile in a game that has spaces in its name.
- Crash if game had no key textures.
- Potential crash if hp.dat had less than 4 entries.
- Custom menu checkboxes didn't assign the default db variable.
- Potential crash if a script tried to give/take/check keys/weapons/ammo with a non-existent ID.
- Fixed slight misalignment with 'bg' images and videos when playing at a resolution other than 1280x720.
- Barrier blocks were blocking bullets and projectiles.
- 3D models in build mode wouldn't be visible until you scrolled to them, scrolled away, then scrolled back again.
- Keybound scripts that ended with quickreturn could interfere with build mode controls (eg script bound to t/g could cause list to scroll very quickly)
- Player height wasn't saved/loaded properly, and wouldn't reset when starting a new game.
- More fsm errors are now caught and logged in startup.log instead of crashing.
- Projectiles could pass through walls (and could hurt the player through thin walls).
- Player was unable to jump if the ceiling was low and they had a high jump height.
- Player could push their face through walls if they were crouched under a low ceiling.
- Made player auto-ducking a bit more reliable.
- Potential crash when loading a game that has exploding enemies.
- Memory leak when loading sounds from a script.
- Added a safety check when posteffects/renderscale is enabled, hopefully preventing crashes on unsupported gpu's (can't confirm if it's fixed, as I have no hardware experiencing this issue)
- Decals are now rendered before entities, avoiding rendering issues with transparent entities.
- Weapon scrolling didn't always match the currently held weapon.
- Using 'MODELTEXTURE' in fsm could spam errors in startup.log if the optional params weren't specified.
- Tiles with cubemap textures could have unnecessary interior faces when you place them next to each other (The whole texture was being checked for transparency, rather than just the visible faces).
- Minimap is now scaled like the other hud elements at resolutions other than 1280x720.
- Decals weren't being frustum culled.
- Writing to arrays in FSM was unreliable.
- Some errors were being logged incorrectly (eg "failed to convert '' to a number").
- Random/intermittent crash if an enemy had a .states file with no valid state definitions.
- Triangle custom modifiers could have weird UV stretching.
- Animated models with animation smoothing enabled could render larger than they were supposed to when playing at a low fps.
- If a script bind in the menu wasn't already bound when the game started, rebinding wouldn't work properly until after you restarted the game.
- Rare script/state processing error caused by multiple spaces at the end of lines, with a comment after the spaces.
- non-ascii text only worked in scripts if it had quotes around it.
- The "double sided" checkbox for custom modifiers only affected the newest shape within the modifier, rather than all of them.
- Many inconsistencies between the custom modifier preview and how the modifier actually appeared in game.
- Rotating whole modifiers 90/-90 degrees didn't always work properly.
- Modifier movement/rotation could cause slight imprecisions (eg each rotation could add/subtract 0.0001).
- Pressing ctrl+s while "door type" was selected would set the door type to "side", because it starts with 's'.
- Spawning an entity via fsm with "0,0,0 0,0" would cause the spawned entity to move slightly towards the player (caused by the z-fighting fix from alpha 45, but I'm using a better method now).
- "enemieslifetime" option in config.ini has been fixed and renamed to "corpsetimer" (renamed because the default was 10, and everyone's games would have suddenly started making enemies disappear after death)
- Crash when using mjpeg videos.
- Potential crash with invalid .vid files (mpeg1 only supports a few framerates, and imgstreamcreator didn't detect when ffmpeg failed to convert).
- Playing more than one video from a script would cause the other videos to be scaled incorrectly.
- Fog distance/colour wasn't saved/loaded.
- Input was sometimes processed when the game was in the background.
- Transparency rendering issues on some amd gpu's.
- "settings set scale" would zoom in/out instead of just adjusting the resolution, if used from the cheat console.
- "settings set scale" was doing a lot of unnecessary work when the scale was already set to the desired value.
- Clicking apply in the settings menu after using the "settings set scale" command would cause the current render scale to be saved to config.ini.
- Player could float on the corners of custom modifiers.
- Static lights weren't being saved correctly.
- Bound scripts which ended with quickreturn could interrupt level transitions.
- Resources for enemy states were being loaded more than once, causing excess memory usage and slower loading times for maps with enemies which had many high-resolution sprites.
- Collision code was doing something stupid, which was hurting performance on maps with many enemies.
- FSM actions directly after a MODELTEXTURE command could potentially be skipped.
- Enemies without a HURT state could still be stun locked.
- A couple of potential crashes if the player had a weapon with an invalid fsm.
- Scripted sounds would stop the first time any non-map/loop script was run, even if they ended with return/quickreturn 2/3.
- SETVAR RANDOM didn't work with variables (eg SETVAR x RANDOM($abc,$map.def)).
- Tile frustum culling wasn't accurate, especially when looking down from a tall height.
- Changing maps while in build mode would make the build UI disappear.
- The lightingquality menu setting didn't let you choose all options from 0-5.
- Fixed potential crash when using performance profiler.
- Thin cylinder modifiers had broken/stretched textures.
- Slope and circle modifiers didn't render when a cubemap texture was used.
- UV stretching on some rectangle modifiers with cubemaps.
- Lighting didn't work properly with 3d weapons.
- Camera rotation speed was affected by frame rate when using a controller.
- Moving your mouse when using a controller would cause the cursor to jump to the middle of the screen.
- A few controller inputs could be spammed when held (dialogues, jumping, interaction).
- Controllers couldn't press vn buttons.
- Pressing 'escape' to cancel rebinding an input would unpause the game.
- Fixed some tab indexes in the editor.


## [2025-12-09_2129](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-12-09-2129.exe) : (1.11 alpha 60)

### Additions:
- Added 'fsmdebug' cheat, which shows the current state, frame, and hp of all entities.

### Fixes:
- 'entity move/delete' could target an adjacent tile instead of the one specified.
- Saving could sometimes add duplicate sounds to the save file, leading to possible audio issues after loading.
- Scripted music didn't continue after loading.
- Hud image blending was inconsistent with earlier versions.
- Player would be in a corrupt state if no 'Player' object was placed on the map.
- Crash if HUD/Cursor.png was missing.
- Keys bound to scripts which ended with 'map quickreturn' could prevent that key being used for anything else (eg scripts bound to wasd could break walking).
- Passing the -map argument to Game.exe with a map that didn't exist would cause the game to get stuck rendering a completely blank menu.


## [2025-12-02_1647](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-12-02_1647.exe) : (1.11 alpha 59)

### Potentially breaking changes:
- "entity delete [x] [y] [z]" will now delete all entities within the specified tile, including entities which aren't in the exact center of the tile.
- "entity move [tileX] [tileY] [tileZ] [offsetX] [offsetY] [offsetZ]" no longer ignores tileZ, and will now move all entities within the tile, rather than moving one enemy exactly in the center of the tile.

### Additions:
- Added the left/center/right alignment option for labels (never existed but was falsely documented)
- Added optional alignment for hud text (hud text [name] [string] [font size] [x] [y] [r] [g] [b] [layer] [alignment: left/center/right])
- Added 'map' menu button functions, eg: mbutton [visible text] [x] [y] "map0" [menuPage], will start a new game on the first map (map0, map1, map2, etc..)

### Changes:
- Improved the security of Data.pak files (Nothing will ever be uncrackable, but the difficulty of creating an unpacker for alpha 59+ games has been raised)
- Performance profiler now displays averages for the past 60 frames, rather than just the previous frame's stats.
- Reduced performance impact of hud images / hud text when no masks are used (most noticable on low-spec laptops)

### Fixes:
- Potential collision-related crash
- The occlusiontest setting didn't work
- Potential crash when loading maps which contained deleted ammo/weapons
- Improved reliability of raycasts against 3d models


## [2025-11-18_1735](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-11-18_1735.exe) : (1.11 alpha 58)

### Additions:
- The engine will now try to create a crash.dmp file if it crashes. If you send me a crash.dmp, it will help me fix the issue.
- Performance stats can be enabled with the 'perf' cheat. This gives you a general idea of what's taking the most time in each frame.
- Added 'light createstatic' script command (exact same parameters as 'light create'). This lets lights spawned in a map script get baked if 'vertex chunk lighting' is enabled.

### Fixes:
- Hazard tiles on floors above the player could still hurt when passing below them.
- Jump sound would be spammed if the player hit their head while jumping.
- Disabled floor collision in build mode (accidentally enabled it again in 57).

## [2025-11-17_1530](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-11-17_1530.exe) : (1.11 alpha 57)

### Fixes:
- Using noclip would cause the player to sink through the ground and the land sound to be spammed (sorry for the hearing damage)
- FSM actions in the DEATH state could be skipped
- Issues with hud images when starting a new game
- A potential inconsistent crash
- Typing in the cheat console would run key-bound scripts and could spam letters
- 3D weapons could render as completely black/white for a couple of frames after loading

## [2025-11-16_2256](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-11-16_2256.exe) : (1.11 alpha 56)

- Fixed a crash related to custom modifiers

## [2025-11-16_2234](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-11-16_2234.exe) : (1.11 alpha 55)

### Breaking changes:
- 'player weapon draw' is no longer off by 1 ("player weapon draw 1" would draw weapon 2).

### Potentially breaking changes:
- FSM states that have "NONE" as the next state will only run once per frame, rather than potentially looping many times in the same frame. This reduces the performance impact of states with very short frame times.
- FSM timing has been adjusted to improve consistency at different framerates (still not 100% consistent, but it's much better than before).
- Improved hinged door UV's

### Additions:
- Added 'Jump Enhancements' setting to the game config (enabled by default). This buffers jumps a few milliseconds before landing and a few milliseconds after walking off an edge, making jumping feel more responsive.
- Added optional 'damage' parameter to 'EXPLOSION' fsm action (default is 80): EXPLOSION [name] [radius] [damage]

### Changes:
- Improved utf-8 text support (languages other than english and russian should work with menu/status/text now).
- Build mode now disables collision, makes the player invincible, and flight speed is set to 2x the walk speed.
- Small performance boost for tile rendering on dedicated gpu's.
- Added cubemap support for steps, thin walls, and custom rectangle modifiers.

### Fixes:
- Some sounds weren't being loaded properly (keys, explosions).
- Timescale pitch change only affected music.
- Scripted music would restart after the script ended.
- Map music would restart from the start after a 'music stop' command.
- Invisible entities could show as a white square.
- Memory corruption issue, which could cause a variety of inconsistent issues (light flickering, sound popping, crashing).
- Weapons with infinite ammo would show a '%' where the ammo is supposed to be.
- Input could become unresponsive while holding a scripted keybind.
- Results from a CHECKPOS fsm action weren't usable until the next 'game' frame (not state frame), and could have issues saving to local variables.
- Non-md3 models didn't work in build mode.
- Crash when 'skybox' command was used in a map script.
- Height offsets for the PROJECTILE fsm command didn't work.


## [2025-10-12_0241](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-10-12_0241.exe) : (1.11 alpha 54)

### Potentially breaking changes:
- Stereo sounds are spatialised now, so if you used 'SOUND' in an FSM to play a '2d' sound (one that can be heard anywhere on the level), you'll need to add some parameters to your SOUND actions to get the same behaviour. (set falloff and directionality to 0, more info below)

### Additions:
- Added 'tile check texture [x] [y] [z] [outVariable]', which sets 'outVariable' to the texture name of the tile at the specified coordinates, or 'None' if there's no tile placed there.
- The 'height' parameter of the 'PROJECTILE' fsm action can now be set to 'player' to target the player's height instead of an offset.
- If a weapon's "Max Ammo" is set below 0, it will now have infinite ammo.
- Added "MOVE [x/side] [y/vertical] [z/front]" fsm action, allowing you to move the player/entity from an fsm. Coordinates are local to the entity, like the PARTICLES/CUSTOMPARTICLE/SPAWN actions. There's probably some collision bugs with this, I've only done some basic testing. 
- Added optional parameters to 'SOUND' fsm action: SOUND [soundID] [Loop 0/1, default: 0] [minRadius, default: 256] [falloff, default: 0.5] [directionality, default: 0.9]. If loop is 1, the sound will loop. If the player is within 'minRadius', the sound will play at full volume. falloff is how quickly the sound will fade when the player moves away from the sound. Directionality is how much the audio left/right volume is affected by the direction the player is facin; 0 = audio stays the same no matter which direction you're facing, 1 = audio is completely muted in the ear facing away from the sound.
- Added 'STOPSOUND' fsm action: STOPSOUND [soundID], to stop a sound which was started from the fsm.
- MP3 support for music files.

### Changes:
- Audio system upgrade (unlimited sounds playing at once, spatialisation of stereo sounds, various other improvements)
- Added playing sounds to savedata (sounds continue from when they were saved)

### Fixes:
- 'status' command wouldn't work if the message didn't change.
- Hud masks weren't scaled properly at resolutions other than 1280x720.
- Opening the pause menu while in a script would cause both the map music and the menu music to play at the same time.
- Entities could replay their death animation after loading a save.
- Collision was broken with tiles at y=0
- Player would get sent to the void if gravity was set to 0.
- Player could go through walls if gravity was negative.
- Side-sliding doors didn't move in a direction that was consistent with their texture UV's.
- Models could sometimes still be culled when 'disable culling' was checked.
- Sounds would continue playing while the game was paused.
- Weapon stats could change after loading a save.
- Save slot asterisks weren't updated until the game was re-launched.
- Editor would crash if you clicked 'test game' while a test build was already running.


## [2025-09-29_1943](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-09-29_1943.exe) : (1.11 alpha 53)
### Additions:
- A game config option to limit the loop script update frequency. 0 = unlimited/same as fps, 20 = run up to 20 times per second. Loop script speed is still also capped by the fps, this just allows you to set an additional lower cap.

### Fixes:
- Enemy barrier blocks did nothing.
- Projectile collisions would break at very high framerates (first world problems amirite).
- Slowdown and startup.log spam when INCREMENT or DECREMENT fsm action was used without a number. (you all know startup.log tells you about script/fsm errors, right?)


## [2025-09-27_1556](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-09-27_1556.exe) : (1.11 alpha 52)
### Fixes:
- Many collision issues.  
- Potential crash/hang while loading a game (could cause Game.exe to stay running in the background, and could also crash the editor).
- Various shader-related rendering issues.
- The MODELTEXTURE command wasn't applying normals/emissives correctly.
- Loading screen images weren't properly scaled to screen resolution/aspect ratio.
- Changing aspect ratio without restarting the game would cause the world to seem stretched/squished.
- Entities could disappear when they or the player was near a closed door.


## [2025-09-25_1802](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-09-25_1802.exe) : (1.11 alpha 51)
### Hotfix for alpha 50
- Fixes a crash on maps with thousands of tiles/entities.

## [2025-09-25_0108](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-09-25_0108.exe) : (1.11 alpha 50)
### Potentially breaking change:
- Local variables (variables that aren't map/global/db) are now reset properly when changing maps or starting a new game.

### Additions:
- Added steam achievement/stat support with some new script commands:
  -  steam achievement unlock [achievement_api_name] //unlocks an achievement. "achievement_api_name" must be the same as it is in your steam developer dashboard.
  - steam achievement check [achievement_api_name] [output variable name] //sets specified variable to 0/1 to indicate if the achievement is unlocked.
  - steam achievement lock [achievement_api_name] //re-locks an achievement (useful for testing).
  - steam stat check [stat_api_name] [output variable name] //sets specified variable to the current stat value.
  - steam stat set [stat_api_name] [value] //sets specified stat to value.
  - steam stat increment [stat_api_name] [value] //adds 'value' to the specified stat.

For testing, you'll need to put a steam_appid.txt file in your .exe folder, but you don't need to include this file in the builds you submit to steam.  
If you aren't using steam, it's 100% safe to delete steam_api.dll from your game's folder.  
	
- Added 'alphablendmode' config.ini option. 0 = same as alpha 49, 1 = slower/multi-pass blending, 2 = no blending. Try 1 or 2 if you have any issues with entities disappearing when you look through transparent tiles (eg when looking through a chain-link fence).
- Status text left/center alignment can now be changed from the hud configurator, rather than requiring a hud.dat modification.
- Reduced default projectile collision radius and added an option in the weapon editor to change it (0 = no collision).
- Added an 'fps' option for animated textures, allowing you to adjust the speed of each animation individually.
- Added optional 'stretch' parameter to foreground/background in hud.dat (foreground [x] [y] [secondsPerFrame] [stretch: 0/1]) (background [x] [y] [stretch: 0/1]), allowing images to automatically stretch to fill the entire screen.
- Added a 'unified pickup size' game config option, allowing all pickups to have the same size, regardless of resolution. (0 = off).
- Added menu.script checkbox support for "texcompression" and "occlusiontest".

### Changes:
- "player camspeed" command and "CAMSPEED" action now also affect keyboard turning speed when 'player turn 1' is enabled.
- Tilting is now disabled when 'player turn 1' is enabled.
- Vsync is now always enabled while in the menu, preventing excess gpu usage while a game is paused.
- Made bullet spark particle directions more accurate.
- Lots of performance optimisations (very game and system dependent, but I've seen some games perform roughly 2x better than alpha 49).

### Fixes:
- Local variables weren't being saved/loaded properly.
- Multi-texture models weren't loading the per-material textures.
- Various collision bugs.
- Variable names couldn't be longer than 32 characters.
- "Test Game/Map" button would break if a game took more than a few seconds to load.
- Any script lines with the word "None" would be skipped.
- Some map scripts could be executed twice, leading to issues like entity duplication if the script spawned entities.
- Explosions and projectiles would show a white square when trying to render a missing / incorrectly-named animation frame.
- Crash when an invalid image was displayed in vn mode while 'textureinterpolation' was enabled.
- Using CAMSPEED in fsm with just one parameter was causing the y-speed to be set to 0, rather than using the same speed for both x and y.
- Shader uniforms weren't reset after starting a new game.
- Shader uniforms weren't saved/loaded.
- Weapon spread reduction while crouched didn't work with controllers.
- Status text set to 'center' alignment wasn't aligned correctly.
- Checkboxes and '<' menu elements didn't have a shadow.
- Weapons brought from previous levels could be lost if the player died after loading their save.
- Animated textures could have unintended duplicate frames if you imported a texture more than once (eg if you imported a texture for both walls and floors).
- 3D weapons could disappear during a muzzleflash if 'posteffects' was enabled.
- A few potential crashes.


## [2025-08-09_2301](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-08-09_2301.exe) : (1.11 alpha 49)
- Fixed a Game.exe hang when config.ini was missing

## [2025-08-09_1817](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-08-09_1817.exe) : (1.11 alpha 48)

### Fixes:
- Some weapons weren't being lit properly
- Potential crash during HOLSTER state
- Crash if there was an extra space at the end of a 'state' line
- Arrays or square brackets used within strings: "abc [] 123", would cause anything after the brackets to be skipped: "abc []"
- Made the editor less likely to hang if Game.exe hangs or crashes
- Made it harder for enemies to walk through walls


## [2025-08-07_2145](https://github.com/CG8516/DumpingGround/raw/main/EFPSE_DEVBUILDS/EasyFPSEditor_CE_DEV_2025-08-07_2145.exe) : (1.11 alpha 47)

### BREAKING CHANGE:
- "player check rotation" no longer returns a value offset by 90. Any scripts which used this will need to be adjusted.

### Potentially breaking changes:
- Active/scripted decorations can now be accessed from above/below
- Enemies with a radius of 0 will no longer be hit by projectiles or collide with the player

### General changes:
- Changed some terminology in the editor to be more descriptive (eg changed "Use Active Decorations On Button Press Only" to "Require button press to collect pickups")
- Spark and blood particles can no longer affect particles created with the PARTICLES/CUSTOMPARTICLE commands.
- Tweaked default stats of new enemies/weapons to make them more instantly usable. (projectile speed, reload speed, fire rate, mag size, recoil recovery)

### New features:
- Arrays can now be used in scripts and fsm's. "x = $map.var[$a]" "whatever[-10]["wtf"][$hi] += 3". Infinite dimensions are supported and there are no sizes.
- Advanced math functions can now be used with 'setvar' in fsm (eg: SETVAR x MIN(3,7))
- Added menu sounds (System resources importer allows unique sounds for hover, click, and when you hit the upper/lower limit of a range)
- Projectile height can now be changed in the enemy editor (0 = at feet, 1 = at head, 0.5 = middle)
- Decoration script interaction mode can now be changed to behave more like triggers (ideal for creating custom pickups without needing fsm + loop scripts, or as movable triggers).
- Added the 'colliders' cheat to show the colliders for triggers, entities, and invisible/hazard/enemy-barrier tiles.
- Added 'game save quick' and 'game load quick' to manually overwrite/load the player's quicksaves (that's rude, bro)
- Added 'player weapon draw [slot]' command, to force the player to draw a specific weapon if they aren't already holding it.
- Added 'quit' script command to instantly close the game
- Added an alternate form of 'player camspeed' and CAMSPEED. Original command still works the same, but now you can also do "player camspeed [speedX] [speedY]" to have different speeds for each axis
- Added three new menu options for allowing script keybinds to be changed, and for modifying db.variables: 
  - minput [posX] [posY] [scriptName.script] [pageNumber]
  - mrange [posX] [posY] [db.varName] [min] [max] [step] [defaultValue] [pageNumber]  ('step' is how much to subtract/add when clicking left/right)
  - mcheckbox [posX] [posY] [db.varName] [defaultValue (0/1)] [pageNumber]
- Added hud configurator option to only show 'spare' ammo, rather than a total that also includes the bullets in the mag. Enabled by default for new projects.

### Experimental features:
- Texture compression. Automatically compresses textures which are larger than 64x64, and have a width/height that are both a multiple of 4 (eg 128\*128, 256\*256, 1280\*720). Can reduce VRAM, but may introduce visual artifacts.
- Chunk occlusion culling. Can help performance, but could potentially reduce performance in some scenarios (more testing needed to verify).  

Both are disabled by default, but can be enabled in config.ini. You'll need to click 'apply' in the in-game settings menu if they aren't already in config.ini.


### Performance changes:
- Better performance for tile rendering and static 3d models (most noticable when using geometry subdivision or with high-poly static 3d models)
- Worse performance for collision code (required to fix some issues).
- Various minor script/fsm performance improvements.
- Greatly reduced performance impact of holding a key-bound script that ends with 'map quickreturn' (eg sprint/swim scripts)

### Fixes:
- Enemies could sometimes evolve the super-human ability to see through walls. 
- Player could clip through the floor when falling from a very tall height.
- Player could clip through ceilings. More testing needed to confirm if it's completely fixed, but I haven't been able to break it yet with these changes. 
- Player was unable to travel through floors while noclip + build was enabled.
- 3D model collider height would change after a save+load.
- Held weapon wouldn't enter custom 'holster' state when picking up a new weapon.
- Removed another method for activating the secret xray feature (triggered when using 'settings set scale' in a loop script).
- INCREMENT/DECREMENT fsm actions would add/subtract 1 if '0' was specified or if the specified variable was set to 0.
- Another potential crash when loading a save, related to hud images.
- Editor instability after duplicating custom modifiers.
- Doors weren't being lit properly.
- Decals weren't being lit properly.
- A potential crash while loading map scripts.
- Crash when 'image' fsm line was used with only one number.
- Decoration/Enemy sprites were low-resolution in their editors, and the scale preview image would be tiny if idle0 wasn't imported in the same editor session.
- Many potential crashes when the editor tried to save or load a number value.
- Some potential editor crashes when trying to replace an asset file with itself (eg replacing armour1 sprite with the existing armour1.png in the project folder).
- Projectile death animations only showed the first two frames.
- Camera rotation wasn't saved properly.
- Potential freeze/crash if the first frame of a state had a time of 0.
- Hud images would persist when starting a new game or when loading a save where they weren't active.
- Ammo would be kept when the player died, allowing ammo to be farmed infinitely.
- Music started from a loop script would stop if another script was executed, even if the other script ended with map return 1/2.
- Holding a key that was bound to a script which ended in map quickreturn while trying to open a door, toggle the map, or toggle the flashlight would cause those actions to be spammed many times per second.
- Removed Malevich's art piece from the top-left corner of the map (uninitialised decals).
- Viewbob speed could change after a save/load.
- Transparent decals could cause rendering issues with the geometry behind them.
- 'player rotation' command was rounding x/y values before applying them
- Fixed 'critical script error' when indenting if/else statements
- Fixed crash when db.txt existed but was empty
- Fixed flicker at end of weapon HOLSTER state


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
