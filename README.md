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

||![4](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/e56acc85-680d-41fc-a6ad-b10fc1767a37)|
|:--:|
|6. After you click LATEST, it directs you to this webpage. Click firmware and extract the two uf2 out. Drop to left and right respectively.|

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
4. The board is pre-flashed with the [left.uf2](https://drive.google.com/file/d/1_m4oQixc_IZxohSQl1CkoeF752q_duMT/view?usp=drive_link) and [right.uf2](https://drive.google.com/file/d/1KWRvnbwFU581RjSXRDAvElPMlIqgQ2dC/view?usp=drive_link). You may always use these to test the board.
5. For niceview version, get it from [here](https://drive.google.com/drive/u/0/folders/1zrGXbjNoFAU9e0BY-wZ6xVu2WyWjd4MS) or [here](https://drive.google.com/drive/folders/1p5twDqSFcLPDTAh1r9uKbbJ-_LQ2O5IX?usp=drive_link). You may refer to [Typeractive documentation](https://docs.typeractive.xyz/build-guides/corne-wireless/firmware) for more details.
6. No key is registering: have you toggled the power button? (if you have one)

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
