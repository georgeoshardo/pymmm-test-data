# pymmm-test-data

Small real acquisitions that [PyMMM](https://github.com/georgeoshardo/PyMMM)'s tests run on.

## 20261005_pbs_psc_yfp_ty013_small.nd2.xz

A piece of a 40x mother-machine time-lapse taken on 5 October 2026: E. coli SB7, SB7 +
pSC101 and SB7 + pBSII in three lanes of one chip, with phage added at frame 22.

| | |
|---|---|
| Shape (T, P, C, Y, X) | 21 × 3 × 2 × 832 × 768, uint16 |
| Positions | 2, 16 and 30 of the original, one per lane (here `XYPos:0` to `XYPos:2`) |
| Frames | 20 to 40 of the original, one minute apart |
| Channels | PC, mCherry |
| Pixel size | 0.1079 µm |
| Size | 161 MB as ND2, 95.5 MB compressed |

The original is 361 frames × 35 positions × 4 channels of 1560 × 2304 pixels (363 GB).
The piece was cut from it with PyMMM's `tests/golden/subset_nd2.py`:

```
python subset_nd2.py 20261005_pbs_psc_yfp_ty013.nd2 20261005_pbs_psc_yfp_ty013_small.nd2 \
    --positions 2 16 30 --times 20 41 --channels 0 1 --y 232 1064 --x 0 768
xz -9 20261005_pbs_psc_yfp_ty013_small.nd2
```

The script copies the original's chunks and changes only the counts, image size and
channel list. The `nd2` package reads every pixel, stage position, focus offset and
frame time of the result exactly as it reads the same part of the original. Nikon's
software has not been tried on it. The file's text description still gives the
original's dimensions.

`SHA256SUMS` holds the checksums of the compressed file and of the ND2 inside it.
