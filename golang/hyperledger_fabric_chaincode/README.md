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
* org.tecnomatica.participant
* org.tecnomatica.fuelbatch
* org.tecnomatica.document
* org.tecnomatica.infraestructure

A **contract namespace** allows it to keep its world state separate from other chaincodes.
Specifically, smart contracts in the same chaincode share direct access to the same world state,
whereas smart contracts **in different chaincodes cannot directly access each other’s world state**.

If a smart contract needs to access another chaincode world state, it can do this by performing a
chaincode-to-chaincode invocation. [more](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/chaincodenamespace.html)

## Chaincode Developer Terminology
### Smart contracts and Chaincode