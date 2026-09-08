# PolyaMath - Vonk Ultra Fuses

A collection of Lua fuses for the Fusion page in DaVinci Resolve, built over the past year to make the animations for the [PolyaMath](https://www.youtube.com/@Polyamathematics) YouTube channel. They extend the [Vonk Ultra](https://kartaverse.github.io/) data node toolset.

---

## About

Vonk Ultra uses Fusion's node-based data pipeline to manipulate numbers, text, arrays, and matrices directly between nodes instead of living inside expressions or scripts. The fuses I've made all add to the vJSON set of nodes and allow you to manipulate JSON strings to hold point and edge data to create graph-based motion graphics.

Currently, this is only a small sample of the nodes I've made; I have a few projects in the works at the moment, but once they're released, I'll add the fuses I used here. I also plan to more clearly organise the fuses moving forward and group together related functionality into single fuses.

**Vonk Ultra is required.** These aren't standalone; without it there's nothing to connect them to.

**Everything here runs in the free version of DaVinci Resolve.** That's the only version I use, so it's the only version anything is tested on. Kartaverse and Vonk Ultra work in free Resolve too.

### Where they've been used

#### [Which Regular Shapes can you draw on any\* Grid?](https://www.youtube.com/watch?v=BJXvaEUZvW0)

A lot of existing nodes for grid generation already worked perfectly for this project. My main additions were automated nodes for generating edge data to control which points get joined together and a project-specific point generation fuse.

**Nodes used:** `vJSONLatticeIntersections`, `vJSONShearX`, `vJSONEdgeShortestDist`, `vJSONEdgeIsolateMerge`, `vJSONEdgeLoop`, `vJSONInterpolate`

<!-- ─────────────────────────────────────────────────────────────────────────────
     TEMPLATE — copy the block below and paste it directly under the "Where
     they've been used" heading to add a newer video at the top of the list.

#### [{{Video Title}}]({{https://www.youtube.com/watch?v=VIDEO_ID}})

{{Two or three sentences on how the nodes were used.}}

**Nodes used:** `{{pmNodeA}}`, `{{pmNodeB}}`

     ───────────────────────────────────────────────────────────────────────────── -->

---

## Nodes

### Original nodes

| Node | Category | Status | Description |
|---|---|---|---|
| `vJSONLatticeIntersections` | Create | Stable | Generates the XYZ coordinates of the points of intersection of a rotated plane with a cubic 3D lattice |
| `vJSONShearX` | Modify | Stable | Shears XYZ points parallel to the x-axis |
| `vJSONEdgeShortestDist` | Edge | Stable | Generates edge data for XYZ points joining them if they are within a threshold |
| `vJSONEdgeIsolateMerge` | Edge | Stable | Generates edge data for merged nodes of XYZ points joining them sequentially if they were from the same node |
| `vJSONEdgeLoop` | Edge | Stable | Generates edge data for XYZ points joining them cyclically |
| `vJSONShapeRenderGPU` | ShapeRender | Experimental | Uses a DCTL kernel for point rendering rather than the CPU-based Fusion API for vector graphic rendering |

### Modified Vonk Ultra nodes

Forks of existing Vonk nodes with changed or added behaviour. These are GPL v3 - see [License](#license).

| Node | Category | Status | Changes |
|---|---|---|---|
| `vJSONInterpolate` | Modify | Stable | Matches array sizes by looping around the shorter array rather than truncating - plan to add nearest neighbour interpolation |
| `vJSONCameraProjection` | Modify | Stable | Fixed points getting reflected after projection - plan to separate transform tools from 3D -> 2D projection |
| `vJSONShapeRender` | ShapeRender | Experimental | Added edge curvature settings and the option to input edge-wise curvature data (requires edge data) |

> **On naming:** modified nodes here use the same name as already existing Vonk Ultra nodes. When installing, if you wish to keep the original Vonk Ultra node, change the `REG_NAME` in the `FuRegisterClass` to something different than the original `FUSE_NAME`

---

## Requirements

- **DaVinci Resolve 19+ (free version)** - developed and tested on Windows using free Resolve only. Should work in Resolve Studio and Fusion Studio, but I can't verify that.
- **[Vonk Ultra](https://kartaverse.github.io/)**, installed via the Reactor package manager.

---

## Installation

Download the latest **[release](https://github.com/NishadDeulkar/PolyaMath-Vonk-Ultra-Fuses/archive/refs/heads/main.zip)** or clone this repo, then copy the `.fuse` files into your Resolve `Fuses` folder:

| OS | Path |
|---|---|
| Windows | `%APPDATA%\Blackmagic Design\DaVinci Resolve\Support\Fusion\Fuses` |
| macOS | `~/Library/Application Support/Blackmagic Design/DaVinci Resolve/Fusion/Fuses` |
| Linux | `~/.local/share/DaVinciResolve/Fusion/Fuses` |

> **If the nodes don't appear,** try the system-wide location instead: `/Library/Application Support/Blackmagic Design/DaVinci Resolve/Fusion/Fuses` on macOS, or `%PROGRAMDATA%\Blackmagic Design\DaVinci Resolve\Fusion\Fuses` on Windows. These paths have shifted between Resolve versions and the official docs haven't always kept up.
> 
>If you have Vonk Ultra installed, then you may prefer to move the `.fuse` files to the same path as these for organisation (won't affect functionality)

---

## Contributing

Bug reports, feature ideas, and pull requests are all welcome, although it may take some time to respond.

Open an issue for anything broken or missing. Including your OS, Resolve version, Vonk Ultra version, and any console output makes it much easier to work out what's going on.
Email polyamathcontact@gmail.com if you'd rather not use GitHub, or if it's about the channel rather than the code.

---

## Credits

- [Vonk Ultra](https://kartaverse.github.io/) and the Kartaverse project by [Andrew Hazelden](https://github.com/AndrewHazelden), with ongoing vMograph development by Dunn Lewis.
- The [We Suck Less](https://www.steakunderwater.com/wesuckless/) community and the Reactor package manager.
