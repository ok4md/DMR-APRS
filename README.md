# DMR-APRS
A high-performance binary utility designed to bridge DMR (Digital Mobile Radio) data stream to the APRS (Automatic Packet Reporting System) network.

## Project Description
`dmr-aprs` is a compiled application that processes live DMR radio traffic logs and extracts GPS/location telemetry. It parses location data sent by digital handhelds or mobiles and transforms it into standard APRS packets, allowing real-time positioning on tracking networks like APRS.fi. Being a compiled binary, it runs with minimal CPU and memory overhead, making it ideal for embedded systems and hotspots based on Raspberry Pi.

⚠️ **CRITICAL REQUIREMENT & WARNING**
This application is strictly compatible only with versions of **MMDVMHost that feature native MQTT logging support**. It reads the live DMR data directly from MQTT topics. Ensure your MMDVMHost is configured to publish to an MQTT broker before deploying this utility.

---

## First-Time Setup & Configuration

Since `dmr-aprs` is distributed as a compiled binary, you do not need to install source code dependencies. 

### 1. Make the binary executable
After downloading or transferring the binary to your Raspbery PI Debian system, grant it execution permissions:
```bash
chmod +x dmr-aprs
```

### 2. Initial Run & Auto-Configuration
When you run the binary for the very first time, it detects that no configuration file exists. **The application will automatically generate a default configuration file** (e.g., `config.json` or `config.ini`) in the same directory and then exit.

Execute the initial run:
```bash
./dmr-aprs
```

### 3. Edit the Configuration
Open the newly generated configuration file using your preferred text editor (for example, `nano`):
```bash
nano config.json
```
*(Replace `config.json` with the actual filename created by the binary, such as `config.ini` or `dmr-aprs.conf`).*

Fill in your specific details:
* **MQTT:** Broker IP address, port, and topics matching your MMDVMHost configuration.
* **APRS-IS:** Your amateur radio Callsign (e.g., `OK1XXX-10`), APRS passcode, and the target APRS server URL.

---

## Daily Usage

Once the configuration file is populated, simply launch the binary again. It will read the settings and start processing the data stream immediately.

### Running in the Foreground (Testing)
```bash
./dmr-aprs
```

### Running in the Background (Production)
For 24/7 headless operation, it is recommended to run the binary as a persistent background process or a system service.

**Using Screen:**
```bash
screen -S dmr-aprs ./dmr-aprs
```
* To detach: Press `Ctrl + A`, then `D`.
* To resume monitoring: `screen -r dmr-aprs`.
