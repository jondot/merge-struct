Merge Struct
============

[<img alt="github" src="https://img.shields.io/badge/github-jondot/merge--struct-8dagcb?style=for-the-badge&labelColor=555555&logo=github" height="20">](https://github.com/jondot/merge-struct)
[<img alt="crates.io" src="https://img.shields.io/crates/v/merge-struct.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/merge-struct)
[<img alt="docs.rs" src="https://img.shields.io/badge/docs.rs-merge-struct-66c2a5?style=for-the-badge&labelColor=555555&logo=docs.rs" height="20">](https://docs.rs/merge-struct)
[<img alt="build status" src="https://img.shields.io/github/workflow/status/jondot/merge-struct/Build/master?style=for-the-badge" height="20">](https://github.com/jondot/merge-struct/actions?query=branch%3Amaster)

This is a Rust library deep merges two serializable structs.

## Dependency

```toml
[dependencies]
merge-struct = "0.1.0"
```

For most recent version see [crates.io](https://crates.io/crates/merge-struct)


## Usage

```rust
use std::collections::BTreeMap;
use serde_json;
use serde::{Deserialize, Serialize};
use merge_struct::merge;

let left: Data = serde_json::from_str(
    r###"
{
    "is_root": false,
    "entries": {
        "/var/log/f2": {
            "name":"f2",
            "size": 5
        }
    },
    "folders": [
        {
            "name": "/var/log",
            "num_files": 20
        }
    ]
}
"###,
)
.unwrap();

let right: Data = serde_json::from_str(
    r###"
{
    "folders":[],
    "entries": {
        "/var/log/f1": {
            "name":"f1",
            "size": 12
        }
    }
}
"###,
).unwrap();

let res = merge(&left, &right);
```


# Copyright

Copyright (c) 2022 [@jondot](http://twitter.com/jondot). See [LICENSE](LICENSE.txt) for further details.
