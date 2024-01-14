# ZkCircuit
ZkCircuit using circom programming language


## Description
This project demonstrates how to create a basic Zkcircuit using gates such as and,or,not gates to derive a sepecific output

## Getting Started
change the inputs a and b accordingly.For deploying in mumbai testnet,add your privatekey through an env file

### Installing
Run npm i to install dependencies

### Executing program

1. Run ``` npx hardhat circom ``` to generate the out directory and the contract file
2. Run ``` npx hardhat run scripts/deploy.ts --network mumbai ``` to deploy the contract to mumbai network and check whether the verifier result is as desired.
```
pragma circom 2.0.0;

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a*b;
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a*b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2*in;
}

template Metacircuit () {  
    signal input a;
    signal input b;

    signal x;
    signal y;

    signal output q;

    component andGate = AND();
    component orGate = OR();
    component notGate = NOT();

    andGate.a <== a;
    andGate.b <== b;
    x <== andGate.out;

    notGate.in <== b;
    y <== notGate.out;

    orGate.a <== x;
    orGate.b <== y;
    q <== orGate.out;
}

component main = Metacircuit();
```

## Authors
Prakash
@Hackprakas

