# MSFS Spoofer

A minimal Windows executable that idles indefinitely under the process name `FlightSimulator2024.exe`. Used for tricking external flight sim apps (e.g. BeyondATC, Mobiflight, ...) which check for a running MSFS 2024 instance before they will start.
>This is intended for MSFS 2024, but may work with 2020, rename to `FlightSimulator.exe`. I've not tested this.

The process uses zero CPU, blocked on `Sleep(INFINITE)`, and just a few MB of RAM.

## Files

- `stub.c` -- source file
- `FlightSimulator2024.exe` -- if you just want to run it

## Using the pre-built binary

Download `FlightSimulator2024.exe` and run it on the BATC/second PC. It will appear in Task Manager under that name with no visible window. Kill it from Task Manager when you're done.

## Building it

If you'd prefer not to run a random person's executable then there are two options here to build yourself from source. I used Visual Studio.
- Download (and inspect if you wish) `stub.c`

### Option A - Visual Studio

You need the **Desktop development with C++** workload installed.

1. Open **Developer PowerShell for VS**
2. Navigate to the folder containing `stub.c`:
   ```powershell
   cd C:\path\to\your\folder
   ```
3. Compile:
   ```
   cl /O2 /DNDEBUG stub.c /link /SUBSYSTEM:WINDOWS /OUT:FlightSimulator2024.exe
   ```
4. `FlightSimulator2024.exe` will appear in the same folder.

### Option B - Tiny C Compiler

TCC should also work, it is a very small download with no installer:
1. Download and install from https://repo.or.cz/tinycc.git or mirrored on github at https://github.com/Tiny-C-Compiler/tinycc-mirror-repository
2. From a command prompt in the folder containing `stub.c`:
   ```
   tcc -Wl,-subsystem=windows stub.c -o FlightSimulator2024.exe
   ```

## Running & Stopping it

No admin needed, just run it. The process has no window and no tray icon. As it uses basically no resources I have it run on system startup.

If needed you can end it from Task Manager.
