## My design for an Xor gate using Nand only

![image](https://github.com/marouene-djabbar/HDL-Programming-Language/assets/165311266/cbc5f1e7-07d6-439d-933d-4256685f3773)

## My code

    CHIP XOr {
    IN c, f;
    OUT out;
    PARTS:    
    //XOR == (c Or f) and (NOT(c and f)) == (c Or f) and (c Nand f) == Not[(c Or f) Nand (c Nand f)]

    // First stage: (c Or f)
    // c Or F == Not((not c) And (not f)) == Not [ Not((not c) Nand (not f))] == (not c) Nand (not f)
    // Inverting c and f to prepare for the OR operation
    Nand(a=c, b=c, out=notc); // not c
    Nand(a=f, b=f, out=notf); // Not f
    Nand(a=notc, b=notf, out=cOrf) // (not c) Nand (not f) == c Or F
    
    // Second stage: (c Nand f)
    Nand(a=c, b=f, out=cNandf); // c Nand f
    
    // Third stage: (c Or f) Nand (c Nand f)
    Nand(a=cOrf, b=cNandf, out=cOrfNandNandf);
    
    // Forth stage: Not[(c Or f) Nand (c Nand f)]
    Nand(a=cOrfNandNandf, b=cOrfNandNandf, out=out);
    }


## Math behind the Xor gate design

1. c XOR f == (c Or f) and (Not (c and f)) == (c Or f) and (c Nand f) == Not ((c Or f) and (c Nand f)).
2. c Or f == Not ( (Not c) And (Not f)) == Not ( Not((Not c) Nand (Not f))) == (Not c) Nand (Not f).
