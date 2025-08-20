# ST-Link support for VSCode-Arduino
### situation
[Arduino 2 is problematic for me.](https://blekenbleu.github.io/static/Arduino2/)  
I installed [VSCode-Arduino Community](https://marketplace.visualstudio.com/items?itemName=vscode-arduino.vscode-arduino-community) without first uninstalling Arduino 2.  
- VSCode-Arduino discovered that installation and used it.  
- programming STM32 boards by ST-Link in that installation is broken for VSCode-Arduino  

*20 Aug 2025*  
- [Arduino STM32 core](https://github.com/stm32duino/Arduino_Core_STM32) at [release 2.7.1](https://github.com/stm32duino/Arduino_Core_STM32/releases/tag/2.7.1)
	was seemingly the last before [stlink programmer removal](https://github.com/stm32duino/Arduino_Core_STM32/commit/f9a35fd714b889475e067d8c2c72c551ea3c0cba),   
	but `boards.txt`, `platform.txt` and `programmers.txt` lack `stlink` back to at least 2.5.0...  

## To enable ST-Link for [VSCode-Arduino](https://blekenbleu.github.io/static/VSCodeArduino/programming.htm):  
- Download this ZIP and extract to a folder
- Configure vscode-arduino to find [**arduino-cli**](https://github.com/arduino/arduino-cli/releases/download/v1.3.0/arduino-cli_1.3.0_Windows_64bit.zip) *this folder*.  
- Download the appropriate arduino-cli release and copy its executible here.
- `stlink.programmer.transport_script={runtime.platform.path}/debugger/select_hla.cfg`  
	in `programmers.txt` did not help.  
- adding `GenF4.programmer.default=stlink` in `boards.txt` was essential to Black Pill uploading.
	- `Arduino: Upload` and `Arduino CLI: Upload` work;  
	- `Arduino CLI: Upload using Programmer` does *NOT*  
- **You must edit** `boards.txt` for other STM32 boards,  
	according to [stm32duino Arduino_Core_STM32 Commit f9a35fd](https://github.com/stm32duino/Arduino_Core_STM32/commit/f9a35fd714b889475e067d8c2c72c551ea3c0cba)
- Debugging in VSCode-Arduino may be a bridge too far;
	- [M$ seemingly dropped debugging at version 0.5.0](https://github.com/Tnthr/vscode-arduino-debug#visual-studio-code-extension-for-arduino-the-fork)
	- [Arduino_Core_STM32 added openocd debug](https://github.com/stm32duino/Arduino_Core_STM32/pull/1976/files#diff-5c378d0844f0422d4d813eabe83f61ffce82014d8b8aa3e93ee35ce2ca14ca7b)
		18 Mar 2023, [discussed here](https://github.com/stm32duino/Arduino_Core_STM32/issues/1896)

