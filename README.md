# This is the repo for experiments/tests I did.
- Cyano tree: I was playing around with the Sourmash matix script.
- ref: https://hackmd.io/9ORFRJGaTOiOdEAY-Aih2A?view#Genome-distance-matrix-dendrograms-and-ordination
  1) finding the GCF# in NCBI with 7 species' name
  2) grep the .sig file from ctbrowngrp gtdb .sig folder
     e.g.: `sourmash sig grep GCF_000009725.1 /group/ctbrowngrp/sourmash-db/gtdb-rs220/gtdb-rs220-k31.zip -o GCF_000009725.1.sig.zip -k 31`
  3) apply loop for remaining species:
```
for GCF in $(cat ../list); do
    sourmash sig grep "$GCF" /group/ctbrowngrp/sourmash-db/gtdb-rs220/gtdb-rs220-k31.zip \
        -o "${GCF}.sig.zip" -k 31
done
```
  5) combine all .sig files in one:
     `sourmash sig cat *.sig.zip -o 7sketches.sig.zip`
  6) Sourmash compare:
     `sourmash compare ../sig/7sketches.sig.zip -o 7sketches.cmp --labels-to 7sketches.labels_to.csv`
  7) generate tree:
     `sourmash scripts plot2 7sketches.cmp 7sketches.labels_to.csv -o 7sketches.mat.png`
 ![Screenshot 2024-11-05 at 13 37 26](https://github.com/user-attachments/assets/5fbbf089-0287-4ff0-bd72-c4e67097afed)

