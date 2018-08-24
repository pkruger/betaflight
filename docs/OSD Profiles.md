# OSD Profiles

An OSD Profile is screen or page of OSD elements.  Four OSD profiles are supported, i.e. you can configure 4 different
OSD pages each with their own OSD elements.  Elements may also be on all four pages.  With the OSD Profiles feature
turned off you can have 1 OSD page as before and also turn the OSD on/off via an AUX channel.  Hence users who don't
want this feature is not affected by its availability.  With OSD Profiles enabled the OSD can still be turned on/off
via an AUX channel.  Keep in mind that if an element is used, it must be in the same position on all pages on which it
is visible.


## Configuration

Currently OSD profiles can only be configured via the CLI.  Layout your OSD using the configurator as before, if
elements will be on different pages, but in the same location on a page, they will overlap in the configurator at
this stage.

1. Enable the OSD profile feature via the feature osdprofile command in the CLI.

2. Configure your OSD via the OSD option in the configurator, i.e. element layout, font etc.

3. Turn on Expert mode - see top right of configurator screen "Enable Expert Mode".

4. The OSD Profile selection is performed using an adjustment configured via the Adjustments tab.
   - Enable an adjustment. (If enabled)
   - Select the AUX channel to be used to change OSD Profile. (when channel)
   - Set the range to cover the entire range of the selected AUX channel. (is in range)
   - For the action select "RC Rate Adjustment". (then apply)  This will be configured in the CLI since OSD Profiles
     is not yet supported by the Configurator. "RC Rate Adjustment" is only selected to make the configuration in the
     CLI a little easier below.
   - Select slot 1. (using slot)  (the slot number does not matter)
   - Select the via channel to match the selected AUX channel of above. (when channel).
   - Save

5. Open the CLI and type adjrange followed by enter.

6. Copy the adjrange configured in step 4 above and past it in the command window.  Change the '1' following the range
   of the channel to '33' and press enter.  Type save and press enter.  The configured adjrange will now be saved and
   the FC will reboot.

7. Open the CLI again and type dump osdprofile followed by enter.  The current OSD Profile configuration will be
   dumped to the CLI.

8. Copy the line of an element configured in the OSD into the command window below, i.e. for vbat:
   osdprofile osd_vbat_pos = none
   Change the "none", above to the OSD profiles on which the battery voltage should be displayed, i.e. for profile
   1,3 and 4, type osdprofile osd_vbat_pos = 1,3,4 and press enter.

9. Repeat step 8 for all elements of interest and when complete, type save followed by enter.

10. Configure the AUX channel on your transmitter.  When this channel is changed the OSD Profiles will change displaying
    all the elements configured for the selected profile.

11. To remove an element from an OSD Profile, simply omit the profile number in the osdprofile command, i.e. To only
    display the battery voltage on profile 1 and 4 now, type osdprofile osd_vbat_pos = 1,4 and press enter.

12. To remove an OSD element from all OSD Profiles, again for battery voltage, use osdprofile osd_vbat_pos = 0 and press
    enter.


## Note:

Configurator 10.4.0 does not support OSD Profile hence this feature can only be configured via the CLI at this
stage.  Making configuration changes on the OSD tab or Adjustments tab using the Configurator will clear previously
configured OSD Profile items.
1. When moving an OSD element on the OSD tab, or turning it on/off and saving it, will clear the OSD Profile for that
   element and this would have to be reconfigured in the CLI using the osdprofile command, e.g.
   osdprofile osd_vbat_pos = 1,2
2. When changing an adjustment on the Adjustments tab, the "then apply" item (33) for OSD Profile will also be cleared,
   i.e. set to 0 and would have to be re-configured via the CLI, e.g. adjrange 0 0 8 900 2100 33 8 0 0.
3. OSD Profile selection is not active if the CLI is open, in other words if you change the adjustment while the CLI is
   open, nothing will change.


## Use

After completing the above configuration, you should be able to select the active OSD profile from your radio.  The
profile can be selected/changed at any time while on the ground or in mid flight.


## Useful OSD Profile commands

dump osdprofile >> displays the current OSD Profile configuration.

osdprofile {enter} >> displays the current OSD Profile configuration.
