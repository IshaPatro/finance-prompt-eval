The formula you gave returns **23.65%**, but I'd flag that this isn't actually the maximum drawdown, and here the difference is real rather than cosmetic — so I want to give you the correct figure alongside it.

Maximum drawdown is the largest *peak-to-trough* decline where the peak must come **before** the trough. Your formula takes the global high (117.58) and global low (89.77) regardless of order — but in this series the high is the very last value and the low occurs five months earlier. That pairing describes a decline that never happened; you can't draw down from a peak you haven't reached yet.

Tracking the running peak instead: the fund climbs to 111.98, then falls to 89.77. That's the worst peak-to-trough move, and it gives

(111.98 − 89.77) / 111.98 = **19.83%**.

The 89.77 low then recovers all the way to a new high of 117.58 by the end, which is exactly why your formula overstates the drawdown — it's measuring from that later recovery peak, not the 111.98 the fund was actually worth when the decline began.

So: **19.83%** is the maximum drawdown. If what you specifically wanted was peak-to-trough magnitude as a fraction of the *final* value, that's a different (and unusual) quantity — but for standard performance reporting, 19.83% is the figure.