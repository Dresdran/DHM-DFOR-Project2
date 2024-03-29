# DHM-DFOR-Project2

**Overview**

Tomb of the Mask is a free-to-play indie arcade game by Playgendary and Happymagenta that can be found on the Google Play Store for Android and Apple App Store for iOS. With over 100 million downloads and 2 million reviews, there are plenty of reviews of this game on the Internet. Few, however, examine the technical side of this app through the use of digital forensics. As a graduate student studying digital forensics, I hope to give to the Internet, and my professor, an adequate review of Tomb of the Mask that factors in both the gameplay and technical aspects of this popular app.

**Gameplay**

The gameplay of Tomb of the Mask is for the most part simple, involving the player dashing about levels, avoiding spiked walls, roaming enemies, and the occasional floor of lava that will end your run if your reflexes aren’t up to the task. Collect dots and stars placed throughout the levels to gain rewards and coins which can be used to buy power-ups and character skins that can be used to make subsequent levels easier and increase the amount of coins you gain.

Traversing the maps is simple but can take some getting used to. You can swipe the screen to change which direction you want your character to go. You don’t need to move them yourself, as once your character changes directions they will move in that direction until they hit a wall. Some walls have clearly visible blue spikes, while others are designed to spawn spikes a second or two after you touch them. As you may might be able to guess, these walls are dangerous. Of the two, I found the latter to be the source of most of my deaths in the early levels.

There are two kinds of levels in Tomb of the Mask: stage levels and arcade levels. Stage levels are procedural generated maps that you unlock as you beat harder and harder levels. Arcade mode levels are randomly generated and endless, only stopping once you run out of lives (which are taken away when you hit spikes, enemies, and the rising lava floor). 

If you manage to get every star in a stage level and finish it you can get a free chest that gives you either a free power-up or coins, though there is a cooldown before you can get another free chest. Collecting every dot in a stage level will likewise give you coins which you can then spend on upgrades. Picking up coins during a level will give you those coins once you complete it, but unlike points or stars you don’t need to get every single coin to get them.

An energy mechanic exists to prevent you from playing the stage maps for too long in a given period of time, with deaths costing energy that is only replaced after some time has passed. As you can still play the arcade mode without energy, you can still binge Tomb of the Mask even if your energy runs out so while the mechanic itself is annoying, it is largely a non-issue.

Overall the gameplay was simple but enjoyable. A good time waster if you don’t already have one. The only thing that tarnished the experience in my eyes was the rather aggressive ad placement between levels and during the opening of loot chests. Difficult to skip and with seemingly no time limit, with a single misplaced tap of the screen these ads will quickly whisk you away to the Play store hoping that you will download whatever they are advertising while you are there. While I was playing, this was most often an ad for TikTok.

There were two ways to get around the aggressive ad placement of this application that I have found. The first is a one-dollar micro-transaction that will get rid of advertisements. The other is by putting your phone into airplay mode. As I am loath to reward companies for overly-aggressive businesses strategies, I have stuck with the latter method to get rid of my ad woes.

**Difficulties**

Tomb of the Mask, like many other apps, collects data on your phone. Officially, the app collects your device’s location data giving it an approximate knowledge of your location, financial information relating to the purchase history, a suite of info from crash logs and internal diagnostics pertaining to the app, and the IDs of the device and “others”. That last bit stuck out to me, as any time there is an open-ended statement like that it usually means that more is being collected than you might think. This app wouldn’t be the first free app that understates what data it collects in its quest to recoup development costs.

With this in mind, I set about rooting an old Android phone of mine, a Cubot Quest running Android 9, so that I could create a full image of my device using Magnet ACQUIRE that contained Tomb of the Mask’s application data. My goal was to see what permissions Tomb of the Mask had on the device and, if possible, what data was collected and sent to its developers. Unfortunately, I ran into some difficulties while attempting to root it.

Acquiring a developer’s privileges was simple enough, seven taps on the build number and I was a developer in the eyes of my Cubot. I then enabled USB Debugging and OEM unlocking so that I could gain access to the bootloader. The problems arose after that, however.

At first I tried to use popular rooting tools to quickly root my old phone. These included Framaroot, which seemed to be the most promising until I learned my device was not compatible with version 1.4.1 (the only version I was able to successfully run); Kingroot and its offshoot Kingoroot; and iRoot.

