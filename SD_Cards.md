# A Summary of SD Card Specifications:

The following is derived from a [video](https://youtu.be/oLQ8A_vcBqU) on the
channel
[Explaining Computers](https://www.youtube.com/channel/UCbiGcwDWZjz05njNPrJU7jA).
A channel with video so awesomely good and useful that I felt compelled to take
notes for future reference. This document is one such case where the best
explanation of SD cards ever is summarized.

## Card Form Factors:

Over the years, different SD card form factors have been introduced:

Year   | Type              | Status             |
-------|-------------------|--------------------|
2000   | Standard SD cards | Older, less common |
2003   | Mini SD cards     | Extinct            |
2005   | Micro SD cards    | Ubiquitous         |

## Card Storage Capacity:

Type                      | Maximum Capacity  |
--------------------------|:-----------------:|
SD                        | 2G                |
SD HC (High Capacity)     | 32G               |
SD XC (Extended Capacity) | 2T                |
SD UC (Ultra Capacity)    | 128T              |

## Card Write Speed:

Since SD cards are often associated with cameras, the devices write speed is
the most important specification in that application.

MB/s| Speed Class | UHS Speed | Video Speed  |
----|:-----------:|:---------:|:------------:|
90  |             |           |     V90      |
60  |             |           |     V60      |
30  |             |     U3    |     V30      |
10  |    C10      |     U1    |     V10      |
6   |    C6       |     V6    |              |
4   |    C4       |           |              |
2   |    C2       |           |              |

## Application Rating:

As SD cards are moving into applications beyond cameras, other aspects of
performance beyond brute write speed become important. This results in an
application rating.

Rating |Read IOPS |Write IOPS | Write Speed |
-------|:--------:|:---------:|:-----------:|
A1     |   1500   |     500   |    >10      |
A2     |   4000   |    1000   |    >10      |

## Bus Interface Ratings:

Finally, the interface between the host system and the SD device has undergone
a few revisions.

Interface  | Bus Speed MB/s | Connection | Status       |
-----------|:--------------:|------------|--------------|
High Speed |       25       |  Standard  |      OK      |
UHS-I      |      104       |  Standard  |      OK      |
UHS-II     |      312       |    2 Rows  |      OK      |
UHS-III    |      624       |    2 Rows  | Not adopted? |
SD Express |      985       |    2 Rows  | Leading edge |

