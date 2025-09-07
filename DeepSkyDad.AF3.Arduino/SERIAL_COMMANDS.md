# DeepSkyDad.AF3.Arduino Command Reference

This firmware accepts ASCII commands over UART for controlling and configuring the AF3 focuser. Each command is 4 characters, optionally followed by a parameter.

## Command List

| Command | Parameter | Description |
|---------|-----------|-------------|
| **LEGT** |           | Run legacy motor test. |
| **GFRM** |           | Get firmware name and version. |
| **GPOS** |           | Get current position. |
| **GTRG** |           | Get current target position. |
| **STRG** | position  | Set target position. |
| **GMOV** |           | Get moving status (1 = moving, 0 = stopped). |
| **SMOV** |           | Start movement to target position. |
| **STOP** |           | Stop the motor. |
| **GMXP** |           | Get maximum allowed position. |
| **SMXP** | position  | Set maximum allowed position. |
| **GMXM** |           | Get maximum allowed movement. |
| **SMXM** | steps     | Set maximum allowed movement. |
| **GMST** |           | Get manual step mode. |
| **GSTP** |           | Get current step mode. |
| **SSTP** | mode      | Set step mode. |
| **GSPD** |           | Get speed mode. |
| **SSPD** | mode      | Set speed mode. |
| **RSET** |           | Reset all settings to defaults. |
| **RBOT** |           | Reboot the controller. |
| **GBUF** |           | Get settle buffer time (ms). |
| **SBUF** | ms        | Set settle buffer time (ms). |
| **WEPR** |           | Write EEPROM (no-op, always OK). |
| **GREV** |           | Get reverse direction (1 = reversed, 0 = normal). |
| **SREV** | 0/1       | Set reverse direction. |
| **SPOS** | position  | Sync current position. |
| **GIDE** |           | Get idle EEPROM write interval (ms). |
| **SIDE** | ms        | Set idle EEPROM write interval (ms). |
| **GMMM** |           | Get motor I-move multiplier. |
| **SMMM** | value     | Set motor I-move multiplier. |
| **GMHM** |           | Get motor I-hold multiplier. |
| **SMHM** | value     | Set motor I-hold multiplier. |
| **GTMC** |           | Get temperature (°C). |
| **DEBG** |           | Print debug info to serial. |

## Response Codes

Each response starts with ( and ends with )
If command results in error, response starts with ! and ends with ), containing error code. List of error codes:
* 100 - command not found
* 101 - relative movement bigger from max. movement
* 102 - invalid step mode
* 103 - invalid speed mode
* 999 - UART not initalized (check motor power)
* The actual set of required commands is based on ASCOM IFocuserV3 interface, for more check:

## Usage

Send commands as ASCII strings. For commands requiring parameters, append the parameter after the command (no separator).

**Example:**  
`STRG10000` — Set target position to 10000.

**Note:**  
Some commands may require the UART to be initialized before use.

---