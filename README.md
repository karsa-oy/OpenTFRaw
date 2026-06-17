# OpenTFRaw

> **Karsa fork.** This is a fork of [OpenTFRaw](https://github.com/Sigilweaver/OpenTFRaw)
> by Nathan Riley, published to PyPI as **`mascope-opentfraw`** (still imported as
> `opentfraw`). It adds Python accessors for profile spectra, per-peak FT labels,
> and the per-scan trailer, plus Exploris scan-event decoding — each also opened
> upstream as a pull request (see [`NOTICE`](NOTICE)). It exists to make these
> available ahead of an upstream release and will be retired once they land
> upstream. Apache-2.0, same as upstream.

[![CI](https://github.com/Sigilweaver/OpenTFRaw/actions/workflows/ci.yml/badge.svg)](https://github.com/Sigilweaver/OpenTFRaw/actions/workflows/ci.yml)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20470601.svg)](https://doi.org/10.5281/zenodo.20470601)
[![crates.io](https://img.shields.io/crates/v/opentfraw.svg)](https://crates.io/crates/opentfraw)
[![PyPI](https://img.shields.io/pypi/v/opentfraw.svg)](https://pypi.org/project/opentfraw/)
[![docs.rs](https://img.shields.io/docsrs/opentfraw)](https://docs.rs/opentfraw)
[![License: Apache-2.0](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](LICENSE)
[![Rust MSRV](https://img.shields.io/badge/rust-1.85%2B-orange.svg)](https://www.rust-lang.org)

> Part of the [OpenProteo](https://sigilweaver.app/openproteo/docs/)
> stack for proteomics raw-file access. Sibling readers:
> [OpenWRaw](https://github.com/Sigilweaver/OpenWRaw) (Waters),
> [OpenTimsTDF](https://github.com/Sigilweaver/OpenTimsTDF) (Bruker).

Rust and Python reader for Thermo Fisher `.raw` mass spectrometry files,
covering format versions 8 through 66 (LCQ Classic through Orbitrap
Astral and modern TSQ).

Documentation: [sigilweaver.app/opentfraw/docs](https://sigilweaver.app/opentfraw/docs)

## Install

Rust:

```sh
cargo add opentfraw
```

Python:

```sh
pip install opentfraw
```

## Quickstart

Rust:

```rust
use opentfraw::RawFileReader;

let raw = RawFileReader::open_path("sample.raw")?;
let mut file = std::fs::File::open("sample.raw")?;
for scan_num in 1..=raw.num_scans {
    let peaks = raw.read_scan_peaks(&mut file, scan_num)?;
    println!("scan {scan_num}: {} peaks", peaks.mz.len());
}
```

Python:

```python
import opentfraw

raw = opentfraw.RawFile("run.raw")
mz, intensity = raw.peaks(3)
print(raw.scan(3)["filter_string"])
raw.to_mzml("run.mzML")
```

See the [docs site](https://sigilweaver.app/opentfraw/docs) for the full
guide, format specification, and API reference.

## License

Apache-2.0. See [LICENSE](LICENSE).

The format specification was developed by binary analysis of public
mass-spectrometry datasets (PRIDE accessions). See
[CORPUS.md](CORPUS.md) and [ATTRIBUTION.md](ATTRIBUTION.md).
