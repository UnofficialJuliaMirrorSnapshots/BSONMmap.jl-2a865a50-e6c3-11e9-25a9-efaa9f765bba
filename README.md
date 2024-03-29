# Add mmap support to to BSON.jl

## Installation

```julia
using Pkg
pkg"add BSONMmap"
```

## Usage

```julia
using BSON, BSONMmap
dict = Dict("a" => ones(Float32, 10), Dict("b" => zeros(10)))
BSON.bson("test.bson", dict)
```

You can load it back using `bsload`

```julia
bsload("test.bson", mmaparrays = true) == dict
```

Or just use `BSON`s native `load`

```julia
withenv("BSON_MMAP" => true) do
    BSON.load("test.bson")
end
```
