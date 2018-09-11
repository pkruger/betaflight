# OSD Profiles

An OSD Profile is a screen or page of OSD elements.  Three OSD profiles are supported, i.e. you can configure 3 different OSD pages each with their own OSD elements.  Elements may also be on all four pages.  With the OSD Profiles feature turned off you can have 1 OSD page as before and also turn the OSD on/off via an AUX channel.  Hence users who don't want this feature is not affected by its availability.  With no profiles configured for elements, all elements are visible, i.e. osdprofile 0.  The OSD can still be turned off via an AUX channel, like before. (This applies to all profiles.)  Keep in mind that if an element is used, it must be in the same position on all pages on which it is visible.  It is not possible to configure an element to be in different locations in different profiles.

## Configuration

Currently (Configurator 10.4.0) OSD profiles can only be configured via the CLI.  Layout your OSD using the configurator as before, if elements will be on different pages, but in the same location on a page, they will overlap in the configurator at this stage.  OSD Profiles can either be selected via an adjustment range (Adjustments tab) or by selecting the osdprofile in the CLI via the osdprofile command.  This works similar to rateprofile.

1. Configure your OSD via the OSD option in the configurator, i.e. element layout, font etc.
2. If using an adjustment range, follow steps 2.1 to 2.5 below:
2.1 Turn on Expert mode - see top right of configurator screen "Enable Expert Mode".
2.2 The OSD Profile selection is performed using an adjustment configured via the Adjustments tab.
    - Enable an adjustment. (If enabled)
    - Select the AUX channel to be used to change OSD Profile. (when channel)
    - Set the range to cover the entire range of the selected AUX channel. (is in range)
    - For the action select "RC Rate Adjustment". (then apply)  This will be configured in the CLI since OSD Profiles is not yet supported by the Configurator. "RC Rate Adjustment" is only selected to make the configuration in the CLI a little easier below.
    - Select slot 1. (using slot)  (the slot number does not matter)
    - Select the via channel to match the selected AUX channel of above. (when channel).
    - Save
2.3 Open the CLI and type adjrange followed by enter.
2.4 Copy the adjrange configured in step 4 above and past it in the command window.  Change the '1' following the range of the channel to '33' and press enter.  Type save and press enter.  The configured adjrange will now be saved and the FC will reboot.
2.5 Configure the AUX channel on your transmitter.  When this channel is changed the selected OSD Profile will change displaying all the elements configured for the selected profile.
3. If using the CLI to choose an OSD profile, follow steps 3.1 to 3.2 below:
3.1 Open the CLI.
3.2 Type osdprofile followed by enter to display the currently selected profile.
3.3 Type osdprofile followed by the profile number to be selected and press enter.
3.4 Type save followed by enter to save the selected profile.
4. Open the CLI and type dump osdprofile followed by enter.  The current OSD Profile configuration will be dumped to the CLI.
5. Copy the line of an element configured in the OSD into the command window below, i.e. for vbat: ```osdprofile osd_vbat_prf = none``` Change the "none", above to the OSD profiles on which the battery voltage should be displayed, i.e. for profile 1,2 and 3, type osdprofile osd_vbat_prf = 1,2,3 and press enter.
6. Repeat step 5 for all elements of interest and when complete, type save followed by enter to save the settings.
7. To remove an element from an OSD Profile, simply omit the profile number in the osdprofile command, i.e. To only display the battery voltage on profile 1 and 3 now, type ```osdprofile osd_vbat_prf = 1,3``` and press enter.
8. To remove an OSD element from all OSD Profiles, i.e. for battery voltage, use ```osdprofile osd_vbat_prf = 0``` and press enter.
9. You can also use set osd_vbat_prf to set the profiles of an element, but in this case only one value is entered and the value needs to be made up in binary, i.e. for profile 1, add 1, for profile 2, add 2 and for profile 3, add 4 (yes 4).  For example, to set profile 1 and 3 for an element, use a value of 5.  And to set profile 2 and 3, use a value of 6.

## Note:

1. When changing an adjustment on the Adjustments tab, the "then apply" item (33) for OSD Profile will also be cleared, i.e. set to 0 and would have to be re-configured via the CLI, e.g. ```adjrange 0 0 8 900 2100 33 8 0 0```
2. OSD Profile selection via adjustment range is not active if the CLI is open, in other words if you change the adjustment while the CLI is open, nothing will change, the selected OSD profile will remain as is.

## Use

After completing the above configuration, you should be able to select the active OSD profile from your radio or via the CLI.  The profile can be selected/changed at any time while on the ground or in mid flight.

## Useful OSD Profile commands

dump osdprofile >> displays the current OSD Profile configuration for each element.

osdprofile {enter} >> displays the currently selected osd profile in the CLI.
