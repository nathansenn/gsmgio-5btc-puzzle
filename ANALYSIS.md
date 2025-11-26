# GSMG.IO 5 BTC Puzzle Analysis

This document contains analysis of the puzzle's current state and attempted solutions.

## Puzzle Status

The puzzle remains **UNSOLVED** as of this analysis. The prize has been reduced from 5 BTC to approximately 1.5 BTC after multiple Bitcoin halvings.

**Prize Address**: `1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe`

## Solved Phases Summary

### Phase 1: Binary Matrix
- Decode 14x14 binary matrix (spiral read pattern)
- Result: `gsmg.io/theseedisplanted`

### Phase 2: The Warning
- Password: `theflowerblossomsthroughwhatseemstobeaconcretesurface`
- Redirects to Phase 3

### Phase 3: Causality
- Password: `causality` (The Matrix Reloaded reference)
- SHA256 hash used for AES decryption

### Phase 3.1: Seven-Part Key
1. `causality`
2. `Safenet`
3. `Luna`
4. `HSM`
5. `11110` (Executive Order 11110)
6. `0x736B6E616220...` (Bitcoin genesis block data)
7. Chess FEN notation: `B5KR/1r5B/2R5/2b1p1p1/2P1k1P1/1p2P2p/1P2P2P/3N1N2 b - - 0 1`

Combined and SHA256 hashed for next phase.

### Phase 3.2: Jacque Fresco
- Password: `jacquefrescogiveitjustonesecondheisenbergsuncertaintyprinciple`
- References:
  - Jacque Fresco: "The future is ours"
  - Alice in Wonderland: "How long is forever? Just one second"
  - Heisenberg's uncertainty principle

### Phase 3.2.1: Beaufort Cipher
- Key: `THEMATRIXHASYOU`
- Uses IBM EBCDIC 1141 encoding hint

### Phase 3.2.2: VIC Cipher
- Alphabet: `FUBCDORA.LETHINGKYMVPS.JQZXW`
- Digits 1 and 4
- Decoded message: "IN CASE YOU MANAGE TO CRACK THIS THE PRIVATE KEYS BELONG TO HALF AND BETTER HALF AND THEY ALSO NEED FUNDS TO LIVE"

## SalPhaselon Phase (Partially Solved)

### How to Access
SHA256(`GSMGIO5BTCPUZZLECHALLENGE1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe`) = `89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32`

URL: `gsmg.io/89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32`

### Decoded Elements

#### Binary (abba) Sections
Using `a=0, b=1`:
1. `matrixsumlist` - suggests calculating matrix sum
2. `enter` - possibly indicates newline or submission

#### Number-to-Letter Encoding
Using `a=1, b=2, ... i=9, o=0`, then converting to base 16 (hex) to ASCII:
1. `174161018595377387932283725836301293648834223172419022725145445` → `lastwordsbeforearchichoice`
2. `36026487402470099740341006948` → `thispassword`

#### Text Hints
- `sha b e f our first hint is your last command` - indicates SHA256 encryption, with first hint being the final key
- `shabefanstoo` - possibly "SHA256 answer too" or similar

### Unsolved AES Blob
```
U2FsdGVkX186tYU0hVJBXXUnBUO7C0+X4KUWnWkCvoZSxbRD3wNsGWVHefvdrd9z
QvX0t8v3jPB4okpspxebRi6sE1BMl5HI8Rku+KejUqTvdWOX6nQjSpepXwGuN/jJ
```

This is AES-256-CBC encrypted, base64 encoded, with salt (indicated by `Salted__` prefix when decoded).

## Password Attempts

The following password patterns have been tested without success:

### Matrix-Related
- `theproblemischoice`
- `yourgreatestweakness`
- `hope`, `humphhope`
- `quintessentialhumandelusion`
- `denial`
- `anomaly`, `theone`
- Various Architect quotes

### Puzzle-Related
- `matrixsumlist`, `enter`, `matrixsumlistenter`
- `theseedisplanted`
- `causality`
- Previous phase passwords

### Numeric
- Matrix sum values (422, 100110001001, 2441)
- Various binary/hex conversions

### Other
- Bitcoin-related terms
- Logic (The Warning song)
- Chess-related terms

## Key Observations

1. **"lastwordsbeforearchichoice"** - The password appears to be the Architect's last words before presenting the choice in Matrix Reloaded. However, standard interpretations haven't worked.

2. **"archi"** might not refer to "Architect":
   - Could be a name
   - Could be "architecture"
   - Could be an abbreviation for something else

3. **Matrix sum hint** - "matrixsumlist" suggests calculating some sum from the SalPhaselon letter grid. The grid uses letters a-i representing 1-9.

4. **First hint = last command** - The phrase suggests the solution involves using an early puzzle element as the final key.

## Cosmic Duality Section

A separate AES blob exists in the Cosmic Duality section below SalPhaselon. This may require solving SalPhaselon first, or could be an alternative path.

## Recommendations for Future Solvers

1. **Research the exact Architect dialogue** - The specific wording matters
2. **Explore alternative meanings of "archi"** - May not be "Architect"
3. **Calculate matrix sums** - Try different sum operations on the letter grid
4. **Visit Decentraland** - The coordinates `-41, -17` may have additional clues
5. **Check for steganography** - Images may contain hidden data
6. **Consider multi-step passwords** - May need to combine multiple elements

## Sources
- [puzzlehunt/gsmgio-5btc-puzzle GitHub](https://github.com/puzzlehunt/gsmgio-5btc-puzzle)
- [Private Keys Directory](https://privatekeys.pw/puzzles/gsmg-puzzle)
- [GitHub Issue #6](https://github.com/puzzlehunt/gsmgio-5btc-puzzle/issues/6)
- [GitHub Issue #15](https://github.com/puzzlehunt/gsmgio-5btc-puzzle/issues/15)
