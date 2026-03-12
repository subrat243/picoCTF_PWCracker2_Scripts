# Hex to ASCII Converter (CTF Utilities)

Utilities created for solving picoCTF challenges such as PW Crack 2 where encoded values (hex / 0x hex) must be converted to readable ASCII during password or flag analysis.

---

## PW Crack 2

### Description

Can you crack the password to get the flag?
Download the password checker and the encrypted flag file. Both files must be placed in the same directory.

The goal of this challenge is to analyze the password checker script, understand how the password is constructed, and recover the correct password to decrypt the flag.

---

## Solution Strategy

1. **Analyze the Provided Script**

   The first step is to inspect the password checker script provided in the challenge.
   Read the code carefully to understand how the password is validated.

   ```bash
   cat level2.py
   ```

2. **Understand the Password Construction**

   While analyzing the script, observe how the password is generated.
   In this challenge, the password is constructed using Python `chr()` functions with hexadecimal values.

   Example pattern:

   ```python
   chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65)
   ```

3. **Convert Hexadecimal Values to ASCII**

   Each `chr()` value represents an ASCII character.
   Converting them reveals the actual password string.

   Example:

   ```
   0x33 → 3
   0x39 → 9
   0x63 → c
   0x65 → e
   ```

   Result:

   ```
   39ce
   ```

4. **Automate the Conversion**

   To simplify decoding, helper scripts were created in this repository to convert:

   * Plain hex → ASCII
   * `0x` formatted hex → ASCII

   These scripts allow quick decoding during CTF analysis.

5. **Use the Correct Password**

   After reconstructing the password, run the password checker with the recovered value.
   If the password is correct, the script will decrypt the encrypted flag.

### Files

```
level2.py
level2.flag.txt.enc
```

### Tools Used

* Python
* Bash
* Hex to ASCII conversion utilities
* Basic script analysis

### Debug / Notes

During analysis, encoded values inside the script may need to be converted from hexadecimal to ASCII. The helper scripts in this repository can be used to quickly decode those values.

---

## Hex to ASCII Converter

Simple utilities to convert hexadecimal values to ASCII text.

### Features

* Python and Bash implementations
* Supports plain hex strings
* Supports `0x` prefixed hex values
* Useful for CTFs and password/flag decoding

---

## Usage

### Python — Plain Hex

```
python3 python/hex_to_ascii_plain.py
```

### Python — 0x Format

```
python3 python/hex_to_ascii_0x.py
```

### Bash — Plain Hex

```
bash bash/hex_to_ascii_plain.sh
```

### Bash — 0x Format

```
bash bash/hex_to_ascii_0x.sh
```

---

## One-Liners

### Python (Plain Hex)

```bash
python3 -c "print(bytes.fromhex(input().strip()).decode())"
```

### Python (0x Format)

```bash
python3 -c "import re;print(''.join(chr(int(x,16)) for x in re.findall(r'0x[0-9a-fA-F]+', input())))"
```

### Bash (Plain Hex)

```bash
echo "48656c6c6f" | xxd -r -p
```

### Bash (0x Format)

```bash
echo "0x48 0x65 0x6c 0x6c 0x6f" | sed 's/0x//g' | tr -d ' ' | xxd -r -p
```

---

## License

MIT License - see [LICENSE](LICENSE) file for details.

---


# File: bash/hex_to_ascii_plain.sh

Make executable:

```
chmod +x bash/hex_to_ascii_plain.sh
```

---

# File: bash/hex_to_ascii_0x.sh

Make executable:

```
chmod +x bash/hex_to_ascii_0x.sh
```
