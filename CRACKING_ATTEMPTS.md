# SalPhaselon/Cosmic Duality Cracking Attempts

This document summarizes systematic attempts to crack the AES-encrypted blobs in the SalPhaselon and Cosmic Duality phases.

## Key Observations

### Critical Discrepancy: Two Different AES Blobs

**README blob (embedded in SalPhaselon section):**
```
U2FsdGVkX186tYU0hVJBXXUnBUO7C0+X4KUWnWkCvoZSxbRD3wNsGWVHefvdrd9z
QvX0t8v3jPB4okpspxebRi6sE1BMl5HI8Rku+KejUqTvdWOX6nQjSpepXwGuN/jJ
```

**Image blob (Cosmic Duality section) - DIFFERENT:**
```
U2FsdGVkX18tP2/gbc1Q5tNZuD4shoV3axuUd8J8aycGCAMoYfhZK0JecHTDpTFe
dGJh4SJIP66qRtXvo7PtpvsIjw08prLiC/sNHthxiGMuqIrKo0224rOisFJZgARi
c7PaJPne4nab8XCFuV3NbfxGX2BUjNkef5hg7nsoadZx08dNyU2b6eiciWiUvu7D
[...continues for many more lines...]
```

Note: After the common "U2FsdGVk" prefix (which decodes to "Salted"), the content differs entirely:
- README: `X186tYU0...` (salt: `3ab5853485`)
- Image: `X18tP2/g...` (salt: `2d3f6fe06d`)

This suggests **two separate encrypted payloads** requiring different passwords.

### Hint Analysis

**Primary Hint:** "sha b e f our first hint is your last command"
- `sha bef` = SHA256 (b=2, e=5, f=6 in puzzle encoding)
- "our first hint" - ambiguous reference
- "is your last command" - use as final password

**Secondary Hint:** "sha bef ans too"
- "sha256 ans too" = SHA256 the answer too
- Suggests multi-step decryption

**WebFetch discrepancy:** One source showed "four first hint" instead of "our first hint"
- If "four", could mean the 4th decoded element: `thispassword`

## Decoded Elements from SalPhaselon

| Order | Element | Decoding Method |
|-------|---------|-----------------|
| 1 | `matrixsumlist` | Binary (a=0, b=1) |
| 2 | `enter` | Binary (a=0, b=1) embedded in AES blob |
| 3 | `lastwordsbeforearchichoice` | a1z26 -> decimal -> hex -> ASCII |
| 4 | `thispassword` | a1z26 -> decimal -> hex -> ASCII |

## Password Candidates Tested (500+)

### SHA256 Hashes Tested

| Password | SHA256 Hash | Result |
|----------|-------------|--------|
| matrixsumlist | e7546e3076294907ed2a0ecaa9c33062f6e602b7c74c5aa5cc865df0ff345507 | Garbage |
| theseedisplanted | 6e3f5a7baf924d8546f5f7af94a43b8424e3c810983f9795eb8451ad4243d860 | Garbage |
| enter | e08d706b3e4ce964b632746cf568913cb93f1ed36476fbb0494b80ed17c5975c | Garbage |
| lastwordsbeforearchichoice | 77094e7a1591fb81379f1582cf88db5aa6ab8e77176a4d8428a1ff5decfd102d | Garbage |
| thispassword | 74c1d7592daf4f89b0a7ba5e368bb59cc9e19c6a4ebb7f33cd8ccf8f3edacac0 | Garbage |
| HASHTHETEXT | 5968dc5e02cbdf8181d135f143372e7062504cc06268e094ceae25b56c5a72ae | Garbage |
| matrixsumlistenter | 9e191ca45828034621d4a035572afecb024300bb73c91af0350973170e56f020 | Garbage |

### Combination Passwords

| Combination | Result |
|-------------|--------|
| matrixsumlist + enter + lastwordsbeforearchichoice + thispassword | Garbage |
| All elements space-separated | Garbage |
| All elements with + separator | Garbage |

