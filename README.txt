## HOW TO CONFIGURE ECLIPSE

### Project setup:
1) File -> New -> Makefile Project with existing code:
    -> select NuttX folder, specify <None> as toolchain
2) in Project Explorer: right click on project
    -> Properties -> C/C++ general -> Preprocessor include paths, Macros, etc. -> GNU C -> CDT User Setting Entries -> Add
        -> specify "Preprocessor Macros File" with "include/nuttx/config.h" as path
    *NOTE* This file will be generated automatically by calling "make context"!

### Debug configuration:
1) right-click project -> Properties (as in step 2 above)
    -> C/C++ Build -> Manage configurations...
        -> Add a new debug configuration (e.g. named "Debug NuttX") and click OK
    -> In the configuration selector, choose the newly created configuration
    -> In the builder settings below, un-check "use default build command" and enter "make CONFIG_DEBUG_SYMBOLS=y" instead
    -> click "Apply and close"
2) right-click project -> Run as -> Run configurations...
    -> right click "GDB OpenOCD Debugging" -> New configuration
        - "Main" tab:
            -> C/C++ Application: enter "nuttx"
            -> Build configuration: select the previously created one
        - "Debugger" tab;
            -> OpenOCD setup -> Config options: enter "-f ${workspace_loc}/resources/STM32F765VG.cfg"
            -> GDB Client Setup: Make sure that "Actual executable" points to the correct GDB binary.
                Example 1: 
                    Edit "Executable name" to /usr/bin/arm-none-eabi-gdb
                Example 2 (recommended): 
                    -> Click on "Variables..." -> "Edit variables..." -> "New..."
                        - Set "Name" to "cross_prefix"
                        - Set "Value" to "arm-none-eabi-"
                    -> Confirm everything
        - "SVD Path" tab:
            -> enter "${workspace_loc}/resources/cmsis-svd/data/STMicro/STM32F7x5.svd"


