# Touhou Danmakufu ph3.5 ~ Woo Edition

## About This Fork

This project is a fork of [Danmakufu-Woo-Edition](https://github.com/WishMakers0/Danmakufu-Woo-Edition), which itself is based on [Danmakufu-ph3](https://github.com/james7132/Danmakufu-ph3).

Danmakufu-Woo-Edition replaced Danmakufu-ph3's custom Mersenne Twister RNG implementation with `std::mt19937`.  
However, this change introduced differences in runtime behavior and broke compatibility with replays.

To restore full compatibility, this fork reverts the RNG implementation back to the original. Specifically:

- The files `source/GcLib/gstd/MersenneTwister.cpp/hpp` were completely rolled back.
- An API name in `source/TouhouDanmakufu/Common/StgStageController.cpp` was also reverted.

### Notice

This fork should be compatible with the executable built from [Danmakufu-ph3 source](https://github.com/james7132/Danmakufu-ph3), with file loading issues patched using the zlib solution from [Danmakufu-Woo-Edition](https://github.com/WishMakers0/Danmakufu-Woo-Edition).  
**However**, the behavior of this fork is still not fully consistent with [the official Danmakufu-ph3 release](https://touhougc.web.fc2.com/products/th_dnh_ph3.html), which, unfortunately, most Danmakufu fangames are based on. Specifically, desync caused by RNG can occur unpredictably, and even when no desync happens, the score may occasionally show minor discrepancies, which is likely due to floating error.
If you intend to create replays that work across both this fork and the official release, please do so at your own risk.  
You are welcome to build this fork yourself. It would be so great if your build achieves better compatibility.

### Build Tips

If you're using a Chinese or non-UTF-8 default locale system, you may run into encoding-related build errors.  
You can try running the following PowerShell command in the project directory to convert all `.cpp` and `.h` files to **UTF-8 with BOM**:

```powershell
Get-ChildItem -Recurse -Include *.cpp, *.h | ForEach-Object {
  $content = Get-Content $_.FullName -Raw
  [System.IO.File]::WriteAllText($_.FullName, $content, [System.Text.Encoding]::UTF8)
}
```

This should resolve any issues caused by illegal escape sequences or corrupted multibyte characters.

The original project includes a dependency on `afxres.h`, which is part of the **Microsoft Foundation Classes (MFC)**. You may install the MFC component via the Visual Studio Installer.

### == Below is the original README content ==

All hail our lord and savior Mima and our queen, Kogasa's Woo. This version of Danmakufu is made for the purposes of both optimization and fixing some issues with the original source that mkm dropped. (See James7132's repo for a link to the original download) <b>This version of Danmakufu is completely backwards compatible with ph3. If something doesn't work as expected, please let me know.</b> My Discord tag is WishMakers#0385 if you need to reach me.

## Changes in Master Branch
Here's a list of changes compared to original Danmakufu that may enable your computer to use it better.
 * Changes the way RNG is determined to be much more stable than previously (mt19937 compared to a Mersenne Twister from 1996, lmao)
 * Removes a lot of repeated function calls (in bullet movement only as of 6/24/2019)
 * Removes a LOT of unnecessary vertices calculated (but not used) when drawing curvy lasers (see Special Thanks)
 * Enables a lot of optimization flags that mkm for some reason disabled (basically everything under /O2)
 * Attempts to fix the window resolution issue (not quite 640x480) that occurs with the source when built, but not the original ph3 build.
 * Dat extraction now works properly, enables the use of games like Kaisendo's Hollow Song of Birds and other games that use dat archives.
 * Side bars in fullscreen are now black as opposed to the ubiquitous DNH Gray.

## Requirements
 * zlib
</br>Best and recommended way to obtain it is to use [vcpkg](https://github.com/Microsoft/vcpkg) C++ Library Manager.

## Known Issues
 * Wine 4.12.1 (confirmed on macOS at least) suffers some scaling problems with the window size, being 9 pixels too wide and 7 pixels too tall.  This causes some nasty scaling on in-game assets, possibly a result of old Windows size calls not being 100% compatible with Wine releases.

## Special Thanks
Natashi - for the code that made curvy lasers run a lot better than what I could do
</br>Trickysticks - for the woo art that graced the world
</br>UltimaOmega - for helping me with my sorry excuse for zlib code

## Contributions
This project is no longer in active development.  I keep this text here in some form in memory of Danmakufu Remastered and Ultima's contributions to the Danmakufu scene over the years, who no longer participates in the community and has formally erased their internet presence.
</br>~~Unlike the original source, this version is *technically* in active development (though my primary focus will be Danmakufu Remastered - check out Ultima's repo for that here) so pull requests are absolutely accepted provided they don't break the game. Though bear in mind that as this version of DNH still relies on mkm's original source code (most of which is either very unoptimized even with optimization flags or is very outdated in execution), there is only so far we can go in attempting to make it better.
</br>In addition, *this build will be focused on optimization and performance improvements only.* If you want to suggest brand new features, bug fixes, etc. please turn your attention to Danmakufu Remastered instead - this version is made to be completely backwards compatible, and as such new features can't simply be added.~~

## New Features Branch
The "newfeatures" branch and its releases exists for those who wish to have some minor functionality improvements that aren't completely 1:1 with original PH3, but would rather not wait until DNH:R is released to use them.  These changes may be mirrored in DNH:R's PH3 compatibility, but as of 8/9/2019 they are currently unimplemented.

## License
zlib library has its own license, please check zlib.h in the repo for that information.</br></br>
(quoted from James7132's repo of the original source, maintaining the same license.) </br>This code is licensed under the NYSL (Niru nari Yaku nari Suki ni shiro License'). Main translated points:

 * "No warranty" disclaimer is explicitly included.
 * Modified version of the software MUST be distributed under the responsibility of the distributer.
 * Official version is written in Japanese.