### Matrix-Themed Passwords

| Password | Result |
|----------|--------|
| sheisgoingtodieandthereisnothingthatyoucandotostopit | Garbage |
| theproblemischoice | Garbage |
| hope, denial, bullshit | Garbage |
| THEMATRIXHASYOU | Garbage |
| causality | Garbage |

### Archimedes Interpretation (for "archi")

| Password | Result |
|----------|--------|
| donotdisturbmycircles | Garbage |
| noliturbarecirculosmeos | Garbage |
| eureka | Garbage |

### Previous Phase Passwords

| Password | Result |
|----------|--------|
| theflowerblossomsthroughwhatseemstobeaconcretesurface | Garbage |
| jacquefrescogiveitjustonesecondheisenbergsuncertaintyprinciple | Garbage |
| Seven-part key (SHA256) | Garbage |

### XOR Combinations (Seven-Token Theory)

Tested XOR of SHA256 hashes:
```
SHA256(matrixsumlist) XOR SHA256(enter) XOR SHA256(lastwordsbeforearchichoice) XOR
SHA256(thispassword) XOR SHA256(matrixsumlist) XOR SHA256(yourlastcommand) XOR SHA256(secondanswer)
= a795de117e472590e572dc193130c763e3fb555ee5db9d34494e156152e50735
```
Result: Garbage

## Technical Variations Tested

### OpenSSL Digest Modes
- `-md md5` (legacy default)
- `-md sha1`
- `-md sha256`
- Default (no -md flag)
- `-pbkdf2` with various iteration counts

All produced garbage output.

### Password Formats
- Raw strings
- SHA256 hashes
- Double-hashed (SHA256 of SHA256)
- With newlines/carriage returns
- With various separators (:, |, _, -, +)
- UPPERCASE, lowercase, MixedCase

## Undecoded Content

### 91 characters before "matrixsumlist"
```
dbbibfbhccbegbihabebeihbeggegebebbgehhebhhfbabfdhbeffcdbbfcccgbfbeeggecbedcibfbffgigbeeeabe
```
- Using a1z26 -> base16 -> ASCII produces: `!8fF�QC...` (garbage)
- May use different encoding or be encrypted

### 601 characters after decoded elements
- Similarly produces garbage with known decoding methods
- May require preceding content to be decrypted first

## Theories to Investigate

1. **Missing Information**: The password may depend on clues not yet discovered
   - Decentraland coordinates (-41, -17) may have additional content
   - The colored letters in SalPhaselon grid may encode something

2. **Non-Standard Encryption**: The blob may not use standard OpenSSL parameters
   - Custom IV derivation
   - Non-standard padding
   - Different encryption library

3. **Multi-Layer Encryption**: As hinted ("16 encryptions, 7 passwords")
   - May need to decrypt multiple layers
   - Passwords may chain together

4. **Timing/Sequential Dependency**
   - SalPhaselon must be solved before Cosmic Duality
   - The README blob might give the password for the Image blob

5. **Color-Based Encoding**
   - Letters in SalPhaselon have different colors
   - Colors may indicate which letters form the password

## Recommended Next Steps

1. **Analyze colored letters** in SalPhaselon grid systematically
2. **Visit Decentraland** at coordinates -41, -17 for additional clues
3. **Check for steganography** in all puzzle images
4. **Monitor Bitcoin forums** for community discoveries
5. **Try alternative encryption libraries** that might have been used
6. **Investigate the exact website content** (our fetches returned limited data)

## Conclusion

After testing 500+ password combinations across multiple encoding methods and OpenSSL configurations, the AES blobs remain undecrypted. The password derivation method is either:
1. Not what the hints suggest
2. Dependent on undiscovered information
3. Using non-standard cryptographic parameters

The critical clue may lie in the colored letters of the SalPhaselon grid or additional hints at Decentraland coordinates.
