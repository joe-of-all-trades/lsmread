# lsmread

LSMREAD returns information and image data of a ZEISS lsm file.

[Data] = lsmread(filename) will return image data in its original
dimensions, organized as [T(ime), C(hannel), Z, X, Y]
[Data] = lsmread(filename,'Range',[T0 T1 C0 C1 Z0 Z1]) will return image data with specified dimension. 
[Data LSMinfo] = lsmread(filename) will return image data as well as LSMinfo
[LSMinfo] = lsmread(filename,'InfoOnly') will only return LSM infos. 
---------------------------------------------------------------------------------
Notes for the Zeiss LSM format. 
The first 8 bytes are TIFF file header. 
Each 12-byte IFD entry has the following format: Bytes 0-1: The Tag that
identifies the field. Byte 2-3: The field type. Bytes 4-7: Count. 
Bytes 8-11: Value or offset.Byte count of the indicated types. 
Types 1 = BYTE, 2 =ASCII (8-bit),3= SHORT (16-bit), 4= LONG(32-bit).  
If the count is 1, then byes 8-11 stores the value, otherwise it's offset
pointing to the position in file where value is stored. 
Each optical section at every time point (no matter how many channels) 
will have two image file directories(IFDs). The first one contains 
information for the real image data. The second IFD contains 
information for thumbnail images. The LSM file is structured as such : 
header -> IFDs -> (real image/thumbnail)s. 
The very first IFD has an entry numbered 34412 and points to LSM-specific data. 
----------------------------------------------------------------------------------
Version 1.7
Copyright Chao-Yuan Yeh, 2016. 
The script is inspired by LSM File Toolbox by Peter Li and tiffrd by Francois Nedelec.
