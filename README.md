# automemlimit

[![Go Reference](https://pkg.go.dev/badge/github.com/KimMachineGun/automemlimit.svg)](https://pkg.go.dev/github.com/KimMachineGun/automemlimit)

Automatically set `GOMEMLIMIT` to match Linux container memory quota.

See more details about `GOMEMLIMIT` [here](https://tip.golang.org/doc/gc-guide#Memory_limit).

## Installation

```shell
go get -u github.com/KimMachineGun/automemlimit
```

## Usage

```go
package main

// It sets `GOMEMLIMIT` to 90% of memory quota for 
// You can configure it with `AUTOMEMLIMIT=(0,1]` environment variable.
import _ "github.com/KimMachineGun/automemlimit"
```

or

```go
package main

import "github.com/KimMachineGun/automemlimit/memlimit"

func init() {
	memlimit.SetGoMemLimit(0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.Limit(1024*1024), 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroup, 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroupV1, 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroupV2, 0.9)
}
```
