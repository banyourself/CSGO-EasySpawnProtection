# EasySpawnProtection (fork)

Spawn protection with a visible highlight for CS:GO. My fork of the **EasySpawnProtection**
plugin by Invex and Byte, with support for my One Versus All gamemode.

Upstream is 418 lines, this is 445. A small fork, but the change matters if you run OVA.

## Install

Drop the `addons` folder into your `csgo` folder:

```
addons/sourcemod/plugins/EasySpawnProtection.smx                   the compiled plugin
addons/sourcemod/scripting/EasySpawnProtection.sp                  source
addons/sourcemod/translations/EasySpawnProtection.phrases.txt      required
```

Convars land in `cfg/sourcemod/easyspawnprotection.cfg` on first run.

## What it does

Gives players a short window of invulnerability when they spawn, with a colored glow so
everyone can see who is still protected. Stops spawn camping on maps with tight spawns.

## What I changed

**It knows about One Versus All.** My hnsova gamemode hands the T role over on every stab, and
the new T has to be killable immediately, otherwise the handover turns into a scramble where
nobody can take the role back.

So while OVA is running, spawn protection does not apply.

The interesting part is *where* that check lives. It is done in one place rather than at the
two call sites, because guarding only the `player_spawn` path left the round-start loop still
granting protection, complete with its green highlight. One guard in the shared function, not
one guard per caller.

**The dependency is optional.** hidenseek exposes the OVA state, but the plugin still loads
normally on a server that does not have it, so this fork is safe to use anywhere.

## Credits

This one has a long lineage, and all of it is in the plugin's own `myinfo`:

* **Invex** and **Byte** ([github.com/mobeigi](https://github.com/mobeigi)), the version I
  forked, published on AlliedModders
* Based on earlier work by **cREANy0** and **Fredd**
* Me, for the OVA support

## License

GPL-3.0, see `LICENSE`.
