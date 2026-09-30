# deckstation-cores

Cores de **libretro para aarch64** que **ninguna fuente publica ya compilados**, compilados por el
proyecto para **DeckStation** (Pocknix / AYN Odin 3).

## Qué hay (release `cores-2026-09`)

| Core | Sistema | Origen | Cómo se compiló |
|---|---|---|---|
| `azahar_libretro.so` | Nintendo 3DS | `azahar-emu/azahar` tag `2126.1.2` | CMake + Ninja + clang, `-DENABLE_LIBRETRO=ON -DENABLE_SSE42=OFF -DENABLE_LTO=OFF` (receta de Batocera). ~35 min en un Odin 3 (8 núcleos). |
| `bsnes_hd_beta_libretro.so` | SNES (HD) | `DerKoun/bsnes-hd` commit `fc26b25e` | `make -C bsnes -f GNUmakefile target=libretro platform=linux local=false` (~5 min). |

Se incluyen los `.info` correspondientes.

## Cómo lo usa DeckStation

`scripts/deckstation-cores-fetch.sh` (en DeckStation) los descarga a la carpeta portable de
RetroArch al instalar DeckStation:

    https://github.com/arcadematicas/deckstation-cores/releases/download/cores-2026-09/<nombre>_libretro.so

El resto de cores (~255) se bajan del set de ArkOS (`christianhaitian/retroarch-cores`, commit
pineado) y del buildbot oficial de libretro.

## Por qué existe

- `azahar_libretro.so` no lo publica ni el buildbot de libretro ni el set de ArkOS, y **no se puede
  compilar en un build con qemu**: gcc peta con un ICE (*Segmentation fault in cc1plus*).
- `bsnes_hd_beta_libretro.so` tampoco está publicado suelto (Batocera lo compila, pero no lo
  distribuye aparte).

## Notas

- Los binarios son de **aarch64** (ARM64) y se han probado en un AYN Odin 3 con Pocknix: ambos
  cargan en RetroArch y sus comandos aparecen en ES-DE.
- Licencias: Azahar GPL-2.0-or-later; bsnes-hd GPL-3.0-only. Se distribuyen respetando sus licencias
  y la atribución de autoría.
