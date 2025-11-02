---
created: 2025-10-16
updated: 2025-10-17
topic: dynamic power load balancer myth
tags: [hallucination, ai, electrical]
---

# Hallucination: Dynamic Power Load Balancer

I asked ChatGPT how to safely power multiple high-draw kitchen appliances when I only had two 16A circuits available. It recommended a so-called “dynamic power load balancer” that would split power across the appliances, capping each line at 16 amps.

The response went further, inventing a shopping list with manufacturer names, model numbers, and spec sheets for devices that supposedly perform this automatic balancing. None of them exist. Searching for the cited models turns up nothing, and electricians I checked with confirmed there is no off‑the‑shelf gadget that safely shares a single circuit this way. There are priority controllers that can cut power to a secondary appliance once the primary load approaches 16A, but they do not magically split 16A into two steady 8A feeds, which is what ChatGPT imagined.

When I pressed for what would happen if I cranked both the oven and the stovetop to max, the assistant doubled down. It claimed a “smart” touch-screen oven would gracefully detect the low current and shut itself down, while a “dumb” analog oven would just heat up more slowly. We can’t even test the scenario because the “dynamic balancer” does not exist, and starving an appliance of current does not have a predictable, tidy outcome. Some hardware might throw error codes, some might limp along and fail to reach temperature, and others could behave erratically.