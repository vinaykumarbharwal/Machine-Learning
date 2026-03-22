# Walkthrough: Decoding Mimir's Rune

I have successfully analyzed the `rune.exe` binary and recovered the hidden flag.

## Steps Taken

### 1. Unpacking the Binary
The file was identified as a Windows PE executable packed with **UPX**. I unpacked it to reveal the underlying machine code.

### 2. Identifying Core Logic
I located several interesting components in the `.text` section:
*   **Static XOR Transformation**: A sequence of 35 bytes is initialized on the stack and then XORed with the constant `0x7F`.
*   **Encrypted Buffer Mapping**: By carefully tracing the `movb` instructions, I mapped the entire 35-byte buffer.

### 3. Decryption
The first 7 bytes of the buffer XORed with `0x7F` yielded `REDFOX{`, confirming the algorithm. Applying this to the entire 35-byte buffer revealed the full flag.

## Verification Results
The logic was confirmed to be a simple **XOR with 0x7F** on a 35-byte stack buffer.

### Recovered Flag
`REDFOX{P4cK_anD_UnP4Ck_th1s_B1n4ry}`

## Produced Files
*   `rune_extracted.exe`: Unpacked binary.
*   [final_flag.py](file:///Users/apple/Desktop/CTF/final_flag.py): Definitive decryption script.
