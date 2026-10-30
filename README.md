# Crypto 101: Intro to Cryptography

A two-hour beginner's talk on cryptography, built as a website. The slides and the live demos are the same page: every cipher, hash and key exchange on the slides runs in your browser as you click through.

**Live deck: <https://zevaryx.github.io/crypto-101/>** · made by [zevaryx](https://github.com/zevaryx). You're welcome to present it yourself; see the license below.

The talk covers five parts, with a five-minute discussion checkpoint after each:

1. **Foundations** (25 min): the four goals of cryptography, Caesar and Vigenère ciphers, the one-time pad, the Enigma machine, bits, bytes, hex and Base64, hashing vs encryption vs encoding
2. **Hashing** (20 min): the avalanche effect, SHA-256 round by round, why MD5 and SHA-1 broke, salt and pepper, slow password hashing
3. **Symmetric encryption** (35 min): XOR, AES step by step, modes from ECB to GCM, the ECB padlock picture, tampering and nonce reuse, why keys need good randomness
4. **Asymmetric** (25 min): RSA with small numbers, elliptic curves, key exchange (with paint, then on P-256), digital signatures, passkeys (simulated, plus an optional real one)
5. **The future and wrap-up** (15 min): post-quantum cryptography and lattices, a secure website from start to finish, inspecting a real certificate, end-to-end encryption, takeaways

## Presenting

Open the site on a laptop or projector and it shows one slide at a time. On a phone it switches to a scrolling page.

| Key | Action |
| --- | --- |
| `→` `Space` `PageDown` | Next slide |
| `←` `PageUp` | Previous slide |
| `Home` / `End` | First / last slide |
| `N` | Show or hide the speaker notes |
| `P` | Open the presenter window (notes, next slide, timer, timing plan). It follows the main window. |
| `O` | Overview of all slides |
| `F` | Full screen |
| `Esc` | Close the notes or overview |

Each checkpoint slide has a 5-minute discussion timer. It starts by itself when the slide appears and resets when you leave; click it to pause or resume. The speaker notes are short cues (Say, Show, Ask, Tip, Next) with a time estimate per slide.

The control bar in the bottom-right corner has the same actions, plus **Scroll view** and **PDF** (print, or save as a PDF with one slide per page). Every slide has its own link, for example `#padlock` or `#ecdh`. Three slides are marked skippable in the notes, presenter window and overview, for when you're running long.

The passkeys slide can create a real passkey through your browser (fingerprint, face or PIN); it's saved as "Crypto 101 demo" in your password manager.

The site needs no internet connection once loaded: fonts and libraries are bundled.

## Running it locally

There is no build step. Serve the `docs/` folder with any static web server, for example:

```sh
python3 -m http.server --directory docs 8000
```

Then open <http://localhost:8000>.

## Publishing on GitHub Pages

In the repository's **Settings → Pages**, choose **Deploy from a branch**, then the `main` branch and the `/docs` folder.

## Project layout

```
docs/
  index.html    all slides, with their speaker notes
  styles.css    the theme, slide layout, scroll view and print layout
  deck.js       slide navigation, notes, overview, presenter window
  app.js        the live demos
  crypto.js     the maths: classical ciphers, SHA-256, AES (ECB/CBC/CTR/GCM), RSA, elliptic curves, passkey
                signature checks, toy lattice encryption
  qr.svg        QR code linking to the live deck
  fonts/        bundled fonts (Chakra Petch, JetBrains Mono)
  vendor/       hash-wasm, used to time bcrypt, scrypt and Argon2id
```

`crypto.js` also works in Node (`require("./docs/crypto.js")`), so the maths can be tested outside the browser. The AES and GCM code matches the official FIPS-197 and NIST test vectors.

## Educational use only

The ciphers here are written from scratch so each step can be shown. They are not hardened, constant-time or audited. Never use this code to protect real data; use the Web Crypto API or a vetted library instead.

## Licenses

- The code in this repository is released under the [MIT License](LICENSE).
- [hash-wasm](https://github.com/Daninet/hash-wasm) (`docs/vendor/`) is MIT-licensed by Dani Biró.
- [Chakra Petch](https://github.com/m4rc1e/Chakra-Petch) and [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) (`docs/fonts/`) are under the SIL Open Font License 1.1; see `docs/fonts/OFL-*.txt`.
