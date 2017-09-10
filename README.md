# makepup
Auto-build woof-CE Pup using single script with optional gui 

[size=18][b]Single script to build a Puppy automatically from woof-CE[/b][/size]

------------------------------------------------------------------------------------
[b]Translations for makepup gui (many thanks to the authors as listed)[/b]

nilsonmorales: Spanish NLS for makepup, fake .tar, delete: [url]http://www.murga-linux.com/puppy/viewtopic.php?p=967250#967250[/url]
-------------------------------------------------------------------------------------

makepup ver 0.0.8 uploaded (developed and tested on Puppy Slacko64 ver 6.3.2). This version of makepup includes a [b]simple gui frontend.[/b]

gui has gettext dialogs so [b]looking-for/inviting language translators[/b] and for testing.

[b]Download available at very foot of this post[/b]. Put a copy of the script in a Linux compatible filesystem (e.g. ext2, ext3, ext4 etc) in the directory you want to make the woof-CE build (around 4 to 5 GB free space is required - a Linux formatted usbstick would be fine, or harddrive with suitably-formatted Linux partition).

To run with gui, open terminal at the above directory (i.e. cd into it), and then:

Before running the script, remove the dummy .tar extension. Open a terminal where the script is, and make it executable with command:

[code]chmod +x makepup[/code]

followed by:

[code]./makepup -g[/code]
(or ./makepup --gui)

Once you are happy with the settings in the gui, simply press button "Build Your Pup!" and then answer the couple of terminal outputted questions with y followed by Enter (to confirm) and then go and have a coffee or something whilst you wait patiently for your Pup to be built to completion. Once the scripts have finished, you should find your built Puppy in woof-out_*/sandbox3/build (as frugal install files) or as a bootable iso in woof-out_*/woof-output-*.

For more details of changes and use, see:

[url]http://www.murga-linux.com/puppy/viewtopic.php?p=967123#967123[/url]

makepup can be used when you want to set up an unattended Pup build from woof-CE (woof-CE provides the distribution, makepup just automates the selection of choices at this stage).

Hopefully makepup is useful if you need to upgrade your distribution with new security fixes and so on since re-running makepup with the same selections will by default download any changes packaged (and can be only changed ones) and rebuild the iso. Updating critical packages can often be difficult or impossible whilst the Puppy is actually running so makepup provides one way currently round that issue.

Disclaimer: For above upgrade scheme to work it is very important that woof branch distro developers maintain their woof-CE builds carefully (and avoid using remastering techniques) since makepup can only (currently) download what is actually provided by woof-CE. makepup may also be useful for experimenting with woof-CE builds so you don't have to sit there continually select options throughout the build process each time you want to rebuild! Not everyone will find makepup useful.


For commandline usage examples see: [url=http://www.murga-linux.com/puppy/viewtopic.php?p=966761#966761][b]Some Simple one-liner Build Pup Recipes Using makepup[/b][/url]

With makepup any distribution type of Pup can be built that is supported by woof-CE (e.g. slackware, debian stretch, ubuntu xenial, devuan, trisquel).

Please refer to the following post for numeric values for the optional commandline arguments to makepup:

[url]http://www.murga-linux.com/puppy/viewtopic.php?p=965543#965543[/url]

Before using makepup, please read all of the following carefully. The usual disclaimers apply in terms of using this script at your own risk, though I can't imagine any major issues...

[b]NOTE WELL:[/b] At the current stage, the attached "makepup" script needs to be run on a relatively recent Puppy Linux system (not on any other type of Linux system). I developed and tested it on my PuppySlacko64 version 6.3.2 system. [b]No devx needs to be loaded[/b] though for some woof-ce-derived distros you may end up with smaller iso if devx is loaded - depends if any binaries need stripped (the program that can do binary strip is in devx).

The default config builds a woof-CE slacko-6.9.9.9.iso from woof-CE-testing branch (using default hugekernel huge-4.4.70-s32-700_PAE) and also by default requires no user input or interaction once the initial "Enter y to continue, any other key to quit" questions are answered. However, the script should basically build from any branch and for any distro once supplied with appropriate commandline options or makepup.conf configuration file.

The directory you run the script from should be on a Linux filesystem (e.g. ext2, ext3, or ext4) of sufficient space to build the new Puppy. The filesystem I used it on had 5GB free and that proved sufficient to complete the build. I don't at this stage know what minimum free space would be sufficient.

[b]Using:[/b]

No script installation is required. Simply download the "makepup.tar" script and copy it into the directory you wish to build the Puppy iso in. You do not need to download or clone woof-CE; the script takes care of all that for you.

Before running the script, remove the dummy .tar extension. Open a terminal where the script is, and make it executable with command:

[code]chmod +x makepup[/code]

Finally, in that same directory, in the terminal, build your woof-CE derived Puppy iso by simply entering the command:

[code]./makepup[/code]
-------------------------------

Notes:

Once the script has finished you will find the bootable iso in directory:

woof-out_<main_distro_name>/woof-output-<derived_distro_name>

Per standard woof-CE practice, the script also provides the files required for a frugal install separately in directory:

woof-out_<main_distro_name>/sandbox3/build

[b]NOTE WELL[/b] that the script does present the usual woof-CE build script dialogs, some of which may appear on the screen for a few seconds. But by default, you should not answer the questions manually because the makepup script will by default do that for you. The build takes a long time, since all woof-CE files are being downloaded from woof-CE github, so be patient!...

The script has only been briefly tested (since tests take a long time because of the amount of downloading involved in building the iso) and should be considered alpha at this stage.

If you want to try modifying the default script yourself, be warned that you should brush up on sed first (!) since it uses sed as an alternative to the likes of tcl expect for auto dialog answering (tcl expect would have required a big download but the makepup script could easily be modified to use that as an alternative).

Although, by default, no separate config files are required, makepup can utilise two separate config files, which need to be stored in the same directory as the makepup script itself: makepup.conf and makepup_extra.conf. The makepup_extra.conf file stores a list of extra packages you might want to install. [b]Default versions of both these text-based config files are now generated automatically if either of them does not already exist.[/b] Commandline arg options override the config file settings.

You can use option -p (--pause) to pause the script at a convenient time to modify the list of optional extra packages you might want to install (which you will add to makepup_extra.conf config file). To do that you would run the script to include the option like so:

[code]./makepup -p [any other optional args you like][/code]

The script will continue on to completion from that stage but you can exit it at that time, for examining the config files (makepup_extra.conf and DISTRO_PKGS_SPECS-distro-version) in a text editor, if you wish.

If you also want a devx squashfile to be created, use option --DEVX (or -D) on the commandline (note it is capital D).

Even at this early development stage there are some other options. You can view brief usage with command:

[code]./makepup -h[/code]

Apart from any urgent bug-fixes, it is likely to be a few days before I further modify this script in any way. It does not yet have any gui, though provision has been made for that. Other developments are also in progress but I wanted to release these early versions now so that bugs can be identified. 

wiak

Note:
ver 0.0.1 was downloaded 44 times
ver 0.0.2 was downloaded 110 times
ver 0.0.3 was downloaded 4 times
ver 0.0.4 was downloaded 44 times
ver 0.0.5 was downloaded 11 times
ver 0.0.6 was downloaded 34 times
