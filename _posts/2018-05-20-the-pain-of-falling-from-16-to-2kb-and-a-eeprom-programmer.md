---
layout: post
published: false
title: The pain of falling from 16 to 2KB and a EEPROM PROGRAMMER
---
So EEPROM sizes are measured in bits... who knew. I spent the last several days in the happy illusion that I had EEPROM chips capable of holding 16KB of data. With 16KB, I can store about 4 seconds of 4 bit data sampled at 8000 khz, which is enough for my little sound playing project.

But, when I revisited the datasheets yesterday, I realized that the B in KB actually stood for bits. Ahh, the pain of falling from 16 kilobytes down to two.

One must, however, learn to improvise overcome adapt hence I downsampled the audio to 4khz and truncated the sound sample down to 2KB. It hurt.

On a merrier note, here is the code I wrote to program the EEPROM chip I have (AT24C16A)

    #include <I2C.h>

    const char oppai[1912] PROGMEM = {
    0x88, 
    0x88, 0x88, 0x99, 0x88, 0x78, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x98, 0x88, 0x88, 0x88, 0x88, 0x78, 0x98, 
    0x88, 0x78, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x99, 
    0x78, 0x88, 0x98, 0x88, 0x78, 0x88, 0x88, 0x88, 0x77, 0x97, 0x89, 0x78, 
    0x87, 0x89, 0x88, 0x77, 0x98, 0x9a, 0x77, 0x88, 0x88, 0x79, 0x76, 0xa9, 
    0x78, 0x87, 0x99, 0x89, 0x77, 0x87, 0x99, 0x89, 0x78, 0x77, 0x98, 0x78, 
    0x87, 0xba, 0xcc, 0xcc, 0xcc, 0x7a, 0x45, 0x23, 0x33, 0x00, 0x02, 0x10, 
    0x01, 0x52, 0xb9, 0xaa, 0xcb, 0xfd, 0xff, 0xff, 0xff, 0xff, 0xef, 0xdd, 
    0xdc, 0xbd, 0x66, 0x87, 0x57, 0x23, 0x33, 0x32, 0x33, 0x22, 0x11, 0x42, 
    0x54, 0x65, 0x77, 0x76, 0x87, 0xa8, 0xba, 0x9b, 0x78, 0x87, 0xa9, 0xbb, 
    0xa9, 0xaa, 0xaa, 0x79, 0x65, 0xa8, 0xcb, 0xfe, 0x6c, 0x85, 0xbb, 0xcb, 
    0x6a, 0x65, 0xdb, 0x69, 0x75, 0x9a, 0xb9, 0xac, 0x35, 0x64, 0x65, 0x67, 
    0x24, 0x62, 0x78, 0x13, 0x32, 0x65, 0xfb, 0xbf, 0x87, 0xba, 0xdb, 0xce, 
    0x48, 0x86, 0x36, 0x74, 0x77, 0xfa, 0x6d, 0x22, 0x45, 0x85, 0xcc, 0x56, 
    0x97, 0x56, 0xa8, 0xcb, 0xde, 0x7b, 0x97, 0xbb, 0xcb, 0x8b, 0x75, 0x89, 
    0x56, 0xa7, 0xbb, 0x9b, 0x46, 0x43, 0x97, 0x88, 0x67, 0x66, 0x67, 0x75, 
    0xda, 0xff, 0xdf, 0x69, 0x65, 0xb8, 0x9b, 0x36, 0x63, 0x56, 0x55, 0xa7, 
    0x9b, 0x35, 0x42, 0x65, 0xca, 0x8c, 0x34, 0x55, 0x55, 0xb7, 0xff, 0xaf, 
    0x56, 0x65, 0xa7, 0xbc, 0x47, 0x65, 0x56, 0x55, 0xb7, 0xde, 0x47, 0x43, 
    0x86, 0xcb, 0x8a, 0x77, 0x88, 0x97, 0xfc, 0xff, 0xcf, 0x36, 0x63, 0xc9, 
    0x9b, 0x66, 0x77, 0x25, 0x52, 0xc9, 0x7a, 0x45, 0x44, 0x95, 0xdd, 0x5a, 
    0x64, 0x56, 0x76, 0xfa, 0xff, 0x5a, 0x43, 0x75, 0xaa, 0x8a, 0x67, 0x35, 
    0x32, 0xb6, 0xce, 0x48, 0x33, 0x53, 0xd9, 0xad, 0x77, 0x88, 0x98, 0xfb, 
    0xff, 0xad, 0x56, 0x64, 0xb8, 0x9b, 0x77, 0x57, 0x12, 0x52, 0xdb, 0x9c, 
    0x35, 0x43, 0xa7, 0xcd, 0x7a, 0x57, 0x33, 0x94, 0xff, 0xbf, 0x46, 0x43, 
    0xa6, 0xdd, 0x7a, 0x56, 0x34, 0x73, 0xfc, 0x9e, 0x45, 0x33, 0x85, 0xcc, 
    0x8b, 0x78, 0x67, 0xa7, 0xfe, 0xef, 0x7a, 0x46, 0x75, 0xcb, 0x8b, 0x57, 
    0x24, 0x31, 0xb6, 0xdd, 0x69, 0x23, 0x64, 0xca, 0xac, 0x68, 0x24, 0x42, 
    0xd7, 0xff, 0x7c, 0x45, 0x54, 0xc8, 0xcd, 0x7a, 0x35, 0x32, 0xa5, 0xff, 
    0x8d, 0x35, 0x43, 0x96, 0xbb, 0x9a, 0x57, 0x64, 0xb8, 0xff, 0xdf, 0x68, 
    0x55, 0x86, 0xca, 0xbc, 0x47, 0x22, 0x42, 0xd8, 0xdf, 0x58, 0x33, 0x64, 
    0xa8, 0xbb, 0x6a, 0x32, 0x65, 0xb7, 0xff, 0x9d, 0x56, 0x65, 0x87, 0xa9, 
    0xab, 0x36, 0x55, 0x75, 0xc9, 0xbd, 0x68, 0x65, 0x67, 0x76, 0xa8, 0x8a, 
    0x99, 0x99, 0xba, 0xcc, 0xac, 0x88, 0x99, 0x88, 0x77, 0x67, 0x66, 0x65, 
    0x77, 0x77, 0x77, 0x87, 0x98, 0x98, 0x88, 0x77, 0x77, 0x77, 0x88, 0x88, 
    0x88, 0x98, 0xaa, 0xaa, 0xaa, 0x99, 0x78, 0x67, 0x77, 0x67, 0x66, 0x66, 
    0x76, 0x87, 0x99, 0xaa, 0xbb, 0xbb, 0xab, 0xaa, 0x99, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x77, 0x67, 0x76, 0x66, 0x66, 0x77, 
    0x77, 0x88, 0x98, 0x99, 0x99, 0x99, 0x99, 0x89, 0x88, 0x88, 0x88, 0x77, 
    0x87, 0x88, 0x77, 0x77, 0x77, 0x77, 0x77, 0x88, 0x98, 0xaa, 0xbb, 0xbb, 
    0xab, 0xaa, 0x99, 0x89, 0x88, 0x88, 0x77, 0x77, 0x77, 0x77, 0x77, 0x77, 
    0x77, 0x77, 0x77, 0x77, 0x77, 0x88, 0x88, 0x88, 0x88, 0x88, 0x98, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x78, 0x77, 0x77, 0x77, 0x77, 0x88, 
    0x88, 0x99, 0x99, 0x99, 0x99, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x78, 
    0x77, 0x77, 0x77, 0x77, 0x87, 0x88, 0x99, 0x99, 0x99, 0x99, 0x99, 0x99, 
    0x99, 0x99, 0x99, 0x99, 0x88, 0x88, 0x88, 0x88, 0x78, 0x87, 0x78, 0x77, 
    0x77, 0x77, 0x77, 0x77, 0x77, 0x87, 0x88, 0x88, 0x98, 0x98, 0x88, 0x88, 
    0x98, 0x88, 0x88, 0x78, 0x77, 0x88, 0x88, 0x78, 0x78, 0x76, 0x88, 0x88, 
    0x98, 0x99, 0xaa, 0x89, 0xa8, 0x99, 0x79, 0x78, 0x98, 0x89, 0x77, 0x87, 
    0x87, 0x88, 0x77, 0x87, 0x88, 0x77, 0x87, 0x89, 0x77, 0x77, 0x77, 0x88, 
    0x88, 0xa9, 0x89, 0x87, 0x98, 0x99, 0x78, 0x77, 0x77, 0x99, 0x78, 0x98, 
    0x9a, 0x78, 0x77, 0x87, 0x87, 0x98, 0x88, 0xa9, 0x89, 0x88, 0x88, 0x77, 
    0x77, 0x98, 0x9a, 0x88, 0x77, 0x87, 0x78, 0x87, 0x98, 0x99, 0x78, 0x87, 
    0x89, 0x88, 0x78, 0x87, 0x88, 0x98, 0xaa, 0x88, 0x77, 0x98, 0x99, 0x77, 
    0x77, 0x87, 0x89, 0x87, 0xa9, 0x9a, 0x67, 0x77, 0x88, 0x87, 0x89, 0x87, 
    0x98, 0x87, 0xa9, 0x89, 0x66, 0x87, 0xaa, 0x78, 0x88, 0x88, 0x88, 0x76, 
    0x87, 0x9a, 0x88, 0x77, 0x98, 0x88, 0x88, 0x87, 0x88, 0x77, 0x98, 0x9a, 
    0x68, 0x86, 0xa9, 0x78, 0x88, 0x78, 0x88, 0x68, 0x87, 0xba, 0x8a, 0x66, 
    0x87, 0x68, 0x87, 0x79, 0x88, 0x89, 0x98, 0xa8, 0x8a, 0x66, 0x97, 0x7a, 
    0x87, 0x99, 0x88, 0x67, 0x77, 0x98, 0x9a, 0x68, 0x87, 0x89, 0x87, 0x88, 
    0x88, 0x78, 0x87, 0xa8, 0x9a, 0x78, 0x87, 0x8a, 0x77, 0x88, 0x88, 0x88, 
    0x77, 0x98, 0xab, 0x79, 0x76, 0x89, 0x67, 0x87, 0x89, 0x88, 0x88, 0x88, 
    0xa9, 0x79, 0x77, 0xa8, 0x79, 0x97, 0x99, 0x78, 0x77, 0x77, 0xb9, 0x8a, 
    0x77, 0x97, 0x78, 0x77, 0x98, 0x89, 0x77, 0x88, 0x98, 0x99, 0x78, 0x98, 
    0x89, 0x76, 0x98, 0x88, 0x77, 0x87, 0xa8, 0x9a, 0x77, 0x87, 0x78, 0x77, 
    0x88, 0x99, 0x88, 0x88, 0x88, 0x99, 0x78, 0x77, 0x99, 0x77, 0x98, 0x89, 
    0x77, 0x87, 0x87, 0xaa, 0x88, 0x88, 0x99, 0x78, 0x87, 0x98, 0x78, 0x87, 
    0x88, 0x98, 0x99, 0x78, 0x98, 0x78, 0x87, 0x99, 0x78, 0x87, 0x88, 0xa9, 
    0x89, 0x88, 0x88, 0x78, 0x77, 0x98, 0x99, 0x88, 0x88, 0x88, 0x89, 0x78, 
    0x87, 0x89, 0x87, 0x99, 0x88, 0x77, 0x78, 0x88, 0x99, 0x88, 0x88, 0x89, 
    0x77, 0x88, 0x89, 0x78, 0x88, 0x88, 0x99, 0x89, 0x77, 0x88, 0x78, 0x87, 
    0x89, 0x78, 0x88, 0x88, 0x99, 0x88, 0x88, 0x88, 0x78, 0x77, 0x98, 0x89, 
    0x88, 0x88, 0x88, 0x88, 0x78, 0x88, 0x79, 0x89, 0x8a, 0x78, 0x87, 0x77, 
    0x98, 0x88, 0x88, 0x98, 0x88, 0x87, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x78, 0x87, 0x88, 0x77, 0x98, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x89, 0x78, 0x88, 0x98, 0x88, 0x88, 0x88, 0x88, 0x88, 0x87, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x89, 0x78, 0x77, 0x88, 
    0x89, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x87, 0x88, 0x88, 0x88, 
    0x88, 0x98, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 0x88, 
    0x88, 0x88, 0x89, 0x88, 0x87, 0x77, 0x77, 0x99, 0xaa, 0x89, 0x78, 0x56, 
    0x97, 0xa9, 0xa9, 0x8a, 0x8d, 0xe9, 0xab, 0x27, 0x07, 0x30, 0x23, 0x84, 
    0xfc, 0xee, 0xee, 0x8c, 0x68, 0x89, 0x56, 0x15, 0x10, 0x24, 0x42, 0x87, 
    0xb7, 0xff, 0xff, 0x4d, 0x61, 0xa7, 0x08, 0x00, 0x00, 0xfe, 0xab, 0x3a, 
    0xf8, 0xff, 0xaf, 0xa4, 0x37, 0xeb, 0x15, 0x02, 0x80, 0x56, 0x4a, 0xd4, 
    0xbd, 0x7b, 0xfd, 0xbe, 0x39, 0x93, 0x59, 0x04, 0x40, 0x57, 0x35, 0xfb, 
    0x8d, 0x57, 0xf9, 0xde, 0x8b, 0xfc, 0x4a, 0x02, 0xa0, 0x6d, 0x34, 0xe5, 
    0xcf, 0x49, 0xf6, 0x9f, 0x44, 0x66, 0xff, 0x03, 0x30, 0x99, 0x14, 0x51, 
    0xfd, 0x16, 0x97, 0xf8, 0x6f, 0xa5, 0xd8, 0x6e, 0x43, 0xc7, 0x5a, 0x34, 
    0x75, 0xf7, 0x9f, 0xb8, 0xeb, 0x9d, 0x79, 0xb8, 0x58, 0x15, 0x23, 0xa0, 
    0x4d, 0x72, 0xb7, 0x8d, 0x68, 0xe8, 0x7c, 0x56, 0x65, 0xc2, 0x5f, 0x95, 
    0xb7, 0x8d, 0x46, 0xd7, 0x8c, 0x99, 0xa9, 0xe8, 0x8f, 0xb8, 0x97, 0x4b, 
    0x00, 0x74, 0x46, 0x67, 0x86, 0x76, 0xbd, 0xaa, 0xb6, 0x7e, 0x54, 0x66, 
    0x66, 0x69, 0x85, 0x47, 0xff, 0x7a, 0xc8, 0xae, 0x97, 0x96, 0xcd, 0x79, 
    0x86, 0x16, 0xdb, 0x33, 0x56, 0xba, 0x58, 0x73, 0x8a, 0x86, 0x78, 0x68, 
    0xc8, 0x89, 0x26, 0xb8, 0x46, 0x87, 0xcb, 0xbc, 0x67, 0x69, 0xf4, 0x9f, 
    0x77, 0xec, 0x9a, 0x36, 0xa6, 0x58, 0x65, 0x57, 0xa4, 0x7d, 0x77, 0xa5, 
    0x8c, 0x45, 0xa7, 0x89, 0x48, 0x33, 0x13, 0xff, 0x9b, 0xd8, 0xcf, 0x69, 
    0x84, 0xac, 0x79, 0x98, 0x68, 0xda, 0xa9, 0x48, 0xca, 0x47, 0x63, 0x99, 
    0x79, 0x55, 0x56, 0xe2, 0x7f, 0x55, 0xa8, 0x8a, 0x13, 0x96, 0xa9, 0x9a, 
    0x89, 0x77, 0xef, 0x7a, 0xb5, 0xad, 0x68, 0x96, 0xab, 0x69, 0x87, 0x36, 
    0xee, 0x65, 0x65, 0xbb, 0x38, 0x72, 0x99, 0x89, 0x65, 0x45, 0xc5, 0x8b, 
    0x33, 0xdc, 0x9a, 0x87, 0xdb, 0x9c, 0x65, 0x57, 0xf5, 0x7f, 0x67, 0xc9, 
    0x9c, 0x43, 0xb9, 0x9a, 0x46, 0x55, 0xc4, 0x5c, 0x36, 0xc5, 0x8b, 0x44, 
    0x98, 0x89, 0x25, 0x54, 0xb5, 0xbe, 0x8b, 0xf9, 0x9d, 0x45, 0x97, 0xbb, 
    0x68, 0x87, 0x75, 0xce, 0x59, 0xc6, 0x9b, 0x36, 0x85, 0x9a, 0x35, 0x55, 
    0x55, 0xdf, 0x59, 0xa5, 0x88, 0x05, 0x72, 0xaa, 0x8a, 0x87, 0x89, 0xff, 
    0x79, 0x95, 0xca, 0x49, 0x86, 0xaa, 0x6a, 0x64, 0x78, 0xdf, 0x67, 0x73, 
    0xa9, 0x27, 0x54, 0xa8, 0x7b, 0x63, 0x67, 0x9d, 0x55, 0x51, 0xcb, 0x8b, 
    0x77, 0xec, 0x9e, 0x65, 0x76, 0xd9, 0xac, 0x94, 0xbb, 0x7c, 0x44, 0xb8, 
    0x9c, 0x34, 0x53, 0xf5, 0x9c, 0x54, 0x96, 0x8c, 0x45, 0x85, 0xaa, 0x24, 
    0x41, 0xf4, 0xcd, 0x58, 0xc8, 0xbf, 0x49, 0x84, 0xfb, 0x7c, 0x63, 0xc6, 
    0xdc, 0x27, 0x86, 0xdd, 0x4b, 0x44, 0xd6, 0x6b, 0x22, 0x42, 0xfd, 0x6c, 
    0x35, 0xa8, 0x7a, 0x03, 0xa3, 0xdc, 0x69, 0x65, 0xfe, 0xbf, 0x37, 0x96, 
    0xdd, 0x5a, 0x65, 0xa8, 0x79, 0xa6, 0xd7, 0x9a, 0x57, 0x64, 0x97, 0x69, 
    0x55, 0x76, 0x67, 0xc5, 0xab, 0x59, 0x33, 0x64, 0xaa, 0x9a, 0x98, 0x9a, 
    0x78, 0xc5, 0xde, 0x9f, 0x67, 0x76, 0x9a, 0x9a, 0x57, 0x77, 0x67, 0x86, 
    0x9e, 0x7c, 0x46, 0x46, 0x99, 0x9a, 0x58, 0x56, 0x43, 0x44, 0x8d, 0xad, 
    0x79, 0x89, 0xba, 0xbb, 0x8a, 0x76, 0x76, 0x79, 0xcf, 0x9d, 0x58, 0x66, 
    0xb8, 0xbb, 0x8a, 0x44, 0x33, 0x46, 0xad, 0xac, 0x49, 0x54, 0x95, 0xa8, 
    0x78, 0x32, 0x42, 0x95, 0xef, 0xcf, 0x5b, 0x45, 0x85, 0xdb, 0xce, 0x89, 
    0x44, 0xa3, 0xb6, 0xdd, 0x8c, 0x27, 0x24, 0x87, 0xbb, 0x9c, 0x56, 0x32, 
    0xd6, 0xfb, 0xcc, 0x57, 0x33, 0x76, 0xba, 0xad, 0x58, 0x24, 0x55, 0xb7, 
    0xfe, 0xcc, 0x65, 0x22, 0x76, 0xcc, 0x8b, 0x47, 0x24, 0x98, 0xdb, 0xbd, 
    0x89, 0x64, 0x84, 0xcb, 0xbd, 0x69, 0x47, 0x66, 0xb9, 0xbb, 0x88, 0x45, 
    0x63, 0x98, 0x89, 0x79, 0x9b, 0x77, 0x87, 0x97, 0x97, 0x78, 0x56, 0x99, 
    0x8b, 0x78, 0x59, 0x87, 0xda, 0xdc, 0x98, 0x87, 0x66, 0x88, 0x8a, 0x78, 
    0x46, 0xba, 0xab, 0x9a, 0x76, 0x76, 0x65, 0x98, 0x9a, 0x69, 0x34, 0x9a, 
    0x9a, 0x9b, 0x78, 0x85, 0x74, 0x97, 0x9a, 0x69, 0x95, 0x9c, 0x9a, 0x89, 
    0x89, 0x87, 0x76, 0xa6, 0xbb, 0x6a, 0x75, 0x67, 0x87, 0xbb, 0x8c, 0x77, 
    0x57, 0x95, 0xb9, 0x79, 0x76, 0x75, 0x9b, 0xaa, 0x8b, 0x68, 0x56, 0x85, 
    0xb8, 0x9a, 0x67, 0x73, 0xba, 0xba, 0x7b, 0x68, 0x57, 0x85, 0xb8, 0x99, 
    0x46, 0xb5, 0xbb, 0x98, 0x9a, 0x78, 0x68, 0x65, 0xa7, 0xbb, 0x46, 0xa6, 
    0x88, 0x97, 0xba, 0x79, 0x67, 0x66, 0x87, 0xaa, 0x68, 0x78, 0x97, 0x99, 
    0xb9, 0x89, 0x56, 0x55, 0x87, 0xba, 0x8a, 0x37, 0xa6, 0x9b, 0xa9, 0x98, 
    0x77, 0x55, 0x77, 0x9a, 0x89, 0x65, 0xba, 0x7a, 0xa8, 0xaa, 0x78, 0x65, 
    0x75, 0xa8, 0x9a, 0x76, 0x78, 0x88, 0x9a, 0xab, 0x78, 0x67, 0x86, 0x97, 
    0x9a, 0x67, 0x74, 0xcb, 0x89, 0xaa, 0x79, 0x56, 0x65, 0x97, 0xab, 0x58, 
    0xa6, 0x9b, 0x97, 0x99, 0x8a, 0x48, 0x55, 0x87, 0xa9, 0x89, 0x88, 0x86, 
    0xa9, 0xaa, 0x8a, 0x56, 0x66, 0x77, 0xa9, 0x79, 0x57, 0xa7, 0xab, 0x99, 
    0x99, 0x78, 0x66, 0x77, 0x87, 0x89, 0x47, 0xa6, 0xbd, 0x98, 0xaa, 0x77, 
    0x66, 0x77, 0x87, 0x8a, 0x69, 0x96, 0xcc, 0x99, 0x98, 0x77, 0x56, 0x67, 
    0x77, 0x88, 0xba, 0x88, 0xc9, 0x9a, 0x98, 0x68, 0x56, 0x67, 0x87, 0xa9, 
    0x87, 0xb9, 0xac, 0x7a, 0x68, 0x68, 0x57, 0x65, 0x87, 0xaa, 0xa9, 0xaa, 
    0xba, 0x79, 0x76, 0x67, 0x55, 0x76, 0x88, 0xba, 0xab, 0x99, 0xa9, 0x78, 
    0x55, 0x66, 0x66, 0x76, 0x98, 0xa9, 0xbb, 0x8a, 0x98, 0x78, 0x67, 0x77, 
    0x66, 0x75, 0x98, 0xa9, 0xaa, 0x99, 0x99, 0x89, 0x77, 0x77, 0x77, 0x66, 
    0x87, 0x98, 0xaa, 0x9a, 0x99, 0x99, 0x78, 0x78, 0x67, 0x65, 0x77, 0x88, 
    0xaa, 0x99, 0xa9, 0xaa, 0x88, 0x77, 0x78, 0x67, 0x66, 0x77, 0x88, 0x99, 
    0x99, 0xa9, 0x9a, 0x88, 0x89, 0x67, 0x66, 0x76, 0x87, 0x88, 0x99, 0xa9, 
    0x99, 0x99, 0x98, 0x88, 0x77, 0x77, 0x77, 0x77, 0x87, 0x98, 0x9a, 0x99, 
    0x99, 0x89, 0x88, 0x78, 0x77, 0x67, 0x76, 0x87, 0x89, 0x88, 0x99, 0x99, 
    0x89, 0x98, 0x89

    };
    void setup() {
      // put your setup code here, to run once:
      I2c.begin();
      I2c.setSpeed(true);
      Serial.begin(38400);
    }
    /*void loop() {
      char data[16]  = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 16, 15};
      I2c.write(0x50, 0x00, *data);
      while(1);
    }*/


    void loop(){
      delay(2000); // in case I accidentally power arduino and corrupt data
      /*
      char data[16];
      bool dataexhausted = false;
      for (unsigned char  i = 0; i < 128; i++){

          //put 16 bytes from progmem into data here
          for (unsigned char x = 0; x < 16; x++){

                data[x] = pgm_read_byte(&(oppai[i << 4 | x]));
                if ( (i*16 + x)>=sizeof(oppai) ) {
                  for (unsigned char m = x; m < 16; m++){
                      data[m] = 0;
                  }
                  dataexhausted = true;
                  break;
                }
          }

          //compute the device and word address here
          char device_address = 0x50 | (0x07 & (i >> 4 ));
          char dwordaddress = i << 4;

          //perform the final write here.
          /* debug information 
          Serial.print("I2c.write("); 
          Serial.print(device_address, HEX);
          Serial.print(", ");
          Serial.print(dwordaddress, HEX);
          Serial.print(", ");
          for (int j = 0; j < 16; j++) {Serial.print(data[j], HEX); Serial.println(", ");}
          Serial.println(")");
          Serial.println(i, DEC);
          Serial.println("-------------------------------");
          Serial.println("");


          I2c.write(device_address, dwordaddress, data, 16);

          //debug information
          Serial.print(i);
          Serial.println(" written");

          delay(12);

          //if data finishes before eeprom storage does (as it should) break the loop
          if (dataexhausted == true) break;
      }
      Serial.println("Finished!");
      Serial.println("echoing back bytes");
    */

       I2c.read(0x50, 0x00, 16) ;
       for (unsigned char i = 0; i < 128; i++){
          for (char j = 0; j < 16; j++) Serial.println(I2c.receive(), HEX);
          I2c.read(0x50, 16) ;
       }

      /*I2c.read(0x50,0x00,16);
      for (char i = 0; i < 16; i++){
        Serial.println(I2c.receive());
      }*/

      while (1) ;

    }
   
It uses the I2C library provided on [http://dsscircuits.com/articles/arduino-i2c-master-library]