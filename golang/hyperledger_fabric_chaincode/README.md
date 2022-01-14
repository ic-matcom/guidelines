## Specifications for the implementation of smart contract
Multiple smart contracts should only be deployed in traceability chaincode because are very closely related and share the same world state.

## Coding Spec
use package names in singular (do not use plural)

use UpperCamelCase in:
* functions name
* contracts name
* structs field

ex:
```golang
    // Request
    type Request struct {
        Amount     float32
        IssuerID   string
        FuelTankID string
    }
```

use lowerCamelCase in:
* json field in structs

ex:
```golang
    // Request
    type Request struct {
        Amount     float32 'json:"amount"'
        IssuerID   string  'json:"issuerID"'
        FuelTankID string  'json:"fuelTankID"'
    }
```
### Comments

Comments serve as program documentation. There are two forms:

1. Line comments start with the character sequence // and stop at the end of the line.
2. ~~General comments start with the character sequence /* and stop with the first subsequent character sequence */.~~
---
**NOTE:**
By agreement we will use only the 1st form
---

e.g:
``` golang
// GetAsset returns bla bla bla.
//
// Arguments:
//		0: objectType - brief comment
//		1: assetID - brief comment
// Returns:
//		0: string
//		1: error
func GetAsset(ctx contractapi.TransactionContextInterface, objectType string, assetID string) (string, error) {
    ...
}
```

``` golang
// Record returns bla bla bla.
//
// Arguments:
//		0: none
// Returns:
//		0: error
func Record(ctx contractapi.TransactionContextInterface) error {
    ...
}
```


### Chaincode namespace
Contracts namespaces:
* org.uh.user
* org.uh.role

A **contract namespace** allows it to keep its world state separate from other chaincodes.
Specifically, smart contracts in the same chaincode share direct access to the same world state,
whereas smart contracts **in different chaincodes cannot directly access each other’s world state**.

If a smart contract needs to access another chaincode world state, it can do this by performing a
chaincode-to-chaincode invocation. [more](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/chaincodenamespace.html)

## Chaincode Developer Terminology
### Smart contracts and Chaincode
A smart contract is defined within a chaincode. Multiple smart contracts can be defined within the same chaincode.
When a chaincode is deployed, all smart contracts within it are made available to applications.

### Contract Name
Each smart contract within a **cc-traceability** chaincode is uniquely identified by its contract name.
Specifically, uses an explicit DNS-style naming convention to help organize clear and meaningful names;
**org.tecnomatica.fuelbatch** conveys that the **channeljet**  network has defined a standard **fuelbatch** smart contract.

### Considerations
- Multiple smart contracts should only be deployed in the same chaincode if they are very closely related. Usually, this is only necessary if they share the same world state.
- Chaincode namespaces provide isolation between different world states. In general it makes sense to isolate unrelated data from each other. Note that you cannot choose the chaincode namespace; it is assigned by Hyperledger Fabric, and maps directly to the name of the chaincode.
- For chaincode to chaincode interactions using the invokeChaincode() API, both chaincodes must be installed on the same peer.
  - For interactions that only require the called chaincode’s world state to be queried, the invocation can be in a different channel to the caller’s chaincode.
  - For interactions that require the called chaincode’s world state to be updated, the invocation must be in the same channel as the caller’s chaincode.
  
[know more](https://hyperledger-fabric.readthedocs.io/en/release-2.2/smartcontract/smartcontract.html)

## Best Practices

[know more](https://blog.learngoprogramming.com/golang-const-type-enums-iota-bc4befd096d3)

## Spec
[know more](https://golang.org/ref/spec)

## Unit Test and BDD
[go to](./testing/README.md)
