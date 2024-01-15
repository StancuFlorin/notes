---
title: "How to upgrade your Fujitsu Esprimo Q558 with 2 SATA3 SSDs"
date: 2024-01-15
---

This tutorial demonstrates how to install two additional SATA3 SSDs on your Fujitsu Esprimo Q558 mini PC without the need for costly OEM cables, which Fujitsu typically charges around $45 for each.

- T26139-Y4033-H103 (HDD / SSD SATA3 and power cable)
- T26139-Y4033-H3 (Optical Drive SATA3 and power cable)

![fujitsu-sata-oem-cables](/assets/img/posts/fujitsu_sata/fujitsu-sata-oem-cables.png)

The sole substitute I discovered in the market for the OEM cables are cables designed for linking SSDs to BananaPi devices. You can find Chinese versions on AliExpress, or opt for premium cables from Delock, priced at approximately $5 each.

- Delock 85238 (10cm version)
- Delock 85242 (30cm version)

![delock-sata-cable](/assets/img/posts/fujitsu_sata/delock-sata-cable.jpg)

The only caveat is that you'll have to modify the power connector to make it compatible with the Fujitsu motherboard.

![motherboard_power_pins](/assets/img/posts/fujitsu_sata/motherboard_power_pins.jpeg)

The brief 10cm cable will be utilized for the HDD bay. Although the motherboard has 3 pins, the 12V will remain unused, as all SSDs operate solely on 5V (as do most 2.5" HDDs). To connect the Delock connector, I had to interchange the red and black wires.

The second SSD will be positioned in the Optidal Drive area and linked with the 30cm cable. I needed to drill two holes to secure it in place (alternatively, double-sided adhesive tape can suffice), and with the help of a Dremel, I trimmed a small section of the optical drive support to accommodate the wires.

![IMG_9724](/assets/img/posts/fujitsu_sata/IMG_9724.jpeg)
![IMG_9726](/assets/img/posts/fujitsu_sata/IMG_9726.jpeg)
![IMG_9728](/assets/img/posts/fujitsu_sata/IMG_9728.jpeg)
![IMG_9730](/assets/img/posts/fujitsu_sata/IMG_9730.jpeg)
![IMG_9733](/assets/img/posts/fujitsu_sata/IMG_9733.jpeg)
![IMG_9732](/assets/img/posts/fujitsu_sata/IMG_9732.jpeg)
![IMG_9700](/assets/img/posts/fujitsu_sata/IMG_9700.jpeg)

While the power connectors may not be an exact 100% match, they are currently functioning effectively (until the accurate connectors will be shipped).

- 3 pin connector // [171822-3](https://www.digikey.ro/en/products/detail/te-connectivity-amp-connectors/171822-3/744756)
- 2 pin connector // [171822-2](https://www.digikey.ro/en/products/detail/te-connectivity-amp-connectors/171822-2/2187783)

![Screenshot 2024-01-15 132852](/assets/img/posts/fujitsu_sata/Screenshot 2024-01-15 132852.png)
