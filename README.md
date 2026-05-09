# Copy-Partitions for Samsung Galaxy A55 (SM-A556E)

This is a flashable zip designed to synchronize critical firmware partitions between Slot A and Slot B on the Samsung Galaxy A55 5G.

## Why use this?
When flashing custom ROMs (like AOSP or GSIs), the device switches to the inactive slot. If that inactive slot contains outdated or missing firmware (bootloader, modem, etc.), the device may fail to boot or "hard-brick."

Samsung devices are particularly sensitive to bootloader version mismatches. This script ensures that your "Known Good" firmware from your active slot is cloned to your inactive slot before you switch ROMs.

## Features
- **Samsung A55 Optimized**: Specifically tailored for the SM-A556E partition map.
- **Safety First**: Automatically skips sensitive partitions like `efs`, `sec_efs`, and `steady` to protect your IMEI and device identity.
- **Data Protection**: Never touches `userdata`, `super`, or `metadata`.
- **Fast & Reliable**: Uses optimized block sizes (`bs=1M`) and `fsync` to ensure data integrity.

## What it copies
- **Bootloader**: `bootloader_a/b`, `sld`, `fld`, `uh`, etc.
- **Radio/Modem**: `radio_a/b`, `cp_debug`.
- **TrustZone**: `tzsw_a/b`, `tzar_a/b`.
- **Boot Components**: `vendor_boot_a/b`, `ldfw`, `up_param`.
- **Config**: `optics_a/b`, `prism_a/b`.

## How to use
1. Download the latest flashable ZIP from the [Releases](https://github.com/simplehima/Samsung-AB-Slot-Syncer-SM-A556E/releases) section.
2. Boot into custom recovery (TWRP/OrangeFox).
3. Flash the ZIP.
4. Verify the summary in the recovery log.

## Credits
Original concept from the Motorola copy-partitions script. 
Modified and audited for Samsung Galaxy A55 compatibility.
