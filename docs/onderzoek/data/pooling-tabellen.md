<!-- Gegenereerd door tools/verwerk_pooling.py; niet met de hand aanpassen. -->

Aantal herhalingen per meetpunt: 6. Alle waarden zijn het gemiddelde over de herhalingen.

### Kogels, patroon gelijkmatig

**Gemiddelde frametijd en pieken (ms, lager is beter)**

| Aantal | Gem. zonder | Gem. met | Verschil | p99 zonder | p99 met | Max zonder | Max met |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 50 | 0.663 | 0.680 | +3% | 1.289 | 1.370 | 2.494 | 4.291 |
| 100 | 0.792 | 0.820 | +4% | 1.431 | 1.389 | 42.026 | 3.712 |
| 200 | 0.860 | 1.037 | +21% | 1.412 | 1.990 | 4.517 | 5.981 |
| 500 | 2.072 | 1.366 | -34% | 2.803 | 2.150 | 9.502 | 10.823 |
| 1000 | 2.686 | 2.119 | -21% | 3.869 | 3.930 | 12.372 | 13.747 |

**Framerate en spreiding tussen de herhalingen**

| Aantal | FPS zonder | FPS met | Gem. frametijd zonder (min-max) | Gem. frametijd met (min-max) |
|---:|---:|---:|---|---|
| 50 | 1512 | 1473 | 0.620 - 0.688 | 0.655 - 0.729 |
| 100 | 1264 | 1221 | 0.764 - 0.827 | 0.769 - 0.854 |
| 200 | 1171 | 970 | 0.784 - 0.983 | 0.964 - 1.192 |
| 500 | 790 | 736 | 0.965 - 6.901 | 1.217 - 1.544 |
| 1000 | 483 | 482 | 1.621 - 6.900 | 1.639 - 2.403 |

**Kosten per frame (ms) en geheugen**

| Aantal | Process zonder | Process met | Physics zonder | Physics met | Aanmaken/opruimen zonder | Aanmaken/opruimen met | Nodes zonder | Nodes met | Geheugen zonder (MB) | Geheugen met (MB) |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 50 | 2.019 | 2.316 | 0.263 | 0.258 | 0.0044 | 0.0033 | 178 | 226 | 0.0 | 0.0 |
| 100 | 2.388 | 2.224 | 0.546 | 0.437 | 0.0077 | 0.0050 | 328 | 391 | 0.0 | 0.0 |
| 200 | 3.448 | 5.878 | 0.857 | 0.804 | 0.0134 | 0.0086 | 628 | 721 | 0.0 | 0.0 |
| 500 | 3.420 | 6.013 | 1.758 | 1.642 | 0.0487 | 0.0189 | 1530 | 1711 | 0.0 | 0.0 |
| 1000 | 3.912 | 5.434 | 3.262 | 3.317 | 0.0968 | 0.0427 | 3028 | 3361 | 0.0 | 0.0 |

**Aantal keer dat er echt een object is aangemaakt tijdens de meting**

| Aantal | Nieuw aangemaakt zonder | Nieuw aangemaakt met | Hergebruikt met |
|---:|---:|---:|---:|
| 50 | 736 | 0 | 736 |
| 100 | 1484 | 0 | 1485 |
| 200 | 2985 | 0 | 2985 |
| 500 | 7484 | 0 | 7480 |
| 1000 | 14956 | 0 | 14962 |

### Vijanden, patroon gelijkmatig

**Gemiddelde frametijd en pieken (ms, lager is beter)**

| Aantal | Gem. zonder | Gem. met | Verschil | p99 zonder | p99 met | Max zonder | Max met |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 50 | 0.802 | 0.761 | -5% | 1.670 | 1.389 | 20.852 | 3.530 |
| 100 | 1.013 | 0.860 | -15% | 1.936 | 1.389 | 7.395 | 48.036 |
| 200 | 1.090 | 1.473 | +35% | 1.786 | 2.407 | 7.353 | 7.415 |
| 500 | 1.970 | 2.227 | +13% | 2.251 | 3.549 | 11.405 | 17.381 |
| 1000 | 5.734 | 7.804 | +36% | 8.715 | 13.679 | 15.050 | 28.704 |

**Framerate en spreiding tussen de herhalingen**

| Aantal | FPS zonder | FPS met | Gem. frametijd zonder (min-max) | Gem. frametijd met (min-max) |
|---:|---:|---:|---|---|
| 50 | 1250 | 1322 | 0.774 - 0.851 | 0.712 - 0.846 |
| 100 | 1019 | 1174 | 0.854 - 1.278 | 0.770 - 0.970 |
| 200 | 918 | 767 | 1.074 - 1.118 | 1.044 - 2.264 |
| 500 | 508 | 452 | 1.882 - 2.076 | 1.996 - 2.375 |
| 1000 | 175 | 129 | 5.476 - 5.962 | 7.162 - 8.339 |

**Kosten per frame (ms) en geheugen**

