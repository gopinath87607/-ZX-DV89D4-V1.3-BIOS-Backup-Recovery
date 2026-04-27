# 🖥️ ZX-DV89D4 V1.3 — BIOS Backup & Recovery

> Community BIOS backup for the **ZX-DV89D4 V1.3** motherboard.  
> Useful if your BIOS chip has been erased, corrupted, or bricked.

---

## 📋 Board Information

| Field | Details |
|---|---|
| **Model** | ZX-DV89D4 V1.3 |
| **Serial** | PG-00-0090.B2XDU99D4V1310100 |
| **BIOS Chip** | SOP8 8-pin (W25Q64 / MX25L128 — verify yours) |
| **File Format** | `.bin` |
| **Programmer** | CH341A + SOIC8 Clip |
| **Software** | NEO Programmer |

---

## 📁 Repository Structure

```
ZX-DV89D4-BIOS/
│
├── README.md               ← This file
├── LICENSE                 ← License (MIT or CC0)
│
├── bios/
│   └── ZX-DV89D4_V1.3.bin ← BIOS binary file
│
├── checksum/
│   └── checksums.txt       ← MD5 / SHA256 hashes
│
├── docs/
│   ├── flash-guide.md      ← Full flashing instructions
│   ├── chip-location.jpg   ← Photo of BIOS chip on board
│   └── wiring-diagram.jpg  ← CH341A clip wiring reference
│
└── tools/
    └── links.md            ← Where to download NEO Programmer
```

---

## ⚙️ Tools Required

| Tool | Type | Purpose |
|---|---|---|
| CH341A USB Programmer | Hardware | Interfaces with BIOS chip |
| SOIC8 Test Clip Cable | Hardware | Clips onto the 8-pin chip |
| NEO Programmer | Software | Read / Erase / Write / Verify |
| Windows PC | OS | Required to run NEO Programmer |

---

## 🔧 How to Flash (Step by Step)

### Before You Start
- ❌ Disconnect ALL ATX power from the motherboard
- ❌ Remove the CMOS battery
- ✅ Wait 30 seconds before touching the chip

---

### Step 1 — Find the BIOS Chip
Look for a small **8-pin SOP8 chip** on the motherboard.  
It will be labeled something like `W25Q64`, `MX25L128`, or similar.  
Usually located near the CMOS battery.

> 📸 See `docs/chip-location.jpg` for a photo reference.

---

### Step 2 — Attach the SOIC8 Clip
Clip the SOIC8 test clip onto the chip.  
**Pin 1 of the clip must align with Pin 1 of the chip** (marked by a small dot or notch on the chip corner).

> ⚠️ Wrong orientation will cause detection failure or damage.

---

### Step 3 — Connect and Detect
1. Plug CH341A into your PC via USB
2. Open **NEO Programmer**
3. Click **Detect** — the chip model should appear automatically
4. If not detected: reseat the clip and try again

---

### Step 4 — Load the BIOS File
1. Click **File → Open**
2. Select `bios/ZX-DV89D4_V1.3.bin`
3. Confirm the file size matches your chip:
   - `8MB = 8,388,608 bytes`
   - `16MB = 16,777,216 bytes`

---

### Step 5 — Erase → Program → Verify
Run these three operations **in order**:

```
1. Erase    ← Clears the chip completely
2. Program  ← Writes the .bin file to the chip
3. Verify   ← Confirms the write was successful
```

> ✅ All three must complete successfully. Do NOT skip Verify.

---

### Step 6 — Reassemble and Test
1. Remove the SOIC8 clip
2. Reinsert the CMOS battery
3. Reconnect all ATX power cables
4. Power on — the board should POST normally

---

## ✅ Verify the File (Checksum)

Before flashing, verify the file integrity:

```bash
# On Windows (PowerShell)
Get-FileHash .\bios\ZX-DV89D4_V1.3.bin -Algorithm MD5

# On Linux / macOS
md5sum bios/ZX-DV89D4_V1.3.bin
```

Compare the output with the hashes in `checksum/checksums.txt`.

---

## ⚠️ Critical Warnings

> **Read before proceeding. Ignoring these can permanently damage your chip.**

- 🔴 **Voltage mismatch kills chips.** Most BIOS chips are 3.3V. Some are 1.8V. Check the chip datasheet BEFORE flashing.
- 🔴 **Many CH341A boards output 3.6V instead of 3.3V.** A voltage mod or 1.8V adapter may be required for sensitive chips.
- 🔴 **Never flash while the board is connected to ATX power.**
- 🟡 If the board does not POST after flashing, repeat the Erase → Program → Verify cycle.
- 🟡 If chip detection fails repeatedly, check clip pin alignment and USB connection.
- 🟢 Always make a **Read backup** of the original chip contents before erasing, if any data remains.

---

## 📦 Checksum File Format

`checksum/checksums.txt`:
```
MD5:    [insert md5 hash here]
SHA256: [insert sha256 hash here]
SIZE:   [insert byte size here]
FILE:   ZX-DV89D4_V1.3.bin
```

---

## 🔗 Useful Links

- [NEO Programmer Download](#) — *(add link)*
- [CH341A Voltage Mod Guide](https://www.badcaps.net/forum/) — Badcaps Forums
- [SOP8 Chip Datasheet lookup](https://www.alldatasheet.com/)
- [Elektroda BIOS Forum](https://www.elektroda.pl/)

---

## 📜 License

This BIOS file is shared for **personal repair and recovery purposes only**.  
Use at your own risk. The author takes no responsibility for damage caused by incorrect flashing.

---

## 💬 Issues & Help

If you run into problems, open a **GitHub Issue** on this repository with:
- Your chip model (read it off the chip physically)
- Which step failed
- Any error message from NEO Programmer

Community help is welcome. ⭐ Star this repo if it helped you!
