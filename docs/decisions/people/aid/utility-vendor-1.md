# Utility vendor — part 1 of 2

[Policy and other cases](README.md)

One approved award of 350.00 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-00001 | 0.00 | 0.00 | 0.00 | Request new 115.50 | Reserve once | 0.00 | 115.50 | 234.50 |
| AID-00002 | 0.00 | 0.00 | 0.00 | Request new 349.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00003 | 0.00 | 0.00 | 0.00 | Request new 350.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00004 | 0.00 | 0.00 | 0.00 | Request new 350.01 | Exceeds remaining authority | 0.00 | 0.00 | 350.00 |
| AID-00005 | 0.00 | 0.00 | 140.00 | Request new 115.50 | Reserve once | 0.00 | 255.50 | 94.50 |
| AID-00006 | 0.00 | 0.00 | 140.00 | Request new 209.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00007 | 0.00 | 0.00 | 140.00 | Request new 210.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00008 | 0.00 | 0.00 | 140.00 | Request new 210.01 | Exceeds remaining authority | 0.00 | 140.00 | 210.00 |
| AID-00009 | 0.00 | 0.00 | 140.00 | Confirm pending 140.00 | Settle original once | 140.00 | 0.00 | 210.00 |
| AID-00010 | 0.00 | 0.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00011 | 0.00 | 0.00 | 350.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00012 | 0.00 | 0.00 | 350.00 | Request new 115.50 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00013 | 0.00 | 0.00 | 350.00 | Confirm pending 350.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00014 | 0.00 | 0.00 | 350.00 | Fail pending 350.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00015 | 70.00 | 0.00 | 0.00 | Request new 115.50 | Reserve once | 70.00 | 115.50 | 164.50 |
| AID-00016 | 70.00 | 0.00 | 0.00 | Request new 279.99 | Reserve once | 70.00 | 279.99 | 0.01 |
| AID-00017 | 70.00 | 0.00 | 0.00 | Request new 280.00 | Reserve once | 70.00 | 280.00 | 0.00 |
| AID-00018 | 70.00 | 0.00 | 0.00 | Request new 280.01 | Exceeds remaining authority | 70.00 | 0.00 | 280.00 |
| AID-00019 | 70.00 | 0.00 | 0.00 | Replay settled 70.00 | Original receipt; no new effect | 70.00 | 0.00 | 280.00 |
| AID-00020 | 70.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 69.99 | 0.00 | 280.01 |
| AID-00021 | 70.00 | 0.00 | 0.00 | Record return 35.00 | Apply linked return once | 35.00 | 0.00 | 315.00 |
| AID-00022 | 70.00 | 0.00 | 0.00 | Record return 70.00 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00023 | 70.00 | 0.00 | 0.00 | Record return 70.01 | Return exceeds net fulfillment | 70.00 | 0.00 | 280.00 |
| AID-00024 | 70.00 | 0.00 | 112.00 | Request new 115.50 | Reserve once | 70.00 | 227.50 | 52.50 |
| AID-00025 | 70.00 | 0.00 | 112.00 | Request new 167.99 | Reserve once | 70.00 | 279.99 | 0.01 |
| AID-00026 | 70.00 | 0.00 | 112.00 | Request new 168.00 | Reserve once | 70.00 | 280.00 | 0.00 |
| AID-00027 | 70.00 | 0.00 | 112.00 | Request new 168.01 | Exceeds remaining authority | 70.00 | 112.00 | 168.00 |
| AID-00028 | 70.00 | 0.00 | 112.00 | Confirm pending 112.00 | Settle original once | 182.00 | 0.00 | 168.00 |
| AID-00029 | 70.00 | 0.00 | 112.00 | Fail pending 112.00 | Release pending reservation | 70.00 | 0.00 | 280.00 |
| AID-00030 | 70.00 | 0.00 | 112.00 | Replay settled 70.00 | Original receipt; no new effect | 70.00 | 112.00 | 168.00 |
| AID-00031 | 70.00 | 0.00 | 112.00 | Record return 0.01 | Apply linked return once | 69.99 | 112.00 | 168.01 |
| AID-00032 | 70.00 | 0.00 | 112.00 | Record return 35.00 | Apply linked return once | 35.00 | 112.00 | 203.00 |
| AID-00033 | 70.00 | 0.00 | 112.00 | Record return 70.00 | Apply linked return once | 0.00 | 112.00 | 238.00 |
| AID-00034 | 70.00 | 0.00 | 112.00 | Record return 70.01 | Return exceeds net fulfillment | 70.00 | 112.00 | 168.00 |
| AID-00035 | 70.00 | 0.00 | 280.00 | Request new 0.01 | Exceeds remaining authority | 70.00 | 280.00 | 0.00 |
| AID-00036 | 70.00 | 0.00 | 280.00 | Request new 115.50 | Exceeds remaining authority | 70.00 | 280.00 | 0.00 |
| AID-00037 | 70.00 | 0.00 | 280.00 | Confirm pending 280.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00038 | 70.00 | 0.00 | 280.00 | Fail pending 280.00 | Release pending reservation | 70.00 | 0.00 | 280.00 |
| AID-00039 | 70.00 | 0.00 | 280.00 | Replay settled 70.00 | Original receipt; no new effect | 70.00 | 280.00 | 0.00 |
| AID-00040 | 70.00 | 0.00 | 280.00 | Record return 0.01 | Apply linked return once | 69.99 | 280.00 | 0.01 |
| AID-00041 | 70.00 | 0.00 | 280.00 | Record return 35.00 | Apply linked return once | 35.00 | 280.00 | 35.00 |
| AID-00042 | 70.00 | 0.00 | 280.00 | Record return 70.00 | Apply linked return once | 0.00 | 280.00 | 70.00 |
| AID-00043 | 70.00 | 0.00 | 280.00 | Record return 70.01 | Return exceeds net fulfillment | 70.00 | 280.00 | 0.00 |
| AID-00044 | 70.00 | 0.01 | 0.00 | Request new 115.50 | Reserve once | 69.99 | 115.50 | 164.51 |
| AID-00045 | 70.00 | 0.01 | 0.00 | Request new 280.00 | Reserve once | 69.99 | 280.00 | 0.01 |
| AID-00046 | 70.00 | 0.01 | 0.00 | Request new 280.01 | Reserve once | 69.99 | 280.01 | 0.00 |
| AID-00047 | 70.00 | 0.01 | 0.00 | Request new 280.02 | Exceeds remaining authority | 69.99 | 0.00 | 280.01 |
| AID-00048 | 70.00 | 0.01 | 0.00 | Replay settled 70.00 | Original receipt; no new effect | 69.99 | 0.00 | 280.01 |
| AID-00049 | 70.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 69.98 | 0.00 | 280.02 |
| AID-00050 | 70.00 | 0.01 | 0.00 | Record return 35.00 | Apply linked return once | 34.99 | 0.00 | 315.01 |
| AID-00051 | 70.00 | 0.01 | 0.00 | Record return 69.99 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00052 | 70.00 | 0.01 | 0.00 | Record return 70.00 | Return exceeds net fulfillment | 69.99 | 0.00 | 280.01 |
| AID-00053 | 70.00 | 0.01 | 112.00 | Request new 115.50 | Reserve once | 69.99 | 227.50 | 52.51 |
| AID-00054 | 70.00 | 0.01 | 112.00 | Request new 168.00 | Reserve once | 69.99 | 280.00 | 0.01 |
| AID-00055 | 70.00 | 0.01 | 112.00 | Request new 168.01 | Reserve once | 69.99 | 280.01 | 0.00 |
| AID-00056 | 70.00 | 0.01 | 112.00 | Request new 168.02 | Exceeds remaining authority | 69.99 | 112.00 | 168.01 |
| AID-00057 | 70.00 | 0.01 | 112.00 | Confirm pending 112.00 | Settle original once | 181.99 | 0.00 | 168.01 |
| AID-00058 | 70.00 | 0.01 | 112.00 | Fail pending 112.00 | Release pending reservation | 69.99 | 0.00 | 280.01 |
| AID-00059 | 70.00 | 0.01 | 112.00 | Replay settled 70.00 | Original receipt; no new effect | 69.99 | 112.00 | 168.01 |
| AID-00060 | 70.00 | 0.01 | 112.00 | Record return 0.01 | Apply linked return once | 69.98 | 112.00 | 168.02 |
| AID-00061 | 70.00 | 0.01 | 112.00 | Record return 35.00 | Apply linked return once | 34.99 | 112.00 | 203.01 |
| AID-00062 | 70.00 | 0.01 | 112.00 | Record return 69.99 | Apply linked return once | 0.00 | 112.00 | 238.00 |
| AID-00063 | 70.00 | 0.01 | 112.00 | Record return 70.00 | Return exceeds net fulfillment | 69.99 | 112.00 | 168.01 |
| AID-00064 | 70.00 | 0.01 | 280.01 | Request new 0.01 | Exceeds remaining authority | 69.99 | 280.01 | 0.00 |
| AID-00065 | 70.00 | 0.01 | 280.01 | Request new 115.50 | Exceeds remaining authority | 69.99 | 280.01 | 0.00 |
| AID-00066 | 70.00 | 0.01 | 280.01 | Confirm pending 280.01 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00067 | 70.00 | 0.01 | 280.01 | Fail pending 280.01 | Release pending reservation | 69.99 | 0.00 | 280.01 |
| AID-00068 | 70.00 | 0.01 | 280.01 | Replay settled 70.00 | Original receipt; no new effect | 69.99 | 280.01 | 0.00 |
| AID-00069 | 70.00 | 0.01 | 280.01 | Record return 0.01 | Apply linked return once | 69.98 | 280.01 | 0.01 |
| AID-00070 | 70.00 | 0.01 | 280.01 | Record return 35.00 | Apply linked return once | 34.99 | 280.01 | 35.00 |
| AID-00071 | 70.00 | 0.01 | 280.01 | Record return 69.99 | Apply linked return once | 0.00 | 280.01 | 69.99 |
| AID-00072 | 70.00 | 0.01 | 280.01 | Record return 70.00 | Return exceeds net fulfillment | 69.99 | 280.01 | 0.00 |
| AID-00073 | 70.00 | 17.50 | 0.00 | Request new 115.50 | Reserve once | 52.50 | 115.50 | 182.00 |
| AID-00074 | 70.00 | 17.50 | 0.00 | Request new 297.49 | Reserve once | 52.50 | 297.49 | 0.01 |
| AID-00075 | 70.00 | 17.50 | 0.00 | Request new 297.50 | Reserve once | 52.50 | 297.50 | 0.00 |
| AID-00076 | 70.00 | 17.50 | 0.00 | Request new 297.51 | Exceeds remaining authority | 52.50 | 0.00 | 297.50 |
| AID-00077 | 70.00 | 17.50 | 0.00 | Replay settled 70.00 | Original receipt; no new effect | 52.50 | 0.00 | 297.50 |
| AID-00078 | 70.00 | 17.50 | 0.00 | Record return 0.01 | Apply linked return once | 52.49 | 0.00 | 297.51 |
| AID-00079 | 70.00 | 17.50 | 0.00 | Record return 26.25 | Apply linked return once | 26.25 | 0.00 | 323.75 |
| AID-00080 | 70.00 | 17.50 | 0.00 | Record return 52.50 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00081 | 70.00 | 17.50 | 0.00 | Record return 52.51 | Return exceeds net fulfillment | 52.50 | 0.00 | 297.50 |
| AID-00082 | 70.00 | 17.50 | 119.00 | Request new 115.50 | Reserve once | 52.50 | 234.50 | 63.00 |
| AID-00083 | 70.00 | 17.50 | 119.00 | Request new 178.49 | Reserve once | 52.50 | 297.49 | 0.01 |
| AID-00084 | 70.00 | 17.50 | 119.00 | Request new 178.50 | Reserve once | 52.50 | 297.50 | 0.00 |
| AID-00085 | 70.00 | 17.50 | 119.00 | Request new 178.51 | Exceeds remaining authority | 52.50 | 119.00 | 178.50 |
| AID-00086 | 70.00 | 17.50 | 119.00 | Confirm pending 119.00 | Settle original once | 171.50 | 0.00 | 178.50 |
| AID-00087 | 70.00 | 17.50 | 119.00 | Fail pending 119.00 | Release pending reservation | 52.50 | 0.00 | 297.50 |
| AID-00088 | 70.00 | 17.50 | 119.00 | Replay settled 70.00 | Original receipt; no new effect | 52.50 | 119.00 | 178.50 |
| AID-00089 | 70.00 | 17.50 | 119.00 | Record return 0.01 | Apply linked return once | 52.49 | 119.00 | 178.51 |
| AID-00090 | 70.00 | 17.50 | 119.00 | Record return 26.25 | Apply linked return once | 26.25 | 119.00 | 204.75 |
| AID-00091 | 70.00 | 17.50 | 119.00 | Record return 52.50 | Apply linked return once | 0.00 | 119.00 | 231.00 |
| AID-00092 | 70.00 | 17.50 | 119.00 | Record return 52.51 | Return exceeds net fulfillment | 52.50 | 119.00 | 178.50 |
| AID-00093 | 70.00 | 17.50 | 297.50 | Request new 0.01 | Exceeds remaining authority | 52.50 | 297.50 | 0.00 |
| AID-00094 | 70.00 | 17.50 | 297.50 | Request new 115.50 | Exceeds remaining authority | 52.50 | 297.50 | 0.00 |
| AID-00095 | 70.00 | 17.50 | 297.50 | Confirm pending 297.50 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00096 | 70.00 | 17.50 | 297.50 | Fail pending 297.50 | Release pending reservation | 52.50 | 0.00 | 297.50 |
| AID-00097 | 70.00 | 17.50 | 297.50 | Replay settled 70.00 | Original receipt; no new effect | 52.50 | 297.50 | 0.00 |
| AID-00098 | 70.00 | 17.50 | 297.50 | Record return 0.01 | Apply linked return once | 52.49 | 297.50 | 0.01 |
| AID-00099 | 70.00 | 17.50 | 297.50 | Record return 26.25 | Apply linked return once | 26.25 | 297.50 | 26.25 |
| AID-00100 | 70.00 | 17.50 | 297.50 | Record return 52.50 | Apply linked return once | 0.00 | 297.50 | 52.50 |
| AID-00101 | 70.00 | 17.50 | 297.50 | Record return 52.51 | Return exceeds net fulfillment | 52.50 | 297.50 | 0.00 |
| AID-00102 | 70.00 | 70.00 | 0.00 | Request new 115.50 | Reserve once | 0.00 | 115.50 | 234.50 |
| AID-00103 | 70.00 | 70.00 | 0.00 | Request new 349.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00104 | 70.00 | 70.00 | 0.00 | Request new 350.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00105 | 70.00 | 70.00 | 0.00 | Request new 350.01 | Exceeds remaining authority | 0.00 | 0.00 | 350.00 |
| AID-00106 | 70.00 | 70.00 | 0.00 | Replay settled 70.00 | Original receipt; no new effect | 0.00 | 0.00 | 350.00 |
| AID-00107 | 70.00 | 70.00 | 140.00 | Request new 115.50 | Reserve once | 0.00 | 255.50 | 94.50 |
| AID-00108 | 70.00 | 70.00 | 140.00 | Request new 209.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00109 | 70.00 | 70.00 | 140.00 | Request new 210.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00110 | 70.00 | 70.00 | 140.00 | Request new 210.01 | Exceeds remaining authority | 0.00 | 140.00 | 210.00 |
| AID-00111 | 70.00 | 70.00 | 140.00 | Confirm pending 140.00 | Settle original once | 140.00 | 0.00 | 210.00 |
| AID-00112 | 70.00 | 70.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00113 | 70.00 | 70.00 | 140.00 | Replay settled 70.00 | Original receipt; no new effect | 0.00 | 140.00 | 210.00 |
| AID-00114 | 70.00 | 70.00 | 350.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00115 | 70.00 | 70.00 | 350.00 | Request new 115.50 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00116 | 70.00 | 70.00 | 350.00 | Confirm pending 350.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00117 | 70.00 | 70.00 | 350.00 | Fail pending 350.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00118 | 70.00 | 70.00 | 350.00 | Replay settled 70.00 | Original receipt; no new effect | 0.00 | 350.00 | 0.00 |
| AID-00119 | 175.00 | 0.00 | 0.00 | Request new 115.50 | Reserve once | 175.00 | 115.50 | 59.50 |
| AID-00120 | 175.00 | 0.00 | 0.00 | Request new 174.99 | Reserve once | 175.00 | 174.99 | 0.01 |
| AID-00121 | 175.00 | 0.00 | 0.00 | Request new 175.00 | Reserve once | 175.00 | 175.00 | 0.00 |
| AID-00122 | 175.00 | 0.00 | 0.00 | Request new 175.01 | Exceeds remaining authority | 175.00 | 0.00 | 175.00 |
| AID-00123 | 175.00 | 0.00 | 0.00 | Replay settled 175.00 | Original receipt; no new effect | 175.00 | 0.00 | 175.00 |
| AID-00124 | 175.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 174.99 | 0.00 | 175.01 |
| AID-00125 | 175.00 | 0.00 | 0.00 | Record return 87.50 | Apply linked return once | 87.50 | 0.00 | 262.50 |
| AID-00126 | 175.00 | 0.00 | 0.00 | Record return 175.00 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00127 | 175.00 | 0.00 | 0.00 | Record return 175.01 | Return exceeds net fulfillment | 175.00 | 0.00 | 175.00 |
| AID-00128 | 175.00 | 0.00 | 70.00 | Request new 104.99 | Reserve once | 175.00 | 174.99 | 0.01 |
| AID-00129 | 175.00 | 0.00 | 70.00 | Request new 105.00 | Reserve once | 175.00 | 175.00 | 0.00 |
| AID-00130 | 175.00 | 0.00 | 70.00 | Request new 105.01 | Exceeds remaining authority | 175.00 | 70.00 | 105.00 |
| AID-00131 | 175.00 | 0.00 | 70.00 | Request new 115.50 | Exceeds remaining authority | 175.00 | 70.00 | 105.00 |
| AID-00132 | 175.00 | 0.00 | 70.00 | Confirm pending 70.00 | Settle original once | 245.00 | 0.00 | 105.00 |
| AID-00133 | 175.00 | 0.00 | 70.00 | Fail pending 70.00 | Release pending reservation | 175.00 | 0.00 | 175.00 |
| AID-00134 | 175.00 | 0.00 | 70.00 | Replay settled 175.00 | Original receipt; no new effect | 175.00 | 70.00 | 105.00 |
| AID-00135 | 175.00 | 0.00 | 70.00 | Record return 0.01 | Apply linked return once | 174.99 | 70.00 | 105.01 |
| AID-00136 | 175.00 | 0.00 | 70.00 | Record return 87.50 | Apply linked return once | 87.50 | 70.00 | 192.50 |
| AID-00137 | 175.00 | 0.00 | 70.00 | Record return 175.00 | Apply linked return once | 0.00 | 70.00 | 280.00 |
| AID-00138 | 175.00 | 0.00 | 70.00 | Record return 175.01 | Return exceeds net fulfillment | 175.00 | 70.00 | 105.00 |
| AID-00139 | 175.00 | 0.00 | 175.00 | Request new 0.01 | Exceeds remaining authority | 175.00 | 175.00 | 0.00 |
| AID-00140 | 175.00 | 0.00 | 175.00 | Request new 115.50 | Exceeds remaining authority | 175.00 | 175.00 | 0.00 |
| AID-00141 | 175.00 | 0.00 | 175.00 | Confirm pending 175.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00142 | 175.00 | 0.00 | 175.00 | Fail pending 175.00 | Release pending reservation | 175.00 | 0.00 | 175.00 |
| AID-00143 | 175.00 | 0.00 | 175.00 | Replay settled 175.00 | Original receipt; no new effect | 175.00 | 175.00 | 0.00 |
| AID-00144 | 175.00 | 0.00 | 175.00 | Record return 0.01 | Apply linked return once | 174.99 | 175.00 | 0.01 |
| AID-00145 | 175.00 | 0.00 | 175.00 | Record return 87.50 | Apply linked return once | 87.50 | 175.00 | 87.50 |
| AID-00146 | 175.00 | 0.00 | 175.00 | Record return 175.00 | Apply linked return once | 0.00 | 175.00 | 175.00 |
| AID-00147 | 175.00 | 0.00 | 175.00 | Record return 175.01 | Return exceeds net fulfillment | 175.00 | 175.00 | 0.00 |
| AID-00148 | 175.00 | 0.01 | 0.00 | Request new 115.50 | Reserve once | 174.99 | 115.50 | 59.51 |
| AID-00149 | 175.00 | 0.01 | 0.00 | Request new 175.00 | Reserve once | 174.99 | 175.00 | 0.01 |
| AID-00150 | 175.00 | 0.01 | 0.00 | Request new 175.01 | Reserve once | 174.99 | 175.01 | 0.00 |
| AID-00151 | 175.00 | 0.01 | 0.00 | Request new 175.02 | Exceeds remaining authority | 174.99 | 0.00 | 175.01 |
| AID-00152 | 175.00 | 0.01 | 0.00 | Replay settled 175.00 | Original receipt; no new effect | 174.99 | 0.00 | 175.01 |
| AID-00153 | 175.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 174.98 | 0.00 | 175.02 |
| AID-00154 | 175.00 | 0.01 | 0.00 | Record return 87.50 | Apply linked return once | 87.49 | 0.00 | 262.51 |
| AID-00155 | 175.00 | 0.01 | 0.00 | Record return 174.99 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00156 | 175.00 | 0.01 | 0.00 | Record return 175.00 | Return exceeds net fulfillment | 174.99 | 0.00 | 175.01 |
| AID-00157 | 175.00 | 0.01 | 70.00 | Request new 105.00 | Reserve once | 174.99 | 175.00 | 0.01 |
| AID-00158 | 175.00 | 0.01 | 70.00 | Request new 105.01 | Reserve once | 174.99 | 175.01 | 0.00 |
| AID-00159 | 175.00 | 0.01 | 70.00 | Request new 105.02 | Exceeds remaining authority | 174.99 | 70.00 | 105.01 |
| AID-00160 | 175.00 | 0.01 | 70.00 | Request new 115.50 | Exceeds remaining authority | 174.99 | 70.00 | 105.01 |
| AID-00161 | 175.00 | 0.01 | 70.00 | Confirm pending 70.00 | Settle original once | 244.99 | 0.00 | 105.01 |
| AID-00162 | 175.00 | 0.01 | 70.00 | Fail pending 70.00 | Release pending reservation | 174.99 | 0.00 | 175.01 |
| AID-00163 | 175.00 | 0.01 | 70.00 | Replay settled 175.00 | Original receipt; no new effect | 174.99 | 70.00 | 105.01 |
| AID-00164 | 175.00 | 0.01 | 70.00 | Record return 0.01 | Apply linked return once | 174.98 | 70.00 | 105.02 |
| AID-00165 | 175.00 | 0.01 | 70.00 | Record return 87.50 | Apply linked return once | 87.49 | 70.00 | 192.51 |
| AID-00166 | 175.00 | 0.01 | 70.00 | Record return 174.99 | Apply linked return once | 0.00 | 70.00 | 280.00 |
| AID-00167 | 175.00 | 0.01 | 70.00 | Record return 175.00 | Return exceeds net fulfillment | 174.99 | 70.00 | 105.01 |
| AID-00168 | 175.00 | 0.01 | 175.01 | Request new 0.01 | Exceeds remaining authority | 174.99 | 175.01 | 0.00 |
| AID-00169 | 175.00 | 0.01 | 175.01 | Request new 115.50 | Exceeds remaining authority | 174.99 | 175.01 | 0.00 |
| AID-00170 | 175.00 | 0.01 | 175.01 | Confirm pending 175.01 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00171 | 175.00 | 0.01 | 175.01 | Fail pending 175.01 | Release pending reservation | 174.99 | 0.00 | 175.01 |
| AID-00172 | 175.00 | 0.01 | 175.01 | Replay settled 175.00 | Original receipt; no new effect | 174.99 | 175.01 | 0.00 |
| AID-00173 | 175.00 | 0.01 | 175.01 | Record return 0.01 | Apply linked return once | 174.98 | 175.01 | 0.01 |
| AID-00174 | 175.00 | 0.01 | 175.01 | Record return 87.50 | Apply linked return once | 87.49 | 175.01 | 87.50 |
| AID-00175 | 175.00 | 0.01 | 175.01 | Record return 174.99 | Apply linked return once | 0.00 | 175.01 | 174.99 |
| AID-00176 | 175.00 | 0.01 | 175.01 | Record return 175.00 | Return exceeds net fulfillment | 174.99 | 175.01 | 0.00 |
| AID-00177 | 175.00 | 43.75 | 0.00 | Request new 115.50 | Reserve once | 131.25 | 115.50 | 103.25 |
| AID-00178 | 175.00 | 43.75 | 0.00 | Request new 218.74 | Reserve once | 131.25 | 218.74 | 0.01 |
| AID-00179 | 175.00 | 43.75 | 0.00 | Request new 218.75 | Reserve once | 131.25 | 218.75 | 0.00 |
| AID-00180 | 175.00 | 43.75 | 0.00 | Request new 218.76 | Exceeds remaining authority | 131.25 | 0.00 | 218.75 |
| AID-00181 | 175.00 | 43.75 | 0.00 | Replay settled 175.00 | Original receipt; no new effect | 131.25 | 0.00 | 218.75 |
| AID-00182 | 175.00 | 43.75 | 0.00 | Record return 0.01 | Apply linked return once | 131.24 | 0.00 | 218.76 |
| AID-00183 | 175.00 | 43.75 | 0.00 | Record return 65.63 | Apply linked return once | 65.62 | 0.00 | 284.38 |
| AID-00184 | 175.00 | 43.75 | 0.00 | Record return 131.25 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00185 | 175.00 | 43.75 | 0.00 | Record return 131.26 | Return exceeds net fulfillment | 131.25 | 0.00 | 218.75 |
| AID-00186 | 175.00 | 43.75 | 87.50 | Request new 115.50 | Reserve once | 131.25 | 203.00 | 15.75 |
| AID-00187 | 175.00 | 43.75 | 87.50 | Request new 131.24 | Reserve once | 131.25 | 218.74 | 0.01 |
| AID-00188 | 175.00 | 43.75 | 87.50 | Request new 131.25 | Reserve once | 131.25 | 218.75 | 0.00 |
| AID-00189 | 175.00 | 43.75 | 87.50 | Request new 131.26 | Exceeds remaining authority | 131.25 | 87.50 | 131.25 |
| AID-00190 | 175.00 | 43.75 | 87.50 | Confirm pending 87.50 | Settle original once | 218.75 | 0.00 | 131.25 |
| AID-00191 | 175.00 | 43.75 | 87.50 | Fail pending 87.50 | Release pending reservation | 131.25 | 0.00 | 218.75 |
| AID-00192 | 175.00 | 43.75 | 87.50 | Replay settled 175.00 | Original receipt; no new effect | 131.25 | 87.50 | 131.25 |
| AID-00193 | 175.00 | 43.75 | 87.50 | Record return 0.01 | Apply linked return once | 131.24 | 87.50 | 131.26 |
| AID-00194 | 175.00 | 43.75 | 87.50 | Record return 65.63 | Apply linked return once | 65.62 | 87.50 | 196.88 |
| AID-00195 | 175.00 | 43.75 | 87.50 | Record return 131.25 | Apply linked return once | 0.00 | 87.50 | 262.50 |
| AID-00196 | 175.00 | 43.75 | 87.50 | Record return 131.26 | Return exceeds net fulfillment | 131.25 | 87.50 | 131.25 |
| AID-00197 | 175.00 | 43.75 | 218.75 | Request new 0.01 | Exceeds remaining authority | 131.25 | 218.75 | 0.00 |
| AID-00198 | 175.00 | 43.75 | 218.75 | Request new 115.50 | Exceeds remaining authority | 131.25 | 218.75 | 0.00 |
| AID-00199 | 175.00 | 43.75 | 218.75 | Confirm pending 218.75 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00200 | 175.00 | 43.75 | 218.75 | Fail pending 218.75 | Release pending reservation | 131.25 | 0.00 | 218.75 |
| AID-00201 | 175.00 | 43.75 | 218.75 | Replay settled 175.00 | Original receipt; no new effect | 131.25 | 218.75 | 0.00 |
| AID-00202 | 175.00 | 43.75 | 218.75 | Record return 0.01 | Apply linked return once | 131.24 | 218.75 | 0.01 |
| AID-00203 | 175.00 | 43.75 | 218.75 | Record return 65.63 | Apply linked return once | 65.62 | 218.75 | 65.63 |
| AID-00204 | 175.00 | 43.75 | 218.75 | Record return 131.25 | Apply linked return once | 0.00 | 218.75 | 131.25 |
| AID-00205 | 175.00 | 43.75 | 218.75 | Record return 131.26 | Return exceeds net fulfillment | 131.25 | 218.75 | 0.00 |
| AID-00206 | 175.00 | 175.00 | 0.00 | Request new 115.50 | Reserve once | 0.00 | 115.50 | 234.50 |
| AID-00207 | 175.00 | 175.00 | 0.00 | Request new 349.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00208 | 175.00 | 175.00 | 0.00 | Request new 350.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00209 | 175.00 | 175.00 | 0.00 | Request new 350.01 | Exceeds remaining authority | 0.00 | 0.00 | 350.00 |
| AID-00210 | 175.00 | 175.00 | 0.00 | Replay settled 175.00 | Original receipt; no new effect | 0.00 | 0.00 | 350.00 |
| AID-00211 | 175.00 | 175.00 | 140.00 | Request new 115.50 | Reserve once | 0.00 | 255.50 | 94.50 |
| AID-00212 | 175.00 | 175.00 | 140.00 | Request new 209.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00213 | 175.00 | 175.00 | 140.00 | Request new 210.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00214 | 175.00 | 175.00 | 140.00 | Request new 210.01 | Exceeds remaining authority | 0.00 | 140.00 | 210.00 |
| AID-00215 | 175.00 | 175.00 | 140.00 | Confirm pending 140.00 | Settle original once | 140.00 | 0.00 | 210.00 |
| AID-00216 | 175.00 | 175.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00217 | 175.00 | 175.00 | 140.00 | Replay settled 175.00 | Original receipt; no new effect | 0.00 | 140.00 | 210.00 |
| AID-00218 | 175.00 | 175.00 | 350.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00219 | 175.00 | 175.00 | 350.00 | Request new 115.50 | Exceeds remaining authority | 0.00 | 350.00 | 0.00 |
| AID-00220 | 175.00 | 175.00 | 350.00 | Confirm pending 350.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00221 | 175.00 | 175.00 | 350.00 | Fail pending 350.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
| AID-00222 | 175.00 | 175.00 | 350.00 | Replay settled 175.00 | Original receipt; no new effect | 0.00 | 350.00 | 0.00 |
| AID-00223 | 280.00 | 0.00 | 0.00 | Request new 69.99 | Reserve once | 280.00 | 69.99 | 0.01 |
| AID-00224 | 280.00 | 0.00 | 0.00 | Request new 70.00 | Reserve once | 280.00 | 70.00 | 0.00 |
| AID-00225 | 280.00 | 0.00 | 0.00 | Request new 70.01 | Exceeds remaining authority | 280.00 | 0.00 | 70.00 |
| AID-00226 | 280.00 | 0.00 | 0.00 | Request new 115.50 | Exceeds remaining authority | 280.00 | 0.00 | 70.00 |
| AID-00227 | 280.00 | 0.00 | 0.00 | Replay settled 280.00 | Original receipt; no new effect | 280.00 | 0.00 | 70.00 |
| AID-00228 | 280.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 279.99 | 0.00 | 70.01 |
| AID-00229 | 280.00 | 0.00 | 0.00 | Record return 140.00 | Apply linked return once | 140.00 | 0.00 | 210.00 |
| AID-00230 | 280.00 | 0.00 | 0.00 | Record return 280.00 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00231 | 280.00 | 0.00 | 0.00 | Record return 280.01 | Return exceeds net fulfillment | 280.00 | 0.00 | 70.00 |
| AID-00232 | 280.00 | 0.00 | 28.00 | Request new 41.99 | Reserve once | 280.00 | 69.99 | 0.01 |
| AID-00233 | 280.00 | 0.00 | 28.00 | Request new 42.00 | Reserve once | 280.00 | 70.00 | 0.00 |
| AID-00234 | 280.00 | 0.00 | 28.00 | Request new 42.01 | Exceeds remaining authority | 280.00 | 28.00 | 42.00 |
| AID-00235 | 280.00 | 0.00 | 28.00 | Request new 115.50 | Exceeds remaining authority | 280.00 | 28.00 | 42.00 |
| AID-00236 | 280.00 | 0.00 | 28.00 | Confirm pending 28.00 | Settle original once | 308.00 | 0.00 | 42.00 |
| AID-00237 | 280.00 | 0.00 | 28.00 | Fail pending 28.00 | Release pending reservation | 280.00 | 0.00 | 70.00 |
| AID-00238 | 280.00 | 0.00 | 28.00 | Replay settled 280.00 | Original receipt; no new effect | 280.00 | 28.00 | 42.00 |
| AID-00239 | 280.00 | 0.00 | 28.00 | Record return 0.01 | Apply linked return once | 279.99 | 28.00 | 42.01 |
| AID-00240 | 280.00 | 0.00 | 28.00 | Record return 140.00 | Apply linked return once | 140.00 | 28.00 | 182.00 |
| AID-00241 | 280.00 | 0.00 | 28.00 | Record return 280.00 | Apply linked return once | 0.00 | 28.00 | 322.00 |
| AID-00242 | 280.00 | 0.00 | 28.00 | Record return 280.01 | Return exceeds net fulfillment | 280.00 | 28.00 | 42.00 |
| AID-00243 | 280.00 | 0.00 | 70.00 | Request new 0.01 | Exceeds remaining authority | 280.00 | 70.00 | 0.00 |
| AID-00244 | 280.00 | 0.00 | 70.00 | Request new 115.50 | Exceeds remaining authority | 280.00 | 70.00 | 0.00 |
| AID-00245 | 280.00 | 0.00 | 70.00 | Confirm pending 70.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00246 | 280.00 | 0.00 | 70.00 | Fail pending 70.00 | Release pending reservation | 280.00 | 0.00 | 70.00 |
| AID-00247 | 280.00 | 0.00 | 70.00 | Replay settled 280.00 | Original receipt; no new effect | 280.00 | 70.00 | 0.00 |
| AID-00248 | 280.00 | 0.00 | 70.00 | Record return 0.01 | Apply linked return once | 279.99 | 70.00 | 0.01 |
| AID-00249 | 280.00 | 0.00 | 70.00 | Record return 140.00 | Apply linked return once | 140.00 | 70.00 | 140.00 |
| AID-00250 | 280.00 | 0.00 | 70.00 | Record return 280.00 | Apply linked return once | 0.00 | 70.00 | 280.00 |
| AID-00251 | 280.00 | 0.00 | 70.00 | Record return 280.01 | Return exceeds net fulfillment | 280.00 | 70.00 | 0.00 |
| AID-00252 | 280.00 | 0.01 | 0.00 | Request new 70.00 | Reserve once | 279.99 | 70.00 | 0.01 |
| AID-00253 | 280.00 | 0.01 | 0.00 | Request new 70.01 | Reserve once | 279.99 | 70.01 | 0.00 |
| AID-00254 | 280.00 | 0.01 | 0.00 | Request new 70.02 | Exceeds remaining authority | 279.99 | 0.00 | 70.01 |
| AID-00255 | 280.00 | 0.01 | 0.00 | Request new 115.50 | Exceeds remaining authority | 279.99 | 0.00 | 70.01 |
| AID-00256 | 280.00 | 0.01 | 0.00 | Replay settled 280.00 | Original receipt; no new effect | 279.99 | 0.00 | 70.01 |
| AID-00257 | 280.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 279.98 | 0.00 | 70.02 |
| AID-00258 | 280.00 | 0.01 | 0.00 | Record return 140.00 | Apply linked return once | 139.99 | 0.00 | 210.01 |
| AID-00259 | 280.00 | 0.01 | 0.00 | Record return 279.99 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00260 | 280.00 | 0.01 | 0.00 | Record return 280.00 | Return exceeds net fulfillment | 279.99 | 0.00 | 70.01 |
| AID-00261 | 280.00 | 0.01 | 28.00 | Request new 42.00 | Reserve once | 279.99 | 70.00 | 0.01 |
| AID-00262 | 280.00 | 0.01 | 28.00 | Request new 42.01 | Reserve once | 279.99 | 70.01 | 0.00 |
| AID-00263 | 280.00 | 0.01 | 28.00 | Request new 42.02 | Exceeds remaining authority | 279.99 | 28.00 | 42.01 |
| AID-00264 | 280.00 | 0.01 | 28.00 | Request new 115.50 | Exceeds remaining authority | 279.99 | 28.00 | 42.01 |
| AID-00265 | 280.00 | 0.01 | 28.00 | Confirm pending 28.00 | Settle original once | 307.99 | 0.00 | 42.01 |
| AID-00266 | 280.00 | 0.01 | 28.00 | Fail pending 28.00 | Release pending reservation | 279.99 | 0.00 | 70.01 |
| AID-00267 | 280.00 | 0.01 | 28.00 | Replay settled 280.00 | Original receipt; no new effect | 279.99 | 28.00 | 42.01 |
| AID-00268 | 280.00 | 0.01 | 28.00 | Record return 0.01 | Apply linked return once | 279.98 | 28.00 | 42.02 |
| AID-00269 | 280.00 | 0.01 | 28.00 | Record return 140.00 | Apply linked return once | 139.99 | 28.00 | 182.01 |
| AID-00270 | 280.00 | 0.01 | 28.00 | Record return 279.99 | Apply linked return once | 0.00 | 28.00 | 322.00 |
| AID-00271 | 280.00 | 0.01 | 28.00 | Record return 280.00 | Return exceeds net fulfillment | 279.99 | 28.00 | 42.01 |
| AID-00272 | 280.00 | 0.01 | 70.01 | Request new 0.01 | Exceeds remaining authority | 279.99 | 70.01 | 0.00 |
| AID-00273 | 280.00 | 0.01 | 70.01 | Request new 115.50 | Exceeds remaining authority | 279.99 | 70.01 | 0.00 |
| AID-00274 | 280.00 | 0.01 | 70.01 | Confirm pending 70.01 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00275 | 280.00 | 0.01 | 70.01 | Fail pending 70.01 | Release pending reservation | 279.99 | 0.00 | 70.01 |
| AID-00276 | 280.00 | 0.01 | 70.01 | Replay settled 280.00 | Original receipt; no new effect | 279.99 | 70.01 | 0.00 |
| AID-00277 | 280.00 | 0.01 | 70.01 | Record return 0.01 | Apply linked return once | 279.98 | 70.01 | 0.01 |
| AID-00278 | 280.00 | 0.01 | 70.01 | Record return 140.00 | Apply linked return once | 139.99 | 70.01 | 140.00 |
| AID-00279 | 280.00 | 0.01 | 70.01 | Record return 279.99 | Apply linked return once | 0.00 | 70.01 | 279.99 |
| AID-00280 | 280.00 | 0.01 | 70.01 | Record return 280.00 | Return exceeds net fulfillment | 279.99 | 70.01 | 0.00 |
| AID-00281 | 280.00 | 70.00 | 0.00 | Request new 115.50 | Reserve once | 210.00 | 115.50 | 24.50 |
| AID-00282 | 280.00 | 70.00 | 0.00 | Request new 139.99 | Reserve once | 210.00 | 139.99 | 0.01 |
| AID-00283 | 280.00 | 70.00 | 0.00 | Request new 140.00 | Reserve once | 210.00 | 140.00 | 0.00 |
| AID-00284 | 280.00 | 70.00 | 0.00 | Request new 140.01 | Exceeds remaining authority | 210.00 | 0.00 | 140.00 |
| AID-00285 | 280.00 | 70.00 | 0.00 | Replay settled 280.00 | Original receipt; no new effect | 210.00 | 0.00 | 140.00 |
| AID-00286 | 280.00 | 70.00 | 0.00 | Record return 0.01 | Apply linked return once | 209.99 | 0.00 | 140.01 |
| AID-00287 | 280.00 | 70.00 | 0.00 | Record return 105.00 | Apply linked return once | 105.00 | 0.00 | 245.00 |
| AID-00288 | 280.00 | 70.00 | 0.00 | Record return 210.00 | Apply linked return once | 0.00 | 0.00 | 350.00 |
| AID-00289 | 280.00 | 70.00 | 0.00 | Record return 210.01 | Return exceeds net fulfillment | 210.00 | 0.00 | 140.00 |
| AID-00290 | 280.00 | 70.00 | 56.00 | Request new 83.99 | Reserve once | 210.00 | 139.99 | 0.01 |
| AID-00291 | 280.00 | 70.00 | 56.00 | Request new 84.00 | Reserve once | 210.00 | 140.00 | 0.00 |
| AID-00292 | 280.00 | 70.00 | 56.00 | Request new 84.01 | Exceeds remaining authority | 210.00 | 56.00 | 84.00 |
| AID-00293 | 280.00 | 70.00 | 56.00 | Request new 115.50 | Exceeds remaining authority | 210.00 | 56.00 | 84.00 |
| AID-00294 | 280.00 | 70.00 | 56.00 | Confirm pending 56.00 | Settle original once | 266.00 | 0.00 | 84.00 |
| AID-00295 | 280.00 | 70.00 | 56.00 | Fail pending 56.00 | Release pending reservation | 210.00 | 0.00 | 140.00 |
| AID-00296 | 280.00 | 70.00 | 56.00 | Replay settled 280.00 | Original receipt; no new effect | 210.00 | 56.00 | 84.00 |
| AID-00297 | 280.00 | 70.00 | 56.00 | Record return 0.01 | Apply linked return once | 209.99 | 56.00 | 84.01 |
| AID-00298 | 280.00 | 70.00 | 56.00 | Record return 105.00 | Apply linked return once | 105.00 | 56.00 | 189.00 |
| AID-00299 | 280.00 | 70.00 | 56.00 | Record return 210.00 | Apply linked return once | 0.00 | 56.00 | 294.00 |
| AID-00300 | 280.00 | 70.00 | 56.00 | Record return 210.01 | Return exceeds net fulfillment | 210.00 | 56.00 | 84.00 |
| AID-00301 | 280.00 | 70.00 | 140.00 | Request new 0.01 | Exceeds remaining authority | 210.00 | 140.00 | 0.00 |
| AID-00302 | 280.00 | 70.00 | 140.00 | Request new 115.50 | Exceeds remaining authority | 210.00 | 140.00 | 0.00 |
| AID-00303 | 280.00 | 70.00 | 140.00 | Confirm pending 140.00 | Settle original once | 350.00 | 0.00 | 0.00 |
| AID-00304 | 280.00 | 70.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 210.00 | 0.00 | 140.00 |
| AID-00305 | 280.00 | 70.00 | 140.00 | Replay settled 280.00 | Original receipt; no new effect | 210.00 | 140.00 | 0.00 |
| AID-00306 | 280.00 | 70.00 | 140.00 | Record return 0.01 | Apply linked return once | 209.99 | 140.00 | 0.01 |
| AID-00307 | 280.00 | 70.00 | 140.00 | Record return 105.00 | Apply linked return once | 105.00 | 140.00 | 105.00 |
| AID-00308 | 280.00 | 70.00 | 140.00 | Record return 210.00 | Apply linked return once | 0.00 | 140.00 | 210.00 |
| AID-00309 | 280.00 | 70.00 | 140.00 | Record return 210.01 | Return exceeds net fulfillment | 210.00 | 140.00 | 0.00 |
| AID-00310 | 280.00 | 280.00 | 0.00 | Request new 115.50 | Reserve once | 0.00 | 115.50 | 234.50 |
| AID-00311 | 280.00 | 280.00 | 0.00 | Request new 349.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00312 | 280.00 | 280.00 | 0.00 | Request new 350.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00313 | 280.00 | 280.00 | 0.00 | Request new 350.01 | Exceeds remaining authority | 0.00 | 0.00 | 350.00 |
| AID-00314 | 280.00 | 280.00 | 0.00 | Replay settled 280.00 | Original receipt; no new effect | 0.00 | 0.00 | 350.00 |
| AID-00315 | 280.00 | 280.00 | 140.00 | Request new 115.50 | Reserve once | 0.00 | 255.50 | 94.50 |
| AID-00316 | 280.00 | 280.00 | 140.00 | Request new 209.99 | Reserve once | 0.00 | 349.99 | 0.01 |
| AID-00317 | 280.00 | 280.00 | 140.00 | Request new 210.00 | Reserve once | 0.00 | 350.00 | 0.00 |
| AID-00318 | 280.00 | 280.00 | 140.00 | Request new 210.01 | Exceeds remaining authority | 0.00 | 140.00 | 210.00 |
| AID-00319 | 280.00 | 280.00 | 140.00 | Confirm pending 140.00 | Settle original once | 140.00 | 0.00 | 210.00 |
| AID-00320 | 280.00 | 280.00 | 140.00 | Fail pending 140.00 | Release pending reservation | 0.00 | 0.00 | 350.00 |
