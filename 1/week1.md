# Week 1: Boolean Functions and Gate Logic

In programming, we don't worry about the "how" (implementation); we only worry about the "what" (abstraction). So we build one stage, and then we move on to building another stage on top of it. In order to do that, we can forget how the first stage was implemented and worry only about its interface.

## Boolean Logic

* x AND y : returns 1 only if BOTH values are 1
* x OR y : returns 1 if ANY one of the values is 1
* NOT(x) : this unary operation returns the opposite of the input value

Every Boolean function can be represented by a *canonical representation,* an expression containing the above three operations. In fact, we can forgo OR because:

* (x OR y) = NOT(NOT(x) AND NOT(y))

Therefore, there is one operation that by itself can represent any Boolean function - the NAND operation! Essentially, NOT(x AND y).

* NOT(x) = (x NAND x)
* (x AND y) = NOT(x NAND y)

## Logic Gates

An elementary logic gate is the building block of a simple chip designed to deliver a specific logical functionality. 

A gate interface is the gate abstraction. It tells the user what the gate is supposed to do. The gate implementation shows how it does what it should do. 

## Hardware Description Language (HDL)

HDL describes logic gate diagrams. It is a functional/declarative language — we use it for nothing more than a static description of the gate diagram. The order of HDL statements is insignificant, but in order to use a chip part you must know its interface.

```
/* Xor gate: out = (a And Not (b)) Or (Not(a) And b) */

CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Not (in=a, out=nota);
    Not (in=b, out=notb);
    And (a=a, b=notb, out=aAndNotb);
    And (a=nota, b=b, out=notaAndb);
    Or (a=aAndNotb, b=notaAndb, out=out);
}
```