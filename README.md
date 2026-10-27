# RSV Restore

Recover interrupted Sony recordings with a simple Vietnamese/English interface.

- Choose an RSV or interrupted MP4/MOV recording; a reference clip is requested only after recovery needs more information.
- Preview recoverable footage and save a new MP4.
- Vietnamese by default for Vietnam browser time zones; English elsewhere. Manual language selection is remembered.
- Coffee support via Vietcombank QR / PayPal, and [Huy Vector Lab on YouTube](https://www.youtube.com/@huyvectorlab).
- Contact: huyvectorskda@gmail.com. If recovery fails, share Google Drive links to a small damaged-file sample and a matching healthy reference clip.

## Running

Open `index.html` from this repository, or use its GitHub Pages link. `rsv-restore-source.zip` contains the editable source and tests. Extract it, then serve `dist/` using any static HTTP server. Run `node build-standalone.mjs` to regenerate the standalone HTML. Node.js and FFmpeg with libx264/libx265 are needed for `npm test`.

## Large recordings and limits

The file selector has no upload-size cap. Chrome/Edge on desktop can write directly to a selected destination in chunks of at most 32 MiB; source offsets use 64-bit MP4 tables. Ensure the destination has enough free space. Read/write MB/s measures completed I/O during processing, not a network upload. When using a browser-managed Blob download, download-to-disk speed is unavailable.

A virtual 256 GiB stream test verifies byte totals, bounded writes and cancellation. It does not establish successful recovery of a real 256 GiB camera recording. Actual compatibility depends on file layout, available memory for frame indexing, browser support and disk space. Current limits include a 256 MiB GOP and 3 million frames per session. Browsers without direct file saving use a 512 MiB Blob fallback; large recordings require desktop Chrome/Edge.

Supported paths cover selected Sony rtmd layouts with AVC/HEVC, progressive video, AUD framing and PCM audio. Embedded configuration is used where found; some files still require a donor with matching camera settings. Unsupported paths include MXF/X-OCN, AAC, interlaced AVC, POC type 1, and arbitrary damage inside a recording. Always check recovered picture and sound.

## Verification

Synthetic AVC/HEVC tests compare decoded frame hashes, timestamps and PCM. Tests cover 10-bit 4:2:2, 50/59.94 fps, all-intra, multi-slice AVC, four mono 24-bit PCM tracks with a donor, late codec parameters, interrupted tails, errors and cancellation. UI checks cover language selection, reference fallback, contact and support controls. Camera files used for private verification are not included in this repository.

Version 0.5.0 · Huy Vector
