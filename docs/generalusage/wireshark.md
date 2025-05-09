---
title: Wireshark
parent: General Usage
layout: default
nav_order: 29
---

If is deflate content type, use the following command (pcap_body is the file in raw format when view in wireshark, use hexed.it to save it as a separate file):\
`printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" | cat - pcap_body | gunzip`