| Aantal | Process zonder | Process met | Physics zonder | Physics met | Aanmaken/opruimen zonder | Aanmaken/opruimen met | Nodes zonder | Nodes met | Geheugen zonder (MB) | Geheugen met (MB) |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 50 | 3.202 | 2.581 | 0.574 | 0.548 | 0.0057 | 0.0047 | 178 | 226 | 0.0 | 0.0 |
| 100 | 3.200 | 2.462 | 0.942 | 0.844 | 0.0108 | 0.0068 | 328 | 391 | 0.0 | 0.0 |
| 200 | 2.711 | 3.118 | 1.430 | 2.092 | 0.0175 | 0.0200 | 629 | 721 | 0.0 | 0.0 |
| 500 | 2.950 | 3.422 | 3.610 | 4.727 | 0.0548 | 0.0434 | 1530 | 1711 | 0.0 | 0.0 |
| 1000 | 5.207 | 4.877 | 9.045 | 11.871 | 0.1767 | 0.1262 | 3033 | 3361 | 0.0 | 0.0 |

**Aantal keer dat er echt een object is aangemaakt tijdens de meting**

| Aantal | Nieuw aangemaakt zonder | Nieuw aangemaakt met | Hergebruikt met |
|---:|---:|---:|---:|
| 50 | 736 | 0 | 736 |
| 100 | 1485 | 0 | 1483 |
| 200 | 2985 | 0 | 2985 |
| 500 | 7483 | 0 | 7479 |
| 1000 | 14946 | 0 | 14934 |

### Kogels, patroon golven

**Gemiddelde frametijd en pieken (ms, lager is beter)**

| Aantal | Gem. zonder | Gem. met | Verschil | p99 zonder | p99 met | Max zonder | Max met |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 200 | 0.761 | 0.713 | -6% | 1.958 | 1.389 | 7.131 | 4.394 |
| 1000 | 1.195 | 1.167 | -2% | 2.315 | 2.300 | 40.977 | 14.109 |

**Framerate en spreiding tussen de herhalingen**

| Aantal | FPS zonder | FPS met | Gem. frametijd zonder (min-max) | Gem. frametijd met (min-max) |
|---:|---:|---:|---|---|
| 200 | 1342 | 1408 | 0.638 - 0.909 | 0.653 - 0.743 |
| 1000 | 861 | 884 | 1.016 - 1.490 | 0.964 - 1.459 |

**Kosten per frame (ms) en geheugen**

| Aantal | Process zonder | Process met | Physics zonder | Physics met | Aanmaken/opruimen zonder | Aanmaken/opruimen met | Nodes zonder | Nodes met | Geheugen zonder (MB) | Geheugen met (MB) |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 200 | 7.953 | 3.720 | 0.805 | 0.826 | 0.0035 | 0.0025 | 631 | 721 | 0.0 | 0.0 |
| 1000 | 20.156 | 9.111 | 3.352 | 3.390 | 0.0144 | 0.0064 | 3033 | 3361 | 0.0 | 0.0 |

**Aantal keer dat er echt een object is aangemaakt tijdens de meting**

| Aantal | Nieuw aangemaakt zonder | Nieuw aangemaakt met | Hergebruikt met |
|---:|---:|---:|---:|
| 200 | 3000 | 0 | 3000 |
| 1000 | 15000 | 0 | 15000 |

### Vijanden, patroon golven

**Gemiddelde frametijd en pieken (ms, lager is beter)**

| Aantal | Gem. zonder | Gem. met | Verschil | p99 zonder | p99 met | Max zonder | Max met |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 200 | 1.241 | 1.136 | -8% | 1.988 | 1.745 | 11.418 | 12.907 |
| 1000 | 5.237 | 7.328 | +40% | 14.729 | 17.661 | 52.584 | 37.615 |

**Framerate en spreiding tussen de herhalingen**

| Aantal | FPS zonder | FPS met | Gem. frametijd zonder (min-max) | Gem. frametijd met (min-max) |
|---:|---:|---:|---|---|
| 200 | 807 | 881 | 1.207 - 1.302 | 1.108 - 1.182 |
| 1000 | 191 | 137 | 5.109 - 5.370 | 7.169 - 7.577 |

**Kosten per frame (ms) en geheugen**

| Aantal | Process zonder | Process met | Physics zonder | Physics met | Aanmaken/opruimen zonder | Aanmaken/opruimen met | Nodes zonder | Nodes met | Geheugen zonder (MB) | Geheugen met (MB) |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 200 | 7.597 | 5.171 | 1.878 | 1.861 | 0.0052 | 0.0038 | 631 | 721 | 0.0 | 0.0 |
| 1000 | 19.951 | 12.789 | 11.795 | 14.217 | 0.0616 | 0.0457 | 3039 | 3361 | 0.0 | 0.0 |

**Aantal keer dat er echt een object is aangemaakt tijdens de meting**

| Aantal | Nieuw aangemaakt zonder | Nieuw aangemaakt met | Hergebruikt met |
|---:|---:|---:|---:|
| 200 | 3000 | 0 | 3000 |
| 1000 | 15000 | 0 | 15000 |

