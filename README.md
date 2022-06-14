# go-keyring
Implement go utilities compatible with Substrate sr25519 keys.

## usage
```
package main

import (
	"fmt"
	"log"

	keyring "github.com/CESSProject/go-keyring"
)

func main() {
	// generate keyring from 12 word mnemonic
	secretURI := "head achieve piano online exhaust bulk trust vote inflict room keen maximum"
	kr, _ := keyring.FromURI(secretURI, keyring.NetSubstrate{})

	// output public SS58 formatted address
	ss58, _ := kr.SS58Address()
	log.Printf("SS58 Address: %s", ss58)

	// sign message
	msg := []byte("setec astronomy")
	sig, _ := kr.Sign(kr.SigningContext(msg))

	// create new keyring from SS58 public address to verify message signature
	verkr, _ := keyring.FromURI(ss58, keyring.NetSubstrate{})

	fmt.Println(verkr.Verify(verkr.SigningContext(msg), sig))
}
```
