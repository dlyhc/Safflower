# Safflower Flower-Head Time-Series Phenotyping Dataset

**Time-series flower-head images, chromatic/phenotypic features and synchronised field environmental records for continuous, non-destructive quality phenotyping of safflower (*Carthamus tinctorius* L.)**

This repository releases the data underlying the manuscript:

> **Continuous Quality Phenotyping of Safflower (*Carthamus tinctorius* L.) Flower Heads: Phenology-Prior-Guided Prediction and Environmental Response Analysis**
> Zhengyang Zhang, Jiyang Zhang, Tianyu Liu, Lingya Pu, Jie Ma, Runbiao Yang, Haichao Yang\*, Yongcheng Yang\*
> *Plant Phenomics* (2026). DOI: `to be added upon publication`

---

## 1. Overview

| Item | Value |
|---|---|
| Crop / cultivar | Safflower (*Carthamus tinctorius* L.), cv. **Yunhong No. 7** |
| Site | Safflower cultivation base, Weishan County, Yunnan, China (~100.2484° E, 25.0735° N, ~1,715 m a.s.l.) |
| Period | **2026-03-28 → 2026-05-13** (images) · **2026-03-01 → 2026-05-12** (environment) |
| Flower heads tracked | **212** IDs (`F0001`–`F0212`); **211** have usable images (`F0181` yielded none) |
| Released images | **1,853** JPEG flower-head crops, 320 × 320 px |
| Observations per head | 3 – 21 (mean 8.78) |
| Acquisition schedule | 3 × daily, nominally 08:00 / 12:00 / 16:00 local time |
| Environmental records | **872** rows × 19 columns, **2-hourly** (73 days × 12 slots/day) |
| Modalities | RGB imagery · CIELAB chromaticity · GLCM texture · morphology · meteorology · soil |

**Files**

```
data/global_env_timeline.csv    872 rows x 19 cols   2-hourly meteorology + soil
data/phenotype_features.csv     1853 rows x 14 cols  per-image chromatic / texture / morphology
safflower_flower_crops.zip      1853 JPEG, 320x320   73.4 MB -> attach to a Release or use Git LFS
```

The dataset supports three linked tasks, in the order used by the manuscript:

1. **Chromatic prediction** — predict a flower head's CIELAB `a*`, `b*` and hue angle `h` at the next observation time from its previous six observations (model: **PhenoDeltaNet**).
2. **Quality measurement** — convert chromaticity into a 0–100 **Comprehensive Chromatic Quality Index (CCQI)** calibrated against HPLC-determined HSYA and kaempferol contents.
3. **Environmental response analysis** — relate short-interval CCQI change (`ΔQ`) to meteorological and soil drivers (GAMM + feature-group permutation).

---

## 2. Known limitations

Read these before drawing conclusions from the data:

1. **Single site, single season, single cultivar.** Cross-year, cross-region and cross-cultivar generalisation is untested.
2. **No absolute colour calibration.** No colour checker was used, so chromaticity is subject to illumination-driven drift. The manuscript quantifies this with an image-based illuminance probe (a fixed support pole in the lower frame): transfer slopes β = 0.0041, 0.0063, 0.0047° per 10⁴ lx for `a*`, `b*`, `h`, giving an upper bound on the imaging artefact contribution to ΔQ. Do not compare absolute chromaticity across widely differing illumination conditions without accounting for this.
3. **Unequal observation intervals.** Daytime gaps are ~4 h; overnight gaps are ~16 h. Always stratify by prediction horizon.
4. **Noisy / unused channels.** `air_pressure` contains outliers (max 179.2 against a normal ~82 kPa); `co2`, `wind_direction` and the soil N/P/K/EC channels are either unstable in scaling or near-constant within the plot. Only air temperature, relative humidity, illuminance, rainfall, soil temperature and soil moisture entered the response analysis.
5. **Small HPLC reference set (30 pooled samples).** The CCQI–constituent association is an exploratory rank-level proxy, not a calibrated regression for absolute content. The 30 HSYA / kaempferol determinations are reported in Table S1 of the Supplementary Material.
6. **2-hourly, not hourly, environmental resolution** in the released file, with real gaps: 108 / 872 rows lack the meteorological block and 63 / 872 lack the soil block (device outages, not imputed).

---

## 3. Citation

If you use this dataset, please cite the manuscript:

```bibtex
@article{Zhang2026Safflower,
  title   = {Continuous Quality Phenotyping of Safflower ({Carthamus tinctorius} L.) Flower Heads: Phenology-Prior-Guided Prediction and Environmental Response Analysis},
  author  = {Zhang, Zhengyang and Zhang, Jiyang and Liu, Tianyu and Pu, Lingya and Ma, Jie and Yang, Runbiao and Yang, Haichao and Yang, Yongcheng},
  journal = {Plant Phenomics},
  year    = {2026},
  doi     = {to be added upon publication}
}
```

And this data release:

```bibtex
@dataset{Zhang2026SafflowerData,
  title     = {Safflower Flower-Head Time-Series Phenotyping Dataset},
  author    = {Zhang, Zhengyang and Zhang, Jiyang and Liu, Tianyu and Pu, Lingya and Ma, Jie and Yang, Runbiao and Yang, Haichao and Yang, Yongcheng},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/<org>/safflower-quality-phenotyping}
}
```

---

## 4. License and contact

- **Data** (`data/*.csv`, `safflower_flower_crops.zip`): [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — free to use with attribution.
- **Code**: MIT (see `LICENSE`).

Corresponding authors:
- Haichao Yang — `dlyhc@163.com`

Affiliations: College of Mathematics and Computer Science, Dali University · College of Pharmacy and Chemistry, Dali University 
