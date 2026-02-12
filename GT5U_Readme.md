# GT5-Unofficial Interfaces Documentation
This document contains all interface declarations found in the GT5-Unofficial repository.
**Repository:** https://github.com/GTNewHorizons/GT5-Unofficial
**Total Interfaces Found:** 228
**Total Packages:** 64

---

## Table of Contents
- [bartworks.API](#bartworks-API) (5 interfaces)
- [bartworks.system.material.werkstoff_loaders](#bartworks-system-material-werkstoff_loaders) (1 interfaces)
- [galacticgreg.api](#galacticgreg-api) (1 interfaces)
- [goodgenerator.blocks.regularBlock](#goodgenerator-blocks-regularBlock) (1 interfaces)
- [gregtech.api.casing](#gregtech-api-casing) (3 interfaces)
- [gregtech.api.covers](#gregtech-api-covers) (2 interfaces)
- [gregtech.api.enums](#gregtech-api-enums) (1 interfaces)
- [gregtech.api.factory](#gregtech-api-factory) (3 interfaces)
- [gregtech.api.factory.test](#gregtech-api-factory-test) (1 interfaces)
- [gregtech.api.gui.modularui](#gregtech-api-gui-modularui) (2 interfaces)
- [gregtech.api.gui.widgets](#gregtech-api-gui-widgets) (1 interfaces)
- [gregtech.api.hazards](#gregtech-api-hazards) (1 interfaces)
- [gregtech.api.interfaces](#gregtech-api-interfaces) (42 interfaces)
- [gregtech.api.interfaces.fluid](#gregtech-api-interfaces-fluid) (4 interfaces)
- [gregtech.api.interfaces.internal](#gregtech-api-interfaces-internal) (3 interfaces)
- [gregtech.api.interfaces.item](#gregtech-api-interfaces-item) (1 interfaces)
- [gregtech.api.interfaces.metatileentity](#gregtech-api-interfaces-metatileentity) (8 interfaces)
- [gregtech.api.interfaces.modularui](#gregtech-api-interfaces-modularui) (8 interfaces)
- [gregtech.api.interfaces.tileentity](#gregtech-api-interfaces-tileentity) (28 interfaces)
- [gregtech.api.net](#gregtech-api-net) (1 interfaces)
- [gregtech.api.recipe](#gregtech-api-recipe) (3 interfaces)
- [gregtech.api.recipe.check](#gregtech-api-recipe-check) (1 interfaces)
- [gregtech.api.recipe.metadata](#gregtech-api-recipe-metadata) (1 interfaces)
- [gregtech.api.render](#gregtech-api-render) (3 interfaces)
- [gregtech.api.structure](#gregtech-api-structure) (4 interfaces)
- [gregtech.api.task](#gregtech-api-task) (2 interfaces)
- [gregtech.api.util](#gregtech-api-util) (14 interfaces)
- [gregtech.api.util.shutdown](#gregtech-api-util-shutdown) (1 interfaces)
- [gregtech.client](#gregtech-client) (1 interfaces)
- [gregtech.client.volumetric](#gregtech-client-volumetric) (1 interfaces)
- [gregtech.common.covers](#gregtech-common-covers) (1 interfaces)
- [gregtech.common.data](#gregtech-common-data) (5 interfaces)
- [gregtech.common.gui.modularui](#gregtech-common-gui-modularui) (1 interfaces)
- [gregtech.common.gui.modularui.multiblock.godforge.data](#gregtech-common-gui-modularui-multiblock-godforge-data) (1 interfaces)
- [gregtech.common.misc](#gregtech-common-misc) (1 interfaces)
- [gregtech.common.misc.spaceprojects.interfaces](#gregtech-common-misc-spaceprojects-interfaces) (4 interfaces)
- [gregtech.common.modularui2.factory](#gregtech-common-modularui2-factory) (1 interfaces)
- [gregtech.common.ores](#gregtech-common-ores) (1 interfaces)
- [gregtech.common.render](#gregtech-common-render) (3 interfaces)
- [gregtech.common.tileentities.generators](#gregtech-common-tileentities-generators) (1 interfaces)
- [gregtech.common.tileentities.machines](#gregtech-common-tileentities-machines) (6 interfaces)
- [gregtech.common.tileentities.machines.outputme.base](#gregtech-common-tileentities-machines-outputme-base) (1 interfaces)
- [gregtech.common.tileentities.machines.outputme.util](#gregtech-common-tileentities-machines-outputme-util) (1 interfaces)
- [gregtech.common.worldgen](#gregtech-common-worldgen) (1 interfaces)
- [gregtech.crossmod.ae2](#gregtech-crossmod-ae2) (1 interfaces)
- [gregtech.crossmod.visualprospecting](#gregtech-crossmod-visualprospecting) (1 interfaces)
- [gregtech.mixin.interfaces.accessors](#gregtech-mixin-interfaces-accessors) (15 interfaces)
- [gregtech.nei.formatter](#gregtech-nei-formatter) (1 interfaces)
- [gtPlusPlus.api.interfaces](#gtPlusPlus-api-interfaces) (3 interfaces)
- [gtPlusPlus.core.interfaces](#gtPlusPlus-core-interfaces) (3 interfaces)
- [gtnhintergalactic.tile.multi.elevator](#gtnhintergalactic-tile-multi-elevator) (1 interfaces)
- [gtnhlanth.common.beamline](#gtnhlanth-common-beamline) (1 interfaces)
- [gtnhlanth.common.item](#gtnhlanth-common-item) (1 interfaces)
- [kubatech.api](#kubatech-api) (8 interfaces)
- [kubatech.api.eig](#kubatech-api-eig) (1 interfaces)
- [kubatech.api.implementations](#kubatech-api-implementations) (1 interfaces)
- [kubatech.api.tileentity](#kubatech-api-tileentity) (1 interfaces)
- [kubatech.loaders.block.kubablock](#kubatech-loaders-block-kubablock) (3 interfaces)
- [kubatech.loaders.item.kubaitem](#kubatech-loaders-item-kubaitem) (1 interfaces)
- [speiger.src.crops.api](#speiger-src-crops-api) (1 interfaces)
- [tectech.mechanics.pipe](#tectech-mechanics-pipe) (3 interfaces)
- [tectech.mechanics.tesla](#tectech-mechanics-tesla) (2 interfaces)
- [tectech.thing.metaTileEntity.multi.base](#tectech-thing-metaTileEntity-multi-base) (3 interfaces)
- [tectech.thing.metaTileEntity.multi.base.parameter](#tectech-thing-metaTileEntity-multi-base-parameter) (1 interfaces)

---

## bartworks.API

### INoiseGen
- **Visibility:** public
- **File:** `bartworks/API/INoiseGen.java`
- **Line:** 16

```java
public interface INoiseGen
```

### IRadMaterial
- **Visibility:** public
- **File:** `bartworks/API/IRadMaterial.java`
- **Line:** 18

```java
public interface IRadMaterial
```

### ITileAddsInformation
- **Visibility:** public
- **File:** `bartworks/API/ITileAddsInformation.java`
- **Line:** 16

```java
public interface ITileAddsInformation
```

### ITileDropsContent
- **Visibility:** public
- **File:** `bartworks/API/ITileDropsContent.java`
- **Line:** 18
- **Extends:** `ISidedInventory`

```java
public interface ITileDropsContent extends ISidedInventory
```

### ITileHasDifferentTextureSides
- **Visibility:** public
- **File:** `bartworks/API/ITileHasDifferentTextureSides.java`
- **Line:** 25

```java
public interface ITileHasDifferentTextureSides
```

## bartworks.system.material.werkstoff_loaders

### IWerkstoffRunnable
- **Visibility:** public
- **File:** `bartworks/system/material/werkstoff_loaders/IWerkstoffRunnable.java`
- **Line:** 18

```java
public interface IWerkstoffRunnable
```

## galacticgreg.api

### ISpaceObjectGenerator
- **Visibility:** public
- **File:** `galacticgreg/api/ISpaceObjectGenerator.java`
- **Line:** 9

```java
public interface ISpaceObjectGenerator
```

## goodgenerator.blocks.regularBlock

### ITextureBlock
- **Visibility:** public
- **File:** `goodgenerator/blocks/regularBlock/ITextureBlock.java`
- **Line:** 9

```java
public interface ITextureBlock
```

## gregtech.api.casing

### CasingElementContext
- **Visibility:** package-private
- **File:** `gregtech/api/casing/ICasing.java`
- **Line:** 74

```java
interface CasingElementContext<T>
```

### ICasing
- **Visibility:** public
- **File:** `gregtech/api/casing/ICasing.java`
- **Line:** 19
- **Extends:** `ImmutableBlockMeta`

```java
public interface ICasing extends ImmutableBlockMeta
```

### ICasingGroup
- **Visibility:** public
- **File:** `gregtech/api/casing/ICasingGroup.java`
- **Line:** 9

```java
public interface ICasingGroup
```

## gregtech.api.covers

### CoverFactory
- **Visibility:** public
- **File:** `gregtech/api/covers/CoverFactory.java`
- **Line:** 6

```java
public interface CoverFactory
```

### CoverPlacementPredicate
- **Visibility:** public
- **File:** `gregtech/api/covers/CoverPlacementPredicate.java`
- **Line:** 9

```java
public interface CoverPlacementPredicate
```

## gregtech.api.enums

### Localizer
- **Visibility:** package-private
- **File:** `gregtech/api/enums/ChatMessage.java`
- **Line:** 43

```java
interface Localizer
```

## gregtech.api.factory

### IFactoryElement
- **Visibility:** public
- **File:** `gregtech/api/factory/IFactoryElement.java`
- **Line:** 14
- **Extends:** `IFactoryElement<TSelf, TNetwork, TGrid>, TNetwork extends IFactoryNetwork<TNetwork, TSelf, TGrid>, TGrid extends IFactoryGrid<TGrid, TSelf, TNetwork>>`

```java
public interface IFactoryElement<TSelf extends IFactoryElement<TSelf, TNetwork, TGrid>, TNetwork extends IFactoryNetwork<TNetwork, TSelf, TGrid>, TGrid extends IFactoryGrid<TGrid, TSelf, TNetwork>>
```

### IFactoryGrid
- **Visibility:** public
- **File:** `gregtech/api/factory/IFactoryGrid.java`
- **Line:** 9
- **Extends:** `IFactoryGrid<TSelf, TElement, TNetwork>, TElement extends IFactoryElement<TElement, TNetwork, TSelf>, TNetwork extends IFactoryNetwork<TNetwork, TElement, TSelf>>`

```java
public interface IFactoryGrid<TSelf extends IFactoryGrid<TSelf, TElement, TNetwork>, TElement extends IFactoryElement<TElement, TNetwork, TSelf>, TNetwork extends IFactoryNetwork<TNetwork, TElement, TSelf>>
```

### IFactoryNetwork
- **Visibility:** public
- **File:** `gregtech/api/factory/IFactoryNetwork.java`
- **Line:** 11
- **Extends:** `IFactoryNetwork<TSelf, TElement, TGrid>, TElement extends IFactoryElement<TElement, TSelf, TGrid>, TGrid extends IFactoryGrid<TGrid, TElement, TSelf>>`

```java
public interface IFactoryNetwork<TSelf extends IFactoryNetwork<TSelf, TElement, TGrid>, TElement extends IFactoryElement<TElement, TSelf, TGrid>, TGrid extends IFactoryGrid<TGrid, TElement, TSelf>>
```

## gregtech.api.factory.test

### TestFactoryElement
- **Visibility:** public
- **File:** `gregtech/api/factory/test/TestFactoryElement.java`
- **Line:** 7
- **Extends:** `IFactoryElement<TestFactoryElement, TestFactoryNetwork, TestFactoryGrid>`

```java
public interface TestFactoryElement extends IFactoryElement<TestFactoryElement, TestFactoryNetwork, TestFactoryGrid>
```

## gregtech.api.gui.modularui

### ContainerConstructor
- **Visibility:** public
- **File:** `gregtech/api/gui/modularui/GTUIInfos.java`
- **Line:** 151

```java
public interface ContainerConstructor
```

### ICoverDataFollowerWidget
- **Visibility:** public
- **File:** `gregtech/api/gui/modularui/ICoverDataFollowerWidget.java`
- **Line:** 24

```java
public interface ICoverDataFollowerWidget<T, U>
```

## gregtech.api.gui.widgets

### CheckboxClicked
- **Visibility:** public
- **File:** `gregtech/api/gui/widgets/CheckboxWidget.java`
- **Line:** 18

```java
public interface CheckboxClicked
```

## gregtech.api.hazards

### IHazardProtector
- **Visibility:** public
- **File:** `gregtech/api/hazards/IHazardProtector.java`
- **Line:** 5

```java
public interface IHazardProtector
```

## gregtech.api.interfaces

### IBlockContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IBlockContainer.java`
- **Line:** 5

```java
public interface IBlockContainer
```

### IBlockOnWalkOver
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IBlockOnWalkOver.java`
- **Line:** 6

```java
public interface IBlockOnWalkOver
```

### IBlockWithActiveOffset
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IBlockWithActiveOffset.java`
- **Line:** 7

```java
public interface IBlockWithActiveOffset
```

### IBlockWithClientMeta
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IBlockWithClientMeta.java`
- **Line:** 11

```java
public interface IBlockWithClientMeta
```

### IBlockWithTextures
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IBlockWithTextures.java`
- **Line:** 7

```java
public interface IBlockWithTextures
```

### IChunkLoader
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IChunkLoader.java`
- **Line:** 6

```java
public interface IChunkLoader
```

### ICleanroom
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ICleanroom.java`
- **Line:** 6

```java
public interface ICleanroom
```

### ICleanroomReceiver
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ICleanroomReceiver.java`
- **Line:** 15

```java
public interface ICleanroomReceiver
```

### IColorModulationContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IColorModulationContainer.java`
- **Line:** 3

```java
public interface IColorModulationContainer
```

### ICondition
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ICondition.java`
- **Line:** 3

```java
public interface ICondition<O>
```

### IConfigurationCircuitSupport
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IConfigurationCircuitSupport.java`
- **Line:** 6

```java
public interface IConfigurationCircuitSupport
```

### IDamagableItem
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IDamagableItem.java`
- **Line:** 5

```java
public interface IDamagableItem
```

### IDataCopyable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IDataCopyable.java`
- **Line:** 6

```java
public interface IDataCopyable
```

### IDebugableBlock
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IDebugableBlock.java`
- **Line:** 10

```java
public interface IDebugableBlock
```

### IDescribable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IDescribable.java`
- **Line:** 6

```java
public interface IDescribable
```

### IFoodStat
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IFoodStat.java`
- **Line:** 9

```java
public interface IFoodStat
```

### IGT_ItemWithMaterialRenderer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IGT_ItemWithMaterialRenderer.java`
- **Line:** 13

```java
public interface IGT_ItemWithMaterialRenderer
```

### IHasIndexedTexture
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IHasIndexedTexture.java`
- **Line:** 6

```java
public interface IHasIndexedTexture
```

### IHatchElement
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IHatchElement.java`
- **Line:** 20

```java
public interface IHatchElement<T>
```

### IHeatingCoil
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IHeatingCoil.java`
- **Line:** 7

```java
public interface IHeatingCoil
```

### IIconContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IIconContainer.java`
- **Line:** 11

```java
public interface IIconContainer
```

### IItemBehaviour
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IItemBehaviour.java`
- **Line:** 21
- **Extends:** `Item>`

```java
public interface IItemBehaviour<E extends Item>
```

### IItemContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IItemContainer.java`
- **Line:** 8

```java
public interface IItemContainer
```

### IMEConnectable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IMEConnectable.java`
- **Line:** 6

```java
public interface IMEConnectable
```

### IMaterialHandler
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IMaterialHandler.java`
- **Line:** 3

```java
public interface IMaterialHandler
```

### INEIPreviewModifier
- **Visibility:** public
- **File:** `gregtech/api/interfaces/INEIPreviewModifier.java`
- **Line:** 8

```java
public interface INEIPreviewModifier
```

### INetworkUpdatableItem
- **Visibility:** public
- **File:** `gregtech/api/interfaces/INetworkUpdatableItem.java`
- **Line:** 14

```java
public interface INetworkUpdatableItem
```

### IOreMaterial
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IOreMaterial.java`
- **Line:** 21
- **Extends:** `ISubTagContainer`

```java
public interface IOreMaterial extends ISubTagContainer
```

### IOreRecipeRegistrator
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IOreRecipeRegistrator.java`
- **Line:** 8

```java
public interface IOreRecipeRegistrator
```

### IOutputBus
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IOutputBus.java`
- **Line:** 8

```java
public interface IOutputBus
```

### IOutputBusTransaction
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IOutputBusTransaction.java`
- **Line:** 14

```java
public interface IOutputBusTransaction
```

### IProjectileItem
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IProjectileItem.java`
- **Line:** 10

```java
public interface IProjectileItem
```

### IRecipeMap
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IRecipeMap.java`
- **Line:** 17

```java
public interface IRecipeMap
```

### IRedstoneCircuitBlock
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IRedstoneCircuitBlock.java`
- **Line:** 13

```java
public interface IRedstoneCircuitBlock
```

### ISecondaryDescribable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ISecondaryDescribable.java`
- **Line:** 6
- **Extends:** `IDescribable`

```java
public interface ISecondaryDescribable extends IDescribable
```

### IStoneCategory
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IStoneCategory.java`
- **Line:** 3

```java
public interface IStoneCategory
```

### IStoneType
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IStoneType.java`
- **Line:** 14

```java
public interface IStoneType
```

### ISubTagContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ISubTagContainer.java`
- **Line:** 5

```java
public interface ISubTagContainer
```

### ITemporaryTE
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ITemporaryTE.java`
- **Line:** 3

```java
public interface ITemporaryTE
```

### ITexture
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ITexture.java`
- **Line:** 8

```java
public interface ITexture
```

### ITextureBuilder
- **Visibility:** public
- **File:** `gregtech/api/interfaces/ITextureBuilder.java`
- **Line:** 18

```java
public interface ITextureBuilder
```

### IToolStats
- **Visibility:** public
- **File:** `gregtech/api/interfaces/IToolStats.java`
- **Line:** 28

```java
public interface IToolStats
```

## gregtech.api.interfaces.fluid

### IFluidStore
- **Visibility:** public
- **File:** `gregtech/api/interfaces/fluid/IFluidStore.java`
- **Line:** 11
- **Extends:** `IFluidTank`

```java
public interface IFluidStore extends IFluidTank
```

### IGTFluid
- **Visibility:** public
- **File:** `gregtech/api/interfaces/fluid/IGTFluid.java`
- **Line:** 6

```java
public interface IGTFluid
```

### IGTFluidBuilder
- **Visibility:** public
- **File:** `gregtech/api/interfaces/fluid/IGTFluidBuilder.java`
- **Line:** 13

```java
public interface IGTFluidBuilder
```

### IGTRegisteredFluid
- **Visibility:** public
- **File:** `gregtech/api/interfaces/fluid/IGTRegisteredFluid.java`
- **Line:** 10

```java
public interface IGTRegisteredFluid
```

## gregtech.api.interfaces.internal

### IGTCraftingRecipe
- **Visibility:** public
- **File:** `gregtech/api/interfaces/internal/IGTCraftingRecipe.java`
- **Line:** 5
- **Extends:** `IRecipe`

```java
public interface IGTCraftingRecipe extends IRecipe
```

### IGTRecipeAdder
- **Visibility:** public
- **File:** `gregtech/api/interfaces/internal/IGTRecipeAdder.java`
- **Line:** 5

```java
public interface IGTRecipeAdder
```

### IThaumcraftCompat
- **Visibility:** public
- **File:** `gregtech/api/interfaces/internal/IThaumcraftCompat.java`
- **Line:** 12

```java
public interface IThaumcraftCompat
```

## gregtech.api.interfaces.item

### ItemStackSizeCalculator
- **Visibility:** public
- **File:** `gregtech/api/interfaces/item/ItemStackSizeCalculator.java`
- **Line:** 5

```java
public interface ItemStackSizeCalculator
```

## gregtech.api.interfaces.metatileentity

### IConnectable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IConnectable.java`
- **Line:** 8

```java
public interface IConnectable
```

### IFluidLockable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IFluidLockable.java`
- **Line:** 9

```java
public interface IFluidLockable
```

### IItemLockable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IItemLockable.java`
- **Line:** 10

```java
public interface IItemLockable
```

### IMetaTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IMetaTileEntity.java`
- **Line:** 45
- **Extends:** `ISidedInventory, IFluidTank, IFluidHandler, IMachineBlockUpdateable, IGregtechWailaProvider, IGetGUITextureSet, IGregTechDeviceInformation, CapabilityProvider, IGuiHolder<PosGuiData>`

```java
public interface IMetaTileEntity extends ISidedInventory, IFluidTank, IFluidHandler, IMachineBlockUpdateable, IGregtechWailaProvider, IGetGUITextureSet, IGregTechDeviceInformation, CapabilityProvider, IGuiHolder<PosGuiData>
```

### IMetaTileEntityCable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IMetaTileEntityCable.java`
- **Line:** 8
- **Extends:** `IMetaTileEntityPipe`

```java
public interface IMetaTileEntityCable extends IMetaTileEntityPipe
```

### IMetaTileEntityItemPipe
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IMetaTileEntityItemPipe.java`
- **Line:** 10
- **Extends:** `IMetaTileEntityPipe`

```java
public interface IMetaTileEntityItemPipe extends IMetaTileEntityPipe
```

### IMetaTileEntityPipe
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IMetaTileEntityPipe.java`
- **Line:** 8
- **Extends:** `IMetaTileEntity`

```java
public interface IMetaTileEntityPipe extends IMetaTileEntity
```

### IMetricsExporter
- **Visibility:** public
- **File:** `gregtech/api/interfaces/metatileentity/IMetricsExporter.java`
- **Line:** 14

```java
public interface IMetricsExporter
```

## gregtech.api.interfaces.modularui

### IAddGregtechLogo
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IAddGregtechLogo.java`
- **Line:** 5

```java
public interface IAddGregtechLogo
```

### IAddInventorySlots
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IAddInventorySlots.java`
- **Line:** 6

```java
public interface IAddInventorySlots
```

### IAddUIWidgets
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IAddUIWidgets.java`
- **Line:** 6

```java
public interface IAddUIWidgets
```

### IBindPlayerInventoryUI
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IBindPlayerInventoryUI.java`
- **Line:** 6

```java
public interface IBindPlayerInventoryUI
```

### IControllerWithOptionalFeatures
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IControllerWithOptionalFeatures.java`
- **Line:** 46
- **Extends:** `IVoidable, IRecipeLockable`

```java
public interface IControllerWithOptionalFeatures extends IVoidable, IRecipeLockable
```

### IGetGUITextureSet
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IGetGUITextureSet.java`
- **Line:** 5

```java
public interface IGetGUITextureSet
```

### IGetTitleColor
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/IGetTitleColor.java`
- **Line:** 5

```java
public interface IGetTitleColor
```

### KeyProvider
- **Visibility:** public
- **File:** `gregtech/api/interfaces/modularui/KeyProvider.java`
- **Line:** 8

```java
public interface KeyProvider
```

## gregtech.api.interfaces.tileentity

### IAllSidedTexturedTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IAllSidedTexturedTileEntity.java`
- **Line:** 11
- **Extends:** `ITexturedTileEntity`

```java
public interface IAllSidedTexturedTileEntity extends ITexturedTileEntity
```

### IBasicEnergyContainer
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IBasicEnergyContainer.java`
- **Line:** 8
- **Extends:** `IEnergyConnected, IHasWorldObjectAndCoords`

```java
public interface IBasicEnergyContainer extends IEnergyConnected, IHasWorldObjectAndCoords
```

### IColoredTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IColoredTileEntity.java`
- **Line:** 5

```java
public interface IColoredTileEntity
```

### ICoverable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/ICoverable.java`
- **Line:** 13
- **Extends:** `IRedstoneTileEntity, IHasInventory, IBasicEnergyContainer`

```java
public interface ICoverable extends IRedstoneTileEntity, IHasInventory, IBasicEnergyContainer
```

### IDebugableTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IDebugableTileEntity.java`
- **Line:** 7

```java
public interface IDebugableTileEntity
```

### IDigitalChest
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IDigitalChest.java`
- **Line:** 8
- **Extends:** `IHasWorldObjectAndCoords`

```java
public interface IDigitalChest extends IHasWorldObjectAndCoords
```

### IEnergyConnected
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IEnergyConnected.java`
- **Line:** 20
- **Extends:** `IColoredTileEntity`

```java
public interface IEnergyConnected extends IColoredTileEntity
```

### IGTEnet
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IGTEnet.java`
- **Line:** 3

```java
public interface IGTEnet
```

### IGregTechDeviceInformation
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IGregTechDeviceInformation.java`
- **Line:** 11

```java
public interface IGregTechDeviceInformation
```

### IGregTechTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IGregTechTileEntity.java`
- **Line:** 32
- **Extends:** `ITexturedTileEntity, ICoverable, IFluidHandler, ITurnable, IGregTechDeviceInformation, IUpgradableMachine, IDigitalChest, IDescribable, IMachineBlockUpdateable, IGregtechWailaProvider, IGetGUITextureSet, IAddInventorySlots, CapabilityProvider`

```java
public interface IGregTechTileEntity extends ITexturedTileEntity, ICoverable, IFluidHandler, ITurnable, IGregTechDeviceInformation, IUpgradableMachine, IDigitalChest, IDescribable, IMachineBlockUpdateable, IGregtechWailaProvider, IGetGUITextureSet, IAddInventorySlots, CapabilityProvider
```

### IGregtechWailaProvider
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IGregtechWailaProvider.java`
- **Line:** 14

```java
public interface IGregtechWailaProvider
```

### IHasInventory
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IHasInventory.java`
- **Line:** 6
- **Extends:** `ISidedInventory, IHasWorldObjectAndCoords`

```java
public interface IHasInventory extends ISidedInventory, IHasWorldObjectAndCoords
```

### IHasWorldObjectAndCoords
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IHasWorldObjectAndCoords.java`
- **Line:** 22

```java
public interface IHasWorldObjectAndCoords
```

### IIC2Enet
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IIC2Enet.java`
- **Line:** 6

```java
public interface IIC2Enet
```

### IMachineBlockUpdateable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IMachineBlockUpdateable.java`
- **Line:** 9

```java
public interface IMachineBlockUpdateable
```

### IMachineProgress
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IMachineProgress.java`
- **Line:** 11
- **Extends:** `IHasWorldObjectAndCoords`

```java
public interface IMachineProgress extends IHasWorldObjectAndCoords
```

### IOverclockDescriptionProvider
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IOverclockDescriptionProvider.java`
- **Line:** 11

```java
public interface IOverclockDescriptionProvider
```

### IPipeRenderedTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IPipeRenderedTileEntity.java`
- **Line:** 7
- **Extends:** `ICoverable, ITexturedTileEntity`

```java
public interface IPipeRenderedTileEntity extends ICoverable, ITexturedTileEntity
```

### IRecipeLockable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IRecipeLockable.java`
- **Line:** 8
- **Extends:** `RecipeMapWorkable`

```java
public interface IRecipeLockable extends RecipeMapWorkable
```

### IRedstoneEmitter
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IRedstoneEmitter.java`
- **Line:** 8
- **Extends:** `IHasWorldObjectAndCoords`

```java
public interface IRedstoneEmitter extends IHasWorldObjectAndCoords
```

### IRedstoneReceiver
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IRedstoneReceiver.java`
- **Line:** 8
- **Extends:** `IHasWorldObjectAndCoords`

```java
public interface IRedstoneReceiver extends IHasWorldObjectAndCoords
```

### IRedstoneTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IRedstoneTileEntity.java`
- **Line:** 6
- **Extends:** `IRedstoneEmitter, IRedstoneReceiver`

```java
public interface IRedstoneTileEntity extends IRedstoneEmitter, IRedstoneReceiver
```

### ITexturedTileEntity
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/ITexturedTileEntity.java`
- **Line:** 9

```java
public interface ITexturedTileEntity
```

### ITurnable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/ITurnable.java`
- **Line:** 8

```java
public interface ITurnable
```

### IUpgradableMachine
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IUpgradableMachine.java`
- **Line:** 8
- **Extends:** `IMachineProgress`

```java
public interface IUpgradableMachine extends IMachineProgress
```

### IVoidable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IVoidable.java`
- **Line:** 16

```java
public interface IVoidable
```

### IWirelessCharger
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/IWirelessCharger.java`
- **Line:** 6

```java
public interface IWirelessCharger
```

### RecipeMapWorkable
- **Visibility:** public
- **File:** `gregtech/api/interfaces/tileentity/RecipeMapWorkable.java`
- **Line:** 16

```java
public interface RecipeMapWorkable
```

## gregtech.api.net

### IGT_NetworkHandler
- **Visibility:** public
- **File:** `gregtech/api/net/IGT_NetworkHandler.java`
- **Line:** 8

```java
public interface IGT_NetworkHandler
```

## gregtech.api.recipe

### BackendCreator
- **Visibility:** public
- **File:** `gregtech/api/recipe/RecipeMapBackend.java`
- **Line:** 483
- **Extends:** `RecipeMapBackend>`

```java
public interface BackendCreator<B extends RecipeMapBackend>
```

### FrontendCreator
- **Visibility:** public
- **File:** `gregtech/api/recipe/RecipeMapFrontend.java`
- **Line:** 398

```java
public interface FrontendCreator
```

### SlotOverlayGetter
- **Visibility:** public
- **File:** `gregtech/api/recipe/BasicUIProperties.java`
- **Line:** 266

```java
public interface SlotOverlayGetter<T>
```

## gregtech.api.recipe.check

### CheckRecipeResult
- **Visibility:** public
- **File:** `gregtech/api/recipe/check/CheckRecipeResult.java`
- **Line:** 11
- **Extends:** `IMachineMessage<CheckRecipeResult>`

```java
public interface CheckRecipeResult extends IMachineMessage<CheckRecipeResult>
```

## gregtech.api.recipe.metadata

### IRecipeMetadataStorage
- **Visibility:** public
- **File:** `gregtech/api/recipe/metadata/IRecipeMetadataStorage.java`
- **Line:** 20

```java
public interface IRecipeMetadataStorage
```

## gregtech.api.render

### ISBRContext
- **Visibility:** public
- **File:** `gregtech/api/render/ISBRContext.java`
- **Line:** 15

```java
public interface ISBRContext
```

### ISBRInventoryContext
- **Visibility:** public
- **File:** `gregtech/api/render/ISBRInventoryContext.java`
- **Line:** 5
- **Extends:** `ISBRContext`

```java
public interface ISBRInventoryContext extends ISBRContext
```

### ISBRWorldContext
- **Visibility:** public
- **File:** `gregtech/api/render/ISBRWorldContext.java`
- **Line:** 10
- **Extends:** `ISBRContext`

```java
public interface ISBRWorldContext extends ISBRContext
```

## gregtech.api.structure

### IStructureChannels
- **Visibility:** public
- **File:** `gregtech/api/structure/IStructureChannels.java`
- **Line:** 9

```java
public interface IStructureChannels
```

### IStructureInstance
- **Visibility:** public
- **File:** `gregtech/api/structure/IStructureInstance.java`
- **Line:** 10

```java
public interface IStructureInstance<MTE>
```

### IStructureProvider
- **Visibility:** public
- **File:** `gregtech/api/structure/IStructureProvider.java`
- **Line:** 8

```java
public interface IStructureProvider<MTE>
```

### ISuperChestAcceptor
- **Visibility:** public
- **File:** `gregtech/api/structure/ISuperChestAcceptor.java`
- **Line:** 6

```java
public interface ISuperChestAcceptor
```

## gregtech.api.task

### CoopTask
- **Visibility:** public
- **File:** `gregtech/api/task/CoopTask.java`
- **Line:** 4

```java
public interface CoopTask<T>
```

### ICoopTaskContext
- **Visibility:** public
- **File:** `gregtech/api/task/ICoopTaskContext.java`
- **Line:** 3

```java
public interface ICoopTaskContext<T>
```

## gregtech.api.util

### ArgProcessor
- **Visibility:** public
- **File:** `gregtech/api/util/Localized.java`
- **Line:** 108

```java
public interface ArgProcessor
```

### Builtin
- **Visibility:** private
- **File:** `gregtech/api/util/HatchElementBuilder.java`
- **Line:** 48

```java
private interface Builtin
```

### IData
- **Visibility:** public
- **File:** `gregtech/api/util/GTChunkAssociatedData.java`
- **Line:** 283

```java
public interface IData
```

### IEntityPlayerWorldSpawnedEvent
- **Visibility:** private
- **File:** `gregtech/api/util/WorldSpawnedEventBuilder.java`
- **Line:** 67

```java
private interface IEntityPlayerWorldSpawnedEvent
```

### IEntityWorldSpawnedEvent
- **Visibility:** private
- **File:** `gregtech/api/util/WorldSpawnedEventBuilder.java`
- **Line:** 60

```java
private interface IEntityWorldSpawnedEvent
```

### IGTHatchAdder
- **Visibility:** public
- **File:** `gregtech/api/util/IGTHatchAdder.java`
- **Line:** 5

```java
public interface IGTHatchAdder<T>
```

### IMachineMessage
- **Visibility:** public
- **File:** `gregtech/api/util/IMachineMessage.java`
- **Line:** 10
- **Extends:** `IMachineMessage<T>>`

```java
public interface IMachineMessage<T extends IMachineMessage<T>>
```

### IPositionedWorldSpawnedEvent
- **Visibility:** private
- **File:** `gregtech/api/util/WorldSpawnedEventBuilder.java`
- **Line:** 51

```java
private interface IPositionedWorldSpawnedEvent
```

### ISoundWorldSpawnedEvent
- **Visibility:** private
- **File:** `gregtech/api/util/WorldSpawnedEventBuilder.java`
- **Line:** 83

```java
private interface ISoundWorldSpawnedEvent
```

### IStringIdentifierWorldSpawnedEvent
- **Visibility:** private
- **File:** `gregtech/api/util/WorldSpawnedEventBuilder.java`
- **Line:** 74

```java
private interface IStringIdentifierWorldSpawnedEvent
```

### InputConsumer
- **Visibility:** public
- **File:** `gregtech/api/util/ParallelHelper.java`
- **Line:** 660

```java
public interface InputConsumer
```

### LongData
- **Visibility:** public
- **File:** `gregtech/api/util/LongData.java`
- **Line:** 5

```java
public interface LongData
```

### MTEAdder
- **Visibility:** public
- **File:** `gregtech/api/util/GTStructureUtility.java`
- **Line:** 889
- **Extends:** `IMetaTileEntity>`

```java
public interface MTEAdder<T, TMTE extends IMetaTileEntity>
```

### MaxParallelCalculator
- **Visibility:** public
- **File:** `gregtech/api/util/ParallelHelper.java`
- **Line:** 654

```java
public interface MaxParallelCalculator
```

## gregtech.api.util.shutdown

### ShutDownReason
- **Visibility:** public
- **File:** `gregtech/api/util/shutdown/ShutDownReason.java`
- **Line:** 5
- **Extends:** `IMachineMessage<ShutDownReason>`

```java
public interface ShutDownReason extends IMachineMessage<ShutDownReason>
```

## gregtech.client

### ISeekingSound
- **Visibility:** public
- **File:** `gregtech/client/ISeekingSound.java`
- **Line:** 8
- **Extends:** `ISound`

```java
public interface ISeekingSound extends ISound
```

## gregtech.client.volumetric

### ISoundPosition
- **Visibility:** public
- **File:** `gregtech/client/volumetric/ISoundPosition.java`
- **Line:** 10

```java
public interface ISoundPosition
```

## gregtech.common.covers

### Invertable
- **Visibility:** public
- **File:** `gregtech/common/covers/Invertable.java`
- **Line:** 3

```java
public interface Invertable
```

## gregtech.common.data

### BlockPosMapComputeFn
- **Visibility:** public
- **File:** `gregtech/common/data/BlockPosMap.java`
- **Line:** 40

```java
public interface BlockPosMapComputeFn<V>
```

### ChunkMapComputeFn
- **Visibility:** public
- **File:** `gregtech/common/data/ChunkMap.java`
- **Line:** 35

```java
public interface ChunkMapComputeFn<V>
```

### FastEntrySet
- **Visibility:** public
- **File:** `gregtech/common/data/BlockPosMap.java`
- **Line:** 61
- **Extends:** `ObjectSet<BlockPosEntry<V>>`

```java
public interface FastEntrySet<V> extends ObjectSet<BlockPosEntry<V>>
```

### FastEntrySet
- **Visibility:** public
- **File:** `gregtech/common/data/ChunkMap.java`
- **Line:** 56
- **Extends:** `ObjectSet<ChunkEntry<V>>`

```java
public interface FastEntrySet<V> extends ObjectSet<ChunkEntry<V>>
```

### MachineOwner
- **Visibility:** package-private
- **File:** `gregtech/common/data/GTPowerfailTracker.java`
- **Line:** 72

```java
interface MachineOwner
```

## gregtech.common.gui.modularui

### ForEachSlot
- **Visibility:** public
- **File:** `gregtech/common/gui/modularui/UIHelper.java`
- **Line:** 197

```java
public interface ForEachSlot
```

## gregtech.common.gui.modularui.multiblock.godforge.data

### IStarColor
- **Visibility:** public
- **File:** `gregtech/common/gui/modularui/multiblock/godforge/data/StarColors.java`
- **Line:** 11

```java
public interface IStarColor
```

## gregtech.common.misc

### IDrillingLogicDelegateOwner
- **Visibility:** public
- **File:** `gregtech/common/misc/IDrillingLogicDelegateOwner.java`
- **Line:** 9
- **Extends:** `IMetaTileEntity`

```java
public interface IDrillingLogicDelegateOwner extends IMetaTileEntity
```

## gregtech.common.misc.spaceprojects.interfaces

### ISP_Requirements
- **Visibility:** package-private
- **File:** `gregtech/common/misc/spaceprojects/interfaces/ISpaceProject.java`
- **Line:** 408

```java
interface ISP_Requirements
```

### ISP_Upgrade
- **Visibility:** package-private
- **File:** `gregtech/common/misc/spaceprojects/interfaces/ISpaceProject.java`
- **Line:** 240

```java
interface ISP_Upgrade
```

### ISpaceBody
- **Visibility:** public
- **File:** `gregtech/common/misc/spaceprojects/interfaces/ISpaceBody.java`
- **Line:** 11

```java
public interface ISpaceBody
```

### ISpaceProject
- **Visibility:** public
- **File:** `gregtech/common/misc/spaceprojects/interfaces/ISpaceProject.java`
- **Line:** 20

```java
public interface ISpaceProject
```

## gregtech.common.modularui2.factory

### OnSelectedAction
- **Visibility:** public
- **File:** `gregtech/common/modularui2/factory/SelectItemGuiBuilder.java`
- **Line:** 238

```java
public interface OnSelectedAction
```

## gregtech.common.ores

### IOreAdapter
- **Visibility:** public
- **File:** `gregtech/common/ores/IOreAdapter.java`
- **Line:** 20
- **Extends:** `IOreMaterial>`

```java
public interface IOreAdapter<TMat extends IOreMaterial>
```

## gregtech.common.render

### IMTERenderer
- **Visibility:** public
- **File:** `gregtech/common/render/IMTERenderer.java`
- **Line:** 5

```java
public interface IMTERenderer
```

### IRenderedBlock
- **Visibility:** public
- **File:** `gregtech/common/render/IRenderedBlock.java`
- **Line:** 16

```java
public interface IRenderedBlock
```

### IRenderedBlockSideCheck
- **Visibility:** public
- **File:** `gregtech/common/render/IRenderedBlockSideCheck.java`
- **Line:** 10

```java
public interface IRenderedBlockSideCheck
```

## gregtech.common.tileentities.generators

### MagicalEnergyBBListener
- **Visibility:** package-private
- **File:** `gregtech/common/tileentities/generators/MTEMagicalEnergyAbsorber.java`
- **Line:** 74

```java
interface MagicalEnergyBBListener
```

## gregtech.common.tileentities.machines

### IDualInputHatch
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/IDualInputHatch.java`
- **Line:** 10

```java
public interface IDualInputHatch
```

### IDualInputHatchWithPattern
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/IDualInputHatchWithPattern.java`
- **Line:** 7
- **Extends:** `IDualInputHatch`

```java
public interface IDualInputHatchWithPattern extends IDualInputHatch
```

### IDualInputInventory
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/IDualInputInventory.java`
- **Line:** 6

```java
public interface IDualInputInventory
```

### IDualInputInventoryWithPattern
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/IDualInputInventoryWithPattern.java`
- **Line:** 5
- **Extends:** `IDualInputInventory`

```java
public interface IDualInputInventoryWithPattern extends IDualInputInventory
```

### IRecipeProcessingAwareHatch
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/IRecipeProcessingAwareHatch.java`
- **Line:** 11

```java
public interface IRecipeProcessingAwareHatch
```

### ISmartInputHatch
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/ISmartInputHatch.java`
- **Line:** 3

```java
public interface ISmartInputHatch
```

## gregtech.common.tileentities.machines.outputme.base

### Environment
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/outputme/base/MTEHatchOutputMEBase.java`
- **Line:** 75
- **Extends:** `IAEStack<T>, F extends MEFilterBase<T, ?, I>, I>`

```java
public interface Environment<T extends IAEStack<T>, F extends MEFilterBase<T, ?, I>, I>
```

## gregtech.common.tileentities.machines.outputme.util

### EntryProcessor
- **Visibility:** public
- **File:** `gregtech/common/tileentities/machines/outputme/util/AECacheCounter.java`
- **Line:** 43

```java
public interface EntryProcessor<T>
```

## gregtech.common.worldgen

### IWorldgenLayer
- **Visibility:** public
- **File:** `gregtech/common/worldgen/IWorldgenLayer.java`
- **Line:** 7

```java
public interface IWorldgenLayer
```

## gregtech.crossmod.ae2

### IMEAwareItemInventory
- **Visibility:** public
- **File:** `gregtech/crossmod/ae2/IMEAwareItemInventory.java`
- **Line:** 9

```java
public interface IMEAwareItemInventory
```

## gregtech.crossmod.visualprospecting

### IDatabase
- **Visibility:** public
- **File:** `gregtech/crossmod/visualprospecting/IDatabase.java`
- **Line:** 7

```java
public interface IDatabase
```

## gregtech.mixin.interfaces.accessors

### AbstractClientPlayerAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/AbstractClientPlayerAccessor.java`
- **Line:** 5

```java
public interface AbstractClientPlayerAccessor
```

### ChunkCacheAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/ChunkCacheAccessor.java`
- **Line:** 5

```java
public interface ChunkCacheAccessor
```

### EntityAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/EntityAccessor.java`
- **Line:** 3

```java
public interface EntityAccessor
```

### EntityItemAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/EntityItemAccessor.java`
- **Line:** 3

```java
public interface EntityItemAccessor
```

### EntityPlayerMPAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/EntityPlayerMPAccessor.java`
- **Line:** 3

```java
public interface EntityPlayerMPAccessor
```

### GuiTextFieldAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/GuiTextFieldAccessor.java`
- **Line:** 3

```java
public interface GuiTextFieldAccessor
```

### HEEChunkProviderAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/HEEChunkProviderAccessor.java`
- **Line:** 5

```java
public interface HEEChunkProviderAccessor
```

### IBlockStemAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/IBlockStemAccessor.java`
- **Line:** 5

```java
public interface IBlockStemAccessor
```

### IRecipeMutableAccess
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/IRecipeMutableAccess.java`
- **Line:** 8

```java
public interface IRecipeMutableAccess
```

### LanguageRegistryAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/LanguageRegistryAccessor.java`
- **Line:** 6

```java
public interface LanguageRegistryAccessor
```

### MapGenIslandAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/MapGenIslandAccessor.java`
- **Line:** 3

```java
public interface MapGenIslandAccessor
```

### PotionAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/PotionAccessor.java`
- **Line:** 3

```java
public interface PotionAccessor
```

### ShapedOreRecipeAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/ShapedOreRecipeAccessor.java`
- **Line:** 3

```java
public interface ShapedOreRecipeAccessor
```

### TesselatorAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/TesselatorAccessor.java`
- **Line:** 3

```java
public interface TesselatorAccessor
```

### WeightedRandomFishableAccessor
- **Visibility:** public
- **File:** `gregtech/mixin/interfaces/accessors/WeightedRandomFishableAccessor.java`
- **Line:** 5

```java
public interface WeightedRandomFishableAccessor
```

## gregtech.nei.formatter

### INEISpecialInfoFormatter
- **Visibility:** public
- **File:** `gregtech/nei/formatter/INEISpecialInfoFormatter.java`
- **Line:** 17

```java
public interface INEISpecialInfoFormatter
```

## gtPlusPlus.api.interfaces

### ITexturedBlock
- **Visibility:** public
- **File:** `gtPlusPlus/api/interfaces/ITexturedBlock.java`
- **Line:** 9
- **Extends:** `ITexturedTileEntity`

```java
public interface ITexturedBlock extends ITexturedTileEntity
```

### ITileTooltip
- **Visibility:** public
- **File:** `gtPlusPlus/api/interfaces/ITileTooltip.java`
- **Line:** 3

```java
public interface ITileTooltip
```

### RunnableWithInfo
- **Visibility:** public
- **File:** `gtPlusPlus/api/interfaces/RunnableWithInfo.java`
- **Line:** 3
- **Extends:** `Runnable`

```java
public interface RunnableWithInfo<V> extends Runnable
```

## gtPlusPlus.core.interfaces

### IGuiManager
- **Visibility:** public
- **File:** `gtPlusPlus/core/interfaces/IGuiManager.java`
- **Line:** 7
- **Extends:** `IGuiManagerMiscUtils`

```java
public interface IGuiManager extends IGuiManagerMiscUtils
```

### IGuiManagerMiscUtils
- **Visibility:** public
- **File:** `gtPlusPlus/core/interfaces/IGuiManagerMiscUtils.java`
- **Line:** 3

```java
public interface IGuiManagerMiscUtils
```

### IItemBlueprint
- **Visibility:** public
- **File:** `gtPlusPlus/core/interfaces/IItemBlueprint.java`
- **Line:** 6

```java
public interface IItemBlueprint
```

## gtnhintergalactic.tile.multi.elevator

### IBlockAdder
- **Visibility:** public
- **File:** `gtnhintergalactic/tile/multi/elevator/ElevatorUtil.java`
- **Line:** 103

```java
public interface IBlockAdder<T>
```

## gtnhlanth.common.beamline

### IConnectsToBeamline
- **Visibility:** public
- **File:** `gtnhlanth/common/beamline/IConnectsToBeamline.java`
- **Line:** 7
- **Extends:** `IMetaTileEntity`

```java
public interface IConnectsToBeamline extends IMetaTileEntity
```

## gtnhlanth.common.item

### ICanFocus
- **Visibility:** public
- **File:** `gtnhlanth/common/item/ICanFocus.java`
- **Line:** 3

```java
public interface ICanFocus
```

## kubatech.api

### TInventoryExtractor
- **Visibility:** public
- **File:** `kubatech/api/EIGDynamicInventory.java`
- **Line:** 467

```java
public interface TInventoryExtractor<T>
```

### TInventoryExtractor
- **Visibility:** public
- **File:** `kubatech/api/DynamicInventory.java`
- **Line:** 444

```java
public interface TInventoryExtractor<T>
```

### TInventoryGetter
- **Visibility:** public
- **File:** `kubatech/api/EIGDynamicInventory.java`
- **Line:** 443

```java
public interface TInventoryGetter<T>
```

### TInventoryGetter
- **Visibility:** public
- **File:** `kubatech/api/DynamicInventory.java`
- **Line:** 420

```java
public interface TInventoryGetter<T>
```

### TInventoryInjector
- **Visibility:** public
- **File:** `kubatech/api/EIGDynamicInventory.java`
- **Line:** 455

```java
public interface TInventoryInjector
```

### TInventoryInjector
- **Visibility:** public
- **File:** `kubatech/api/DynamicInventory.java`
- **Line:** 432

```java
public interface TInventoryInjector
```

### TInventoryReplacerOrMerger
- **Visibility:** public
- **File:** `kubatech/api/EIGDynamicInventory.java`
- **Line:** 478

```java
public interface TInventoryReplacerOrMerger
```

### TInventoryReplacerOrMerger
- **Visibility:** public
- **File:** `kubatech/api/DynamicInventory.java`
- **Line:** 456

```java
public interface TInventoryReplacerOrMerger
```

## kubatech.api.eig

### IEIGBucketFactory
- **Visibility:** public
- **File:** `kubatech/api/eig/IEIGBucketFactory.java`
- **Line:** 8

```java
public interface IEIGBucketFactory
```

## kubatech.api.implementations

### KTContainerConstructor
- **Visibility:** protected
- **File:** `kubatech/api/implementations/KubaTechGTMultiBlockBase.java`
- **Line:** 109
- **Extends:** `KubaTechGTMultiBlockBase<?>>`

```java
protected interface KTContainerConstructor<T extends KubaTechGTMultiBlockBase<?>>
```

## kubatech.api.tileentity

### CustomTileEntityPacketHandler
- **Visibility:** public
- **File:** `kubatech/api/tileentity/CustomTileEntityPacketHandler.java`
- **Line:** 25

```java
public interface CustomTileEntityPacketHandler
```

## kubatech.loaders.block.kubablock

### IModularUIContainerCreator
- **Visibility:** public
- **File:** `kubatech/loaders/block/kubablock/KubaBlock.java`
- **Line:** 188

```java
public interface IModularUIContainerCreator
```

### IModularUIProvider
- **Visibility:** public
- **File:** `kubatech/loaders/block/kubablock/KubaBlock.java`
- **Line:** 194

```java
public interface IModularUIProvider
```

### IProxyTileEntityProvider
- **Visibility:** public
- **File:** `kubatech/loaders/block/kubablock/IProxyTileEntityProvider.java`
- **Line:** 26

```java
public interface IProxyTileEntityProvider
```

## kubatech.loaders.item.kubaitem

### IItemProxyGUI
- **Visibility:** public
- **File:** `kubatech/loaders/item/kubaitem/IItemProxyGUI.java`
- **Line:** 28

```java
public interface IItemProxyGUI
```

## speiger.src.crops.api

### ICropCardInfo
- **Visibility:** public
- **File:** `speiger/src/crops/api/ICropCardInfo.java`
- **Line:** 14

```java
public interface ICropCardInfo
```

## tectech.mechanics.pipe

### IActivePipe
- **Visibility:** public
- **File:** `tectech/mechanics/pipe/IActivePipe.java`
- **Line:** 5
- **Extends:** `IMetaTileEntity`

```java
public interface IActivePipe extends IMetaTileEntity
```

### IConnectsToDataPipe
- **Visibility:** public
- **File:** `tectech/mechanics/pipe/IConnectsToDataPipe.java`
- **Line:** 8

```java
public interface IConnectsToDataPipe
```

### IConnectsToEnergyTunnel
- **Visibility:** public
- **File:** `tectech/mechanics/pipe/IConnectsToEnergyTunnel.java`
- **Line:** 8

```java
public interface IConnectsToEnergyTunnel
```

## tectech.mechanics.tesla

### ITeslaConnectable
- **Visibility:** public
- **File:** `tectech/mechanics/tesla/ITeslaConnectable.java`
- **Line:** 15
- **Extends:** `ITeslaConnectableSimple`

```java
public interface ITeslaConnectable extends ITeslaConnectableSimple
```

### ITeslaConnectableSimple
- **Visibility:** public
- **File:** `tectech/mechanics/tesla/ITeslaConnectableSimple.java`
- **Line:** 5

```java
public interface ITeslaConnectableSimple
```

## tectech.thing.metaTileEntity.multi.base

### INameFunction
- **Visibility:** public
- **File:** `tectech/thing/metaTileEntity/multi/base/INameFunction.java`
- **Line:** 3
- **Extends:** `TTMultiblockBase>`

```java
public interface INameFunction<T extends TTMultiblockBase>
```

### IParameter
- **Visibility:** public
- **File:** `tectech/thing/metaTileEntity/multi/base/Parameters.java`
- **Line:** 127

```java
public interface IParameter
```

### IStatusFunction
- **Visibility:** public
- **File:** `tectech/thing/metaTileEntity/multi/base/IStatusFunction.java`
- **Line:** 3
- **Extends:** `TTMultiblockBase>`

```java
public interface IStatusFunction<T extends TTMultiblockBase>
```

## tectech.thing.metaTileEntity.multi.base.parameter

### IParametrized
- **Visibility:** public
- **File:** `tectech/thing/metaTileEntity/multi/base/parameter/IParametrized.java`
- **Line:** 5

```java
public interface IParametrized
```

