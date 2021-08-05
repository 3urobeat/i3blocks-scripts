# i3blocks-scripts
My self-made i3blocks scripts

## Scripts:

### cpu
Gets the utilization (load) & temperature from 'mpstat' & 'sensors' to be used with i3blocks. Supports warn and crit colors.  

Call file with -f flag and provide format in a string. The script will replace the keywords in your format string with the corresponding values.  
Provide the chip flag with the sensor of your CPU temp. Be sure to run 'sudo sensors-detect' in order to find and probe your CPU temp sensor. For me (AMD Ryzen) it is 'k10temp-pci-00c3'.  
Provide the lwarn and or lcrit flag with a number to change the color of the load output.  
Provide the twarn and or tcrit flag with a number to change the color of the temperature output.  

Example: `./cpu -chip k10temp-pci-00c3 -f "CPU: {load} {temp}"`    ...will result in: "CPU: 34% 39°C"  

**Disclaimer:** Read the pango font note under 'Additional informations' at the bottom of this file otherwise the warn & crit colors won't work!  

### gpu
Supports only Nvidia cards.  
Gets the utilization (load), temperature & vram usage from nvidia-settings to be used with i3blocks. Supports warn and crit colors.  

Call file with -f flag and provide format in a string. The script will replace the keywords in your format string with the corresponding values (see example below).  
Provide the lwarn and or lcrit flag with a number to change the color of the load and vram output.  
Provide the twarn and or tcrit flag with a number to change the color of the temperature output.  

Example: `./gpu -f "GPU: {load} TEMP: {temp} VRAM: {vram}"`    ...will result in: "GPU: 34% TEMP: 39°C VRAM: 17%"  
  
**Disclaimer:** Read the pango font note under 'Additional informations' at the bottom of this file otherwise the warn & crit colors won't work!  

### updates
Gets the amount of available package updates (+AUR).  
Click the block to see which packages can be updated (notification).  
  
Disclaimer: Needs 'checkupdates+aur' package from the AUR to work.  

### volume
Shows the current master volume from amixer. Scroll up/down to change volume. Middle click to mute.  


## Additional informations

### pango
Your i3block needs to include 'markup=pango' and the font you are using when calling the bar in your i3 config needs to be prefixed with 'pango:' for the colors to work!  
i3blocks.conf example:  
```
[gpu]
command=$SCRIPT_DIR/gpu -f "GPU: {load} TEMP: {temp} VRAM: {vram}"
markup=pango
interval=3
```  
  
config:  
```
bar {
    font pango:Futura Bk Bt Bold 11
    status_command i3blocks -c ~/.config/i3/i3blocks.conf
}
```  