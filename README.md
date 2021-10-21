# Rotation Matrix to Euler Angles (RM2EA)

`RM2EA` is a function defined to convert a standard 3 x 3 rotation matrix into its Euler angle (i.e. roll, pitch, yaw) equivalent. This function is based upon [Computing Euler angles from a rotation matrix](https://github.com/Tinker-Twins/RM2EA/blob/main/RM2EA.pdf) by Gregory G. Slabaugh.

## Definition
```python
import numpy as np
import math

def isClose(x, y, rtol=1.e-5, atol=1.e-8):
    return abs(x-y) <= atol + rtol * abs(y)
    
def RM2EA(R):
    phi = 0.0
    if isClose(R[2,0],-1.0):
        theta = math.pi/2.0
        psi = math.atan2(R[0,1],R[0,2])
    elif isClose(R[2,0],1.0):
        theta = -math.pi/2.0
        psi = math.atan2(-R[0,1],-R[0,2])
    else:
        theta = -math.asin(R[2,0])
        cos_theta = math.cos(theta)
        psi = math.atan2(R[2,1]/cos_theta, R[2,2]/cos_theta)
        phi = math.atan2(R[1,0]/cos_theta, R[0,0]/cos_theta)
    return psi, theta, phi
```
