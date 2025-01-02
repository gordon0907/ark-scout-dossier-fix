# ARK: Survival Evolved - "Scout FM" Dossier Check-Off Fix

## Description
In the Explorer Notes tab of **ARK: Survival Evolved**, dossiers for tamed creatures are marked with a "✓" symbol upon completion. However, for "Scout FM" (Santiago), a bug prevents players from achieving this check-off, regardless of their efforts.  

Discussions about this issue can be found in various forums:  
- [Steam Community Discussion](https://steamcommunity.com/app/346110/discussions/0/1752402822289941748/)  
- [Reddit Thread](https://www.reddit.com/r/ARK/comments/rvgy48/scout_dossier_not_checked_off/)  
- [SurviveTheArk Forum Post](https://survivetheark.com/index.php?/forums/topic/475467-unable-to-tick-off-scout-and-mega-mek-dossiers/)

This guide provides a solution to achieve the check-off for "Scout FM" by editing your save file.

---

## Instructions

### Requirements
- A binary file editor (e.g., `010 Editor`).  

### Steps
1. Locate your save file:  
   The file `PlayerLocalData.arkprofile` can typically be found at:  
   `C:\Program Files (x86)\Steam\steamapps\common\ARK\ShooterGame\Saved\LocalProfiles`.  

2. Open the file using your binary file editor.

3. Search for the text string `TamedDinoTags`.

4. Look for the hexadecimal sequence `4E 61 6D 65 50 72 6F 70 65 72 74 79 00` immediately following the `TamedDinoTags` string.  
   - This sequence translates to the text `NameProperty\0`.

5. Modify the `int32` value immediately following the hex sequence:  
   - For example, if the original sequence is:  
     `4E 61 6D 65 50 72 6F 70 65 72 74 79 00 7C 00 00 00`  
     Increment it by 1 to:  
     `4E 61 6D 65 50 72 6F 70 65 72 74 79 00 7D 00 00 00`.

6. Insert 10 bytes immediately after the updated `int32` value:  
   - Using the previous example, insert 10 bytes after:  
     `7D 00 00 00`.

7. Replace the newly inserted 10 bytes with the following sequence:  
   `06 00 00 00 53 63 6F 75 74 00`  
   - Explanation:  
     - The first 4 bytes (`06 00 00 00`) represent the length of the dossier name in Little-Endian format, including the null terminator.  
     - The remaining bytes (`53 63 6F 75 74 00`) correspond to the text `Scout\0`.

8. Save the file and close the editor.  

Congratulations, the "Scout FM" dossier check-off should now be completed!

---

## Disclaimer
Editing save files carries inherent risks. Proceed with caution and back up your files before making any changes.  
