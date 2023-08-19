# Basic Setup for ZMK CRKBD CORNE
This is a zmk config that is suitable for you to test the board. It is built according to the default keymap of crkbd. Minor changes applied to the BLE keycode allows 5 column CRKBD users to connect BLE. 

The board is pre-flashed with the [left.uf2](https://drive.google.com/file/d/1_m4oQixc_IZxohSQl1CkoeF752q_duMT/view?usp=drive_link) and [right.uf2](https://drive.google.com/file/d/1KWRvnbwFU581RjSXRDAvElPMlIqgQ2dC/view?usp=drive_link). You may always use these to test the board. Additional image called [setting reset.uf2](https://drive.google.com/file/d/1r3C8MBEVbgs5SK3Hc2CyoOIaiAPLB_zp/view?usp=drive_link) for reset purpose, if only if you need it. 

For niceview version, get it from [here](https://drive.google.com/drive/u/0/folders/1zrGXbjNoFAU9e0BY-wZ6xVu2WyWjd4MS). You may refer to [Typeractive documentation](https://docs.typeractive.xyz/build-guides/corne-wireless/firmware) for more details.

## Key remap
1. Fork this repo to your github. Find the `fork` button on the top right of this page. 
2. Edit keymap in zmk-config-crkbd/config/corne.keymap, you may refer to <Example of keycodes for ZMK remap>(https://github.com/superxc3/zmk-config-crkbd/tree/master#example-of-keycodes-for-zmk-remap) in this page. Alternatively, you can use [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/)
3. Commit changes
4. Go to `Actions`, click `Build`, `Run workflow`.
5. Download the firmware from the `Actions` tab.

## First time bluetooth connection
![ble keyboard corne](https://user-images.githubusercontent.com/79617315/230918198-c6b5562f-e7e5-463d-b915-6c299875f332.jpg)

## Flashing u2f to split
1. Connect left and right splits to your pc (both connect together using type c cable)
2. Put right into bootloader mode (press the reset button), one window is popped out showing "nicenano" folder. Dont do anything yet, remember this folder as right split. 
3. Now press reset button on your left split, one window will be popped out as previous step.
4. Drag left and right u2f to respective folders.
5. Do not disconnect right split yet. 
6. Remove left split from type c cable. Proceed to `First time bluetooth connection` to connect your board to pc. If successfully connected, you shall able to type without cable now. 
8. If so, remove the right split from type c cable. Both should be working good now!

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
