### Really Simple Algorithm

We found a strange service running over TCP (my my, there do seem to be a lot of those as of late!). Connect to the service and see if you can't exploit it somehow.

Author: Bottersnike

---

On connecting, we were presented with with a bunch of numbers (or variables, perhaps).  
p, q, e, ct.

It was obvious that it was an RSA based challenge. Note, the title itself can be shortened to RSA. This was the easiest of the 4 linked RSA based challenges.
We've provided a sample input (since the message/plaintext was the same, but you'd have different p, q, e, and ct (ciphertext) each time you'd connect).

Essentialy, it's decrypting RSA when all information is given.

```python
from socket import socket
import math

host = <host>
port = <port>


def getModInverse(a, m):
    if math.gcd(a, m) != 1:
        return None
    u1, u2, u3 = 1, 0, a
    v1, v2, v3 = 0, 1, m

    while v3 != 0:
        q = u3 // v3
        v1, v2, v3, u1, u2, u3 = (
            u1 - q * v1), (u2 - q * v2), (u3 - q * v3), v1, v2, v3
    return u1 % m


def solversa(p, q, e, ct):
    n = p * q
    d = getModInverse(e, (p - 1) * (q - 1))
    pt = pow(ct, d, n)
    print("pt: " + str(pt))
    return str(pt)


def main():
    # sock = socket()
    # sock.connect((host, port))
    # text = sock.recv(2048)
    # sock.close()
    text = """
    p: 10683073138988793841949022563881321947262549152628491523512835408728360585373972388855575177278916794195623064389028727303690432129451612061311381272091801
    q: 13327288536213421153506444018238059880708942714494343534745962482893352745440070645490695469126971983698353651711694276813959973549546395575273272509230031
    e: 65537
    ct: 55688704982012410273973841630902893183494310777536917448544284534489906064245438856093341065122659044623503762971994416786108918096619340013192080110031626460485555758150570512989202108903762970210074758240790271067917228549782099357274207235898614261185490682552916455757800284346445266589353469364744921339
    """
    text = text.split()
    p = int(text[1])
    q = int(text[3])
    e = int(text[5])
    ct = int(text[7])

    ret = solversa(p, q, e, ct)
    print(bytes.fromhex(hex(int(ret))[2:]).decode("utf-8"))
```
    
#### Flag
`ractf{JustLikeInTheSimulations}`
