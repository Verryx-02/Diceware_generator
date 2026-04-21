# Diceware_generator

A single-file, offline, zero-dependency HTML generator for strong passphrases.


Tarin Gamberini's Italian Diceware wordlist.

## What is Diceware

Diceware is a method for producing memorable high-entropy passphrases.  
A word is picked at random from a fixed list of 7776 words (one entry per outcome of rolling five six-sided dice).  
A passphrase of *n* Diceware words has exactly `log2(7776) × n ≈ 12.925 × n` bits of entropy, assuming each word is selected uniformly and independently.  

This tool replaces the physical dice with `crypto.getRandomValues()`.

## Features

- **Number of words**: 5 to 8 (default 6)
- **Separator**: any string you like (default `-`)
- **Capitalization**: none / first letter of every word / one random word
- **Optional digit**: append a random digit (0–9) to one random word
- **Live entropy display**: bits of entropy recomputed on every change
- **Bilingual UI** (Italian / English), auto-detected from `navigator.language`.

## Wordlist import

The wordlist is **not** embedded in the HTML. You import it yourself, once, via the file picker on the page.  
It is then cached in your browser's `localStorage` so you don't have to re-import it on subsequent visits.

The imported file must satisfy the following rules:

1. UTF-8 encoded plain text (`.txt`).
2. Contains the two marker lines `BEGIN_word_list_diceware_it-IT` and `END_word_list_diceware_it-IT`, each on its own line.
3. Every non-empty line *between* the markers has the format `NNNNN word` — five digits, whitespace, one word with no internal spaces.
4. Exactly **7776** words between the markers.

## Security notes

- **Randomness**: every random choice: word indices, the position of the capitalized word, the position and value of the appended digit — comes from `crypto.getRandomValues()`.
- **No network requests** at runtime. Everything runs in the browser. The page contains no external fonts, CDNs, analytics, or third-party scripts, and sets `<meta name="referrer" content="no-referrer">`.
- **Persistent storage is limited to the wordlist.** Only the imported wordlist is written to `localStorage`, under the key `diceware-it-wordlist-v4`. No passphrases, no history, and no settings are persisted.

## Wordlist verification

Because you supply the wordlist file yourself, you can verify it directly before importing it. Recommended checks:

- **Inspect the file** in any text editor; it is plain text.
- **Compare the italian list against the original** from Gamberini's website using `sha256sum` on both copies and checking that the digests match. You can find the file [here](https://www.taringamberini.com/)

## How to use

**Locally:** download `diceware.html`, open it in any browser, and import the wordlist file.

On first load you will be asked to import the wordlist. From then on, the browser remembers it until you remove it or clear site data.

## License

The source code of this project is licensed under the [MIT License](LICENSE).

The Italian Diceware wordlist (`wordlist/word_list_diceware_it-IT.txt`) is authored by
[Tarin Gamberini](https://www.taringamberini.com) and is licensed under the
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.html).
The wordlist is redistributed here unmodified, in compliance with its license terms. 