I then attempted to root my phone using Magisk. Using a handy guide from the XDA Developers site, “How to Install Magisk on your Android Phone”, I attempted to use a patched boot image to finally root my phone. The images *Must Update Android Driver* and *BootLoader Not Working* in this project were the results of two different attempts at using Magisk. Unfortunately, that is when I hit learned of a very difficult roadblock that had so far thwarted my attempts to root the device. 

While I was able to issue CMD commands to my phone (as seen in the image *Failed Magisk Root*), while I was able to transfer files to and from the Cubot, it would appear that a driver issue prevented me from issuing any fastboot command that did not involve putting my phone into fastboot mode. I searched for ways to get the driver’s to work or circumvent it through using different cables and even changing which computer the commands were being sent from, however my time was running out on this project and so I went with plan B.

**Technical**

As such this project of mine does not, much to my chagrin, involve digging through the electronic guts of phone to find the juicy data hidden away. Instead I will be using the digital equivalent of panning for gold, identifying interesting little bits of data that I was able to acquire from a quick image of my phone using Magnet ACQUIRE while the game was running in the background as well as one or two educated guesses based on what I observed.

When I first began sifting through the quick image using Autopsy, I was worried that my quick image would give me nothing on the app. This was because of a keyword list I created that contained tomb of the mask, tombofthemask, and tomb_of_the_mask. This search gave me a single result, package.txt, which simply told me that the app had been installed. 

The good news is that through a bit of rooting around in the data files I learned that the app used Tomb of the Mask’s developer, Playgendary, when referring to the app itself. When I searched for Playgendary as a regular expression through the search function, that is when I found my data. The file *Playgendary - Search Results* shows a small snippet of this result.

Browsing through the files, we can see that quite a few of these files are records of activity that correspond to me running and playing Tomb of the Mask. SurfaceFlinger.txt and vibrator.txt entries correspond to when I swiped the screen to move my character and felt slight vibrations from hitting walls. That there was an audio.txt entry is a bit odd as no music played when I played on the app, but as it seems to have been a one-time occurrence that was abandoned it may correspond to an ad I got before I turned on airplane mode. These three files can be seen in *Playgendary - Surface Flinger*, *Playgendary - Vibration Permission*, and *Playgendary - Audio*.

Similarly, files such as media.metrics.txt and gfxinfo.txt (*Playgendary - Media Metrics* and *Playgendary - GFX Info* respecitvely as well as *Playgendary - Proc Stats* and *Playgendary - Task Stats*) give us information on the encoding/decoding processes of the app and its frame rate information, among other things. If this were a review of its specifications and how well the app runs these files would be useful, however I am more interested in the security flaws, if any, of this app as that is what I am most familiar with.

Most of the files from this search are fairly easy to understand, however I will admit that the global-metadata.dat files were incomprehensible to me and gave me a headache whenever I tried to understand the lines upon lines of uninterrupted text. If you want to see a small snippet of this, go to *Playgendary - Global Metadata*.

Based on how the deluge of ads stopped the moment I turned on airplane mode and how the ads returned when I turned said mode off, it is safe to say that the ads are not part of the app itself but are sent across the Internet to whatever device Tomb of the Mask is on from some server no doubt owned by either the publisher or developer of the app. 

The file wifi.txt contains entries that may correspond to these ads, as it is linked to the app itself, but as it stands I do not have enough knowledge to say whether the entries are linked to the ads or to a different function of the app. See *Playgendary - Wifi*.

There also exists a few entries in dbinfo.txt, which seems to correspond to several different attempts to pull in ads between levels. With how many ads I got in the brief 10 minutes I played before I learned the airplane mode tricks, the number of entries is unsurprising. See *Playgendary - DB Info*.

From a security perspective this ability of the app to request ads is a red flag, as all it takes is for one enterprising bad actor to find a way to hijack the server or message being sent to inject malicious software onto your phone. 

When combined with the ability to write data to the phone as seen in the appops.txt (which by itself is harmless as the app needs to write data to the phone so it can store your progress), this could potentially allow an attacker to infect the application and use it to write whatever data it wants to your phone. See *Playgendary - Appops*.

This is unfortunately the extent of what I was able to find that did not involve battery statistics, the window activities, and other mundane statistics like those found in vibrator.txt and company. 

**Conclusion**

If there is anything to take away from this review, its that if you are interested in this game you should only play it on airplane mode. That way the app cannot talk to servers and potentially bring in infected ads to your device. It is both safer and more enjoyable, a rare combination in this world of software.
