# Supported G-Code

## Overview

G-Code first came about in the late 1950s and is considered a computer programming language.  It is standardized under [ISO 6983-1](https://www.iso.org/standard/34608.html) and [NIST RS274](https://ws680.nist.gov/publication/get_pdf.cfm?pub_id=823374).  Intimidating?

Don’t worry; we include this information just for completeness.  The 3D printing industry has only adopted portions of the code which has significantly simplified it from a full-blown programming language into a simpler set of instructions.  M3D has continued to optimize this set of instructions to be as efficient as possible which will account for differences between our G-Code and other G-Code flavors, though we strive to keep these differences to a minimum.

{% hint style="info" %}
What follows on this page may include information that is specific to M3D's implementation of G-Code in the Micro, Pro and Micro+ products.
{% endhint %}

Let’s go over a short overview.  G-Codes always have a standard format.  They are a list of pairs where a pair is a single character followed by a number.  The character defines how to interpret and apply the number that follows.  The first pair in a line \(command number\) is always the letter M or G which specifies the command set.  This is followed by the command number, which is an integer that specifies the command the printer will attempt to execute.  This is followed by a set of pairs that modify the command's behavior and differ based on what command is being sent.  These pairs are separated by a space.  Within each pair, there is no space between the letter and the number.  Don't worry, the rest of this page covers these fields and their formats and gives examples.  Lastly, the line is terminated by a newline character \(or enter on the keyboard\).

A semi-colon denotes a comment; any text written afterward will be ignored by the printer.

## G-Codes
* **G0 X Y Z E F** - [Move](https://reprap.org/wiki/G-code#G0_.26_G1:_Move)
  * **G0 Z0** - Go to printer's Z-0 (lowest Z point). Make sure to switch to Absolute Mode first.
* **G1 X Y Z E F** - [Move](https://reprap.org/wiki/G-code#G0_.26_G1:_Move)
* **G4 S P** - [Dwell](https://reprap.org/wiki/G-code#G4:_Dwell)
* **G20** - [Set Units to Inches](https://reprap.org/wiki/G-code#G20:_Set_Units_to_Inches)
* **G28** - [Move to Home Location](https://reprap.org/wiki/G-code#G28:_Move_to_Origin_.28Home.29)
* **G30 Z** - probably [Single Z-Probe](https://reprap.org/wiki/G-code#G30:_Single_Z-Probe)
* **G32 Z** - probably [Probe and Calculate](https://reprap.org/wiki/G-code#Probe_and_calculate_in_Reprapfirmware)
* **G33** - Save the current Z height as the printer's Z-0
* **G90** - [Set to Absolute](https://reprap.org/wiki/G-code#G90:_Set_to_Absolute_Positioning)
* **G91** - [Set to Relative](https://reprap.org/wiki/G-code#G91:_Set_to_Relative_Positioning)
* **G92 X Y Z E** - [Set Position](https://reprap.org/wiki/G-code#G92:_Set_Position)
  * **G92 E0** - Reset E

## M-Codes

* **M0** - [Emergency Stop](https://reprap.org/wiki/G-code#M0:_Stop_or_Unconditional_stop)
* **M1** - [Halt All Moves](https://reprap.org/wiki/G-code#M1:_Sleep_or_Conditional_stop)
* **M17** - probably [Enable all motors](https://reprap.org/wiki/G-code#M17:_Enable.2FPower_all_stepper_motors)
* **M18** - probably [Disable all motors](https://reprap.org/wiki/G-code#M18:_Disable_all_stepper_motors)
* **M20** - [Refresh SD Card List](https://reprap.org/wiki/G-code#M20:_List_SD_card)
* **M21** - probably [Initialize SD Card](https://reprap.org/wiki/G-code#M21:_Initialize_SD_card)
* **M22** - probably [Release SD Card](https://reprap.org/wiki/G-code#M22:_Release_SD_card)
* **M23** - probably [Select SD Card](https://reprap.org/wiki/G-code#M23:_Select_SD_file)
* **M24** - probably [Start/Resume SD Print](https://reprap.org/wiki/G-code#M24:_Start.2Fresume_SD_print)
* **M25** - probably [Pause SD Print](https://reprap.org/wiki/G-code#M25:_Pause_SD_print)
* **M26 S** - probably [Set SD Position](https://reprap.org/wiki/G-code#M26:_Set_SD_position)
* **M27** - probably [Report SD Print Status](https://reprap.org/wiki/G-code#M27:_Report_SD_print_status)
* **M28** - probably [Begin Write to SD Card](https://reprap.org/wiki/G-code#M28:_Begin_write_to_SD_card)
* **M29** - probably [Stop Write to SD Card](https://reprap.org/wiki/G-code#M29:_Stop_writing_to_SD_card)
* **M30 _filename_** - [Delete File from SD Card](https://reprap.org/wiki/G-code#M30:_Delete_a_file_on_the_SD_card)
* **M31** - possibly [Output time since last M109 or SD Card Start](https://reprap.org/wiki/G-code#M31:_Output_time_since_last_M109_or_SD_card_start_to_serial)
* **M32** - probably [Begin Print from SD Card](https://reprap.org/wiki/G-code#M32:_Select_file_and_start_SD_print)
* **M104 S** - [Set Extruder Temp](https://reprap.org/wiki/G-code#M104:_Set_Extruder_Temperature)
* **M105** - [Get Extruder Temp](https://reprap.org/wiki/G-code#M105:_Get_Extruder_Temperature)
* **M106 S** - [Fan on](https://reprap.org/wiki/G-code#M106:_Fan_On)
* **M107** - [Fan off](https://reprap.org/wiki/G-code#M107:_Fan_Off)
* **M109 S** - [Set extruder temp and wait](https://reprap.org/wiki/G-code#M109:_Set_Extruder_Temperature_and_Wait)
* **M110** - possibly [Set current line number](https://reprap.org/wiki/G-code#M110:_Set_Current_Line_Number)
* **M114** - [Get Extruder Location](https://reprap.org/wiki/G-code#M114:_Get_Current_Position)
* **M115 S628** - Only support S == 628 ; [Go To Bootloader](https://reprap.org/wiki/G-code#M115:_Get_Firmware_Version_and_Capabilities)
* **M116** - [Wait](https://reprap.org/wiki/G-code#M116:_Wait)
* **M117** - [Get Internal State](https://reprap.org/wiki/G-code#M117:_Get_Zero_Position)
* **M140 S** - [Set Bed Temp](https://reprap.org/wiki/G-code#M140:_Set_Bed_Temperature_.28Fast.29)
* **M190 S** - [Wait for bed to reach temp](https://reprap.org/wiki/G-code#M190:_Wait_for_bed_temperature_to_reach_target_temp)
* **M303** -  Set Gantry Clips To Off
* **M304** - Set Gantry Clips To On
* **M333 X** - Unknown
* **M404 R** - probably Clear Power Recovery Fault
* **M405** - Unkown
* **M420 T** - Unknown
* **M570 P** - Set Filament Id
  * Generates `M618 S P T` based on P value.
* **M571 X Y** - Set Backlash Constants 
  * Generates `M618 S P T` based on X Y values.
* **M572** - Get Backlash
* **M573** - Get Bed Leveling Values
* **M575 S P T E I R** - Set Filament 
  * S:FilamentColorId, P:FilamentTypeId, T:FilamentTemperatureId, E:FilamentAmount I:FilamentSize R:Unused
  * Generates `M618 S P T` based on S P T E I R values.
* **M576** - Get Filament Info
* **M577 X Y Z E F I** ; SetBedOffsets 
  * X:BackLeftOffset, Y:BackRightOffset, Z:FrontRightOffset, E:FrontLeftOffset, F:ZOffset I:CalibrationOffset
  * Generates `M618 S P T` based on X Y Z E F I values.
* **M578** - Get Current Bed Offsets
* **M580 X** - Set Backlash Speed
* **M581** - Get Backlash Speed
* **M582 S** - Set Nozzle Width
  * S:NozzleWidth
  * (Doesn't appear to be supported in main switch statement)
  * Generates `M618 S P T` based on S value.
* **M583** - Get Nozzle Width
* **M618 S P T** - Set value in eeprom
  * S:eepromAddress P:value T:size
* **M619 S T** - Probably Read value in eeprom.
  * S:eepromAddress T:size
* **M682 X Y Z E R** - Set Limiting Speed 
  * Generates `M618 S P T` based on X Y Z E R value.
* **M683** - Get Limiting Speed
* **M684** - Print All Eeprom Values
* **M997** - Unknown
* **M998** - Unknown
* **M999** - Unknown
* **M1011** - Enable Bounds Checking
* **M1012** - Disable Bounds Checking/Unlock Z axis (for calibration)
* **M1013** - Stopwatch Start
* **M1014** - Stopwatch Stop
* **M5321 X** - Unknown
* **M5680** - Get Hours Used
* **M16007** - Unknown
* **M17013** - Unknown
* **M18010** - Unknown
* **M19007** - Unknown
* **M20904** - Unknown
* **M21914** - Unknown
* **M23975** - Unknown


