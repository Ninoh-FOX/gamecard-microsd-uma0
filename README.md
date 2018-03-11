# PS Vita gamecard to microSD adapter

## Software

`driver` contains a kernel module. Add it to taihen's `config.txt` KERNEL section. You can download a precompiled `.skprx` from the [Releases](https://github.com/Ninoh-FOX/gamecard-microsd-uma0/releases) section.

Your microSD card must have no partition table. exFAT filesystem should be written directly to the device. On Linux, do:

```
mkfs.exfat /dev/sdx # (without a number)
```

On Windows, this works: https://redd.it/6o4gqh / https://redd.it/6o62vx

On Mac this should work (Tested on OSX 10.12):

```
sudo newfs_exfat -R /dev/diskn  (where n is the number of the mounted sd card)
```

After that, the card still works on both Linux and Windows, however other devices might have some problems.

### Compiling the driver

To compile:

```
cd driver
mkdir build && cd build
cmake ..
make
```

## Hardware

`board` contains Autodesk EAGLE schematics and board files. **Note: last revision still untested.**

The pcb has to be 1mm thick. This means I only tested 1mm thick PCBs and found them to work fine. I don't know if other thicknesses work.

Note how the pcb has a hole in place of microsd socket. You need to flip the socket and mount it into the hole .

![](https://i.imgur.com/5X5qVBu.jpg)

The socket should look like that. You can buy these from aliexpress for about $0.1-0.2/piece. Check out [issue 2](https://github.com/xyzz/gamecard-microsd/issues/2) for a buying guide.

There's no case for the adapter. Make sure to cover testpoints with some tape to prevent shorts. (v3.0 of the design has no test pads so you do not have to insulate anything). You also will have to use tweezers to remove adapter from PS Vita. Don't grab the adapter by the socket or you risk damaging it.

The adapter does not use Vita gamecard push-pull mechanism. If you feel a spring while inserting it, this means you are inserting it wrong.

If you accidentally short contacts, the Vita will power off. However, in my testing, this does not seem to cause any permanent damage.

Once you insert the adapter, you can replace microSD without taking the adapter out.

## Version history

### v1.0

mod for original code of @xyzz for mount sd2vita in uma0

## Alternative designs

You can find some alternative designs here:

* https://github.com/Gadorach/SD2VITA
* https://www.elotrolado.net/hilo_proyecto-hardmod-para-poner-un-lector-de-micro-sd-en-la-psvita_2229693 (Spanish)

(Send a pr if you want to be included here)

## License

Code inside the `driver` directory is licensed under GPLv3 or later.

Contents of the `board` directory are licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/).

## Special thanks to

* @motoharu-gosuto for their work on gamecard RE
* @TheOfficialFlow for providing original version of the usbmc plugin
* @xyzz for the original code https://github.com/xyzz/gamecard-microsd
