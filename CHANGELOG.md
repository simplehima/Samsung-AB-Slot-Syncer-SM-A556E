# Changelog for Samsung Galaxy A55 (SM-A556E) Copy-Partitions

This file documents the changes made to the original `update-binary` script to make it safe and functional for the Samsung Galaxy A55.

## 1. Fixed Critical Copy-Paste Bug
- **Issue**: The original script had a bug on line 98 (`if [[ -n "$part_active" && -n "$part_active" ]]`) where it checked the active partition twice instead of checking if the inactive partition existed. This could have caused it to write to the wrong location if a symlink was broken.
- **Fix**: Corrected the logic to verify both `$part_active` and `$part_inactive` exist before attempting the copy.

## 2. Added `vendor_boot` to the Copy List
- **Issue**: The original script included `vendor_boot_a` and `vendor_boot_b` in the `IGNORED` list, meaning it would skip them.
- **Fix**: Removed `vendor_boot_a` and `vendor_boot_b` from the `IGNORED` list as requested, ensuring they are properly cloned to the inactive slot.

## 3. Added Samsung-Specific Safety Checks
- **Issue**: The script was originally designed for Motorola. Samsung devices have critical partitions containing IMEI and calibration data (`efs`, `sec_efs`, `persist`, `steady`). Blindly copying all partitions could accidentally corrupt these if they ever existed as A/B slots.
- **Fix**: Added a `NEVER_TOUCH` list specifically for Samsung calibration partitions to guarantee they are safely ignored.

## 4. Improved Copy Speed and Reliability
- **Issue**: The `dd` command was running with default block sizes (very slow) and without forcing a sync to disk.
- **Fix**: Added `bs=1M` (1 Megabyte block size) for significantly faster copying, and `conv=fsync` to ensure all data is safely written to the physical storage before moving on.

## 5. Added Better Logging and Error Handling
- **Issue**: The old script failed silently if a copy operation failed, leaving you guessing if it actually worked.
- **Fix**: Added proper `echo` statements so you can see exactly which partitions are copied or skipped in TWRP. Added a summary at the end showing the total number of copied, skipped, and failed partitions.
