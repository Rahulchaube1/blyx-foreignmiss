<img src="assets/logo.png" width="112" height="112" alt="ForeignMiss logo">

# ForeignMiss

Count child rows referencing absent numeric parent keys. This Blyx library is part of the databases and migrations collection.

A child reference can look valid while the parent key is duplicated. Check uniqueness and referential integrity before a bulk import. [PostgreSQL, unique and foreign key constraints](https://www.postgresql.org/docs/current/ddl-constraints.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-foreignmiss.git
cd blyx-foreignmiss
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-foreignmiss) · [Package page](https://www.blyx-lang.space/packages/foreignmiss) · [Handbook](https://doc.blyx-lang.space/guide/dunlin)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-foreignmiss.git vendor/foreignmiss
```

```blyx
use vendor::foreignmiss::foreignmiss;

fn main() {
    let parents = [1, 3];
    let children = [1, 2, 2];
    let result = foreignmiss_count(parents, children);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
2
1
```

## API

`foreignmiss_count(parents, children)`

Returns [orphan rows, first orphan row]. Repeated child references are checked independently; represent missing/null separately. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| parents | Vector of values, each a exact signed integer |
| children | Vector of values, each a exact signed integer |

## In use

[Dunlin](https://github.com/Rahulchaube1/blyx-dunlin) uses this module to audit a table export for duplicate parents and orphaned child rows.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-foreignmiss/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
