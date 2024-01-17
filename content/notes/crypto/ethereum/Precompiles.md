---
title: "Precompiles"
---

A precompile in the context of Ethereum is a precompiled "contract" that can be run like a smart contract but outside of the context of the EVM. What this means is that, instead of dealing with EVM opcodes, we can deal directly with Golang-compiled machine code instead, which allows us to perform much more complex computation.

This works by:
- Setting up a list of precompiled "contracts" or functions that is referred to by the ethereum client, eg. geth / go-ethereum or op-geth (Optimism's geth client).
- These precompiled contracts exist at special reserved addresses, for example at `0x01`.
- When a smart contract calls a precompile through, say, `ecrecover`, it is actually calling a wrapper function that either calls `call` or `staticcall` under the hood, towards the corresponding contract address that contains elliptic curve recovery logic, and sending it the corresponding parameters.
- For example, say I would like to add my own precompile to perform `secp256r1` verification at the address `0x10`, this is the function I would need to include in the relevant places for my contracts to be able to call `secp256r1Verify()`. So, the call flow goes as dapp / frontend -> my custom contract -> `secp256r1Verify` method -> ethereum client Golang code.
```go
function secp256r1Verify(
	bytes32 r,
	bytes32 s,
	bytes32 x,
	bytes32 y,
	bytes32 hash
) public view returns (uint8) {
	uint8 output;
	bytes memory args = abi.encodePacked(r, s, x, y, hash);
	assembly {
		if iszero(
			// 0x10 for the precompile address
			// add(args, 32) for ???
			// 0xa0 for the size of the input (160 bytes)
			// output for the output
			// 0x01 for the size of the output flag (1 byte)
			staticcall(not(0), 0x10, add(args, 32), 0xa0, output, 0x01)
		) {
			revert(0, 0)
		}
	}
	
	return output;
}
```

# Resources

- https://stack.optimism.io/docs/build/tutorials/new-precomp/#
- https://docs.moonbeam.network/builders/pallets-precompiles/precompiles/eth-mainnet/#introduction