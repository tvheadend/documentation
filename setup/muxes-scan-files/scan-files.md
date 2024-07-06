# Scan Files

Scan files are used by TVHeadEnd (TVH) during the setup process to create muxes and scan for services available on those muxes.\
\
An excerpt from a scan file may look like this:

`[CHANNEL]`\
&#x20;     `DELIVERY_SYSTEM = DVBT`\
&#x20;     `FREQUENCY = 226500000`\
&#x20;     `BANDWIDTH_HZ = 7000000`\
&#x20;     `CODE_RATE_HP = AUTO`\
&#x20;     `CODE_RATE_LP = AUTO`\
&#x20;     `MODULATION = QAM/64`\
&#x20;     `TRANSMISSION_MODE = 8K`\
&#x20;     `GUARD_INTERVAL = 1/16`\
&#x20;     `HIERARCHY = NONE`\
&#x20;     `INVERSION = AUTO`

The location of the scan files may vary based upon the TVH version.\
\
`/usr/local/share/tvheadend/data/dvb-scan/`\
`/usr/share/tvheadend/data/dvb-scan/`

Depending on the value of the `DELIVERY_SYSTEM`, TVH recognises the following parameters.

<table data-full-width="true"><thead><tr><th width="338">Parameter</th><th width="101" align="center">DVB-T/2</th><th width="103" align="center">DVB-S/2</th><th width="89" align="center">DVB-C</th><th width="81" align="center">ATSC</th><th width="100" align="center">ISDB-T</th></tr></thead><tbody><tr><td><a href="scan-files.md#delivery_system">DELIVERY_SYSTEM</a></td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td><a href="scan-files.md#frequency">FREQUENCY</a></td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td><a href="scan-files.md#bandwidth_hz">BANDWIDTH_HZ</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td><a href="scan-files.md#code_rate_hp-code_rate_lp-inner_fec">CODE_RATE_HP</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#code_rate_hp-code_rate_lp-inner_fec">CODE_RATE_LP</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#modulation">MODULATION</a></td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center"></td></tr><tr><td><a href="scan-files.md#transmission_mode">TRANSMISSION_MODE</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#guard_interval">GUARD_INTERVAL</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td><a href="scan-files.md#hierarchy">HIERARCHY</a></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#inversion">INVERSION</a></td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td>STREAM_ID</td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#code_rate_hp-code_rate_lp-inner_fec">INNER_FEC</a></td><td align="center"></td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#rolloff">ROLLOFF</a></td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#pilot">PILOT</a></td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#pls_code">PLS_CODE</a></td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td><a href="scan-files.md#polarization">POLARIZATION</a></td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>SYMBOL_RATE</td><td align="center"></td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td></tr><tr><td>ISDBT_LAYERA_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr></tbody></table>

### Accepted values

The following values are accepted for the parameter fields.\
Please note that an 'accepted' value may not always be processed.

### DELIVERY\_SYSTEM

NONE, **DVB-C**, **DVBC/ANNEX\_A**, **DVBC\_ANNEX\_A**, **ATSC-C**, CableCARD, **DVBC/ANNEX\_B**, **DVBC\_ANNEX\_B**, **DVB-C/ANNEX-C**, **DVBC/ANNEX\_C**, **DVBC\_ANNEX\_C**, DVBC\_ANNEX\_AC, **DVB-T**, **DVBT**, **DVB-T2**, **DVBT2**, **DVB-S**, **DVBS**, **DVB-S2**, **DVBS2**, DVB-H, DVBH, **ISDB-T**, **ISDBT**, ISDB-S, ISDBS, ISDB-C, ISDBC, **ATSC-T**, ATSC, ATSCM-H, ATSCMH, DTMB, DMBTH, CMMB, DAB, DSS, TURBO.

### FREQUENCY

Frequency in hertz.

### BANDWIDTH\_HZ

(Bandwidth in hertz)\
1700000, 5000000, 6000000, 7000000, 8000000, 10000000.

### CODE\_RATE\_HP / CODE\_RATE\_LP / INNER\_FEC

1/2, 1/3, 1/4, 1/5, 2/3, 2/5, 2/9, 3/4, 3/5, 4/5, 4/15, 5/6, 5/9, 6/7, 7/8, 7/9, 7/15, 8/9, 8/15, 9/10, 9/20, 11/15, 11/20, 11/45, 13/18, 13/45, 14/45, 23/36, 25/36, 26/45, 28/45, 29/45, 31/45, 32/45, 77/90.

### MODULATION

NONE, AUTO, QPSK, QAM4NR, QAM/AUTO, QAM-AUTO, QAM/16, QAM16, QAM/32, QAM32, QAM/64, QAM64, QAM/128, QAM128, QAM/256, QAM256, QAM/1024, QAM1024, QAM/4096, QAM4096,VSB/8, 8VSB, VSB/16, 16VSB, PSK/8, 8PSK, DQPSK, BPSK, BPSK-S, 16APSK, 32APSK, 64APSK, 128APSK, 256APSK,8APSK-L, 16APSK-L, 32APSK-L, 64APSK-L, 128APSK-L, 256APSK-L.

### TRANSMISSION\_MODE

NONE, AUTO, 1k, 2k, 8k, 4k, 16k, 32k, C1, C3780.

### GUARD\_INTERVAL

NONE, AUTO, 1/4, 1/8, 1/32, 1/16, 1/128, 19/128, 19/256, PN420, PN595, PN945.

### HIERARCHY

NONE, AUTO, 1, 2, 4.

### INVERSION

NONE, AUTO, ON, OFF.

### ROLLOFF

5, 10, 15, 20, 25, 35.

### PILOT

NONE, AUTO, ON, OFF.

### PLS\_CODE

(Physical Layer Scrambling)\
ROOT, GOLD, COMBO.

### POLARIZATION

V, H, L, R, O.

### References

[https://github.com/tvheadend/tvheadend/blob/master/src/input/mpegts/scanfile.c](https://github.com/tvheadend/tvheadend/blob/master/src/input/mpegts/scanfile.c)\
[https://github.com/tvheadend/tvheadend/blob/master/src/input/mpegts/dvb\_support.c](https://github.com/tvheadend/tvheadend/blob/master/src/input/mpegts/dvb\_support.c)\
\
[https://en.wikipedia.org/wiki/DVB](https://en.wikipedia.org/wiki/DVB)\
[https://en.wikipedia.org/wiki/ISDB](https://en.wikipedia.org/wiki/ISDB)\
[https://en.wikipedia.org/wiki/ATSC\_standards](https://en.wikipedia.org/wiki/ATSC\_standards)
