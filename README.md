
            OCLP-Tahoe (OpenCore Legacy Patcher — Tahoe Edition)

**OCLP-Tahoe** is a community-maintained continuation of OpenCore Legacy Patcher focused on extending **macOS 26 Tahoe** support to dropped Intel Macs—including **2017–2020 Apple T2 Macs** alongside classic 2008–2019 non-T2 Intel hardware. 

**Disclaimer:** This is an unofficial, experimental fork intended for testing and hardware preservation. Always back up your data with Time Machine before installing or patching macOS. 

#### Key Features Added in OCLP-Tahoe

* **Expanded Apple T2 Mac Support:** Adds OpenCore EFI generation, SMBIOS mapping, and post-install patch support for dropped 2017–2020 T2 Intel Macs: 

  * iMacPro1,1 (2017)
  * MacBookPro15,1, MacBookPro15,2, MacBookPro15,3, MacBookPro15,4 (2018–2019)
  * MacBookPro16,3 (2020)
  * MacBookAir8,1, MacBookAir8,2 (2018–2019) and MacBookAir9,1 (2020)
  * Macmini8,1 (2018)
* **T2-Safe SMBIOS & Security Configuration:** 

  * Maps dropped T2 Macs strictly to Tahoe-supported T2 SMBIOS targets (MacBookPro16,1, MacBookPro16,2, MacPro7,1) to prevent bridgeOS (AppleT2) and AppleANS2Controller NVMe panics.
  * Automatically sets SecureBootModel = Disabled and injects AMFIPass.kext on T2 models so patched Tahoe kernelcaches boot cleanly.
* **T2 Broadcom Wireless Detection (BCM4364 / BCM4377):** Adds AppleBCMWLANBusInterfacePCIe chipset detection to ModernWireless so T2 Macs receive wireless root patches on macOS 26 Tahoe.
* **Live Apple Software Update Catalog (sucatalog) Discovery:** Fetches macOS 26 Tahoe installers directly from Apple's live sucatalog feeds (Public Release & Developer Seed) without waiting for third-party database mirrors.
* **Seamless Unsigned / Community Build Elevation:** Includes an automatic osascript administrator elevation fallback when running self-compiled or unsigned builds alongside an existing Dortania Privileged Helper installation.

#### Requirements for Apple T2 Macs

Before booting OpenCore or installing macOS 26 Tahoe on a **T2 Intel Mac** (MacBookPro15,x, MacBookPro16,3, MacBookAir8,x/9,1, Macmini8,1, iMacPro1,1): 

1. Shut down your Mac completely.
2. Turn it on and immediately hold **Command (⌘) + R** until the Apple logo appears to enter **macOS Recovery**.
3. Open **Utilities → Startup Security Utility** from the top menu bar.
4. Set **Secure Boot** to **No Security**.
5. Set **Allowed Boot Media** to **Allow booting from external or removable media**.
6. Reboot into your normal macOS installation, run **OCLP-Tahoe**, build and install OpenCore to your target disk, and reboot holding **Option (⌥)** to select **EFI Boot**.

#### Building from Source

bash

git clone https://github.com/<your-username>/OCLP-Tahoe.git
cd OCLP-Tahoe
python3 -m venv oclp_venv
./oclp_venv/bin/pip install --upgrade pip
./oclp_venv/bin/pip install -r requirements.txt pyinstaller
PYTHONPATH=. ./oclp_venv/bin/python3 Build-Project.command --git-branch "3.1.0-tahoe.1"

Use code with caution.

Copy code text to clipboard.

The compiled application bundle will be generated at dist/OpenCore-Patcher.app. 

#### Credits

* **[Dortania](https://github.com/dortania/OpenCore-Legacy-Patcher)** — Original OpenCore Legacy Patcher codebase, documentation, and root-patching architecture.
* **[Acidanthera](https://github.com/acidanthera)** — OpenCorePkg, Lilu, WhateverGreen, RestrictEvents, AppleALC, and essential kernel extensions.
