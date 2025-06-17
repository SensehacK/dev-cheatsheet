

## Encoding

For all Apple devices, the streaming format should be HLS `m3u8` with `cbcs` encryption.  
i.e. `https://sle1--prd-ak-azukw``.``cdn01.sa.com/v2/bmff/cbcs/t/sa:e1cc88cc-6717-4120-9cac-6b01345520d1_GB.m3u8`
For the Safari web browser, the streaming format should be DASH `mpd` with `cbcs` encryption.  
i.e. `https://-prd-ak-azukw``.``cdn01.asa.com/v2/bmff/cbcs/t/asfa:e1cc88cc-6717-4120-9cac-6b013455sda.mpd`For all other devices (including web browsers), the streaming format should be DASH `mpd` with `cenc` encryption.  
i.e. `https://sleprd-ak-azukw``.``cdn01.sae.com/v2/bmff/cenc/t/a3r3:e1cc88cc-6717-4120-9cac-6b0sd.mpd`If there are issues with playback we need to work with the player team to help resolve them.