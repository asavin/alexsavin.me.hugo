+++ 
draft = false 
date = 2023-11-03T05:37:10Z
title = "Acorn Archimedes and floppy discs"
description = "How to write Acorn Archimedes compatible disc images to floppies today"
slug = "2023-11-03-acorn-floppy-discs" 
tags = ['retro', 'acorn']
categories = []
externalLink = ""
series = []
+++

![](https://alexsavin.me/photos/2023-11-03-acorn/acorn_floppy.jpg)

I've been gradually restoring a 35 years old Acorn Archimedes computer. Gifted by a friend, who used it in their childhood and then fathfully kept it safe in the attic - it is quite a piece of retro computing.

The model I have - 440/I - features one of the original ARM CPUs, 4Mb of RAM, RISC OS, a hard drive and a floppy drive. It also has a built-in 8-channel sound and a speaker. I've been also lucky enough to get the original monitor, keyboard and a mouse. All in all, full package, if slightly broken at the beginning. The computer would turn on, but would refuse to properly boot, weird sounds would come out of the base unit, and keyboard was mostly non-functional.

1980:s in the UK were the decade of home computing. Dominated by ZX Spectrums of various sizes, with an occasional Amstrad. At the same time Acorn was in every classroom, again - mostly represented by the BBC Micro model. Archimedes was a later upgrade, incredibly powerful, but also much more expensive. 

Although, compared to then Apple prices, it was still a bargain. The original Macintosh demanded $2495, while Archimedes started at around £900. To be fair, model 440/I was £1499, inching towards that Macintosh price, but still about half way there.

The reason I want to compare it to the Macintosh is they both feature OS with a graphical UI, driven by mouse. Both of them also rely on 3.5 inch floppy discs. In many respects you would get so much more for your buck with Archimedes, which came out only 3 years later - including a hard drive, an insane amount of RAM (Macintosh, and most Speccies would still only offer you 128kb of it), and a very powerful new ARM CPU - which ironically Apple would adopt 30 years later.

My restoration so far included removing old bloated batteries from the motherboard, cleaning the leakage, removing old fan filter - and hopefully replacing the fan too at some point. I had to practically re-build the keyboard too, cleaning everything in there, replacing membranes with springs, and soaking all the original keycaps. 

![](https://alexsavin.me/photos/2023-11-03-acorn/arch_kb_02.jpg)

Hard drive is completely unresponsive, but luckily it is also optional. RISC OS boots directly from ROM chips - and I've upgraded it to the latest version 3 by physically replacing those chips.

![](https://alexsavin.me/photos/2023-11-03-acorn/arch_roms.jpg)

This computer boots from cold to GUI in under 5 seconds. My VSCode today takes longer to start.

Now, the question of the month - how do you get apps on it?

There is support for expandable hardware modules - and I know there are modules supporting modern-ish memory cards that you could plug into the motherboard and they will pretend to be an IDE hard drive. I feel like this will be one of the things on my list to do.

For now though, we have a floppy drive.

Not any floppy drive, but a double-density floppy drive. This gives us twice as much, as Apple Macintosh's floppy - a whole 800kb on a single floppy. Another good news - Amigas used the exact same double density (DD) floppy discs.

Now some bad news - DD floppies are not the same as HD floppies - the ones that could fit a whopping 1.4Mb of data. HD floppies were the ones most of us ever saw, and also most of computers all the way up to 2010:s featured. You can buy "Amiga compatible" floppies on Ebay - and they will work perfectly fine on the Archimedes (assuming your floppy drive is alive). That's exactly what I did - and my Arch happily formatted the blue looking floppy and saved some of my drawings from RISC Paint app to it.

But how would I write some new apps to it?

Enter [OmniFlop](http://www.shlock.co.uk/Utils/OmniFlop/OmniFlop.htm). A miracle of an app that is able to read, write and format floppies in hundreds of exotic formats. Yes, it will require an actual floppy drive, and a Windows XP. Or a newer Windows, but apparently you'll need to do some extra tweaking.

![](https://alexsavin.me/photos/2023-11-03-acorn/omniflop_01.jpg)

As the luck would have it, I have a Windows XP laptop with a floppy drive, if you can believe it. OmniFlop was installed - and everything just worked.

Well, sort of.

To get things really working you will have to patch the floppy drive and floppy controller drivers. OmniFlop effectively takes over the whole floppy thing to be able to write in all the exotic formats. Replacing drivers in WinXP is done by going to Hardware Manager, finding that hardware that you want to update, and manually pointing it to a driver provided by OmniFlop. When was the last time you've installed drivers? Me neither.

![](https://alexsavin.me/photos/2023-11-03-acorn/omniflop_02.jpg)

This totally worked though, and after formatting floppies into `Acorn ADFS DD 800kb` format, I was able to write a disc image onto the floppy. There is one final trick you have to know about - most Archimedes images will be with ADF file extension. OmniFlop knows ADF, but somehow thinks this is only a "single side" image. It will happily accept it, but will only write half of it - first 400kb, and stop afterwards.

What you have to do is to rename your ADF image file to ADL. This is a double side format, and OmniFlop will happily write it to both sides of the floppy, all 800kb of it.

![](https://alexsavin.me/photos/2023-11-03-acorn/acorn_elite.jpg)

That's it - you can plug the floppy into the Archimedes, and launch whatever retro app or game you were trying to get to it. Happy days. Even though Arch was not the most popular gaming platform - the games that made it there are incredibly well done, and totally worth the trouble.
