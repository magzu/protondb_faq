## Språk
-  [Engelsk](#table-of-content)
-  [Tysk](README_DE.md) (Oversatt av [CrackedCrafterz](https://github.com/CrackedCrafterz))
-  [Spanish](README_ESP.md) (Oversatt av [Willdrick](https://github.com/Willdrick))
-  French (Ser fremdeles etter noen som kan oversette.)
-  Italian (Snart)

## Innholdsfortegnelse
  - [Hvorfor krasjer spillet mitt, er treg eller har grafikk problemer?](#why-do-my-games-crash-on-start-run-very-slow-or-have-rendering-issues)
  - [Spillet mitt crasher etter en stund men fungerer fint uten esync](#my-game-crashes-after-a-while-but-works-fine-without-esync)
  - [Spillet viser ingen tekst](#the-game-doesnt-show-any-text)
  - [Noen spill som Witcher 3 mangler fiender eller tekstur](#some-games-like-witcher-3-have-missing-texturesenemies)
  - [Noen reporter sier de fikk spillet til å kjøre, ved å installere ekstra programvare. Hvordan?](#some-reports-say-they-made-the-game-running-by-installing-some-software-how-do-i-do-that)
  - [Hvordan kjører jeg Windows spill jeg ikke eier på Steam?](#how-do-i-run-windows-games-i-dont-own-on-steam)
  - [Spill lagret på min Windows partisjon (NTFS) vill ikke starte](#games-stored-on-my-windows-partition-ntfs-wont-start)
## Hvorfor krasjer spillet mitt, er treg eller har grafikk problemer?

#### Sørg for at maskinen er oppdatert og at du har installert siste grafikk kort driver.

#### Sjekk ut denne nettsiden for spillet ditt [WineHQ](https://appdb.winehq.org), Så kan du finne metoder for å få spillet til å kjøre. Hvis det står på WineHQ at spillet kjører fint i Wine, så kan det hende det er proton eller treddeparts DRM som "Denuvo" som foresaker at spillet ikke kjører.

#### Sørg for at du bruker steam sitt bibliotek (Steam Runtime):

- Arch: Bruk Steam (Runtime)

- Solus: Her må du skru av Solus sin egene "[linux-steam-integration-tool](https://raw.githubusercontent.com/solus-project/linux-steam-integration/master/.github/LSI_Settings.png)"

Merk:

- Dette er Stabile drivere, Hvis du vil kjøre nyere drivere som Beta eller Utvikler drivere. Så må du gjøre det på egenhånd.

- LLVM 7 eller nyere er påkrevd for å løse mange grafikk problemer. Hvis din distro fortsatt bruker LLVM 6, som Solus for eksempel så må du si ifra til Distro eierene at de må oppdatere.



##
### Installasjon av Grafikk driver
#### AMD

Arch/Manjaro/Antergos:
```
sudo pacman -S vulkan-radeon lib32-vulkan-radeon lib32-mesa lib32-vulkan-icd-loader vulkan-tools
```

Ubuntu 18.04:
```
sudo add-apt-repository ppa:paulo-miguel-dias/pkppa
sudo apt update
sudo apt install mesa-vulkan-drivers mesa-vulkan-drivers:i386
```
Ubuntu 18.10

```
sudo apt install mesa-utils
sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
```
##
#### Nvidia

Arch/Manjaro/Antergos:
```
sudo pacman -S lib32-nvidia-utils lib32-opencl lib32-nvidia nvidia nvidia-utils
```

Ubuntu 18.10:
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-396
```

Ubuntu 18.04:
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-driver-396
```
##
#### Intel

Arch/Manjaro/Antergos:
```
sudo pacman -S lib32-vulkan-intel vulkan-intel lib32-mesa lib32-vulkan-icd-loader vulkan-tools
```

Ubuntu 18.10:
```
sudo apt install mesa-utils
sudo apt install libvulkan1 mesa-vulkan-drivers vulkan-utils
```

Ubuntu 18.04:
```
sudo add-apt-repository ppa:paulo-miguel-dias/pkppa
sudo apt update
sudo apt install mesa-vulkan-drivers mesa-vulkan-drivers:i386
```
##
For å se om Vulkan fungerer, kjør følgende kommando: `vulkaninfo`

Her er et [Example](https://raw.githubusercontent.com/NoXPhasma/protondb_faq/master/VulkaninfoExample.png) På hvordan det skal se ut.

Hvis du får: "Cannot create Vulkan instance." Prøv å restart din PC. Hvis du fremdeles får feilmeldingen og du er sikker på at alle pakker er installert. Spør etter hjelp på Discord: [Discord](https://discord.gg/uuwK9EV) 

## Spillet mitt crasher etter en stund men fungerer fint uten esync

Fleste esync problemer er relatert til en begrensning av hvor mange filer som kan være åpene. Før du rapporterer problemer med esync sørg for at kommando 'ulimit -Hn' viser mer enn 4096. Hvis den ikke gjør dette så må du følge instruksene her: these instructions](https://github.com/zfigura/wine/blob/esync/README.esync) for å skru opp fil begrensningene.

## Spillet viser ingen tekst

Noen spill er avhengig av at Windows fonter er installert. Etter Proton versjon [3.16-4](https://github.com/ValveSoftware/Proton/wiki/Changelog#316-4) er dette installert automatisk. Hvis du bruker Proton 3.7, prøv å bytt til versjon 3.16-4 eller høyere å se om dette løser problemet.

For å bytte Proton versjon, Gå til Steam instillinger. Der vil du ha et valg som heter Steam Play gå til denne. Huk av på valget "Bruk dette verktøyet i stedet for spillspesifikke valg fra Steam". Velg så Proton versjon fra menyen under, Sørg for å velge versjon 3.16-4 eller høyere.

## Some games like Witcher 3 have missing textures/enemies

This is fixed since DXVK Version [0.90](https://github.com/doitsujin/dxvk/releases/tag/v0.90) and Vulkan 1.1.88. Unfortunately at time of this writing, you need beta drivers for Nvidia (396.54.09) and AMD users need at least Mesa version 18.3.

## Some reports say they made the game running by installing some software, how do I do that?

There are two ways to install additional software into the games prefix:

#### Use of Winetricks
Make sure you have winetricks installed on your system. This package should be in your distributions repository.

Open a Terminal and use
```
WINEPREFIX=(Steam-folder)/steamapps/compatdata/(GAME-ID)/pfx/ winetricks
```
(GAME-ID) must be replaced with the game id for example 4000 for Garry´s Mod, you can use [SteamDB](https://steamdb.info) to find out what id your game have.

(Steam-folder) must be replaced with your .steam folder loaction.

Here is an example

```
WINEPREFIX=/home/alexander/.steam/steam/steamapps/compatdata/4000/pfx/ winetricks
```
##
#### Use of Tools

The two most popular currently are [Protontricks](https://github.com/Sirmentio/protontricks) and [ProtonFixes](https://github.com/simons-public/protonfixes).

Please read the instructions about those tools on their respective sites.

## How do I run Windows games I don't own on Steam?

To run games which are not on Steam, you can use [Lutris](https://lutris.net/) to run them with Wine. Lutris is a game manager which offers support for a lot of different compatibility layers/emulators, including Wine/Proton.

## Games stored on my Windows partition (NTFS) won't start

By default Linux mounts NFTS partitions only writable by Root. [WIP]
