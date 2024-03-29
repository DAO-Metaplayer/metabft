[![codecov](https://codecov.io/gh/DAO-Metaplayer/metabft/branch/main/graph/badge.svg?token=0vLkmaEq3h)](https://codecov.io/gh/DAO-Metaplayer/metabft)
# metabft README

## Overview

`metabft` is a simple, straightforward, METABFT state machine implementation.

It doesn't contain fancy synchronization logic, or any kind of transaction execution layer.
Instead, `metabft` is designed from the ground up to respect and adhere to the `METABFT 2.0` specification document.

Inside this package, you’ll find that it solves the underlying liveness and persistence issues of the original METABFT specification, as well as that it contains a plethora of optimizations that make it faster and more lightweight. For a complete specification overview on the package, you can check out the official documentation.

As mentioned before, `metabft` implements basic METABFT 2.0 state machine logic, meaning it doesn’t have any kind of transaction execution or block building mechanics. That responsibility is left to the `Backend` implementation.

## Installation

To get up and running with the `metabft` package, you can pull it into your project using:

`go get github.com/DAO-Metaplayer/metabft`

Currently, the minimum required go version is `go 1.17`.

## Usage Examples

```go
package main

import "github.com/DAO-Metaplayer/metabft"

// METABFTBackend is the structure that implements all required
// metabft Backend interfaces
type METABFTBackend struct {
	// ...
}

// METABFTLogger is the structure that implements all required
// metabft Logger interface
type METABFTLogger struct {
	// ...
}

// METABFTTransport is the structure that implements all required
// metabft Transport interface
type METABFTTransport struct {
	// ...
}

// ...

func main() {
	backend := NewMETABFTBackned(...)
	logger := NewMETABFTLogger(...)
	transport := NewMETABFTTransport(...)

	metabft := NewMETABFT(logger, backend, transport)

	blockHeight := uint64(1)
	ctx, cancelFn := context.WithCancel(context.Background())

	go func () {
		// Run the consensus sequence for the block height.
		// When the method returns, that means that
		// consensus was reached
		i := RunSequence(ctx, blockHeight)
	}

	// ...

	// Stop the sequence by cancelling the context
	cancelFn()
}
```

## License

Copyright 2022 Metaplayerone Team.
Licensed under the Apache License, Version 2.0 (the “License”); you may not use this file except in compliance with the License. You may obtain a copy of the License at

### http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an “ AS IS” BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
