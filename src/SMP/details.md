# Technical Details

- Private key is a randomly generated, 256 bit number
    - private key = \\(k\\)
- multiply (dot) this private key by the Generator point, \\(G\\), (is the same every time) using elliptic curve multiplication (we can choose G)
    - \\(G\\) is of the form \\((x, y)\\)
    - Elliptic curve multiplication is just Elliptic curve addition up to \\(k\\)
    - \\(K = k \cdot G = G + G+ G ...\\) (up to k times)
    - This gives you a new (very large) point
    - Say you want to add two points to get a new point. Addition on an elliptic curve is done by doing.
    
    \\[
    P_1 + P_2 = \dot{P_3}
    \\]
    
    \\[
    P_3 = \text{reflection of }\dot{P_3} \text{ in } x \text{ axis } \implies P_3(x, y) = \dot{P_3}{{(x,-y)}}
    \\]
    
    - this can be done using a `secp256k1` library
    - `secp256k1` produces the equation:
    
    \\[
    y^2 \mod p= (x^3 +7) \mod p
    \\]
    
    where \\(p = 2^{256} - 2^{32} - 2^9 - 2^8- 2^7- 2^6 - 2^4 -1\\)
    
- \\(K=\\) concatenation of the 32 byte x-coordinate and the 32 byte y-coordinate from the elliptic curve multiplication
- Then use `Keccak-256` on \\(K=\\) to get a useable public ID