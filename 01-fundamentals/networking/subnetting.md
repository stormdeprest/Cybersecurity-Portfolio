# Subnetting Step-by-Step Guide

## Given Information

- IP Address: `182.211.89.2/17`
    
- Subnet Mask: `/17` → `255.255.128.0` (binary: `11111111.11111111.10000000.00000000`)
    

## Step 1: Determine Block Size

Look at the first octet that is not 255 → in this case, the third octet = 128

256−128=128256−128=128

Therefore, block size = **128** in the third octet.

## Step 2: Find the Subnet

Third octet of IP = 89

Blocks in that octet: 0–127, 128–255, …

89 falls within the **0–127** range

👉 Network address = **182.211.0.0**

## Step 3: Calculate Broadcast Address

Next block starts at 128 → broadcast = 128 − 1 = 127 in that octet

Therefore, broadcast address = **182.211.127.255**

## Summary

- **Network Address:** `182.211.0.0/17`
    
- **Broadcast Address:** `182.211.127.255`
    
- **Usable IP Range:** `182.211.0.1` - `182.211.127.254`