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

<table><thead><tr><th width="338">Parameter</th><th align="center">DVB-T/2</th><th align="center">DVB-S/2</th><th align="center">DVB-C</th><th align="center">ATSC</th><th align="center">ISDB-T</th></tr></thead><tbody><tr><td>DELIVERY_SYSTEM</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td>FREQUENCY</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td>BANDWIDTH_HZ</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>CODE_RATE_HP</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>CODE_RATE_LP</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>MODULATION</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center"></td></tr><tr><td>TRANSMISSION_MODE</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>GUARD_INTERVAL</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>HIERARCHY</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>INVERSION</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td><td align="center">✓</td></tr><tr><td>STREAM_ID</td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>INNER_FEC</td><td align="center"></td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td></tr><tr><td>ROLLOFF</td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>PILOT</td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>PLS_CODE</td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>POLARIZATION</td><td align="center"></td><td align="center">✓</td><td align="center"></td><td align="center"></td><td align="center"></td></tr><tr><td>SYMBOL_RATE</td><td align="center"></td><td align="center">✓</td><td align="center">✓</td><td align="center"></td><td align="center"></td></tr><tr><td>ISDBT_LAYERA_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_FEC</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_MODULATION</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_SEGMENT_COUNT</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERA_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERB_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr><tr><td>ISDBT_LAYERC_TIME_INTERLEAVING</td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center"></td><td align="center">✓</td></tr></tbody></table>

**TODO** - Section detailing the recognised values for each parameter.

### Accepted values

The following values are accepted for the parameter fields.\
Please note that an 'accepted' value may not always be processed.

### DELIVERY\_SYSTEM

NONE, **DVB-C**, **DVBC/ANNEX\_A**, **DVBC\_ANNEX\_A**, **ATSC-C**, CableCARD, **DVBC/ANNEX\_B**, **DVBC\_ANNEX\_B**, **DVB-C/ANNEX-C**, **DVBC/ANNEX\_C**, **DVBC\_ANNEX\_C**, DVBC\_ANNEX\_AC, **DVB-T**, **DVBT**, **DVB-T2**, **DVBT2**, **DVB-S**, **DVBS**, **DVB-S2**, **DVBS2**, DVB-H, DVBH, **ISDB-T**, **ISDBT**, ISDB-S, ISDBS, ISDB-C, ISDBC, **ATSC-T**, ATSC, ATSCM-H, ATSCMH, DTMB, DMBTH, CMMB, DAB, DSS, TURBO.

### FREQUENCY

Frequency in hertz.
