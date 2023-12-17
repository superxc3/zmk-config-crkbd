# Basic Setup for ZMK CRKBD CORNE
This is a zmk config that is suitable for you to test the board. It is built according to the default keymap of crkbd. Minor changes applied to the BLE keycode allows 5 column CRKBD users to connect BLE. 

## First time bluetooth connection
Please test before flashing to avoid complicating troubleshoot procedure.
![ble keyboard corne](https://user-images.githubusercontent.com/79617315/230918198-c6b5562f-e7e5-463d-b915-6c299875f332.jpg)


## Key remap
After you make sure that the board can be connected and every key is registering, you can proceed to remap the keys according to your needs.

|![1fork](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/c1d1d583-d07d-4178-bc88-3ae4230202e6)|
|:--:|
|1. Please fork this github [niceview github](https://github.com/typeractivexyz/corne-wireless-view-zmk-config). Applicable for 5column, board with/without niceview.|

|![2 githubsignin](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/53f00200-1405-48dd-85db-231bd4cf28db)|
|:--:|
|2. Go to [keymap editor](https://nickcoutsos.github.io/keymap-editor/) to edit keymap.	Choose Github from the list. 3. Sign in your github account.|

|![3](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/69422119-67fd-4c99-99bf-5a27e0ba2fab)|
|:--:|
| 4. Choose github repo you just forked in 1. 5. Start edit your keymap, after finish click SAVE. Wait until it finished sync, click LATEST and download the firmware. If it does not auto run, Go to `Actions`, click `Build`, `Run workflow`.|

|![4](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/e56acc85-680d-41fc-a6ad-b10fc1767a37)|
|:--:|
|6. After you click LATEST, it directs you to this webpage. Click firmware and extract the two uf2 out. Drop to left and right respectively.|

## Key remap for mouse repo using keymap editor 
Supports provided by nickcoutsos. Please follow step 1-4 above. We are using the popular choice https://github.com/urob/zmk/tree/mouse-3.2 mouse emulation branch that maintained by zmk users. 

a. Create a new branch in Keymap Editor. Click the three dots beside Latest> Create new branch > Name your branch, eg. mouse

b. Go to the top right setting icon. Tick Mouse keys/button/scroll

c. Start mapping your keymaps in Keymap Editor > save

d. Edit your `config/west.yml`. Kindly copy the following and paste. It will not worked if you accidentally add an extra space before `-`. 
```
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: urob
      url-base: https://github.com/urob
  projects:
    - name: zmk
      remote: urob
      revision: mouse-3.2
      import: app/west.yml
  self:
    path: config
```

e. Add `#include <dt-bindings/zmk/mouse.h>` to `config/keymap`.

f. Go to Action and wait for the firmware to be compiled.


## Flashing uf2 to split
You may refer to the [demo](https://drive.google.com/file/d/1_iiBsk6CXnIYhRzzQHDtAJCxdc7E1w-u/view?usp=sharing) for flashing procedure. Details as follow:
1. Connect left and right splits to your pc (both connect together using type c cable). 
2. Put right into bootloader mode (press the reset button), one window is popped out showing "nicenano" folder. Dont do anything yet, remember this folder as right split. 
3. Now press reset button on your left split, one window will be popped out as previous step.
4. Drag left and right uf2 to respective folders.
5. Do not disconnect right split yet. 
6. Remove left split from type c cable. Proceed to `First time bluetooth connection` to connect your board to pc. If successfully connected, you shall able to type without cable now. 
8. If so, remove the right split from type c cable. Both should be working good now!
9. If you dont have extra usb c cable...You can do left first, then quickly move to right so the right can sync with left.


## Common Issues and Troubleshooting
1. [Mac or Window OS connected but not responding](https://zmk.dev/docs/features/bluetooth#macos-connected-but-not-working), this is working for Bluetooth 5.2 Windows.
2. Master connected and can type, but not slave refer to [Split Keyboard Halves Unable to Pair](https://zmk.dev/docs/troubleshooting#split-keyboard-halves-unable-to-pair).
3. You may compile the reset.uf2 yourself or get it from [setting reset.uf2](https://drive.google.com/file/d/1r3C8MBEVbgs5SK3Hc2CyoOIaiAPLB_zp/view?usp=drive_link).
4. The board is pre-flashed with the [these uf2](https://drive.google.com/drive/folders/1p5twDqSFcLPDTAh1r9uKbbJ-_LQ2O5IX?usp=drive_link). You may always use these to test the board.
5. No key is registering: have you toggled the power button? (if you have one)

## Light indicator from Supermini MCU
1. Blue light: you are connected to usb c and the board is charging
2. Slight blue light blinking: you are connected to usb c but not connected to battery. Toggle power button to allow charging.
3. Blink red once: when you toggle the power button on
4. Flashing red: no firmware flashed to the mcu yet

## Light indicator from Nicenano v2 MCU
1. Blue light: you are connected to usb c and the board is charging
2. Blue blinking: bootloader mode, no firmware is loaded
   
## Power button toggle
1. For mx, slide to left = off. Slide to right = on. Applicable on both sides.

## Switch installation
1. For mx with pom switch plate, no foam. You will face difficulty in inserting the switch directly to the board. Dissemble the top five screw on each side, push the switch one by one. Fill up the switch plate, then only assemble it back to the board. This is because pom is flex and soft, hence the difficulty to install the switch directly.
2. For mx with carbon fibre switch plate. If you face difficulty in inserting the switch directly, do the same as step 1.
3. For lp choc, just push the switch directly. You may face difficulty in removing the switch for certain model. If the switch doesnt pull up when you pull the keycaps, you have to dissemble the bottom plate and push the choc switch from bottom of pcb. This is because lp choc switch doesnt have dedicated switch puller. 

# Future planning
To change the keymap according to Klein's or Bastard C Nano for better inspiration.


# Below for manual zmk setup who not using keymap editor.

## Example of keycodes for ZMK remap
The default firmware does not support mousekeys. However, the encoders on both sides are working as written and prepared by author snstein. For additional features, please refer to the ZMK website. If you have any questions, you can ask in their Discord server. The following are some basic and essential keycodes:


### Single tap
Always remember their prefix `&kp` or `&trans` or `to` etc. Refer to [Keyboard Codes of ZMK](https://zmk.dev/docs/codes).

### Hold
The most basic `&lt 5 Z` means hold to access layer 5, tap as z; while `&mt LSHIFT TAB` means hold as modifier Left Shift, tap as Tab.


### Macro
You can copy the following and edit according to your needs. Just need to note that for Left Shift+X it is `&macro_press &kp LSHFT &macro_tap &kp X &macro_release &kp LSHFT`; while single key tap for example c8 is `&macro_tap &kp C &kp N8`. In key remap, use `&gmail` to register macro.

```
/ {
    macros {
		gmail: gmail {
        compatible = "zmk,behavior-macro";
        label = "ZM_gmail";
        #binding-cells = <0>;
        wait-ms = <10>;
        tap-ms = <10>;
        bindings = <&macro_tap &kp X &kp C &kp H &kp C &kp L &kp O &kp W &kp AT_SIGN &kp G &kp M &kp A &kp I &kp L &kp PERIOD &kp C &kp O &kp M>;
        };

    };
};
```



:star: If you like our service or products, please tell your friends and family about us so we can grow and offer more options in the future. We strive to provide comprehensive user manuals to save you time exploring our products. We welcome any suggestions you have to help us improve our boards.
