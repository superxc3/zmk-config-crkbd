# Corne ZMK setup
This is suitable for Corne with the following features:
- 42 keys
- 36 keys (change to `&five_column_transform` in `corne.keymap`, delete outer columns in keymap)
- with or without niceview support

## Repo to go
1. Corne 42/36 keys with niceview, please fork [niceview](https://github.com/typeractivexyz/corne-wireless-view-zmk-config).
2. Corne 42/36 keys with oled, please fork this repo. 

</br>

## First time bluetooth connection
Please test before flashing to avoid complicating troubleshoot procedure.
![ble keyboard corne](https://user-images.githubusercontent.com/79617315/230918198-c6b5562f-e7e5-463d-b915-6c299875f332.jpg)

</br>

## Key remap
After you make sure that the board can be connected and every key is registering, you can proceed to remap the keys according to your needs.

### Steps
|![1fork](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/c1d1d583-d07d-4178-bc88-3ae4230202e6)|
|:--:|
|1. Please fork this repo for oled display or [niceview](https://github.com/typeractivexyz/corne-wireless-view-zmk-config).|

|![2 githubsignin](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/53f00200-1405-48dd-85db-231bd4cf28db)|
|:--:|
|2. Go to [keymap editor](https://nickcoutsos.github.io/keymap-editor/) to edit keymap.	Choose Github from the list. 3. Sign in your github account.|

|![3](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/69422119-67fd-4c99-99bf-5a27e0ba2fab)|
|:-|
| 4. Choose github repo you just forked in 1. (for advanced users with mousekey supports make sure you choose the correct branch)|
| 5. Start edit your keymap, after finish click SAVE. |
|![image](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/ad01038c-450a-40eb-826e-58a48b027377)|
| 6. For advanced users with mouse keys, please refer to [Keycode](https://github.com/urob/zmk-config/blob/upstream-mouse/config/mouse.dtsi). Head to `corne.keymap` and key in mouse keycode. You can refer to layer 7 in Keymap Editor for some samples. |
| 7. Click save or commit changes. If it does not auto run, Go to `Actions`, click `Build`, `Run workflow`|

|![4](https://github.com/superxc3/zmk-config-crkbd/assets/79617315/e56acc85-680d-41fc-a6ad-b10fc1767a37)|
|:--:|
|8. Click firmware and extract the two uf2 out. Drop to left and right respectively.|



</br>

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

</br>

## Common Issues and Troubleshooting
1. [Mac or Window OS connected but not responding](https://zmk.dev/docs/features/bluetooth#macos-connected-but-not-working), this is working for Bluetooth 5.2 Windows.
2. Master connected and can type, but not slave refer to [Split Keyboard Halves Unable to Pair](https://zmk.dev/docs/troubleshooting#split-keyboard-halves-unable-to-pair).
3. You may compile the reset.uf2 yourself or get it from [setting reset.uf2](https://drive.google.com/file/d/1r3C8MBEVbgs5SK3Hc2CyoOIaiAPLB_zp/view?usp=drive_link).
4. The board is pre-flashed with the [mouse-native.uf2](https://drive.google.com/drive/folders/1EStNUWT_zY0m-xmcMmOKRE_ifORbUOOl). You may always use these to test the board.
5. No key is registering: have you toggled the power button? (if you have one)

</br>

## Light indicator from Supermini MCU
1. Blue light: you are connected to usb c and the board is charging
2. Slight blue light blinking: you are connected to usb c but not connected to battery. Toggle power button to allow charging.
3. Blink red once: when you toggle the power button on
4. Flashing red: no firmware flashed to the mcu yet

## Light indicator from Nicenano v2 MCU
1. Blue light: you are connected to usb c and the board is charging
2. Blue blinking: bootloader mode, no firmware is loaded
   
</br>

## Advanced user
- with mousekey enabled, quick link to [mouse-native-repo](https://github.com/superxc3/corne-wireless-view-zmk-config/blob/main-with-native-mouse/README.md).
- kindly note that some keycodes are different from zmk mouse repo, please refer to [native-keycode](https://github.com/urob/zmk-config/blob/upstream-mouse/config/mouse.dtsi) for full list. Use these keycodes in `corne.keymap`, some codes are not available and synced with Keymap Editor, you are not encouraged to remap mouse key in Keymap Editor. You have to update the corne.keymap through coding but not Keymap Editor.
- Miryoku layout just head to [miryoku_zmk](https://github.com/manna-harbour/miryoku_zmk), follow their guides: [Quickstart](https://github.com/manna-harbour/miryoku_zmk/tree/master/docs/quickstart).

### Keycodes for mouse-native-repo
[Source](https://github.com/urob/zmk-config/blob/upstream-mouse/config/mouse.dtsi)

| Mouse Function   | Keycode in corne.keymap |
|------------------|-------------------------|
| Mouse Button 1   | `&mkp MB1`              |
| Mouse Button 2   | `&mkp MB2`              |
| Mouse Button 3   | `&mkp MB3`              |
| Move Cursor Up   | `&mmv MOVE_UP`          |
| Move Cursor Down | `&mmv MOVE_DOWN`        |
| Move Cursor Left | `&mmv MOVE_LEFT`        |
| Move Cursor Right| `&mmv MOVE_RIGHT`       |
| Mouse Scroll Up  | `&msc SCROLL_UP`        |
| Mouse Scroll Down| `&msc SCROLL_DOWN`      |
| Mouse Scroll Left| `&msc SCROLL_LEFT`      |
| Mouse Scroll Right| `&msc SCROLL_RIGHT`    |






