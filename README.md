# Unreal Engine Standards (Style-Guide, Personalized)

*A mostly reasonable approach to coding and management standards in Unreal Engine 5.*

*Originally created by [Allar](https://github.com/Allar), and can be viewed here: [ue5-style-guide](https://github.com/Allar/ue5-style-guide).*

*Edited by me to fit my needs and standards and serve as a coding standard reference during personal development using Unreal Engine 5.*

## Linking To This Document

Every section of this style guide is numbered for both easy reference and easy linking.

You can link to any section directly by simply append a hash tag and the section number to the end of https://github.com/AntonVasserman/ue5-standards.

For example, if you want to send someone to the first principle of this style guide you would append `#0.1`, resulting in https://github.com/AntonVasserman/ue5-standards#0.1.

## Table of contents
- [Important Terminology](#important-terminology)
  - [Levels/Maps](#terms-level-map)
  - [Identifiers](#terms-identifiers)
  - [Cases](#terms-cases)
  - [Variables / Properties](#terms-var-prop)
    - [Property](#terms-property)
    - [Variable](#terms-variable)
- [0. Principles](#0)
  - [0.1 All structure, assets, and code in any Unreal Engine 5 project should look like a single person created it, no matter how many people contributed](#0.1)
  - [0.2 Friends do not let friends have bad style](#0.2)
  - [0.3 A team without a style guide is no team of mine](#0.3)
- [1. Globally Enforced Opinions](#1)
  - [1.1 Forbidden Characters](#1.1)
    - [1.1.1 Identifiers](#identifiers)
- [2. Asset Naming Conventions](#anc)
  - [2.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`](#base-asset-name)
    - [2.1 Examples](#2.1-examples)
  - [2.2 Asset Name Modifiers](#asset-name-modifiers)
    - [2.2.1 Animations](#anc-animations)
    - [2.2.2 Artificial Intelligence](#anc-ai)
    - [2.2.3 Blueprints](#anc-bp)
    - [2.2.4 Effects](#anc-effects)
    - [2.2.5 Inputs](#anc-inputs)
    - [2.2.6 Materials](#anc-materials)
    - [2.2.7 Paper 2D](#anc-paper2d)
    - [2.2.8 Paper ZD](#anc-paperzd)
    - [2.2.9 Physics](#anc-physics)
    - [2.2.10 Sounds](#anc-sounds)
    - [2.2.11 Textures](#anc-textures)
      - [2.2.11.1 Texture Packing](#anc-textures-packing)
    - [2.2.12 User Interface](#anc-ui)
    - [2.2.13 Miscellaneous](#anc-misc)
- [3. Content Directory Structure](#structure)
  - [3e1 Example Project Content Structure](#3e1)
  - [3.1 Folder Names](#structure-folder-names)
    - [3.1.1 Always Use PascalCase](#3.1.1)
    - [3.1.2 Never Use Spaces](#3.1.2)
    - [3.1.3 Never Use Unicode Characters And Other Symbols](#3.1.3)
  - [3.2 Use A Top Level Folder For Project Specific Assets](#structure-top-level)
    - [3.2.1 No Global Assets](#3.2.1)
    - [3.2.2 Reduce Migration Conflicts](#3.2.2)
      - [3.2.2e1 Master Material Example](#3.2.2e1)
    - [3.2.3 Samples, Templates, and Marketplace Content Are Risk-Free](#3.2.3)
    - [3.2.4 DLC, Sub-Projects, and Patches Are Easily Maintained](#3.2.4)
  - [3.3 Use Developers Folder For Local Testing](#structure-developers)
  - [3.4 All Map<sup>*</sup> Files Belong In A Folder Called Maps](#structure-maps)
  - [3.5 Use A `Core` Folder For Critical Blueprints And Other Assets](#structure-core)
  - [3.6 Do Not Create Folders Called `Assets` or `AssetTypes`](#structure-assettypes)
    - [3.6.1 Creating a folder named `Assets` is redundant](#3.6.1)
    - [3.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant](#3.6.2)
  - [3.7 Very Large Asset Sets Get Their Own Folder Layout](#structure-large-sets)
  - [3.8 `MaterialLibrary`](#structure-material-library)
  - [3.9 No Empty Folders](#structure-no-empty-folders)
- [4. C++](#cpp)
  - [4.1 Compiling](#cpp-compiling)
  - [4.2 Variables](#cpp-vars)
    - [4.2.1 Naming](#cpp-vars-naming)
      - [4.2.1.1 Nouns](#cpp-vars-naming-nouns)
      - [4.2.1.2 PascalCase](#cpp-vars-naming-case)
      - [4.2.1.3 Boolean Names](#cpp-vars-bool-names)
        - [4.2.1.3.1 Boolean `b` Prefix](#4.2.1.3.1)
        - [4.2.1.3.2 General And Independent State Information](#4.2.1.3.2)
      - [4.2.1.4 Do _Not_ Include Atomic Type Names](#cpp-vars-naming-atomic)
      - [4.2.1.5 Arrays](#cpp-vars-naming-arrays)
  - [4.3 Statements](#cpp-statements)
  - [4.4 Functions](#cpp-functions)
    - [4.4.1 Avoid passing Literals](#cpp-functions-passing-literals)
  - [4.5 Structs](#cpp-structs)
  - [4.6 Classes](#cpp-classes)
    - [4.6.1 Naming](#cpp-classes-naming)
    - [4.6.2 Data Members/Properties](#cpp-classes-data-members)
      - [4.6.2.1 Naming](#cpp-classes-data-members-naming)
        - [4.6.2.1.1 Complex States](#cpp-classes-data-members-naming-complex-states)
        - [4.6.2.1.2 Considered Context](#cpp-classes-data-members-naming-context)
        - [4.6.2.1.3 Do Include Non-Atomic Type Names](#cpp-classes-data-members-naming-atomic-names)
      - [4.6.2.2 Editable Data Members](#cpp-classes-data-members-editable)
        - [4.6.2.2.1 Slider And Value Ranges](#cpp-classes-data-members-editable-ranges)
      - [4.6.2.3 Categories](#cpp-classes-data-members-categories)
      - [4.6.2.4 Data Members Access Level](#cpp-classes-data-members-access)
      - [4.6.2.5 Advanced Display](#cpp-classes-data-members-advanced)
      - [4.6.2.6 Interface Data Members](#cpp-classes-data-members-interface)
    - [4.6.3 cpp-classes-component-data-members](#cpp-classes-component-data-members)
      - [4.6.3.1 Naming](#cpp-classes-component-data-members-naming)
      - [4.6.3.2 Garbage Collection](#cpp-classes-component-data-members-gc)
    - [4.6.4 Functions/Methods](#cpp-classes-funcs)
      - [4.6.4.1 Naming](#cpp-classes-funcs-naming)
        - [4.6.4.1.1 All Functions Should Be Verbs](#cpp-classes-funcs-naming-verbs)
        - [4.6.4.1.2 Property RepNotify Functions Always `OnRep_Variable`](#cpp-classes-funcs-naming-onrep)
        - [4.6.4.1.3 Info Functions Returning Bool Should Ask Questions](#cpp-classes-funcs-naming-bool)
        - [4.6.4.1.4 Remote Procedure Calls Should Be Prefixed With Target](#cpp-classes-funcs-naming-rpcs)
      - [4.6.4.2 Getters and Setters](#cpp-classes-funcs-getset)
      - [4.6.4.3 Inline Functions](#cpp-classes-funcs-inline)
      - [4.6.4.4 Const Correctness](#cpp-classes-funcs-const)
      - [4.6.4.5 Parameter Names](#cpp-classes-funcs-params)
        - [4.6.4.5.1 Names](#cpp-classes-funcs-params-names)
        - [4.6.4.5.2 Const Correctness](#cpp-classes-funcs-params-const)
        - [4.6.4.5.3 Avoid boolean flags parameters](#cpp-classes-funcs-params-bool-flags)
  - [4.7 Enums](#cpp-enums)
    - [4.7.1 Naming](#cpp-enums-naming)
      - [4.7.1.1 Enum Values Prefix](#cpp-enums-naming-value-prefix)
    - [4.7.2 Display Name](#cpp-enums-displayname)
    - [4.7.3 Enums as Flags](#cpp-enums-flags)
  - [4.8 Interfaces](#cpp-interfaces)
    - [4.8.1 Naming](#cpp-interfaces-naming)
    - [4.8.2 Non-pure functions in Interfaces](#cpp-interfaces-non-pure-functions)
  - [4.9 Delegates and Events](#cpp-delegates-and-events)
    - [4.9.1 Naming](#cpp-events-naming)
      - [4.9.1.1 Delegate Declarations, Events, Event Handlers and Event Dispatchers Should Start With `On`](#cpp-events-naming-eventhandlers)
      - [4.9.1.2 Internal Delegates Should Not Start With `On` and Should End With `Delegate`](#cpp-events-naming-internal-delegates)
    - [4.9.2 Event Binding](#cpp-events-binding)
  - [4.10 Typedefs](#cpp-typedefs)
  - [4.11 Macros](#cpp-macros)
  - [4.12 Comments](#cpp-comments)
    - [4.12.1 Third Party Code](#cpp-comments-thirdparty)
  - [4.13 Namespaces](#cpp-namespaces)
- [5. Blueprints](#bp)
  - [5.1 Compiling](#bp-compiling)
  - [5.2 Variables](#bp-vars)
    - [5.2.1 Naming](#bp-vars-naming)
    - [5.2.2 Editable Variables](#bp-vars-editable)
      - [5.2.2.1 Tooltips](#bp-vars-editable-tooltips)
    - [5.2.3 Variable Access Level](#bp-vars-access)
    - [5.2.4 Advanced Display](#bp-vars-advanced)
    - [5.2.5 Transient Variables](#bp-vars-transient)
    - [5.2.6 Config Variables](#bp-vars-config)
  - [5.3 Functions, Delegates, Events, Event Handlers, and Event Dispatchers](#bp-funcs)
    - [5.3.1 Function Naming](#bp-funcs-naming)
      - [5.3.1.1 Event Handlers and Dispatchers Should Start With `On`](#bp-funcs-naming-eventhandlers)
    - [5.3.2 All Functions Must Have Return Nodes](#bp-funcs-return)
    - [5.3.3 No Function Should Have More Than 50 Nodes](#bp-funcs-node-limit)
    - [5.3.4 All Public Functions Should Have A Description](#bp-funcs-description)
    - [5.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name](#bp-funcs-plugin-category)
  - [5.4 Blueprint Graphs](#bp-graphs)
    - [5.4.1 No Spaghetti](#bp-graphs-spaghetti)
    - [5.4.2 Align Wires Not Nodes](#bp-graphs-align-wires)
    - [5.4.3 White Exec Lines Are Top Priority](#bp-graphs-exec-first-class)
    - [5.4.4 Place All Parameters Under The Node They Go To](#bp-graphs-parameters-under-node)
    - [5.4.5 Do Not Favor Property Reuse, Favor Additional Getters](#bp-graphs-no-property-reuse)
    - [5.4.6 Graphs Should Be Reasonably Commented](#bp-graphs-block-comments)
    - [5.4.7 Graphs Should Handle Casting Errors Where Appropriate](#bp-graphs-cast-error-handling)
    - [5.4.8 Graphs Should Not Have Any Dangling / Loose / Dead Nodes](#bp-graphs-dangling-nodes)
- [6. Static Meshes](#5)
  - [6.1 Static Mesh UVs](#s-uvs)
    - [6.1.1 All Meshes Must Have UVs](#s-uvs-no-missing)
    - [6.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps](#s-uvs-no-overlapping)
  - [6.2 LODs Should Be Set Up Correctly](#s-lods)
  - [6.3 Modular Socketless Assets Should Snap To The Grid Cleanly](#s-modular-snapping)
  - [6.4 All Meshes Must Have Collision](#s-collision)
  - [6.5 All Meshes Should Be Scaled Correctly](#s-scaled)
- [7. Niagara](#Niagara)
  - [7.1 No Spaces, Ever](#ng-rules)
- [8. Levels / Maps](#levels)
  - [8.1 No Errors Or Warnings](#levels-no-errors-or-warnings)
  - [8.2 Lighting Should Be Built](#levels-lighting-should-be-built)
  - [8.3 No Player Visible Z Fighting](#levels-no-visible-z-fighting)
  - [8.4 Marketplace Specific Rules](#levels-mp-rules)
    - [8.4.1 Overview Level](#levels-mp-rules-overview)
    - [8.4.2 Demo Level](#levels-mp-rules-demo)
- [9. Textures](#textures)
  - [9.1 Dimensions Are Powers of 2](#textures-dimensions)
  - [9.2 Texture Density Should Be Uniform](#textures-density)
  - [9.3 Textures Should Be No Bigger than 8192](#textures-max-size)
  - [9.4 Textures Should Be Grouped Correctly](#textures-group)

## Important Terminology

<a name="terms-level-map"></a>
##### Levels/Maps

The word 'map' generally refers to what the average person calls a 'level' and may be used interchangeably. See this term's history [here](https://en.wikipedia.org/wiki/Level_(video_gaming)).

> **_NOTE_:** With that being said, the Levels/Maps folder will be named `Maps` (to align with most projects and conventions) while the Levels will be prefixed with `LVL_` (to align with UE Standards).

<a name="terms-identifiers"></a>
##### Identifiers
An `Identifier` is anything that resembles or serves as a "name". For example, the name of an asset, or the name of a material later, or a blueprint property, a variable, or a folder name, or for a data table row name, etc...

<a name="terms-cases"></a>
##### Cases

There are a few different ways you can `CaseWordsWhenNaming`. Here are some common casing types:

> ###### PascalCase
>
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
>
> ###### camelCase
>
> The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### Snake_case
>
> Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

> **_NOTE_:** Aligning with the UE Standards, 99% of the time we will be using `PascalCase`.

<a name="terms-var-prop"></a>
##### Variables / Properties

The words 'variable' and 'property' in most contexts are interchangable. If they are both used together in the same context however:

<a name="terms-property"></a>
###### Property
Usually refers to a variable defined in a class. For example, if `BP_Barrel` had a variable `bExploded`, `bExploded` may be referred to as a property of `BP_Barrel`.

When in the context of a class, it is often used to imply accessing previously defined data.

<a name="terms-variable"></a>
###### Variable
Usually refers to a variable defined as a function argument or a local variable inside a function.

When in the context of a class, it is often used to convey discussion about its definition and what it will hold.

<a name="0"></a>
## 0. Principles

These principles have been adapted from [idomatic.js style guide](https://github.com/rwaldron/idiomatic.js/).

<a name="0.1"></a>
### 0.1 All structure, assets, and code in any Unreal Engine 5 project should look like a single person created it, no matter how many people contributed

Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style.

<a name="0.2"></a>
### 0.2 Friends do not let friends have bad style

If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community such as [Unreal Slackers](http://join.unrealslackers.org/), it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's Blueprint spaghetti or deal with assets that have names they can't understand.

If you are helping someone whose work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them to one.

<a name="0.3"></a>
### 0.3 A team without a style guide is no team of mine

When joining an Unreal Engine 5 team, one of your first questions should be "Do you have a style guide?". If the answer is no, you should suggest them one. If they don't want to use a style guide, be skeptical about their ability to work as a team.

**[⬆ Back to Top](#table-of-contents)**


<a name="1"></a>
## 1. Globally Enforced Opinions

<a name="1.1"></a>
### 1.1 Forbidden Characters

<a name="identifiers"></a>
<a name="1.1.1"></a>
#### Identifiers

In any `Identifier` of any kind, **never** use the following unless absolutely forced to:

* White space of any kind
* Backward slashes `\`
* Symbols i.e. `#!@$%`
* Any Unicode character

Any `Identifier` should strive to only have the following characters when possible (the RegEx `[A-Za-z0-9_]+`)

* ABCDEFGHIJKLMNOPQRSTUVWXYZ
* abcdefghijklmnopqrstuvwxyz
* 1234567890
* _ (sparingly)

The reasoning for this is this will ensure the greatest compatibility of all data across all platforms across all tools, and help prevent downtime due to potentially bad character handling for identifiers in code you don't control.

**[⬆ Back to Top](#table-of-contents)**


<a name="2"></a>
<a name="anc"></a>
## 2. Asset Naming Conventions

Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched, parsed, and maintained with incredible ease.

Most things are prefixed with prefixes being generally an acronym of the asset type followed by an underscore.

<a name="base-asset-name"></a>
<a name="2.1"></a>
### 2.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`

All assets should have a _Base Asset Name_. A Base Asset Name represents a logical grouping of related assets. Any asset that is part of this logical group should follow the standard of  `Prefix_BaseAssetName_Variant_Suffix`.

Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` and in mind and using common sense is generally enough to warrant good asset names. Here are some detailed rules regarding each element.

`Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) tables.

`BaseAssetName` should be determined by a short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.

For unique and specific variations of assets, `Variant` is either a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred to as `Bob_Retro`.

For unique but generic variations of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.

Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

<a name="2.1-examples"></a>
#### 2.1 Examples

##### 2.1e1 Bob

| Asset Type              | Asset Name                                                 |
| ----------------------- | ---------------------------------------------------------- |
| Material                | M_Bob                                                      |
| Skeletal Mesh           | SK_Bob                                                     |
| Texture (Diffuse/Albedo)| T_Bob_D                                                    |
| Texture (Normal)        | T_Bob_N                                                    |
| Texture (Evil Diffuse)  | T_Bob_Evil_D                                               |

##### 2.1e2 Rocks

| Asset Type              | Asset Name                                                 |
| ----------------------- | ---------------------------------------------------------- |
| Material                | M_Rock                                                     |
| Material Instance (Snow)| MI_Rock_Snow                                               |
| Static Mesh (01)        | SM_Rock_01                                                 |
| Static Mesh (02)        | SM_Rock_02                                                 |
| Static Mesh (03)        | SM_Rock_03                                                 |

<a name="asset-name-modifiers"></a>
<a name="2.2"></a>
### 2.2 Asset Name Modifiers

When naming an asset, use these tables to determine the prefix and suffix to use with an asset's [Base Asset Name](#base-asset-name).

<a name="anc-animations"></a>
<a name="2.2.1"></a>
#### 2.2.1 Animations

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Aim Offset              | AO_        |            |                                  |
| Aim Offset 1D           | AO_        | _1D        |                                  |
| Animation Blueprint     | ABP_       |            |                                  |
| Animation Composite     | AC_        |            |                                  |
| Animation Montage       | AM_        |            |                                  |
| Animation Sequence      | AS_        |            |                                  |
| Blend Space             | BS_        |            |                                  |
| Blend Space 1D          | BS_        | _1D        |                                  |
| IK Rig                  | IK_        |            |                                  |
| IK Retargeter           | RTG_       |            |                                  |
| Level Sequence          | LS_        |            |                                  |
| Morph Target            | MT_        |            |                                  |
| Rig                     | Rig_       |            |                                  |
| Sequencer Edits         | EDIT_      |            |                                  |
| Skeletal Mesh           | SK_        |            |                                  |
| Skeleton                | SKEL_      |            |                                  |

<a name="anc-ai"></a>
<a name="2.2.2"></a>
### 2.2.2 Artificial Intelligence

| Asset Type              | Prefix       | Suffix     | Notes                            |
| ----------------------- | ------------ | ---------- | -------------------------------- |
| AI Controller           | AIC_         |            |                                  |
| Behavior Tree           | BT_          |            |                                  |
| Blackboard              | BB_          |            |                                  |
| Decorator               | BTDecorator_ |            |                                  |
| Environment Query       | EQS_         |            |                                  |
| EnvQueryContext         | EQS_         | Context    |                                  |
| Service                 | BTService_   |            |                                  |
| Task                    | BTTask_      |            |                                  |

<a name="anc-bp"></a>
<a name="2.2.3"></a>
### 2.2.3 Blueprints

| Asset Type                 | Prefix     | Suffix     | Notes                            |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| Blueprint                  | BP_        |            |                                  |
| Blueprint Component        | BP_        | Component  | I.e. BP_InventoryComponent       |
| Blueprint Function Library | BPFL_      |            |                                  |
| Blueprint Interface        | BPI_       |            |                                  |
| Blueprint Macro Library    | BPML_      |            | Do not use macro libraries if possible. |
| Enumeration                | E          |            | No underscore.                   |
| Structure                  | F or S     |            | No underscore.                   |
| Tutorial Blueprint         | TBP_       |            |                                  |
| Widget Blueprint           | WBP_       |            |                                  |

<a name="anc-effects"></a>
<a name="2.2.4"></a>
### 2.2.4 Effects

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Niagara Emitter         | FXE_       |            |                                  |
| Niagara System          | FXS_       |            |                                  |
| Niagara Function        | FXF_       |            |                                  |
| Particle System         | PS_        |            |                                  |

<a name="anc-inputs"></a>
<a name="2.2.5"></a>
### 2.2.5 Inputs

| Asset Type                    | Prefix     | Suffix     | Notes                            |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Force Feedback Effect         | FFE_       |            |                                  |
| Input Action                  | IA_        |            |                                  |
| Input Mapping Context         | IMC_       |            |                                  |

<a name="anc-materials"></a>
<a name="2.2.6"></a>
### 2.2.6 Materials

| Asset Type                    | Prefix     | Suffix     | Notes                            |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Material                      | M_         |            |                                  |
| Material Function             | MF_        |            |                                  |
| Material Instance             | MI_        |            |                                  |
| Material Parameter Collection | MPC_       |            |                                  |
| Subsurface Profile            | SP_        |            |                                  |
| Post Process Material         | PPM_       |            |                                  |
| Decal                         | M_, MI_    | _Decal     |                                  |

<a name="anc-paper2d"></a>
<a name="2.2.7"></a>
### 2.2.7 Paper 2D

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          | PFB_       |            |                                  |
| Sprite                  | SPR_       |            |                                  |
| Sprite Atlas Group      | SPRG_      |            |                                  |
| Sprite Sheet            | SS_        |            |                                  |
| Tile Map                | TM_        |            |                                  |
| Tile Set                | TS_        |            |                                  |

<a name="anc-paperzd"></a>
<a name="2.2.8"></a>
### 2.2.8 Paper ZD

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Animation Blueprint     | ABP_       | _2D        |                                  |
| Animation Sequence      | AS_        | _2D        |                                  |
| Animation Source        | ASRC_      |            |                                  |

<a name="anc-physics"></a>
<a name="2.2.9"></a>
### 2.2.9 Physics

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Physical Material       | PM_        |            |                                  |
| Physics Asset           | PHYS_      |            |                                  |
| Destructible Mesh       | DM_        |            |                                  |

<a name="anc-sounds"></a>
<a name="2.2.10"></a>
### 2.2.10 Sounds

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          | DV_        |            |                                  |
| Dialogue Wave           | DW_        |            |                                  |
| Media Output            | MO_        |            |                                  |
| Media Player            | MP_        |            |                                  |
| Media Profile           | MPR_       |            |                                  |
| Media Sound Wave        | MSW_       |            |                                  |
| Media Source            | MS_        |            |                                  |
| Reverb Effect           | Reverb_    |            |                                  |
| Sound Attenuation       | ATT_       |            |                                  |
| Sound Class             |            |            | No prefix/suffix. Should be put in a folder called SoundClasses |
| Sound Concurrency       |            | _SC        | Should be named after a SoundClass |
| Sound Cue               | A_         | _Cue       |                                  |
| Sound Mix               | Mix_       |            |                                  |
| Sound Wave              | A_         |            |                                  |

<a name="anc-textures"></a>
<a name="2.2.11"></a>
### 2.2.11 Textures

| Asset Type                          | Prefix        | Suffix     | Notes                            |
| ----------------------------------- | ------------- | ---------- | -------------------------------- |
| Texture                             | T_            |            |                                  |
| Texture (Diffuse/Albedo/Base Color) | T_            | _D         |                                  |
| Texture (Normal)                    | T_            | _N         |                                  |
| Texture (Roughness)                 | T_            | _R         |                                  |
| Texture (Alpha/Opacity)             | T_            | _A         |                                  |
| Texture (Ambient Occlusion)         | T_            | _O         |                                  |
| Texture (Bump)                      | T_            | _B         |                                  |
| Texture (Emissive)                  | T_            | _E         |                                  |
| Texture (Mask)                      | T_            | _M         |                                  |
| Texture (Specular)                  | T_            | _S         |                                  |
| Texture (Metallic)                  | T_            | _M         |                                  |
| Texture (Packed)                    | T_            | _*         | See notes below about [packing](#anc-textures-packing). |
| Texture Cube                        | TC_           |            |                                  |
| Media Texture                       | MT_           |            |                                  |
| Render Target                       | RT_           |            |                                  |
| Cube Render Target                  | RTC_          |            |                                  |
| Texture Light Profile               | TLP           |            |                                  |

<a name="anc-textures-packing"></a>
<a name="2.2.11.1"></a>
#### 2.2.11.1 Texture Packing
It is common practice to pack multiple layers of texture data into one texture. An example of this is packing Emissive, Roughness, Ambient Occlusion together as the Red, Green, and Blue channels of a texture respectively. To determine the suffix, simply stack (in lexicographic order) the given suffix letters from above together, e.g. `_ERO`.

> It is generally acceptable to include an Alpha/Opacity layer in your Diffuse/Albedo's alpha channel and as this is common practice, adding `A` to the `_D` suffix is optional.

Packing 4 channels of data into a texture (RGBA) is not recommended except for an Alpha/Opacity mask in the Diffuse/Albedo's alpha channel as a texture with an alpha channel incurs more overhead than one without.

<a name="anc-ui"></a>
<a name="2.2.12"></a>
### 2.2.12 User Interface

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    | Font_      |            |                                  |
| Slate Brush             | Brush_     |            |                                  |
| Slate Widget Style      | Style_     |            |                                  |

<a name="anc-misc"></a>
<a name="2.2.13"></a>
### 2.2.13 Miscellaneous

| Asset Type                 | Prefix     | Suffix     | Notes                            |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| Animated Vector Field      | VFA_       |            |                                  |
| Camera Anim                | CA_        |            |                                  |
| Color Curve                | Curve_     | _Color     |                                  |
| Curve Table                | Curve_     | _Table     |                                  |
| Data Asset                 | *_         |            | Prefix should be based on class. |
| Data Table                 | DT_        |            |                                  |
| File Media Source          | FMS_       |            |                                  |
| Float Curve                | Curve_     | _Float     |                                  |
| Foliage Type               | FT_        |            |                                  |
| Force Feedback Effect      | FFE_       |            |                                  |
| HDRI                       | HDR_       |            |                                  |
| Landscape Grass Type       | LG_        |            |                                  |
| Landscape Layer            | LL_        |            |                                  |
| Level / Map                | LVL_       |            | [Should be in a folder called Maps.](#3.4) |
| Level Instance             | LVLI_      |            |                                  |
| Level (Audio)              | LVL_       | _Audio     |                                  |
| Level (Gameplay)           | LVL_       | _Gameplay  |                                  |
| Level (Geometry)           | LVL_       | _Geo       |                                  |
| Level (Lighting)           | LVL_       | _Lighting  |                                  |
| Level (Persistent)         | LVL_       | _P         |                                  |
| Level Snapshot             | SNAP_      |            |                                  |
| Matinee Data               | Matinee_   |            |                                  |
| NDisplay Configuration     | NDC_       |            |                                  |
| Object Library             | OL_        |            |                                  |
| OCIO Profile               | OCIO_      |            |                                  |
| Redirector                 |            |            | These should be fixed up ASAP.   |
| Remote Conrtol Preset      | RCP_       |            |                                  |
| Static Mesh                | SM_        |            |                                  |
| Static Vector Field        | VF_        |            |                                  |
| Substance Graph Instance   | SGI_       |            |                                  |
| Substance Instance Factory | SIF_       |            |                                  |
| Touch Interface Setup      | TI_        |            |                                  |
| Vector Curve               | Curve_     | _Vector    |                                  |

**[⬆ Back to Top](#table-of-contents)**


<a name="3"></a>
<a name="structure"></a>
## 3. Content Directory Structure

Equally important as asset names, the directory structure style of a project should be considered law. Asset naming conventions and content directory structure go hand in hand, and a violation of either causes unneeded chaos.

There are multiple ways to lay out the content of a UE5 project. In this style, we will be using a structure that relies more on filtering and search abilities of the Content Browser for those working with assets to find assets of a specific type instead of another common structure that groups asset types with folders.

> If you are using the prefix [naming convention](#2.2) above, using folders to contain assets of similar types such as `Meshes`, `Textures`, and `Materials` is a redundant practice as asset types are already both sorted by prefix as well as able to be filtered in the content browser.

<a name="3e1"><a>
### 3e1 Example Project Content Structure
<pre>
|-- Content
    |-- <a href="#3.2">Game Name</a>
        |-- Art
        |-- Audio
        |   |-- Music
        |   |-- Nature
        |   |   |-- Ambient
        |   |   |-- Foliage
        |   |   |-- Rocks
        |   |   |-- Trees
        |   |-- SFX
        |-- Characters
        |   |-- Bob
        |   |-- Common
        |   |   |-- <a href="#3.7">Animations</a>
        |   |   |   |-- Cinematic
        |   |   |   |-- Locomotion
        |   |   |-- Audio
        |   |-- Jack
        |   |-- Steve
        |   |-- <a href="#3.1.3">Zoe</a>
        |-- <a href="#3.5">Core</a>
        |   |-- Characters
        |   |-- Controllers
        |   |-- Engine
        |   |-- <a href="#3.1.2">GameModes</a>
        |   |   |-- GameStates
        |   |-- Inputs
        |   |   |-- Actions
        |   |-- Interactables
        |   |-- Pickups
        |   |-- Weapons
        |-- Effects
        |   |-- Electrical
        |   |-- Fire
        |   |-- Weather
        |-- <a href="#3.4">Maps</a>
        |   |-- Gyms
        |   |-- Level_0
        |   |-- Level_1
        |-- <a href="#3.8">MaterialLibrary</a>
        |   |-- Debug
        |   |-- Metal
        |   |-- Paint
        |   |-- Utility
        |   |-- Weathering
        |-- Placeables
        |   |-- Pickups
        |-- Weapons
            |-- Common
            |-- Pistols
            |   |-- DesertEagle
            |   |-- RocketPistol
            |-- Rifles
</pre>

The reasons for this structure are listed in the following sub-sections.

<a name="3.1"></a>
<a name="structure-folder-names"><a>
### 3.1 Folder Names

These are common rules for naming any folder in the content structure.

<a name="3.1.1"></a>
#### 3.1.1 Always Use PascalCase[<sup>*</sup>](#terms-cases)

PascalCase refers to starting a name with a capital letter and then instead of using spaces, every following word also starts with a capital letter. For example, `DesertEagle`, `RocketPistol`, and `ASeriesOfWords`.

See [Cases](#terms-cases).

<a name="3.1.2"></a>
#### 3.1.2 Never Use Spaces

Re-enforcing [3.1.1](#3.1.1), never use spaces. Spaces can cause various engineering tools and batch processes to fail. Ideally, your project's root also contains no spaces and is located somewhere such as `D:\Project` instead of `C:\Users\My Name\My Documents\Unreal Projects`.

<a name="3.1.3"></a>
#### 3.1.3 Never Use Unicode Characters And Other Symbols

If one of your game characters is named 'Zoë', its folder name should be `Zoe`. Unicode characters can be worse than [Spaces](#3.1.2) for engineering tool and some parts of UE5 don't support Unicode characters in paths either.

Related to this, if your project has [unexplained issues](https://answers.unrealengine.com/questions/101207/undefined.html) and your computer's user name has a Unicode character (i.e. your name is `Zoë`), any project located in your `My Documents` folder will suffer from this issue. Often simply moving your project to something like `D:\Project` will fix these mysterious issues.

Using other characters outside `a-z`, `A-Z`, and `0-9` such as `@`, `-`, `_`, `,`, `*`, and `#` can also lead to unexpected and hard to track issues on other platforms, source control, and weaker engineering tools.

<a name="3.2"></a>
<a name="structure-top-level"><a>
### 3.2 Use A Top Level Folder For Project Specific Assets

All of a project's assets should exist in a folder named after the project. For example, if your project is named 'Generic Shooter', _all_ of it's content should exist in `Content/GenericShooter`.

Consier also set it as favorite and set its color to highlight it from all the other folders (I personally use `3333FFFF` (0.2, 0.2, 1.0)).

> The `Developers` folder is not for assets that your project relies on and therefore is not project specific. See [Developer Folders](#3.3) for details about this.

There are multiple reasons for this approach.

<a name="3.2.1"></a>
#### 3.2.1 No Global Assets

Often in code style guides it is written that you should not pollute the global namespace and this follows the same principle. When assets are allowed to exist outside of a project folder, it often becomes much harder to enforce a strict structure layout as assets not in a folder encourages the bad behavior of not having to organize assets.

Every asset should have a purpose, otherwise it does not belong in a project. If an asset is an experimental test and shouldn't be used by the project it should be put in a [`Developer`](#3.3) folder.

<a name="3.2.2"></a>
#### 3.2.2 Reduce Migration Conflicts

When working on multiple projects it is common for a team to copy assets from one project to another if they have made something useful for both. When this occurs, the easiest way to perform the copy is to use the Content Browser's Migrate functionality as it will copy over not just the selected asset but all of its dependencies.

These dependencies are what can easily get you into trouble. If two project's assets do not have a top level folder and they happen to have similarly named or already previously migrated assets, a new migration can accidentally wipe any changes to the existing assets.

This is also the primary reason why Fab (previously Epic's Marketplace) staff enforces the same policy for submitted assets.

After a migration, safe merging of assets can be done using the 'Replace References' tool in the content browser with the added clarity of assets not belonging to a project's top level folder are clearly pending a merge. Once assets are merged and fully migrated, there shouldn't be another top level folder in your Content tree. This method is _100%_ guaranteed to make any migrations that occur completely safe.

<a name="3.2.2e1"></a>
##### 3.2.2e1 Master Material Example

For example, say you created a master material in one project that you would like to use in another project so you migrated that asset over. If this asset is not in a top level folder, it may have a name like `Content/MaterialLibrary/M_Master`. If the target project doesn't have a master material already, this should work without issue.

As work on one or both projects progress, their respective master materials may change to be tailored for their specific projects due to the course of normal development.

The issue comes when, for example, an artist for one project created a nice generic modular set of static meshes and someone wants to include that set of static meshes in the second project. If the artist who created the assets used material instances based on `Content/MaterialLibrary/M_Master` as they're instructed to, when a migration is performed there is a great chance of conflict for the previously migrated `Content/MaterialLibrary/M_Master` asset.

This issue can be hard to predict and hard to account for. The person migrating the static meshes may not be the same person who is familiar with the development of both project's master material, and they may not be even aware that the static meshes in question rely on material instances which then rely on the master material. The Migrate tool requires the entire chain of dependencies to work however, and so it will be forced to grab `Content/MaterialLibrary/M_Master` when it copies these assets to the other project and it will overwrite the existing asset.

It is at this point where if the master materials for both projects are incompatible in _any way_, you risk breaking possibly the entire material library for a project as well as any other dependencies that may have already been migrated, simply because assets were not stored in a top level folder. The simple migration of static meshes now becomes a very ugly task.

<a name="3.2.3"></a>
#### 3.2.3 Samples, Templates, and Fab Content Are Risk-Free

An extension to [3.2.2](#3.2.2), if a team member decides to add sample content, template files, or assets they bought from Fab, it is guaranteed, as long your project's top-level folder is uniquely named, that these new assets will not interfere with your project.

You can not trust Fab content to fully conform to the [top level folder rule](#3.2). There exists many assets that have the majority of their content in a top level folder but also have possibly modified Epic sample content as well as level files polluting the global `Content` folder.

When adhering to [3.2](#3.2), the worst Fab conflict you can have is if two Fab assets both have the same Epic sample content. If all your assets are in a project specific folder, including sample content you may have moved into your folder, your project will never break.

<a name="3.2.4"></a>
#### 3.2.4 DLC, Sub-Projects, and Patches Are Easily Maintained

If your project plans to release DLC or has multiple sub-projects associated with it that may either be migrated out or simply not cooked in a build, assets relating to these projects should have their own separate top level content folder. This make cooking DLC separate from main project content far easier. Sub-projects can also be migrated in and out with minimal effort. If you need to change a material of an asset or add some very specific asset override behavior in a patch, you can easily put these changes in a patch folder and work safely without the chance of breaking the core project.

<a name="3.3"></a>
<a name="structure-developers"></a>
### 3.3 Use Developers Folder For Local Testing

During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control server. Not all teams require use of Developer folders, but ones that do use them often run into a common problem with assets submitted to source control.

It is very easy for a team member to accidentally use assets that are not ready for use, which will cause issues once those assets are removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they could be subject to incredible change and/or removal. This causes massive amounts of re-working for everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never have had a reason to use them and the whole issue would never happen. The Content Browser has specific View Options that will hide Developer folders (they are hidden by default) making it impossible to accidentally use Developer assets under normal use.

Once the assets are ready for use, an artist simply has to move the assets into the project specific folder and fix up redirectors. This is essentially 'promoting' the assets from experimental to production.

<a name="3.4"></a>
<a name="structure-maps"></a>
### 3.4 All Map[<sup>*</sup>](#terms-level-map) Files Belong In A Folder Called Maps

Map files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `/Content/Project/Maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `Maps`, such as `Maps/Campaign1/` or `Maps/Arenas`, but the most important thing here is that they all exist within `/Content/Project/Maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well as QA processes.

If Gym maps are used, put them under `/Content/Project/Maps/Gyms` (Consider setting a special color to this folder, as it has unique purpose, I personally set it to `404040FF` (0.25, 0.25, 0.25)).

<a name="3.5"></a>
<a name="structure-core"></a>
### 3.5 Use A `Core` Folder For Critical Blueprints And Other Assets

Use `/Content/Project/Core` folder for assets that are absolutely fundamental to a project's workings. For example, base `GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`, and related Blueprints should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the `Core` folder. Following good code structure style, designers should be making their gameplay tweaks in child classes that expose functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `Core/Pickups` that defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as `/Content/Project/Placeables/Pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not touch `Core/Pickups` as they may unintentionally break pickups project-wide.

<a name="3.6"></a>
<a name="structure-assettypes"></a>
### 3.6 Do Not Create Folders Called `Assets` or `AssetTypes`

<a name="3.6.1"></a>
#### 3.6.1 Creating a folder named `Assets` is redundant

All assets are assets.

<a name="3.6.2"></a>
#### 3.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant

All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `SM_` prefix for a static mesh is only two characters, whereas `Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<a name="3.7"></a>
<a name="structure-large-sets"></a>
### 3.7 Very Large Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [3.6](#3.6).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#3.8).

<a name="3.8"></a>
<a name="structure-material-library"></a>
### 3.8 `MaterialLibrary`

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Content/Project/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="3.9"></a>
<a name="structure-no-empty-folders"></a>
### 3.9 No Empty Folders

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:
1. Be sure you're using source control.
2. Immediately run Fix Up Redirectors on your project.
3. Navigate to the folder on-disk and delete the assets inside.
4. Close the editor.
5. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
6. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
7. Ensure the folder is now gone.
8. Submit changes to source control.

**[⬆ Back to Top](#table-of-contents)**

<a name="4"></a>
<a name="cpp"></a>
## 4. C++

This section will focus on C++ Coding standards. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

<a name="4.1"></a>
<a name="cpp-compiling"></a>
### 4.1 Compiling

All C++ code should compile with zero warnings and zero errors (ignore everything outside your game project). You should fix warnings immediately as they can quickly cascade into runtime errors and scary unexpected behavior (and even crash the engine).

<a name="4.2"></a>
<a name="cpp-vars"></a>
### 4.2 Variables

The word `variable` here refers to scoped variables inside statements. Not to be confused with `data members` (also referred as `property`) which are variables scoped under a specific `struct`/`class`. 

<a name="4.2.1"></a>
<a name="cpp-vars-naming"></a>
#### 4.2.1 Naming

<a name="4.2.1.1"></a>
<a name="cpp-vars-naming-nouns"></a>
##### 4.2.1.1 Nouns

All non-boolean variable names must be clear, unambiguous, and descriptive nouns.

<a name="4.2.1.2"></a>
<a name="cpp-vars-naming-case"></a>
##### 4.2.1.2 PascalCase

All non-boolean variables should be in the form of [PascalCase](#terms-cases) and should not include underscores between words.

Examples:

* `Score` **not** `score`
* `Kills` **not** `kills`
* `TargetPlayer` **not** `targetPlayer`
* `CrosshairColor` **not** `crosshair_color`

<a name="4.2.1.3"></a>
<a name="cpp-vars-bool-names"></a>
##### 4.2.1.3 Boolean Names

<a name="4.2.1.3.1"></a>
###### 4.2.1.3.1 Boolean `b` Prefix

All booleans should be named in PascalCase but prefixed with a lowercase `b`.

Example: Use `bDead` and `bEvil`, **not** `Dead` and `Evil`.

<a name="4.2.1.3.2"></a>
###### 4.2.1.3.2 General And Independent State Information

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase the variable as a question, such as `Is`. This is reserved for functions.

Example: Use `bDead` and `bHostile` **not** `bIsDead` and `bIsHostile`.

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

<a name="4.2.1.4"></a>
<a name="cpp-vars-naming-atomic"></a>
##### 4.2.1.4 Do _Not_ Include Atomic Type Names

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats, and enumerations.

Strings and vectors are considered atomic in terms of style when working with C++/Blueprints, however they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do _not_ consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of a string of characters is `String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted _and_ when using a name without a variable type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may potentially read as an Array of a variable type named `Post`.

<a name="4.2.1.5"></a>
<a name="cpp-vars-naming-arrays"></a>
##### 4.2.1.5 Arrays

Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.

<a name="4.3"></a>
<a name="cpp-statements"></a>
### 4.3 Statements

All statement bodies (`if`, `for`, etc.) should be wrapped with block wrappers (curly braces) instead of one liners.

Example:
```
// GOOD
if (bFalling)
{
  ...
}
else
{
  ...
}

// BAD
if (bfalling)
  ...
else
  ...
```

<a name="4.4"></a>
<a name="cpp-functions"></a>
### 4.4 Functions

<a name="4.4.1"></a>
<a name="cpp-functions-passing-literals"></a>
### 4.4.1 Avoid passing Literals

Avoid using literals in function calls.

Prefer named constants which describe their meaning. This makes intent more obvious as it avoids the need to look up the function declaration to understand it.

Example:
```
// Avoid
Trigger(TEXT("Soldier"), 5, true);.
 
// Instead use
const FName ObjectName                = TEXT("Soldier");
const float CooldownInSeconds         = 5;
const bool bVulnerableDuringCooldown  = true;
Trigger(ObjectName, CooldownInSeconds, bVulnerableDuringCooldown);
```

<a name="4.5"></a>
<a name="cpp-structs"></a>
### 4.5 Structs

As a rule of thumb all structs should be prefixed with `F`, and contain only data, no functionality.

<a name="4.6"></a>
<a name="cpp-classes"></a>
### 4.6 Classes

All classes should have the `UCLASS` macro (so they are exposed to Blueprints) and inherit from `UObject` or one of its derivatives.

<a name="4.6.1"></a>
<a name="cpp-classes-naming"></a>
#### 4.6.1 Naming

A class that inherits from `UObject` should be prefixed with `U`.

A class that inherits from `AActor` should be prefixed with `A`.

A class that inherits from `SWidget` should be prefixed with `S`.

<a name="4.6.2"></a>
<a name="cpp-classes-data-members"></a>
#### 4.6.2 Data Members/Properties

The words `data member` and `property` may be used interchangeably.

<a name="4.6.2.1"></a>
<a name="cpp-classes-data-members-naming"></a>
##### 4.6.2.1 Naming

Class data members namings should follow all rules stated in [C++ Variables Naming](#cpp-var-naming), with the addition of the following rules below.

<a name="4.6.2.1.1"></a>
<a name="cpp-classes-data-members-naming-complex-states"></a>
###### 4.6.2.1.1 Complex States

Do not to use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `EWeaponState` and use a data member with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined state names.

<a name="4.6.2.1.2"></a>
<a name="cpp-classes-data-members-naming-context"></a>
###### 4.6.2.1.2 Considered Context

All data member names must not be redundant with their context as all data member references always have context in a class/struct.

Examples:

Consider a Class called `APlayerCharacter`.

**Bad**

* `PlayerScore`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these data members are named redundantly. It is implied that the data member is representative of the `APlayerCharacter` it belongs to because it is `APlayerCharacter` that is defining these data members.

**Good**

* `Score`
* `Name`
* `Skills`
* `Skin`

<a name="4.6.2.1.3"></a>
<a name="cpp-classes-data-members-naming-atomic-names"></a>
###### 4.6.2.1.3 Do Include Non-Atomic Type Names

Non-atomic or complex data members are data members that represent data as a collection of atomic data members. Structs, Classes, Interfaces, and primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic data member type is a list of data members, Arrays do not change the 'atomicness' of a data member type.

These data members should include their type name while still considering their context.

If a class owns an instance of a complex data member, i.e. if a `APlayerCharacter` owns a `AHat`, it should be stored as the data member type as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex data member represents, you should use a noun along with the data member type.

Example: If a `ATurret` has the ability to target a `APlayerCharacter`, it should store its target as `TargetPlayer` as when in the context of `ATurret` it should be clear that it is a reference to another complex data member type that it does not own.

<a name="4.6.2.2"></a>
<a name="cpp-classes-data-members-editable"></a>
##### 4.6.2.2 Editable Data Members

All data members that are safe to change in an inheriting Blueprint should be marked with a `UPROPERTY` macro that has the `EditAnywhere`/`BlueprintReadWrite` specifiers.

> **_NOTE_:** I personally believe that having a data member both `EditAnywhere` and `BlueprintReadWrite` can lead to unexpected runtime behavior, especially for designers since this is exposing the member for editing in one too many places.
> Due to that, I personally prefer using the next two combinations `UPROPERTY(EditAnywhere + BlueprintReadOnly)` or `UPROPERTY(VisibleAnywhere + BlueprintReadWrite)`.
> On that note, I also prefer the usage of `EditDefaultsOnly` and `EditInstanceOnly` in favor of `EditAnywhere`, due to similar reasons.

<a name="4.6.2.2.1"></a>
<a name="cpp-classes-data-members-editable-ranges"></a>
###### 4.6.2.2.1 Slider And Value Ranges

All `Editable` data members should make use of slider and value ranges if there is ever a value that should _not_ be allowed.

Example: A class that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

<a name="4.6.2.3"></a>
<a name="cpp-classes-data-members-categories"></a>
##### 4.6.2.3 Categories

If a class has only a small number of data members, categories are not required.

If a class has a moderate amount of data members (5-10), all `Editable` data members should have a non-default category assigned. A common category is `Config`.

If a class has a large amount of data members, all `Editable` data members should be categorized into sub-categories using the category `Config` as the base category. Non-editable data members should be categorized into descriptive categories describing their usage.

> You can define sub-categories by using the pipe character `|`, i.e. `Config | Animations`.

Example: A weapon class set of data members might be organized as:

    |-- Config
    |    |-- Animations
    |    |-- Effects
    |    |-- Audio
    |    |-- Recoil
    |    |-- Timings
    |-- Animations
    |-- Input
    |-- State
    |-- Visuals

<a name="4.6.2.4"></a>
<a name="cpp-classes-data-members-access"></a>
##### 4.6.2.4 Data Members Access Level

In C++, data members have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

All data members should be marked as `protected` or `private` according to their needs, but never `public`! If a data member needs to be accessed from a different class, define a Getter function.

<a name="4.6.2.5"></a>
<a name="cpp-classes-data-members-advanced"></a>
##### 4.6.2.5 Advanced Display

If a data member should be editable but often untouched, add the `Advanced Display` specifier. This makes the data member hidden unless the advanced display arrow is clicked.

<a name="4.6.2.6"></a>
<a name="cpp-classes-data-members-interface"></a>
#### 4.6.2.6 Interface Data Members

An interface data member (whose type leverages `UInterface`) should be stored using `TScriptInterface<T>` of that interface type.

This allows for easier use and safe copying of the interface pointer as well as the `UObject` that implements it.

References:
[Determine Whether a Class Implements an Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/interfaces-in-unreal-engine#determinewhetheraclassimplementsaninterface)
[Safely Store Object and Interface Pointers](https://dev.epicgames.com/documentation/en-us/unreal-engine/interfaces-in-unreal-engine#safelystoreobjectandinterfacepointers)

<a name="4.6.3"></a>
<a name="cpp-classes-component-data-members"></a>
#### 4.6.3 cpp-classes-component-data-members

A data member that inherits from `UActorComponent` is a component data member.

<a name="4.6.3.1"></a>
<a name="cpp-classes-component-data-members-naming"></a>
##### 4.6.3.1 Naming

A component data member should be suffixed with `Comp`.

A component data member's object name shouldn't be suffixed with `Comp` or `Component`, as this is redundant.

Example: Favor `SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("Spring Arm"));` over `SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("Spring Arm Component"));`.

<a name="4.6.3.2"></a>
<a name="cpp-classes-component-data-members-gc"></a>
##### 4.6.3.2 Garbage Collection

A component data member should have a `UPROPERTY` macro so it's exposed to UE Garbage Collection, and preferably leverage `TObjectPtr<T>` instead of a raw pointer.

> **_NOTE_:** `TObjectPtr<T>` was introduced in UE5, and although is optional, considered a better practice. See [C++ Object Pointer Properties](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-5-migration-guide#c++objectpointerproperties)

<a name="4.6.4"></a>
<a name="cpp-classes-funcs"></a>
#### 4.6.4 Functions/Methods

This section describes how you should author class functions.

A method is a function belonging to a class, so the words 'method' and 'function' are interchangable in most contexts.

<a name="4.6.4.1"></a>
<a name="cpp-classes-funcs-naming"></a>
##### 4.6.4.1 Naming

The naming of functions is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

Function declarations should be in a single line. In case of many parameters, split the parameters to several lines.

<a name="4.6.4.1.1"></a>
<a name="cpp-classes-funcs-naming-verbs"></a>
###### 4.6.4.1.1 All Functions Should Be Verbs

All functions perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy`

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

<a name="4.6.4.1.2"></a>
<a name="cpp-classes-funcs-naming-onrep"></a>
###### 4.6.4.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`, and exposed to Blueprints.

<a name="4.6.4.1.3"></a>
<a name="cpp-classes-funcs-naming-bool"></a>
###### 4.6.4.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#cpp-classes-funcs-naming-verbs).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

<a name="4.6.4.1.4"></a>
<a name="cpp-classes-funcs-naming-rpcs"></a>
###### 4.6.4.1.4 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be prefixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the prefix, follow all other rules regarding function naming.

Good examples:

* `ServerFireWeapon`
* `ClientNotifyDeath`
* `MulticastSpawnTracerEffect`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.

<a name="4.6.4.2"></a>
<a name="cpp-classes-funcs-getset"></a>
##### 4.6.4.2 Getters and Setters

Classes that want to expose private/protected data members for editting through other classes should add Getter and Setter functions.

When using Unreal Engine's API always prefer using a Getter instead of the actual data memeber. This is because the API changes, and at some point the said data member could become private, resulting in a code break.

<a name="4.6.4.3"></a>
<a name="cpp-classes-funcs-inline"></a>
##### 4.6.4.3 Inline Functions

Functions that are used as trivial accessors should always be inline functions and have the `FORCEINLINE` macro.

But do not overuse `FORCEINLINE` for everything one line function, as this forces rebuilds.

<a name="4.6.4.4"></a>
<a name="cpp-classes-funcs-const"></a>
##### 4.6.4.4 Const Correctness

If a method doesn't modify the state of the object, mark it as `const`.

Example:
```
void FThing::SomeNonMutatingOperation() const
{
    // This code will not modify the FThing it is invoked on
}
```

<a name="4.6.4.5"></a>
<a name="cpp-classes-funcs-params"></a>
##### 4.6.4.5 Parameters

<a name="4.6.4.5.1"></a>
<a name="cpp-classes-funcs-params-names"></a>
##### 4.6.4.5.1 Names

If a function parameter is passed by reference, and it's expected that the function will edit its value, it is recommended to be prefixed with `Out`.

If the parameter is a boolean, prefix with `b` before `In`/`Out` prefixes.

<a name="4.6.4.5.2"></a>
<a name="cpp-classes-funcs-params-const"></a>
##### 4.6.4.5.2 Const Correctness

If a function parameter is not intended to be modified by the function pass it as `const` pointer/reference.

Example: 
```
void SomeMutatingOperation(FThing& OutResult, const TArray<Int32>& Array)
{
    // Array will not be modified here, but OutResult probably will be
}
```

<a name="4.6.4.5.3"></a>
<a name="cpp-classes-funcs-params-bool-flags"></a>
##### 4.6.4.5.3 Avoid boolean flags parameters

Avoid using many boolean parameters in a function, instead prefer [Enum Flags](#cpp-enums-flags).

Example:
```
// Avoid
FCup* MakeCupOfTea(FTea* Tea, bool bAddSugar = false, bool bAddMilk = false, bool bAddHoney = false, bool bAddLemon = false);
FCup* Cup = MakeCupOfTea(Tea, false, true, true);
 
// Instead use
enum class ETeaFlags
{
    None,
    Milk  = 0x01,
    Sugar = 0x02,
    Honey = 0x04,
    Lemon = 0x08
};
ENUM_CLASS_FLAGS(ETeaFlags)
 
FCup* MakeCupOfTea(FTea* Tea, ETeaFlags Flags = ETeaFlags::None);
```

<a name="4.7"></a>
<a name="cpp-enums"></a>
### 4.7 Enums

An enumeration (`Enum`) is often used to store a finite amount of options, such as a state.

In Unreal Engine Enums should often use the `UENUM()` macro to be exposed to Blueprints.

Enums that are exposed to Blueprints, must be of type `uint8`.

<a name="4.7.1"></a>
<a name="cpp-enums-naming"></a>
#### 4.7.1 Naming

Enums should always be prefixed with `E`.

<a name="4.7.1.1"></a>
<a name="cpp-enums-naming-value-prefix"></a>
##### 4.7.1.1 Enum Values Prefix

It is common (not always) to prefix each value in the Enum with an abbreviation of the Enum name.

Example:

```
UENUM()
enum class ECurveEditorSnapAxis : uint8
{
	CESA_None UMETA(DisplayName = "None"),
	CESA_X UMETA(DisplayName = "X Only"),
	CESA_Y UMETA(DisplayName = "Y Only")
};
```

This rule is important in case you are not using a class enum, in which case the enum name isn't required when passing that enum's value. In that case the abbreviation adds clarity to what this enum is.

In case you do use a class enum, then the only advantage of this rule is that it's easier to find the enum in an IDE by writing the abbreviation. But this is less relevant with modern IDEs such as JetBrains Rider that finds classes by the abbreviation anyway.

<a name="4.7.2"></a>
<a name="cpp-enums-displayname"></a>
#### 4.7.2 Display Name

Favor using (especially for unclear enum values) the `UMETA()` macro and adding a `DisplayName` for a friendly clear display name in Blueprints.

Example:

```
UENUM()
enum class EMaterialBakeMethod : uint8
{
	IndividualMaterial UMETA(DisplayName = "Bake out Materials Individually"),
	AtlasMaterial UMETA(DisplayName = "Combine Materials into Atlassed Material"),
	BinnedMaterial UMETA(DisplayName = "Combine Materials into Binned Material")
};
```

<a name="4.7.3"></a>
<a name="cpp-enums-flags"></a>
#### 4.7.3 Enums as Flags

Enum classes used as flags should use `ENUM_CLASS_FLAGS(EnumType)` macro to automatically define all their bitwise operators.

Example:
```
enum class EFlags
{
  None = 0x00,
  Flag1 = 0x01,
  Flag2 = 0x02,
  Flag3 = 0x04
};
 
ENUM_CLASS_FLAGS(EFlags)
```

This has one exception, which is the usage of flags in an `if` and truth context. Due to that Flag Enums classes should always include a value called `None` set to 0, to be used in comparisons.

Example:
```
// Old
if (Flags & EFlags::Flag1)

// New
if ((Flags & EFlags::Flag1) != EFlags::None)
```

<a name="4.8"></a>
<a name="cpp-interfaces"></a>
### 4.8 Interfaces

Interface classes should always be abstract.

When creating an abstract interface class, we need to create two classes, `UInterface` (with `MinimalAPI` specifier prefixed with `U`) and `IInterface` (with the Game's API macro prefixed with `I`).

Example:
```
UINTERFACE(MinimalAPI)
class UPRSOperatableInterface : public UInterface
{
	GENERATED_BODY()
};

class PERSPECTIVE_API IPRSOperatableInterface
{
	GENERATED_BODY()

public:
  ...
};
```

> **_NOTE_:** Both should reside in the same interface file, in this example in `PRSOperatableInterface.h`.

<a name="4.8.1"></a>
<a name="cpp-interfaces-naming"></a>
#### 4.8.1 Naming

The `UInterface` class should be prefixed with `U`.

The `IInterface` class should be prefixed with `I`.

Both should be suffixed with `Interface`.

Example:
```
UINTERFACE(MinimalAPI)
class UPRSOperatableInterface : public UInterface
{
	GENERATED_BODY()
};

class PERSPECTIVE_API IPRSOperatableInterface
{
	GENERATED_BODY()

public:
  ...
};
```

<a name="4.8.2"></a>
<a name="cpp-interfaces-non-pure-functions"></a>
#### 4.8.2 Non-pure functions in Interfaces

Interfaces are allowed to contain non-virtual or static functions, as long as they are implemented inline (and leverage `FORCEINLINE`).

<a name="4.9"></a>
<a name="cpp-delegates-and-events"></a>
### 4.9 Delegates and Events

<a name="4.9.1"></a>
<a name="cpp-events-naming"></a>
#### 4.9.1 Naming

In addition to the following rules, all names should also follow the rules here: [C++ Classes Function Names](#cpp-classes-funcs-naming).

<a name="4.9.1.1"></a>
<a name="cpp-events-naming-eventhandlers"></a>
##### 4.9.1.1 Delegate Declarations, Events, Event Handlers and Event Dispatchers Should Start With `On`

Delegate Declarations as well as exposed Events should start with `FOn`.

For example:

* `DECLARE_DYNAMIC_MULTICAST_DELEGATE(FOnAwaitingDuel);`
* `DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnPhaseChanged, EPhase, Phase);`

Exposed Events (as in events that can be registered by other classes) should start with `On`.

For example:

* `FOnAwaitingDuel OnAwaitingDuel;`
* `FOnPhaseChanged OnPhaseChanged;`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#bp-funcs-naming-verbs). The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

<a name="4.9.1.2"></a>
<a name="cpp-events-naming-internal-delegates"></a>
##### 4.9.1.2 Internal Delegates Should Not Start With `On` and Should End With `Delegate`

Delegates declared inside a class to serve as a wrapper to an Event Handler should not start with `On`. This is because the event handling function they wrap already starts with `On` and most likely has an identical name so this will cause a conflict.

Hence we suffix with a `Delegate` to clarify that this is a wrapping delegate.

For example:

* `FOnTimelineFloat AttackPostUpdateDelegate;`
* `FOnTimelineEvent AttackEventDelegate;`

<a name="4.9.2"></a>
<a name="cpp-events-binding"></a>
#### 4.9.2 Event Binding

Binding to other data member's events should be either in the `PostInitializeComponents()` or the `BeginPlay()` function.

> **_NOTE_:** While `BeginPlay()` is in general the most common place to bind to events, the correct place on paper to bind to events is `PostInitializeComponents()`, as it is the earliest point where the actor is in a fully-formed state, hence making sense to include code that initializes the actor at the start of the game.

You should never bind to other data member events in the Constructor, this could lead to undesired side effects can occur due to the CDO (Class Default Object), such as the function continue being binded even if the code is removed.

> **_NOTE_:** As a rule, the Constructor should not contain any gameplay-related code, it should be used to for establishing universal details for the class, not for modifying any particular instance of that class.

<a name="4.10"></a>
<a name="cpp-typedefs"></a>
#### 4.10 Typedefs

Typedefs should be prefixed by what is appropriate for that type, such as `F` for structs, or `U` for `UObject`.

Example: `typedef TArray<FMytype> FArrayOfMyTypes;`

<a name="4.11"></a>
<a name="cpp-macros"></a>
#### 4.11 Macros

Macro names (as opposed to function names) should be fully capitalized with words separated by underscores, and prefixed with the projects name.

Example for UE macros: `#define UE_AUDIT_SPRITER_IMPORT`

Example for project with an abbreviation of `QD`: `#define QD_SOME_MACRO`

<a name="4.12"></a>
<a name="cpp-comments"></a>
#### 4.12 Comments

This section discusses use of comments in the code.

<a name="4.12.1"></a>
<a name="cpp-comments-thirdparty"></a>
#### 4.12.1 Third Party Code

Whenever you modify the engine code, make sure to add a comment with a //@UE5 tag, and an explanation of why the change was made.

Example:
```
// @third party code - BEGIN PhysX
#include <physx.h>
// @third party code - END PhysX
// @third party code - BEGIN MSDN SetThreadName
// [http://msdn.microsoft.com/en-us/library/xcb2z8hs.aspx]
// Used to set the thread name in the debugger
...
//@third party code - END MSDN SetThreadName
```

This is done to make the merging process on newer UE versions easier.

<a name="4.13"></a>
<a name="cpp-namespaces"></a>
#### 4.13 Namespaces

This section discuss guildlines to follow when using namespaces to organize code.

* Namespaces are not supported by the `UHT (UnrealHeaderTool)` so they shouldn't be used when defining `UCLASS`es, `USTRUCT`s and so on.
* New APIs (which aren't `UCLASS`es, `USTRUCT`s and so on) should be placed in a common namespace (the code name of the project), and ideally a nested namespace such as `Audio` or `Material` resulting in `QD::Audio::`.
* Do not use `using` declarations in the global scope, even in a `.cpp` file. Use namespaces only in other namespaces or function bodies.
* Forward-declared types need to be declared within their respoective namespace.
* Macros can't be used in namespaces, instead just follow the [C++ Macros](#cpp-macros) nameing rule.

**[⬆ Back to Top](#table-of-contents)**

<a name="5"></a>
<a name="bp"></a>
## 5. Blueprints

This section will focus on Blueprint classes and their internals. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

<a name="5.1"></a>
<a name="bp-compiling"></a>
### 5.1 Compiling

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken blueprints to source control. If you must store them on source control, shelve them instead (or use the [Developers Folder](#3.3)).

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures, and frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

<a name="5.2"></a>
<a name="bp-vars"></a>
### 5.2 Variables

The words `variable` and `property` may be used interchangeably and refer to variables scoped under the specific Blueprint struct/class.

<a name="5.2.1"></a>
<a name="bp-vars-naming"></a>
#### 5.2.1 Naming

Blueprint variable namings should follow all rules stated in [C++ Class Data Members Naming](#cpp-classes-data-members-naming), with the addition of the following rules below.

<a name="5.2.2"></a>
<a name="bp-vars-editable"></a>
#### 5.2.2 Editable Variables

All variables that are safe to change the value of in order to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should _not_ be marked as editable, unless for engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

<a name="5.2.2.1"></a>
<a name="bp-vars-editable-tooltips"></a>
##### 5.2.2.1 Tooltips

All `Editable` variables, including those marked editable just so they can be marked as `Expose On Spawn`, should have a description in their `Tooltip` fields that explains how changing this value affects the behavior of the blueprint.

<a name="5.2.3"></a>
<a name="bp-vars-access"></a>
#### 5.2.3 Variable Access Level

In C++, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

Blueprints do not have a defined concept of protected access currently.

Treat `Editable` variables as public variables. Treat non-editable variables as protected variables.

<a name="5.2.4"></a>
<a name="bp-vars-advanced"></a>
#### 5.2.4 Advanced Display

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

<a name="5.2.5"></a>
<a name="bp-vars-transient"></a>
#### 5.2.5 Transient Variables

Transient variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is useful for references to other objects and actors who's value isn't known until run-time. This prevents the editor from ever saving a reference to it, and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

<a name="5.2.6"></a>
<a name="bp-vars-config"></a>
#### 5.2.6 Config Variables

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

<a name="5.3"></a>
<a name="bp-funcs"></a>
### 5.3 Functions, Delegates, Events, Event Handlers, and Event Dispatchers

This section describes how you should author functions, delegates, events, event handlers, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

<a name="5.3.1"></a>
<a name="bp-funcs-naming"></a>
### 5.3.1 Function Naming

Function naming should follow all rules stated in [C++ Classes Functions Naming](#cpp-classes-funcs-naming), with the addition of the following rules below.

<a name="5.3.1.1"></a>
<a name="bp-funcs-naming-eventhandlers"></a>
#### 5.3.1.1 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [C++ Events, Event Handlers and Event Dispatchers rule](#cpp-events-naming-eventhandlers).

<a name="5.3.2"></a>
<a name="bp-funcs-return"></a>
#### 5.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

<a name="5.3.3"></a>
<a name="bp-funcs-node-limit"></a>
#### 5.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="5.3.4"></a>
<a name="bp-funcs-description"></a>
#### 5.3.4 All Public Functions Should Have A Description

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specifier of Public should have its description filled out.

<a name="5.3.5"></a>
<a name="bp-funcs-plugin-category"></a>
#### 5.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

<a name="5.4"></a>
<a name="bp-graphs"></a>
### 5.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

<a name="5.4.1"></a>
<a name="bp-graphs-spaghetti"></a>
#### 5.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

<a name="5.4.2"></a>
<a name="bp-graphs-align-wires"></a>
#### 5.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

<a name="5.4.3"></a>
<a name="bp-graphs-exec-first-class"></a>
#### 5.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

<a name="5.4.4"></a>
<a name="bp-graphs-parameters-under-node"></a>
#### 5.4.4 Place All Parameters Under The Node They Go To

When providing parameters to a certain Node (wheter it's a Pure Function or an Exec line) prefer stacking the parameters vertically under the Node instead of spreading them horizontally elsewhere.

I find this method easier to follow, it provides a clear structure, it helps easily find the used parameters, and it removes the need to follow lines backward in the flow, allowing to stay concentrated at the current flow.

<a name="5.4.5"></a>
<a name="bp-graphs-no-property-reuse"></a>
#### 5.4.5 Do Not Favor Property Reuse, Favor Additional Getters

Following on 5.4.4, for similar reasons favor calling a getter again, and pulling a function parameter explicitly instead of dragging their lines from previous nodes.

This (as mentioned) removes the need to follow lines backward in the flow and searchfing for the relevant parameters.

<a name="5.4.6"></a>
<a name="bp-graphs-block-comments"></a>
#### 5.4.6 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and description should suffice.

<a name="5.4.7"></a>
<a name="bp-graphs-cast-error-handling"></a>
#### 5.4.7 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

<a name="5.4.8"></a>
<a name="bp-graphs-dangling-nodes"></a>
#### 5.4.8 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.

**[⬆ Back to Top](#table-of-contents)**

<a name="6"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 6. Static Meshes

This section will focus on Static Mesh assets and their internals.

<a name="6.1"></a>
<a name="s-uvs"></a>
### 6.1 Static Mesh UVs

<a name="6.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 6.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="6.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 6.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="6.2"></a>
<a name="s-lods"></a>
### 6.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="6.3"></a>
<a name="s-modular-snapping"></a>
### 6.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for Fab, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="6.4"></a>
<a name="s-collision"></a>
### 6.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="6.5"></a>
<a name="s-scaled"></a>
### 6.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**


<a name="7"></a>
<a name="Niagara"></a>
<a name="ng"></a>
## 7. Niagara

This section will focus on Niagara assets and their internals.

<a name="7.1"></a>
<a name="ng-rules"></a>
### 7.1 No Spaces, Ever

As mentioned in [1.1 Forbidden Identifiers](#1.1), spaces and all white space characters are forbidden in identifiers. This is especially true for Niagara systems as it makes working with things significantly harder if not impossible when working with HLSL or other means of scripting within Niagara and trying to reference an identifier.

**[⬆ Back to Top](#table-of-contents)**


<a name="8"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 8. Levels / Maps

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

<a name="8.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 8.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

<a name="8.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 8.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="8.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 8.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

<a name="8.4"></a>
<a name="levels-mp-rules"></a>
### 8.4 Fab Specific Rules

If a project is to be sold on Fab, it must follow these rules.

<a name="8.4.1"></a>
<a name="levels-mp-rules-overview"></a>
#### 8.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

For example, `LVL_InteractionComponent_Overview`.

<a name="8.4.2"></a>
<a name="levels-mp-rules-demo"></a>
#### 8.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `LVL_InteractionComponent_Overview_Demo`, `LVL_ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**


<a name="9"></a>
<a name="textures"></a>
## 9. Textures

This section will focus on Texture assets and their internals.

<a name="9.1"></a>
<a name="textures-dimensions"></a>
### 9.1 Dimensions Are Powers of 2

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="9.2"></a>
<a name="textures-density"></a>
### 9.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="9.3"></a>
<a name="textures-max-size"></a>
### 9.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="9.4"></a>
<a name="textures-group"></a>
### 9.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**

## License & Credits

Copyright (c) 2016 Gamemakin LLC

See [LICENSE](/LICENSE)

Original Author:
* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)

Additional Contributors:
* [akenatsu](https://github.com/akenatsu)
* [billymcguffin](https://github.com/billymcguffin)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [dunenkoff](https://github.com/Allar/ue5-style-guide/issues/58)

**[⬆ Back to Top](#table-of-contents)**
