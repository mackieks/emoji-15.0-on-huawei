## emoji-15.0-on-huawei
How to install the latest and greatest emojis (Emoji 15.0) on older Huawei devices (EMUI 11-ish)

# The state of emoji on Huawei devices in 2023
Pre-ban devices (Mate 20 Pro, P30 Pro) have the latest emoji even if they're running EMUI 11! How? Google serves new emoji to Gboard through the [EmojiCompat library](https://developer.android.com/develop/ui/views/text-and-emoji/emoji-compat) **via Google Mobile Services.** Yes, Google now gates access to the latest Unicode standard via their monopolistic mobile services platform.

Post-ban devices (P40+, Mate 30+) lack GMS. That means no EmojiCompat and no OTA emoji from Google. HarmonyOS 3.0 and EMUI 13.0 devices may be in a better state, but my Mate 40 Pro running EMUI 11 has been stuck with [Android 10 emoji](https://emojipedia.org/google/android-10.0/) since release. Exchanging messages with friends and family (most of whom have iPhones) gets annoying when all you can see is inscrutable tofus instead of ["Smiling Face with Tear"](https://emojipedia.org/smiling-face-with-tear/), ["Pink Heart"](https://emojipedia.org/pink-heart/), or ["Melting Face"](https://emojipedia.org/melting-face/).

# Existing workarounds
The usual workarounds for getting new emoji all suck. I don't want to install an "iOS 16.4 emoji pack" with ZFont3; I want [Noto Color emoji](https://fonts.google.com/noto/specimen/Noto+Color+Emoji) like every other decent Android device. Half the time with these glitchy packs the tofus in *received* messages will be fixed, but Gboard doesn't pick up the new emoji, so you can't *send* them. And for some reason no premade Unicode 14.0 or 15.0 Noto Color emoji packs are listed! 

# Trying to install NotoColorEmoji.ttf directly
Using [Font Manager for Huawei/Honor](https://play.google.com/store/apps/details?id=com.deishelon.emuifontmanager) to install [NotoColorEmoji.ttf](https://github.com/googlefonts/noto-emoji/tree/main/fonts) as a "Text Style" in the Themes app works... *sort of*. It seems the Font Manager app just copies the .ttf into /Huawei/Themes/ (and maybe does something else to tell the system it's a usable "Text Style"?) After applying it, all Unicode 15.0 emoji are visible and usable in Gboard! But there are some weird side effects— numerals 0 through 9 are replaced with emoji, and spaces (U+0020) are super wide. Basically unusable.


# The True Solution
#### (I've uploaded a pre-edited `.ttf` to this repo, so you can skip the entire PC section if you want. 🙂)

On PC:
1. Purchase and install [Dutch Type Library OTMaster 8.9](https://www.fontmaster.nl/otmaster.html) (font/glyph editor with FULL NATIVE CBDT/CBLC support, unlike FontLab!)
2. Download the latest [NotoColorEmoji.ttf](https://github.com/googlefonts/noto-emoji/tree/main/fonts)
3. Open NotoColorEmoji.ttf in OTMaster 8.9
4. Navigate to the 'cmap subtables'. These tables store the actual mappings from Unicode to glyphs. So deleting entries in these tables is like deleting a Unicode character from the font.
5. Expand the first subtable (*Unicode; Variation Sequences*) and select row 2 `0x000030`. This is the zero numeral glyph.
6. Click Edit > Cut to delete this glyph. Repeat for every glyph up to `0x000039` (numeral 9).
7. Expand the next subtable (*Microsoft; Unicode full repertoire*) and select row 2 `0x000020`. This is the space glyph.
8. Click Edit > Cut to delete the space glyph. Repeat this process for glyphs `0x000030` through `0x000039` to delete the numerals.
9. Press File > Save As and save the edited `.ttf` somewhere. Copy the `.ttf` to your phone.
 
On phone:
1. Install [Font Manager for Huawei/Honor](https://play.google.com/store/apps/details?id=com.deishelon.emuifontmanager) from Aurora Store or wherever.
2. Navigate to Tools > Create font (.ttf) and select the edited font from earlier
3. Force close the Huawei Themes app from the Settings menu to force a Text Styles refresh
4. Open Themes, go to Me > Text Styles and select the Noto Color Emoji text style in the 'Downloaded' section
5. Enjoy Emoji 15.0 emojis in Gboard! (Make sure Gboard is up to date)

