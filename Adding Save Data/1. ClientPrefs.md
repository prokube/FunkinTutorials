# Adding Save Data
So basically you wanna add in some sort of star system or whatever? Yeah sure follow this

## ClientPrefs Variable

In `ClientPrefs.hx`, add a `public static` variable named whatever you want. (Using `starsUnlocked`, a bool Array, as an example.)

```haxe
class ClientPrefs {
	public static var downScroll:Bool = false;
	public static var middleScroll:Bool = false;
	public static var showFPS:Bool = true;
	public static var flashing:Bool = true;
...
	public static var starsUnlocked:Array<Bool> = [false, false, false]; // Three stars, 1 for completing main week and 2 for completing secret songs.
...
}
```

Then, attach it to a save data pointer. (Line 93 in Psych-Engine EK)
```haxe
public static function saveSettings() {
	FlxG.save.data.downScroll = downScroll;
	FlxG.save.data.middleScroll = middleScroll;
	FlxG.save.data.showFPS = showFPS;
...
	FlxG.save.data.starsUnlocked = starsUnlocked;
    FlxG.save.flush();
...
}
```

Be sure to load it back in when the game loads save data:
```haxe
public static function loadPrefs() {
	if(FlxG.save.data.downScroll != null) {
		downScroll = FlxG.save.data.downScroll;
	}
	if(FlxG.save.data.middleScroll != null) {
		middleScroll = FlxG.save.data.middleScroll;
	}
	if(FlxG.save.data.showFPS != null) {
		showFPS = FlxG.save.data.showFPS;
		if(Main.fpsVar != null) {
			Main.fpsVar.visible = showFPS;
		}
	}
...
    if(FlxG.save.data.starsUnlocked != null) {
		starsUnlocked = FlxG.save.data.starsUnlocked;
	}
```

From here, just reference `ClientPrefs.starsUnlocked` (or whatever your variable is) and make it do something based off that.
