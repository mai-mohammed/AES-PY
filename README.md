# AES Encryption Algorithm (Advanced Encryption Standard)

## **Introduction**

AES (Advanced Encryption Standard) is a symmetric encryption algorithm widely used to secure sensitive data. It is efficient, fast, and robust against cryptanalysis, making it a global standard for encrypting electronic data.

---

## **Key Features**

- **Symmetric Algorithm:** Uses the same key for encryption and decryption.
- **Block Cipher:** Operates on fixed-size blocks (128 bits).
- **Key Lengths:** Supports 128-bit, 192-bit, and 256-bit keys.
- **Rounds:** The number of processing rounds depends on the key length:
  - 10 rounds for 128-bit keys.
  - 12 rounds for 192-bit keys.
  - 14 rounds for 256-bit keys.

---

## **Steps in AES Algorithm**

### **Initialization**
1. The plaintext is divided into 128-bit blocks.
2. The key is expanded into multiple round keys using a key schedule.

### **Input Transformation**
1. The plaintext block is organized into a 4x4 matrix called the state matrix.
2. The initial round key is XORed with the state matrix (AddRoundKey).

### **Rounds (Except Final Round)**
Each round consists of four steps:

1. **SubBytes:**
   - Non-linear byte substitution using a substitution box (S-box).
   - Ensures confusion by replacing each byte with a corresponding byte from the S-box.


2. **ShiftRows:**
   - Rows of the state matrix are cyclically shifted:
     - Row 0 remains unchanged.
     - Row 1 shifts by 1 byte.
     - Row 2 shifts by 2 bytes.
     - Row 3 shifts by 3 bytes.


3. **MixColumns:**
   - Each column of the state matrix is transformed using matrix multiplication over a finite field.
   - Introduces diffusion by mixing data across columns.

4. **AddRoundKey:**
   - The state matrix is XORed with the round key derived from the key schedule.

### **Final Round**
The last round omits the **MixColumns** step and performs only:
- SubBytes
- ShiftRows
- AddRoundKey

### **Output**
After the final round, the state matrix is converted back to a linear array, producing the ciphertext.

---

## **Decryption**
Decryption in AES reverses the encryption process using the same key. Steps like **InvSubBytes**, **InvShiftRows**, and **InvMixColumns** are applied. The round keys are applied in reverse order.

---

## **Security**

- **Key Size:** Longer keys (256 bits) provide higher security but may slow down performance.
- **Non-linear S-Box:** Protects against linear and differential cryptanalysis.
- **Diffusion and Confusion:** Achieved through ShiftRows, MixColumns, and SubBytes operations.

---

## **Applications**

- **Secure Communication:** HTTPS, VPNs.
- **Data Protection:** File and disk encryption.
- **Authentication:** Digital signatures, tokens.

---

## **Implementation Details**

### **1. `main-algo.py`**
- Implements and tests the AES encryption and decryption algorithm as per the **NIST FIPS 197** standard.
- Includes test cases for AES-128, AES-192, and AES-256 with plaintext and keys derived from the official specification.
- Verifies correctness by comparing encrypted outputs (ciphertexts) with expected values from the standard.

#### **Sample Output**
The output includes plaintext, ciphertext, and verification of encryption and decryption:
```
Testing AES-128...
Plaintext: 00112233445566778899aabbccddeeff
Key: 000102030405060708090a0b0c0d0e0f
Ciphertext: 69c4e0d86a7b0430d8cdb78070b4c55a
Recovered Plaintext: 00112233445566778899aabbccddeeff
AES-128 passed successfully!

Testing AES-192...
Plaintext: 00112233445566778899aabbccddeeff
Key: 000102030405060708090a0b0c0d0e0f1011121314151617
Ciphertext: dda97ca4864cdfe06eaf70a0ec0d7191
Recovered Plaintext: 00112233445566778899aabbccddeeff
AES-192 passed successfully!

Testing AES-256...
Plaintext: 00112233445566778899aabbccddeeff
Key: 000102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f
Ciphertext: 8ea2b7ca516745bfeafc49904b496089
Recovered Plaintext: 00112233445566778899aabbccddeeff
AES-256 passed successfully!
```

### **2. `custom-text.py`**
- Extends AES functionality to handle arbitrary plaintext inputs.
- Adds padding to support plaintexts of any size, ensuring compatibility with AES's 16-byte block size requirement.
- Tests AES-128, AES-192, and AES-256 using the custom text: **"mai-mohammed"**.
- Demonstrates padding and unpadding operations with clear outputs, showing the encryption-decryption process step-by-step.


#### **Sample Output**
The output explains padding, encryption, and decryption:
```
Testing AES-128...
Original Plaintext (hex): 6d61692d6d6f61686d6d6564
Padded Plaintext (hex): 6d61692d6d6f61686d6d656404040404
Key (hex): 000102030405060708090a0b0c0d0e0f
Ciphertext (hex): fdc63eedb95970f33ff9f598fe63efa5
Recovered Plaintext (utf-8): mai-moahmmed

Testing AES-192...
Original Plaintext (hex): 6d61692d6d6f61686d6d6564
Padded Plaintext (hex): 6d61692d6d6f61686d6d656404040404
Key (hex): 000102030405060708090a0b0c0d0e0f1011121314151617
Ciphertext (hex): c29c7a4fb5807fdaa0d117ff8fe6a04d
Recovered Plaintext (utf-8): mai-moahmmed

Testing AES-256...
Original Plaintext (hex): 6d61692d6d6f61686d6d6564
Padded Plaintext (hex): 6d61692d6d6f61686d6d656404040404
Key (hex): 000102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f
Ciphertext (hex): 9121f37b1caa75948699b8be8d8a6522
Recovered Plaintext (utf-8): mai-moahmmed
```

---

## **References**

1. [YouTube Playlist: AES Basics and Implementations](https://www.youtube.com/playlist?list=PLBlnK6fEyqRgj06MEnp2VebJ8DgMpF0Zj) - Covers foundational concepts of AES and practical implementations.
2. [YouTube Playlist: Advanced Cryptographic Techniques](https://www.youtube.com/playlist?list=PLWjMI9CAmVU4--SmpzgswTvxLkZqC9QWn) - Provides insights into advanced cryptographic algorithms and their applications.
3. [NIST FIPS 197 Document](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.197-upd1.pdf) - The official specification for the AES encryption standard.