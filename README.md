# Xiaomi.eu HyperOS Root & Google Pay/Play Integrity Fix

A comprehensive guide to rooting Xiaomi.eu HyperOS and fixing Play Integrity to enable Google Pay and other banking apps.

> **Tested on:** Redmi K60 (Mondrian)
>
> **Method:** This tutorial uses the `fastboot` command-line tool, eliminating the need for a custom recovery like TWRP (though you can use TWRP if you prefer).

## ⚠️ Disclaimer

> **DO THIS AT YOUR OWN RISK\!**
>
> Flashing custom files to your device can potentially lead to data loss or "bricking" your phone. The author of this guide and its contributors are not responsible for any damage that may occur. **Always back up your important data before proceeding.**

-----

## Part 1: Rooting Your Device

> **IMPORTANT:** This rooting process must be repeated every time you update your Xiaomi.eu ROM.

### Requirements

  - [**Platform Tools (ADB & Fastboot)**](https://developer.android.com/tools/releases/platform-tools?#downloads) downloaded and extracted to your computer.
  - The raw `boot.img` file for your specific ROM version.
  - A root management app of your choice (e.g., Magisk, APatch, Kitsune Mask).
  - A USB data transfer cable.

### Instructions

1.  **Extract `boot.img`**: Unzip your Xiaomi.eu ROM file (e.g., `xiaomi.eu_MULTI_XXX_OS1.X.X.X_XX.zip`). Navigate to the `images` folder and copy the `boot.img` file to your phone's internal storage.

2.  **Patch the Boot Image**:

      - Open your chosen root management app (Magisk, APatch, etc.).
      - Select the option to patch a file (e.g., in Magisk, tap `Install` -\> `Select and Patch a File`).
      - Navigate to and select the raw `boot.img` you transferred in Step 1.
      - The app will begin the patching process.

3.  **Transfer Patched File**:

      - Once patching is complete, a new file will be created in your phone's `/Download/` folder (e.g., `magisk_patched-XXXXX_XXXXX.img`).
      - Connect your phone to your computer and transfer this newly patched `.img` file to your `platform-tools` folder on the computer.

4.  **Enter Fastboot Mode**:

      - Power off your phone completely.
      - Press and hold the **Volume Down + Power** buttons simultaneously.
      - Keep holding the buttons. The phone may take a screenshot first, then the screen will turn off. Continue holding until a screen with the "FASTBOOT" text in orange appears.

5.  **Flash the Patched Boot Image**:

      - On your computer, open a Command Prompt (CMD) or Terminal inside your `platform-tools` folder.
      - Type the following commands. Replace `<patched_file.img>` with the actual name of the file you transferred in Step 3.

    <!-- end list -->

    ```bash
    # For Windows:
    fastboot flash boot_ab <patched_file.img>

    # For macOS/Linux:
    ./fastboot flash boot_ab <patched_file.img>

    # --- TROUBLESHOOTING ---
    # If the command above fails, try flashing to the init_boot partition instead:
    # fastboot flash init_boot_ab <patched_file.img>
    # ./fastboot flash init_boot_ab <patched_file.img>
    ```

6.  **Reboot**: Once the flash completes successfully, reboot your device with the following command:

    ```bash
    # For Windows:
    fastboot reboot

    # For macOS/Linux:
    ./fastboot reboot
    ```

7.  **Complete Installation**: After your phone reboots, open the root management app again. If prompted, follow the on-screen instructions to complete the installation (this may involve a "Direct Install" step and another reboot). Your device is now rooted\!

-----

## Part 2: Fixing Google Pay & Play Integrity

This section will help you pass Google's Play Integrity checks, allowing you to use Google Pay and other sensitive apps.

### Requirements

  - **PlayIntegrityFix-NEXT** (version 1.5 or newer recommended)
  - **ReZygisk** (Required for APatch users)
  - **TrickyStore**
  - **Tricky Addon**

### Instructions

1.  **Disable Xiaomi.eu Inject Module**: You **must** disable or uninstall the `eu.xiaomi.module.inject` Magisk module. This module conflicts with modern integrity fixes and will cause a bootloop if left active.

    > As explained by the Xiaomi.eu team, this module is no longer effective due to strengthened Play Integrity security. [Read more here](https://xiaomi.eu/community/threads/regarding-google-play-integrity-google-pay-wallet.75761/).

2.  **Install Required Modules**: Install all the modules listed in the requirements section via your root management app and **reboot your device**.

3.  **Configure PlayIntegrityFix-NEXT**:

      - Open the `PlayIntegrityFix-NEXT` app from your app drawer.
      - Press **"Fetch pif.json"** to download the latest integrity profile.
      - Tap **"Advanced"**.
      - **Turn OFF all toggles EXCEPT for "Use preview fingerprint"**.

4.  **Configure TrickyStore**:

      - Open the `TrickyStore` app.
      - Open the side menu (hamburger icon).
      - Tap **"Select All"**.
      - Tap **"Deselect Unnecessary"**.
      - Tap **"Set Security Patch"**.
      - Tap **"Get Security Patch Date"**.

5.  **Save and Reboot**: Save your settings in TrickyStore and **reboot your phone** one last time.

After rebooting, you should now pass all three levels of Play Integrity (check with an app like "Play Integrity API Checker") and be able to add your cards to Google Wallet/Pay successfully.

-----

## Disclaimer?
I am not the owner of Xiaomi.eu nor any modules and apps, I do not come up with these tutorial myself but gather information from many places and test them out!
