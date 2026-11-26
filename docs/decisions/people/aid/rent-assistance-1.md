# Rent assistance — part 1 of 2

[Policy and other cases](README.md)

One approved award of 1200.00 currency units; all inputs use currency units at 2 decimal places. One original settled fulfillment, when present, may be partially returned. An outstanding payment or stock issue is reserved against authority. Historical issued and returned amounts are kept even when the net amount is zero. Reviewers can reconstruct this case using the supplied opening facts.

| Case | Opening gross | Opening returns | Opening reserved | Requested event and value | Decision | New net delivered | New reserved | New free authority |
|---|---|---|---|---|---|---|---|---|
| AID-03133 | 0.00 | 0.00 | 0.00 | Request new 396.00 | Reserve once | 0.00 | 396.00 | 804.00 |
| AID-03134 | 0.00 | 0.00 | 0.00 | Request new 1199.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03135 | 0.00 | 0.00 | 0.00 | Request new 1200.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03136 | 0.00 | 0.00 | 0.00 | Request new 1200.01 | Exceeds remaining authority | 0.00 | 0.00 | 1200.00 |
| AID-03137 | 0.00 | 0.00 | 480.00 | Request new 396.00 | Reserve once | 0.00 | 876.00 | 324.00 |
| AID-03138 | 0.00 | 0.00 | 480.00 | Request new 719.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03139 | 0.00 | 0.00 | 480.00 | Request new 720.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03140 | 0.00 | 0.00 | 480.00 | Request new 720.01 | Exceeds remaining authority | 0.00 | 480.00 | 720.00 |
| AID-03141 | 0.00 | 0.00 | 480.00 | Confirm pending 480.00 | Settle original once | 480.00 | 0.00 | 720.00 |
| AID-03142 | 0.00 | 0.00 | 480.00 | Fail pending 480.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03143 | 0.00 | 0.00 | 1200.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03144 | 0.00 | 0.00 | 1200.00 | Request new 396.00 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03145 | 0.00 | 0.00 | 1200.00 | Confirm pending 1200.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03146 | 0.00 | 0.00 | 1200.00 | Fail pending 1200.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03147 | 240.00 | 0.00 | 0.00 | Request new 396.00 | Reserve once | 240.00 | 396.00 | 564.00 |
| AID-03148 | 240.00 | 0.00 | 0.00 | Request new 959.99 | Reserve once | 240.00 | 959.99 | 0.01 |
| AID-03149 | 240.00 | 0.00 | 0.00 | Request new 960.00 | Reserve once | 240.00 | 960.00 | 0.00 |
| AID-03150 | 240.00 | 0.00 | 0.00 | Request new 960.01 | Exceeds remaining authority | 240.00 | 0.00 | 960.00 |
| AID-03151 | 240.00 | 0.00 | 0.00 | Replay settled 240.00 | Original receipt; no new effect | 240.00 | 0.00 | 960.00 |
| AID-03152 | 240.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 239.99 | 0.00 | 960.01 |
| AID-03153 | 240.00 | 0.00 | 0.00 | Record return 120.00 | Apply linked return once | 120.00 | 0.00 | 1080.00 |
| AID-03154 | 240.00 | 0.00 | 0.00 | Record return 240.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03155 | 240.00 | 0.00 | 0.00 | Record return 240.01 | Return exceeds net fulfillment | 240.00 | 0.00 | 960.00 |
| AID-03156 | 240.00 | 0.00 | 384.00 | Request new 396.00 | Reserve once | 240.00 | 780.00 | 180.00 |
| AID-03157 | 240.00 | 0.00 | 384.00 | Request new 575.99 | Reserve once | 240.00 | 959.99 | 0.01 |
| AID-03158 | 240.00 | 0.00 | 384.00 | Request new 576.00 | Reserve once | 240.00 | 960.00 | 0.00 |
| AID-03159 | 240.00 | 0.00 | 384.00 | Request new 576.01 | Exceeds remaining authority | 240.00 | 384.00 | 576.00 |
| AID-03160 | 240.00 | 0.00 | 384.00 | Confirm pending 384.00 | Settle original once | 624.00 | 0.00 | 576.00 |
| AID-03161 | 240.00 | 0.00 | 384.00 | Fail pending 384.00 | Release pending reservation | 240.00 | 0.00 | 960.00 |
| AID-03162 | 240.00 | 0.00 | 384.00 | Replay settled 240.00 | Original receipt; no new effect | 240.00 | 384.00 | 576.00 |
| AID-03163 | 240.00 | 0.00 | 384.00 | Record return 0.01 | Apply linked return once | 239.99 | 384.00 | 576.01 |
| AID-03164 | 240.00 | 0.00 | 384.00 | Record return 120.00 | Apply linked return once | 120.00 | 384.00 | 696.00 |
| AID-03165 | 240.00 | 0.00 | 384.00 | Record return 240.00 | Apply linked return once | 0.00 | 384.00 | 816.00 |
| AID-03166 | 240.00 | 0.00 | 384.00 | Record return 240.01 | Return exceeds net fulfillment | 240.00 | 384.00 | 576.00 |
| AID-03167 | 240.00 | 0.00 | 960.00 | Request new 0.01 | Exceeds remaining authority | 240.00 | 960.00 | 0.00 |
| AID-03168 | 240.00 | 0.00 | 960.00 | Request new 396.00 | Exceeds remaining authority | 240.00 | 960.00 | 0.00 |
| AID-03169 | 240.00 | 0.00 | 960.00 | Confirm pending 960.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03170 | 240.00 | 0.00 | 960.00 | Fail pending 960.00 | Release pending reservation | 240.00 | 0.00 | 960.00 |
| AID-03171 | 240.00 | 0.00 | 960.00 | Replay settled 240.00 | Original receipt; no new effect | 240.00 | 960.00 | 0.00 |
| AID-03172 | 240.00 | 0.00 | 960.00 | Record return 0.01 | Apply linked return once | 239.99 | 960.00 | 0.01 |
| AID-03173 | 240.00 | 0.00 | 960.00 | Record return 120.00 | Apply linked return once | 120.00 | 960.00 | 120.00 |
| AID-03174 | 240.00 | 0.00 | 960.00 | Record return 240.00 | Apply linked return once | 0.00 | 960.00 | 240.00 |
| AID-03175 | 240.00 | 0.00 | 960.00 | Record return 240.01 | Return exceeds net fulfillment | 240.00 | 960.00 | 0.00 |
| AID-03176 | 240.00 | 0.01 | 0.00 | Request new 396.00 | Reserve once | 239.99 | 396.00 | 564.01 |
| AID-03177 | 240.00 | 0.01 | 0.00 | Request new 960.00 | Reserve once | 239.99 | 960.00 | 0.01 |
| AID-03178 | 240.00 | 0.01 | 0.00 | Request new 960.01 | Reserve once | 239.99 | 960.01 | 0.00 |
| AID-03179 | 240.00 | 0.01 | 0.00 | Request new 960.02 | Exceeds remaining authority | 239.99 | 0.00 | 960.01 |
| AID-03180 | 240.00 | 0.01 | 0.00 | Replay settled 240.00 | Original receipt; no new effect | 239.99 | 0.00 | 960.01 |
| AID-03181 | 240.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 239.98 | 0.00 | 960.02 |
| AID-03182 | 240.00 | 0.01 | 0.00 | Record return 120.00 | Apply linked return once | 119.99 | 0.00 | 1080.01 |
| AID-03183 | 240.00 | 0.01 | 0.00 | Record return 239.99 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03184 | 240.00 | 0.01 | 0.00 | Record return 240.00 | Return exceeds net fulfillment | 239.99 | 0.00 | 960.01 |
| AID-03185 | 240.00 | 0.01 | 384.00 | Request new 396.00 | Reserve once | 239.99 | 780.00 | 180.01 |
| AID-03186 | 240.00 | 0.01 | 384.00 | Request new 576.00 | Reserve once | 239.99 | 960.00 | 0.01 |
| AID-03187 | 240.00 | 0.01 | 384.00 | Request new 576.01 | Reserve once | 239.99 | 960.01 | 0.00 |
| AID-03188 | 240.00 | 0.01 | 384.00 | Request new 576.02 | Exceeds remaining authority | 239.99 | 384.00 | 576.01 |
| AID-03189 | 240.00 | 0.01 | 384.00 | Confirm pending 384.00 | Settle original once | 623.99 | 0.00 | 576.01 |
| AID-03190 | 240.00 | 0.01 | 384.00 | Fail pending 384.00 | Release pending reservation | 239.99 | 0.00 | 960.01 |
| AID-03191 | 240.00 | 0.01 | 384.00 | Replay settled 240.00 | Original receipt; no new effect | 239.99 | 384.00 | 576.01 |
| AID-03192 | 240.00 | 0.01 | 384.00 | Record return 0.01 | Apply linked return once | 239.98 | 384.00 | 576.02 |
| AID-03193 | 240.00 | 0.01 | 384.00 | Record return 120.00 | Apply linked return once | 119.99 | 384.00 | 696.01 |
| AID-03194 | 240.00 | 0.01 | 384.00 | Record return 239.99 | Apply linked return once | 0.00 | 384.00 | 816.00 |
| AID-03195 | 240.00 | 0.01 | 384.00 | Record return 240.00 | Return exceeds net fulfillment | 239.99 | 384.00 | 576.01 |
| AID-03196 | 240.00 | 0.01 | 960.01 | Request new 0.01 | Exceeds remaining authority | 239.99 | 960.01 | 0.00 |
| AID-03197 | 240.00 | 0.01 | 960.01 | Request new 396.00 | Exceeds remaining authority | 239.99 | 960.01 | 0.00 |
| AID-03198 | 240.00 | 0.01 | 960.01 | Confirm pending 960.01 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03199 | 240.00 | 0.01 | 960.01 | Fail pending 960.01 | Release pending reservation | 239.99 | 0.00 | 960.01 |
| AID-03200 | 240.00 | 0.01 | 960.01 | Replay settled 240.00 | Original receipt; no new effect | 239.99 | 960.01 | 0.00 |
| AID-03201 | 240.00 | 0.01 | 960.01 | Record return 0.01 | Apply linked return once | 239.98 | 960.01 | 0.01 |
| AID-03202 | 240.00 | 0.01 | 960.01 | Record return 120.00 | Apply linked return once | 119.99 | 960.01 | 120.00 |
| AID-03203 | 240.00 | 0.01 | 960.01 | Record return 239.99 | Apply linked return once | 0.00 | 960.01 | 239.99 |
| AID-03204 | 240.00 | 0.01 | 960.01 | Record return 240.00 | Return exceeds net fulfillment | 239.99 | 960.01 | 0.00 |
| AID-03205 | 240.00 | 60.00 | 0.00 | Request new 396.00 | Reserve once | 180.00 | 396.00 | 624.00 |
| AID-03206 | 240.00 | 60.00 | 0.00 | Request new 1019.99 | Reserve once | 180.00 | 1019.99 | 0.01 |
| AID-03207 | 240.00 | 60.00 | 0.00 | Request new 1020.00 | Reserve once | 180.00 | 1020.00 | 0.00 |
| AID-03208 | 240.00 | 60.00 | 0.00 | Request new 1020.01 | Exceeds remaining authority | 180.00 | 0.00 | 1020.00 |
| AID-03209 | 240.00 | 60.00 | 0.00 | Replay settled 240.00 | Original receipt; no new effect | 180.00 | 0.00 | 1020.00 |
| AID-03210 | 240.00 | 60.00 | 0.00 | Record return 0.01 | Apply linked return once | 179.99 | 0.00 | 1020.01 |
| AID-03211 | 240.00 | 60.00 | 0.00 | Record return 90.00 | Apply linked return once | 90.00 | 0.00 | 1110.00 |
| AID-03212 | 240.00 | 60.00 | 0.00 | Record return 180.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03213 | 240.00 | 60.00 | 0.00 | Record return 180.01 | Return exceeds net fulfillment | 180.00 | 0.00 | 1020.00 |
| AID-03214 | 240.00 | 60.00 | 408.00 | Request new 396.00 | Reserve once | 180.00 | 804.00 | 216.00 |
| AID-03215 | 240.00 | 60.00 | 408.00 | Request new 611.99 | Reserve once | 180.00 | 1019.99 | 0.01 |
| AID-03216 | 240.00 | 60.00 | 408.00 | Request new 612.00 | Reserve once | 180.00 | 1020.00 | 0.00 |
| AID-03217 | 240.00 | 60.00 | 408.00 | Request new 612.01 | Exceeds remaining authority | 180.00 | 408.00 | 612.00 |
| AID-03218 | 240.00 | 60.00 | 408.00 | Confirm pending 408.00 | Settle original once | 588.00 | 0.00 | 612.00 |
| AID-03219 | 240.00 | 60.00 | 408.00 | Fail pending 408.00 | Release pending reservation | 180.00 | 0.00 | 1020.00 |
| AID-03220 | 240.00 | 60.00 | 408.00 | Replay settled 240.00 | Original receipt; no new effect | 180.00 | 408.00 | 612.00 |
| AID-03221 | 240.00 | 60.00 | 408.00 | Record return 0.01 | Apply linked return once | 179.99 | 408.00 | 612.01 |
| AID-03222 | 240.00 | 60.00 | 408.00 | Record return 90.00 | Apply linked return once | 90.00 | 408.00 | 702.00 |
| AID-03223 | 240.00 | 60.00 | 408.00 | Record return 180.00 | Apply linked return once | 0.00 | 408.00 | 792.00 |
| AID-03224 | 240.00 | 60.00 | 408.00 | Record return 180.01 | Return exceeds net fulfillment | 180.00 | 408.00 | 612.00 |
| AID-03225 | 240.00 | 60.00 | 1020.00 | Request new 0.01 | Exceeds remaining authority | 180.00 | 1020.00 | 0.00 |
| AID-03226 | 240.00 | 60.00 | 1020.00 | Request new 396.00 | Exceeds remaining authority | 180.00 | 1020.00 | 0.00 |
| AID-03227 | 240.00 | 60.00 | 1020.00 | Confirm pending 1020.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03228 | 240.00 | 60.00 | 1020.00 | Fail pending 1020.00 | Release pending reservation | 180.00 | 0.00 | 1020.00 |
| AID-03229 | 240.00 | 60.00 | 1020.00 | Replay settled 240.00 | Original receipt; no new effect | 180.00 | 1020.00 | 0.00 |
| AID-03230 | 240.00 | 60.00 | 1020.00 | Record return 0.01 | Apply linked return once | 179.99 | 1020.00 | 0.01 |
| AID-03231 | 240.00 | 60.00 | 1020.00 | Record return 90.00 | Apply linked return once | 90.00 | 1020.00 | 90.00 |
| AID-03232 | 240.00 | 60.00 | 1020.00 | Record return 180.00 | Apply linked return once | 0.00 | 1020.00 | 180.00 |
| AID-03233 | 240.00 | 60.00 | 1020.00 | Record return 180.01 | Return exceeds net fulfillment | 180.00 | 1020.00 | 0.00 |
| AID-03234 | 240.00 | 240.00 | 0.00 | Request new 396.00 | Reserve once | 0.00 | 396.00 | 804.00 |
| AID-03235 | 240.00 | 240.00 | 0.00 | Request new 1199.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03236 | 240.00 | 240.00 | 0.00 | Request new 1200.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03237 | 240.00 | 240.00 | 0.00 | Request new 1200.01 | Exceeds remaining authority | 0.00 | 0.00 | 1200.00 |
| AID-03238 | 240.00 | 240.00 | 0.00 | Replay settled 240.00 | Original receipt; no new effect | 0.00 | 0.00 | 1200.00 |
| AID-03239 | 240.00 | 240.00 | 480.00 | Request new 396.00 | Reserve once | 0.00 | 876.00 | 324.00 |
| AID-03240 | 240.00 | 240.00 | 480.00 | Request new 719.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03241 | 240.00 | 240.00 | 480.00 | Request new 720.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03242 | 240.00 | 240.00 | 480.00 | Request new 720.01 | Exceeds remaining authority | 0.00 | 480.00 | 720.00 |
| AID-03243 | 240.00 | 240.00 | 480.00 | Confirm pending 480.00 | Settle original once | 480.00 | 0.00 | 720.00 |
| AID-03244 | 240.00 | 240.00 | 480.00 | Fail pending 480.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03245 | 240.00 | 240.00 | 480.00 | Replay settled 240.00 | Original receipt; no new effect | 0.00 | 480.00 | 720.00 |
| AID-03246 | 240.00 | 240.00 | 1200.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03247 | 240.00 | 240.00 | 1200.00 | Request new 396.00 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03248 | 240.00 | 240.00 | 1200.00 | Confirm pending 1200.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03249 | 240.00 | 240.00 | 1200.00 | Fail pending 1200.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03250 | 240.00 | 240.00 | 1200.00 | Replay settled 240.00 | Original receipt; no new effect | 0.00 | 1200.00 | 0.00 |
| AID-03251 | 600.00 | 0.00 | 0.00 | Request new 396.00 | Reserve once | 600.00 | 396.00 | 204.00 |
| AID-03252 | 600.00 | 0.00 | 0.00 | Request new 599.99 | Reserve once | 600.00 | 599.99 | 0.01 |
| AID-03253 | 600.00 | 0.00 | 0.00 | Request new 600.00 | Reserve once | 600.00 | 600.00 | 0.00 |
| AID-03254 | 600.00 | 0.00 | 0.00 | Request new 600.01 | Exceeds remaining authority | 600.00 | 0.00 | 600.00 |
| AID-03255 | 600.00 | 0.00 | 0.00 | Replay settled 600.00 | Original receipt; no new effect | 600.00 | 0.00 | 600.00 |
| AID-03256 | 600.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 599.99 | 0.00 | 600.01 |
| AID-03257 | 600.00 | 0.00 | 0.00 | Record return 300.00 | Apply linked return once | 300.00 | 0.00 | 900.00 |
| AID-03258 | 600.00 | 0.00 | 0.00 | Record return 600.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03259 | 600.00 | 0.00 | 0.00 | Record return 600.01 | Return exceeds net fulfillment | 600.00 | 0.00 | 600.00 |
| AID-03260 | 600.00 | 0.00 | 240.00 | Request new 359.99 | Reserve once | 600.00 | 599.99 | 0.01 |
| AID-03261 | 600.00 | 0.00 | 240.00 | Request new 360.00 | Reserve once | 600.00 | 600.00 | 0.00 |
| AID-03262 | 600.00 | 0.00 | 240.00 | Request new 360.01 | Exceeds remaining authority | 600.00 | 240.00 | 360.00 |
| AID-03263 | 600.00 | 0.00 | 240.00 | Request new 396.00 | Exceeds remaining authority | 600.00 | 240.00 | 360.00 |
| AID-03264 | 600.00 | 0.00 | 240.00 | Confirm pending 240.00 | Settle original once | 840.00 | 0.00 | 360.00 |
| AID-03265 | 600.00 | 0.00 | 240.00 | Fail pending 240.00 | Release pending reservation | 600.00 | 0.00 | 600.00 |
| AID-03266 | 600.00 | 0.00 | 240.00 | Replay settled 600.00 | Original receipt; no new effect | 600.00 | 240.00 | 360.00 |
| AID-03267 | 600.00 | 0.00 | 240.00 | Record return 0.01 | Apply linked return once | 599.99 | 240.00 | 360.01 |
| AID-03268 | 600.00 | 0.00 | 240.00 | Record return 300.00 | Apply linked return once | 300.00 | 240.00 | 660.00 |
| AID-03269 | 600.00 | 0.00 | 240.00 | Record return 600.00 | Apply linked return once | 0.00 | 240.00 | 960.00 |
| AID-03270 | 600.00 | 0.00 | 240.00 | Record return 600.01 | Return exceeds net fulfillment | 600.00 | 240.00 | 360.00 |
| AID-03271 | 600.00 | 0.00 | 600.00 | Request new 0.01 | Exceeds remaining authority | 600.00 | 600.00 | 0.00 |
| AID-03272 | 600.00 | 0.00 | 600.00 | Request new 396.00 | Exceeds remaining authority | 600.00 | 600.00 | 0.00 |
| AID-03273 | 600.00 | 0.00 | 600.00 | Confirm pending 600.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03274 | 600.00 | 0.00 | 600.00 | Fail pending 600.00 | Release pending reservation | 600.00 | 0.00 | 600.00 |
| AID-03275 | 600.00 | 0.00 | 600.00 | Replay settled 600.00 | Original receipt; no new effect | 600.00 | 600.00 | 0.00 |
| AID-03276 | 600.00 | 0.00 | 600.00 | Record return 0.01 | Apply linked return once | 599.99 | 600.00 | 0.01 |
| AID-03277 | 600.00 | 0.00 | 600.00 | Record return 300.00 | Apply linked return once | 300.00 | 600.00 | 300.00 |
| AID-03278 | 600.00 | 0.00 | 600.00 | Record return 600.00 | Apply linked return once | 0.00 | 600.00 | 600.00 |
| AID-03279 | 600.00 | 0.00 | 600.00 | Record return 600.01 | Return exceeds net fulfillment | 600.00 | 600.00 | 0.00 |
| AID-03280 | 600.00 | 0.01 | 0.00 | Request new 396.00 | Reserve once | 599.99 | 396.00 | 204.01 |
| AID-03281 | 600.00 | 0.01 | 0.00 | Request new 600.00 | Reserve once | 599.99 | 600.00 | 0.01 |
| AID-03282 | 600.00 | 0.01 | 0.00 | Request new 600.01 | Reserve once | 599.99 | 600.01 | 0.00 |
| AID-03283 | 600.00 | 0.01 | 0.00 | Request new 600.02 | Exceeds remaining authority | 599.99 | 0.00 | 600.01 |
| AID-03284 | 600.00 | 0.01 | 0.00 | Replay settled 600.00 | Original receipt; no new effect | 599.99 | 0.00 | 600.01 |
| AID-03285 | 600.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 599.98 | 0.00 | 600.02 |
| AID-03286 | 600.00 | 0.01 | 0.00 | Record return 300.00 | Apply linked return once | 299.99 | 0.00 | 900.01 |
| AID-03287 | 600.00 | 0.01 | 0.00 | Record return 599.99 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03288 | 600.00 | 0.01 | 0.00 | Record return 600.00 | Return exceeds net fulfillment | 599.99 | 0.00 | 600.01 |
| AID-03289 | 600.00 | 0.01 | 240.00 | Request new 360.00 | Reserve once | 599.99 | 600.00 | 0.01 |
| AID-03290 | 600.00 | 0.01 | 240.00 | Request new 360.01 | Reserve once | 599.99 | 600.01 | 0.00 |
| AID-03291 | 600.00 | 0.01 | 240.00 | Request new 360.02 | Exceeds remaining authority | 599.99 | 240.00 | 360.01 |
| AID-03292 | 600.00 | 0.01 | 240.00 | Request new 396.00 | Exceeds remaining authority | 599.99 | 240.00 | 360.01 |
| AID-03293 | 600.00 | 0.01 | 240.00 | Confirm pending 240.00 | Settle original once | 839.99 | 0.00 | 360.01 |
| AID-03294 | 600.00 | 0.01 | 240.00 | Fail pending 240.00 | Release pending reservation | 599.99 | 0.00 | 600.01 |
| AID-03295 | 600.00 | 0.01 | 240.00 | Replay settled 600.00 | Original receipt; no new effect | 599.99 | 240.00 | 360.01 |
| AID-03296 | 600.00 | 0.01 | 240.00 | Record return 0.01 | Apply linked return once | 599.98 | 240.00 | 360.02 |
| AID-03297 | 600.00 | 0.01 | 240.00 | Record return 300.00 | Apply linked return once | 299.99 | 240.00 | 660.01 |
| AID-03298 | 600.00 | 0.01 | 240.00 | Record return 599.99 | Apply linked return once | 0.00 | 240.00 | 960.00 |
| AID-03299 | 600.00 | 0.01 | 240.00 | Record return 600.00 | Return exceeds net fulfillment | 599.99 | 240.00 | 360.01 |
| AID-03300 | 600.00 | 0.01 | 600.01 | Request new 0.01 | Exceeds remaining authority | 599.99 | 600.01 | 0.00 |
| AID-03301 | 600.00 | 0.01 | 600.01 | Request new 396.00 | Exceeds remaining authority | 599.99 | 600.01 | 0.00 |
| AID-03302 | 600.00 | 0.01 | 600.01 | Confirm pending 600.01 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03303 | 600.00 | 0.01 | 600.01 | Fail pending 600.01 | Release pending reservation | 599.99 | 0.00 | 600.01 |
| AID-03304 | 600.00 | 0.01 | 600.01 | Replay settled 600.00 | Original receipt; no new effect | 599.99 | 600.01 | 0.00 |
| AID-03305 | 600.00 | 0.01 | 600.01 | Record return 0.01 | Apply linked return once | 599.98 | 600.01 | 0.01 |
| AID-03306 | 600.00 | 0.01 | 600.01 | Record return 300.00 | Apply linked return once | 299.99 | 600.01 | 300.00 |
| AID-03307 | 600.00 | 0.01 | 600.01 | Record return 599.99 | Apply linked return once | 0.00 | 600.01 | 599.99 |
| AID-03308 | 600.00 | 0.01 | 600.01 | Record return 600.00 | Return exceeds net fulfillment | 599.99 | 600.01 | 0.00 |
| AID-03309 | 600.00 | 150.00 | 0.00 | Request new 396.00 | Reserve once | 450.00 | 396.00 | 354.00 |
| AID-03310 | 600.00 | 150.00 | 0.00 | Request new 749.99 | Reserve once | 450.00 | 749.99 | 0.01 |
| AID-03311 | 600.00 | 150.00 | 0.00 | Request new 750.00 | Reserve once | 450.00 | 750.00 | 0.00 |
| AID-03312 | 600.00 | 150.00 | 0.00 | Request new 750.01 | Exceeds remaining authority | 450.00 | 0.00 | 750.00 |
| AID-03313 | 600.00 | 150.00 | 0.00 | Replay settled 600.00 | Original receipt; no new effect | 450.00 | 0.00 | 750.00 |
| AID-03314 | 600.00 | 150.00 | 0.00 | Record return 0.01 | Apply linked return once | 449.99 | 0.00 | 750.01 |
| AID-03315 | 600.00 | 150.00 | 0.00 | Record return 225.00 | Apply linked return once | 225.00 | 0.00 | 975.00 |
| AID-03316 | 600.00 | 150.00 | 0.00 | Record return 450.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03317 | 600.00 | 150.00 | 0.00 | Record return 450.01 | Return exceeds net fulfillment | 450.00 | 0.00 | 750.00 |
| AID-03318 | 600.00 | 150.00 | 300.00 | Request new 396.00 | Reserve once | 450.00 | 696.00 | 54.00 |
| AID-03319 | 600.00 | 150.00 | 300.00 | Request new 449.99 | Reserve once | 450.00 | 749.99 | 0.01 |
| AID-03320 | 600.00 | 150.00 | 300.00 | Request new 450.00 | Reserve once | 450.00 | 750.00 | 0.00 |
| AID-03321 | 600.00 | 150.00 | 300.00 | Request new 450.01 | Exceeds remaining authority | 450.00 | 300.00 | 450.00 |
| AID-03322 | 600.00 | 150.00 | 300.00 | Confirm pending 300.00 | Settle original once | 750.00 | 0.00 | 450.00 |
| AID-03323 | 600.00 | 150.00 | 300.00 | Fail pending 300.00 | Release pending reservation | 450.00 | 0.00 | 750.00 |
| AID-03324 | 600.00 | 150.00 | 300.00 | Replay settled 600.00 | Original receipt; no new effect | 450.00 | 300.00 | 450.00 |
| AID-03325 | 600.00 | 150.00 | 300.00 | Record return 0.01 | Apply linked return once | 449.99 | 300.00 | 450.01 |
| AID-03326 | 600.00 | 150.00 | 300.00 | Record return 225.00 | Apply linked return once | 225.00 | 300.00 | 675.00 |
| AID-03327 | 600.00 | 150.00 | 300.00 | Record return 450.00 | Apply linked return once | 0.00 | 300.00 | 900.00 |
| AID-03328 | 600.00 | 150.00 | 300.00 | Record return 450.01 | Return exceeds net fulfillment | 450.00 | 300.00 | 450.00 |
| AID-03329 | 600.00 | 150.00 | 750.00 | Request new 0.01 | Exceeds remaining authority | 450.00 | 750.00 | 0.00 |
| AID-03330 | 600.00 | 150.00 | 750.00 | Request new 396.00 | Exceeds remaining authority | 450.00 | 750.00 | 0.00 |
| AID-03331 | 600.00 | 150.00 | 750.00 | Confirm pending 750.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03332 | 600.00 | 150.00 | 750.00 | Fail pending 750.00 | Release pending reservation | 450.00 | 0.00 | 750.00 |
| AID-03333 | 600.00 | 150.00 | 750.00 | Replay settled 600.00 | Original receipt; no new effect | 450.00 | 750.00 | 0.00 |
| AID-03334 | 600.00 | 150.00 | 750.00 | Record return 0.01 | Apply linked return once | 449.99 | 750.00 | 0.01 |
| AID-03335 | 600.00 | 150.00 | 750.00 | Record return 225.00 | Apply linked return once | 225.00 | 750.00 | 225.00 |
| AID-03336 | 600.00 | 150.00 | 750.00 | Record return 450.00 | Apply linked return once | 0.00 | 750.00 | 450.00 |
| AID-03337 | 600.00 | 150.00 | 750.00 | Record return 450.01 | Return exceeds net fulfillment | 450.00 | 750.00 | 0.00 |
| AID-03338 | 600.00 | 600.00 | 0.00 | Request new 396.00 | Reserve once | 0.00 | 396.00 | 804.00 |
| AID-03339 | 600.00 | 600.00 | 0.00 | Request new 1199.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03340 | 600.00 | 600.00 | 0.00 | Request new 1200.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03341 | 600.00 | 600.00 | 0.00 | Request new 1200.01 | Exceeds remaining authority | 0.00 | 0.00 | 1200.00 |
| AID-03342 | 600.00 | 600.00 | 0.00 | Replay settled 600.00 | Original receipt; no new effect | 0.00 | 0.00 | 1200.00 |
| AID-03343 | 600.00 | 600.00 | 480.00 | Request new 396.00 | Reserve once | 0.00 | 876.00 | 324.00 |
| AID-03344 | 600.00 | 600.00 | 480.00 | Request new 719.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03345 | 600.00 | 600.00 | 480.00 | Request new 720.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03346 | 600.00 | 600.00 | 480.00 | Request new 720.01 | Exceeds remaining authority | 0.00 | 480.00 | 720.00 |
| AID-03347 | 600.00 | 600.00 | 480.00 | Confirm pending 480.00 | Settle original once | 480.00 | 0.00 | 720.00 |
| AID-03348 | 600.00 | 600.00 | 480.00 | Fail pending 480.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03349 | 600.00 | 600.00 | 480.00 | Replay settled 600.00 | Original receipt; no new effect | 0.00 | 480.00 | 720.00 |
| AID-03350 | 600.00 | 600.00 | 1200.00 | Request new 0.01 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03351 | 600.00 | 600.00 | 1200.00 | Request new 396.00 | Exceeds remaining authority | 0.00 | 1200.00 | 0.00 |
| AID-03352 | 600.00 | 600.00 | 1200.00 | Confirm pending 1200.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03353 | 600.00 | 600.00 | 1200.00 | Fail pending 1200.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
| AID-03354 | 600.00 | 600.00 | 1200.00 | Replay settled 600.00 | Original receipt; no new effect | 0.00 | 1200.00 | 0.00 |
| AID-03355 | 960.00 | 0.00 | 0.00 | Request new 239.99 | Reserve once | 960.00 | 239.99 | 0.01 |
| AID-03356 | 960.00 | 0.00 | 0.00 | Request new 240.00 | Reserve once | 960.00 | 240.00 | 0.00 |
| AID-03357 | 960.00 | 0.00 | 0.00 | Request new 240.01 | Exceeds remaining authority | 960.00 | 0.00 | 240.00 |
| AID-03358 | 960.00 | 0.00 | 0.00 | Request new 396.00 | Exceeds remaining authority | 960.00 | 0.00 | 240.00 |
| AID-03359 | 960.00 | 0.00 | 0.00 | Replay settled 960.00 | Original receipt; no new effect | 960.00 | 0.00 | 240.00 |
| AID-03360 | 960.00 | 0.00 | 0.00 | Record return 0.01 | Apply linked return once | 959.99 | 0.00 | 240.01 |
| AID-03361 | 960.00 | 0.00 | 0.00 | Record return 480.00 | Apply linked return once | 480.00 | 0.00 | 720.00 |
| AID-03362 | 960.00 | 0.00 | 0.00 | Record return 960.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03363 | 960.00 | 0.00 | 0.00 | Record return 960.01 | Return exceeds net fulfillment | 960.00 | 0.00 | 240.00 |
| AID-03364 | 960.00 | 0.00 | 96.00 | Request new 143.99 | Reserve once | 960.00 | 239.99 | 0.01 |
| AID-03365 | 960.00 | 0.00 | 96.00 | Request new 144.00 | Reserve once | 960.00 | 240.00 | 0.00 |
| AID-03366 | 960.00 | 0.00 | 96.00 | Request new 144.01 | Exceeds remaining authority | 960.00 | 96.00 | 144.00 |
| AID-03367 | 960.00 | 0.00 | 96.00 | Request new 396.00 | Exceeds remaining authority | 960.00 | 96.00 | 144.00 |
| AID-03368 | 960.00 | 0.00 | 96.00 | Confirm pending 96.00 | Settle original once | 1056.00 | 0.00 | 144.00 |
| AID-03369 | 960.00 | 0.00 | 96.00 | Fail pending 96.00 | Release pending reservation | 960.00 | 0.00 | 240.00 |
| AID-03370 | 960.00 | 0.00 | 96.00 | Replay settled 960.00 | Original receipt; no new effect | 960.00 | 96.00 | 144.00 |
| AID-03371 | 960.00 | 0.00 | 96.00 | Record return 0.01 | Apply linked return once | 959.99 | 96.00 | 144.01 |
| AID-03372 | 960.00 | 0.00 | 96.00 | Record return 480.00 | Apply linked return once | 480.00 | 96.00 | 624.00 |
| AID-03373 | 960.00 | 0.00 | 96.00 | Record return 960.00 | Apply linked return once | 0.00 | 96.00 | 1104.00 |
| AID-03374 | 960.00 | 0.00 | 96.00 | Record return 960.01 | Return exceeds net fulfillment | 960.00 | 96.00 | 144.00 |
| AID-03375 | 960.00 | 0.00 | 240.00 | Request new 0.01 | Exceeds remaining authority | 960.00 | 240.00 | 0.00 |
| AID-03376 | 960.00 | 0.00 | 240.00 | Request new 396.00 | Exceeds remaining authority | 960.00 | 240.00 | 0.00 |
| AID-03377 | 960.00 | 0.00 | 240.00 | Confirm pending 240.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03378 | 960.00 | 0.00 | 240.00 | Fail pending 240.00 | Release pending reservation | 960.00 | 0.00 | 240.00 |
| AID-03379 | 960.00 | 0.00 | 240.00 | Replay settled 960.00 | Original receipt; no new effect | 960.00 | 240.00 | 0.00 |
| AID-03380 | 960.00 | 0.00 | 240.00 | Record return 0.01 | Apply linked return once | 959.99 | 240.00 | 0.01 |
| AID-03381 | 960.00 | 0.00 | 240.00 | Record return 480.00 | Apply linked return once | 480.00 | 240.00 | 480.00 |
| AID-03382 | 960.00 | 0.00 | 240.00 | Record return 960.00 | Apply linked return once | 0.00 | 240.00 | 960.00 |
| AID-03383 | 960.00 | 0.00 | 240.00 | Record return 960.01 | Return exceeds net fulfillment | 960.00 | 240.00 | 0.00 |
| AID-03384 | 960.00 | 0.01 | 0.00 | Request new 240.00 | Reserve once | 959.99 | 240.00 | 0.01 |
| AID-03385 | 960.00 | 0.01 | 0.00 | Request new 240.01 | Reserve once | 959.99 | 240.01 | 0.00 |
| AID-03386 | 960.00 | 0.01 | 0.00 | Request new 240.02 | Exceeds remaining authority | 959.99 | 0.00 | 240.01 |
| AID-03387 | 960.00 | 0.01 | 0.00 | Request new 396.00 | Exceeds remaining authority | 959.99 | 0.00 | 240.01 |
| AID-03388 | 960.00 | 0.01 | 0.00 | Replay settled 960.00 | Original receipt; no new effect | 959.99 | 0.00 | 240.01 |
| AID-03389 | 960.00 | 0.01 | 0.00 | Record return 0.01 | Apply linked return once | 959.98 | 0.00 | 240.02 |
| AID-03390 | 960.00 | 0.01 | 0.00 | Record return 480.00 | Apply linked return once | 479.99 | 0.00 | 720.01 |
| AID-03391 | 960.00 | 0.01 | 0.00 | Record return 959.99 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03392 | 960.00 | 0.01 | 0.00 | Record return 960.00 | Return exceeds net fulfillment | 959.99 | 0.00 | 240.01 |
| AID-03393 | 960.00 | 0.01 | 96.00 | Request new 144.00 | Reserve once | 959.99 | 240.00 | 0.01 |
| AID-03394 | 960.00 | 0.01 | 96.00 | Request new 144.01 | Reserve once | 959.99 | 240.01 | 0.00 |
| AID-03395 | 960.00 | 0.01 | 96.00 | Request new 144.02 | Exceeds remaining authority | 959.99 | 96.00 | 144.01 |
| AID-03396 | 960.00 | 0.01 | 96.00 | Request new 396.00 | Exceeds remaining authority | 959.99 | 96.00 | 144.01 |
| AID-03397 | 960.00 | 0.01 | 96.00 | Confirm pending 96.00 | Settle original once | 1055.99 | 0.00 | 144.01 |
| AID-03398 | 960.00 | 0.01 | 96.00 | Fail pending 96.00 | Release pending reservation | 959.99 | 0.00 | 240.01 |
| AID-03399 | 960.00 | 0.01 | 96.00 | Replay settled 960.00 | Original receipt; no new effect | 959.99 | 96.00 | 144.01 |
| AID-03400 | 960.00 | 0.01 | 96.00 | Record return 0.01 | Apply linked return once | 959.98 | 96.00 | 144.02 |
| AID-03401 | 960.00 | 0.01 | 96.00 | Record return 480.00 | Apply linked return once | 479.99 | 96.00 | 624.01 |
| AID-03402 | 960.00 | 0.01 | 96.00 | Record return 959.99 | Apply linked return once | 0.00 | 96.00 | 1104.00 |
| AID-03403 | 960.00 | 0.01 | 96.00 | Record return 960.00 | Return exceeds net fulfillment | 959.99 | 96.00 | 144.01 |
| AID-03404 | 960.00 | 0.01 | 240.01 | Request new 0.01 | Exceeds remaining authority | 959.99 | 240.01 | 0.00 |
| AID-03405 | 960.00 | 0.01 | 240.01 | Request new 396.00 | Exceeds remaining authority | 959.99 | 240.01 | 0.00 |
| AID-03406 | 960.00 | 0.01 | 240.01 | Confirm pending 240.01 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03407 | 960.00 | 0.01 | 240.01 | Fail pending 240.01 | Release pending reservation | 959.99 | 0.00 | 240.01 |
| AID-03408 | 960.00 | 0.01 | 240.01 | Replay settled 960.00 | Original receipt; no new effect | 959.99 | 240.01 | 0.00 |
| AID-03409 | 960.00 | 0.01 | 240.01 | Record return 0.01 | Apply linked return once | 959.98 | 240.01 | 0.01 |
| AID-03410 | 960.00 | 0.01 | 240.01 | Record return 480.00 | Apply linked return once | 479.99 | 240.01 | 480.00 |
| AID-03411 | 960.00 | 0.01 | 240.01 | Record return 959.99 | Apply linked return once | 0.00 | 240.01 | 959.99 |
| AID-03412 | 960.00 | 0.01 | 240.01 | Record return 960.00 | Return exceeds net fulfillment | 959.99 | 240.01 | 0.00 |
| AID-03413 | 960.00 | 240.00 | 0.00 | Request new 396.00 | Reserve once | 720.00 | 396.00 | 84.00 |
| AID-03414 | 960.00 | 240.00 | 0.00 | Request new 479.99 | Reserve once | 720.00 | 479.99 | 0.01 |
| AID-03415 | 960.00 | 240.00 | 0.00 | Request new 480.00 | Reserve once | 720.00 | 480.00 | 0.00 |
| AID-03416 | 960.00 | 240.00 | 0.00 | Request new 480.01 | Exceeds remaining authority | 720.00 | 0.00 | 480.00 |
| AID-03417 | 960.00 | 240.00 | 0.00 | Replay settled 960.00 | Original receipt; no new effect | 720.00 | 0.00 | 480.00 |
| AID-03418 | 960.00 | 240.00 | 0.00 | Record return 0.01 | Apply linked return once | 719.99 | 0.00 | 480.01 |
| AID-03419 | 960.00 | 240.00 | 0.00 | Record return 360.00 | Apply linked return once | 360.00 | 0.00 | 840.00 |
| AID-03420 | 960.00 | 240.00 | 0.00 | Record return 720.00 | Apply linked return once | 0.00 | 0.00 | 1200.00 |
| AID-03421 | 960.00 | 240.00 | 0.00 | Record return 720.01 | Return exceeds net fulfillment | 720.00 | 0.00 | 480.00 |
| AID-03422 | 960.00 | 240.00 | 192.00 | Request new 287.99 | Reserve once | 720.00 | 479.99 | 0.01 |
| AID-03423 | 960.00 | 240.00 | 192.00 | Request new 288.00 | Reserve once | 720.00 | 480.00 | 0.00 |
| AID-03424 | 960.00 | 240.00 | 192.00 | Request new 288.01 | Exceeds remaining authority | 720.00 | 192.00 | 288.00 |
| AID-03425 | 960.00 | 240.00 | 192.00 | Request new 396.00 | Exceeds remaining authority | 720.00 | 192.00 | 288.00 |
| AID-03426 | 960.00 | 240.00 | 192.00 | Confirm pending 192.00 | Settle original once | 912.00 | 0.00 | 288.00 |
| AID-03427 | 960.00 | 240.00 | 192.00 | Fail pending 192.00 | Release pending reservation | 720.00 | 0.00 | 480.00 |
| AID-03428 | 960.00 | 240.00 | 192.00 | Replay settled 960.00 | Original receipt; no new effect | 720.00 | 192.00 | 288.00 |
| AID-03429 | 960.00 | 240.00 | 192.00 | Record return 0.01 | Apply linked return once | 719.99 | 192.00 | 288.01 |
| AID-03430 | 960.00 | 240.00 | 192.00 | Record return 360.00 | Apply linked return once | 360.00 | 192.00 | 648.00 |
| AID-03431 | 960.00 | 240.00 | 192.00 | Record return 720.00 | Apply linked return once | 0.00 | 192.00 | 1008.00 |
| AID-03432 | 960.00 | 240.00 | 192.00 | Record return 720.01 | Return exceeds net fulfillment | 720.00 | 192.00 | 288.00 |
| AID-03433 | 960.00 | 240.00 | 480.00 | Request new 0.01 | Exceeds remaining authority | 720.00 | 480.00 | 0.00 |
| AID-03434 | 960.00 | 240.00 | 480.00 | Request new 396.00 | Exceeds remaining authority | 720.00 | 480.00 | 0.00 |
| AID-03435 | 960.00 | 240.00 | 480.00 | Confirm pending 480.00 | Settle original once | 1200.00 | 0.00 | 0.00 |
| AID-03436 | 960.00 | 240.00 | 480.00 | Fail pending 480.00 | Release pending reservation | 720.00 | 0.00 | 480.00 |
| AID-03437 | 960.00 | 240.00 | 480.00 | Replay settled 960.00 | Original receipt; no new effect | 720.00 | 480.00 | 0.00 |
| AID-03438 | 960.00 | 240.00 | 480.00 | Record return 0.01 | Apply linked return once | 719.99 | 480.00 | 0.01 |
| AID-03439 | 960.00 | 240.00 | 480.00 | Record return 360.00 | Apply linked return once | 360.00 | 480.00 | 360.00 |
| AID-03440 | 960.00 | 240.00 | 480.00 | Record return 720.00 | Apply linked return once | 0.00 | 480.00 | 720.00 |
| AID-03441 | 960.00 | 240.00 | 480.00 | Record return 720.01 | Return exceeds net fulfillment | 720.00 | 480.00 | 0.00 |
| AID-03442 | 960.00 | 960.00 | 0.00 | Request new 396.00 | Reserve once | 0.00 | 396.00 | 804.00 |
| AID-03443 | 960.00 | 960.00 | 0.00 | Request new 1199.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03444 | 960.00 | 960.00 | 0.00 | Request new 1200.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03445 | 960.00 | 960.00 | 0.00 | Request new 1200.01 | Exceeds remaining authority | 0.00 | 0.00 | 1200.00 |
| AID-03446 | 960.00 | 960.00 | 0.00 | Replay settled 960.00 | Original receipt; no new effect | 0.00 | 0.00 | 1200.00 |
| AID-03447 | 960.00 | 960.00 | 480.00 | Request new 396.00 | Reserve once | 0.00 | 876.00 | 324.00 |
| AID-03448 | 960.00 | 960.00 | 480.00 | Request new 719.99 | Reserve once | 0.00 | 1199.99 | 0.01 |
| AID-03449 | 960.00 | 960.00 | 480.00 | Request new 720.00 | Reserve once | 0.00 | 1200.00 | 0.00 |
| AID-03450 | 960.00 | 960.00 | 480.00 | Request new 720.01 | Exceeds remaining authority | 0.00 | 480.00 | 720.00 |
| AID-03451 | 960.00 | 960.00 | 480.00 | Confirm pending 480.00 | Settle original once | 480.00 | 0.00 | 720.00 |
| AID-03452 | 960.00 | 960.00 | 480.00 | Fail pending 480.00 | Release pending reservation | 0.00 | 0.00 | 1200.00 |
