# GregTech 物品列表 (ItemList)

**模块**: GregTech (核心)
**总计**: 2745 个物品
**文件**: `src/main/java/gregtech/api/enums/ItemList.java`
**GitHub**: https://github.com/GTNewHorizons/GT5-Unofficial/blob/master/src/main/java/gregtech/api/enums/ItemList.java

---

## 📋 说明

本文档列出GregTech主模块的所有ItemList枚举项。

### 格式

| 枚举键值 | 获取方法 |
|---------|---------|
| `ItemName` | `ItemList.ItemName.get(amount)` |

### 使用示例

```java
import gregtech.api.enums.ItemList;

// 获取1个物品
ItemStack item = ItemList.Machine_Multi_BlastFurnace.get(1);

// 获取64个物品
ItemStack items = ItemList.Casing_Pipe_Bronze.get(64);

// 检查物品是否已注册
if (ItemList.Hull_LV.hasBeenSet()) {
    // 使用物品
}
```

---

## 📂 分类目录

- [AcceleratorEV](#category-acceleratorev) (1个)
- [AcceleratorHV](#category-acceleratorhv) (1个)
- [AcceleratorIV](#category-acceleratoriv) (1个)
- [AcceleratorLV](#category-acceleratorlv) (1个)
- [AcceleratorLuV](#category-acceleratorluv) (1个)
- [AcceleratorMV](#category-acceleratormv) (1个)
- [AcceleratorUV](#category-acceleratoruv) (1个)
- [AcceleratorZPM](#category-acceleratorzpm) (1个)
- [ActivatedCarbonFilterMesh](#category-activatedcarbonfiltermesh) (1个)
- [AdvDebugStructureWriter](#category-advdebugstructurewriter) (1个)
- [AlloySmelterLuV](#category-alloysmelterluv) (1个)
- [AlloySmelterUEV](#category-alloysmelteruev) (1个)
- [AlloySmelterUHV](#category-alloysmelteruhv) (1个)
- [AlloySmelterUIV](#category-alloysmelteruiv) (1个)
- [AlloySmelterUMV](#category-alloysmelterumv) (1个)
- [AlloySmelterUV](#category-alloysmelteruv) (1个)
- [AlloySmelterZPM](#category-alloysmelterzpm) (1个)
- [Alumina](#category-alumina) (2个)
- [AmplifabricatorLuV](#category-amplifabricatorluv) (1个)
- [AmplifabricatorUEV](#category-amplifabricatoruev) (1个)
- [AmplifabricatorUHV](#category-amplifabricatoruhv) (1个)
- [AmplifabricatorUIV](#category-amplifabricatoruiv) (1个)
- [AmplifabricatorUMV](#category-amplifabricatorumv) (1个)
- [AmplifabricatorUV](#category-amplifabricatoruv) (1个)
- [AmplifabricatorZPM](#category-amplifabricatorzpm) (1个)
- [ArcFurnaceLuV](#category-arcfurnaceluv) (1个)
- [ArcFurnaceUEV](#category-arcfurnaceuev) (1个)
- [ArcFurnaceUHV](#category-arcfurnaceuhv) (1个)
- [ArcFurnaceUIV](#category-arcfurnaceuiv) (1个)
- [ArcFurnaceUMV](#category-arcfurnaceumv) (1个)
- [ArcFurnaceUV](#category-arcfurnaceuv) (1个)
- [ArcFurnaceZPM](#category-arcfurnacezpm) (1个)
- [Armor](#category-armor) (6个)
- [AssemblingMachineLuV](#category-assemblingmachineluv) (1个)
- [AssemblingMachineUEV](#category-assemblingmachineuev) (1个)
- [AssemblingMachineUHV](#category-assemblingmachineuhv) (1个)
- [AssemblingMachineUIV](#category-assemblingmachineuiv) (1个)
- [AssemblingMachineUMV](#category-assemblingmachineumv) (1个)
- [AssemblingMachineUV](#category-assemblingmachineuv) (1个)
- [AssemblingMachineZPM](#category-assemblingmachinezpm) (1个)
- [AutoclaveLuV](#category-autoclaveluv) (1个)
- [AutoclaveUEV](#category-autoclaveuev) (1个)
- [AutoclaveUHV](#category-autoclaveuhv) (1个)
- [AutoclaveUIV](#category-autoclaveuiv) (1个)
- [AutoclaveUMV](#category-autoclaveumv) (1个)
- [AutoclaveUV](#category-autoclaveuv) (1个)
- [AutoclaveZPM](#category-autoclavezpm) (1个)
- [Automation](#category-automation) (74个)
- [Background](#category-background) (1个)
- [BasicCircuitBoard](#category-basiccircuitboard) (1个)
- [BasicPhotolithographicFrameworkCasing](#category-basicphotolithographicframeworkcasing) (1个)
- [Battery](#category-battery) (103个)
- [BatteryHull](#category-batteryhull) (20个)
- [BendingMachineLuV](#category-bendingmachineluv) (1个)
- [BendingMachineUEV](#category-bendingmachineuev) (1个)
- [BendingMachineUHV](#category-bendingmachineuhv) (1个)
- [BendingMachineUIV](#category-bendingmachineuiv) (1个)
- [BendingMachineUMV](#category-bendingmachineumv) (1个)
- [BendingMachineUV](#category-bendingmachineuv) (1个)
- [BendingMachineZPM](#category-bendingmachinezpm) (1个)
- [Beryllium](#category-beryllium) (1个)
- [BetterJukebox](#category-betterjukebox) (5个)
- [Black](#category-black) (3个)
- [Block](#category-block) (13个)
- [BlockExtremeCorrosionResistantCasing](#category-blockextremecorrosionresistantcasing) (1个)
- [BlockFlocculationCasing](#category-blockflocculationcasing) (1个)
- [BlockHighPressureResistantCasing](#category-blockhighpressureresistantcasing) (1个)
- [BlockIndustrialStrengthConcrete](#category-blockindustrialstrengthconcrete) (1个)
- [BlockIndustrialWaterPlantCasing](#category-blockindustrialwaterplantcasing) (1个)
- [BlockNaquadahReinforcedWaterPlantCasing](#category-blocknaquadahreinforcedwaterplantcasing) (1个)
- [BlockNaquadriaReinforcedWaterPlantCasing](#category-blocknaquadriareinforcedwaterplantcasing) (1个)
- [BlockOzoneCasing](#category-blockozonecasing) (1个)
- [BlockPlasmaHeatingCasing](#category-blockplasmaheatingcasing) (1个)
- [BlockQuarkContainmentCasing](#category-blockquarkcontainmentcasing) (1个)
- [BlockQuarkPipe](#category-blockquarkpipe) (1个)
- [BlockQuarkReleaseChamber](#category-blockquarkreleasechamber) (1个)
- [BlockSterileWaterPlantCasing](#category-blocksterilewaterplantcasing) (1个)
- [BlockUltraVioletLaserEmitter](#category-blockultravioletlaseremitter) (1个)
- [Book](#category-book) (4个)
- [Bottle](#category-bottle) (39个)
- [BreweryLuV](#category-breweryluv) (1个)
- [BreweryUEV](#category-breweryuev) (1个)
- [BreweryUHV](#category-breweryuhv) (1个)
- [BreweryUIV](#category-breweryuiv) (1个)
- [BreweryUMV](#category-breweryumv) (1个)
- [BreweryUV](#category-breweryuv) (1个)
- [BreweryZPM](#category-breweryzpm) (1个)
- [Brittle](#category-brittle) (1个)
- [CanningMachineLuV](#category-canningmachineluv) (1个)
- [CanningMachineUEV](#category-canningmachineuev) (1个)
- [CanningMachineUHV](#category-canningmachineuhv) (1个)
- [CanningMachineUIV](#category-canningmachineuiv) (1个)
- [CanningMachineUMV](#category-canningmachineumv) (1个)
- [CanningMachineUV](#category-canningmachineuv) (1个)
- [CanningMachineZPM](#category-canningmachinezpm) (1个)
- [Casing](#category-casing) (135个)
- [CasingIchorium](#category-casingichorium) (1个)
- [CasingThaumium](#category-casingthaumium) (1个)
- [CasingVoid](#category-casingvoid) (1个)
- [Cell](#category-cell) (5个)
- [Central](#category-central) (1个)
- [CentrifugeLuV](#category-centrifugeluv) (1个)
- [CentrifugeUEV](#category-centrifugeuev) (1个)
- [CentrifugeUHV](#category-centrifugeuhv) (1个)
- [CentrifugeUIV](#category-centrifugeuiv) (1个)
- [CentrifugeUMV](#category-centrifugeumv) (1个)
- [CentrifugeUV](#category-centrifugeuv) (1个)
- [CentrifugeZPM](#category-centrifugezpm) (1个)
- [ChaosLocator](#category-chaoslocator) (1个)
- [Charcoal](#category-charcoal) (1个)
- [ChemicalBathLuV](#category-chemicalbathluv) (1个)
- [ChemicalBathUEV](#category-chemicalbathuev) (1个)
- [ChemicalBathUHV](#category-chemicalbathuhv) (1个)
- [ChemicalBathUIV](#category-chemicalbathuiv) (1个)
- [ChemicalBathUMV](#category-chemicalbathumv) (1个)
- [ChemicalBathUV](#category-chemicalbathuv) (1个)
- [ChemicalBathZPM](#category-chemicalbathzpm) (1个)
- [ChemicalReactorLuV](#category-chemicalreactorluv) (1个)
- [ChemicalReactorUEV](#category-chemicalreactoruev) (1个)
- [ChemicalReactorUHV](#category-chemicalreactoruhv) (1个)
- [ChemicalReactorUIV](#category-chemicalreactoruiv) (1个)
- [ChemicalReactorUMV](#category-chemicalreactorumv) (1个)
- [ChemicalReactorUV](#category-chemicalreactoruv) (1个)
- [ChemicalReactorZPM](#category-chemicalreactorzpm) (1个)
- [Circuit](#category-circuit) (160个)
- [CircuitAssemblerMAX](#category-circuitassemblermax) (1个)
- [CircuitAssemblerUEV](#category-circuitassembleruev) (1个)
- [CircuitAssemblerUHV](#category-circuitassembleruhv) (1个)
- [CircuitAssemblerUIV](#category-circuitassembleruiv) (1个)
- [CircuitAssemblerUMV](#category-circuitassemblerumv) (1个)
- [CircuitAssemblerUXV](#category-circuitassembleruxv) (1个)
- [CircuitImprint](#category-circuitimprint) (37个)
- [Coin](#category-coin) (3个)
- [CokeOvenCasing](#category-cokeovencasing) (1个)
- [CokeOvenController](#category-cokeovencontroller) (1个)
- [CokeOvenHatch](#category-cokeovenhatch) (1个)
- [Color](#category-color) (17个)
- [ComplexNanochipGlass](#category-complexnanochipglass) (1个)
- [Component](#category-component) (12个)
- [CompressedFireclay](#category-compressedfireclay) (1个)
- [CompressedInputBusLuV](#category-compressedinputbusluv) (1个)
- [CompressedInputBusUEV](#category-compressedinputbusuev) (1个)
- [CompressedInputBusUHV](#category-compressedinputbusuhv) (1个)
- [CompressedInputBusUIV](#category-compressedinputbusuiv) (1个)
- [CompressedInputBusUMV](#category-compressedinputbusumv) (1个)
- [CompressedInputBusUV](#category-compressedinputbusuv) (1个)
- [CompressedInputBusUXV](#category-compressedinputbusuxv) (1个)
- [CompressedInputBusZPM](#category-compressedinputbuszpm) (1个)
- [CompressedOutputBusLuV](#category-compressedoutputbusluv) (1个)
- [CompressedOutputBusUEV](#category-compressedoutputbusuev) (1个)
- [CompressedOutputBusUHV](#category-compressedoutputbusuhv) (1个)
- [CompressedOutputBusUIV](#category-compressedoutputbusuiv) (1个)
- [CompressedOutputBusUMV](#category-compressedoutputbusumv) (1个)
- [CompressedOutputBusUV](#category-compressedoutputbusuv) (1个)
- [CompressedOutputBusUXV](#category-compressedoutputbusuxv) (1个)
- [CompressedOutputBusZPM](#category-compressedoutputbuszpm) (1个)
- [Compressor](#category-compressor) (2个)
- [CompressorLuV](#category-compressorluv) (1个)
- [CompressorUEV](#category-compressoruev) (1个)
- [CompressorUHV](#category-compressoruhv) (1个)
- [CompressorUIV](#category-compressoruiv) (1个)
- [CompressorUMV](#category-compressorumv) (1个)
- [CompressorUV](#category-compressoruv) (1个)
- [CompressorZPM](#category-compressorzpm) (1个)
- [ComputationalMatrixNanochipCasing](#category-computationalmatrixnanochipcasing) (1个)
- [ConcreteBackfiller1](#category-concretebackfiller1) (1个)
- [ConcreteBackfiller2](#category-concretebackfiller2) (1个)
- [ControllerCircuit](#category-controllercircuit) (1个)
- [Conveyor](#category-conveyor) (14个)
- [Coolant](#category-coolant) (1个)
- [Cover](#category-cover) (60个)
- [Credit](#category-credit) (14个)
- [Crop](#category-crop) (35个)
- [CuringOven](#category-curingoven) (1个)
- [CuttingMachineLuV](#category-cuttingmachineluv) (1个)
- [CuttingMachineUEV](#category-cuttingmachineuev) (1个)
- [CuttingMachineUHV](#category-cuttingmachineuhv) (1个)
- [CuttingMachineUIV](#category-cuttingmachineuiv) (1个)
- [CuttingMachineUMV](#category-cuttingmachineumv) (1个)
- [CuttingMachineUV](#category-cuttingmachineuv) (1个)
- [CuttingMachineZPM](#category-cuttingmachinezpm) (1个)
- [Debug](#category-debug) (1个)
- [DebugEnergyHatch](#category-debugenergyhatch) (1个)
- [DecayWarehouse](#category-decaywarehouse) (1个)
- [DepletedRodExcitedPlutonium](#category-depletedrodexcitedplutonium) (1个)
- [DepletedRodExcitedPlutonium2](#category-depletedrodexcitedplutonium2) (1个)
- [DepletedRodExcitedPlutonium4](#category-depletedrodexcitedplutonium4) (1个)
- [DepletedRodExcitedUranium](#category-depletedrodexciteduranium) (1个)
- [DepletedRodExcitedUranium2](#category-depletedrodexciteduranium2) (1个)
- [DepletedRodExcitedUranium4](#category-depletedrodexciteduranium4) (1个)
- [DepletedRodGlowstone](#category-depletedrodglowstone) (1个)
- [DepletedRodHighDensityPlutonium](#category-depletedrodhighdensityplutonium) (1个)
- [DepletedRodHighDensityPlutonium2](#category-depletedrodhighdensityplutonium2) (1个)
- [DepletedRodHighDensityPlutonium4](#category-depletedrodhighdensityplutonium4) (1个)
- [DepletedRodHighDensityUranium](#category-depletedrodhighdensityuranium) (1个)
- [DepletedRodHighDensityUranium2](#category-depletedrodhighdensityuranium2) (1个)
- [DepletedRodHighDensityUranium4](#category-depletedrodhighdensityuranium4) (1个)
- [DepletedRodLithium](#category-depletedrodlithium) (1个)
- [DepletedRodMOX](#category-depletedrodmox) (1个)
- [DepletedRodMOX2](#category-depletedrodmox2) (1个)
- [DepletedRodMOX4](#category-depletedrodmox4) (1个)
- [DepletedRodNaquadah](#category-depletedrodnaquadah) (1个)
- [DepletedRodNaquadah2](#category-depletedrodnaquadah2) (1个)
- [DepletedRodNaquadah32](#category-depletedrodnaquadah32) (1个)
- [DepletedRodNaquadah4](#category-depletedrodnaquadah4) (1个)
- [DepletedRodNaquadria](#category-depletedrodnaquadria) (1个)
- [DepletedRodNaquadria2](#category-depletedrodnaquadria2) (1个)
- [DepletedRodNaquadria4](#category-depletedrodnaquadria4) (1个)
- [DepletedRodThorium](#category-depletedrodthorium) (1个)
- [DepletedRodThorium2](#category-depletedrodthorium2) (1个)
- [DepletedRodThorium4](#category-depletedrodthorium4) (1个)
- [DepletedRodTiberium](#category-depletedrodtiberium) (1个)
- [DepletedRodTiberium2](#category-depletedrodtiberium2) (1个)
- [DepletedRodTiberium4](#category-depletedrodtiberium4) (1个)
- [DepletedRodUranium](#category-depletedroduranium) (1个)
- [DepletedRodUranium2](#category-depletedroduranium2) (1个)
- [DepletedRodUranium4](#category-depletedroduranium4) (1个)
- [Display](#category-display) (2个)
- [Distillation](#category-distillation) (1个)
- [DistilleryLuV](#category-distilleryluv) (1个)
- [DistilleryUEV](#category-distilleryuev) (1个)
- [DistilleryUHV](#category-distilleryuhv) (1个)
- [DistilleryUIV](#category-distilleryuiv) (1个)
- [DistilleryUMV](#category-distilleryumv) (1个)
- [DistilleryUV](#category-distilleryuv) (1个)
- [DistilleryZPM](#category-distilleryzpm) (1个)
- [DroneRemoteInterface](#category-droneremoteinterface) (1个)
- [Duct](#category-duct) (1个)
- [Dye](#category-dye) (4个)
- [DysonSwarmControlCasing](#category-dysonswarmcontrolcasing) (1个)
- [DysonSwarmControlPrimary](#category-dysonswarmcontrolprimary) (1个)
- [DysonSwarmControlSecondary](#category-dysonswarmcontrolsecondary) (1个)
- [DysonSwarmControlToroid](#category-dysonswarmcontroltoroid) (1个)
- [DysonSwarmController](#category-dysonswarmcontroller) (1个)
- [DysonSwarmDeploymentUnitCasing](#category-dysonswarmdeploymentunitcasing) (1个)
- [DysonSwarmDeploymentUnitCore](#category-dysonswarmdeploymentunitcore) (1个)
- [DysonSwarmDeploymentUnitMagnet](#category-dysonswarmdeploymentunitmagnet) (1个)
- [DysonSwarmModule](#category-dysonswarmmodule) (1个)
- [DysonSwarmReceiverCasing](#category-dysonswarmreceivercasing) (1个)
- [DysonSwarmReceiverDish](#category-dysonswarmreceiverdish) (1个)
- [EV](#category-ev) (1个)
- [Efficient](#category-efficient) (1个)
- [Electric](#category-electric) (42个)
- [ElectricFurnaceLuV](#category-electricfurnaceluv) (1个)
- [ElectricFurnaceUEV](#category-electricfurnaceuev) (1个)
- [ElectricFurnaceUHV](#category-electricfurnaceuhv) (1个)
- [ElectricFurnaceUIV](#category-electricfurnaceuiv) (1个)
- [ElectricFurnaceUMV](#category-electricfurnaceumv) (1个)
- [ElectricFurnaceUV](#category-electricfurnaceuv) (1个)
- [ElectricFurnaceZPM](#category-electricfurnacezpm) (1个)
- [ElectricOvenLuV](#category-electricovenluv) (1个)
- [ElectricOvenUEV](#category-electricovenuev) (1个)
- [ElectricOvenUHV](#category-electricovenuhv) (1个)
- [ElectricOvenUIV](#category-electricovenuiv) (1个)
- [ElectricOvenUMV](#category-electricovenumv) (1个)
- [ElectricOvenUV](#category-electricovenuv) (1个)
- [ElectricOvenZPM](#category-electricovenzpm) (1个)
- [ElectrolyzerLuV](#category-electrolyzerluv) (1个)
- [ElectrolyzerUEV](#category-electrolyzeruev) (1个)
- [ElectrolyzerUHV](#category-electrolyzeruhv) (1个)
- [ElectrolyzerUIV](#category-electrolyzeruiv) (1个)
- [ElectrolyzerUMV](#category-electrolyzerumv) (1个)
- [ElectrolyzerUV](#category-electrolyzeruv) (1个)
- [ElectrolyzerZPM](#category-electrolyzerzpm) (1个)
- [Electromagnet](#category-electromagnet) (5个)
- [ElectromagneticSeparatorLuV](#category-electromagneticseparatorluv) (1个)
- [ElectromagneticSeparatorUEV](#category-electromagneticseparatoruev) (1个)
- [ElectromagneticSeparatorUHV](#category-electromagneticseparatoruhv) (1个)
- [ElectromagneticSeparatorUIV](#category-electromagneticseparatoruiv) (1个)
- [ElectromagneticSeparatorUMV](#category-electromagneticseparatorumv) (1个)
- [ElectromagneticSeparatorUV](#category-electromagneticseparatoruv) (1个)
- [ElectromagneticSeparatorZPM](#category-electromagneticseparatorzpm) (1个)
- [ElectronicsLump](#category-electronicslump) (1个)
- [Emitter](#category-emitter) (14个)
- [Empty](#category-empty) (2个)
- [EnergisedTesseract](#category-energisedtesseract) (1个)
- [Energy](#category-energy) (4个)
- [EnhancedCircuitBoard](#category-enhancedcircuitboard) (1个)
- [EntropicProcessor](#category-entropicprocessor) (1个)
- [Extra](#category-extra) (1个)
- [ExtractorLuV](#category-extractorluv) (1个)
- [ExtractorUEV](#category-extractoruev) (1个)
- [ExtractorUHV](#category-extractoruhv) (1个)
- [ExtractorUIV](#category-extractoruiv) (1个)
- [ExtractorUMV](#category-extractorumv) (1个)
- [ExtractorUV](#category-extractoruv) (1个)
- [ExtractorZPM](#category-extractorzpm) (1个)
- [Extreme](#category-extreme) (1个)
- [ExtruderLuV](#category-extruderluv) (1个)
- [ExtruderUEV](#category-extruderuev) (1个)
- [ExtruderUHV](#category-extruderuhv) (1个)
- [ExtruderUIV](#category-extruderuiv) (1个)
- [ExtruderUMV](#category-extruderumv) (1个)
- [ExtruderUV](#category-extruderuv) (1个)
- [ExtruderZPM](#category-extruderzpm) (1个)
- [FR](#category-fr) (22个)
- [FermenterLuV](#category-fermenterluv) (1个)
- [FermenterUEV](#category-fermenteruev) (1个)
- [FermenterUHV](#category-fermenteruhv) (1个)
- [FermenterUIV](#category-fermenteruiv) (1个)
- [FermenterUMV](#category-fermenterumv) (1个)
- [FermenterUV](#category-fermenteruv) (1个)
- [FermenterZPM](#category-fermenterzpm) (1个)
- [Field](#category-field) (14个)
- [FieldEnergyAbsorberCasing](#category-fieldenergyabsorbercasing) (1个)
- [Firebrick](#category-firebrick) (1个)
- [FirewallProjectionNanochipCasing](#category-firewallprojectionnanochipcasing) (1个)
- [FluidCannerLuV](#category-fluidcannerluv) (1个)
- [FluidCannerUEV](#category-fluidcanneruev) (1个)
- [FluidCannerUHV](#category-fluidcanneruhv) (1个)
- [FluidCannerUIV](#category-fluidcanneruiv) (1个)
- [FluidCannerUMV](#category-fluidcannerumv) (1个)
- [FluidCannerUV](#category-fluidcanneruv) (1个)
- [FluidCannerZPM](#category-fluidcannerzpm) (1个)
- [FluidExtractorLuV](#category-fluidextractorluv) (1个)
- [FluidExtractorUEV](#category-fluidextractoruev) (1个)
- [FluidExtractorUHV](#category-fluidextractoruhv) (1个)
- [FluidExtractorUIV](#category-fluidextractoruiv) (1个)
- [FluidExtractorUMV](#category-fluidextractorumv) (1个)
- [FluidExtractorUV](#category-fluidextractoruv) (1个)
- [FluidExtractorZPM](#category-fluidextractorzpm) (1个)
- [FluidFilter](#category-fluidfilter) (1个)
- [FluidHeaterLuV](#category-fluidheaterluv) (1个)
- [FluidHeaterUEV](#category-fluidheateruev) (1个)
- [FluidHeaterUHV](#category-fluidheateruhv) (1个)
- [FluidHeaterUIV](#category-fluidheateruiv) (1个)
- [FluidHeaterUMV](#category-fluidheaterumv) (1个)
- [FluidHeaterUV](#category-fluidheateruv) (1个)
- [FluidHeaterZPM](#category-fluidheaterzpm) (1个)
- [FluidRegulator](#category-fluidregulator) (14个)
- [FluidSolidifierLuV](#category-fluidsolidifierluv) (1个)
- [FluidSolidifierUEV](#category-fluidsolidifieruev) (1个)
- [FluidSolidifierUHV](#category-fluidsolidifieruhv) (1个)
- [FluidSolidifierUIV](#category-fluidsolidifieruiv) (1个)
- [FluidSolidifierUMV](#category-fluidsolidifierumv) (1个)
- [FluidSolidifierUV](#category-fluidsolidifieruv) (1个)
- [FluidSolidifierZPM](#category-fluidsolidifierzpm) (1个)
- [Food](#category-food) (58个)
- [ForgeHammerLuV](#category-forgehammerluv) (1个)
- [ForgeHammerUEV](#category-forgehammeruev) (1个)
- [ForgeHammerUHV](#category-forgehammeruhv) (1个)
- [ForgeHammerUIV](#category-forgehammeruiv) (1个)
- [ForgeHammerUMV](#category-forgehammerumv) (1个)
- [ForgeHammerUV](#category-forgehammeruv) (1个)
- [ForgeHammerZPM](#category-forgehammerzpm) (1个)
- [FormingPressLuV](#category-formingpressluv) (1个)
- [FormingPressUEV](#category-formingpressuev) (1个)
- [FormingPressUHV](#category-formingpressuhv) (1个)
- [FormingPressUIV](#category-formingpressuiv) (1个)
- [FormingPressUMV](#category-formingpressumv) (1个)
- [FormingPressUV](#category-formingpressuv) (1个)
- [FormingPressZPM](#category-formingpresszpm) (1个)
- [Fuel](#category-fuel) (2个)
- [FusionComputer](#category-fusioncomputer) (3个)
- [GalliumArsenideCrystal](#category-galliumarsenidecrystal) (1个)
- [GalliumArsenideCrystalSmallPart](#category-galliumarsenidecrystalsmallpart) (1个)
- [GelledToluene](#category-gelledtoluene) (1个)
- [Generator](#category-generator) (25个)
- [GigaChad](#category-gigachad) (1个)
- [Glass](#category-glass) (1个)
- [GlassOmniPurposeInfinityFused](#category-glassomnipurposeinfinityfused) (1个)
- [GlassPHResistant](#category-glassphresistant) (1个)
- [GlassQuarkContainment](#category-glassquarkcontainment) (1个)
- [GlassTintedIndustrialBlack](#category-glasstintedindustrialblack) (1个)
- [GlassTintedIndustrialGray](#category-glasstintedindustrialgray) (1个)
- [GlassTintedIndustrialLightGray](#category-glasstintedindustriallightgray) (1个)
- [GlassTintedIndustrialWhite](#category-glasstintedindustrialwhite) (1个)
- [GlassUVResistant](#category-glassuvresistant) (1个)
- [Gravistar](#category-gravistar) (1个)
- [HV](#category-hv) (1个)
- [Harmonic](#category-harmonic) (1个)
- [Hatch](#category-hatch) (137个)
- [Hawking](#category-hawking) (1个)
- [Heating](#category-heating) (1个)
- [Heavy](#category-heavy) (1个)
- [Heliocast](#category-heliocast) (1个)
- [HighEnergyFlowCircuit](#category-highenergyflowcircuit) (1个)
- [Honeycomb](#category-honeycomb) (1个)
- [Hot](#category-hot) (1个)
- [Hull](#category-hull) (20个)
- [Hypercooler](#category-hypercooler) (1个)
- [IC2](#category-ic2) (44个)
- [IV](#category-iv) (1个)
- [ImprintBoard](#category-imprintboard) (1个)
- [IndustrialApiary](#category-industrialapiary) (32个)
- [IndustrialCentrifuge](#category-industrialcentrifuge) (1个)
- [IndustrialPackager](#category-industrialpackager) (1个)
- [IndustrialWireFactory](#category-industrialwirefactory) (1个)
- [InfinityCooledCasing](#category-infinitycooledcasing) (1个)
- [Ingot](#category-ingot) (4个)
- [Intensely](#category-intensely) (1个)
- [IntricateCircuitBoard](#category-intricatecircuitboard) (1个)
- [Item](#category-item) (2个)
- [ItemFilter](#category-itemfilter) (2个)
- [KevlarFiber](#category-kevlarfiber) (1个)
- [LATEX](#category-latex) (1个)
- [LV](#category-lv) (1个)
- [Large](#category-large) (9个)
- [LargeFluidExtractor](#category-largefluidextractor) (1个)
- [LargeGasTurbine](#category-largegasturbine) (1个)
- [LargeHPSteamTurbine](#category-largehpsteamturbine) (1个)
- [LargeMolecularAssembler](#category-largemolecularassembler) (1个)
- [LargePlasmaTurbine](#category-largeplasmaturbine) (1个)
- [LargeSteamTurbine](#category-largesteamturbine) (1个)
- [Laser](#category-laser) (1个)
- [LatheLuV](#category-latheluv) (1个)
- [LatheUEV](#category-latheuev) (1个)
- [LatheUHV](#category-latheuhv) (1个)
- [LatheUIV](#category-latheuiv) (1个)
- [LatheUMV](#category-latheumv) (1个)
- [LatheUV](#category-latheuv) (1个)
- [LatheZPM](#category-lathezpm) (1个)
- [LoadbearingDistributionCasing](#category-loadbearingdistributioncasing) (1个)
- [Locker](#category-locker) (10个)
- [Long](#category-long) (4个)
- [LuV](#category-luv) (1个)
- [MSFMixture](#category-msfmixture) (1个)
- [MV](#category-mv) (1个)
- [MaceratorLuV](#category-maceratorluv) (1个)
- [MaceratorUEV](#category-maceratoruev) (1个)
- [MaceratorUHV](#category-maceratoruhv) (1个)
- [MaceratorUIV](#category-maceratoruiv) (1个)
- [MaceratorUMV](#category-maceratorumv) (1个)
- [MaceratorUV](#category-maceratoruv) (1个)
- [MaceratorZPM](#category-maceratorzpm) (1个)
- [Machine](#category-machine) (334个)
- [MagLevHarness](#category-maglevharness) (1个)
- [MagLevPython](#category-maglevpython) (3个)
- [MagicEnergyAbsorber](#category-magicenergyabsorber) (4个)
- [MagicEnergyConverter](#category-magicenergyconverter) (3个)
- [Magnetic](#category-magnetic) (3个)
- [MagneticAnchorCasing](#category-magneticanchorcasing) (1个)
- [Magnetron](#category-magnetron) (1个)
- [ManaFly](#category-manafly) (1个)
- [MassFabricatorLuV](#category-massfabricatorluv) (1个)
- [MassFabricatorUEV](#category-massfabricatoruev) (1个)
- [MassFabricatorUHV](#category-massfabricatoruhv) (1个)
- [MassFabricatorUIV](#category-massfabricatoruiv) (1个)
- [MassFabricatorUMV](#category-massfabricatorumv) (1个)
- [MassFabricatorUV](#category-massfabricatoruv) (1个)
- [MassFabricatorZPM](#category-massfabricatorzpm) (1个)
- [McGuffium](#category-mcguffium) (1个)
- [MegaChemicalReactor](#category-megachemicalreactor) (1个)
- [MeshInterfaceNanochipCasing](#category-meshinterfacenanochipcasing) (1个)
- [MicroTransmitter](#category-microtransmitter) (6个)
- [MicrowaveLuV](#category-microwaveluv) (1个)
- [MicrowaveUEV](#category-microwaveuev) (1个)
- [MicrowaveUHV](#category-microwaveuhv) (1个)
- [MicrowaveUIV](#category-microwaveuiv) (1个)
- [MicrowaveUMV](#category-microwaveumv) (1个)
- [MicrowaveUV](#category-microwaveuv) (1个)
- [MicrowaveZPM](#category-microwavezpm) (1个)
- [MiningDroneEV](#category-miningdroneev) (1个)
- [MiningDroneHV](#category-miningdronehv) (1个)
- [MiningDroneIV](#category-miningdroneiv) (1个)
- [MiningDroneLV](#category-miningdronelv) (1个)
- [MiningDroneLuV](#category-miningdroneluv) (1个)
- [MiningDroneMAX](#category-miningdronemax) (1个)
- [MiningDroneMV](#category-miningdronemv) (1个)
- [MiningDroneUEV](#category-miningdroneuev) (1个)
- [MiningDroneUHV](#category-miningdroneuhv) (1个)
- [MiningDroneUIV](#category-miningdroneuiv) (1个)
- [MiningDroneUMV](#category-miningdroneumv) (1个)
- [MiningDroneUV](#category-miningdroneuv) (1个)
- [MiningDroneUXV](#category-miningdroneuxv) (1个)
- [MiningDroneZPM](#category-miningdronezpm) (1个)
- [MixerLuV](#category-mixerluv) (1个)
- [MixerUEV](#category-mixeruev) (1个)
- [MixerUHV](#category-mixeruhv) (1个)
- [MixerUIV](#category-mixeruiv) (1个)
- [MixerUMV](#category-mixerumv) (1个)
- [MixerUV](#category-mixeruv) (1个)
- [MixerZPM](#category-mixerzpm) (1个)
- [MobRep](#category-mobrep) (8个)
- [NC](#category-nc) (3个)
- [NULL](#category-null) (1个)
- [NameRemover](#category-nameremover) (1个)
- [NandChip](#category-nandchip) (1个)
- [NandChipArray](#category-nandchiparray) (1个)
- [NaniteFramework](#category-naniteframework) (1个)
- [NaniteShieldingGlass](#category-naniteshieldingglass) (1个)
- [NanoChipModule](#category-nanochipmodule) (11个)
- [NanoForge](#category-nanoforge) (1个)
- [NanotubeSpool](#category-nanotubespool) (1个)
- [NaquadriaSupersolid](#category-naquadriasupersolid) (1个)
- [Naquarite](#category-naquarite) (1个)
- [Netherite](#category-netherite) (2个)
- [Neutron](#category-neutron) (1个)
- [Neutronium](#category-neutronium) (3个)
- [NtNanofibers](#category-ntnanofibers) (1个)
- [NtNanoparticles](#category-ntnanoparticles) (1个)
- [NuclearStar](#category-nuclearstar) (1个)
- [OilCracker](#category-oilcracker) (1个)
- [OilDrill1](#category-oildrill1) (1个)
- [OilDrill2](#category-oildrill2) (1个)
- [OilDrill3](#category-oildrill3) (1个)
- [OilDrill4](#category-oildrill4) (1个)
- [OilDrillInfinite](#category-oildrillinfinite) (1个)
- [Optical](#category-optical) (1个)
- [Optically](#category-optically) (2个)
- [Ore](#category-ore) (1个)
- [OreDrill1](#category-oredrill1) (1个)
- [OreDrill2](#category-oredrill2) (1个)
- [OreDrill3](#category-oredrill3) (1个)
- [OreDrill4](#category-oredrill4) (1个)
- [OreWashingPlantLuV](#category-orewashingplantluv) (1个)
- [OreWashingPlantUEV](#category-orewashingplantuev) (1个)
- [OreWashingPlantUHV](#category-orewashingplantuhv) (1个)
- [OreWashingPlantUIV](#category-orewashingplantuiv) (1个)
- [OreWashingPlantUMV](#category-orewashingplantumv) (1个)
- [OreWashingPlantUV](#category-orewashingplantuv) (1个)
- [OreWashingPlantZPM](#category-orewashingplantzpm) (1个)
- [PCBBioChamber](#category-pcbbiochamber) (1个)
- [PCBCoolingTower](#category-pcbcoolingtower) (1个)
- [PCBFactory](#category-pcbfactory) (1个)
- [Paper](#category-paper) (6个)
- [Phononic](#category-phononic) (1个)
- [PlanetaryGasSiphonCasing](#category-planetarygassiphoncasing) (1个)
- [PlanetaryGasSiphonController](#category-planetarygassiphoncontroller) (1个)
- [Plank](#category-plank) (31个)
- [PlasmaArcFurnaceLuV](#category-plasmaarcfurnaceluv) (1个)
- [PlasmaArcFurnaceUEV](#category-plasmaarcfurnaceuev) (1个)
- [PlasmaArcFurnaceUHV](#category-plasmaarcfurnaceuhv) (1个)
- [PlasmaArcFurnaceUIV](#category-plasmaarcfurnaceuiv) (1个)
- [PlasmaArcFurnaceUMV](#category-plasmaarcfurnaceumv) (1个)
- [PlasmaArcFurnaceUV](#category-plasmaarcfurnaceuv) (1个)
- [PlasmaArcFurnaceZPM](#category-plasmaarcfurnacezpm) (1个)
- [PolarizerLuV](#category-polarizerluv) (1个)
- [PolarizerUEV](#category-polarizeruev) (1个)
- [PolarizerUHV](#category-polarizeruhv) (1个)
- [PolarizerUIV](#category-polarizeruiv) (1个)
- [PolarizerUMV](#category-polarizerumv) (1个)
- [PolarizerUV](#category-polarizeruv) (1个)
- [PolarizerZPM](#category-polarizerzpm) (1个)
- [Power](#category-power) (1个)
- [PrecisionFieldSyncCasing](#category-precisionfieldsynccasing) (1个)
- [PrecisionLaserEngraverLuV](#category-precisionlaserengraverluv) (1个)
- [PrecisionLaserEngraverUEV](#category-precisionlaserengraveruev) (1个)
- [PrecisionLaserEngraverUHV](#category-precisionlaserengraveruhv) (1个)
- [PrecisionLaserEngraverUIV](#category-precisionlaserengraveruiv) (1个)
- [PrecisionLaserEngraverUMV](#category-precisionlaserengraverumv) (1个)
- [PrecisionLaserEngraverUV](#category-precisionlaserengraveruv) (1个)
- [PrecisionLaserEngraverZPM](#category-precisionlaserengraverzpm) (1个)
- [Primary](#category-primary) (1个)
- [Prismarine](#category-prismarine) (1个)
- [Prismatic](#category-prismatic) (1个)
- [Pump](#category-pump) (3个)
- [PyrolyseOven](#category-pyrolyseoven) (1个)
- [Quantum](#category-quantum) (10个)
- [QuantumEye](#category-quantumeye) (1个)
- [QuantumStar](#category-quantumstar) (1个)
- [Quark](#category-quark) (8个)
- [RC](#category-rc) (13个)
- [RadiantNaquadahAlloyCasing](#category-radiantnaquadahalloycasing) (1个)
- [Radiation](#category-radiation) (1个)
- [RadiationProofPhotolithographicFrameworkCasing](#category-radiationproofphotolithographicframeworkcasing) (1个)
- [Radiator](#category-radiator) (1个)
- [RawImprintBoard](#category-rawimprintboard) (1个)
- [Reactor](#category-reactor) (11个)
- [ReceiverCircuit](#category-receivercircuit) (1个)
- [RecyclerLuV](#category-recyclerluv) (1个)
- [RecyclerUEV](#category-recycleruev) (1个)
- [RecyclerUHV](#category-recycleruhv) (1个)
- [RecyclerUIV](#category-recycleruiv) (1个)
- [RecyclerUMV](#category-recyclerumv) (1个)
- [RecyclerUV](#category-recycleruv) (1个)
- [RecyclerZPM](#category-recyclerzpm) (1个)
- [RefinedCircuitBoard](#category-refinedcircuitboard) (1个)
- [ReinforcedPhotolithographicFrameworkCasing](#category-reinforcedphotolithographicframeworkcasing) (1个)
- [ReinforcementNanochipCasing](#category-reinforcementnanochipcasing) (1个)
- [Relativistic](#category-relativistic) (1个)
- [ReplicatorLuV](#category-replicatorluv) (1个)
- [ReplicatorUEV](#category-replicatoruev) (1个)
- [ReplicatorUHV](#category-replicatoruhv) (1个)
- [ReplicatorUIV](#category-replicatoruiv) (1个)
- [ReplicatorUMV](#category-replicatorumv) (1个)
- [ReplicatorUV](#category-replicatoruv) (1个)
- [ReplicatorZPM](#category-replicatorzpm) (1个)
- [ResearchCompleter](#category-researchcompleter) (1个)
- [Robot](#category-robot) (14个)
- [RockBreakerLuV](#category-rockbreakerluv) (1个)
- [RockBreakerUEV](#category-rockbreakeruev) (1个)
- [RockBreakerUHV](#category-rockbreakeruhv) (1个)
- [RockBreakerUIV](#category-rockbreakeruiv) (1个)
- [RockBreakerUMV](#category-rockbreakerumv) (1个)
- [RockBreakerUV](#category-rockbreakeruv) (1个)
- [RockBreakerZPM](#category-rockbreakerzpm) (1个)
- [RodExcitedPlutonium](#category-rodexcitedplutonium) (1个)
- [RodExcitedPlutonium2](#category-rodexcitedplutonium2) (1个)
- [RodExcitedPlutonium4](#category-rodexcitedplutonium4) (1个)
- [RodExcitedUranium](#category-rodexciteduranium) (1个)
- [RodExcitedUranium2](#category-rodexciteduranium2) (1个)
- [RodExcitedUranium4](#category-rodexciteduranium4) (1个)
- [RodGlowstone](#category-rodglowstone) (1个)
- [RodHighDensityPlutonium](#category-rodhighdensityplutonium) (1个)
- [RodHighDensityPlutonium2](#category-rodhighdensityplutonium2) (1个)
- [RodHighDensityPlutonium4](#category-rodhighdensityplutonium4) (1个)
- [RodHighDensityUranium](#category-rodhighdensityuranium) (1个)
- [RodHighDensityUranium2](#category-rodhighdensityuranium2) (1个)
- [RodHighDensityUranium4](#category-rodhighdensityuranium4) (1个)
- [RodLithium](#category-rodlithium) (1个)
- [RodMOX](#category-rodmox) (1个)
- [RodMOX2](#category-rodmox2) (1个)
- [RodMOX4](#category-rodmox4) (1个)
- [RodNaquadah](#category-rodnaquadah) (1个)
- [RodNaquadah2](#category-rodnaquadah2) (1个)
- [RodNaquadah32](#category-rodnaquadah32) (1个)
- [RodNaquadah4](#category-rodnaquadah4) (1个)
- [RodNaquadria](#category-rodnaquadria) (1个)
- [RodNaquadria2](#category-rodnaquadria2) (1个)
- [RodNaquadria4](#category-rodnaquadria4) (1个)
- [RodThorium](#category-rodthorium) (1个)
- [RodThorium2](#category-rodthorium2) (1个)
- [RodThorium4](#category-rodthorium4) (1个)
- [RodTiberium](#category-rodtiberium) (1个)
- [RodTiberium2](#category-rodtiberium2) (1个)
- [RodTiberium4](#category-rodtiberium4) (1个)
- [RodUranium](#category-roduranium) (1个)
- [RodUranium2](#category-roduranium2) (1个)
- [RodUranium4](#category-roduranium4) (1个)
- [Rotor](#category-rotor) (5个)
- [SFMixture](#category-sfmixture) (1个)
- [ScannerLuV](#category-scannerluv) (1个)
- [ScannerUEV](#category-scanneruev) (1个)
- [ScannerUHV](#category-scanneruhv) (1个)
- [ScannerUIV](#category-scanneruiv) (1个)
- [ScannerUMV](#category-scannerumv) (1个)
- [ScannerUV](#category-scanneruv) (1个)
- [ScannerZPM](#category-scannerzpm) (1个)
- [Schematic](#category-schematic) (7个)
- [Secondary](#category-secondary) (1个)
- [Seismic](#category-seismic) (4个)
- [Sensor](#category-sensor) (14个)
- [Shape](#category-shape) (62个)
- [SiftingMachineLuV](#category-siftingmachineluv) (1个)
- [SiftingMachineUEV](#category-siftingmachineuev) (1个)
- [SiftingMachineUHV](#category-siftingmachineuhv) (1个)
- [SiftingMachineUIV](#category-siftingmachineuiv) (1个)
- [SiftingMachineUMV](#category-siftingmachineumv) (1个)
- [SiftingMachineUV](#category-siftingmachineuv) (1个)
- [SiftingMachineZPM](#category-siftingmachinezpm) (1个)
- [SignalCircuit](#category-signalcircuit) (1个)
- [SlicedCircuit](#category-slicedcircuit) (37个)
- [SolarFactory](#category-solarfactory) (1个)
- [SpaceElevatorBaseCasing](#category-spaceelevatorbasecasing) (1个)
- [SpaceElevatorCable](#category-spaceelevatorcable) (1个)
- [SpaceElevatorController](#category-spaceelevatorcontroller) (1个)
- [SpaceElevatorInternalStructure](#category-spaceelevatorinternalstructure) (1个)
- [SpaceElevatorModuleAssemblerT1](#category-spaceelevatormoduleassemblert1) (1个)
- [SpaceElevatorModuleAssemblerT2](#category-spaceelevatormoduleassemblert2) (1个)
- [SpaceElevatorModuleAssemblerT3](#category-spaceelevatormoduleassemblert3) (1个)
- [SpaceElevatorModuleManager](#category-spaceelevatormodulemanager) (1个)
- [SpaceElevatorModuleMinerT1](#category-spaceelevatormoduleminert1) (1个)
- [SpaceElevatorModuleMinerT2](#category-spaceelevatormoduleminert2) (1个)
- [SpaceElevatorModuleMinerT3](#category-spaceelevatormoduleminert3) (1个)
- [SpaceElevatorModulePumpT1](#category-spaceelevatormodulepumpt1) (1个)
- [SpaceElevatorModulePumpT2](#category-spaceelevatormodulepumpt2) (1个)
- [SpaceElevatorModulePumpT3](#category-spaceelevatormodulepumpt3) (1个)
- [SpaceElevatorModuleResearch](#category-spaceelevatormoduleresearch) (1个)
- [SpaceElevatorMotorT1](#category-spaceelevatormotort1) (1个)
- [SpaceElevatorMotorT2](#category-spaceelevatormotort2) (1个)
- [SpaceElevatorMotorT3](#category-spaceelevatormotort3) (1个)
- [SpaceElevatorMotorT4](#category-spaceelevatormotort4) (1个)
- [SpaceElevatorMotorT5](#category-spaceelevatormotort5) (1个)
- [SpaceElevatorSupportStructure](#category-spaceelevatorsupportstructure) (1个)
- [Spinmatron](#category-spinmatron) (2个)
- [Spinneret](#category-spinneret) (1个)
- [Spray](#category-spray) (48个)
- [StableAdhesive](#category-stableadhesive) (1个)
- [Steam](#category-steam) (10个)
- [Streamlined](#category-streamlined) (1个)
- [Super](#category-super) (10个)
- [Superconducting](#category-superconducting) (11个)
- [SuperconductorComposite](#category-superconductorcomposite) (1个)
- [TC](#category-tc) (1个)
- [TF](#category-tf) (3个)
- [TaHfCNanofibers](#category-tahfcnanofibers) (1个)
- [TaHfNanoparticles](#category-tahfnanoparticles) (1个)
- [Teleporter](#category-teleporter) (1个)
- [Tesseract](#category-tesseract) (1个)
- [Thermal](#category-thermal) (1个)
- [ThermalCentrifugeLuV](#category-thermalcentrifugeluv) (1个)
- [ThermalCentrifugeUEV](#category-thermalcentrifugeuev) (1个)
- [ThermalCentrifugeUHV](#category-thermalcentrifugeuhv) (1个)
- [ThermalCentrifugeUIV](#category-thermalcentrifugeuiv) (1个)
- [ThermalCentrifugeUMV](#category-thermalcentrifugeumv) (1个)
- [ThermalCentrifugeUV](#category-thermalcentrifugeuv) (1个)
- [ThermalCentrifugeZPM](#category-thermalcentrifugezpm) (1个)
- [ThermosCan](#category-thermoscan) (11个)
- [TierdDrone0](#category-tierddrone0) (1个)
- [TierdDrone1](#category-tierddrone1) (1个)
- [TierdDrone2](#category-tierddrone2) (1个)
- [TierdDrone3](#category-tierddrone3) (1个)
- [Timepiece](#category-timepiece) (1个)
- [Tool](#category-tool) (25个)
- [Transdimensional](#category-transdimensional) (1个)
- [Transformer](#category-transformer) (20个)
- [Tube](#category-tube) (1个)
- [UHTResistantMesh](#category-uhtresistantmesh) (1个)
- [UHV](#category-uhv) (1个)
- [ULV](#category-ulv) (1个)
- [UV](#category-uv) (1个)
- [UltraHighStrengthConcrete](#category-ultrahighstrengthconcrete) (1个)
- [Universal](#category-universal) (1个)
- [Upgrade](#category-upgrade) (4个)
- [VOLUMETRIC](#category-volumetric) (1个)
- [VacuumConveyorPipe](#category-vacuumconveyorpipe) (1个)
- [Vajra](#category-vajra) (1个)
- [WetTransformer](#category-wettransformer) (14个)
- [Wireless](#category-wireless) (33个)
- [WirelessHeadphones](#category-wirelessheadphones) (1个)
- [WiremillLuV](#category-wiremillluv) (1个)
- [WiremillUEV](#category-wiremilluev) (1个)
- [WiremillUHV](#category-wiremilluhv) (1个)
- [WiremillUIV](#category-wiremilluiv) (1个)
- [WiremillUMV](#category-wiremillumv) (1个)
- [WiremillUV](#category-wiremilluv) (1个)
- [WiremillZPM](#category-wiremillzpm) (1个)
- [WoodenCasing](#category-woodencasing) (1个)
- [WormholeGenerator](#category-wormholegenerator) (1个)
- [WovenKevlar](#category-wovenkevlar) (1个)
- [Wrap](#category-wrap) (65个)
- [ZPM](#category-zpm) (2个)
- [ZPM2](#category-zpm2) (1个)
- [ZPM3](#category-zpm3) (1个)
- [ZPM4](#category-zpm4) (1个)
- [ZPM5](#category-zpm5) (1个)
- [ZPM6](#category-zpm6) (1个)

---

## 📜 完整列表

### Category: AcceleratorEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorEV` | `ItemList.AcceleratorEV.get(1)` |

### Category: AcceleratorHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorHV` | `ItemList.AcceleratorHV.get(1)` |

### Category: AcceleratorIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorIV` | `ItemList.AcceleratorIV.get(1)` |

### Category: AcceleratorLV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorLV` | `ItemList.AcceleratorLV.get(1)` |

### Category: AcceleratorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorLuV` | `ItemList.AcceleratorLuV.get(1)` |

### Category: AcceleratorMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorMV` | `ItemList.AcceleratorMV.get(1)` |

### Category: AcceleratorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorUV` | `ItemList.AcceleratorUV.get(1)` |

### Category: AcceleratorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `AcceleratorZPM` | `ItemList.AcceleratorZPM.get(1)` |

### Category: ActivatedCarbonFilterMesh

| 枚举键值 | 获取代码 |
|---------|---------|
| `ActivatedCarbonFilterMesh` | `ItemList.ActivatedCarbonFilterMesh.get(1)` |

### Category: AdvDebugStructureWriter

| 枚举键值 | 获取代码 |
|---------|---------|
| `AdvDebugStructureWriter` | `ItemList.AdvDebugStructureWriter.get(1)` |

### Category: AlloySmelterLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterLuV` | `ItemList.AlloySmelterLuV.get(1)` |

### Category: AlloySmelterUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterUEV` | `ItemList.AlloySmelterUEV.get(1)` |

### Category: AlloySmelterUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterUHV` | `ItemList.AlloySmelterUHV.get(1)` |

### Category: AlloySmelterUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterUIV` | `ItemList.AlloySmelterUIV.get(1)` |

### Category: AlloySmelterUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterUMV` | `ItemList.AlloySmelterUMV.get(1)` |

### Category: AlloySmelterUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterUV` | `ItemList.AlloySmelterUV.get(1)` |

### Category: AlloySmelterZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `AlloySmelterZPM` | `ItemList.AlloySmelterZPM.get(1)` |

### Category: Alumina

| 枚举键值 | 获取代码 |
|---------|---------|
| `Alumina_Support_Ring` | `ItemList.Alumina_Support_Ring.get(1)` |
| `Alumina_Support_Ring_Raw` | `ItemList.Alumina_Support_Ring_Raw.get(1)` |

### Category: AmplifabricatorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorLuV` | `ItemList.AmplifabricatorLuV.get(1)` |

### Category: AmplifabricatorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorUEV` | `ItemList.AmplifabricatorUEV.get(1)` |

### Category: AmplifabricatorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorUHV` | `ItemList.AmplifabricatorUHV.get(1)` |

### Category: AmplifabricatorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorUIV` | `ItemList.AmplifabricatorUIV.get(1)` |

### Category: AmplifabricatorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorUMV` | `ItemList.AmplifabricatorUMV.get(1)` |

### Category: AmplifabricatorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorUV` | `ItemList.AmplifabricatorUV.get(1)` |

### Category: AmplifabricatorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `AmplifabricatorZPM` | `ItemList.AmplifabricatorZPM.get(1)` |

### Category: ArcFurnaceLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceLuV` | `ItemList.ArcFurnaceLuV.get(1)` |

### Category: ArcFurnaceUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceUEV` | `ItemList.ArcFurnaceUEV.get(1)` |

### Category: ArcFurnaceUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceUHV` | `ItemList.ArcFurnaceUHV.get(1)` |

### Category: ArcFurnaceUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceUIV` | `ItemList.ArcFurnaceUIV.get(1)` |

### Category: ArcFurnaceUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceUMV` | `ItemList.ArcFurnaceUMV.get(1)` |

### Category: ArcFurnaceUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceUV` | `ItemList.ArcFurnaceUV.get(1)` |

### Category: ArcFurnaceZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ArcFurnaceZPM` | `ItemList.ArcFurnaceZPM.get(1)` |

### Category: Armor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Armor_Cheat` | `ItemList.Armor_Cheat.get(1)` |
| `Armor_Cloaking` | `ItemList.Armor_Cloaking.get(1)` |
| `Armor_ForceField` | `ItemList.Armor_ForceField.get(1)` |
| `Armor_Lamp` | `ItemList.Armor_Lamp.get(1)` |
| `Armor_LapotronicPack` | `ItemList.Armor_LapotronicPack.get(1)` |
| `Armor_LithiumPack` | `ItemList.Armor_LithiumPack.get(1)` |

### Category: AssemblingMachineLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineLuV` | `ItemList.AssemblingMachineLuV.get(1)` |

### Category: AssemblingMachineUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineUEV` | `ItemList.AssemblingMachineUEV.get(1)` |

### Category: AssemblingMachineUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineUHV` | `ItemList.AssemblingMachineUHV.get(1)` |

### Category: AssemblingMachineUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineUIV` | `ItemList.AssemblingMachineUIV.get(1)` |

### Category: AssemblingMachineUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineUMV` | `ItemList.AssemblingMachineUMV.get(1)` |

### Category: AssemblingMachineUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineUV` | `ItemList.AssemblingMachineUV.get(1)` |

### Category: AssemblingMachineZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `AssemblingMachineZPM` | `ItemList.AssemblingMachineZPM.get(1)` |

### Category: AutoclaveLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveLuV` | `ItemList.AutoclaveLuV.get(1)` |

### Category: AutoclaveUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveUEV` | `ItemList.AutoclaveUEV.get(1)` |

### Category: AutoclaveUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveUHV` | `ItemList.AutoclaveUHV.get(1)` |

### Category: AutoclaveUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveUIV` | `ItemList.AutoclaveUIV.get(1)` |

### Category: AutoclaveUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveUMV` | `ItemList.AutoclaveUMV.get(1)` |

### Category: AutoclaveUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveUV` | `ItemList.AutoclaveUV.get(1)` |

### Category: AutoclaveZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `AutoclaveZPM` | `ItemList.AutoclaveZPM.get(1)` |

### Category: Automation

| 枚举键值 | 获取代码 |
|---------|---------|
| `Automation_ChestBuffer_EV` | `ItemList.Automation_ChestBuffer_EV.get(1)` |
| `Automation_ChestBuffer_HV` | `ItemList.Automation_ChestBuffer_HV.get(1)` |
| `Automation_ChestBuffer_IV` | `ItemList.Automation_ChestBuffer_IV.get(1)` |
| `Automation_ChestBuffer_LV` | `ItemList.Automation_ChestBuffer_LV.get(1)` |
| `Automation_ChestBuffer_LuV` | `ItemList.Automation_ChestBuffer_LuV.get(1)` |
| `Automation_ChestBuffer_MV` | `ItemList.Automation_ChestBuffer_MV.get(1)` |
| `Automation_ChestBuffer_UEV` | `ItemList.Automation_ChestBuffer_UEV.get(1)` |
| `Automation_ChestBuffer_UHV` | `ItemList.Automation_ChestBuffer_UHV.get(1)` |
| `Automation_ChestBuffer_UIV` | `ItemList.Automation_ChestBuffer_UIV.get(1)` |
| `Automation_ChestBuffer_ULV` | `ItemList.Automation_ChestBuffer_ULV.get(1)` |
| `Automation_ChestBuffer_UMV` | `ItemList.Automation_ChestBuffer_UMV.get(1)` |
| `Automation_ChestBuffer_UV` | `ItemList.Automation_ChestBuffer_UV.get(1)` |
| `Automation_ChestBuffer_UXV` | `ItemList.Automation_ChestBuffer_UXV.get(1)` |
| `Automation_ChestBuffer_ZPM` | `ItemList.Automation_ChestBuffer_ZPM.get(1)` |
| `Automation_Filter_EV` | `ItemList.Automation_Filter_EV.get(1)` |
| `Automation_Filter_HV` | `ItemList.Automation_Filter_HV.get(1)` |
| `Automation_Filter_IV` | `ItemList.Automation_Filter_IV.get(1)` |
| `Automation_Filter_LV` | `ItemList.Automation_Filter_LV.get(1)` |
| `Automation_Filter_LuV` | `ItemList.Automation_Filter_LuV.get(1)` |
| `Automation_Filter_MAX` | `ItemList.Automation_Filter_MAX.get(1)` |
| `Automation_Filter_MV` | `ItemList.Automation_Filter_MV.get(1)` |
| `Automation_Filter_ULV` | `ItemList.Automation_Filter_ULV.get(1)` |
| `Automation_Filter_UV` | `ItemList.Automation_Filter_UV.get(1)` |
| `Automation_Filter_ZPM` | `ItemList.Automation_Filter_ZPM.get(1)` |
| `Automation_ItemDistributor_EV` | `ItemList.Automation_ItemDistributor_EV.get(1)` |
| `Automation_ItemDistributor_HV` | `ItemList.Automation_ItemDistributor_HV.get(1)` |
| `Automation_ItemDistributor_IV` | `ItemList.Automation_ItemDistributor_IV.get(1)` |
| `Automation_ItemDistributor_LV` | `ItemList.Automation_ItemDistributor_LV.get(1)` |
| `Automation_ItemDistributor_LuV` | `ItemList.Automation_ItemDistributor_LuV.get(1)` |
| `Automation_ItemDistributor_MAX` | `ItemList.Automation_ItemDistributor_MAX.get(1)` |
| `Automation_ItemDistributor_MV` | `ItemList.Automation_ItemDistributor_MV.get(1)` |
| `Automation_ItemDistributor_ULV` | `ItemList.Automation_ItemDistributor_ULV.get(1)` |
| `Automation_ItemDistributor_UV` | `ItemList.Automation_ItemDistributor_UV.get(1)` |
| `Automation_ItemDistributor_ZPM` | `ItemList.Automation_ItemDistributor_ZPM.get(1)` |
| `Automation_RecipeFilter_EV` | `ItemList.Automation_RecipeFilter_EV.get(1)` |
| `Automation_RecipeFilter_HV` | `ItemList.Automation_RecipeFilter_HV.get(1)` |
| `Automation_RecipeFilter_IV` | `ItemList.Automation_RecipeFilter_IV.get(1)` |
| `Automation_RecipeFilter_LV` | `ItemList.Automation_RecipeFilter_LV.get(1)` |
| `Automation_RecipeFilter_LuV` | `ItemList.Automation_RecipeFilter_LuV.get(1)` |
| `Automation_RecipeFilter_MAX` | `ItemList.Automation_RecipeFilter_MAX.get(1)` |
| `Automation_RecipeFilter_MV` | `ItemList.Automation_RecipeFilter_MV.get(1)` |
| `Automation_RecipeFilter_ULV` | `ItemList.Automation_RecipeFilter_ULV.get(1)` |
| `Automation_RecipeFilter_UV` | `ItemList.Automation_RecipeFilter_UV.get(1)` |
| `Automation_RecipeFilter_ZPM` | `ItemList.Automation_RecipeFilter_ZPM.get(1)` |
| `Automation_Regulator_EV` | `ItemList.Automation_Regulator_EV.get(1)` |
| `Automation_Regulator_HV` | `ItemList.Automation_Regulator_HV.get(1)` |
| `Automation_Regulator_IV` | `ItemList.Automation_Regulator_IV.get(1)` |
| `Automation_Regulator_LV` | `ItemList.Automation_Regulator_LV.get(1)` |
| `Automation_Regulator_LuV` | `ItemList.Automation_Regulator_LuV.get(1)` |
| `Automation_Regulator_MAX` | `ItemList.Automation_Regulator_MAX.get(1)` |
| `Automation_Regulator_MV` | `ItemList.Automation_Regulator_MV.get(1)` |
| `Automation_Regulator_ULV` | `ItemList.Automation_Regulator_ULV.get(1)` |
| `Automation_Regulator_UV` | `ItemList.Automation_Regulator_UV.get(1)` |
| `Automation_Regulator_ZPM` | `ItemList.Automation_Regulator_ZPM.get(1)` |
| `Automation_SuperBuffer_EV` | `ItemList.Automation_SuperBuffer_EV.get(1)` |
| `Automation_SuperBuffer_HV` | `ItemList.Automation_SuperBuffer_HV.get(1)` |
| `Automation_SuperBuffer_IV` | `ItemList.Automation_SuperBuffer_IV.get(1)` |
| `Automation_SuperBuffer_LV` | `ItemList.Automation_SuperBuffer_LV.get(1)` |
| `Automation_SuperBuffer_LuV` | `ItemList.Automation_SuperBuffer_LuV.get(1)` |
| `Automation_SuperBuffer_MAX` | `ItemList.Automation_SuperBuffer_MAX.get(1)` |
| `Automation_SuperBuffer_MV` | `ItemList.Automation_SuperBuffer_MV.get(1)` |
| `Automation_SuperBuffer_ULV` | `ItemList.Automation_SuperBuffer_ULV.get(1)` |
| `Automation_SuperBuffer_UV` | `ItemList.Automation_SuperBuffer_UV.get(1)` |
| `Automation_SuperBuffer_ZPM` | `ItemList.Automation_SuperBuffer_ZPM.get(1)` |
| `Automation_TypeFilter_EV` | `ItemList.Automation_TypeFilter_EV.get(1)` |
| `Automation_TypeFilter_HV` | `ItemList.Automation_TypeFilter_HV.get(1)` |
| `Automation_TypeFilter_IV` | `ItemList.Automation_TypeFilter_IV.get(1)` |
| `Automation_TypeFilter_LV` | `ItemList.Automation_TypeFilter_LV.get(1)` |
| `Automation_TypeFilter_LuV` | `ItemList.Automation_TypeFilter_LuV.get(1)` |
| `Automation_TypeFilter_MAX` | `ItemList.Automation_TypeFilter_MAX.get(1)` |
| `Automation_TypeFilter_MV` | `ItemList.Automation_TypeFilter_MV.get(1)` |
| `Automation_TypeFilter_ULV` | `ItemList.Automation_TypeFilter_ULV.get(1)` |
| `Automation_TypeFilter_UV` | `ItemList.Automation_TypeFilter_UV.get(1)` |
| `Automation_TypeFilter_ZPM` | `ItemList.Automation_TypeFilter_ZPM.get(1)` |

### Category: Background

| 枚举键值 | 获取代码 |
|---------|---------|
| `Background_Radiation_Casing` | `ItemList.Background_Radiation_Casing.get(1)` |

### Category: BasicCircuitBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `BasicCircuitBoard` | `ItemList.BasicCircuitBoard.get(1)` |

### Category: BasicPhotolithographicFrameworkCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BasicPhotolithographicFrameworkCasing` | `ItemList.BasicPhotolithographicFrameworkCasing.get(1)` |

### Category: Battery

| 枚举键值 | 获取代码 |
|---------|---------|
| `Battery_Buffer_1by1_EV` | `ItemList.Battery_Buffer_1by1_EV.get(1)` |
| `Battery_Buffer_1by1_HV` | `ItemList.Battery_Buffer_1by1_HV.get(1)` |
| `Battery_Buffer_1by1_IV` | `ItemList.Battery_Buffer_1by1_IV.get(1)` |
| `Battery_Buffer_1by1_LV` | `ItemList.Battery_Buffer_1by1_LV.get(1)` |
| `Battery_Buffer_1by1_LuV` | `ItemList.Battery_Buffer_1by1_LuV.get(1)` |
| `Battery_Buffer_1by1_MAXV` | `ItemList.Battery_Buffer_1by1_MAXV.get(1)` |
| `Battery_Buffer_1by1_MV` | `ItemList.Battery_Buffer_1by1_MV.get(1)` |
| `Battery_Buffer_1by1_UEV` | `ItemList.Battery_Buffer_1by1_UEV.get(1)` |
| `Battery_Buffer_1by1_UHV` | `ItemList.Battery_Buffer_1by1_UHV.get(1)` |
| `Battery_Buffer_1by1_UIV` | `ItemList.Battery_Buffer_1by1_UIV.get(1)` |
| `Battery_Buffer_1by1_ULV` | `ItemList.Battery_Buffer_1by1_ULV.get(1)` |
| `Battery_Buffer_1by1_UMV` | `ItemList.Battery_Buffer_1by1_UMV.get(1)` |
| `Battery_Buffer_1by1_UV` | `ItemList.Battery_Buffer_1by1_UV.get(1)` |
| `Battery_Buffer_1by1_UXV` | `ItemList.Battery_Buffer_1by1_UXV.get(1)` |
| `Battery_Buffer_1by1_ZPM` | `ItemList.Battery_Buffer_1by1_ZPM.get(1)` |
| `Battery_Buffer_2by2_EV` | `ItemList.Battery_Buffer_2by2_EV.get(1)` |
| `Battery_Buffer_2by2_HV` | `ItemList.Battery_Buffer_2by2_HV.get(1)` |
| `Battery_Buffer_2by2_IV` | `ItemList.Battery_Buffer_2by2_IV.get(1)` |
| `Battery_Buffer_2by2_LV` | `ItemList.Battery_Buffer_2by2_LV.get(1)` |
| `Battery_Buffer_2by2_LuV` | `ItemList.Battery_Buffer_2by2_LuV.get(1)` |
| `Battery_Buffer_2by2_MAXV` | `ItemList.Battery_Buffer_2by2_MAXV.get(1)` |
| `Battery_Buffer_2by2_MV` | `ItemList.Battery_Buffer_2by2_MV.get(1)` |
| `Battery_Buffer_2by2_UEV` | `ItemList.Battery_Buffer_2by2_UEV.get(1)` |
| `Battery_Buffer_2by2_UHV` | `ItemList.Battery_Buffer_2by2_UHV.get(1)` |
| `Battery_Buffer_2by2_UIV` | `ItemList.Battery_Buffer_2by2_UIV.get(1)` |
| `Battery_Buffer_2by2_ULV` | `ItemList.Battery_Buffer_2by2_ULV.get(1)` |
| `Battery_Buffer_2by2_UMV` | `ItemList.Battery_Buffer_2by2_UMV.get(1)` |
| `Battery_Buffer_2by2_UV` | `ItemList.Battery_Buffer_2by2_UV.get(1)` |
| `Battery_Buffer_2by2_UXV` | `ItemList.Battery_Buffer_2by2_UXV.get(1)` |
| `Battery_Buffer_2by2_ZPM` | `ItemList.Battery_Buffer_2by2_ZPM.get(1)` |
| `Battery_Buffer_3by3_EV` | `ItemList.Battery_Buffer_3by3_EV.get(1)` |
| `Battery_Buffer_3by3_HV` | `ItemList.Battery_Buffer_3by3_HV.get(1)` |
| `Battery_Buffer_3by3_IV` | `ItemList.Battery_Buffer_3by3_IV.get(1)` |
| `Battery_Buffer_3by3_LV` | `ItemList.Battery_Buffer_3by3_LV.get(1)` |
| `Battery_Buffer_3by3_LuV` | `ItemList.Battery_Buffer_3by3_LuV.get(1)` |
| `Battery_Buffer_3by3_MAXV` | `ItemList.Battery_Buffer_3by3_MAXV.get(1)` |
| `Battery_Buffer_3by3_MV` | `ItemList.Battery_Buffer_3by3_MV.get(1)` |
| `Battery_Buffer_3by3_UEV` | `ItemList.Battery_Buffer_3by3_UEV.get(1)` |
| `Battery_Buffer_3by3_UHV` | `ItemList.Battery_Buffer_3by3_UHV.get(1)` |
| `Battery_Buffer_3by3_UIV` | `ItemList.Battery_Buffer_3by3_UIV.get(1)` |
| `Battery_Buffer_3by3_ULV` | `ItemList.Battery_Buffer_3by3_ULV.get(1)` |
| `Battery_Buffer_3by3_UMV` | `ItemList.Battery_Buffer_3by3_UMV.get(1)` |
| `Battery_Buffer_3by3_UV` | `ItemList.Battery_Buffer_3by3_UV.get(1)` |
| `Battery_Buffer_3by3_UXV` | `ItemList.Battery_Buffer_3by3_UXV.get(1)` |
| `Battery_Buffer_3by3_ZPM` | `ItemList.Battery_Buffer_3by3_ZPM.get(1)` |
| `Battery_Buffer_4by4_EV` | `ItemList.Battery_Buffer_4by4_EV.get(1)` |
| `Battery_Buffer_4by4_HV` | `ItemList.Battery_Buffer_4by4_HV.get(1)` |
| `Battery_Buffer_4by4_IV` | `ItemList.Battery_Buffer_4by4_IV.get(1)` |
| `Battery_Buffer_4by4_LV` | `ItemList.Battery_Buffer_4by4_LV.get(1)` |
| `Battery_Buffer_4by4_LuV` | `ItemList.Battery_Buffer_4by4_LuV.get(1)` |
| `Battery_Buffer_4by4_MAXV` | `ItemList.Battery_Buffer_4by4_MAXV.get(1)` |
| `Battery_Buffer_4by4_MV` | `ItemList.Battery_Buffer_4by4_MV.get(1)` |
| `Battery_Buffer_4by4_UEV` | `ItemList.Battery_Buffer_4by4_UEV.get(1)` |
| `Battery_Buffer_4by4_UHV` | `ItemList.Battery_Buffer_4by4_UHV.get(1)` |
| `Battery_Buffer_4by4_UIV` | `ItemList.Battery_Buffer_4by4_UIV.get(1)` |
| `Battery_Buffer_4by4_ULV` | `ItemList.Battery_Buffer_4by4_ULV.get(1)` |
| `Battery_Buffer_4by4_UMV` | `ItemList.Battery_Buffer_4by4_UMV.get(1)` |
| `Battery_Buffer_4by4_UV` | `ItemList.Battery_Buffer_4by4_UV.get(1)` |
| `Battery_Buffer_4by4_UXV` | `ItemList.Battery_Buffer_4by4_UXV.get(1)` |
| `Battery_Buffer_4by4_ZPM` | `ItemList.Battery_Buffer_4by4_ZPM.get(1)` |
| `Battery_Charger_4by4_EV` | `ItemList.Battery_Charger_4by4_EV.get(1)` |
| `Battery_Charger_4by4_HV` | `ItemList.Battery_Charger_4by4_HV.get(1)` |
| `Battery_Charger_4by4_IV` | `ItemList.Battery_Charger_4by4_IV.get(1)` |
| `Battery_Charger_4by4_LV` | `ItemList.Battery_Charger_4by4_LV.get(1)` |
| `Battery_Charger_4by4_LuV` | `ItemList.Battery_Charger_4by4_LuV.get(1)` |
| `Battery_Charger_4by4_MV` | `ItemList.Battery_Charger_4by4_MV.get(1)` |
| `Battery_Charger_4by4_UEV` | `ItemList.Battery_Charger_4by4_UEV.get(1)` |
| `Battery_Charger_4by4_UHV` | `ItemList.Battery_Charger_4by4_UHV.get(1)` |
| `Battery_Charger_4by4_UIV` | `ItemList.Battery_Charger_4by4_UIV.get(1)` |
| `Battery_Charger_4by4_ULV` | `ItemList.Battery_Charger_4by4_ULV.get(1)` |
| `Battery_Charger_4by4_UMV` | `ItemList.Battery_Charger_4by4_UMV.get(1)` |
| `Battery_Charger_4by4_UV` | `ItemList.Battery_Charger_4by4_UV.get(1)` |
| `Battery_Charger_4by4_UXV` | `ItemList.Battery_Charger_4by4_UXV.get(1)` |
| `Battery_Charger_4by4_ZPM` | `ItemList.Battery_Charger_4by4_ZPM.get(1)` |
| `Battery_Hull_HV` | `ItemList.Battery_Hull_HV.get(1)` |
| `Battery_Hull_LV` | `ItemList.Battery_Hull_LV.get(1)` |
| `Battery_Hull_MV` | `ItemList.Battery_Hull_MV.get(1)` |
| `Battery_RE_HV_Cadmium` | `ItemList.Battery_RE_HV_Cadmium.get(1)` |
| `Battery_RE_HV_Lithium` | `ItemList.Battery_RE_HV_Lithium.get(1)` |
| `Battery_RE_HV_Sodium` | `ItemList.Battery_RE_HV_Sodium.get(1)` |
| `Battery_RE_LV_Cadmium` | `ItemList.Battery_RE_LV_Cadmium.get(1)` |
| `Battery_RE_LV_Lithium` | `ItemList.Battery_RE_LV_Lithium.get(1)` |
| `Battery_RE_LV_Sodium` | `ItemList.Battery_RE_LV_Sodium.get(1)` |
| `Battery_RE_MV_Cadmium` | `ItemList.Battery_RE_MV_Cadmium.get(1)` |
| `Battery_RE_MV_Lithium` | `ItemList.Battery_RE_MV_Lithium.get(1)` |
| `Battery_RE_MV_Sodium` | `ItemList.Battery_RE_MV_Sodium.get(1)` |
| `Battery_RE_ULV_Tantalum` | `ItemList.Battery_RE_ULV_Tantalum.get(1)` |
| `Battery_SU_HV_Mercury` | `ItemList.Battery_SU_HV_Mercury.get(1)` |
| `Battery_SU_HV_SulfuricAcid` | `ItemList.Battery_SU_HV_SulfuricAcid.get(1)` |
| `Battery_SU_LV_Mercury` | `ItemList.Battery_SU_LV_Mercury.get(1)` |
| `Battery_SU_LV_SulfuricAcid` | `ItemList.Battery_SU_LV_SulfuricAcid.get(1)` |
| `Battery_SU_MV_Mercury` | `ItemList.Battery_SU_MV_Mercury.get(1)` |
| `Battery_SU_MV_SulfuricAcid` | `ItemList.Battery_SU_MV_SulfuricAcid.get(1)` |
| `Battery_TurboCharger_4by4_EV` | `ItemList.Battery_TurboCharger_4by4_EV.get(1)` |
| `Battery_TurboCharger_4by4_HV` | `ItemList.Battery_TurboCharger_4by4_HV.get(1)` |
| `Battery_TurboCharger_4by4_IV` | `ItemList.Battery_TurboCharger_4by4_IV.get(1)` |
| `Battery_TurboCharger_4by4_LV` | `ItemList.Battery_TurboCharger_4by4_LV.get(1)` |
| `Battery_TurboCharger_4by4_LuV` | `ItemList.Battery_TurboCharger_4by4_LuV.get(1)` |
| `Battery_TurboCharger_4by4_MV` | `ItemList.Battery_TurboCharger_4by4_MV.get(1)` |
| `Battery_TurboCharger_4by4_UHV` | `ItemList.Battery_TurboCharger_4by4_UHV.get(1)` |
| `Battery_TurboCharger_4by4_ULV` | `ItemList.Battery_TurboCharger_4by4_ULV.get(1)` |
| `Battery_TurboCharger_4by4_UV` | `ItemList.Battery_TurboCharger_4by4_UV.get(1)` |
| `Battery_TurboCharger_4by4_ZPM` | `ItemList.Battery_TurboCharger_4by4_ZPM.get(1)` |

### Category: BatteryHull

| 枚举键值 | 获取代码 |
|---------|---------|
| `BatteryHull_EV` | `ItemList.BatteryHull_EV.get(1)` |
| `BatteryHull_EV_Full` | `ItemList.BatteryHull_EV_Full.get(1)` |
| `BatteryHull_IV` | `ItemList.BatteryHull_IV.get(1)` |
| `BatteryHull_IV_Full` | `ItemList.BatteryHull_IV_Full.get(1)` |
| `BatteryHull_LuV` | `ItemList.BatteryHull_LuV.get(1)` |
| `BatteryHull_LuV_Full` | `ItemList.BatteryHull_LuV_Full.get(1)` |
| `BatteryHull_UEV` | `ItemList.BatteryHull_UEV.get(1)` |
| `BatteryHull_UEV_Full` | `ItemList.BatteryHull_UEV_Full.get(1)` |
| `BatteryHull_UHV` | `ItemList.BatteryHull_UHV.get(1)` |
| `BatteryHull_UHV_Full` | `ItemList.BatteryHull_UHV_Full.get(1)` |
| `BatteryHull_UIV` | `ItemList.BatteryHull_UIV.get(1)` |
| `BatteryHull_UIV_Full` | `ItemList.BatteryHull_UIV_Full.get(1)` |
| `BatteryHull_UMV` | `ItemList.BatteryHull_UMV.get(1)` |
| `BatteryHull_UMV_Full` | `ItemList.BatteryHull_UMV_Full.get(1)` |
| `BatteryHull_UV` | `ItemList.BatteryHull_UV.get(1)` |
| `BatteryHull_UV_Full` | `ItemList.BatteryHull_UV_Full.get(1)` |
| `BatteryHull_UxV` | `ItemList.BatteryHull_UxV.get(1)` |
| `BatteryHull_UxV_Full` | `ItemList.BatteryHull_UxV_Full.get(1)` |
| `BatteryHull_ZPM` | `ItemList.BatteryHull_ZPM.get(1)` |
| `BatteryHull_ZPM_Full` | `ItemList.BatteryHull_ZPM_Full.get(1)` |

### Category: BendingMachineLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineLuV` | `ItemList.BendingMachineLuV.get(1)` |

### Category: BendingMachineUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineUEV` | `ItemList.BendingMachineUEV.get(1)` |

### Category: BendingMachineUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineUHV` | `ItemList.BendingMachineUHV.get(1)` |

### Category: BendingMachineUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineUIV` | `ItemList.BendingMachineUIV.get(1)` |

### Category: BendingMachineUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineUMV` | `ItemList.BendingMachineUMV.get(1)` |

### Category: BendingMachineUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineUV` | `ItemList.BendingMachineUV.get(1)` |

### Category: BendingMachineZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `BendingMachineZPM` | `ItemList.BendingMachineZPM.get(1)` |

### Category: Beryllium

| 枚举键值 | 获取代码 |
|---------|---------|
| `Beryllium_Shielding_Plate` | `ItemList.Beryllium_Shielding_Plate.get(1)` |

### Category: BetterJukebox

| 枚举键值 | 获取代码 |
|---------|---------|
| `BetterJukebox_EV` | `ItemList.BetterJukebox_EV.get(1)` |
| `BetterJukebox_HV` | `ItemList.BetterJukebox_HV.get(1)` |
| `BetterJukebox_IV` | `ItemList.BetterJukebox_IV.get(1)` |
| `BetterJukebox_LV` | `ItemList.BetterJukebox_LV.get(1)` |
| `BetterJukebox_MV` | `ItemList.BetterJukebox_MV.get(1)` |

### Category: Black

| 枚举键值 | 获取代码 |
|---------|---------|
| `Black_Hole_Closer` | `ItemList.Black_Hole_Closer.get(1)` |
| `Black_Hole_Opener` | `ItemList.Black_Hole_Opener.get(1)` |
| `Black_Hole_Stabilizer` | `ItemList.Black_Hole_Stabilizer.get(1)` |

### Category: Block

| 枚举键值 | 获取代码 |
|---------|---------|
| `Block_BedrockiumCompressed` | `ItemList.Block_BedrockiumCompressed.get(1)` |
| `Block_BrittleCharcoal` | `ItemList.Block_BrittleCharcoal.get(1)` |
| `Block_BronzePlate` | `ItemList.Block_BronzePlate.get(1)` |
| `Block_IridiumTungstensteel` | `ItemList.Block_IridiumTungstensteel.get(1)` |
| `Block_MSSFUEL` | `ItemList.Block_MSSFUEL.get(1)` |
| `Block_NaquadahPlate` | `ItemList.Block_NaquadahPlate.get(1)` |
| `Block_NeutroniumPlate` | `ItemList.Block_NeutroniumPlate.get(1)` |
| `Block_Plascrete` | `ItemList.Block_Plascrete.get(1)` |
| `Block_Powderbarrel` | `ItemList.Block_Powderbarrel.get(1)` |
| `Block_SSFUEL` | `ItemList.Block_SSFUEL.get(1)` |
| `Block_SteelPlate` | `ItemList.Block_SteelPlate.get(1)` |
| `Block_TitaniumPlate` | `ItemList.Block_TitaniumPlate.get(1)` |
| `Block_TungstenSteelReinforced` | `ItemList.Block_TungstenSteelReinforced.get(1)` |

### Category: BlockExtremeCorrosionResistantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockExtremeCorrosionResistantCasing` | `ItemList.BlockExtremeCorrosionResistantCasing.get(1)` |

### Category: BlockFlocculationCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockFlocculationCasing` | `ItemList.BlockFlocculationCasing.get(1)` |

### Category: BlockHighPressureResistantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockHighPressureResistantCasing` | `ItemList.BlockHighPressureResistantCasing.get(1)` |

### Category: BlockIndustrialStrengthConcrete

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockIndustrialStrengthConcrete` | `ItemList.BlockIndustrialStrengthConcrete.get(1)` |

### Category: BlockIndustrialWaterPlantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockIndustrialWaterPlantCasing` | `ItemList.BlockIndustrialWaterPlantCasing.get(1)` |

### Category: BlockNaquadahReinforcedWaterPlantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockNaquadahReinforcedWaterPlantCasing` | `ItemList.BlockNaquadahReinforcedWaterPlantCasing.get(1)` |

### Category: BlockNaquadriaReinforcedWaterPlantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockNaquadriaReinforcedWaterPlantCasing` | `ItemList.BlockNaquadriaReinforcedWaterPlantCasing.get(1)` |

### Category: BlockOzoneCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockOzoneCasing` | `ItemList.BlockOzoneCasing.get(1)` |

### Category: BlockPlasmaHeatingCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockPlasmaHeatingCasing` | `ItemList.BlockPlasmaHeatingCasing.get(1)` |

### Category: BlockQuarkContainmentCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockQuarkContainmentCasing` | `ItemList.BlockQuarkContainmentCasing.get(1)` |

### Category: BlockQuarkPipe

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockQuarkPipe` | `ItemList.BlockQuarkPipe.get(1)` |

### Category: BlockQuarkReleaseChamber

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockQuarkReleaseChamber` | `ItemList.BlockQuarkReleaseChamber.get(1)` |

### Category: BlockSterileWaterPlantCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockSterileWaterPlantCasing` | `ItemList.BlockSterileWaterPlantCasing.get(1)` |

### Category: BlockUltraVioletLaserEmitter

| 枚举键值 | 获取代码 |
|---------|---------|
| `BlockUltraVioletLaserEmitter` | `ItemList.BlockUltraVioletLaserEmitter.get(1)` |

### Category: Book

| 枚举键值 | 获取代码 |
|---------|---------|
| `Book_Written_00` | `ItemList.Book_Written_00.get(1)` |
| `Book_Written_01` | `ItemList.Book_Written_01.get(1)` |
| `Book_Written_02` | `ItemList.Book_Written_02.get(1)` |
| `Book_Written_03` | `ItemList.Book_Written_03.get(1)` |

### Category: Bottle

| 枚举键值 | 获取代码 |
|---------|---------|
| `Bottle_Alcopops` | `ItemList.Bottle_Alcopops.get(1)` |
| `Bottle_Apple_Juice` | `ItemList.Bottle_Apple_Juice.get(1)` |
| `Bottle_Beer` | `ItemList.Bottle_Beer.get(1)` |
| `Bottle_Cave_Johnsons_Grenade_Juice` | `ItemList.Bottle_Cave_Johnsons_Grenade_Juice.get(1)` |
| `Bottle_Chilly_Sauce` | `ItemList.Bottle_Chilly_Sauce.get(1)` |
| `Bottle_Cider` | `ItemList.Bottle_Cider.get(1)` |
| `Bottle_Dark_Beer` | `ItemList.Bottle_Dark_Beer.get(1)` |
| `Bottle_Diablo_Sauce` | `ItemList.Bottle_Diablo_Sauce.get(1)` |
| `Bottle_Diabolo_Sauce` | `ItemList.Bottle_Diabolo_Sauce.get(1)` |
| `Bottle_Dragon_Blood` | `ItemList.Bottle_Dragon_Blood.get(1)` |
| `Bottle_Empty` | `ItemList.Bottle_Empty.get(1)` |
| `Bottle_Glen_McKenner` | `ItemList.Bottle_Glen_McKenner.get(1)` |
| `Bottle_Golden_Apple_Juice` | `ItemList.Bottle_Golden_Apple_Juice.get(1)` |
| `Bottle_Golden_Cider` | `ItemList.Bottle_Golden_Cider.get(1)` |
| `Bottle_Grape_Juice` | `ItemList.Bottle_Grape_Juice.get(1)` |
| `Bottle_Holy_Water` | `ItemList.Bottle_Holy_Water.get(1)` |
| `Bottle_Hops_Juice` | `ItemList.Bottle_Hops_Juice.get(1)` |
| `Bottle_Hot_Sauce` | `ItemList.Bottle_Hot_Sauce.get(1)` |
| `Bottle_Iduns_Apple_Juice` | `ItemList.Bottle_Iduns_Apple_Juice.get(1)` |
| `Bottle_Lemon_Juice` | `ItemList.Bottle_Lemon_Juice.get(1)` |
| `Bottle_Lemonade` | `ItemList.Bottle_Lemonade.get(1)` |
| `Bottle_Leninade` | `ItemList.Bottle_Leninade.get(1)` |
| `Bottle_Limoncello` | `ItemList.Bottle_Limoncello.get(1)` |
| `Bottle_Milk` | `ItemList.Bottle_Milk.get(1)` |
| `Bottle_Mineral_Water` | `ItemList.Bottle_Mineral_Water.get(1)` |
| `Bottle_Notches_Brew` | `ItemList.Bottle_Notches_Brew.get(1)` |
| `Bottle_Pirate_Brew` | `ItemList.Bottle_Pirate_Brew.get(1)` |
| `Bottle_Potato_Juice` | `ItemList.Bottle_Potato_Juice.get(1)` |
| `Bottle_Purple_Drink` | `ItemList.Bottle_Purple_Drink.get(1)` |
| `Bottle_Reed_Water` | `ItemList.Bottle_Reed_Water.get(1)` |
| `Bottle_Rum` | `ItemList.Bottle_Rum.get(1)` |
| `Bottle_Salty_Water` | `ItemList.Bottle_Salty_Water.get(1)` |
| `Bottle_Scotch` | `ItemList.Bottle_Scotch.get(1)` |
| `Bottle_Snitches_Glitch_Sauce` | `ItemList.Bottle_Snitches_Glitch_Sauce.get(1)` |
| `Bottle_Vinegar` | `ItemList.Bottle_Vinegar.get(1)` |
| `Bottle_Vodka` | `ItemList.Bottle_Vodka.get(1)` |
| `Bottle_Wheaty_Hops_Juice` | `ItemList.Bottle_Wheaty_Hops_Juice.get(1)` |
| `Bottle_Wheaty_Juice` | `ItemList.Bottle_Wheaty_Juice.get(1)` |
| `Bottle_Wine` | `ItemList.Bottle_Wine.get(1)` |

### Category: BreweryLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryLuV` | `ItemList.BreweryLuV.get(1)` |

### Category: BreweryUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryUEV` | `ItemList.BreweryUEV.get(1)` |

### Category: BreweryUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryUHV` | `ItemList.BreweryUHV.get(1)` |

### Category: BreweryUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryUIV` | `ItemList.BreweryUIV.get(1)` |

### Category: BreweryUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryUMV` | `ItemList.BreweryUMV.get(1)` |

### Category: BreweryUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryUV` | `ItemList.BreweryUV.get(1)` |

### Category: BreweryZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `BreweryZPM` | `ItemList.BreweryZPM.get(1)` |

### Category: Brittle

| 枚举键值 | 获取代码 |
|---------|---------|
| `Brittle_Netherite_Scrap` | `ItemList.Brittle_Netherite_Scrap.get(1)` |

### Category: CanningMachineLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineLuV` | `ItemList.CanningMachineLuV.get(1)` |

### Category: CanningMachineUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineUEV` | `ItemList.CanningMachineUEV.get(1)` |

### Category: CanningMachineUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineUHV` | `ItemList.CanningMachineUHV.get(1)` |

### Category: CanningMachineUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineUIV` | `ItemList.CanningMachineUIV.get(1)` |

### Category: CanningMachineUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineUMV` | `ItemList.CanningMachineUMV.get(1)` |

### Category: CanningMachineUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineUV` | `ItemList.CanningMachineUV.get(1)` |

### Category: CanningMachineZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CanningMachineZPM` | `ItemList.CanningMachineZPM.get(1)` |

### Category: Casing

| 枚举键值 | 获取代码 |
|---------|---------|
| `Casing_AcidHazard` | `ItemList.Casing_AcidHazard.get(1)` |
| `Casing_AdvancedRadiationProof` | `ItemList.Casing_AdvancedRadiationProof.get(1)` |
| `Casing_Advanced_Iridium` | `ItemList.Casing_Advanced_Iridium.get(1)` |
| `Casing_Advanced_Rhodium_Palladium` | `ItemList.Casing_Advanced_Rhodium_Palladium.get(1)` |
| `Casing_AirFilter_Turbine_T1` | `ItemList.Casing_AirFilter_Turbine_T1.get(1)` |
| `Casing_AirFilter_Turbine_T2` | `ItemList.Casing_AirFilter_Turbine_T2.get(1)` |
| `Casing_AirFilter_Turbine_T3` | `ItemList.Casing_AirFilter_Turbine_T3.get(1)` |
| `Casing_AirFilter_Vent_T1` | `ItemList.Casing_AirFilter_Vent_T1.get(1)` |
| `Casing_AirFilter_Vent_T2` | `ItemList.Casing_AirFilter_Vent_T2.get(1)` |
| `Casing_AirFilter_Vent_T3` | `ItemList.Casing_AirFilter_Vent_T3.get(1)` |
| `Casing_Assembler` | `ItemList.Casing_Assembler.get(1)` |
| `Casing_Autoclave` | `ItemList.Casing_Autoclave.get(1)` |
| `Casing_Beryllium_Integrated_Reactor` | `ItemList.Casing_Beryllium_Integrated_Reactor.get(1)` |
| `Casing_BioHazard` | `ItemList.Casing_BioHazard.get(1)` |
| `Casing_BronzePlatedBricks` | `ItemList.Casing_BronzePlatedBricks.get(1)` |
| `Casing_Cable` | `ItemList.Casing_Cable.get(1)` |
| `Casing_Chemically_Inert` | `ItemList.Casing_Chemically_Inert.get(1)` |
| `Casing_CleanStainlessSteel` | `ItemList.Casing_CleanStainlessSteel.get(1)` |
| `Casing_Coil_AwakenedDraconium` | `ItemList.Casing_Coil_AwakenedDraconium.get(1)` |
| `Casing_Coil_CosmicNeutronium` | `ItemList.Casing_Coil_CosmicNeutronium.get(1)` |
| `Casing_Coil_Cupronickel` | `ItemList.Casing_Coil_Cupronickel.get(1)` |
| `Casing_Coil_ElectrumFlux` | `ItemList.Casing_Coil_ElectrumFlux.get(1)` |
| `Casing_Coil_Eternal` | `ItemList.Casing_Coil_Eternal.get(1)` |
| `Casing_Coil_HSSG` | `ItemList.Casing_Coil_HSSG.get(1)` |
| `Casing_Coil_HSSS` | `ItemList.Casing_Coil_HSSS.get(1)` |
| `Casing_Coil_Hypogen` | `ItemList.Casing_Coil_Hypogen.get(1)` |
| `Casing_Coil_Infinity` | `ItemList.Casing_Coil_Infinity.get(1)` |
| `Casing_Coil_Kanthal` | `ItemList.Casing_Coil_Kanthal.get(1)` |
| `Casing_Coil_Naquadah` | `ItemList.Casing_Coil_Naquadah.get(1)` |
| `Casing_Coil_NaquadahAlloy` | `ItemList.Casing_Coil_NaquadahAlloy.get(1)` |
| `Casing_Coil_Nichrome` | `ItemList.Casing_Coil_Nichrome.get(1)` |
| `Casing_Coil_Superconductor` | `ItemList.Casing_Coil_Superconductor.get(1)` |
| `Casing_Coil_Trinium` | `ItemList.Casing_Coil_Trinium.get(1)` |
| `Casing_Coil_TungstenSteel` | `ItemList.Casing_Coil_TungstenSteel.get(1)` |
| `Casing_ContainmentField` | `ItemList.Casing_ContainmentField.get(1)` |
| `Casing_DataDrive` | `ItemList.Casing_DataDrive.get(1)` |
| `Casing_Dim_Bridge` | `ItemList.Casing_Dim_Bridge.get(1)` |
| `Casing_Dim_Injector` | `ItemList.Casing_Dim_Injector.get(1)` |
| `Casing_Dim_Trans` | `ItemList.Casing_Dim_Trans.get(1)` |
| `Casing_EV` | `ItemList.Casing_EV.get(1)` |
| `Casing_Electromagnetic_Separator` | `ItemList.Casing_Electromagnetic_Separator.get(1)` |
| `Casing_EngineIntake` | `ItemList.Casing_EngineIntake.get(1)` |
| `Casing_ExplosionHazard` | `ItemList.Casing_ExplosionHazard.get(1)` |
| `Casing_ExtremeEngineIntake` | `ItemList.Casing_ExtremeEngineIntake.get(1)` |
| `Casing_FireHazard` | `ItemList.Casing_FireHazard.get(1)` |
| `Casing_Firebox_Bronze` | `ItemList.Casing_Firebox_Bronze.get(1)` |
| `Casing_Firebox_Steel` | `ItemList.Casing_Firebox_Steel.get(1)` |
| `Casing_Firebox_Titanium` | `ItemList.Casing_Firebox_Titanium.get(1)` |
| `Casing_Firebox_TungstenSteel` | `ItemList.Casing_Firebox_TungstenSteel.get(1)` |
| `Casing_Firebricks` | `ItemList.Casing_Firebricks.get(1)` |
| `Casing_Fluid_Solidifier` | `ItemList.Casing_Fluid_Solidifier.get(1)` |
| `Casing_FrostHazard` | `ItemList.Casing_FrostHazard.get(1)` |
| `Casing_FrostProof` | `ItemList.Casing_FrostProof.get(1)` |
| `Casing_Fusion` | `ItemList.Casing_Fusion.get(1)` |
| `Casing_Fusion2` | `ItemList.Casing_Fusion2.get(1)` |
| `Casing_Fusion_Coil` | `ItemList.Casing_Fusion_Coil.get(1)` |
| `Casing_Gearbox_Bronze` | `ItemList.Casing_Gearbox_Bronze.get(1)` |
| `Casing_Gearbox_Steel` | `ItemList.Casing_Gearbox_Steel.get(1)` |
| `Casing_Gearbox_Titanium` | `ItemList.Casing_Gearbox_Titanium.get(1)` |
| `Casing_Gearbox_TungstenSteel` | `ItemList.Casing_Gearbox_TungstenSteel.get(1)` |
| `Casing_Graphite_Moderator` | `ItemList.Casing_Graphite_Moderator.get(1)` |
| `Casing_Grate` | `ItemList.Casing_Grate.get(1)` |
| `Casing_HV` | `ItemList.Casing_HV.get(1)` |
| `Casing_HeatProof` | `ItemList.Casing_HeatProof.get(1)` |
| `Casing_IV` | `ItemList.Casing_IV.get(1)` |
| `Casing_Insulated_Fluid_Pipe` | `ItemList.Casing_Insulated_Fluid_Pipe.get(1)` |
| `Casing_Item_Pipe_Black_Plutonium` | `ItemList.Casing_Item_Pipe_Black_Plutonium.get(1)` |
| `Casing_Item_Pipe_Brass` | `ItemList.Casing_Item_Pipe_Brass.get(1)` |
| `Casing_Item_Pipe_Electrum` | `ItemList.Casing_Item_Pipe_Electrum.get(1)` |
| `Casing_Item_Pipe_Fluxed_Electrum` | `ItemList.Casing_Item_Pipe_Fluxed_Electrum.get(1)` |
| `Casing_Item_Pipe_Osmium` | `ItemList.Casing_Item_Pipe_Osmium.get(1)` |
| `Casing_Item_Pipe_Platinum` | `ItemList.Casing_Item_Pipe_Platinum.get(1)` |
| `Casing_Item_Pipe_Quantium` | `ItemList.Casing_Item_Pipe_Quantium.get(1)` |
| `Casing_Item_Pipe_Tin` | `ItemList.Casing_Item_Pipe_Tin.get(1)` |
| `Casing_LV` | `ItemList.Casing_LV.get(1)` |
| `Casing_Laser` | `ItemList.Casing_Laser.get(1)` |
| `Casing_LuV` | `ItemList.Casing_LuV.get(1)` |
| `Casing_MAX` | `ItemList.Casing_MAX.get(1)` |
| `Casing_MAXV` | `ItemList.Casing_MAXV.get(1)` |
| `Casing_MV` | `ItemList.Casing_MV.get(1)` |
| `Casing_MagicHazard` | `ItemList.Casing_MagicHazard.get(1)` |
| `Casing_Magical` | `ItemList.Casing_Magical.get(1)` |
| `Casing_MiningBlackPlutonium` | `ItemList.Casing_MiningBlackPlutonium.get(1)` |
| `Casing_MiningNeutronium` | `ItemList.Casing_MiningNeutronium.get(1)` |
| `Casing_MiningOsmiridium` | `ItemList.Casing_MiningOsmiridium.get(1)` |
| `Casing_Motor` | `ItemList.Casing_Motor.get(1)` |
| `Casing_NoiseHazard` | `ItemList.Casing_NoiseHazard.get(1)` |
| `Casing_Pipe_Bronze` | `ItemList.Casing_Pipe_Bronze.get(1)` |
| `Casing_Pipe_Polybenzimidazole` | `ItemList.Casing_Pipe_Polybenzimidazole.get(1)` |
| `Casing_Pipe_Polytetrafluoroethylene` | `ItemList.Casing_Pipe_Polytetrafluoroethylene.get(1)` |
| `Casing_Pipe_Steel` | `ItemList.Casing_Pipe_Steel.get(1)` |
| `Casing_Pipe_Titanium` | `ItemList.Casing_Pipe_Titanium.get(1)` |
| `Casing_Pipe_TungstenSteel` | `ItemList.Casing_Pipe_TungstenSteel.get(1)` |
| `Casing_Processor` | `ItemList.Casing_Processor.get(1)` |
| `Casing_Pump` | `ItemList.Casing_Pump.get(1)` |
| `Casing_Pyrolyse` | `ItemList.Casing_Pyrolyse.get(1)` |
| `Casing_RadiationProof` | `ItemList.Casing_RadiationProof.get(1)` |
| `Casing_RadioactiveHazard` | `ItemList.Casing_RadioactiveHazard.get(1)` |
| `Casing_Refined_Graphite` | `ItemList.Casing_Refined_Graphite.get(1)` |
| `Casing_Reinforced_Wood` | `ItemList.Casing_Reinforced_Wood.get(1)` |
| `Casing_RobustTungstenSteel` | `ItemList.Casing_RobustTungstenSteel.get(1)` |
| `Casing_SolidSteel` | `ItemList.Casing_SolidSteel.get(1)` |
| `Casing_StableTitanium` | `ItemList.Casing_StableTitanium.get(1)` |
| `Casing_Stripes_A` | `ItemList.Casing_Stripes_A.get(1)` |
| `Casing_Stripes_B` | `ItemList.Casing_Stripes_B.get(1)` |
| `Casing_Tank_0` | `ItemList.Casing_Tank_0.get(1)` |
| `Casing_Tank_1` | `ItemList.Casing_Tank_1.get(1)` |
| `Casing_Tank_10` | `ItemList.Casing_Tank_10.get(1)` |
| `Casing_Tank_11` | `ItemList.Casing_Tank_11.get(1)` |
| `Casing_Tank_12` | `ItemList.Casing_Tank_12.get(1)` |
| `Casing_Tank_13` | `ItemList.Casing_Tank_13.get(1)` |
| `Casing_Tank_14` | `ItemList.Casing_Tank_14.get(1)` |
| `Casing_Tank_15` | `ItemList.Casing_Tank_15.get(1)` |
| `Casing_Tank_2` | `ItemList.Casing_Tank_2.get(1)` |
| `Casing_Tank_3` | `ItemList.Casing_Tank_3.get(1)` |
| `Casing_Tank_4` | `ItemList.Casing_Tank_4.get(1)` |
| `Casing_Tank_5` | `ItemList.Casing_Tank_5.get(1)` |
| `Casing_Tank_6` | `ItemList.Casing_Tank_6.get(1)` |
| `Casing_Tank_7` | `ItemList.Casing_Tank_7.get(1)` |
| `Casing_Tank_8` | `ItemList.Casing_Tank_8.get(1)` |
| `Casing_Tank_9` | `ItemList.Casing_Tank_9.get(1)` |
| `Casing_Turbine` | `ItemList.Casing_Turbine.get(1)` |
| `Casing_Turbine1` | `ItemList.Casing_Turbine1.get(1)` |
| `Casing_Turbine2` | `ItemList.Casing_Turbine2.get(1)` |
| `Casing_Turbine3` | `ItemList.Casing_Turbine3.get(1)` |
| `Casing_UEV` | `ItemList.Casing_UEV.get(1)` |
| `Casing_UIV` | `ItemList.Casing_UIV.get(1)` |
| `Casing_ULV` | `ItemList.Casing_ULV.get(1)` |
| `Casing_UMV` | `ItemList.Casing_UMV.get(1)` |
| `Casing_UV` | `ItemList.Casing_UV.get(1)` |
| `Casing_UV` | `ItemList.Casing_UV.get(1)` |
| `Casing_UXV` | `ItemList.Casing_UXV.get(1)` |
| `Casing_Vent` | `ItemList.Casing_Vent.get(1)` |
| `Casing_Vent_T2` | `ItemList.Casing_Vent_T2.get(1)` |
| `Casing_ZPM` | `ItemList.Casing_ZPM.get(1)` |

### Category: CasingIchorium

| 枚举键值 | 获取代码 |
|---------|---------|
| `CasingIchorium` | `ItemList.CasingIchorium.get(1)` |

### Category: CasingThaumium

| 枚举键值 | 获取代码 |
|---------|---------|
| `CasingThaumium` | `ItemList.CasingThaumium.get(1)` |

### Category: CasingVoid

| 枚举键值 | 获取代码 |
|---------|---------|
| `CasingVoid` | `ItemList.CasingVoid.get(1)` |

### Category: Cell

| 枚举键值 | 获取代码 |
|---------|---------|
| `Cell_Air` | `ItemList.Cell_Air.get(1)` |
| `Cell_Empty` | `ItemList.Cell_Empty.get(1)` |
| `Cell_Lava` | `ItemList.Cell_Lava.get(1)` |
| `Cell_Universal_Fluid` | `ItemList.Cell_Universal_Fluid.get(1)` |
| `Cell_Water` | `ItemList.Cell_Water.get(1)` |

### Category: Central

| 枚举键值 | 获取代码 |
|---------|---------|
| `Central_Casing_ExoFoundry` | `ItemList.Central_Casing_ExoFoundry.get(1)` |

### Category: CentrifugeLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeLuV` | `ItemList.CentrifugeLuV.get(1)` |

### Category: CentrifugeUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeUEV` | `ItemList.CentrifugeUEV.get(1)` |

### Category: CentrifugeUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeUHV` | `ItemList.CentrifugeUHV.get(1)` |

### Category: CentrifugeUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeUIV` | `ItemList.CentrifugeUIV.get(1)` |

### Category: CentrifugeUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeUMV` | `ItemList.CentrifugeUMV.get(1)` |

### Category: CentrifugeUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeUV` | `ItemList.CentrifugeUV.get(1)` |

### Category: CentrifugeZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CentrifugeZPM` | `ItemList.CentrifugeZPM.get(1)` |

### Category: ChaosLocator

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChaosLocator` | `ItemList.ChaosLocator.get(1)` |

### Category: Charcoal

| 枚举键值 | 获取代码 |
|---------|---------|
| `Charcoal_Pile` | `ItemList.Charcoal_Pile.get(1)` |

### Category: ChemicalBathLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathLuV` | `ItemList.ChemicalBathLuV.get(1)` |

### Category: ChemicalBathUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathUEV` | `ItemList.ChemicalBathUEV.get(1)` |

### Category: ChemicalBathUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathUHV` | `ItemList.ChemicalBathUHV.get(1)` |

### Category: ChemicalBathUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathUIV` | `ItemList.ChemicalBathUIV.get(1)` |

### Category: ChemicalBathUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathUMV` | `ItemList.ChemicalBathUMV.get(1)` |

### Category: ChemicalBathUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathUV` | `ItemList.ChemicalBathUV.get(1)` |

### Category: ChemicalBathZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalBathZPM` | `ItemList.ChemicalBathZPM.get(1)` |

### Category: ChemicalReactorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorLuV` | `ItemList.ChemicalReactorLuV.get(1)` |

### Category: ChemicalReactorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorUEV` | `ItemList.ChemicalReactorUEV.get(1)` |

### Category: ChemicalReactorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorUHV` | `ItemList.ChemicalReactorUHV.get(1)` |

### Category: ChemicalReactorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorUIV` | `ItemList.ChemicalReactorUIV.get(1)` |

### Category: ChemicalReactorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorUMV` | `ItemList.ChemicalReactorUMV.get(1)` |

### Category: ChemicalReactorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorUV` | `ItemList.ChemicalReactorUV.get(1)` |

### Category: ChemicalReactorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ChemicalReactorZPM` | `ItemList.ChemicalReactorZPM.get(1)` |

### Category: Circuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `Circuit_Advanced` | `ItemList.Circuit_Advanced.get(1)` |
| `Circuit_Basic` | `ItemList.Circuit_Basic.get(1)` |
| `Circuit_Biomainframe` | `ItemList.Circuit_Biomainframe.get(1)` |
| `Circuit_Bioprocessor` | `ItemList.Circuit_Bioprocessor.get(1)` |
| `Circuit_Biowarecomputer` | `ItemList.Circuit_Biowarecomputer.get(1)` |
| `Circuit_Biowaresupercomputer` | `ItemList.Circuit_Biowaresupercomputer.get(1)` |
| `Circuit_Board_Advanced` | `ItemList.Circuit_Board_Advanced.get(1)` |
| `Circuit_Board_Basic` | `ItemList.Circuit_Board_Basic.get(1)` |
| `Circuit_Board_Bio` | `ItemList.Circuit_Board_Bio.get(1)` |
| `Circuit_Board_Bio_Ultra` | `ItemList.Circuit_Board_Bio_Ultra.get(1)` |
| `Circuit_Board_Coated` | `ItemList.Circuit_Board_Coated.get(1)` |
| `Circuit_Board_Coated_Basic` | `ItemList.Circuit_Board_Coated_Basic.get(1)` |
| `Circuit_Board_Elite` | `ItemList.Circuit_Board_Elite.get(1)` |
| `Circuit_Board_Epoxy` | `ItemList.Circuit_Board_Epoxy.get(1)` |
| `Circuit_Board_Epoxy_Advanced` | `ItemList.Circuit_Board_Epoxy_Advanced.get(1)` |
| `Circuit_Board_Fiberglass` | `ItemList.Circuit_Board_Fiberglass.get(1)` |
| `Circuit_Board_Fiberglass_Advanced` | `ItemList.Circuit_Board_Fiberglass_Advanced.get(1)` |
| `Circuit_Board_Multifiberglass` | `ItemList.Circuit_Board_Multifiberglass.get(1)` |
| `Circuit_Board_Multifiberglass_Elite` | `ItemList.Circuit_Board_Multifiberglass_Elite.get(1)` |
| `Circuit_Board_Optical` | `ItemList.Circuit_Board_Optical.get(1)` |
| `Circuit_Board_Phenolic` | `ItemList.Circuit_Board_Phenolic.get(1)` |
| `Circuit_Board_Phenolic_Good` | `ItemList.Circuit_Board_Phenolic_Good.get(1)` |
| `Circuit_Board_Plastic` | `ItemList.Circuit_Board_Plastic.get(1)` |
| `Circuit_Board_Plastic_Advanced` | `ItemList.Circuit_Board_Plastic_Advanced.get(1)` |
| `Circuit_Board_Wetware` | `ItemList.Circuit_Board_Wetware.get(1)` |
| `Circuit_Board_Wetware_Extreme` | `ItemList.Circuit_Board_Wetware_Extreme.get(1)` |
| `Circuit_Chip_BioCPU` | `ItemList.Circuit_Chip_BioCPU.get(1)` |
| `Circuit_Chip_Biocell` | `ItemList.Circuit_Chip_Biocell.get(1)` |
| `Circuit_Chip_CPU` | `ItemList.Circuit_Chip_CPU.get(1)` |
| `Circuit_Chip_CrystalCPU` | `ItemList.Circuit_Chip_CrystalCPU.get(1)` |
| `Circuit_Chip_CrystalSoC` | `ItemList.Circuit_Chip_CrystalSoC.get(1)` |
| `Circuit_Chip_CrystalSoC2` | `ItemList.Circuit_Chip_CrystalSoC2.get(1)` |
| `Circuit_Chip_HPIC` | `ItemList.Circuit_Chip_HPIC.get(1)` |
| `Circuit_Chip_ILC` | `ItemList.Circuit_Chip_ILC.get(1)` |
| `Circuit_Chip_LPIC` | `ItemList.Circuit_Chip_LPIC.get(1)` |
| `Circuit_Chip_NAND` | `ItemList.Circuit_Chip_NAND.get(1)` |
| `Circuit_Chip_NOR` | `ItemList.Circuit_Chip_NOR.get(1)` |
| `Circuit_Chip_NPIC` | `ItemList.Circuit_Chip_NPIC.get(1)` |
| `Circuit_Chip_NanoCPU` | `ItemList.Circuit_Chip_NanoCPU.get(1)` |
| `Circuit_Chip_NeuroCPU` | `ItemList.Circuit_Chip_NeuroCPU.get(1)` |
| `Circuit_Chip_Optical` | `ItemList.Circuit_Chip_Optical.get(1)` |
| `Circuit_Chip_PIC` | `ItemList.Circuit_Chip_PIC.get(1)` |
| `Circuit_Chip_PPIC` | `ItemList.Circuit_Chip_PPIC.get(1)` |
| `Circuit_Chip_QPIC` | `ItemList.Circuit_Chip_QPIC.get(1)` |
| `Circuit_Chip_QuantumCPU` | `ItemList.Circuit_Chip_QuantumCPU.get(1)` |
| `Circuit_Chip_Ram` | `ItemList.Circuit_Chip_Ram.get(1)` |
| `Circuit_Chip_Simple_SoC` | `ItemList.Circuit_Chip_Simple_SoC.get(1)` |
| `Circuit_Chip_SoC` | `ItemList.Circuit_Chip_SoC.get(1)` |
| `Circuit_Chip_SoC2` | `ItemList.Circuit_Chip_SoC2.get(1)` |
| `Circuit_Chip_Stemcell` | `ItemList.Circuit_Chip_Stemcell.get(1)` |
| `Circuit_Chip_UHPIC` | `ItemList.Circuit_Chip_UHPIC.get(1)` |
| `Circuit_Chip_ULPIC` | `ItemList.Circuit_Chip_ULPIC.get(1)` |
| `Circuit_Computer` | `ItemList.Circuit_Computer.get(1)` |
| `Circuit_CosmicAssembly` | `ItemList.Circuit_CosmicAssembly.get(1)` |
| `Circuit_CosmicComputer` | `ItemList.Circuit_CosmicComputer.get(1)` |
| `Circuit_CosmicMainframe` | `ItemList.Circuit_CosmicMainframe.get(1)` |
| `Circuit_CosmicProcessor` | `ItemList.Circuit_CosmicProcessor.get(1)` |
| `Circuit_Crystalcomputer` | `ItemList.Circuit_Crystalcomputer.get(1)` |
| `Circuit_Crystalmainframe` | `ItemList.Circuit_Crystalmainframe.get(1)` |
| `Circuit_Crystalprocessor` | `ItemList.Circuit_Crystalprocessor.get(1)` |
| `Circuit_Data` | `ItemList.Circuit_Data.get(1)` |
| `Circuit_Elite` | `ItemList.Circuit_Elite.get(1)` |
| `Circuit_Elitenanocomputer` | `ItemList.Circuit_Elitenanocomputer.get(1)` |
| `Circuit_ExoticAssembly` | `ItemList.Circuit_ExoticAssembly.get(1)` |
| `Circuit_ExoticComputer` | `ItemList.Circuit_ExoticComputer.get(1)` |
| `Circuit_ExoticMainframe` | `ItemList.Circuit_ExoticMainframe.get(1)` |
| `Circuit_ExoticProcessor` | `ItemList.Circuit_ExoticProcessor.get(1)` |
| `Circuit_Good` | `ItemList.Circuit_Good.get(1)` |
| `Circuit_Integrated` | `ItemList.Circuit_Integrated.get(1)` |
| `Circuit_Integrated_Good` | `ItemList.Circuit_Integrated_Good.get(1)` |
| `Circuit_Master` | `ItemList.Circuit_Master.get(1)` |
| `Circuit_Masterquantumcomputer` | `ItemList.Circuit_Masterquantumcomputer.get(1)` |
| `Circuit_Microprocessor` | `ItemList.Circuit_Microprocessor.get(1)` |
| `Circuit_Nanocomputer` | `ItemList.Circuit_Nanocomputer.get(1)` |
| `Circuit_Nanoprocessor` | `ItemList.Circuit_Nanoprocessor.get(1)` |
| `Circuit_Neuroprocessor` | `ItemList.Circuit_Neuroprocessor.get(1)` |
| `Circuit_OpticalAssembly` | `ItemList.Circuit_OpticalAssembly.get(1)` |
| `Circuit_OpticalComputer` | `ItemList.Circuit_OpticalComputer.get(1)` |
| `Circuit_OpticalMainframe` | `ItemList.Circuit_OpticalMainframe.get(1)` |
| `Circuit_OpticalProcessor` | `ItemList.Circuit_OpticalProcessor.get(1)` |
| `Circuit_Parts_Advanced` | `ItemList.Circuit_Parts_Advanced.get(1)` |
| `Circuit_Parts_Capacitor` | `ItemList.Circuit_Parts_Capacitor.get(1)` |
| `Circuit_Parts_CapacitorASMD` | `ItemList.Circuit_Parts_CapacitorASMD.get(1)` |
| `Circuit_Parts_CapacitorSMD` | `ItemList.Circuit_Parts_CapacitorSMD.get(1)` |
| `Circuit_Parts_CapacitorXSMD` | `ItemList.Circuit_Parts_CapacitorXSMD.get(1)` |
| `Circuit_Parts_Chip_Bioware` | `ItemList.Circuit_Parts_Chip_Bioware.get(1)` |
| `Circuit_Parts_Coil` | `ItemList.Circuit_Parts_Coil.get(1)` |
| `Circuit_Parts_Crystal_Chip_Elite` | `ItemList.Circuit_Parts_Crystal_Chip_Elite.get(1)` |
| `Circuit_Parts_Crystal_Chip_Master` | `ItemList.Circuit_Parts_Crystal_Chip_Master.get(1)` |
| `Circuit_Parts_Crystal_Chip_Wetware` | `ItemList.Circuit_Parts_Crystal_Chip_Wetware.get(1)` |
| `Circuit_Parts_Diode` | `ItemList.Circuit_Parts_Diode.get(1)` |
| `Circuit_Parts_DiodeASMD` | `ItemList.Circuit_Parts_DiodeASMD.get(1)` |
| `Circuit_Parts_DiodeSMD` | `ItemList.Circuit_Parts_DiodeSMD.get(1)` |
| `Circuit_Parts_DiodeXSMD` | `ItemList.Circuit_Parts_DiodeXSMD.get(1)` |
| `Circuit_Parts_GlassFiber` | `ItemList.Circuit_Parts_GlassFiber.get(1)` |
| `Circuit_Parts_Glass_Tube` | `ItemList.Circuit_Parts_Glass_Tube.get(1)` |
| `Circuit_Parts_InductorASMD` | `ItemList.Circuit_Parts_InductorASMD.get(1)` |
| `Circuit_Parts_InductorSMD` | `ItemList.Circuit_Parts_InductorSMD.get(1)` |
| `Circuit_Parts_InductorXSMD` | `ItemList.Circuit_Parts_InductorXSMD.get(1)` |
| `Circuit_Parts_PetriDish` | `ItemList.Circuit_Parts_PetriDish.get(1)` |
| `Circuit_Parts_RawCrystalChip` | `ItemList.Circuit_Parts_RawCrystalChip.get(1)` |
| `Circuit_Parts_RawCrystalParts` | `ItemList.Circuit_Parts_RawCrystalParts.get(1)` |
| `Circuit_Parts_Reinforced_Glass_Tube` | `ItemList.Circuit_Parts_Reinforced_Glass_Tube.get(1)` |
| `Circuit_Parts_Resistor` | `ItemList.Circuit_Parts_Resistor.get(1)` |
| `Circuit_Parts_ResistorASMD` | `ItemList.Circuit_Parts_ResistorASMD.get(1)` |
| `Circuit_Parts_ResistorSMD` | `ItemList.Circuit_Parts_ResistorSMD.get(1)` |
| `Circuit_Parts_ResistorXSMD` | `ItemList.Circuit_Parts_ResistorXSMD.get(1)` |
| `Circuit_Parts_Transistor` | `ItemList.Circuit_Parts_Transistor.get(1)` |
| `Circuit_Parts_TransistorASMD` | `ItemList.Circuit_Parts_TransistorASMD.get(1)` |
| `Circuit_Parts_TransistorSMD` | `ItemList.Circuit_Parts_TransistorSMD.get(1)` |
| `Circuit_Parts_TransistorXSMD` | `ItemList.Circuit_Parts_TransistorXSMD.get(1)` |
| `Circuit_Parts_Vacuum_Tube` | `ItemList.Circuit_Parts_Vacuum_Tube.get(1)` |
| `Circuit_Parts_Wiring_Advanced` | `ItemList.Circuit_Parts_Wiring_Advanced.get(1)` |
| `Circuit_Parts_Wiring_Basic` | `ItemList.Circuit_Parts_Wiring_Basic.get(1)` |
| `Circuit_Parts_Wiring_Elite` | `ItemList.Circuit_Parts_Wiring_Elite.get(1)` |
| `Circuit_Primitive` | `ItemList.Circuit_Primitive.get(1)` |
| `Circuit_Processor` | `ItemList.Circuit_Processor.get(1)` |
| `Circuit_Quantumcomputer` | `ItemList.Circuit_Quantumcomputer.get(1)` |
| `Circuit_Quantummainframe` | `ItemList.Circuit_Quantummainframe.get(1)` |
| `Circuit_Quantumprocessor` | `ItemList.Circuit_Quantumprocessor.get(1)` |
| `Circuit_Silicon_Ingot` | `ItemList.Circuit_Silicon_Ingot.get(1)` |
| `Circuit_Silicon_Ingot2` | `ItemList.Circuit_Silicon_Ingot2.get(1)` |
| `Circuit_Silicon_Ingot3` | `ItemList.Circuit_Silicon_Ingot3.get(1)` |
| `Circuit_Silicon_Ingot4` | `ItemList.Circuit_Silicon_Ingot4.get(1)` |
| `Circuit_Silicon_Ingot5` | `ItemList.Circuit_Silicon_Ingot5.get(1)` |
| `Circuit_Silicon_Ingot6` | `ItemList.Circuit_Silicon_Ingot6.get(1)` |
| `Circuit_Silicon_Wafer` | `ItemList.Circuit_Silicon_Wafer.get(1)` |
| `Circuit_Silicon_Wafer2` | `ItemList.Circuit_Silicon_Wafer2.get(1)` |
| `Circuit_Silicon_Wafer3` | `ItemList.Circuit_Silicon_Wafer3.get(1)` |
| `Circuit_Silicon_Wafer4` | `ItemList.Circuit_Silicon_Wafer4.get(1)` |
| `Circuit_Silicon_Wafer5` | `ItemList.Circuit_Silicon_Wafer5.get(1)` |
| `Circuit_Silicon_Wafer6` | `ItemList.Circuit_Silicon_Wafer6.get(1)` |
| `Circuit_Silicon_Wafer7` | `ItemList.Circuit_Silicon_Wafer7.get(1)` |
| `Circuit_TranscendentAssembly` | `ItemList.Circuit_TranscendentAssembly.get(1)` |
| `Circuit_TranscendentComputer` | `ItemList.Circuit_TranscendentComputer.get(1)` |
| `Circuit_TranscendentMainframe` | `ItemList.Circuit_TranscendentMainframe.get(1)` |
| `Circuit_TranscendentProcessor` | `ItemList.Circuit_TranscendentProcessor.get(1)` |
| `Circuit_Ultimatecrystalcomputer` | `ItemList.Circuit_Ultimatecrystalcomputer.get(1)` |
| `Circuit_Wafer_Bioware` | `ItemList.Circuit_Wafer_Bioware.get(1)` |
| `Circuit_Wafer_CPU` | `ItemList.Circuit_Wafer_CPU.get(1)` |
| `Circuit_Wafer_HPIC` | `ItemList.Circuit_Wafer_HPIC.get(1)` |
| `Circuit_Wafer_ILC` | `ItemList.Circuit_Wafer_ILC.get(1)` |
| `Circuit_Wafer_LPIC` | `ItemList.Circuit_Wafer_LPIC.get(1)` |
| `Circuit_Wafer_NAND` | `ItemList.Circuit_Wafer_NAND.get(1)` |
| `Circuit_Wafer_NOR` | `ItemList.Circuit_Wafer_NOR.get(1)` |
| `Circuit_Wafer_NPIC` | `ItemList.Circuit_Wafer_NPIC.get(1)` |
| `Circuit_Wafer_NanoCPU` | `ItemList.Circuit_Wafer_NanoCPU.get(1)` |
| `Circuit_Wafer_PIC` | `ItemList.Circuit_Wafer_PIC.get(1)` |
| `Circuit_Wafer_PPIC` | `ItemList.Circuit_Wafer_PPIC.get(1)` |
| `Circuit_Wafer_QPIC` | `ItemList.Circuit_Wafer_QPIC.get(1)` |
| `Circuit_Wafer_QuantumCPU` | `ItemList.Circuit_Wafer_QuantumCPU.get(1)` |
| `Circuit_Wafer_Ram` | `ItemList.Circuit_Wafer_Ram.get(1)` |
| `Circuit_Wafer_Simple_SoC` | `ItemList.Circuit_Wafer_Simple_SoC.get(1)` |
| `Circuit_Wafer_SoC` | `ItemList.Circuit_Wafer_SoC.get(1)` |
| `Circuit_Wafer_SoC2` | `ItemList.Circuit_Wafer_SoC2.get(1)` |
| `Circuit_Wafer_UHPIC` | `ItemList.Circuit_Wafer_UHPIC.get(1)` |
| `Circuit_Wafer_ULPIC` | `ItemList.Circuit_Wafer_ULPIC.get(1)` |
| `Circuit_Wetwarecomputer` | `ItemList.Circuit_Wetwarecomputer.get(1)` |
| `Circuit_Wetwaremainframe` | `ItemList.Circuit_Wetwaremainframe.get(1)` |
| `Circuit_Wetwaresupercomputer` | `ItemList.Circuit_Wetwaresupercomputer.get(1)` |

### Category: CircuitAssemblerMAX

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerMAX` | `ItemList.CircuitAssemblerMAX.get(1)` |

### Category: CircuitAssemblerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerUEV` | `ItemList.CircuitAssemblerUEV.get(1)` |

### Category: CircuitAssemblerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerUHV` | `ItemList.CircuitAssemblerUHV.get(1)` |

### Category: CircuitAssemblerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerUIV` | `ItemList.CircuitAssemblerUIV.get(1)` |

### Category: CircuitAssemblerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerUMV` | `ItemList.CircuitAssemblerUMV.get(1)` |

### Category: CircuitAssemblerUXV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitAssemblerUXV` | `ItemList.CircuitAssemblerUXV.get(1)` |

### Category: CircuitImprint

| 枚举键值 | 获取代码 |
|---------|---------|
| `CircuitImprint_AdvancedCircuit` | `ItemList.CircuitImprint_AdvancedCircuit.get(1)` |
| `CircuitImprint_BasicCircuitBoard` | `ItemList.CircuitImprint_BasicCircuitBoard.get(1)` |
| `CircuitImprint_BiowareAssembly` | `ItemList.CircuitImprint_BiowareAssembly.get(1)` |
| `CircuitImprint_BiowareProcessor` | `ItemList.CircuitImprint_BiowareProcessor.get(1)` |
| `CircuitImprint_ControllerCircuit` | `ItemList.CircuitImprint_ControllerCircuit.get(1)` |
| `CircuitImprint_CrystalAssembly` | `ItemList.CircuitImprint_CrystalAssembly.get(1)` |
| `CircuitImprint_CrystalMainframe` | `ItemList.CircuitImprint_CrystalMainframe.get(1)` |
| `CircuitImprint_CrystalProcessor` | `ItemList.CircuitImprint_CrystalProcessor.get(1)` |
| `CircuitImprint_CrystalSupercomputer` | `ItemList.CircuitImprint_CrystalSupercomputer.get(1)` |
| `CircuitImprint_ElectronicCircuit` | `ItemList.CircuitImprint_ElectronicCircuit.get(1)` |
| `CircuitImprint_EnhancedCircuitBoard` | `ItemList.CircuitImprint_EnhancedCircuitBoard.get(1)` |
| `CircuitImprint_GoodElectronicCircuit` | `ItemList.CircuitImprint_GoodElectronicCircuit.get(1)` |
| `CircuitImprint_GoodIntegratedCircuit` | `ItemList.CircuitImprint_GoodIntegratedCircuit.get(1)` |
| `CircuitImprint_HighEnergyFlowCircuit` | `ItemList.CircuitImprint_HighEnergyFlowCircuit.get(1)` |
| `CircuitImprint_IntegratedLogicCircuit` | `ItemList.CircuitImprint_IntegratedLogicCircuit.get(1)` |
| `CircuitImprint_IntegratedProcessor` | `ItemList.CircuitImprint_IntegratedProcessor.get(1)` |
| `CircuitImprint_IntricateCircuitBoard` | `ItemList.CircuitImprint_IntricateCircuitBoard.get(1)` |
| `CircuitImprint_Mainframe` | `ItemList.CircuitImprint_Mainframe.get(1)` |
| `CircuitImprint_Microprocessor` | `ItemList.CircuitImprint_Microprocessor.get(1)` |
| `CircuitImprint_NANDChipArray` | `ItemList.CircuitImprint_NANDChipArray.get(1)` |
| `CircuitImprint_NanoAssembly` | `ItemList.CircuitImprint_NanoAssembly.get(1)` |
| `CircuitImprint_NanoMainframe` | `ItemList.CircuitImprint_NanoMainframe.get(1)` |
| `CircuitImprint_NanoProcessor` | `ItemList.CircuitImprint_NanoProcessor.get(1)` |
| `CircuitImprint_NanoSupercomputer` | `ItemList.CircuitImprint_NanoSupercomputer.get(1)` |
| `CircuitImprint_OpticalProcessor` | `ItemList.CircuitImprint_OpticalProcessor.get(1)` |
| `CircuitImprint_ProcessorAssembly` | `ItemList.CircuitImprint_ProcessorAssembly.get(1)` |
| `CircuitImprint_QuantumAssembly` | `ItemList.CircuitImprint_QuantumAssembly.get(1)` |
| `CircuitImprint_QuantumMainframe` | `ItemList.CircuitImprint_QuantumMainframe.get(1)` |
| `CircuitImprint_QuantumProcessor` | `ItemList.CircuitImprint_QuantumProcessor.get(1)` |
| `CircuitImprint_QuantumSupercomputer` | `ItemList.CircuitImprint_QuantumSupercomputer.get(1)` |
| `CircuitImprint_ReceiverCircuit` | `ItemList.CircuitImprint_ReceiverCircuit.get(1)` |
| `CircuitImprint_RefinedCircuitBoard` | `ItemList.CircuitImprint_RefinedCircuitBoard.get(1)` |
| `CircuitImprint_SignalCircuit` | `ItemList.CircuitImprint_SignalCircuit.get(1)` |
| `CircuitImprint_WetwareAssembly` | `ItemList.CircuitImprint_WetwareAssembly.get(1)` |
| `CircuitImprint_WetwareProcessor` | `ItemList.CircuitImprint_WetwareProcessor.get(1)` |
| `CircuitImprint_WetwareSupercomputer` | `ItemList.CircuitImprint_WetwareSupercomputer.get(1)` |
| `CircuitImprint_Workstation` | `ItemList.CircuitImprint_Workstation.get(1)` |

### Category: Coin

| 枚举键值 | 获取代码 |
|---------|---------|
| `Coin_Chocolate` | `ItemList.Coin_Chocolate.get(1)` |
| `Coin_Doge` | `ItemList.Coin_Doge.get(1)` |
| `Coin_Gold_Ancient` | `ItemList.Coin_Gold_Ancient.get(1)` |

### Category: CokeOvenCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `CokeOvenCasing` | `ItemList.CokeOvenCasing.get(1)` |

### Category: CokeOvenController

| 枚举键值 | 获取代码 |
|---------|---------|
| `CokeOvenController` | `ItemList.CokeOvenController.get(1)` |

### Category: CokeOvenHatch

| 枚举键值 | 获取代码 |
|---------|---------|
| `CokeOvenHatch` | `ItemList.CokeOvenHatch.get(1)` |

### Category: Color

| 枚举键值 | 获取代码 |
|---------|---------|
| `Color_00` | `ItemList.Color_00.get(1)` |
| `Color_01` | `ItemList.Color_01.get(1)` |
| `Color_02` | `ItemList.Color_02.get(1)` |
| `Color_03` | `ItemList.Color_03.get(1)` |
| `Color_04` | `ItemList.Color_04.get(1)` |
| `Color_05` | `ItemList.Color_05.get(1)` |
| `Color_06` | `ItemList.Color_06.get(1)` |
| `Color_06` | `ItemList.Color_06.get(1)` |
| `Color_07` | `ItemList.Color_07.get(1)` |
| `Color_08` | `ItemList.Color_08.get(1)` |
| `Color_09` | `ItemList.Color_09.get(1)` |
| `Color_10` | `ItemList.Color_10.get(1)` |
| `Color_11` | `ItemList.Color_11.get(1)` |
| `Color_12` | `ItemList.Color_12.get(1)` |
| `Color_13` | `ItemList.Color_13.get(1)` |
| `Color_14` | `ItemList.Color_14.get(1)` |
| `Color_15` | `ItemList.Color_15.get(1)` |

### Category: ComplexNanochipGlass

| 枚举键值 | 获取代码 |
|---------|---------|
| `ComplexNanochipGlass` | `ItemList.ComplexNanochipGlass.get(1)` |

### Category: Component

| 枚举键值 | 获取代码 |
|---------|---------|
| `Component_Filter` | `ItemList.Component_Filter.get(1)` |
| `Component_Grinder_Diamond` | `ItemList.Component_Grinder_Diamond.get(1)` |
| `Component_Grinder_Tungsten` | `ItemList.Component_Grinder_Tungsten.get(1)` |
| `Component_LavaFilter` | `ItemList.Component_LavaFilter.get(1)` |
| `Component_Minecart_Wheels_Iron` | `ItemList.Component_Minecart_Wheels_Iron.get(1)` |
| `Component_Minecart_Wheels_Steel` | `ItemList.Component_Minecart_Wheels_Steel.get(1)` |
| `Component_Sawblade_Diamond` | `ItemList.Component_Sawblade_Diamond.get(1)` |
| `Component_Turbine_Bronze` | `ItemList.Component_Turbine_Bronze.get(1)` |
| `Component_Turbine_Carbon` | `ItemList.Component_Turbine_Carbon.get(1)` |
| `Component_Turbine_Magnalium` | `ItemList.Component_Turbine_Magnalium.get(1)` |
| `Component_Turbine_Steel` | `ItemList.Component_Turbine_Steel.get(1)` |
| `Component_Turbine_TungstenSteel` | `ItemList.Component_Turbine_TungstenSteel.get(1)` |

### Category: CompressedFireclay

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedFireclay` | `ItemList.CompressedFireclay.get(1)` |

### Category: CompressedInputBusLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusLuV` | `ItemList.CompressedInputBusLuV.get(1)` |

### Category: CompressedInputBusUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUEV` | `ItemList.CompressedInputBusUEV.get(1)` |

### Category: CompressedInputBusUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUHV` | `ItemList.CompressedInputBusUHV.get(1)` |

### Category: CompressedInputBusUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUIV` | `ItemList.CompressedInputBusUIV.get(1)` |

### Category: CompressedInputBusUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUMV` | `ItemList.CompressedInputBusUMV.get(1)` |

### Category: CompressedInputBusUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUV` | `ItemList.CompressedInputBusUV.get(1)` |

### Category: CompressedInputBusUXV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusUXV` | `ItemList.CompressedInputBusUXV.get(1)` |

### Category: CompressedInputBusZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedInputBusZPM` | `ItemList.CompressedInputBusZPM.get(1)` |

### Category: CompressedOutputBusLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusLuV` | `ItemList.CompressedOutputBusLuV.get(1)` |

### Category: CompressedOutputBusUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUEV` | `ItemList.CompressedOutputBusUEV.get(1)` |

### Category: CompressedOutputBusUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUHV` | `ItemList.CompressedOutputBusUHV.get(1)` |

### Category: CompressedOutputBusUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUIV` | `ItemList.CompressedOutputBusUIV.get(1)` |

### Category: CompressedOutputBusUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUMV` | `ItemList.CompressedOutputBusUMV.get(1)` |

### Category: CompressedOutputBusUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUV` | `ItemList.CompressedOutputBusUV.get(1)` |

### Category: CompressedOutputBusUXV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusUXV` | `ItemList.CompressedOutputBusUXV.get(1)` |

### Category: CompressedOutputBusZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressedOutputBusZPM` | `ItemList.CompressedOutputBusZPM.get(1)` |

### Category: Compressor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Compressor_Casing` | `ItemList.Compressor_Casing.get(1)` |
| `Compressor_Pipe_Casing` | `ItemList.Compressor_Pipe_Casing.get(1)` |

### Category: CompressorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorLuV` | `ItemList.CompressorLuV.get(1)` |

### Category: CompressorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorUEV` | `ItemList.CompressorUEV.get(1)` |

### Category: CompressorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorUHV` | `ItemList.CompressorUHV.get(1)` |

### Category: CompressorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorUIV` | `ItemList.CompressorUIV.get(1)` |

### Category: CompressorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorUMV` | `ItemList.CompressorUMV.get(1)` |

### Category: CompressorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorUV` | `ItemList.CompressorUV.get(1)` |

### Category: CompressorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CompressorZPM` | `ItemList.CompressorZPM.get(1)` |

### Category: ComputationalMatrixNanochipCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `ComputationalMatrixNanochipCasing` | `ItemList.ComputationalMatrixNanochipCasing.get(1)` |

### Category: ConcreteBackfiller1

| 枚举键值 | 获取代码 |
|---------|---------|
| `ConcreteBackfiller1` | `ItemList.ConcreteBackfiller1.get(1)` |

### Category: ConcreteBackfiller2

| 枚举键值 | 获取代码 |
|---------|---------|
| `ConcreteBackfiller2` | `ItemList.ConcreteBackfiller2.get(1)` |

### Category: ControllerCircuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `ControllerCircuit` | `ItemList.ControllerCircuit.get(1)` |

### Category: Conveyor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Conveyor_Module_EV` | `ItemList.Conveyor_Module_EV.get(1)` |
| `Conveyor_Module_HV` | `ItemList.Conveyor_Module_HV.get(1)` |
| `Conveyor_Module_IV` | `ItemList.Conveyor_Module_IV.get(1)` |
| `Conveyor_Module_LV` | `ItemList.Conveyor_Module_LV.get(1)` |
| `Conveyor_Module_LuV` | `ItemList.Conveyor_Module_LuV.get(1)` |
| `Conveyor_Module_MAX` | `ItemList.Conveyor_Module_MAX.get(1)` |
| `Conveyor_Module_MV` | `ItemList.Conveyor_Module_MV.get(1)` |
| `Conveyor_Module_UEV` | `ItemList.Conveyor_Module_UEV.get(1)` |
| `Conveyor_Module_UHV` | `ItemList.Conveyor_Module_UHV.get(1)` |
| `Conveyor_Module_UIV` | `ItemList.Conveyor_Module_UIV.get(1)` |
| `Conveyor_Module_UMV` | `ItemList.Conveyor_Module_UMV.get(1)` |
| `Conveyor_Module_UV` | `ItemList.Conveyor_Module_UV.get(1)` |
| `Conveyor_Module_UXV` | `ItemList.Conveyor_Module_UXV.get(1)` |
| `Conveyor_Module_ZPM` | `ItemList.Conveyor_Module_ZPM.get(1)` |

### Category: Coolant

| 枚举键值 | 获取代码 |
|---------|---------|
| `Coolant_Duct_Casing` | `ItemList.Coolant_Duct_Casing.get(1)` |

### Category: Cover

| 枚举键值 | 获取代码 |
|---------|---------|
| `Cover_ActivityDetector` | `ItemList.Cover_ActivityDetector.get(1)` |
| `Cover_AdvancedRedstoneReceiver` | `ItemList.Cover_AdvancedRedstoneReceiver.get(1)` |
| `Cover_AdvancedRedstoneReceiverInternal` | `ItemList.Cover_AdvancedRedstoneReceiverInternal.get(1)` |
| `Cover_AdvancedRedstoneTransmitter` | `ItemList.Cover_AdvancedRedstoneTransmitter.get(1)` |
| `Cover_AdvancedRedstoneTransmitterInternal` | `ItemList.Cover_AdvancedRedstoneTransmitterInternal.get(1)` |
| `Cover_Chest_Advanced` | `ItemList.Cover_Chest_Advanced.get(1)` |
| `Cover_Chest_Basic` | `ItemList.Cover_Chest_Basic.get(1)` |
| `Cover_Chest_Good` | `ItemList.Cover_Chest_Good.get(1)` |
| `Cover_Controller` | `ItemList.Cover_Controller.get(1)` |
| `Cover_Crafting` | `ItemList.Cover_Crafting.get(1)` |
| `Cover_Drain` | `ItemList.Cover_Drain.get(1)` |
| `Cover_EnergyDetector` | `ItemList.Cover_EnergyDetector.get(1)` |
| `Cover_FluidDetector` | `ItemList.Cover_FluidDetector.get(1)` |
| `Cover_FluidLimiter` | `ItemList.Cover_FluidLimiter.get(1)` |
| `Cover_FluidStorageMonitor` | `ItemList.Cover_FluidStorageMonitor.get(1)` |
| `Cover_ItemDetector` | `ItemList.Cover_ItemDetector.get(1)` |
| `Cover_Metrics_Transmitter` | `ItemList.Cover_Metrics_Transmitter.get(1)` |
| `Cover_NeedsMaintainance` | `ItemList.Cover_NeedsMaintainance.get(1)` |
| `Cover_PlayerDetector` | `ItemList.Cover_PlayerDetector.get(1)` |
| `Cover_RedstoneReceiver` | `ItemList.Cover_RedstoneReceiver.get(1)` |
| `Cover_RedstoneTransmitter` | `ItemList.Cover_RedstoneTransmitter.get(1)` |
| `Cover_RedstoneTransmitterInternal` | `ItemList.Cover_RedstoneTransmitterInternal.get(1)` |
| `Cover_Screen` | `ItemList.Cover_Screen.get(1)` |
| `Cover_Shutter` | `ItemList.Cover_Shutter.get(1)` |
| `Cover_SolarPanel` | `ItemList.Cover_SolarPanel.get(1)` |
| `Cover_SolarPanel_8V` | `ItemList.Cover_SolarPanel_8V.get(1)` |
| `Cover_SolarPanel_EV` | `ItemList.Cover_SolarPanel_EV.get(1)` |
| `Cover_SolarPanel_HV` | `ItemList.Cover_SolarPanel_HV.get(1)` |
| `Cover_SolarPanel_IV` | `ItemList.Cover_SolarPanel_IV.get(1)` |
| `Cover_SolarPanel_LV` | `ItemList.Cover_SolarPanel_LV.get(1)` |
| `Cover_SolarPanel_LuV` | `ItemList.Cover_SolarPanel_LuV.get(1)` |
| `Cover_SolarPanel_MV` | `ItemList.Cover_SolarPanel_MV.get(1)` |
| `Cover_SolarPanel_UEV` | `ItemList.Cover_SolarPanel_UEV.get(1)` |
| `Cover_SolarPanel_UHV` | `ItemList.Cover_SolarPanel_UHV.get(1)` |
| `Cover_SolarPanel_UIV` | `ItemList.Cover_SolarPanel_UIV.get(1)` |
| `Cover_SolarPanel_UV` | `ItemList.Cover_SolarPanel_UV.get(1)` |
| `Cover_SolarPanel_ZPM` | `ItemList.Cover_SolarPanel_ZPM.get(1)` |
| `Cover_WirelessActivityDetector` | `ItemList.Cover_WirelessActivityDetector.get(1)` |
| `Cover_WirelessController` | `ItemList.Cover_WirelessController.get(1)` |
| `Cover_WirelessFluidDetector` | `ItemList.Cover_WirelessFluidDetector.get(1)` |
| `Cover_WirelessItemDetector` | `ItemList.Cover_WirelessItemDetector.get(1)` |
| `Cover_WirelessNeedsMaintainance` | `ItemList.Cover_WirelessNeedsMaintainance.get(1)` |
| `Cover_Wireless_Energy_Debug` | `ItemList.Cover_Wireless_Energy_Debug.get(1)` |
| `Cover_Wireless_Energy_EV` | `ItemList.Cover_Wireless_Energy_EV.get(1)` |
| `Cover_Wireless_Energy_EV` | `ItemList.Cover_Wireless_Energy_EV.get(1)` |
| `Cover_Wireless_Energy_HV` | `ItemList.Cover_Wireless_Energy_HV.get(1)` |
| `Cover_Wireless_Energy_IV` | `ItemList.Cover_Wireless_Energy_IV.get(1)` |
| `Cover_Wireless_Energy_LV` | `ItemList.Cover_Wireless_Energy_LV.get(1)` |
| `Cover_Wireless_Energy_LuV` | `ItemList.Cover_Wireless_Energy_LuV.get(1)` |
| `Cover_Wireless_Energy_MAX` | `ItemList.Cover_Wireless_Energy_MAX.get(1)` |
| `Cover_Wireless_Energy_MV` | `ItemList.Cover_Wireless_Energy_MV.get(1)` |
| `Cover_Wireless_Energy_UEV` | `ItemList.Cover_Wireless_Energy_UEV.get(1)` |
| `Cover_Wireless_Energy_UHV` | `ItemList.Cover_Wireless_Energy_UHV.get(1)` |
| `Cover_Wireless_Energy_UIV` | `ItemList.Cover_Wireless_Energy_UIV.get(1)` |
| `Cover_Wireless_Energy_UMV` | `ItemList.Cover_Wireless_Energy_UMV.get(1)` |
| `Cover_Wireless_Energy_UMV` | `ItemList.Cover_Wireless_Energy_UMV.get(1)` |
| `Cover_Wireless_Energy_UV` | `ItemList.Cover_Wireless_Energy_UV.get(1)` |
| `Cover_Wireless_Energy_UV` | `ItemList.Cover_Wireless_Energy_UV.get(1)` |
| `Cover_Wireless_Energy_UXV` | `ItemList.Cover_Wireless_Energy_UXV.get(1)` |
| `Cover_Wireless_Energy_ZPM` | `ItemList.Cover_Wireless_Energy_ZPM.get(1)` |

### Category: Credit

| 枚举键值 | 获取代码 |
|---------|---------|
| `Credit_Copper` | `ItemList.Credit_Copper.get(1)` |
| `Credit_Gold` | `ItemList.Credit_Gold.get(1)` |
| `Credit_Greg_Copper` | `ItemList.Credit_Greg_Copper.get(1)` |
| `Credit_Greg_Cupronickel` | `ItemList.Credit_Greg_Cupronickel.get(1)` |
| `Credit_Greg_Gold` | `ItemList.Credit_Greg_Gold.get(1)` |
| `Credit_Greg_Naquadah` | `ItemList.Credit_Greg_Naquadah.get(1)` |
| `Credit_Greg_Neutronium` | `ItemList.Credit_Greg_Neutronium.get(1)` |
| `Credit_Greg_Osmium` | `ItemList.Credit_Greg_Osmium.get(1)` |
| `Credit_Greg_Platinum` | `ItemList.Credit_Greg_Platinum.get(1)` |
| `Credit_Greg_Silver` | `ItemList.Credit_Greg_Silver.get(1)` |
| `Credit_Iron` | `ItemList.Credit_Iron.get(1)` |
| `Credit_Osmium` | `ItemList.Credit_Osmium.get(1)` |
| `Credit_Platinum` | `ItemList.Credit_Platinum.get(1)` |
| `Credit_Silver` | `ItemList.Credit_Silver.get(1)` |

### Category: Crop

| 枚举键值 | 获取代码 |
|---------|---------|
| `Crop_Drop_Argentia` | `ItemList.Crop_Drop_Argentia.get(1)` |
| `Crop_Drop_Aurelia` | `ItemList.Crop_Drop_Aurelia.get(1)` |
| `Crop_Drop_Bauxite` | `ItemList.Crop_Drop_Bauxite.get(1)` |
| `Crop_Drop_BobsYerUncleRanks` | `ItemList.Crop_Drop_BobsYerUncleRanks.get(1)` |
| `Crop_Drop_Chilly` | `ItemList.Crop_Drop_Chilly.get(1)` |
| `Crop_Drop_Coppon` | `ItemList.Crop_Drop_Coppon.get(1)` |
| `Crop_Drop_Cucumber` | `ItemList.Crop_Drop_Cucumber.get(1)` |
| `Crop_Drop_Ferru` | `ItemList.Crop_Drop_Ferru.get(1)` |
| `Crop_Drop_Grapes` | `ItemList.Crop_Drop_Grapes.get(1)` |
| `Crop_Drop_Ilmenite` | `ItemList.Crop_Drop_Ilmenite.get(1)` |
| `Crop_Drop_Indigo` | `ItemList.Crop_Drop_Indigo.get(1)` |
| `Crop_Drop_Iridium` | `ItemList.Crop_Drop_Iridium.get(1)` |
| `Crop_Drop_Lemon` | `ItemList.Crop_Drop_Lemon.get(1)` |
| `Crop_Drop_MTomato` | `ItemList.Crop_Drop_MTomato.get(1)` |
| `Crop_Drop_Manganese` | `ItemList.Crop_Drop_Manganese.get(1)` |
| `Crop_Drop_Mica` | `ItemList.Crop_Drop_Mica.get(1)` |
| `Crop_Drop_MilkWart` | `ItemList.Crop_Drop_MilkWart.get(1)` |
| `Crop_Drop_Naquadah` | `ItemList.Crop_Drop_Naquadah.get(1)` |
| `Crop_Drop_Nickel` | `ItemList.Crop_Drop_Nickel.get(1)` |
| `Crop_Drop_OilBerry` | `ItemList.Crop_Drop_OilBerry.get(1)` |
| `Crop_Drop_Onion` | `ItemList.Crop_Drop_Onion.get(1)` |
| `Crop_Drop_Osmium` | `ItemList.Crop_Drop_Osmium.get(1)` |
| `Crop_Drop_Pitchblende` | `ItemList.Crop_Drop_Pitchblende.get(1)` |
| `Crop_Drop_Platinum` | `ItemList.Crop_Drop_Platinum.get(1)` |
| `Crop_Drop_Plumbilia` | `ItemList.Crop_Drop_Plumbilia.get(1)` |
| `Crop_Drop_Rape` | `ItemList.Crop_Drop_Rape.get(1)` |
| `Crop_Drop_Scheelite` | `ItemList.Crop_Drop_Scheelite.get(1)` |
| `Crop_Drop_TeaLeaf` | `ItemList.Crop_Drop_TeaLeaf.get(1)` |
| `Crop_Drop_Thorium` | `ItemList.Crop_Drop_Thorium.get(1)` |
| `Crop_Drop_Tine` | `ItemList.Crop_Drop_Tine.get(1)` |
| `Crop_Drop_Tomato` | `ItemList.Crop_Drop_Tomato.get(1)` |
| `Crop_Drop_UUABerry` | `ItemList.Crop_Drop_UUABerry.get(1)` |
| `Crop_Drop_UUMBerry` | `ItemList.Crop_Drop_UUMBerry.get(1)` |
| `Crop_Drop_Uraninite` | `ItemList.Crop_Drop_Uraninite.get(1)` |
| `Crop_Drop_Zinc` | `ItemList.Crop_Drop_Zinc.get(1)` |

### Category: CuringOven

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuringOven` | `ItemList.CuringOven.get(1)` |

### Category: CuttingMachineLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineLuV` | `ItemList.CuttingMachineLuV.get(1)` |

### Category: CuttingMachineUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineUEV` | `ItemList.CuttingMachineUEV.get(1)` |

### Category: CuttingMachineUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineUHV` | `ItemList.CuttingMachineUHV.get(1)` |

### Category: CuttingMachineUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineUIV` | `ItemList.CuttingMachineUIV.get(1)` |

### Category: CuttingMachineUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineUMV` | `ItemList.CuttingMachineUMV.get(1)` |

### Category: CuttingMachineUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineUV` | `ItemList.CuttingMachineUV.get(1)` |

### Category: CuttingMachineZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `CuttingMachineZPM` | `ItemList.CuttingMachineZPM.get(1)` |

### Category: Debug

| 枚举键值 | 获取代码 |
|---------|---------|
| `Debug_Fluid_Tank` | `ItemList.Debug_Fluid_Tank.get(1)` |

### Category: DebugEnergyHatch

| 枚举键值 | 获取代码 |
|---------|---------|
| `DebugEnergyHatch` | `ItemList.DebugEnergyHatch.get(1)` |

### Category: DecayWarehouse

| 枚举键值 | 获取代码 |
|---------|---------|
| `DecayWarehouse` | `ItemList.DecayWarehouse.get(1)` |

### Category: DepletedRodExcitedPlutonium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedPlutonium` | `ItemList.DepletedRodExcitedPlutonium.get(1)` |

### Category: DepletedRodExcitedPlutonium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedPlutonium2` | `ItemList.DepletedRodExcitedPlutonium2.get(1)` |

### Category: DepletedRodExcitedPlutonium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedPlutonium4` | `ItemList.DepletedRodExcitedPlutonium4.get(1)` |

### Category: DepletedRodExcitedUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedUranium` | `ItemList.DepletedRodExcitedUranium.get(1)` |

### Category: DepletedRodExcitedUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedUranium2` | `ItemList.DepletedRodExcitedUranium2.get(1)` |

### Category: DepletedRodExcitedUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodExcitedUranium4` | `ItemList.DepletedRodExcitedUranium4.get(1)` |

### Category: DepletedRodGlowstone

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodGlowstone` | `ItemList.DepletedRodGlowstone.get(1)` |

### Category: DepletedRodHighDensityPlutonium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityPlutonium` | `ItemList.DepletedRodHighDensityPlutonium.get(1)` |

### Category: DepletedRodHighDensityPlutonium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityPlutonium2` | `ItemList.DepletedRodHighDensityPlutonium2.get(1)` |

### Category: DepletedRodHighDensityPlutonium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityPlutonium4` | `ItemList.DepletedRodHighDensityPlutonium4.get(1)` |

### Category: DepletedRodHighDensityUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityUranium` | `ItemList.DepletedRodHighDensityUranium.get(1)` |

### Category: DepletedRodHighDensityUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityUranium2` | `ItemList.DepletedRodHighDensityUranium2.get(1)` |

### Category: DepletedRodHighDensityUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodHighDensityUranium4` | `ItemList.DepletedRodHighDensityUranium4.get(1)` |

### Category: DepletedRodLithium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodLithium` | `ItemList.DepletedRodLithium.get(1)` |

### Category: DepletedRodMOX

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodMOX` | `ItemList.DepletedRodMOX.get(1)` |

### Category: DepletedRodMOX2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodMOX2` | `ItemList.DepletedRodMOX2.get(1)` |

### Category: DepletedRodMOX4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodMOX4` | `ItemList.DepletedRodMOX4.get(1)` |

### Category: DepletedRodNaquadah

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadah` | `ItemList.DepletedRodNaquadah.get(1)` |

### Category: DepletedRodNaquadah2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadah2` | `ItemList.DepletedRodNaquadah2.get(1)` |

### Category: DepletedRodNaquadah32

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadah32` | `ItemList.DepletedRodNaquadah32.get(1)` |

### Category: DepletedRodNaquadah4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadah4` | `ItemList.DepletedRodNaquadah4.get(1)` |

### Category: DepletedRodNaquadria

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadria` | `ItemList.DepletedRodNaquadria.get(1)` |

### Category: DepletedRodNaquadria2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadria2` | `ItemList.DepletedRodNaquadria2.get(1)` |

### Category: DepletedRodNaquadria4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodNaquadria4` | `ItemList.DepletedRodNaquadria4.get(1)` |

### Category: DepletedRodThorium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodThorium` | `ItemList.DepletedRodThorium.get(1)` |

### Category: DepletedRodThorium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodThorium2` | `ItemList.DepletedRodThorium2.get(1)` |

### Category: DepletedRodThorium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodThorium4` | `ItemList.DepletedRodThorium4.get(1)` |

### Category: DepletedRodTiberium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodTiberium` | `ItemList.DepletedRodTiberium.get(1)` |

### Category: DepletedRodTiberium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodTiberium2` | `ItemList.DepletedRodTiberium2.get(1)` |

### Category: DepletedRodTiberium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodTiberium4` | `ItemList.DepletedRodTiberium4.get(1)` |

### Category: DepletedRodUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodUranium` | `ItemList.DepletedRodUranium.get(1)` |

### Category: DepletedRodUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodUranium2` | `ItemList.DepletedRodUranium2.get(1)` |

### Category: DepletedRodUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `DepletedRodUranium4` | `ItemList.DepletedRodUranium4.get(1)` |

### Category: Display

| 枚举键值 | 获取代码 |
|---------|---------|
| `Display_Fluid` | `ItemList.Display_Fluid.get(1)` |
| `Display_ITS_FREE` | `ItemList.Display_ITS_FREE.get(1)` |

### Category: Distillation

| 枚举键值 | 获取代码 |
|---------|---------|
| `Distillation_Tower` | `ItemList.Distillation_Tower.get(1)` |

### Category: DistilleryLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryLuV` | `ItemList.DistilleryLuV.get(1)` |

### Category: DistilleryUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryUEV` | `ItemList.DistilleryUEV.get(1)` |

### Category: DistilleryUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryUHV` | `ItemList.DistilleryUHV.get(1)` |

### Category: DistilleryUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryUIV` | `ItemList.DistilleryUIV.get(1)` |

### Category: DistilleryUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryUMV` | `ItemList.DistilleryUMV.get(1)` |

### Category: DistilleryUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryUV` | `ItemList.DistilleryUV.get(1)` |

### Category: DistilleryZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `DistilleryZPM` | `ItemList.DistilleryZPM.get(1)` |

### Category: DroneRemoteInterface

| 枚举键值 | 获取代码 |
|---------|---------|
| `DroneRemoteInterface` | `ItemList.DroneRemoteInterface.get(1)` |

### Category: Duct

| 枚举键值 | 获取代码 |
|---------|---------|
| `Duct_Tape` | `ItemList.Duct_Tape.get(1)` |

### Category: Dye

| 枚举键值 | 获取代码 |
|---------|---------|
| `Dye_Bonemeal` | `ItemList.Dye_Bonemeal.get(1)` |
| `Dye_Cocoa` | `ItemList.Dye_Cocoa.get(1)` |
| `Dye_Indigo` | `ItemList.Dye_Indigo.get(1)` |
| `Dye_SquidInk` | `ItemList.Dye_SquidInk.get(1)` |

### Category: DysonSwarmControlCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmControlCasing` | `ItemList.DysonSwarmControlCasing.get(1)` |

### Category: DysonSwarmControlPrimary

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmControlPrimary` | `ItemList.DysonSwarmControlPrimary.get(1)` |

### Category: DysonSwarmControlSecondary

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmControlSecondary` | `ItemList.DysonSwarmControlSecondary.get(1)` |

### Category: DysonSwarmControlToroid

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmControlToroid` | `ItemList.DysonSwarmControlToroid.get(1)` |

### Category: DysonSwarmController

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmController` | `ItemList.DysonSwarmController.get(1)` |

### Category: DysonSwarmDeploymentUnitCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmDeploymentUnitCasing` | `ItemList.DysonSwarmDeploymentUnitCasing.get(1)` |

### Category: DysonSwarmDeploymentUnitCore

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmDeploymentUnitCore` | `ItemList.DysonSwarmDeploymentUnitCore.get(1)` |

### Category: DysonSwarmDeploymentUnitMagnet

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmDeploymentUnitMagnet` | `ItemList.DysonSwarmDeploymentUnitMagnet.get(1)` |

### Category: DysonSwarmModule

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmModule` | `ItemList.DysonSwarmModule.get(1)` |

### Category: DysonSwarmReceiverCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmReceiverCasing` | `ItemList.DysonSwarmReceiverCasing.get(1)` |

### Category: DysonSwarmReceiverDish

| 枚举键值 | 获取代码 |
|---------|---------|
| `DysonSwarmReceiverDish` | `ItemList.DysonSwarmReceiverDish.get(1)` |

### Category: EV

| 枚举键值 | 获取代码 |
|---------|---------|
| `EV_Coil` | `ItemList.EV_Coil.get(1)` |

### Category: Efficient

| 枚举键值 | 获取代码 |
|---------|---------|
| `Efficient_Overclocking_ExoFoundry` | `ItemList.Efficient_Overclocking_ExoFoundry.get(1)` |

### Category: Electric

| 枚举键值 | 获取代码 |
|---------|---------|
| `Electric_Motor_EV` | `ItemList.Electric_Motor_EV.get(1)` |
| `Electric_Motor_HV` | `ItemList.Electric_Motor_HV.get(1)` |
| `Electric_Motor_IV` | `ItemList.Electric_Motor_IV.get(1)` |
| `Electric_Motor_LV` | `ItemList.Electric_Motor_LV.get(1)` |
| `Electric_Motor_LuV` | `ItemList.Electric_Motor_LuV.get(1)` |
| `Electric_Motor_MAX` | `ItemList.Electric_Motor_MAX.get(1)` |
| `Electric_Motor_MV` | `ItemList.Electric_Motor_MV.get(1)` |
| `Electric_Motor_UEV` | `ItemList.Electric_Motor_UEV.get(1)` |
| `Electric_Motor_UHV` | `ItemList.Electric_Motor_UHV.get(1)` |
| `Electric_Motor_UIV` | `ItemList.Electric_Motor_UIV.get(1)` |
| `Electric_Motor_UMV` | `ItemList.Electric_Motor_UMV.get(1)` |
| `Electric_Motor_UV` | `ItemList.Electric_Motor_UV.get(1)` |
| `Electric_Motor_UXV` | `ItemList.Electric_Motor_UXV.get(1)` |
| `Electric_Motor_ZPM` | `ItemList.Electric_Motor_ZPM.get(1)` |
| `Electric_Piston_EV` | `ItemList.Electric_Piston_EV.get(1)` |
| `Electric_Piston_HV` | `ItemList.Electric_Piston_HV.get(1)` |
| `Electric_Piston_IV` | `ItemList.Electric_Piston_IV.get(1)` |
| `Electric_Piston_LV` | `ItemList.Electric_Piston_LV.get(1)` |
| `Electric_Piston_LuV` | `ItemList.Electric_Piston_LuV.get(1)` |
| `Electric_Piston_MAX` | `ItemList.Electric_Piston_MAX.get(1)` |
| `Electric_Piston_MV` | `ItemList.Electric_Piston_MV.get(1)` |
| `Electric_Piston_UEV` | `ItemList.Electric_Piston_UEV.get(1)` |
| `Electric_Piston_UHV` | `ItemList.Electric_Piston_UHV.get(1)` |
| `Electric_Piston_UIV` | `ItemList.Electric_Piston_UIV.get(1)` |
| `Electric_Piston_UMV` | `ItemList.Electric_Piston_UMV.get(1)` |
| `Electric_Piston_UV` | `ItemList.Electric_Piston_UV.get(1)` |
| `Electric_Piston_UXV` | `ItemList.Electric_Piston_UXV.get(1)` |
| `Electric_Piston_ZPM` | `ItemList.Electric_Piston_ZPM.get(1)` |
| `Electric_Pump_EV` | `ItemList.Electric_Pump_EV.get(1)` |
| `Electric_Pump_HV` | `ItemList.Electric_Pump_HV.get(1)` |
| `Electric_Pump_IV` | `ItemList.Electric_Pump_IV.get(1)` |
| `Electric_Pump_LV` | `ItemList.Electric_Pump_LV.get(1)` |
| `Electric_Pump_LuV` | `ItemList.Electric_Pump_LuV.get(1)` |
| `Electric_Pump_MAX` | `ItemList.Electric_Pump_MAX.get(1)` |
| `Electric_Pump_MV` | `ItemList.Electric_Pump_MV.get(1)` |
| `Electric_Pump_UEV` | `ItemList.Electric_Pump_UEV.get(1)` |
| `Electric_Pump_UHV` | `ItemList.Electric_Pump_UHV.get(1)` |
| `Electric_Pump_UIV` | `ItemList.Electric_Pump_UIV.get(1)` |
| `Electric_Pump_UMV` | `ItemList.Electric_Pump_UMV.get(1)` |
| `Electric_Pump_UV` | `ItemList.Electric_Pump_UV.get(1)` |
| `Electric_Pump_UXV` | `ItemList.Electric_Pump_UXV.get(1)` |
| `Electric_Pump_ZPM` | `ItemList.Electric_Pump_ZPM.get(1)` |

### Category: ElectricFurnaceLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceLuV` | `ItemList.ElectricFurnaceLuV.get(1)` |

### Category: ElectricFurnaceUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceUEV` | `ItemList.ElectricFurnaceUEV.get(1)` |

### Category: ElectricFurnaceUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceUHV` | `ItemList.ElectricFurnaceUHV.get(1)` |

### Category: ElectricFurnaceUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceUIV` | `ItemList.ElectricFurnaceUIV.get(1)` |

### Category: ElectricFurnaceUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceUMV` | `ItemList.ElectricFurnaceUMV.get(1)` |

### Category: ElectricFurnaceUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceUV` | `ItemList.ElectricFurnaceUV.get(1)` |

### Category: ElectricFurnaceZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricFurnaceZPM` | `ItemList.ElectricFurnaceZPM.get(1)` |

### Category: ElectricOvenLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenLuV` | `ItemList.ElectricOvenLuV.get(1)` |

### Category: ElectricOvenUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenUEV` | `ItemList.ElectricOvenUEV.get(1)` |

### Category: ElectricOvenUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenUHV` | `ItemList.ElectricOvenUHV.get(1)` |

### Category: ElectricOvenUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenUIV` | `ItemList.ElectricOvenUIV.get(1)` |

### Category: ElectricOvenUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenUMV` | `ItemList.ElectricOvenUMV.get(1)` |

### Category: ElectricOvenUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenUV` | `ItemList.ElectricOvenUV.get(1)` |

### Category: ElectricOvenZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectricOvenZPM` | `ItemList.ElectricOvenZPM.get(1)` |

### Category: ElectrolyzerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerLuV` | `ItemList.ElectrolyzerLuV.get(1)` |

### Category: ElectrolyzerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerUEV` | `ItemList.ElectrolyzerUEV.get(1)` |

### Category: ElectrolyzerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerUHV` | `ItemList.ElectrolyzerUHV.get(1)` |

### Category: ElectrolyzerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerUIV` | `ItemList.ElectrolyzerUIV.get(1)` |

### Category: ElectrolyzerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerUMV` | `ItemList.ElectrolyzerUMV.get(1)` |

### Category: ElectrolyzerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerUV` | `ItemList.ElectrolyzerUV.get(1)` |

### Category: ElectrolyzerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectrolyzerZPM` | `ItemList.ElectrolyzerZPM.get(1)` |

### Category: Electromagnet

| 枚举键值 | 获取代码 |
|---------|---------|
| `Electromagnet_Iron` | `ItemList.Electromagnet_Iron.get(1)` |
| `Electromagnet_Neodymium` | `ItemList.Electromagnet_Neodymium.get(1)` |
| `Electromagnet_Samarium` | `ItemList.Electromagnet_Samarium.get(1)` |
| `Electromagnet_Steel` | `ItemList.Electromagnet_Steel.get(1)` |
| `Electromagnet_Tengam` | `ItemList.Electromagnet_Tengam.get(1)` |

### Category: ElectromagneticSeparatorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorLuV` | `ItemList.ElectromagneticSeparatorLuV.get(1)` |

### Category: ElectromagneticSeparatorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorUEV` | `ItemList.ElectromagneticSeparatorUEV.get(1)` |

### Category: ElectromagneticSeparatorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorUHV` | `ItemList.ElectromagneticSeparatorUHV.get(1)` |

### Category: ElectromagneticSeparatorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorUIV` | `ItemList.ElectromagneticSeparatorUIV.get(1)` |

### Category: ElectromagneticSeparatorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorUMV` | `ItemList.ElectromagneticSeparatorUMV.get(1)` |

### Category: ElectromagneticSeparatorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorUV` | `ItemList.ElectromagneticSeparatorUV.get(1)` |

### Category: ElectromagneticSeparatorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectromagneticSeparatorZPM` | `ItemList.ElectromagneticSeparatorZPM.get(1)` |

### Category: ElectronicsLump

| 枚举键值 | 获取代码 |
|---------|---------|
| `ElectronicsLump` | `ItemList.ElectronicsLump.get(1)` |

### Category: Emitter

| 枚举键值 | 获取代码 |
|---------|---------|
| `Emitter_EV` | `ItemList.Emitter_EV.get(1)` |
| `Emitter_HV` | `ItemList.Emitter_HV.get(1)` |
| `Emitter_IV` | `ItemList.Emitter_IV.get(1)` |
| `Emitter_LV` | `ItemList.Emitter_LV.get(1)` |
| `Emitter_LuV` | `ItemList.Emitter_LuV.get(1)` |
| `Emitter_MAX` | `ItemList.Emitter_MAX.get(1)` |
| `Emitter_MV` | `ItemList.Emitter_MV.get(1)` |
| `Emitter_UEV` | `ItemList.Emitter_UEV.get(1)` |
| `Emitter_UHV` | `ItemList.Emitter_UHV.get(1)` |
| `Emitter_UIV` | `ItemList.Emitter_UIV.get(1)` |
| `Emitter_UMV` | `ItemList.Emitter_UMV.get(1)` |
| `Emitter_UV` | `ItemList.Emitter_UV.get(1)` |
| `Emitter_UXV` | `ItemList.Emitter_UXV.get(1)` |
| `Emitter_ZPM` | `ItemList.Emitter_ZPM.get(1)` |

### Category: Empty

| 枚举键值 | 获取代码 |
|---------|---------|
| `Empty_Board_Basic` | `ItemList.Empty_Board_Basic.get(1)` |
| `Empty_Board_Elite` | `ItemList.Empty_Board_Elite.get(1)` |

### Category: EnergisedTesseract

| 枚举键值 | 获取代码 |
|---------|---------|
| `EnergisedTesseract` | `ItemList.EnergisedTesseract.get(1)` |

### Category: Energy

| 枚举键值 | 获取代码 |
|---------|---------|
| `Energy_Cluster` | `ItemList.Energy_Cluster.get(1)` |
| `Energy_LapotronicOrb` | `ItemList.Energy_LapotronicOrb.get(1)` |
| `Energy_LapotronicOrb2` | `ItemList.Energy_LapotronicOrb2.get(1)` |
| `Energy_Module` | `ItemList.Energy_Module.get(1)` |

### Category: EnhancedCircuitBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `EnhancedCircuitBoard` | `ItemList.EnhancedCircuitBoard.get(1)` |

### Category: EntropicProcessor

| 枚举键值 | 获取代码 |
|---------|---------|
| `EntropicProcessor` | `ItemList.EntropicProcessor.get(1)` |

### Category: Extra

| 枚举键值 | 获取代码 |
|---------|---------|
| `Extra_Casting_Basins_ExoFoundry` | `ItemList.Extra_Casting_Basins_ExoFoundry.get(1)` |

### Category: ExtractorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorLuV` | `ItemList.ExtractorLuV.get(1)` |

### Category: ExtractorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorUEV` | `ItemList.ExtractorUEV.get(1)` |

### Category: ExtractorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorUHV` | `ItemList.ExtractorUHV.get(1)` |

### Category: ExtractorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorUIV` | `ItemList.ExtractorUIV.get(1)` |

### Category: ExtractorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorUMV` | `ItemList.ExtractorUMV.get(1)` |

### Category: ExtractorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorUV` | `ItemList.ExtractorUV.get(1)` |

### Category: ExtractorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtractorZPM` | `ItemList.ExtractorZPM.get(1)` |

### Category: Extreme

| 枚举键值 | 获取代码 |
|---------|---------|
| `Extreme_Density_Casing` | `ItemList.Extreme_Density_Casing.get(1)` |

### Category: ExtruderLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderLuV` | `ItemList.ExtruderLuV.get(1)` |

### Category: ExtruderUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderUEV` | `ItemList.ExtruderUEV.get(1)` |

### Category: ExtruderUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderUHV` | `ItemList.ExtruderUHV.get(1)` |

### Category: ExtruderUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderUIV` | `ItemList.ExtruderUIV.get(1)` |

### Category: ExtruderUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderUMV` | `ItemList.ExtruderUMV.get(1)` |

### Category: ExtruderUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderUV` | `ItemList.ExtruderUV.get(1)` |

### Category: ExtruderZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ExtruderZPM` | `ItemList.ExtruderZPM.get(1)` |

### Category: FR

| 枚举键值 | 获取代码 |
|---------|---------|
| `FR_Bee_Drone` | `ItemList.FR_Bee_Drone.get(1)` |
| `FR_Bee_Princess` | `ItemList.FR_Bee_Princess.get(1)` |
| `FR_Bee_Queen` | `ItemList.FR_Bee_Queen.get(1)` |
| `FR_Butterfly` | `ItemList.FR_Butterfly.get(1)` |
| `FR_Casing_Hardened` | `ItemList.FR_Casing_Hardened.get(1)` |
| `FR_Casing_Impregnated` | `ItemList.FR_Casing_Impregnated.get(1)` |
| `FR_Casing_Sturdy` | `ItemList.FR_Casing_Sturdy.get(1)` |
| `FR_Caterpillar` | `ItemList.FR_Caterpillar.get(1)` |
| `FR_Compost` | `ItemList.FR_Compost.get(1)` |
| `FR_Fertilizer` | `ItemList.FR_Fertilizer.get(1)` |
| `FR_Larvae` | `ItemList.FR_Larvae.get(1)` |
| `FR_Lemon` | `ItemList.FR_Lemon.get(1)` |
| `FR_Mulch` | `ItemList.FR_Mulch.get(1)` |
| `FR_PollenFertile` | `ItemList.FR_PollenFertile.get(1)` |
| `FR_RefractoryCapsule` | `ItemList.FR_RefractoryCapsule.get(1)` |
| `FR_RefractoryWax` | `ItemList.FR_RefractoryWax.get(1)` |
| `FR_Serum` | `ItemList.FR_Serum.get(1)` |
| `FR_Silk` | `ItemList.FR_Silk.get(1)` |
| `FR_Stick` | `ItemList.FR_Stick.get(1)` |
| `FR_Tree_Sapling` | `ItemList.FR_Tree_Sapling.get(1)` |
| `FR_Wax` | `ItemList.FR_Wax.get(1)` |
| `FR_WaxCapsule` | `ItemList.FR_WaxCapsule.get(1)` |

### Category: FermenterLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterLuV` | `ItemList.FermenterLuV.get(1)` |

### Category: FermenterUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterUEV` | `ItemList.FermenterUEV.get(1)` |

### Category: FermenterUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterUHV` | `ItemList.FermenterUHV.get(1)` |

### Category: FermenterUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterUIV` | `ItemList.FermenterUIV.get(1)` |

### Category: FermenterUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterUMV` | `ItemList.FermenterUMV.get(1)` |

### Category: FermenterUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterUV` | `ItemList.FermenterUV.get(1)` |

### Category: FermenterZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FermenterZPM` | `ItemList.FermenterZPM.get(1)` |

### Category: Field

| 枚举键值 | 获取代码 |
|---------|---------|
| `Field_Generator_EV` | `ItemList.Field_Generator_EV.get(1)` |
| `Field_Generator_HV` | `ItemList.Field_Generator_HV.get(1)` |
| `Field_Generator_IV` | `ItemList.Field_Generator_IV.get(1)` |
| `Field_Generator_LV` | `ItemList.Field_Generator_LV.get(1)` |
| `Field_Generator_LuV` | `ItemList.Field_Generator_LuV.get(1)` |
| `Field_Generator_MAX` | `ItemList.Field_Generator_MAX.get(1)` |
| `Field_Generator_MV` | `ItemList.Field_Generator_MV.get(1)` |
| `Field_Generator_UEV` | `ItemList.Field_Generator_UEV.get(1)` |
| `Field_Generator_UHV` | `ItemList.Field_Generator_UHV.get(1)` |
| `Field_Generator_UIV` | `ItemList.Field_Generator_UIV.get(1)` |
| `Field_Generator_UMV` | `ItemList.Field_Generator_UMV.get(1)` |
| `Field_Generator_UV` | `ItemList.Field_Generator_UV.get(1)` |
| `Field_Generator_UXV` | `ItemList.Field_Generator_UXV.get(1)` |
| `Field_Generator_ZPM` | `ItemList.Field_Generator_ZPM.get(1)` |

### Category: FieldEnergyAbsorberCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `FieldEnergyAbsorberCasing` | `ItemList.FieldEnergyAbsorberCasing.get(1)` |

### Category: Firebrick

| 枚举键值 | 获取代码 |
|---------|---------|
| `Firebrick` | `ItemList.Firebrick.get(1)` |

### Category: FirewallProjectionNanochipCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `FirewallProjectionNanochipCasing` | `ItemList.FirewallProjectionNanochipCasing.get(1)` |

### Category: FluidCannerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerLuV` | `ItemList.FluidCannerLuV.get(1)` |

### Category: FluidCannerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerUEV` | `ItemList.FluidCannerUEV.get(1)` |

### Category: FluidCannerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerUHV` | `ItemList.FluidCannerUHV.get(1)` |

### Category: FluidCannerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerUIV` | `ItemList.FluidCannerUIV.get(1)` |

### Category: FluidCannerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerUMV` | `ItemList.FluidCannerUMV.get(1)` |

### Category: FluidCannerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerUV` | `ItemList.FluidCannerUV.get(1)` |

### Category: FluidCannerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidCannerZPM` | `ItemList.FluidCannerZPM.get(1)` |

### Category: FluidExtractorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorLuV` | `ItemList.FluidExtractorLuV.get(1)` |

### Category: FluidExtractorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorUEV` | `ItemList.FluidExtractorUEV.get(1)` |

### Category: FluidExtractorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorUHV` | `ItemList.FluidExtractorUHV.get(1)` |

### Category: FluidExtractorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorUIV` | `ItemList.FluidExtractorUIV.get(1)` |

### Category: FluidExtractorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorUMV` | `ItemList.FluidExtractorUMV.get(1)` |

### Category: FluidExtractorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorUV` | `ItemList.FluidExtractorUV.get(1)` |

### Category: FluidExtractorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidExtractorZPM` | `ItemList.FluidExtractorZPM.get(1)` |

### Category: FluidFilter

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidFilter` | `ItemList.FluidFilter.get(1)` |

### Category: FluidHeaterLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterLuV` | `ItemList.FluidHeaterLuV.get(1)` |

### Category: FluidHeaterUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterUEV` | `ItemList.FluidHeaterUEV.get(1)` |

### Category: FluidHeaterUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterUHV` | `ItemList.FluidHeaterUHV.get(1)` |

### Category: FluidHeaterUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterUIV` | `ItemList.FluidHeaterUIV.get(1)` |

### Category: FluidHeaterUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterUMV` | `ItemList.FluidHeaterUMV.get(1)` |

### Category: FluidHeaterUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterUV` | `ItemList.FluidHeaterUV.get(1)` |

### Category: FluidHeaterZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidHeaterZPM` | `ItemList.FluidHeaterZPM.get(1)` |

### Category: FluidRegulator

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidRegulator_EV` | `ItemList.FluidRegulator_EV.get(1)` |
| `FluidRegulator_HV` | `ItemList.FluidRegulator_HV.get(1)` |
| `FluidRegulator_IV` | `ItemList.FluidRegulator_IV.get(1)` |
| `FluidRegulator_LV` | `ItemList.FluidRegulator_LV.get(1)` |
| `FluidRegulator_LuV` | `ItemList.FluidRegulator_LuV.get(1)` |
| `FluidRegulator_MAX` | `ItemList.FluidRegulator_MAX.get(1)` |
| `FluidRegulator_MV` | `ItemList.FluidRegulator_MV.get(1)` |
| `FluidRegulator_UEV` | `ItemList.FluidRegulator_UEV.get(1)` |
| `FluidRegulator_UHV` | `ItemList.FluidRegulator_UHV.get(1)` |
| `FluidRegulator_UIV` | `ItemList.FluidRegulator_UIV.get(1)` |
| `FluidRegulator_UMV` | `ItemList.FluidRegulator_UMV.get(1)` |
| `FluidRegulator_UV` | `ItemList.FluidRegulator_UV.get(1)` |
| `FluidRegulator_UXV` | `ItemList.FluidRegulator_UXV.get(1)` |
| `FluidRegulator_ZPM` | `ItemList.FluidRegulator_ZPM.get(1)` |

### Category: FluidSolidifierLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierLuV` | `ItemList.FluidSolidifierLuV.get(1)` |

### Category: FluidSolidifierUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierUEV` | `ItemList.FluidSolidifierUEV.get(1)` |

### Category: FluidSolidifierUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierUHV` | `ItemList.FluidSolidifierUHV.get(1)` |

### Category: FluidSolidifierUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierUIV` | `ItemList.FluidSolidifierUIV.get(1)` |

### Category: FluidSolidifierUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierUMV` | `ItemList.FluidSolidifierUMV.get(1)` |

### Category: FluidSolidifierUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierUV` | `ItemList.FluidSolidifierUV.get(1)` |

### Category: FluidSolidifierZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FluidSolidifierZPM` | `ItemList.FluidSolidifierZPM.get(1)` |

### Category: Food

| 枚举键值 | 获取代码 |
|---------|---------|
| `Food_Baked_Baguette` | `ItemList.Food_Baked_Baguette.get(1)` |
| `Food_Baked_Bread` | `ItemList.Food_Baked_Bread.get(1)` |
| `Food_Baked_Bun` | `ItemList.Food_Baked_Bun.get(1)` |
| `Food_Baked_Cake` | `ItemList.Food_Baked_Cake.get(1)` |
| `Food_Baked_Pizza_Cheese` | `ItemList.Food_Baked_Pizza_Cheese.get(1)` |
| `Food_Baked_Pizza_Meat` | `ItemList.Food_Baked_Pizza_Meat.get(1)` |
| `Food_Baked_Pizza_Veggie` | `ItemList.Food_Baked_Pizza_Veggie.get(1)` |
| `Food_Baked_Potato` | `ItemList.Food_Baked_Potato.get(1)` |
| `Food_Burger_Cheese` | `ItemList.Food_Burger_Cheese.get(1)` |
| `Food_Burger_Chum` | `ItemList.Food_Burger_Chum.get(1)` |
| `Food_Burger_Meat` | `ItemList.Food_Burger_Meat.get(1)` |
| `Food_Burger_Veggie` | `ItemList.Food_Burger_Veggie.get(1)` |
| `Food_Cheese` | `ItemList.Food_Cheese.get(1)` |
| `Food_ChiliChips` | `ItemList.Food_ChiliChips.get(1)` |
| `Food_Chum` | `ItemList.Food_Chum.get(1)` |
| `Food_Chum_On_Stick` | `ItemList.Food_Chum_On_Stick.get(1)` |
| `Food_Dough` | `ItemList.Food_Dough.get(1)` |
| `Food_Dough_Chocolate` | `ItemList.Food_Dough_Chocolate.get(1)` |
| `Food_Dough_Sugar` | `ItemList.Food_Dough_Sugar.get(1)` |
| `Food_Flat_Dough` | `ItemList.Food_Flat_Dough.get(1)` |
| `Food_Fries` | `ItemList.Food_Fries.get(1)` |
| `Food_Large_Sandwich_Bacon` | `ItemList.Food_Large_Sandwich_Bacon.get(1)` |
| `Food_Large_Sandwich_Cheese` | `ItemList.Food_Large_Sandwich_Cheese.get(1)` |
| `Food_Large_Sandwich_Steak` | `ItemList.Food_Large_Sandwich_Steak.get(1)` |
| `Food_Large_Sandwich_Veggie` | `ItemList.Food_Large_Sandwich_Veggie.get(1)` |
| `Food_Packaged_ChiliChips` | `ItemList.Food_Packaged_ChiliChips.get(1)` |
| `Food_Packaged_Fries` | `ItemList.Food_Packaged_Fries.get(1)` |
| `Food_Packaged_PotatoChips` | `ItemList.Food_Packaged_PotatoChips.get(1)` |
| `Food_Poisonous_Potato` | `ItemList.Food_Poisonous_Potato.get(1)` |
| `Food_PotatoChips` | `ItemList.Food_PotatoChips.get(1)` |
| `Food_Potato_On_Stick` | `ItemList.Food_Potato_On_Stick.get(1)` |
| `Food_Potato_On_Stick_Roasted` | `ItemList.Food_Potato_On_Stick_Roasted.get(1)` |
| `Food_Raw_Baguette` | `ItemList.Food_Raw_Baguette.get(1)` |
| `Food_Raw_Bread` | `ItemList.Food_Raw_Bread.get(1)` |
| `Food_Raw_Bun` | `ItemList.Food_Raw_Bun.get(1)` |
| `Food_Raw_Cake` | `ItemList.Food_Raw_Cake.get(1)` |
| `Food_Raw_Cookie` | `ItemList.Food_Raw_Cookie.get(1)` |
| `Food_Raw_Fries` | `ItemList.Food_Raw_Fries.get(1)` |
| `Food_Raw_Pizza_Cheese` | `ItemList.Food_Raw_Pizza_Cheese.get(1)` |
| `Food_Raw_Pizza_Meat` | `ItemList.Food_Raw_Pizza_Meat.get(1)` |
| `Food_Raw_Pizza_Veggie` | `ItemList.Food_Raw_Pizza_Veggie.get(1)` |
| `Food_Raw_Potato` | `ItemList.Food_Raw_Potato.get(1)` |
| `Food_Raw_PotatoChips` | `ItemList.Food_Raw_PotatoChips.get(1)` |
| `Food_Sandwich_Bacon` | `ItemList.Food_Sandwich_Bacon.get(1)` |
| `Food_Sandwich_Cheese` | `ItemList.Food_Sandwich_Cheese.get(1)` |
| `Food_Sandwich_Steak` | `ItemList.Food_Sandwich_Steak.get(1)` |
| `Food_Sandwich_Veggie` | `ItemList.Food_Sandwich_Veggie.get(1)` |
| `Food_Sliced_Baguette` | `ItemList.Food_Sliced_Baguette.get(1)` |
| `Food_Sliced_Baguettes` | `ItemList.Food_Sliced_Baguettes.get(1)` |
| `Food_Sliced_Bread` | `ItemList.Food_Sliced_Bread.get(1)` |
| `Food_Sliced_Breads` | `ItemList.Food_Sliced_Breads.get(1)` |
| `Food_Sliced_Bun` | `ItemList.Food_Sliced_Bun.get(1)` |
| `Food_Sliced_Buns` | `ItemList.Food_Sliced_Buns.get(1)` |
| `Food_Sliced_Cheese` | `ItemList.Food_Sliced_Cheese.get(1)` |
| `Food_Sliced_Cucumber` | `ItemList.Food_Sliced_Cucumber.get(1)` |
| `Food_Sliced_Lemon` | `ItemList.Food_Sliced_Lemon.get(1)` |
| `Food_Sliced_Onion` | `ItemList.Food_Sliced_Onion.get(1)` |
| `Food_Sliced_Tomato` | `ItemList.Food_Sliced_Tomato.get(1)` |

### Category: ForgeHammerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerLuV` | `ItemList.ForgeHammerLuV.get(1)` |

### Category: ForgeHammerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerUEV` | `ItemList.ForgeHammerUEV.get(1)` |

### Category: ForgeHammerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerUHV` | `ItemList.ForgeHammerUHV.get(1)` |

### Category: ForgeHammerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerUIV` | `ItemList.ForgeHammerUIV.get(1)` |

### Category: ForgeHammerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerUMV` | `ItemList.ForgeHammerUMV.get(1)` |

### Category: ForgeHammerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerUV` | `ItemList.ForgeHammerUV.get(1)` |

### Category: ForgeHammerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ForgeHammerZPM` | `ItemList.ForgeHammerZPM.get(1)` |

### Category: FormingPressLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressLuV` | `ItemList.FormingPressLuV.get(1)` |

### Category: FormingPressUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressUEV` | `ItemList.FormingPressUEV.get(1)` |

### Category: FormingPressUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressUHV` | `ItemList.FormingPressUHV.get(1)` |

### Category: FormingPressUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressUIV` | `ItemList.FormingPressUIV.get(1)` |

### Category: FormingPressUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressUMV` | `ItemList.FormingPressUMV.get(1)` |

### Category: FormingPressUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressUV` | `ItemList.FormingPressUV.get(1)` |

### Category: FormingPressZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `FormingPressZPM` | `ItemList.FormingPressZPM.get(1)` |

### Category: Fuel

| 枚举键值 | 获取代码 |
|---------|---------|
| `Fuel_Can_Plastic_Empty` | `ItemList.Fuel_Can_Plastic_Empty.get(1)` |
| `Fuel_Can_Plastic_Filled` | `ItemList.Fuel_Can_Plastic_Filled.get(1)` |

### Category: FusionComputer

| 枚举键值 | 获取代码 |
|---------|---------|
| `FusionComputer_LuV` | `ItemList.FusionComputer_LuV.get(1)` |
| `FusionComputer_UV` | `ItemList.FusionComputer_UV.get(1)` |
| `FusionComputer_ZPMV` | `ItemList.FusionComputer_ZPMV.get(1)` |

### Category: GalliumArsenideCrystal

| 枚举键值 | 获取代码 |
|---------|---------|
| `GalliumArsenideCrystal` | `ItemList.GalliumArsenideCrystal.get(1)` |

### Category: GalliumArsenideCrystalSmallPart

| 枚举键值 | 获取代码 |
|---------|---------|
| `GalliumArsenideCrystalSmallPart` | `ItemList.GalliumArsenideCrystalSmallPart.get(1)` |

### Category: GelledToluene

| 枚举键值 | 获取代码 |
|---------|---------|
| `GelledToluene` | `ItemList.GelledToluene.get(1)` |

### Category: Generator

| 枚举键值 | 获取代码 |
|---------|---------|
| `Generator_Diesel_HV` | `ItemList.Generator_Diesel_HV.get(1)` |
| `Generator_Diesel_LV` | `ItemList.Generator_Diesel_LV.get(1)` |
| `Generator_Diesel_MV` | `ItemList.Generator_Diesel_MV.get(1)` |
| `Generator_Gas_Turbine_EV` | `ItemList.Generator_Gas_Turbine_EV.get(1)` |
| `Generator_Gas_Turbine_HV` | `ItemList.Generator_Gas_Turbine_HV.get(1)` |
| `Generator_Gas_Turbine_IV` | `ItemList.Generator_Gas_Turbine_IV.get(1)` |
| `Generator_Gas_Turbine_LV` | `ItemList.Generator_Gas_Turbine_LV.get(1)` |
| `Generator_Gas_Turbine_MV` | `ItemList.Generator_Gas_Turbine_MV.get(1)` |
| `Generator_Naquadah_Mark_I` | `ItemList.Generator_Naquadah_Mark_I.get(1)` |
| `Generator_Naquadah_Mark_II` | `ItemList.Generator_Naquadah_Mark_II.get(1)` |
| `Generator_Naquadah_Mark_III` | `ItemList.Generator_Naquadah_Mark_III.get(1)` |
| `Generator_Naquadah_Mark_IV` | `ItemList.Generator_Naquadah_Mark_IV.get(1)` |
| `Generator_Naquadah_Mark_V` | `ItemList.Generator_Naquadah_Mark_V.get(1)` |
| `Generator_Plasma_EV` | `ItemList.Generator_Plasma_EV.get(1)` |
| `Generator_Plasma_IV` | `ItemList.Generator_Plasma_IV.get(1)` |
| `Generator_Plasma_LuV` | `ItemList.Generator_Plasma_LuV.get(1)` |
| `Generator_Plasma_UEV` | `ItemList.Generator_Plasma_UEV.get(1)` |
| `Generator_Plasma_UHV` | `ItemList.Generator_Plasma_UHV.get(1)` |
| `Generator_Plasma_UIV` | `ItemList.Generator_Plasma_UIV.get(1)` |
| `Generator_Plasma_UMV` | `ItemList.Generator_Plasma_UMV.get(1)` |
| `Generator_Plasma_UV` | `ItemList.Generator_Plasma_UV.get(1)` |
| `Generator_Plasma_ZPMV` | `ItemList.Generator_Plasma_ZPMV.get(1)` |
| `Generator_Steam_Turbine_HV` | `ItemList.Generator_Steam_Turbine_HV.get(1)` |
| `Generator_Steam_Turbine_LV` | `ItemList.Generator_Steam_Turbine_LV.get(1)` |
| `Generator_Steam_Turbine_MV` | `ItemList.Generator_Steam_Turbine_MV.get(1)` |

### Category: GigaChad

| 枚举键值 | 获取代码 |
|---------|---------|
| `GigaChad` | `ItemList.GigaChad.get(1)` |

### Category: Glass

| 枚举键值 | 获取代码 |
|---------|---------|
| `Glass_ExoFoundry` | `ItemList.Glass_ExoFoundry.get(1)` |

### Category: GlassOmniPurposeInfinityFused

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassOmniPurposeInfinityFused` | `ItemList.GlassOmniPurposeInfinityFused.get(1)` |

### Category: GlassPHResistant

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassPHResistant` | `ItemList.GlassPHResistant.get(1)` |

### Category: GlassQuarkContainment

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassQuarkContainment` | `ItemList.GlassQuarkContainment.get(1)` |

### Category: GlassTintedIndustrialBlack

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassTintedIndustrialBlack` | `ItemList.GlassTintedIndustrialBlack.get(1)` |

### Category: GlassTintedIndustrialGray

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassTintedIndustrialGray` | `ItemList.GlassTintedIndustrialGray.get(1)` |

### Category: GlassTintedIndustrialLightGray

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassTintedIndustrialLightGray` | `ItemList.GlassTintedIndustrialLightGray.get(1)` |

### Category: GlassTintedIndustrialWhite

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassTintedIndustrialWhite` | `ItemList.GlassTintedIndustrialWhite.get(1)` |

### Category: GlassUVResistant

| 枚举键值 | 获取代码 |
|---------|---------|
| `GlassUVResistant` | `ItemList.GlassUVResistant.get(1)` |

### Category: Gravistar

| 枚举键值 | 获取代码 |
|---------|---------|
| `Gravistar` | `ItemList.Gravistar.get(1)` |

### Category: HV

| 枚举键值 | 获取代码 |
|---------|---------|
| `HV_Coil` | `ItemList.HV_Coil.get(1)` |

### Category: Harmonic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Harmonic_Compound` | `ItemList.Harmonic_Compound.get(1)` |

### Category: Hatch

| 枚举键值 | 获取代码 |
|---------|---------|
| `Hatch_Antimatter` | `ItemList.Hatch_Antimatter.get(1)` |
| `Hatch_AutoMaintenance` | `ItemList.Hatch_AutoMaintenance.get(1)` |
| `Hatch_BlackHoleUtility` | `ItemList.Hatch_BlackHoleUtility.get(1)` |
| `Hatch_Catalyst_Bulk` | `ItemList.Hatch_Catalyst_Bulk.get(1)` |
| `Hatch_CraftingInput_Bus_ME` | `ItemList.Hatch_CraftingInput_Bus_ME.get(1)` |
| `Hatch_CraftingInput_Bus_ME_ItemOnly` | `ItemList.Hatch_CraftingInput_Bus_ME_ItemOnly.get(1)` |
| `Hatch_CraftingInput_Bus_Slave` | `ItemList.Hatch_CraftingInput_Bus_Slave.get(1)` |
| `Hatch_DataAccess_EV` | `ItemList.Hatch_DataAccess_EV.get(1)` |
| `Hatch_DataAccess_LuV` | `ItemList.Hatch_DataAccess_LuV.get(1)` |
| `Hatch_DataAccess_UV` | `ItemList.Hatch_DataAccess_UV.get(1)` |
| `Hatch_DegasifierControl` | `ItemList.Hatch_DegasifierControl.get(1)` |
| `Hatch_DroneDownLink` | `ItemList.Hatch_DroneDownLink.get(1)` |
| `Hatch_Dynamo_EV` | `ItemList.Hatch_Dynamo_EV.get(1)` |
| `Hatch_Dynamo_HV` | `ItemList.Hatch_Dynamo_HV.get(1)` |
| `Hatch_Dynamo_IV` | `ItemList.Hatch_Dynamo_IV.get(1)` |
| `Hatch_Dynamo_IV` | `ItemList.Hatch_Dynamo_IV.get(1)` |
| `Hatch_Dynamo_LV` | `ItemList.Hatch_Dynamo_LV.get(1)` |
| `Hatch_Dynamo_LuV` | `ItemList.Hatch_Dynamo_LuV.get(1)` |
| `Hatch_Dynamo_MV` | `ItemList.Hatch_Dynamo_MV.get(1)` |
| `Hatch_Dynamo_UEV` | `ItemList.Hatch_Dynamo_UEV.get(1)` |
| `Hatch_Dynamo_UHV` | `ItemList.Hatch_Dynamo_UHV.get(1)` |
| `Hatch_Dynamo_UIV` | `ItemList.Hatch_Dynamo_UIV.get(1)` |
| `Hatch_Dynamo_ULV` | `ItemList.Hatch_Dynamo_ULV.get(1)` |
| `Hatch_Dynamo_UMV` | `ItemList.Hatch_Dynamo_UMV.get(1)` |
| `Hatch_Dynamo_UV` | `ItemList.Hatch_Dynamo_UV.get(1)` |
| `Hatch_Dynamo_UXV` | `ItemList.Hatch_Dynamo_UXV.get(1)` |
| `Hatch_Dynamo_ZPM` | `ItemList.Hatch_Dynamo_ZPM.get(1)` |
| `Hatch_Electromagnet` | `ItemList.Hatch_Electromagnet.get(1)` |
| `Hatch_Energy_EV` | `ItemList.Hatch_Energy_EV.get(1)` |
| `Hatch_Energy_HV` | `ItemList.Hatch_Energy_HV.get(1)` |
| `Hatch_Energy_IV` | `ItemList.Hatch_Energy_IV.get(1)` |
| `Hatch_Energy_IV` | `ItemList.Hatch_Energy_IV.get(1)` |
| `Hatch_Energy_LV` | `ItemList.Hatch_Energy_LV.get(1)` |
| `Hatch_Energy_LuV` | `ItemList.Hatch_Energy_LuV.get(1)` |
| `Hatch_Energy_MV` | `ItemList.Hatch_Energy_MV.get(1)` |
| `Hatch_Energy_UEV` | `ItemList.Hatch_Energy_UEV.get(1)` |
| `Hatch_Energy_UHV` | `ItemList.Hatch_Energy_UHV.get(1)` |
| `Hatch_Energy_UIV` | `ItemList.Hatch_Energy_UIV.get(1)` |
| `Hatch_Energy_ULV` | `ItemList.Hatch_Energy_ULV.get(1)` |
| `Hatch_Energy_UMV` | `ItemList.Hatch_Energy_UMV.get(1)` |
| `Hatch_Energy_UV` | `ItemList.Hatch_Energy_UV.get(1)` |
| `Hatch_Energy_UXV` | `ItemList.Hatch_Energy_UXV.get(1)` |
| `Hatch_Energy_ZPM` | `ItemList.Hatch_Energy_ZPM.get(1)` |
| `Hatch_HeatSensor` | `ItemList.Hatch_HeatSensor.get(1)` |
| `Hatch_Input_Bus_Debug` | `ItemList.Hatch_Input_Bus_Debug.get(1)` |
| `Hatch_Input_Bus_EV` | `ItemList.Hatch_Input_Bus_EV.get(1)` |
| `Hatch_Input_Bus_EV` | `ItemList.Hatch_Input_Bus_EV.get(1)` |
| `Hatch_Input_Bus_HV` | `ItemList.Hatch_Input_Bus_HV.get(1)` |
| `Hatch_Input_Bus_IV` | `ItemList.Hatch_Input_Bus_IV.get(1)` |
| `Hatch_Input_Bus_LV` | `ItemList.Hatch_Input_Bus_LV.get(1)` |
| `Hatch_Input_Bus_LuV` | `ItemList.Hatch_Input_Bus_LuV.get(1)` |
| `Hatch_Input_Bus_MAX` | `ItemList.Hatch_Input_Bus_MAX.get(1)` |
| `Hatch_Input_Bus_ME` | `ItemList.Hatch_Input_Bus_ME.get(1)` |
| `Hatch_Input_Bus_ME_Advanced` | `ItemList.Hatch_Input_Bus_ME_Advanced.get(1)` |
| `Hatch_Input_Bus_MV` | `ItemList.Hatch_Input_Bus_MV.get(1)` |
| `Hatch_Input_Bus_ULV` | `ItemList.Hatch_Input_Bus_ULV.get(1)` |
| `Hatch_Input_Bus_UV` | `ItemList.Hatch_Input_Bus_UV.get(1)` |
| `Hatch_Input_Bus_ZPM` | `ItemList.Hatch_Input_Bus_ZPM.get(1)` |
| `Hatch_Input_Debug` | `ItemList.Hatch_Input_Debug.get(1)` |
| `Hatch_Input_EV` | `ItemList.Hatch_Input_EV.get(1)` |
| `Hatch_Input_HV` | `ItemList.Hatch_Input_HV.get(1)` |
| `Hatch_Input_IV` | `ItemList.Hatch_Input_IV.get(1)` |
| `Hatch_Input_IV` | `ItemList.Hatch_Input_IV.get(1)` |
| `Hatch_Input_LV` | `ItemList.Hatch_Input_LV.get(1)` |
| `Hatch_Input_LuV` | `ItemList.Hatch_Input_LuV.get(1)` |
| `Hatch_Input_MAX` | `ItemList.Hatch_Input_MAX.get(1)` |
| `Hatch_Input_ME` | `ItemList.Hatch_Input_ME.get(1)` |
| `Hatch_Input_ME_Advanced` | `ItemList.Hatch_Input_ME_Advanced.get(1)` |
| `Hatch_Input_MV` | `ItemList.Hatch_Input_MV.get(1)` |
| `Hatch_Input_Multi_2x2_EV` | `ItemList.Hatch_Input_Multi_2x2_EV.get(1)` |
| `Hatch_Input_Multi_2x2_Humongous` | `ItemList.Hatch_Input_Multi_2x2_Humongous.get(1)` |
| `Hatch_Input_Multi_2x2_IV` | `ItemList.Hatch_Input_Multi_2x2_IV.get(1)` |
| `Hatch_Input_Multi_2x2_LuV` | `ItemList.Hatch_Input_Multi_2x2_LuV.get(1)` |
| `Hatch_Input_Multi_2x2_UEV` | `ItemList.Hatch_Input_Multi_2x2_UEV.get(1)` |
| `Hatch_Input_Multi_2x2_UHV` | `ItemList.Hatch_Input_Multi_2x2_UHV.get(1)` |
| `Hatch_Input_Multi_2x2_UIV` | `ItemList.Hatch_Input_Multi_2x2_UIV.get(1)` |
| `Hatch_Input_Multi_2x2_UMV` | `ItemList.Hatch_Input_Multi_2x2_UMV.get(1)` |
| `Hatch_Input_Multi_2x2_UV` | `ItemList.Hatch_Input_Multi_2x2_UV.get(1)` |
| `Hatch_Input_Multi_2x2_UXV` | `ItemList.Hatch_Input_Multi_2x2_UXV.get(1)` |
| `Hatch_Input_Multi_2x2_ZPM` | `ItemList.Hatch_Input_Multi_2x2_ZPM.get(1)` |
| `Hatch_Input_UEV` | `ItemList.Hatch_Input_UEV.get(1)` |
| `Hatch_Input_UHV` | `ItemList.Hatch_Input_UHV.get(1)` |
| `Hatch_Input_UIV` | `ItemList.Hatch_Input_UIV.get(1)` |
| `Hatch_Input_ULV` | `ItemList.Hatch_Input_ULV.get(1)` |
| `Hatch_Input_UMV` | `ItemList.Hatch_Input_UMV.get(1)` |
| `Hatch_Input_UV` | `ItemList.Hatch_Input_UV.get(1)` |
| `Hatch_Input_UXV` | `ItemList.Hatch_Input_UXV.get(1)` |
| `Hatch_Input_ZPM` | `ItemList.Hatch_Input_ZPM.get(1)` |
| `Hatch_LensHousing` | `ItemList.Hatch_LensHousing.get(1)` |
| `Hatch_LensIndicator` | `ItemList.Hatch_LensIndicator.get(1)` |
| `Hatch_Maintenance` | `ItemList.Hatch_Maintenance.get(1)` |
| `Hatch_Muffler_EV` | `ItemList.Hatch_Muffler_EV.get(1)` |
| `Hatch_Muffler_HV` | `ItemList.Hatch_Muffler_HV.get(1)` |
| `Hatch_Muffler_IV` | `ItemList.Hatch_Muffler_IV.get(1)` |
| `Hatch_Muffler_IV` | `ItemList.Hatch_Muffler_IV.get(1)` |
| `Hatch_Muffler_LV` | `ItemList.Hatch_Muffler_LV.get(1)` |
| `Hatch_Muffler_LuV` | `ItemList.Hatch_Muffler_LuV.get(1)` |
| `Hatch_Muffler_MAX` | `ItemList.Hatch_Muffler_MAX.get(1)` |
| `Hatch_Muffler_MV` | `ItemList.Hatch_Muffler_MV.get(1)` |
| `Hatch_Muffler_UV` | `ItemList.Hatch_Muffler_UV.get(1)` |
| `Hatch_Muffler_ZPM` | `ItemList.Hatch_Muffler_ZPM.get(1)` |
| `Hatch_Nanite` | `ItemList.Hatch_Nanite.get(1)` |
| `Hatch_Output_Bus_EV` | `ItemList.Hatch_Output_Bus_EV.get(1)` |
| `Hatch_Output_Bus_EV` | `ItemList.Hatch_Output_Bus_EV.get(1)` |
| `Hatch_Output_Bus_HV` | `ItemList.Hatch_Output_Bus_HV.get(1)` |
| `Hatch_Output_Bus_IV` | `ItemList.Hatch_Output_Bus_IV.get(1)` |
| `Hatch_Output_Bus_LV` | `ItemList.Hatch_Output_Bus_LV.get(1)` |
| `Hatch_Output_Bus_LuV` | `ItemList.Hatch_Output_Bus_LuV.get(1)` |
| `Hatch_Output_Bus_MAX` | `ItemList.Hatch_Output_Bus_MAX.get(1)` |
| `Hatch_Output_Bus_ME` | `ItemList.Hatch_Output_Bus_ME.get(1)` |
| `Hatch_Output_Bus_MV` | `ItemList.Hatch_Output_Bus_MV.get(1)` |
| `Hatch_Output_Bus_ULV` | `ItemList.Hatch_Output_Bus_ULV.get(1)` |
| `Hatch_Output_Bus_UV` | `ItemList.Hatch_Output_Bus_UV.get(1)` |
| `Hatch_Output_Bus_ZPM` | `ItemList.Hatch_Output_Bus_ZPM.get(1)` |
| `Hatch_Output_EV` | `ItemList.Hatch_Output_EV.get(1)` |
| `Hatch_Output_HV` | `ItemList.Hatch_Output_HV.get(1)` |
| `Hatch_Output_IV` | `ItemList.Hatch_Output_IV.get(1)` |
| `Hatch_Output_IV` | `ItemList.Hatch_Output_IV.get(1)` |
| `Hatch_Output_LV` | `ItemList.Hatch_Output_LV.get(1)` |
| `Hatch_Output_LuV` | `ItemList.Hatch_Output_LuV.get(1)` |
| `Hatch_Output_MAX` | `ItemList.Hatch_Output_MAX.get(1)` |
| `Hatch_Output_ME` | `ItemList.Hatch_Output_ME.get(1)` |
| `Hatch_Output_MV` | `ItemList.Hatch_Output_MV.get(1)` |
| `Hatch_Output_UEV` | `ItemList.Hatch_Output_UEV.get(1)` |
| `Hatch_Output_UHV` | `ItemList.Hatch_Output_UHV.get(1)` |
| `Hatch_Output_UIV` | `ItemList.Hatch_Output_UIV.get(1)` |
| `Hatch_Output_ULV` | `ItemList.Hatch_Output_ULV.get(1)` |
| `Hatch_Output_UMV` | `ItemList.Hatch_Output_UMV.get(1)` |
| `Hatch_Output_UV` | `ItemList.Hatch_Output_UV.get(1)` |
| `Hatch_Output_UXV` | `ItemList.Hatch_Output_UXV.get(1)` |
| `Hatch_Output_ZPM` | `ItemList.Hatch_Output_ZPM.get(1)` |
| `Hatch_Splitter_Level` | `ItemList.Hatch_Splitter_Level.get(1)` |
| `Hatch_VacuumConveyor_Input` | `ItemList.Hatch_VacuumConveyor_Input.get(1)` |
| `Hatch_VacuumConveyor_Output` | `ItemList.Hatch_VacuumConveyor_Output.get(1)` |
| `Hatch_Void` | `ItemList.Hatch_Void.get(1)` |
| `Hatch_Void_Bus` | `ItemList.Hatch_Void_Bus.get(1)` |
| `Hatch_pHSensor` | `ItemList.Hatch_pHSensor.get(1)` |

### Category: Hawking

| 枚举键值 | 获取代码 |
|---------|---------|
| `Hawking_Glass` | `ItemList.Hawking_Glass.get(1)` |

### Category: Heating

| 枚举键值 | 获取代码 |
|---------|---------|
| `Heating_Duct_Casing` | `ItemList.Heating_Duct_Casing.get(1)` |

### Category: Heavy

| 枚举键值 | 获取代码 |
|---------|---------|
| `Heavy_Hellish_Mud` | `ItemList.Heavy_Hellish_Mud.get(1)` |

### Category: Heliocast

| 枚举键值 | 获取代码 |
|---------|---------|
| `Heliocast_Reinforcement_ExoFoundry` | `ItemList.Heliocast_Reinforcement_ExoFoundry.get(1)` |

### Category: HighEnergyFlowCircuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `HighEnergyFlowCircuit` | `ItemList.HighEnergyFlowCircuit.get(1)` |

### Category: Honeycomb

| 枚举键值 | 获取代码 |
|---------|---------|
| `Honeycomb` | `ItemList.Honeycomb.get(1)` |

### Category: Hot

| 枚举键值 | 获取代码 |
|---------|---------|
| `Hot_Netherite_Scrap` | `ItemList.Hot_Netherite_Scrap.get(1)` |

### Category: Hull

| 枚举键值 | 获取代码 |
|---------|---------|
| `Hull_Bronze` | `ItemList.Hull_Bronze.get(1)` |
| `Hull_Bronze_Bricks` | `ItemList.Hull_Bronze_Bricks.get(1)` |
| `Hull_EV` | `ItemList.Hull_EV.get(1)` |
| `Hull_HP` | `ItemList.Hull_HP.get(1)` |
| `Hull_HP_Bricks` | `ItemList.Hull_HP_Bricks.get(1)` |
| `Hull_HV` | `ItemList.Hull_HV.get(1)` |
| `Hull_IV` | `ItemList.Hull_IV.get(1)` |
| `Hull_LV` | `ItemList.Hull_LV.get(1)` |
| `Hull_LuV` | `ItemList.Hull_LuV.get(1)` |
| `Hull_MAX` | `ItemList.Hull_MAX.get(1)` |
| `Hull_MAXV` | `ItemList.Hull_MAXV.get(1)` |
| `Hull_MV` | `ItemList.Hull_MV.get(1)` |
| `Hull_UEV` | `ItemList.Hull_UEV.get(1)` |
| `Hull_UEV` | `ItemList.Hull_UEV.get(1)` |
| `Hull_UIV` | `ItemList.Hull_UIV.get(1)` |
| `Hull_ULV` | `ItemList.Hull_ULV.get(1)` |
| `Hull_UMV` | `ItemList.Hull_UMV.get(1)` |
| `Hull_UV` | `ItemList.Hull_UV.get(1)` |
| `Hull_UXV` | `ItemList.Hull_UXV.get(1)` |
| `Hull_ZPM` | `ItemList.Hull_ZPM.get(1)` |

### Category: Hypercooler

| 枚举键值 | 获取代码 |
|---------|---------|
| `Hypercooler_ExoFoundry` | `ItemList.Hypercooler_ExoFoundry.get(1)` |

### Category: IC2

| 枚举键值 | 获取代码 |
|---------|---------|
| `IC2_AdvBattery` | `ItemList.IC2_AdvBattery.get(1)` |
| `IC2_CoffeeBeans` | `ItemList.IC2_CoffeeBeans.get(1)` |
| `IC2_CoffeePowder` | `ItemList.IC2_CoffeePowder.get(1)` |
| `IC2_Compressed_Coal_Ball` | `ItemList.IC2_Compressed_Coal_Ball.get(1)` |
| `IC2_Compressed_Coal_Chunk` | `ItemList.IC2_Compressed_Coal_Chunk.get(1)` |
| `IC2_Crop_Seeds` | `ItemList.IC2_Crop_Seeds.get(1)` |
| `IC2_Energium_Dust` | `ItemList.IC2_Energium_Dust.get(1)` |
| `IC2_EnergyCrystal` | `ItemList.IC2_EnergyCrystal.get(1)` |
| `IC2_Fertilizer` | `ItemList.IC2_Fertilizer.get(1)` |
| `IC2_Food_Can_Empty` | `ItemList.IC2_Food_Can_Empty.get(1)` |
| `IC2_Food_Can_Filled` | `ItemList.IC2_Food_Can_Filled.get(1)` |
| `IC2_Food_Can_Spoiled` | `ItemList.IC2_Food_Can_Spoiled.get(1)` |
| `IC2_ForgeHammer` | `ItemList.IC2_ForgeHammer.get(1)` |
| `IC2_Fuel_Rod_Empty` | `ItemList.IC2_Fuel_Rod_Empty.get(1)` |
| `IC2_Grin_Powder` | `ItemList.IC2_Grin_Powder.get(1)` |
| `IC2_Hops` | `ItemList.IC2_Hops.get(1)` |
| `IC2_Industrial_Diamond` | `ItemList.IC2_Industrial_Diamond.get(1)` |
| `IC2_Item_Casing_Bronze` | `ItemList.IC2_Item_Casing_Bronze.get(1)` |
| `IC2_Item_Casing_Copper` | `ItemList.IC2_Item_Casing_Copper.get(1)` |
| `IC2_Item_Casing_Gold` | `ItemList.IC2_Item_Casing_Gold.get(1)` |
| `IC2_Item_Casing_Iron` | `ItemList.IC2_Item_Casing_Iron.get(1)` |
| `IC2_Item_Casing_Lead` | `ItemList.IC2_Item_Casing_Lead.get(1)` |
| `IC2_Item_Casing_Steel` | `ItemList.IC2_Item_Casing_Steel.get(1)` |
| `IC2_Item_Casing_Tin` | `ItemList.IC2_Item_Casing_Tin.get(1)` |
| `IC2_LapotronCrystal` | `ItemList.IC2_LapotronCrystal.get(1)` |
| `IC2_MOX_Fuel` | `ItemList.IC2_MOX_Fuel.get(1)` |
| `IC2_Mixed_Metal_Ingot` | `ItemList.IC2_Mixed_Metal_Ingot.get(1)` |
| `IC2_Plantball` | `ItemList.IC2_Plantball.get(1)` |
| `IC2_PlantballCompressed` | `ItemList.IC2_PlantballCompressed.get(1)` |
| `IC2_Plutonium` | `ItemList.IC2_Plutonium.get(1)` |
| `IC2_Plutonium_Small` | `ItemList.IC2_Plutonium_Small.get(1)` |
| `IC2_ReBattery` | `ItemList.IC2_ReBattery.get(1)` |
| `IC2_Resin` | `ItemList.IC2_Resin.get(1)` |
| `IC2_Scrap` | `ItemList.IC2_Scrap.get(1)` |
| `IC2_Scrapbox` | `ItemList.IC2_Scrapbox.get(1)` |
| `IC2_ShaftIron` | `ItemList.IC2_ShaftIron.get(1)` |
| `IC2_ShaftSteel` | `ItemList.IC2_ShaftSteel.get(1)` |
| `IC2_Spray_WeedEx` | `ItemList.IC2_Spray_WeedEx.get(1)` |
| `IC2_SuBattery` | `ItemList.IC2_SuBattery.get(1)` |
| `IC2_Uranium_235` | `ItemList.IC2_Uranium_235.get(1)` |
| `IC2_Uranium_235_Small` | `ItemList.IC2_Uranium_235_Small.get(1)` |
| `IC2_Uranium_238` | `ItemList.IC2_Uranium_238.get(1)` |
| `IC2_Uranium_Fuel` | `ItemList.IC2_Uranium_Fuel.get(1)` |
| `IC2_WireCutter` | `ItemList.IC2_WireCutter.get(1)` |

### Category: IV

| 枚举键值 | 获取代码 |
|---------|---------|
| `IV_Coil` | `ItemList.IV_Coil.get(1)` |

### Category: ImprintBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `ImprintBoard` | `ItemList.ImprintBoard.get(1)` |

### Category: IndustrialApiary

| 枚举键值 | 获取代码 |
|---------|---------|
| `IndustrialApiary_Upgrade_AUTOMATION` | `ItemList.IndustrialApiary_Upgrade_AUTOMATION.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_1` | `ItemList.IndustrialApiary_Upgrade_Acceleration_1.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_2` | `ItemList.IndustrialApiary_Upgrade_Acceleration_2.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_3` | `ItemList.IndustrialApiary_Upgrade_Acceleration_3.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_4` | `ItemList.IndustrialApiary_Upgrade_Acceleration_4.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_5` | `ItemList.IndustrialApiary_Upgrade_Acceleration_5.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_6` | `ItemList.IndustrialApiary_Upgrade_Acceleration_6.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_7` | `ItemList.IndustrialApiary_Upgrade_Acceleration_7.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_8` | `ItemList.IndustrialApiary_Upgrade_Acceleration_8.get(1)` |
| `IndustrialApiary_Upgrade_Acceleration_8_Upgraded` | `ItemList.IndustrialApiary_Upgrade_Acceleration_8_Upgraded.get(1)` |
| `IndustrialApiary_Upgrade_COOLER` | `ItemList.IndustrialApiary_Upgrade_COOLER.get(1)` |
| `IndustrialApiary_Upgrade_DESERT` | `ItemList.IndustrialApiary_Upgrade_DESERT.get(1)` |
| `IndustrialApiary_Upgrade_DRYER` | `ItemList.IndustrialApiary_Upgrade_DRYER.get(1)` |
| `IndustrialApiary_Upgrade_FLOWERING` | `ItemList.IndustrialApiary_Upgrade_FLOWERING.get(1)` |
| `IndustrialApiary_Upgrade_Frame` | `ItemList.IndustrialApiary_Upgrade_Frame.get(1)` |
| `IndustrialApiary_Upgrade_HEATER` | `ItemList.IndustrialApiary_Upgrade_HEATER.get(1)` |
| `IndustrialApiary_Upgrade_HELL` | `ItemList.IndustrialApiary_Upgrade_HELL.get(1)` |
| `IndustrialApiary_Upgrade_HUMIDIFIER` | `ItemList.IndustrialApiary_Upgrade_HUMIDIFIER.get(1)` |
| `IndustrialApiary_Upgrade_JUNGLE` | `ItemList.IndustrialApiary_Upgrade_JUNGLE.get(1)` |
| `IndustrialApiary_Upgrade_LIFESPAN` | `ItemList.IndustrialApiary_Upgrade_LIFESPAN.get(1)` |
| `IndustrialApiary_Upgrade_LIGHT` | `ItemList.IndustrialApiary_Upgrade_LIGHT.get(1)` |
| `IndustrialApiary_Upgrade_OCEAN` | `ItemList.IndustrialApiary_Upgrade_OCEAN.get(1)` |
| `IndustrialApiary_Upgrade_PLAINS` | `ItemList.IndustrialApiary_Upgrade_PLAINS.get(1)` |
| `IndustrialApiary_Upgrade_POLLEN` | `ItemList.IndustrialApiary_Upgrade_POLLEN.get(1)` |
| `IndustrialApiary_Upgrade_PRODUCTION` | `ItemList.IndustrialApiary_Upgrade_PRODUCTION.get(1)` |
| `IndustrialApiary_Upgrade_SEAL` | `ItemList.IndustrialApiary_Upgrade_SEAL.get(1)` |
| `IndustrialApiary_Upgrade_SIEVE` | `ItemList.IndustrialApiary_Upgrade_SIEVE.get(1)` |
| `IndustrialApiary_Upgrade_SKY` | `ItemList.IndustrialApiary_Upgrade_SKY.get(1)` |
| `IndustrialApiary_Upgrade_STABILIZER` | `ItemList.IndustrialApiary_Upgrade_STABILIZER.get(1)` |
| `IndustrialApiary_Upgrade_TERRITORY` | `ItemList.IndustrialApiary_Upgrade_TERRITORY.get(1)` |
| `IndustrialApiary_Upgrade_UNLIGHT` | `ItemList.IndustrialApiary_Upgrade_UNLIGHT.get(1)` |
| `IndustrialApiary_Upgrade_WINTER` | `ItemList.IndustrialApiary_Upgrade_WINTER.get(1)` |

### Category: IndustrialCentrifuge

| 枚举键值 | 获取代码 |
|---------|---------|
| `IndustrialCentrifuge` | `ItemList.IndustrialCentrifuge.get(1)` |

### Category: IndustrialPackager

| 枚举键值 | 获取代码 |
|---------|---------|
| `IndustrialPackager` | `ItemList.IndustrialPackager.get(1)` |

### Category: IndustrialWireFactory

| 枚举键值 | 获取代码 |
|---------|---------|
| `IndustrialWireFactory` | `ItemList.IndustrialWireFactory.get(1)` |

### Category: InfinityCooledCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `InfinityCooledCasing` | `ItemList.InfinityCooledCasing.get(1)` |

### Category: Ingot

| 枚举键值 | 获取代码 |
|---------|---------|
| `Ingot_Heavy1` | `ItemList.Ingot_Heavy1.get(1)` |
| `Ingot_Heavy2` | `ItemList.Ingot_Heavy2.get(1)` |
| `Ingot_Heavy3` | `ItemList.Ingot_Heavy3.get(1)` |
| `Ingot_IridiumAlloy` | `ItemList.Ingot_IridiumAlloy.get(1)` |

### Category: Intensely

| 枚举键值 | 获取代码 |
|---------|---------|
| `Intensely_Bonded_Netherite_Nanoparticles` | `ItemList.Intensely_Bonded_Netherite_Nanoparticles.get(1)` |

### Category: IntricateCircuitBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `IntricateCircuitBoard` | `ItemList.IntricateCircuitBoard.get(1)` |

### Category: Item

| 枚举键值 | 获取代码 |
|---------|---------|
| `Item_Power_Goggles` | `ItemList.Item_Power_Goggles.get(1)` |
| `Item_Redstone_Sniffer` | `ItemList.Item_Redstone_Sniffer.get(1)` |

### Category: ItemFilter

| 枚举键值 | 获取代码 |
|---------|---------|
| `ItemFilter_Export` | `ItemList.ItemFilter_Export.get(1)` |
| `ItemFilter_Import` | `ItemList.ItemFilter_Import.get(1)` |

### Category: KevlarFiber

| 枚举键值 | 获取代码 |
|---------|---------|
| `KevlarFiber` | `ItemList.KevlarFiber.get(1)` |

### Category: LATEX

| 枚举键值 | 获取代码 |
|---------|---------|
| `LATEX` | `ItemList.LATEX.get(1)` |

### Category: LV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LV_Coil` | `ItemList.LV_Coil.get(1)` |

### Category: Large

| 枚举键值 | 获取代码 |
|---------|---------|
| `Large_Fluid_Cell_Aluminium` | `ItemList.Large_Fluid_Cell_Aluminium.get(1)` |
| `Large_Fluid_Cell_Chrome` | `ItemList.Large_Fluid_Cell_Chrome.get(1)` |
| `Large_Fluid_Cell_Iridium` | `ItemList.Large_Fluid_Cell_Iridium.get(1)` |
| `Large_Fluid_Cell_Neutronium` | `ItemList.Large_Fluid_Cell_Neutronium.get(1)` |
| `Large_Fluid_Cell_Osmium` | `ItemList.Large_Fluid_Cell_Osmium.get(1)` |
| `Large_Fluid_Cell_StainlessSteel` | `ItemList.Large_Fluid_Cell_StainlessSteel.get(1)` |
| `Large_Fluid_Cell_Steel` | `ItemList.Large_Fluid_Cell_Steel.get(1)` |
| `Large_Fluid_Cell_Titanium` | `ItemList.Large_Fluid_Cell_Titanium.get(1)` |
| `Large_Fluid_Cell_TungstenSteel` | `ItemList.Large_Fluid_Cell_TungstenSteel.get(1)` |

### Category: LargeFluidExtractor

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargeFluidExtractor` | `ItemList.LargeFluidExtractor.get(1)` |

### Category: LargeGasTurbine

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargeGasTurbine` | `ItemList.LargeGasTurbine.get(1)` |

### Category: LargeHPSteamTurbine

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargeHPSteamTurbine` | `ItemList.LargeHPSteamTurbine.get(1)` |

### Category: LargeMolecularAssembler

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargeMolecularAssembler` | `ItemList.LargeMolecularAssembler.get(1)` |

### Category: LargePlasmaTurbine

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargePlasmaTurbine` | `ItemList.LargePlasmaTurbine.get(1)` |

### Category: LargeSteamTurbine

| 枚举键值 | 获取代码 |
|---------|---------|
| `LargeSteamTurbine` | `ItemList.LargeSteamTurbine.get(1)` |

### Category: Laser

| 枚举键值 | 获取代码 |
|---------|---------|
| `Laser_Plate` | `ItemList.Laser_Plate.get(1)` |

### Category: LatheLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheLuV` | `ItemList.LatheLuV.get(1)` |

### Category: LatheUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheUEV` | `ItemList.LatheUEV.get(1)` |

### Category: LatheUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheUHV` | `ItemList.LatheUHV.get(1)` |

### Category: LatheUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheUIV` | `ItemList.LatheUIV.get(1)` |

### Category: LatheUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheUMV` | `ItemList.LatheUMV.get(1)` |

### Category: LatheUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheUV` | `ItemList.LatheUV.get(1)` |

### Category: LatheZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `LatheZPM` | `ItemList.LatheZPM.get(1)` |

### Category: LoadbearingDistributionCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `LoadbearingDistributionCasing` | `ItemList.LoadbearingDistributionCasing.get(1)` |

### Category: Locker

| 枚举键值 | 获取代码 |
|---------|---------|
| `Locker_EV` | `ItemList.Locker_EV.get(1)` |
| `Locker_HV` | `ItemList.Locker_HV.get(1)` |
| `Locker_IV` | `ItemList.Locker_IV.get(1)` |
| `Locker_LV` | `ItemList.Locker_LV.get(1)` |
| `Locker_LuV` | `ItemList.Locker_LuV.get(1)` |
| `Locker_MAX` | `ItemList.Locker_MAX.get(1)` |
| `Locker_MV` | `ItemList.Locker_MV.get(1)` |
| `Locker_ULV` | `ItemList.Locker_ULV.get(1)` |
| `Locker_UV` | `ItemList.Locker_UV.get(1)` |
| `Locker_ZPM` | `ItemList.Locker_ZPM.get(1)` |

### Category: Long

| 枚举键值 | 获取代码 |
|---------|---------|
| `Long_Distance_Pipeline_Fluid` | `ItemList.Long_Distance_Pipeline_Fluid.get(1)` |
| `Long_Distance_Pipeline_Fluid_Pipe` | `ItemList.Long_Distance_Pipeline_Fluid_Pipe.get(1)` |
| `Long_Distance_Pipeline_Item` | `ItemList.Long_Distance_Pipeline_Item.get(1)` |
| `Long_Distance_Pipeline_Item_Pipe` | `ItemList.Long_Distance_Pipeline_Item_Pipe.get(1)` |

### Category: LuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `LuV_Coil` | `ItemList.LuV_Coil.get(1)` |

### Category: MSFMixture

| 枚举键值 | 获取代码 |
|---------|---------|
| `MSFMixture` | `ItemList.MSFMixture.get(1)` |

### Category: MV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MV_Coil` | `ItemList.MV_Coil.get(1)` |

### Category: MaceratorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorLuV` | `ItemList.MaceratorLuV.get(1)` |

### Category: MaceratorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorUEV` | `ItemList.MaceratorUEV.get(1)` |

### Category: MaceratorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorUHV` | `ItemList.MaceratorUHV.get(1)` |

### Category: MaceratorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorUIV` | `ItemList.MaceratorUIV.get(1)` |

### Category: MaceratorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorUMV` | `ItemList.MaceratorUMV.get(1)` |

### Category: MaceratorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorUV` | `ItemList.MaceratorUV.get(1)` |

### Category: MaceratorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `MaceratorZPM` | `ItemList.MaceratorZPM.get(1)` |

### Category: Machine

| 枚举键值 | 获取代码 |
|---------|---------|
| `Machine_Bricked_BlastFurnace` | `ItemList.Machine_Bricked_BlastFurnace.get(1)` |
| `Machine_Bronze_AlloySmelter` | `ItemList.Machine_Bronze_AlloySmelter.get(1)` |
| `Machine_Bronze_Boiler` | `ItemList.Machine_Bronze_Boiler.get(1)` |
| `Machine_Bronze_Boiler_Solar` | `ItemList.Machine_Bronze_Boiler_Solar.get(1)` |
| `Machine_Bronze_Compressor` | `ItemList.Machine_Bronze_Compressor.get(1)` |
| `Machine_Bronze_CraftingTable` | `ItemList.Machine_Bronze_CraftingTable.get(1)` |
| `Machine_Bronze_Extractor` | `ItemList.Machine_Bronze_Extractor.get(1)` |
| `Machine_Bronze_Furnace` | `ItemList.Machine_Bronze_Furnace.get(1)` |
| `Machine_Bronze_Hammer` | `ItemList.Machine_Bronze_Hammer.get(1)` |
| `Machine_Bronze_Macerator` | `ItemList.Machine_Bronze_Macerator.get(1)` |
| `Machine_EV_AlloySmelter` | `ItemList.Machine_EV_AlloySmelter.get(1)` |
| `Machine_EV_Amplifab` | `ItemList.Machine_EV_Amplifab.get(1)` |
| `Machine_EV_ArcFurnace` | `ItemList.Machine_EV_ArcFurnace.get(1)` |
| `Machine_EV_Assembler` | `ItemList.Machine_EV_Assembler.get(1)` |
| `Machine_EV_Autoclave` | `ItemList.Machine_EV_Autoclave.get(1)` |
| `Machine_EV_Bender` | `ItemList.Machine_EV_Bender.get(1)` |
| `Machine_EV_Boxinator` | `ItemList.Machine_EV_Boxinator.get(1)` |
| `Machine_EV_Brewery` | `ItemList.Machine_EV_Brewery.get(1)` |
| `Machine_EV_Bundler` | `ItemList.Machine_EV_Bundler.get(1)` |
| `Machine_EV_Canner` | `ItemList.Machine_EV_Canner.get(1)` |
| `Machine_EV_Centrifuge` | `ItemList.Machine_EV_Centrifuge.get(1)` |
| `Machine_EV_ChemicalBath` | `ItemList.Machine_EV_ChemicalBath.get(1)` |
| `Machine_EV_ChemicalReactor` | `ItemList.Machine_EV_ChemicalReactor.get(1)` |
| `Machine_EV_CircuitAssembler` | `ItemList.Machine_EV_CircuitAssembler.get(1)` |
| `Machine_EV_Compressor` | `ItemList.Machine_EV_Compressor.get(1)` |
| `Machine_EV_Cutter` | `ItemList.Machine_EV_Cutter.get(1)` |
| `Machine_EV_Distillery` | `ItemList.Machine_EV_Distillery.get(1)` |
| `Machine_EV_E_Furnace` | `ItemList.Machine_EV_E_Furnace.get(1)` |
| `Machine_EV_Electrolyzer` | `ItemList.Machine_EV_Electrolyzer.get(1)` |
| `Machine_EV_ElectromagneticSeparator` | `ItemList.Machine_EV_ElectromagneticSeparator.get(1)` |
| `Machine_EV_Extractor` | `ItemList.Machine_EV_Extractor.get(1)` |
| `Machine_EV_Extruder` | `ItemList.Machine_EV_Extruder.get(1)` |
| `Machine_EV_Fermenter` | `ItemList.Machine_EV_Fermenter.get(1)` |
| `Machine_EV_FluidCanner` | `ItemList.Machine_EV_FluidCanner.get(1)` |
| `Machine_EV_FluidExtractor` | `ItemList.Machine_EV_FluidExtractor.get(1)` |
| `Machine_EV_FluidHeater` | `ItemList.Machine_EV_FluidHeater.get(1)` |
| `Machine_EV_FluidSolidifier` | `ItemList.Machine_EV_FluidSolidifier.get(1)` |
| `Machine_EV_Hammer` | `ItemList.Machine_EV_Hammer.get(1)` |
| `Machine_EV_LaserEngraver` | `ItemList.Machine_EV_LaserEngraver.get(1)` |
| `Machine_EV_Lathe` | `ItemList.Machine_EV_Lathe.get(1)` |
| `Machine_EV_LightningRod` | `ItemList.Machine_EV_LightningRod.get(1)` |
| `Machine_EV_Macerator` | `ItemList.Machine_EV_Macerator.get(1)` |
| `Machine_EV_Massfab` | `ItemList.Machine_EV_Massfab.get(1)` |
| `Machine_EV_Microwave` | `ItemList.Machine_EV_Microwave.get(1)` |
| `Machine_EV_Mixer` | `ItemList.Machine_EV_Mixer.get(1)` |
| `Machine_EV_OreWasher` | `ItemList.Machine_EV_OreWasher.get(1)` |
| `Machine_EV_Oven` | `ItemList.Machine_EV_Oven.get(1)` |
| `Machine_EV_PlasmaArcFurnace` | `ItemList.Machine_EV_PlasmaArcFurnace.get(1)` |
| `Machine_EV_Polarizer` | `ItemList.Machine_EV_Polarizer.get(1)` |
| `Machine_EV_Press` | `ItemList.Machine_EV_Press.get(1)` |
| `Machine_EV_Printer` | `ItemList.Machine_EV_Printer.get(1)` |
| `Machine_EV_Recycler` | `ItemList.Machine_EV_Recycler.get(1)` |
| `Machine_EV_Replicator` | `ItemList.Machine_EV_Replicator.get(1)` |
| `Machine_EV_RockBreaker` | `ItemList.Machine_EV_RockBreaker.get(1)` |
| `Machine_EV_Scanner` | `ItemList.Machine_EV_Scanner.get(1)` |
| `Machine_EV_Sifter` | `ItemList.Machine_EV_Sifter.get(1)` |
| `Machine_EV_SolarPanel` | `ItemList.Machine_EV_SolarPanel.get(1)` |
| `Machine_EV_ThermalCentrifuge` | `ItemList.Machine_EV_ThermalCentrifuge.get(1)` |
| `Machine_EV_Unboxinator` | `ItemList.Machine_EV_Unboxinator.get(1)` |
| `Machine_EV_Wiremill` | `ItemList.Machine_EV_Wiremill.get(1)` |
| `Machine_Fluid_Shaper` | `ItemList.Machine_Fluid_Shaper.get(1)` |
| `Machine_HP_AlloySmelter` | `ItemList.Machine_HP_AlloySmelter.get(1)` |
| `Machine_HP_Compressor` | `ItemList.Machine_HP_Compressor.get(1)` |
| `Machine_HP_Extractor` | `ItemList.Machine_HP_Extractor.get(1)` |
| `Machine_HP_Furnace` | `ItemList.Machine_HP_Furnace.get(1)` |
| `Machine_HP_Hammer` | `ItemList.Machine_HP_Hammer.get(1)` |
| `Machine_HP_Macerator` | `ItemList.Machine_HP_Macerator.get(1)` |
| `Machine_HP_Solar` | `ItemList.Machine_HP_Solar.get(1)` |
| `Machine_HV_AlloySmelter` | `ItemList.Machine_HV_AlloySmelter.get(1)` |
| `Machine_HV_Amplifab` | `ItemList.Machine_HV_Amplifab.get(1)` |
| `Machine_HV_ArcFurnace` | `ItemList.Machine_HV_ArcFurnace.get(1)` |
| `Machine_HV_Assembler` | `ItemList.Machine_HV_Assembler.get(1)` |
| `Machine_HV_Autoclave` | `ItemList.Machine_HV_Autoclave.get(1)` |
| `Machine_HV_Bender` | `ItemList.Machine_HV_Bender.get(1)` |
| `Machine_HV_Boxinator` | `ItemList.Machine_HV_Boxinator.get(1)` |
| `Machine_HV_Brewery` | `ItemList.Machine_HV_Brewery.get(1)` |
| `Machine_HV_Bundler` | `ItemList.Machine_HV_Bundler.get(1)` |
| `Machine_HV_Canner` | `ItemList.Machine_HV_Canner.get(1)` |
| `Machine_HV_Centrifuge` | `ItemList.Machine_HV_Centrifuge.get(1)` |
| `Machine_HV_ChemicalBath` | `ItemList.Machine_HV_ChemicalBath.get(1)` |
| `Machine_HV_ChemicalReactor` | `ItemList.Machine_HV_ChemicalReactor.get(1)` |
| `Machine_HV_CircuitAssembler` | `ItemList.Machine_HV_CircuitAssembler.get(1)` |
| `Machine_HV_Compressor` | `ItemList.Machine_HV_Compressor.get(1)` |
| `Machine_HV_Cutter` | `ItemList.Machine_HV_Cutter.get(1)` |
| `Machine_HV_Distillery` | `ItemList.Machine_HV_Distillery.get(1)` |
| `Machine_HV_DrawerFramer` | `ItemList.Machine_HV_DrawerFramer.get(1)` |
| `Machine_HV_E_Furnace` | `ItemList.Machine_HV_E_Furnace.get(1)` |
| `Machine_HV_Electrolyzer` | `ItemList.Machine_HV_Electrolyzer.get(1)` |
| `Machine_HV_ElectromagneticSeparator` | `ItemList.Machine_HV_ElectromagneticSeparator.get(1)` |
| `Machine_HV_Extractor` | `ItemList.Machine_HV_Extractor.get(1)` |
| `Machine_HV_Extruder` | `ItemList.Machine_HV_Extruder.get(1)` |
| `Machine_HV_Fermenter` | `ItemList.Machine_HV_Fermenter.get(1)` |
| `Machine_HV_FluidCanner` | `ItemList.Machine_HV_FluidCanner.get(1)` |
| `Machine_HV_FluidExtractor` | `ItemList.Machine_HV_FluidExtractor.get(1)` |
| `Machine_HV_FluidHeater` | `ItemList.Machine_HV_FluidHeater.get(1)` |
| `Machine_HV_FluidSolidifier` | `ItemList.Machine_HV_FluidSolidifier.get(1)` |
| `Machine_HV_Hammer` | `ItemList.Machine_HV_Hammer.get(1)` |
| `Machine_HV_LaserEngraver` | `ItemList.Machine_HV_LaserEngraver.get(1)` |
| `Machine_HV_Lathe` | `ItemList.Machine_HV_Lathe.get(1)` |
| `Machine_HV_LightningRod` | `ItemList.Machine_HV_LightningRod.get(1)` |
| `Machine_HV_Macerator` | `ItemList.Machine_HV_Macerator.get(1)` |
| `Machine_HV_Massfab` | `ItemList.Machine_HV_Massfab.get(1)` |
| `Machine_HV_Microwave` | `ItemList.Machine_HV_Microwave.get(1)` |
| `Machine_HV_Miner` | `ItemList.Machine_HV_Miner.get(1)` |
| `Machine_HV_Mixer` | `ItemList.Machine_HV_Mixer.get(1)` |
| `Machine_HV_OreWasher` | `ItemList.Machine_HV_OreWasher.get(1)` |
| `Machine_HV_Oven` | `ItemList.Machine_HV_Oven.get(1)` |
| `Machine_HV_PlasmaArcFurnace` | `ItemList.Machine_HV_PlasmaArcFurnace.get(1)` |
| `Machine_HV_Polarizer` | `ItemList.Machine_HV_Polarizer.get(1)` |
| `Machine_HV_Press` | `ItemList.Machine_HV_Press.get(1)` |
| `Machine_HV_Printer` | `ItemList.Machine_HV_Printer.get(1)` |
| `Machine_HV_Recycler` | `ItemList.Machine_HV_Recycler.get(1)` |
| `Machine_HV_Replicator` | `ItemList.Machine_HV_Replicator.get(1)` |
| `Machine_HV_RockBreaker` | `ItemList.Machine_HV_RockBreaker.get(1)` |
| `Machine_HV_Scanner` | `ItemList.Machine_HV_Scanner.get(1)` |
| `Machine_HV_Sifter` | `ItemList.Machine_HV_Sifter.get(1)` |
| `Machine_HV_SolarPanel` | `ItemList.Machine_HV_SolarPanel.get(1)` |
| `Machine_HV_ThermalCentrifuge` | `ItemList.Machine_HV_ThermalCentrifuge.get(1)` |
| `Machine_HV_Unboxinator` | `ItemList.Machine_HV_Unboxinator.get(1)` |
| `Machine_HV_Wiremill` | `ItemList.Machine_HV_Wiremill.get(1)` |
| `Machine_IV_AlloySmelter` | `ItemList.Machine_IV_AlloySmelter.get(1)` |
| `Machine_IV_Amplifab` | `ItemList.Machine_IV_Amplifab.get(1)` |
| `Machine_IV_ArcFurnace` | `ItemList.Machine_IV_ArcFurnace.get(1)` |
| `Machine_IV_Assembler` | `ItemList.Machine_IV_Assembler.get(1)` |
| `Machine_IV_Autoclave` | `ItemList.Machine_IV_Autoclave.get(1)` |
| `Machine_IV_Bender` | `ItemList.Machine_IV_Bender.get(1)` |
| `Machine_IV_Boxinator` | `ItemList.Machine_IV_Boxinator.get(1)` |
| `Machine_IV_Brewery` | `ItemList.Machine_IV_Brewery.get(1)` |
| `Machine_IV_Bundler` | `ItemList.Machine_IV_Bundler.get(1)` |
| `Machine_IV_Canner` | `ItemList.Machine_IV_Canner.get(1)` |
| `Machine_IV_Centrifuge` | `ItemList.Machine_IV_Centrifuge.get(1)` |
| `Machine_IV_ChemicalBath` | `ItemList.Machine_IV_ChemicalBath.get(1)` |
| `Machine_IV_ChemicalReactor` | `ItemList.Machine_IV_ChemicalReactor.get(1)` |
| `Machine_IV_CircuitAssembler` | `ItemList.Machine_IV_CircuitAssembler.get(1)` |
| `Machine_IV_Compressor` | `ItemList.Machine_IV_Compressor.get(1)` |
| `Machine_IV_Cutter` | `ItemList.Machine_IV_Cutter.get(1)` |
| `Machine_IV_Distillery` | `ItemList.Machine_IV_Distillery.get(1)` |
| `Machine_IV_E_Furnace` | `ItemList.Machine_IV_E_Furnace.get(1)` |
| `Machine_IV_Electrolyzer` | `ItemList.Machine_IV_Electrolyzer.get(1)` |
| `Machine_IV_ElectromagneticSeparator` | `ItemList.Machine_IV_ElectromagneticSeparator.get(1)` |
| `Machine_IV_Extractor` | `ItemList.Machine_IV_Extractor.get(1)` |
| `Machine_IV_Extruder` | `ItemList.Machine_IV_Extruder.get(1)` |
| `Machine_IV_Fermenter` | `ItemList.Machine_IV_Fermenter.get(1)` |
| `Machine_IV_FluidCanner` | `ItemList.Machine_IV_FluidCanner.get(1)` |
| `Machine_IV_FluidExtractor` | `ItemList.Machine_IV_FluidExtractor.get(1)` |
| `Machine_IV_FluidHeater` | `ItemList.Machine_IV_FluidHeater.get(1)` |
| `Machine_IV_FluidSolidifier` | `ItemList.Machine_IV_FluidSolidifier.get(1)` |
| `Machine_IV_Hammer` | `ItemList.Machine_IV_Hammer.get(1)` |
| `Machine_IV_LaserEngraver` | `ItemList.Machine_IV_LaserEngraver.get(1)` |
| `Machine_IV_Lathe` | `ItemList.Machine_IV_Lathe.get(1)` |
| `Machine_IV_LightningRod` | `ItemList.Machine_IV_LightningRod.get(1)` |
| `Machine_IV_Macerator` | `ItemList.Machine_IV_Macerator.get(1)` |
| `Machine_IV_Massfab` | `ItemList.Machine_IV_Massfab.get(1)` |
| `Machine_IV_Microwave` | `ItemList.Machine_IV_Microwave.get(1)` |
| `Machine_IV_Mixer` | `ItemList.Machine_IV_Mixer.get(1)` |
| `Machine_IV_OreWasher` | `ItemList.Machine_IV_OreWasher.get(1)` |
| `Machine_IV_Oven` | `ItemList.Machine_IV_Oven.get(1)` |
| `Machine_IV_PlasmaArcFurnace` | `ItemList.Machine_IV_PlasmaArcFurnace.get(1)` |
| `Machine_IV_Polarizer` | `ItemList.Machine_IV_Polarizer.get(1)` |
| `Machine_IV_Press` | `ItemList.Machine_IV_Press.get(1)` |
| `Machine_IV_Printer` | `ItemList.Machine_IV_Printer.get(1)` |
| `Machine_IV_Recycler` | `ItemList.Machine_IV_Recycler.get(1)` |
| `Machine_IV_Replicator` | `ItemList.Machine_IV_Replicator.get(1)` |
| `Machine_IV_RockBreaker` | `ItemList.Machine_IV_RockBreaker.get(1)` |
| `Machine_IV_Scanner` | `ItemList.Machine_IV_Scanner.get(1)` |
| `Machine_IV_Sifter` | `ItemList.Machine_IV_Sifter.get(1)` |
| `Machine_IV_SolarPanel` | `ItemList.Machine_IV_SolarPanel.get(1)` |
| `Machine_IV_ThermalCentrifuge` | `ItemList.Machine_IV_ThermalCentrifuge.get(1)` |
| `Machine_IV_Unboxinator` | `ItemList.Machine_IV_Unboxinator.get(1)` |
| `Machine_IV_Wiremill` | `ItemList.Machine_IV_Wiremill.get(1)` |
| `Machine_IndustrialApiary` | `ItemList.Machine_IndustrialApiary.get(1)` |
| `Machine_LV_AlloySmelter` | `ItemList.Machine_LV_AlloySmelter.get(1)` |
| `Machine_LV_Amplifab` | `ItemList.Machine_LV_Amplifab.get(1)` |
| `Machine_LV_ArcFurnace` | `ItemList.Machine_LV_ArcFurnace.get(1)` |
| `Machine_LV_Assembler` | `ItemList.Machine_LV_Assembler.get(1)` |
| `Machine_LV_Autoclave` | `ItemList.Machine_LV_Autoclave.get(1)` |
| `Machine_LV_Bender` | `ItemList.Machine_LV_Bender.get(1)` |
| `Machine_LV_Boxinator` | `ItemList.Machine_LV_Boxinator.get(1)` |
| `Machine_LV_Brewery` | `ItemList.Machine_LV_Brewery.get(1)` |
| `Machine_LV_Bundler` | `ItemList.Machine_LV_Bundler.get(1)` |
| `Machine_LV_Canner` | `ItemList.Machine_LV_Canner.get(1)` |
| `Machine_LV_Centrifuge` | `ItemList.Machine_LV_Centrifuge.get(1)` |
| `Machine_LV_ChemicalBath` | `ItemList.Machine_LV_ChemicalBath.get(1)` |
| `Machine_LV_ChemicalReactor` | `ItemList.Machine_LV_ChemicalReactor.get(1)` |
| `Machine_LV_CircuitAssembler` | `ItemList.Machine_LV_CircuitAssembler.get(1)` |
| `Machine_LV_Compressor` | `ItemList.Machine_LV_Compressor.get(1)` |
| `Machine_LV_Cutter` | `ItemList.Machine_LV_Cutter.get(1)` |
| `Machine_LV_Distillery` | `ItemList.Machine_LV_Distillery.get(1)` |
| `Machine_LV_DrawerFramer` | `ItemList.Machine_LV_DrawerFramer.get(1)` |
| `Machine_LV_E_Furnace` | `ItemList.Machine_LV_E_Furnace.get(1)` |
| `Machine_LV_Electrolyzer` | `ItemList.Machine_LV_Electrolyzer.get(1)` |
| `Machine_LV_ElectromagneticSeparator` | `ItemList.Machine_LV_ElectromagneticSeparator.get(1)` |
| `Machine_LV_Extractor` | `ItemList.Machine_LV_Extractor.get(1)` |
| `Machine_LV_Extruder` | `ItemList.Machine_LV_Extruder.get(1)` |
| `Machine_LV_Fermenter` | `ItemList.Machine_LV_Fermenter.get(1)` |
| `Machine_LV_FluidCanner` | `ItemList.Machine_LV_FluidCanner.get(1)` |
| `Machine_LV_FluidExtractor` | `ItemList.Machine_LV_FluidExtractor.get(1)` |
| `Machine_LV_FluidHeater` | `ItemList.Machine_LV_FluidHeater.get(1)` |
| `Machine_LV_FluidSolidifier` | `ItemList.Machine_LV_FluidSolidifier.get(1)` |
| `Machine_LV_Hammer` | `ItemList.Machine_LV_Hammer.get(1)` |
| `Machine_LV_LaserEngraver` | `ItemList.Machine_LV_LaserEngraver.get(1)` |
| `Machine_LV_Lathe` | `ItemList.Machine_LV_Lathe.get(1)` |
| `Machine_LV_Macerator` | `ItemList.Machine_LV_Macerator.get(1)` |
| `Machine_LV_Massfab` | `ItemList.Machine_LV_Massfab.get(1)` |
| `Machine_LV_Microwave` | `ItemList.Machine_LV_Microwave.get(1)` |
| `Machine_LV_Miner` | `ItemList.Machine_LV_Miner.get(1)` |
| `Machine_LV_Mixer` | `ItemList.Machine_LV_Mixer.get(1)` |
| `Machine_LV_OreWasher` | `ItemList.Machine_LV_OreWasher.get(1)` |
| `Machine_LV_Oven` | `ItemList.Machine_LV_Oven.get(1)` |
| `Machine_LV_PlasmaArcFurnace` | `ItemList.Machine_LV_PlasmaArcFurnace.get(1)` |
| `Machine_LV_Polarizer` | `ItemList.Machine_LV_Polarizer.get(1)` |
| `Machine_LV_Press` | `ItemList.Machine_LV_Press.get(1)` |
| `Machine_LV_Printer` | `ItemList.Machine_LV_Printer.get(1)` |
| `Machine_LV_Recycler` | `ItemList.Machine_LV_Recycler.get(1)` |
| `Machine_LV_Replicator` | `ItemList.Machine_LV_Replicator.get(1)` |
| `Machine_LV_RockBreaker` | `ItemList.Machine_LV_RockBreaker.get(1)` |
| `Machine_LV_Scanner` | `ItemList.Machine_LV_Scanner.get(1)` |
| `Machine_LV_Sifter` | `ItemList.Machine_LV_Sifter.get(1)` |
| `Machine_LV_SolarPanel` | `ItemList.Machine_LV_SolarPanel.get(1)` |
| `Machine_LV_ThermalCentrifuge` | `ItemList.Machine_LV_ThermalCentrifuge.get(1)` |
| `Machine_LV_Unboxinator` | `ItemList.Machine_LV_Unboxinator.get(1)` |
| `Machine_LV_Wiremill` | `ItemList.Machine_LV_Wiremill.get(1)` |
| `Machine_LuV_Boxinator` | `ItemList.Machine_LuV_Boxinator.get(1)` |
| `Machine_LuV_CircuitAssembler` | `ItemList.Machine_LuV_CircuitAssembler.get(1)` |
| `Machine_LuV_Printer` | `ItemList.Machine_LuV_Printer.get(1)` |
| `Machine_LuV_SolarPanel` | `ItemList.Machine_LuV_SolarPanel.get(1)` |
| `Machine_LuV_Unboxinator` | `ItemList.Machine_LuV_Unboxinator.get(1)` |
| `Machine_MV_AlloySmelter` | `ItemList.Machine_MV_AlloySmelter.get(1)` |
| `Machine_MV_Amplifab` | `ItemList.Machine_MV_Amplifab.get(1)` |
| `Machine_MV_ArcFurnace` | `ItemList.Machine_MV_ArcFurnace.get(1)` |
| `Machine_MV_Assembler` | `ItemList.Machine_MV_Assembler.get(1)` |
| `Machine_MV_Autoclave` | `ItemList.Machine_MV_Autoclave.get(1)` |
| `Machine_MV_Bender` | `ItemList.Machine_MV_Bender.get(1)` |
| `Machine_MV_Boxinator` | `ItemList.Machine_MV_Boxinator.get(1)` |
| `Machine_MV_Brewery` | `ItemList.Machine_MV_Brewery.get(1)` |
| `Machine_MV_Bundler` | `ItemList.Machine_MV_Bundler.get(1)` |
| `Machine_MV_Canner` | `ItemList.Machine_MV_Canner.get(1)` |
| `Machine_MV_Centrifuge` | `ItemList.Machine_MV_Centrifuge.get(1)` |
| `Machine_MV_ChemicalBath` | `ItemList.Machine_MV_ChemicalBath.get(1)` |
| `Machine_MV_ChemicalReactor` | `ItemList.Machine_MV_ChemicalReactor.get(1)` |
| `Machine_MV_CircuitAssembler` | `ItemList.Machine_MV_CircuitAssembler.get(1)` |
| `Machine_MV_Compressor` | `ItemList.Machine_MV_Compressor.get(1)` |
| `Machine_MV_Cutter` | `ItemList.Machine_MV_Cutter.get(1)` |
| `Machine_MV_Distillery` | `ItemList.Machine_MV_Distillery.get(1)` |
| `Machine_MV_DrawerFramer` | `ItemList.Machine_MV_DrawerFramer.get(1)` |
| `Machine_MV_E_Furnace` | `ItemList.Machine_MV_E_Furnace.get(1)` |
| `Machine_MV_Electrolyzer` | `ItemList.Machine_MV_Electrolyzer.get(1)` |
| `Machine_MV_ElectromagneticSeparator` | `ItemList.Machine_MV_ElectromagneticSeparator.get(1)` |
| `Machine_MV_Extractor` | `ItemList.Machine_MV_Extractor.get(1)` |
| `Machine_MV_Extruder` | `ItemList.Machine_MV_Extruder.get(1)` |
| `Machine_MV_Fermenter` | `ItemList.Machine_MV_Fermenter.get(1)` |
| `Machine_MV_FluidCanner` | `ItemList.Machine_MV_FluidCanner.get(1)` |
| `Machine_MV_FluidExtractor` | `ItemList.Machine_MV_FluidExtractor.get(1)` |
| `Machine_MV_FluidHeater` | `ItemList.Machine_MV_FluidHeater.get(1)` |
| `Machine_MV_FluidSolidifier` | `ItemList.Machine_MV_FluidSolidifier.get(1)` |
| `Machine_MV_Hammer` | `ItemList.Machine_MV_Hammer.get(1)` |
| `Machine_MV_LaserEngraver` | `ItemList.Machine_MV_LaserEngraver.get(1)` |
| `Machine_MV_Lathe` | `ItemList.Machine_MV_Lathe.get(1)` |
| `Machine_MV_Macerator` | `ItemList.Machine_MV_Macerator.get(1)` |
| `Machine_MV_Massfab` | `ItemList.Machine_MV_Massfab.get(1)` |
| `Machine_MV_Microwave` | `ItemList.Machine_MV_Microwave.get(1)` |
| `Machine_MV_Miner` | `ItemList.Machine_MV_Miner.get(1)` |
| `Machine_MV_Mixer` | `ItemList.Machine_MV_Mixer.get(1)` |
| `Machine_MV_OreWasher` | `ItemList.Machine_MV_OreWasher.get(1)` |
| `Machine_MV_Oven` | `ItemList.Machine_MV_Oven.get(1)` |
| `Machine_MV_PlasmaArcFurnace` | `ItemList.Machine_MV_PlasmaArcFurnace.get(1)` |
| `Machine_MV_Polarizer` | `ItemList.Machine_MV_Polarizer.get(1)` |
| `Machine_MV_Press` | `ItemList.Machine_MV_Press.get(1)` |
| `Machine_MV_Printer` | `ItemList.Machine_MV_Printer.get(1)` |
| `Machine_MV_Recycler` | `ItemList.Machine_MV_Recycler.get(1)` |
| `Machine_MV_Replicator` | `ItemList.Machine_MV_Replicator.get(1)` |
| `Machine_MV_RockBreaker` | `ItemList.Machine_MV_RockBreaker.get(1)` |
| `Machine_MV_Scanner` | `ItemList.Machine_MV_Scanner.get(1)` |
| `Machine_MV_Sifter` | `ItemList.Machine_MV_Sifter.get(1)` |
| `Machine_MV_SolarPanel` | `ItemList.Machine_MV_SolarPanel.get(1)` |
| `Machine_MV_ThermalCentrifuge` | `ItemList.Machine_MV_ThermalCentrifuge.get(1)` |
| `Machine_MV_Unboxinator` | `ItemList.Machine_MV_Unboxinator.get(1)` |
| `Machine_MV_Wiremill` | `ItemList.Machine_MV_Wiremill.get(1)` |
| `Machine_Mass_Solidifier` | `ItemList.Machine_Mass_Solidifier.get(1)` |
| `Machine_Multi_AirFilterT1` | `ItemList.Machine_Multi_AirFilterT1.get(1)` |
| `Machine_Multi_AirFilterT2` | `ItemList.Machine_Multi_AirFilterT2.get(1)` |
| `Machine_Multi_AirFilterT3` | `ItemList.Machine_Multi_AirFilterT3.get(1)` |
| `Machine_Multi_Assemblyline` | `ItemList.Machine_Multi_Assemblyline.get(1)` |
| `Machine_Multi_Autoclave` | `ItemList.Machine_Multi_Autoclave.get(1)` |
| `Machine_Multi_BlackHoleCompressor` | `ItemList.Machine_Multi_BlackHoleCompressor.get(1)` |
| `Machine_Multi_BlastFurnace` | `ItemList.Machine_Multi_BlastFurnace.get(1)` |
| `Machine_Multi_Canner` | `ItemList.Machine_Multi_Canner.get(1)` |
| `Machine_Multi_Cleanroom` | `ItemList.Machine_Multi_Cleanroom.get(1)` |
| `Machine_Multi_DieselEngine` | `ItemList.Machine_Multi_DieselEngine.get(1)` |
| `Machine_Multi_DroneCentre` | `ItemList.Machine_Multi_DroneCentre.get(1)` |
| `Machine_Multi_ExoFoundry` | `ItemList.Machine_Multi_ExoFoundry.get(1)` |
| `Machine_Multi_ExtremeDieselEngine` | `ItemList.Machine_Multi_ExtremeDieselEngine.get(1)` |
| `Machine_Multi_Furnace` | `ItemList.Machine_Multi_Furnace.get(1)` |
| `Machine_Multi_HIPCompressor` | `ItemList.Machine_Multi_HIPCompressor.get(1)` |
| `Machine_Multi_HeatExchanger` | `ItemList.Machine_Multi_HeatExchanger.get(1)` |
| `Machine_Multi_ImplosionCompressor` | `ItemList.Machine_Multi_ImplosionCompressor.get(1)` |
| `Machine_Multi_IndustrialBrewery` | `ItemList.Machine_Multi_IndustrialBrewery.get(1)` |
| `Machine_Multi_IndustrialCompressor` | `ItemList.Machine_Multi_IndustrialCompressor.get(1)` |
| `Machine_Multi_IndustrialElectromagneticSeparator` | `ItemList.Machine_Multi_IndustrialElectromagneticSeparator.get(1)` |
| `Machine_Multi_IndustrialExtractor` | `ItemList.Machine_Multi_IndustrialExtractor.get(1)` |
| `Machine_Multi_IndustrialLaserEngraver` | `ItemList.Machine_Multi_IndustrialLaserEngraver.get(1)` |
| `Machine_Multi_LargeBoiler_Bronze` | `ItemList.Machine_Multi_LargeBoiler_Bronze.get(1)` |
| `Machine_Multi_LargeBoiler_Steel` | `ItemList.Machine_Multi_LargeBoiler_Steel.get(1)` |
| `Machine_Multi_LargeBoiler_Titanium` | `ItemList.Machine_Multi_LargeBoiler_Titanium.get(1)` |
| `Machine_Multi_LargeBoiler_TungstenSteel` | `ItemList.Machine_Multi_LargeBoiler_TungstenSteel.get(1)` |
| `Machine_Multi_LargeChemicalReactor` | `ItemList.Machine_Multi_LargeChemicalReactor.get(1)` |
| `Machine_Multi_Lathe` | `ItemList.Machine_Multi_Lathe.get(1)` |
| `Machine_Multi_NanochipAssemblyComplex` | `ItemList.Machine_Multi_NanochipAssemblyComplex.get(1)` |
| `Machine_Multi_NeutroniumCompressor` | `ItemList.Machine_Multi_NeutroniumCompressor.get(1)` |
| `Machine_Multi_PlasmaForge` | `ItemList.Machine_Multi_PlasmaForge.get(1)` |
| `Machine_Multi_PurificationPlant` | `ItemList.Machine_Multi_PurificationPlant.get(1)` |
| `Machine_Multi_PurificationUnitClarifier` | `ItemList.Machine_Multi_PurificationUnitClarifier.get(1)` |
| `Machine_Multi_PurificationUnitDegasifier` | `ItemList.Machine_Multi_PurificationUnitDegasifier.get(1)` |
| `Machine_Multi_PurificationUnitFlocculator` | `ItemList.Machine_Multi_PurificationUnitFlocculator.get(1)` |
| `Machine_Multi_PurificationUnitOzonation` | `ItemList.Machine_Multi_PurificationUnitOzonation.get(1)` |
| `Machine_Multi_PurificationUnitParticleExtractor` | `ItemList.Machine_Multi_PurificationUnitParticleExtractor.get(1)` |
| `Machine_Multi_PurificationUnitPhAdjustment` | `ItemList.Machine_Multi_PurificationUnitPhAdjustment.get(1)` |
| `Machine_Multi_PurificationUnitPlasmaHeater` | `ItemList.Machine_Multi_PurificationUnitPlasmaHeater.get(1)` |
| `Machine_Multi_PurificationUnitUVTreatment` | `ItemList.Machine_Multi_PurificationUnitUVTreatment.get(1)` |
| `Machine_Multi_Spinmatron` | `ItemList.Machine_Multi_Spinmatron.get(1)` |
| `Machine_Multi_TranscendentPlasmaMixer` | `ItemList.Machine_Multi_TranscendentPlasmaMixer.get(1)` |
| `Machine_Multi_VacuumFreezer` | `ItemList.Machine_Multi_VacuumFreezer.get(1)` |
| `Machine_Steel_Boiler` | `ItemList.Machine_Steel_Boiler.get(1)` |
| `Machine_Steel_Boiler_Lava` | `ItemList.Machine_Steel_Boiler_Lava.get(1)` |
| `Machine_UV_Boxinator` | `ItemList.Machine_UV_Boxinator.get(1)` |
| `Machine_UV_CircuitAssembler` | `ItemList.Machine_UV_CircuitAssembler.get(1)` |
| `Machine_UV_Printer` | `ItemList.Machine_UV_Printer.get(1)` |
| `Machine_UV_SolarPanel` | `ItemList.Machine_UV_SolarPanel.get(1)` |
| `Machine_UV_Unboxinator` | `ItemList.Machine_UV_Unboxinator.get(1)` |
| `Machine_ZPM_Boxinator` | `ItemList.Machine_ZPM_Boxinator.get(1)` |
| `Machine_ZPM_CircuitAssembler` | `ItemList.Machine_ZPM_CircuitAssembler.get(1)` |
| `Machine_ZPM_Printer` | `ItemList.Machine_ZPM_Printer.get(1)` |
| `Machine_ZPM_SolarPanel` | `ItemList.Machine_ZPM_SolarPanel.get(1)` |
| `Machine_ZPM_Unboxinator` | `ItemList.Machine_ZPM_Unboxinator.get(1)` |

### Category: MagLevHarness

| 枚举键值 | 获取代码 |
|---------|---------|
| `MagLevHarness` | `ItemList.MagLevHarness.get(1)` |

### Category: MagLevPython

| 枚举键值 | 获取代码 |
|---------|---------|
| `MagLevPython_EV` | `ItemList.MagLevPython_EV.get(1)` |
| `MagLevPython_HV` | `ItemList.MagLevPython_HV.get(1)` |
| `MagLevPython_MV` | `ItemList.MagLevPython_MV.get(1)` |

### Category: MagicEnergyAbsorber

| 枚举键值 | 获取代码 |
|---------|---------|
| `MagicEnergyAbsorber_EV` | `ItemList.MagicEnergyAbsorber_EV.get(1)` |
| `MagicEnergyAbsorber_HV` | `ItemList.MagicEnergyAbsorber_HV.get(1)` |
| `MagicEnergyAbsorber_LV` | `ItemList.MagicEnergyAbsorber_LV.get(1)` |
| `MagicEnergyAbsorber_MV` | `ItemList.MagicEnergyAbsorber_MV.get(1)` |

### Category: MagicEnergyConverter

| 枚举键值 | 获取代码 |
|---------|---------|
| `MagicEnergyConverter_HV` | `ItemList.MagicEnergyConverter_HV.get(1)` |
| `MagicEnergyConverter_LV` | `ItemList.MagicEnergyConverter_LV.get(1)` |
| `MagicEnergyConverter_MV` | `ItemList.MagicEnergyConverter_MV.get(1)` |

### Category: Magnetic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Magnetic_Chassis_T1_ExoFoundry` | `ItemList.Magnetic_Chassis_T1_ExoFoundry.get(1)` |
| `Magnetic_Chassis_T2_ExoFoundry` | `ItemList.Magnetic_Chassis_T2_ExoFoundry.get(1)` |
| `Magnetic_Chassis_T3_ExoFoundry` | `ItemList.Magnetic_Chassis_T3_ExoFoundry.get(1)` |

### Category: MagneticAnchorCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `MagneticAnchorCasing` | `ItemList.MagneticAnchorCasing.get(1)` |

### Category: Magnetron

| 枚举键值 | 获取代码 |
|---------|---------|
| `Magnetron` | `ItemList.Magnetron.get(1)` |

### Category: ManaFly

| 枚举键值 | 获取代码 |
|---------|---------|
| `ManaFly` | `ItemList.ManaFly.get(1)` |

### Category: MassFabricatorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorLuV` | `ItemList.MassFabricatorLuV.get(1)` |

### Category: MassFabricatorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorUEV` | `ItemList.MassFabricatorUEV.get(1)` |

### Category: MassFabricatorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorUHV` | `ItemList.MassFabricatorUHV.get(1)` |

### Category: MassFabricatorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorUIV` | `ItemList.MassFabricatorUIV.get(1)` |

### Category: MassFabricatorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorUMV` | `ItemList.MassFabricatorUMV.get(1)` |

### Category: MassFabricatorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorUV` | `ItemList.MassFabricatorUV.get(1)` |

### Category: MassFabricatorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `MassFabricatorZPM` | `ItemList.MassFabricatorZPM.get(1)` |

### Category: McGuffium

| 枚举键值 | 获取代码 |
|---------|---------|
| `McGuffium_239` | `ItemList.McGuffium_239.get(1)` |

### Category: MegaChemicalReactor

| 枚举键值 | 获取代码 |
|---------|---------|
| `MegaChemicalReactor` | `ItemList.MegaChemicalReactor.get(1)` |

### Category: MeshInterfaceNanochipCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `MeshInterfaceNanochipCasing` | `ItemList.MeshInterfaceNanochipCasing.get(1)` |

### Category: MicroTransmitter

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicroTransmitter_EV` | `ItemList.MicroTransmitter_EV.get(1)` |
| `MicroTransmitter_HV` | `ItemList.MicroTransmitter_HV.get(1)` |
| `MicroTransmitter_IV` | `ItemList.MicroTransmitter_IV.get(1)` |
| `MicroTransmitter_LUV` | `ItemList.MicroTransmitter_LUV.get(1)` |
| `MicroTransmitter_UV` | `ItemList.MicroTransmitter_UV.get(1)` |
| `MicroTransmitter_ZPM` | `ItemList.MicroTransmitter_ZPM.get(1)` |

### Category: MicrowaveLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveLuV` | `ItemList.MicrowaveLuV.get(1)` |

### Category: MicrowaveUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveUEV` | `ItemList.MicrowaveUEV.get(1)` |

### Category: MicrowaveUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveUHV` | `ItemList.MicrowaveUHV.get(1)` |

### Category: MicrowaveUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveUIV` | `ItemList.MicrowaveUIV.get(1)` |

### Category: MicrowaveUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveUMV` | `ItemList.MicrowaveUMV.get(1)` |

### Category: MicrowaveUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveUV` | `ItemList.MicrowaveUV.get(1)` |

### Category: MicrowaveZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `MicrowaveZPM` | `ItemList.MicrowaveZPM.get(1)` |

### Category: MiningDroneEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneEV` | `ItemList.MiningDroneEV.get(1)` |

### Category: MiningDroneHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneHV` | `ItemList.MiningDroneHV.get(1)` |

### Category: MiningDroneIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneIV` | `ItemList.MiningDroneIV.get(1)` |

### Category: MiningDroneLV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneLV` | `ItemList.MiningDroneLV.get(1)` |

### Category: MiningDroneLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneLuV` | `ItemList.MiningDroneLuV.get(1)` |

### Category: MiningDroneMAX

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneMAX` | `ItemList.MiningDroneMAX.get(1)` |

### Category: MiningDroneMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneMV` | `ItemList.MiningDroneMV.get(1)` |

### Category: MiningDroneUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUEV` | `ItemList.MiningDroneUEV.get(1)` |

### Category: MiningDroneUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUHV` | `ItemList.MiningDroneUHV.get(1)` |

### Category: MiningDroneUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUIV` | `ItemList.MiningDroneUIV.get(1)` |

### Category: MiningDroneUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUMV` | `ItemList.MiningDroneUMV.get(1)` |

### Category: MiningDroneUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUV` | `ItemList.MiningDroneUV.get(1)` |

### Category: MiningDroneUXV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneUXV` | `ItemList.MiningDroneUXV.get(1)` |

### Category: MiningDroneZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `MiningDroneZPM` | `ItemList.MiningDroneZPM.get(1)` |

### Category: MixerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerLuV` | `ItemList.MixerLuV.get(1)` |

### Category: MixerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerUEV` | `ItemList.MixerUEV.get(1)` |

### Category: MixerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerUHV` | `ItemList.MixerUHV.get(1)` |

### Category: MixerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerUIV` | `ItemList.MixerUIV.get(1)` |

### Category: MixerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerUMV` | `ItemList.MixerUMV.get(1)` |

### Category: MixerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerUV` | `ItemList.MixerUV.get(1)` |

### Category: MixerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `MixerZPM` | `ItemList.MixerZPM.get(1)` |

### Category: MobRep

| 枚举键值 | 获取代码 |
|---------|---------|
| `MobRep_EV` | `ItemList.MobRep_EV.get(1)` |
| `MobRep_HV` | `ItemList.MobRep_HV.get(1)` |
| `MobRep_IV` | `ItemList.MobRep_IV.get(1)` |
| `MobRep_LV` | `ItemList.MobRep_LV.get(1)` |
| `MobRep_LuV` | `ItemList.MobRep_LuV.get(1)` |
| `MobRep_MV` | `ItemList.MobRep_MV.get(1)` |
| `MobRep_UV` | `ItemList.MobRep_UV.get(1)` |
| `MobRep_ZPM` | `ItemList.MobRep_ZPM.get(1)` |

### Category: NC

| 枚举键值 | 获取代码 |
|---------|---------|
| `NC_AdvancedSensorCard` | `ItemList.NC_AdvancedSensorCard.get(1)` |
| `NC_SensorCard` | `ItemList.NC_SensorCard.get(1)` |
| `NC_SensorKit` | `ItemList.NC_SensorKit.get(1)` |

### Category: NULL

| 枚举键值 | 获取代码 |
|---------|---------|
| `NULL` | `ItemList.NULL.get(1)` |

### Category: NameRemover

| 枚举键值 | 获取代码 |
|---------|---------|
| `NameRemover` | `ItemList.NameRemover.get(1)` |

### Category: NandChip

| 枚举键值 | 获取代码 |
|---------|---------|
| `NandChip` | `ItemList.NandChip.get(1)` |

### Category: NandChipArray

| 枚举键值 | 获取代码 |
|---------|---------|
| `NandChipArray` | `ItemList.NandChipArray.get(1)` |

### Category: NaniteFramework

| 枚举键值 | 获取代码 |
|---------|---------|
| `NaniteFramework` | `ItemList.NaniteFramework.get(1)` |

### Category: NaniteShieldingGlass

| 枚举键值 | 获取代码 |
|---------|---------|
| `NaniteShieldingGlass` | `ItemList.NaniteShieldingGlass.get(1)` |

### Category: NanoChipModule

| 枚举键值 | 获取代码 |
|---------|---------|
| `NanoChipModule_AssemblyMatrix` | `ItemList.NanoChipModule_AssemblyMatrix.get(1)` |
| `NanoChipModule_BiologicalCoordinator` | `ItemList.NanoChipModule_BiologicalCoordinator.get(1)` |
| `NanoChipModule_BoardProcessor` | `ItemList.NanoChipModule_BoardProcessor.get(1)` |
| `NanoChipModule_CuttingChamber` | `ItemList.NanoChipModule_CuttingChamber.get(1)` |
| `NanoChipModule_EncasementWrapper` | `ItemList.NanoChipModule_EncasementWrapper.get(1)` |
| `NanoChipModule_EtchingArray` | `ItemList.NanoChipModule_EtchingArray.get(1)` |
| `NanoChipModule_OpticalOrganizer` | `ItemList.NanoChipModule_OpticalOrganizer.get(1)` |
| `NanoChipModule_SMDProcessor` | `ItemList.NanoChipModule_SMDProcessor.get(1)` |
| `NanoChipModule_Splitter` | `ItemList.NanoChipModule_Splitter.get(1)` |
| `NanoChipModule_SuperconductorSplitter` | `ItemList.NanoChipModule_SuperconductorSplitter.get(1)` |
| `NanoChipModule_WireTracer` | `ItemList.NanoChipModule_WireTracer.get(1)` |

### Category: NanoForge

| 枚举键值 | 获取代码 |
|---------|---------|
| `NanoForge` | `ItemList.NanoForge.get(1)` |

### Category: NanotubeSpool

| 枚举键值 | 获取代码 |
|---------|---------|
| `NanotubeSpool` | `ItemList.NanotubeSpool.get(1)` |

### Category: NaquadriaSupersolid

| 枚举键值 | 获取代码 |
|---------|---------|
| `NaquadriaSupersolid` | `ItemList.NaquadriaSupersolid.get(1)` |

### Category: Naquarite

| 枚举键值 | 获取代码 |
|---------|---------|
| `Naquarite_Universal_Insulator_Foil` | `ItemList.Naquarite_Universal_Insulator_Foil.get(1)` |

### Category: Netherite

| 枚举键值 | 获取代码 |
|---------|---------|
| `Netherite_Nanoparticles` | `ItemList.Netherite_Nanoparticles.get(1)` |
| `Netherite_Scrap_Seed` | `ItemList.Netherite_Scrap_Seed.get(1)` |

### Category: Neutron

| 枚举键值 | 获取代码 |
|---------|---------|
| `Neutron_Reflector` | `ItemList.Neutron_Reflector.get(1)` |

### Category: Neutronium

| 枚举键值 | 获取代码 |
|---------|---------|
| `Neutronium_Active_Casing` | `ItemList.Neutronium_Active_Casing.get(1)` |
| `Neutronium_Casing` | `ItemList.Neutronium_Casing.get(1)` |
| `Neutronium_Stable_Casing` | `ItemList.Neutronium_Stable_Casing.get(1)` |

### Category: NtNanofibers

| 枚举键值 | 获取代码 |
|---------|---------|
| `NtNanofibers` | `ItemList.NtNanofibers.get(1)` |

### Category: NtNanoparticles

| 枚举键值 | 获取代码 |
|---------|---------|
| `NtNanoparticles` | `ItemList.NtNanoparticles.get(1)` |

### Category: NuclearStar

| 枚举键值 | 获取代码 |
|---------|---------|
| `NuclearStar` | `ItemList.NuclearStar.get(1)` |

### Category: OilCracker

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilCracker` | `ItemList.OilCracker.get(1)` |

### Category: OilDrill1

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilDrill1` | `ItemList.OilDrill1.get(1)` |

### Category: OilDrill2

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilDrill2` | `ItemList.OilDrill2.get(1)` |

### Category: OilDrill3

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilDrill3` | `ItemList.OilDrill3.get(1)` |

### Category: OilDrill4

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilDrill4` | `ItemList.OilDrill4.get(1)` |

### Category: OilDrillInfinite

| 枚举键值 | 获取代码 |
|---------|---------|
| `OilDrillInfinite` | `ItemList.OilDrillInfinite.get(1)` |

### Category: Optical

| 枚举键值 | 获取代码 |
|---------|---------|
| `Optical_Cpu_Containment_Housing` | `ItemList.Optical_Cpu_Containment_Housing.get(1)` |

### Category: Optically

| 枚举键值 | 获取代码 |
|---------|---------|
| `Optically_Compatible_Memory` | `ItemList.Optically_Compatible_Memory.get(1)` |
| `Optically_Perfected_CPU` | `ItemList.Optically_Perfected_CPU.get(1)` |

### Category: Ore

| 枚举键值 | 获取代码 |
|---------|---------|
| `Ore_Processor` | `ItemList.Ore_Processor.get(1)` |

### Category: OreDrill1

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreDrill1` | `ItemList.OreDrill1.get(1)` |

### Category: OreDrill2

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreDrill2` | `ItemList.OreDrill2.get(1)` |

### Category: OreDrill3

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreDrill3` | `ItemList.OreDrill3.get(1)` |

### Category: OreDrill4

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreDrill4` | `ItemList.OreDrill4.get(1)` |

### Category: OreWashingPlantLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantLuV` | `ItemList.OreWashingPlantLuV.get(1)` |

### Category: OreWashingPlantUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantUEV` | `ItemList.OreWashingPlantUEV.get(1)` |

### Category: OreWashingPlantUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantUHV` | `ItemList.OreWashingPlantUHV.get(1)` |

### Category: OreWashingPlantUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantUIV` | `ItemList.OreWashingPlantUIV.get(1)` |

### Category: OreWashingPlantUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantUMV` | `ItemList.OreWashingPlantUMV.get(1)` |

### Category: OreWashingPlantUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantUV` | `ItemList.OreWashingPlantUV.get(1)` |

### Category: OreWashingPlantZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `OreWashingPlantZPM` | `ItemList.OreWashingPlantZPM.get(1)` |

### Category: PCBBioChamber

| 枚举键值 | 获取代码 |
|---------|---------|
| `PCBBioChamber` | `ItemList.PCBBioChamber.get(1)` |

### Category: PCBCoolingTower

| 枚举键值 | 获取代码 |
|---------|---------|
| `PCBCoolingTower` | `ItemList.PCBCoolingTower.get(1)` |

### Category: PCBFactory

| 枚举键值 | 获取代码 |
|---------|---------|
| `PCBFactory` | `ItemList.PCBFactory.get(1)` |

### Category: Paper

| 枚举键值 | 获取代码 |
|---------|---------|
| `Paper_Magic_Empty` | `ItemList.Paper_Magic_Empty.get(1)` |
| `Paper_Magic_Page` | `ItemList.Paper_Magic_Page.get(1)` |
| `Paper_Magic_Pages` | `ItemList.Paper_Magic_Pages.get(1)` |
| `Paper_Printed_Pages` | `ItemList.Paper_Printed_Pages.get(1)` |
| `Paper_Punch_Card_Empty` | `ItemList.Paper_Punch_Card_Empty.get(1)` |
| `Paper_Punch_Card_Encoded` | `ItemList.Paper_Punch_Card_Encoded.get(1)` |

### Category: Phononic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Phononic_Seed_Crystal` | `ItemList.Phononic_Seed_Crystal.get(1)` |

### Category: PlanetaryGasSiphonCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlanetaryGasSiphonCasing` | `ItemList.PlanetaryGasSiphonCasing.get(1)` |

### Category: PlanetaryGasSiphonController

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlanetaryGasSiphonController` | `ItemList.PlanetaryGasSiphonController.get(1)` |

### Category: Plank

| 枚举键值 | 获取代码 |
|---------|---------|
| `Plank_Acacia` | `ItemList.Plank_Acacia.get(1)` |
| `Plank_Acacia_Green` | `ItemList.Plank_Acacia_Green.get(1)` |
| `Plank_Balsa` | `ItemList.Plank_Balsa.get(1)` |
| `Plank_Baobab` | `ItemList.Plank_Baobab.get(1)` |
| `Plank_Birch` | `ItemList.Plank_Birch.get(1)` |
| `Plank_Cherry` | `ItemList.Plank_Cherry.get(1)` |
| `Plank_Cherry_EFR` | `ItemList.Plank_Cherry_EFR.get(1)` |
| `Plank_Chestnut` | `ItemList.Plank_Chestnut.get(1)` |
| `Plank_Citrus` | `ItemList.Plank_Citrus.get(1)` |
| `Plank_DarkOak` | `ItemList.Plank_DarkOak.get(1)` |
| `Plank_Ebony` | `ItemList.Plank_Ebony.get(1)` |
| `Plank_Greenheart` | `ItemList.Plank_Greenheart.get(1)` |
| `Plank_Jungle` | `ItemList.Plank_Jungle.get(1)` |
| `Plank_Kapok` | `ItemList.Plank_Kapok.get(1)` |
| `Plank_Larch` | `ItemList.Plank_Larch.get(1)` |
| `Plank_Lime` | `ItemList.Plank_Lime.get(1)` |
| `Plank_Mahagony` | `ItemList.Plank_Mahagony.get(1)` |
| `Plank_Mahoe` | `ItemList.Plank_Mahoe.get(1)` |
| `Plank_Maple` | `ItemList.Plank_Maple.get(1)` |
| `Plank_Oak` | `ItemList.Plank_Oak.get(1)` |
| `Plank_Palm` | `ItemList.Plank_Palm.get(1)` |
| `Plank_Papaya` | `ItemList.Plank_Papaya.get(1)` |
| `Plank_Pine` | `ItemList.Plank_Pine.get(1)` |
| `Plank_Plum` | `ItemList.Plank_Plum.get(1)` |
| `Plank_Poplar` | `ItemList.Plank_Poplar.get(1)` |
| `Plank_Sequoia` | `ItemList.Plank_Sequoia.get(1)` |
| `Plank_Spruce` | `ItemList.Plank_Spruce.get(1)` |
| `Plank_Teak` | `ItemList.Plank_Teak.get(1)` |
| `Plank_Walnut` | `ItemList.Plank_Walnut.get(1)` |
| `Plank_Wenge` | `ItemList.Plank_Wenge.get(1)` |
| `Plank_Willow` | `ItemList.Plank_Willow.get(1)` |

### Category: PlasmaArcFurnaceLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceLuV` | `ItemList.PlasmaArcFurnaceLuV.get(1)` |

### Category: PlasmaArcFurnaceUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceUEV` | `ItemList.PlasmaArcFurnaceUEV.get(1)` |

### Category: PlasmaArcFurnaceUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceUHV` | `ItemList.PlasmaArcFurnaceUHV.get(1)` |

### Category: PlasmaArcFurnaceUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceUIV` | `ItemList.PlasmaArcFurnaceUIV.get(1)` |

### Category: PlasmaArcFurnaceUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceUMV` | `ItemList.PlasmaArcFurnaceUMV.get(1)` |

### Category: PlasmaArcFurnaceUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceUV` | `ItemList.PlasmaArcFurnaceUV.get(1)` |

### Category: PlasmaArcFurnaceZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `PlasmaArcFurnaceZPM` | `ItemList.PlasmaArcFurnaceZPM.get(1)` |

### Category: PolarizerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerLuV` | `ItemList.PolarizerLuV.get(1)` |

### Category: PolarizerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerUEV` | `ItemList.PolarizerUEV.get(1)` |

### Category: PolarizerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerUHV` | `ItemList.PolarizerUHV.get(1)` |

### Category: PolarizerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerUIV` | `ItemList.PolarizerUIV.get(1)` |

### Category: PolarizerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerUMV` | `ItemList.PolarizerUMV.get(1)` |

### Category: PolarizerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerUV` | `ItemList.PolarizerUV.get(1)` |

### Category: PolarizerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `PolarizerZPM` | `ItemList.PolarizerZPM.get(1)` |

### Category: Power

| 枚举键值 | 获取代码 |
|---------|---------|
| `Power_Efficient_Subsystems_ExoFoundry` | `ItemList.Power_Efficient_Subsystems_ExoFoundry.get(1)` |

### Category: PrecisionFieldSyncCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionFieldSyncCasing` | `ItemList.PrecisionFieldSyncCasing.get(1)` |

### Category: PrecisionLaserEngraverLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverLuV` | `ItemList.PrecisionLaserEngraverLuV.get(1)` |

### Category: PrecisionLaserEngraverUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverUEV` | `ItemList.PrecisionLaserEngraverUEV.get(1)` |

### Category: PrecisionLaserEngraverUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverUHV` | `ItemList.PrecisionLaserEngraverUHV.get(1)` |

### Category: PrecisionLaserEngraverUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverUIV` | `ItemList.PrecisionLaserEngraverUIV.get(1)` |

### Category: PrecisionLaserEngraverUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverUMV` | `ItemList.PrecisionLaserEngraverUMV.get(1)` |

### Category: PrecisionLaserEngraverUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverUV` | `ItemList.PrecisionLaserEngraverUV.get(1)` |

### Category: PrecisionLaserEngraverZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `PrecisionLaserEngraverZPM` | `ItemList.PrecisionLaserEngraverZPM.get(1)` |

### Category: Primary

| 枚举键值 | 获取代码 |
|---------|---------|
| `Primary_Casing_ExoFoundry` | `ItemList.Primary_Casing_ExoFoundry.get(1)` |

### Category: Prismarine

| 枚举键值 | 获取代码 |
|---------|---------|
| `Prismarine_Precipitate` | `ItemList.Prismarine_Precipitate.get(1)` |

### Category: Prismatic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Prismatic_Crystal` | `ItemList.Prismatic_Crystal.get(1)` |

### Category: Pump

| 枚举键值 | 获取代码 |
|---------|---------|
| `Pump_HV` | `ItemList.Pump_HV.get(1)` |
| `Pump_LV` | `ItemList.Pump_LV.get(1)` |
| `Pump_MV` | `ItemList.Pump_MV.get(1)` |

### Category: PyrolyseOven

| 枚举键值 | 获取代码 |
|---------|---------|
| `PyrolyseOven` | `ItemList.PyrolyseOven.get(1)` |

### Category: Quantum

| 枚举键值 | 获取代码 |
|---------|---------|
| `Quantum_Chest_EV` | `ItemList.Quantum_Chest_EV.get(1)` |
| `Quantum_Chest_HV` | `ItemList.Quantum_Chest_HV.get(1)` |
| `Quantum_Chest_IV` | `ItemList.Quantum_Chest_IV.get(1)` |
| `Quantum_Chest_LV` | `ItemList.Quantum_Chest_LV.get(1)` |
| `Quantum_Chest_MV` | `ItemList.Quantum_Chest_MV.get(1)` |
| `Quantum_Tank_EV` | `ItemList.Quantum_Tank_EV.get(1)` |
| `Quantum_Tank_HV` | `ItemList.Quantum_Tank_HV.get(1)` |
| `Quantum_Tank_IV` | `ItemList.Quantum_Tank_IV.get(1)` |
| `Quantum_Tank_LV` | `ItemList.Quantum_Tank_LV.get(1)` |
| `Quantum_Tank_MV` | `ItemList.Quantum_Tank_MV.get(1)` |

### Category: QuantumEye

| 枚举键值 | 获取代码 |
|---------|---------|
| `QuantumEye` | `ItemList.QuantumEye.get(1)` |

### Category: QuantumStar

| 枚举键值 | 获取代码 |
|---------|---------|
| `QuantumStar` | `ItemList.QuantumStar.get(1)` |

### Category: Quark

| 枚举键值 | 获取代码 |
|---------|---------|
| `Quark_Catalyst_Housing` | `ItemList.Quark_Catalyst_Housing.get(1)` |
| `Quark_Creation_Catalyst_Bottom` | `ItemList.Quark_Creation_Catalyst_Bottom.get(1)` |
| `Quark_Creation_Catalyst_Charm` | `ItemList.Quark_Creation_Catalyst_Charm.get(1)` |
| `Quark_Creation_Catalyst_Down` | `ItemList.Quark_Creation_Catalyst_Down.get(1)` |
| `Quark_Creation_Catalyst_Strange` | `ItemList.Quark_Creation_Catalyst_Strange.get(1)` |
| `Quark_Creation_Catalyst_Top` | `ItemList.Quark_Creation_Catalyst_Top.get(1)` |
| `Quark_Creation_Catalyst_Unaligned` | `ItemList.Quark_Creation_Catalyst_Unaligned.get(1)` |
| `Quark_Creation_Catalyst_Up` | `ItemList.Quark_Creation_Catalyst_Up.get(1)` |

### Category: RC

| 枚举键值 | 获取代码 |
|---------|---------|
| `RC_Bed_Stone` | `ItemList.RC_Bed_Stone.get(1)` |
| `RC_Bed_Wood` | `ItemList.RC_Bed_Wood.get(1)` |
| `RC_Rail_Adv` | `ItemList.RC_Rail_Adv.get(1)` |
| `RC_Rail_Electric` | `ItemList.RC_Rail_Electric.get(1)` |
| `RC_Rail_HS` | `ItemList.RC_Rail_HS.get(1)` |
| `RC_Rail_Reinforced` | `ItemList.RC_Rail_Reinforced.get(1)` |
| `RC_Rail_Standard` | `ItemList.RC_Rail_Standard.get(1)` |
| `RC_Rail_Wooden` | `ItemList.RC_Rail_Wooden.get(1)` |
| `RC_Rebar` | `ItemList.RC_Rebar.get(1)` |
| `RC_ShuntingWire` | `ItemList.RC_ShuntingWire.get(1)` |
| `RC_ShuntingWireFrame` | `ItemList.RC_ShuntingWireFrame.get(1)` |
| `RC_Tie_Stone` | `ItemList.RC_Tie_Stone.get(1)` |
| `RC_Tie_Wood` | `ItemList.RC_Tie_Wood.get(1)` |

### Category: RadiantNaquadahAlloyCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `RadiantNaquadahAlloyCasing` | `ItemList.RadiantNaquadahAlloyCasing.get(1)` |

### Category: Radiation

| 枚举键值 | 获取代码 |
|---------|---------|
| `Radiation_Proof_Prismatic_Naquadah_Composite_Sheet` | `ItemList.Radiation_Proof_Prismatic_Naquadah_Composite_Sheet.get(1)` |

### Category: RadiationProofPhotolithographicFrameworkCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `RadiationProofPhotolithographicFrameworkCasing` | `ItemList.RadiationProofPhotolithographicFrameworkCasing.get(1)` |

### Category: Radiator

| 枚举键值 | 获取代码 |
|---------|---------|
| `Radiator_Fluid_Solidifier` | `ItemList.Radiator_Fluid_Solidifier.get(1)` |

### Category: RawImprintBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `RawImprintBoard` | `ItemList.RawImprintBoard.get(1)` |

### Category: Reactor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Reactor_Coolant_He_1` | `ItemList.Reactor_Coolant_He_1.get(1)` |
| `Reactor_Coolant_He_3` | `ItemList.Reactor_Coolant_He_3.get(1)` |
| `Reactor_Coolant_He_6` | `ItemList.Reactor_Coolant_He_6.get(1)` |
| `Reactor_Coolant_NaK_1` | `ItemList.Reactor_Coolant_NaK_1.get(1)` |
| `Reactor_Coolant_NaK_3` | `ItemList.Reactor_Coolant_NaK_3.get(1)` |
| `Reactor_Coolant_NaK_6` | `ItemList.Reactor_Coolant_NaK_6.get(1)` |
| `Reactor_Coolant_Sp_1` | `ItemList.Reactor_Coolant_Sp_1.get(1)` |
| `Reactor_Coolant_Sp_2` | `ItemList.Reactor_Coolant_Sp_2.get(1)` |
| `Reactor_Coolant_Sp_3` | `ItemList.Reactor_Coolant_Sp_3.get(1)` |
| `Reactor_Coolant_Sp_6` | `ItemList.Reactor_Coolant_Sp_6.get(1)` |
| `Reactor_NeutronReflector` | `ItemList.Reactor_NeutronReflector.get(1)` |

### Category: ReceiverCircuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReceiverCircuit` | `ItemList.ReceiverCircuit.get(1)` |

### Category: RecyclerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerLuV` | `ItemList.RecyclerLuV.get(1)` |

### Category: RecyclerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerUEV` | `ItemList.RecyclerUEV.get(1)` |

### Category: RecyclerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerUHV` | `ItemList.RecyclerUHV.get(1)` |

### Category: RecyclerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerUIV` | `ItemList.RecyclerUIV.get(1)` |

### Category: RecyclerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerUMV` | `ItemList.RecyclerUMV.get(1)` |

### Category: RecyclerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerUV` | `ItemList.RecyclerUV.get(1)` |

### Category: RecyclerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `RecyclerZPM` | `ItemList.RecyclerZPM.get(1)` |

### Category: RefinedCircuitBoard

| 枚举键值 | 获取代码 |
|---------|---------|
| `RefinedCircuitBoard` | `ItemList.RefinedCircuitBoard.get(1)` |

### Category: ReinforcedPhotolithographicFrameworkCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReinforcedPhotolithographicFrameworkCasing` | `ItemList.ReinforcedPhotolithographicFrameworkCasing.get(1)` |

### Category: ReinforcementNanochipCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReinforcementNanochipCasing` | `ItemList.ReinforcementNanochipCasing.get(1)` |

### Category: Relativistic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Relativistic_Heat_Capacitor` | `ItemList.Relativistic_Heat_Capacitor.get(1)` |

### Category: ReplicatorLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorLuV` | `ItemList.ReplicatorLuV.get(1)` |

### Category: ReplicatorUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorUEV` | `ItemList.ReplicatorUEV.get(1)` |

### Category: ReplicatorUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorUHV` | `ItemList.ReplicatorUHV.get(1)` |

### Category: ReplicatorUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorUIV` | `ItemList.ReplicatorUIV.get(1)` |

### Category: ReplicatorUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorUMV` | `ItemList.ReplicatorUMV.get(1)` |

### Category: ReplicatorUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorUV` | `ItemList.ReplicatorUV.get(1)` |

### Category: ReplicatorZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ReplicatorZPM` | `ItemList.ReplicatorZPM.get(1)` |

### Category: ResearchCompleter

| 枚举键值 | 获取代码 |
|---------|---------|
| `ResearchCompleter` | `ItemList.ResearchCompleter.get(1)` |

### Category: Robot

| 枚举键值 | 获取代码 |
|---------|---------|
| `Robot_Arm_EV` | `ItemList.Robot_Arm_EV.get(1)` |
| `Robot_Arm_HV` | `ItemList.Robot_Arm_HV.get(1)` |
| `Robot_Arm_IV` | `ItemList.Robot_Arm_IV.get(1)` |
| `Robot_Arm_LV` | `ItemList.Robot_Arm_LV.get(1)` |
| `Robot_Arm_LuV` | `ItemList.Robot_Arm_LuV.get(1)` |
| `Robot_Arm_MAX` | `ItemList.Robot_Arm_MAX.get(1)` |
| `Robot_Arm_MV` | `ItemList.Robot_Arm_MV.get(1)` |
| `Robot_Arm_UEV` | `ItemList.Robot_Arm_UEV.get(1)` |
| `Robot_Arm_UHV` | `ItemList.Robot_Arm_UHV.get(1)` |
| `Robot_Arm_UIV` | `ItemList.Robot_Arm_UIV.get(1)` |
| `Robot_Arm_UMV` | `ItemList.Robot_Arm_UMV.get(1)` |
| `Robot_Arm_UV` | `ItemList.Robot_Arm_UV.get(1)` |
| `Robot_Arm_UXV` | `ItemList.Robot_Arm_UXV.get(1)` |
| `Robot_Arm_ZPM` | `ItemList.Robot_Arm_ZPM.get(1)` |

### Category: RockBreakerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerLuV` | `ItemList.RockBreakerLuV.get(1)` |

### Category: RockBreakerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerUEV` | `ItemList.RockBreakerUEV.get(1)` |

### Category: RockBreakerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerUHV` | `ItemList.RockBreakerUHV.get(1)` |

### Category: RockBreakerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerUIV` | `ItemList.RockBreakerUIV.get(1)` |

### Category: RockBreakerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerUMV` | `ItemList.RockBreakerUMV.get(1)` |

### Category: RockBreakerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerUV` | `ItemList.RockBreakerUV.get(1)` |

### Category: RockBreakerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `RockBreakerZPM` | `ItemList.RockBreakerZPM.get(1)` |

### Category: RodExcitedPlutonium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedPlutonium` | `ItemList.RodExcitedPlutonium.get(1)` |

### Category: RodExcitedPlutonium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedPlutonium2` | `ItemList.RodExcitedPlutonium2.get(1)` |

### Category: RodExcitedPlutonium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedPlutonium4` | `ItemList.RodExcitedPlutonium4.get(1)` |

### Category: RodExcitedUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedUranium` | `ItemList.RodExcitedUranium.get(1)` |

### Category: RodExcitedUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedUranium2` | `ItemList.RodExcitedUranium2.get(1)` |

### Category: RodExcitedUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodExcitedUranium4` | `ItemList.RodExcitedUranium4.get(1)` |

### Category: RodGlowstone

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodGlowstone` | `ItemList.RodGlowstone.get(1)` |

### Category: RodHighDensityPlutonium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityPlutonium` | `ItemList.RodHighDensityPlutonium.get(1)` |

### Category: RodHighDensityPlutonium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityPlutonium2` | `ItemList.RodHighDensityPlutonium2.get(1)` |

### Category: RodHighDensityPlutonium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityPlutonium4` | `ItemList.RodHighDensityPlutonium4.get(1)` |

### Category: RodHighDensityUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityUranium` | `ItemList.RodHighDensityUranium.get(1)` |

### Category: RodHighDensityUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityUranium2` | `ItemList.RodHighDensityUranium2.get(1)` |

### Category: RodHighDensityUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodHighDensityUranium4` | `ItemList.RodHighDensityUranium4.get(1)` |

### Category: RodLithium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodLithium` | `ItemList.RodLithium.get(1)` |

### Category: RodMOX

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodMOX` | `ItemList.RodMOX.get(1)` |

### Category: RodMOX2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodMOX2` | `ItemList.RodMOX2.get(1)` |

### Category: RodMOX4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodMOX4` | `ItemList.RodMOX4.get(1)` |

### Category: RodNaquadah

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadah` | `ItemList.RodNaquadah.get(1)` |

### Category: RodNaquadah2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadah2` | `ItemList.RodNaquadah2.get(1)` |

### Category: RodNaquadah32

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadah32` | `ItemList.RodNaquadah32.get(1)` |

### Category: RodNaquadah4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadah4` | `ItemList.RodNaquadah4.get(1)` |

### Category: RodNaquadria

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadria` | `ItemList.RodNaquadria.get(1)` |

### Category: RodNaquadria2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadria2` | `ItemList.RodNaquadria2.get(1)` |

### Category: RodNaquadria4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodNaquadria4` | `ItemList.RodNaquadria4.get(1)` |

### Category: RodThorium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodThorium` | `ItemList.RodThorium.get(1)` |

### Category: RodThorium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodThorium2` | `ItemList.RodThorium2.get(1)` |

### Category: RodThorium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodThorium4` | `ItemList.RodThorium4.get(1)` |

### Category: RodTiberium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodTiberium` | `ItemList.RodTiberium.get(1)` |

### Category: RodTiberium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodTiberium2` | `ItemList.RodTiberium2.get(1)` |

### Category: RodTiberium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodTiberium4` | `ItemList.RodTiberium4.get(1)` |

### Category: RodUranium

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodUranium` | `ItemList.RodUranium.get(1)` |

### Category: RodUranium2

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodUranium2` | `ItemList.RodUranium2.get(1)` |

### Category: RodUranium4

| 枚举键值 | 获取代码 |
|---------|---------|
| `RodUranium4` | `ItemList.RodUranium4.get(1)` |

### Category: Rotor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Rotor_EV` | `ItemList.Rotor_EV.get(1)` |
| `Rotor_HV` | `ItemList.Rotor_HV.get(1)` |
| `Rotor_IV` | `ItemList.Rotor_IV.get(1)` |
| `Rotor_LV` | `ItemList.Rotor_LV.get(1)` |
| `Rotor_MV` | `ItemList.Rotor_MV.get(1)` |

### Category: SFMixture

| 枚举键值 | 获取代码 |
|---------|---------|
| `SFMixture` | `ItemList.SFMixture.get(1)` |

### Category: ScannerLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerLuV` | `ItemList.ScannerLuV.get(1)` |

### Category: ScannerUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerUEV` | `ItemList.ScannerUEV.get(1)` |

### Category: ScannerUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerUHV` | `ItemList.ScannerUHV.get(1)` |

### Category: ScannerUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerUIV` | `ItemList.ScannerUIV.get(1)` |

### Category: ScannerUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerUMV` | `ItemList.ScannerUMV.get(1)` |

### Category: ScannerUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerUV` | `ItemList.ScannerUV.get(1)` |

### Category: ScannerZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ScannerZPM` | `ItemList.ScannerZPM.get(1)` |

### Category: Schematic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Schematic` | `ItemList.Schematic.get(1)` |
| `Schematic_1by1` | `ItemList.Schematic_1by1.get(1)` |
| `Schematic_2by2` | `ItemList.Schematic_2by2.get(1)` |
| `Schematic_3by3` | `ItemList.Schematic_3by3.get(1)` |
| `Schematic_Crafting` | `ItemList.Schematic_Crafting.get(1)` |
| `Schematic_Dust` | `ItemList.Schematic_Dust.get(1)` |
| `Schematic_Dust_Small` | `ItemList.Schematic_Dust_Small.get(1)` |

### Category: Secondary

| 枚举键值 | 获取代码 |
|---------|---------|
| `Secondary_Casing_ExoFoundry` | `ItemList.Secondary_Casing_ExoFoundry.get(1)` |

### Category: Seismic

| 枚举键值 | 获取代码 |
|---------|---------|
| `Seismic_Prospector_Adv_EV` | `ItemList.Seismic_Prospector_Adv_EV.get(1)` |
| `Seismic_Prospector_Adv_HV` | `ItemList.Seismic_Prospector_Adv_HV.get(1)` |
| `Seismic_Prospector_Adv_LV` | `ItemList.Seismic_Prospector_Adv_LV.get(1)` |
| `Seismic_Prospector_Adv_MV` | `ItemList.Seismic_Prospector_Adv_MV.get(1)` |

### Category: Sensor

| 枚举键值 | 获取代码 |
|---------|---------|
| `Sensor_EV` | `ItemList.Sensor_EV.get(1)` |
| `Sensor_HV` | `ItemList.Sensor_HV.get(1)` |
| `Sensor_IV` | `ItemList.Sensor_IV.get(1)` |
| `Sensor_LV` | `ItemList.Sensor_LV.get(1)` |
| `Sensor_LuV` | `ItemList.Sensor_LuV.get(1)` |
| `Sensor_MAX` | `ItemList.Sensor_MAX.get(1)` |
| `Sensor_MV` | `ItemList.Sensor_MV.get(1)` |
| `Sensor_UEV` | `ItemList.Sensor_UEV.get(1)` |
| `Sensor_UHV` | `ItemList.Sensor_UHV.get(1)` |
| `Sensor_UIV` | `ItemList.Sensor_UIV.get(1)` |
| `Sensor_UMV` | `ItemList.Sensor_UMV.get(1)` |
| `Sensor_UV` | `ItemList.Sensor_UV.get(1)` |
| `Sensor_UXV` | `ItemList.Sensor_UXV.get(1)` |
| `Sensor_ZPM` | `ItemList.Sensor_ZPM.get(1)` |

### Category: Shape

| 枚举键值 | 获取代码 |
|---------|---------|
| `Shape_Empty` | `ItemList.Shape_Empty.get(1)` |
| `Shape_Extruder_Axe` | `ItemList.Shape_Extruder_Axe.get(1)` |
| `Shape_Extruder_Block` | `ItemList.Shape_Extruder_Block.get(1)` |
| `Shape_Extruder_Bolt` | `ItemList.Shape_Extruder_Bolt.get(1)` |
| `Shape_Extruder_Bottle` | `ItemList.Shape_Extruder_Bottle.get(1)` |
| `Shape_Extruder_Casing` | `ItemList.Shape_Extruder_Casing.get(1)` |
| `Shape_Extruder_Cell` | `ItemList.Shape_Extruder_Cell.get(1)` |
| `Shape_Extruder_File` | `ItemList.Shape_Extruder_File.get(1)` |
| `Shape_Extruder_Gear` | `ItemList.Shape_Extruder_Gear.get(1)` |
| `Shape_Extruder_Hammer` | `ItemList.Shape_Extruder_Hammer.get(1)` |
| `Shape_Extruder_Hoe` | `ItemList.Shape_Extruder_Hoe.get(1)` |
| `Shape_Extruder_Ingot` | `ItemList.Shape_Extruder_Ingot.get(1)` |
| `Shape_Extruder_Pickaxe` | `ItemList.Shape_Extruder_Pickaxe.get(1)` |
| `Shape_Extruder_Pipe_Huge` | `ItemList.Shape_Extruder_Pipe_Huge.get(1)` |
| `Shape_Extruder_Pipe_Large` | `ItemList.Shape_Extruder_Pipe_Large.get(1)` |
| `Shape_Extruder_Pipe_Medium` | `ItemList.Shape_Extruder_Pipe_Medium.get(1)` |
| `Shape_Extruder_Pipe_Small` | `ItemList.Shape_Extruder_Pipe_Small.get(1)` |
| `Shape_Extruder_Pipe_Tiny` | `ItemList.Shape_Extruder_Pipe_Tiny.get(1)` |
| `Shape_Extruder_Plate` | `ItemList.Shape_Extruder_Plate.get(1)` |
| `Shape_Extruder_Ring` | `ItemList.Shape_Extruder_Ring.get(1)` |
| `Shape_Extruder_Rod` | `ItemList.Shape_Extruder_Rod.get(1)` |
| `Shape_Extruder_Rotor` | `ItemList.Shape_Extruder_Rotor.get(1)` |
| `Shape_Extruder_Saw` | `ItemList.Shape_Extruder_Saw.get(1)` |
| `Shape_Extruder_Shovel` | `ItemList.Shape_Extruder_Shovel.get(1)` |
| `Shape_Extruder_Small_Gear` | `ItemList.Shape_Extruder_Small_Gear.get(1)` |
| `Shape_Extruder_Sword` | `ItemList.Shape_Extruder_Sword.get(1)` |
| `Shape_Extruder_ToolHeadDrill` | `ItemList.Shape_Extruder_ToolHeadDrill.get(1)` |
| `Shape_Extruder_Turbine_Blade` | `ItemList.Shape_Extruder_Turbine_Blade.get(1)` |
| `Shape_Extruder_Wire` | `ItemList.Shape_Extruder_Wire.get(1)` |
| `Shape_Mold_Anvil` | `ItemList.Shape_Mold_Anvil.get(1)` |
| `Shape_Mold_Arrow` | `ItemList.Shape_Mold_Arrow.get(1)` |
| `Shape_Mold_Baguette` | `ItemList.Shape_Mold_Baguette.get(1)` |
| `Shape_Mold_Ball` | `ItemList.Shape_Mold_Ball.get(1)` |
| `Shape_Mold_Block` | `ItemList.Shape_Mold_Block.get(1)` |
| `Shape_Mold_Bolt` | `ItemList.Shape_Mold_Bolt.get(1)` |
| `Shape_Mold_Bottle` | `ItemList.Shape_Mold_Bottle.get(1)` |
| `Shape_Mold_Bread` | `ItemList.Shape_Mold_Bread.get(1)` |
| `Shape_Mold_Bun` | `ItemList.Shape_Mold_Bun.get(1)` |
| `Shape_Mold_Casing` | `ItemList.Shape_Mold_Casing.get(1)` |
| `Shape_Mold_Credit` | `ItemList.Shape_Mold_Credit.get(1)` |
| `Shape_Mold_Cylinder` | `ItemList.Shape_Mold_Cylinder.get(1)` |
| `Shape_Mold_Gear` | `ItemList.Shape_Mold_Gear.get(1)` |
| `Shape_Mold_Gear_Small` | `ItemList.Shape_Mold_Gear_Small.get(1)` |
| `Shape_Mold_Ingot` | `ItemList.Shape_Mold_Ingot.get(1)` |
| `Shape_Mold_Name` | `ItemList.Shape_Mold_Name.get(1)` |
| `Shape_Mold_Nugget` | `ItemList.Shape_Mold_Nugget.get(1)` |
| `Shape_Mold_Pipe_Huge` | `ItemList.Shape_Mold_Pipe_Huge.get(1)` |
| `Shape_Mold_Pipe_Large` | `ItemList.Shape_Mold_Pipe_Large.get(1)` |
| `Shape_Mold_Pipe_Medium` | `ItemList.Shape_Mold_Pipe_Medium.get(1)` |
| `Shape_Mold_Pipe_Small` | `ItemList.Shape_Mold_Pipe_Small.get(1)` |
| `Shape_Mold_Pipe_Tiny` | `ItemList.Shape_Mold_Pipe_Tiny.get(1)` |
| `Shape_Mold_Plate` | `ItemList.Shape_Mold_Plate.get(1)` |
| `Shape_Mold_Ring` | `ItemList.Shape_Mold_Ring.get(1)` |
| `Shape_Mold_Rod` | `ItemList.Shape_Mold_Rod.get(1)` |
| `Shape_Mold_Rod_Long` | `ItemList.Shape_Mold_Rod_Long.get(1)` |
| `Shape_Mold_Rotor` | `ItemList.Shape_Mold_Rotor.get(1)` |
| `Shape_Mold_Round` | `ItemList.Shape_Mold_Round.get(1)` |
| `Shape_Mold_Screw` | `ItemList.Shape_Mold_Screw.get(1)` |
| `Shape_Mold_ToolHeadDrill` | `ItemList.Shape_Mold_ToolHeadDrill.get(1)` |
| `Shape_Mold_Turbine_Blade` | `ItemList.Shape_Mold_Turbine_Blade.get(1)` |
| `Shape_Slicer_Flat` | `ItemList.Shape_Slicer_Flat.get(1)` |
| `Shape_Slicer_Stripes` | `ItemList.Shape_Slicer_Stripes.get(1)` |

### Category: SiftingMachineLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineLuV` | `ItemList.SiftingMachineLuV.get(1)` |

### Category: SiftingMachineUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineUEV` | `ItemList.SiftingMachineUEV.get(1)` |

### Category: SiftingMachineUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineUHV` | `ItemList.SiftingMachineUHV.get(1)` |

### Category: SiftingMachineUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineUIV` | `ItemList.SiftingMachineUIV.get(1)` |

### Category: SiftingMachineUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineUMV` | `ItemList.SiftingMachineUMV.get(1)` |

### Category: SiftingMachineUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineUV` | `ItemList.SiftingMachineUV.get(1)` |

### Category: SiftingMachineZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `SiftingMachineZPM` | `ItemList.SiftingMachineZPM.get(1)` |

### Category: SignalCircuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `SignalCircuit` | `ItemList.SignalCircuit.get(1)` |

### Category: SlicedCircuit

| 枚举键值 | 获取代码 |
|---------|---------|
| `SlicedCircuit_AdvancedCircuit` | `ItemList.SlicedCircuit_AdvancedCircuit.get(1)` |
| `SlicedCircuit_BasicCircuitBoard` | `ItemList.SlicedCircuit_BasicCircuitBoard.get(1)` |
| `SlicedCircuit_BiowareAssembly` | `ItemList.SlicedCircuit_BiowareAssembly.get(1)` |
| `SlicedCircuit_BiowareProcessor` | `ItemList.SlicedCircuit_BiowareProcessor.get(1)` |
| `SlicedCircuit_ControllerCircuit` | `ItemList.SlicedCircuit_ControllerCircuit.get(1)` |
| `SlicedCircuit_CrystalAssembly` | `ItemList.SlicedCircuit_CrystalAssembly.get(1)` |
| `SlicedCircuit_CrystalMainframe` | `ItemList.SlicedCircuit_CrystalMainframe.get(1)` |
| `SlicedCircuit_CrystalProcessor` | `ItemList.SlicedCircuit_CrystalProcessor.get(1)` |
| `SlicedCircuit_CrystalSupercomputer` | `ItemList.SlicedCircuit_CrystalSupercomputer.get(1)` |
| `SlicedCircuit_ElectronicCircuit` | `ItemList.SlicedCircuit_ElectronicCircuit.get(1)` |
| `SlicedCircuit_EnhancedCircuitBoard` | `ItemList.SlicedCircuit_EnhancedCircuitBoard.get(1)` |
| `SlicedCircuit_GoodElectronicCircuit` | `ItemList.SlicedCircuit_GoodElectronicCircuit.get(1)` |
| `SlicedCircuit_GoodIntegratedCircuit` | `ItemList.SlicedCircuit_GoodIntegratedCircuit.get(1)` |
| `SlicedCircuit_HighEnergyFlowCircuit` | `ItemList.SlicedCircuit_HighEnergyFlowCircuit.get(1)` |
| `SlicedCircuit_IntegratedLogicCircuit` | `ItemList.SlicedCircuit_IntegratedLogicCircuit.get(1)` |
| `SlicedCircuit_IntegratedProcessor` | `ItemList.SlicedCircuit_IntegratedProcessor.get(1)` |
| `SlicedCircuit_IntricateCircuitBoard` | `ItemList.SlicedCircuit_IntricateCircuitBoard.get(1)` |
| `SlicedCircuit_Mainframe` | `ItemList.SlicedCircuit_Mainframe.get(1)` |
| `SlicedCircuit_Microprocessor` | `ItemList.SlicedCircuit_Microprocessor.get(1)` |
| `SlicedCircuit_NANDChipArray` | `ItemList.SlicedCircuit_NANDChipArray.get(1)` |
| `SlicedCircuit_NanoAssembly` | `ItemList.SlicedCircuit_NanoAssembly.get(1)` |
| `SlicedCircuit_NanoMainframe` | `ItemList.SlicedCircuit_NanoMainframe.get(1)` |
| `SlicedCircuit_NanoProcessor` | `ItemList.SlicedCircuit_NanoProcessor.get(1)` |
| `SlicedCircuit_NanoSupercomputer` | `ItemList.SlicedCircuit_NanoSupercomputer.get(1)` |
| `SlicedCircuit_OpticalProcessor` | `ItemList.SlicedCircuit_OpticalProcessor.get(1)` |
| `SlicedCircuit_ProcessorAssembly` | `ItemList.SlicedCircuit_ProcessorAssembly.get(1)` |
| `SlicedCircuit_QuantumAssembly` | `ItemList.SlicedCircuit_QuantumAssembly.get(1)` |
| `SlicedCircuit_QuantumMainframe` | `ItemList.SlicedCircuit_QuantumMainframe.get(1)` |
| `SlicedCircuit_QuantumProcessor` | `ItemList.SlicedCircuit_QuantumProcessor.get(1)` |
| `SlicedCircuit_QuantumSupercomputer` | `ItemList.SlicedCircuit_QuantumSupercomputer.get(1)` |
| `SlicedCircuit_ReceiverCircuit` | `ItemList.SlicedCircuit_ReceiverCircuit.get(1)` |
| `SlicedCircuit_RefinedCircuitBoard` | `ItemList.SlicedCircuit_RefinedCircuitBoard.get(1)` |
| `SlicedCircuit_SignalCircuit` | `ItemList.SlicedCircuit_SignalCircuit.get(1)` |
| `SlicedCircuit_WetwareAssembly` | `ItemList.SlicedCircuit_WetwareAssembly.get(1)` |
| `SlicedCircuit_WetwareProcessor` | `ItemList.SlicedCircuit_WetwareProcessor.get(1)` |
| `SlicedCircuit_WetwareSupercomputer` | `ItemList.SlicedCircuit_WetwareSupercomputer.get(1)` |
| `SlicedCircuit_Workstation` | `ItemList.SlicedCircuit_Workstation.get(1)` |

### Category: SolarFactory

| 枚举键值 | 获取代码 |
|---------|---------|
| `SolarFactory` | `ItemList.SolarFactory.get(1)` |

### Category: SpaceElevatorBaseCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorBaseCasing` | `ItemList.SpaceElevatorBaseCasing.get(1)` |

### Category: SpaceElevatorCable

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorCable` | `ItemList.SpaceElevatorCable.get(1)` |

### Category: SpaceElevatorController

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorController` | `ItemList.SpaceElevatorController.get(1)` |

### Category: SpaceElevatorInternalStructure

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorInternalStructure` | `ItemList.SpaceElevatorInternalStructure.get(1)` |

### Category: SpaceElevatorModuleAssemblerT1

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleAssemblerT1` | `ItemList.SpaceElevatorModuleAssemblerT1.get(1)` |

### Category: SpaceElevatorModuleAssemblerT2

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleAssemblerT2` | `ItemList.SpaceElevatorModuleAssemblerT2.get(1)` |

### Category: SpaceElevatorModuleAssemblerT3

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleAssemblerT3` | `ItemList.SpaceElevatorModuleAssemblerT3.get(1)` |

### Category: SpaceElevatorModuleManager

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleManager` | `ItemList.SpaceElevatorModuleManager.get(1)` |

### Category: SpaceElevatorModuleMinerT1

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleMinerT1` | `ItemList.SpaceElevatorModuleMinerT1.get(1)` |

### Category: SpaceElevatorModuleMinerT2

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleMinerT2` | `ItemList.SpaceElevatorModuleMinerT2.get(1)` |

### Category: SpaceElevatorModuleMinerT3

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleMinerT3` | `ItemList.SpaceElevatorModuleMinerT3.get(1)` |

### Category: SpaceElevatorModulePumpT1

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModulePumpT1` | `ItemList.SpaceElevatorModulePumpT1.get(1)` |

### Category: SpaceElevatorModulePumpT2

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModulePumpT2` | `ItemList.SpaceElevatorModulePumpT2.get(1)` |

### Category: SpaceElevatorModulePumpT3

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModulePumpT3` | `ItemList.SpaceElevatorModulePumpT3.get(1)` |

### Category: SpaceElevatorModuleResearch

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorModuleResearch` | `ItemList.SpaceElevatorModuleResearch.get(1)` |

### Category: SpaceElevatorMotorT1

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorMotorT1` | `ItemList.SpaceElevatorMotorT1.get(1)` |

### Category: SpaceElevatorMotorT2

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorMotorT2` | `ItemList.SpaceElevatorMotorT2.get(1)` |

### Category: SpaceElevatorMotorT3

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorMotorT3` | `ItemList.SpaceElevatorMotorT3.get(1)` |

### Category: SpaceElevatorMotorT4

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorMotorT4` | `ItemList.SpaceElevatorMotorT4.get(1)` |

### Category: SpaceElevatorMotorT5

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorMotorT5` | `ItemList.SpaceElevatorMotorT5.get(1)` |

### Category: SpaceElevatorSupportStructure

| 枚举键值 | 获取代码 |
|---------|---------|
| `SpaceElevatorSupportStructure` | `ItemList.SpaceElevatorSupportStructure.get(1)` |

### Category: Spinmatron

| 枚举键值 | 获取代码 |
|---------|---------|
| `Spinmatron_Casing` | `ItemList.Spinmatron_Casing.get(1)` |
| `Spinmatron_Chamber_Grate` | `ItemList.Spinmatron_Chamber_Grate.get(1)` |

### Category: Spinneret

| 枚举键值 | 获取代码 |
|---------|---------|
| `Spinneret` | `ItemList.Spinneret.get(1)` |

### Category: Spray

| 枚举键值 | 获取代码 |
|---------|---------|
| `Spray_Bug` | `ItemList.Spray_Bug.get(1)` |
| `Spray_CFoam` | `ItemList.Spray_CFoam.get(1)` |
| `Spray_Color_00` | `ItemList.Spray_Color_00.get(1)` |
| `Spray_Color_01` | `ItemList.Spray_Color_01.get(1)` |
| `Spray_Color_02` | `ItemList.Spray_Color_02.get(1)` |
| `Spray_Color_03` | `ItemList.Spray_Color_03.get(1)` |
| `Spray_Color_04` | `ItemList.Spray_Color_04.get(1)` |
| `Spray_Color_05` | `ItemList.Spray_Color_05.get(1)` |
| `Spray_Color_05` | `ItemList.Spray_Color_05.get(1)` |
| `Spray_Color_06` | `ItemList.Spray_Color_06.get(1)` |
| `Spray_Color_07` | `ItemList.Spray_Color_07.get(1)` |
| `Spray_Color_08` | `ItemList.Spray_Color_08.get(1)` |
| `Spray_Color_09` | `ItemList.Spray_Color_09.get(1)` |
| `Spray_Color_10` | `ItemList.Spray_Color_10.get(1)` |
| `Spray_Color_11` | `ItemList.Spray_Color_11.get(1)` |
| `Spray_Color_11` | `ItemList.Spray_Color_11.get(1)` |
| `Spray_Color_12` | `ItemList.Spray_Color_12.get(1)` |
| `Spray_Color_13` | `ItemList.Spray_Color_13.get(1)` |
| `Spray_Color_14` | `ItemList.Spray_Color_14.get(1)` |
| `Spray_Color_15` | `ItemList.Spray_Color_15.get(1)` |
| `Spray_Color_Infinite` | `ItemList.Spray_Color_Infinite.get(1)` |
| `Spray_Color_Remover` | `ItemList.Spray_Color_Remover.get(1)` |
| `Spray_Color_Remover_Empty` | `ItemList.Spray_Color_Remover_Empty.get(1)` |
| `Spray_Color_Used_00` | `ItemList.Spray_Color_Used_00.get(1)` |
| `Spray_Color_Used_01` | `ItemList.Spray_Color_Used_01.get(1)` |
| `Spray_Color_Used_02` | `ItemList.Spray_Color_Used_02.get(1)` |
| `Spray_Color_Used_03` | `ItemList.Spray_Color_Used_03.get(1)` |
| `Spray_Color_Used_04` | `ItemList.Spray_Color_Used_04.get(1)` |
| `Spray_Color_Used_04` | `ItemList.Spray_Color_Used_04.get(1)` |
| `Spray_Color_Used_05` | `ItemList.Spray_Color_Used_05.get(1)` |
| `Spray_Color_Used_06` | `ItemList.Spray_Color_Used_06.get(1)` |
| `Spray_Color_Used_07` | `ItemList.Spray_Color_Used_07.get(1)` |
| `Spray_Color_Used_08` | `ItemList.Spray_Color_Used_08.get(1)` |
| `Spray_Color_Used_09` | `ItemList.Spray_Color_Used_09.get(1)` |
| `Spray_Color_Used_09` | `ItemList.Spray_Color_Used_09.get(1)` |
| `Spray_Color_Used_10` | `ItemList.Spray_Color_Used_10.get(1)` |
| `Spray_Color_Used_11` | `ItemList.Spray_Color_Used_11.get(1)` |
| `Spray_Color_Used_12` | `ItemList.Spray_Color_Used_12.get(1)` |
| `Spray_Color_Used_13` | `ItemList.Spray_Color_Used_13.get(1)` |
| `Spray_Color_Used_14` | `ItemList.Spray_Color_Used_14.get(1)` |
| `Spray_Color_Used_14` | `ItemList.Spray_Color_Used_14.get(1)` |
| `Spray_Color_Used_15` | `ItemList.Spray_Color_Used_15.get(1)` |
| `Spray_Color_Used_Remover` | `ItemList.Spray_Color_Used_Remover.get(1)` |
| `Spray_Empty` | `ItemList.Spray_Empty.get(1)` |
| `Spray_Hardener` | `ItemList.Spray_Hardener.get(1)` |
| `Spray_Hydration` | `ItemList.Spray_Hydration.get(1)` |
| `Spray_Ice` | `ItemList.Spray_Ice.get(1)` |
| `Spray_Pepper` | `ItemList.Spray_Pepper.get(1)` |

### Category: StableAdhesive

| 枚举键值 | 获取代码 |
|---------|---------|
| `StableAdhesive` | `ItemList.StableAdhesive.get(1)` |

### Category: Steam

| 枚举键值 | 获取代码 |
|---------|---------|
| `Steam_Regulator_EV` | `ItemList.Steam_Regulator_EV.get(1)` |
| `Steam_Regulator_HV` | `ItemList.Steam_Regulator_HV.get(1)` |
| `Steam_Regulator_IV` | `ItemList.Steam_Regulator_IV.get(1)` |
| `Steam_Regulator_LV` | `ItemList.Steam_Regulator_LV.get(1)` |
| `Steam_Regulator_MV` | `ItemList.Steam_Regulator_MV.get(1)` |
| `Steam_Valve_EV` | `ItemList.Steam_Valve_EV.get(1)` |
| `Steam_Valve_HV` | `ItemList.Steam_Valve_HV.get(1)` |
| `Steam_Valve_IV` | `ItemList.Steam_Valve_IV.get(1)` |
| `Steam_Valve_LV` | `ItemList.Steam_Valve_LV.get(1)` |
| `Steam_Valve_MV` | `ItemList.Steam_Valve_MV.get(1)` |

### Category: Streamlined

| 枚举键值 | 获取代码 |
|---------|---------|
| `Streamlined_Casters_ExoFoundry` | `ItemList.Streamlined_Casters_ExoFoundry.get(1)` |

### Category: Super

| 枚举键值 | 获取代码 |
|---------|---------|
| `Super_Chest_EV` | `ItemList.Super_Chest_EV.get(1)` |
| `Super_Chest_HV` | `ItemList.Super_Chest_HV.get(1)` |
| `Super_Chest_IV` | `ItemList.Super_Chest_IV.get(1)` |
| `Super_Chest_LV` | `ItemList.Super_Chest_LV.get(1)` |
| `Super_Chest_MV` | `ItemList.Super_Chest_MV.get(1)` |
| `Super_Tank_EV` | `ItemList.Super_Tank_EV.get(1)` |
| `Super_Tank_HV` | `ItemList.Super_Tank_HV.get(1)` |
| `Super_Tank_IV` | `ItemList.Super_Tank_IV.get(1)` |
| `Super_Tank_LV` | `ItemList.Super_Tank_LV.get(1)` |
| `Super_Tank_MV` | `ItemList.Super_Tank_MV.get(1)` |

### Category: Superconducting

| 枚举键值 | 获取代码 |
|---------|---------|
| `Superconducting_Magnet_Solenoid_EV` | `ItemList.Superconducting_Magnet_Solenoid_EV.get(1)` |
| `Superconducting_Magnet_Solenoid_HV` | `ItemList.Superconducting_Magnet_Solenoid_HV.get(1)` |
| `Superconducting_Magnet_Solenoid_IV` | `ItemList.Superconducting_Magnet_Solenoid_IV.get(1)` |
| `Superconducting_Magnet_Solenoid_LuV` | `ItemList.Superconducting_Magnet_Solenoid_LuV.get(1)` |
| `Superconducting_Magnet_Solenoid_MV` | `ItemList.Superconducting_Magnet_Solenoid_MV.get(1)` |
| `Superconducting_Magnet_Solenoid_UEV` | `ItemList.Superconducting_Magnet_Solenoid_UEV.get(1)` |
| `Superconducting_Magnet_Solenoid_UHV` | `ItemList.Superconducting_Magnet_Solenoid_UHV.get(1)` |
| `Superconducting_Magnet_Solenoid_UIV` | `ItemList.Superconducting_Magnet_Solenoid_UIV.get(1)` |
| `Superconducting_Magnet_Solenoid_UMV` | `ItemList.Superconducting_Magnet_Solenoid_UMV.get(1)` |
| `Superconducting_Magnet_Solenoid_UV` | `ItemList.Superconducting_Magnet_Solenoid_UV.get(1)` |
| `Superconducting_Magnet_Solenoid_ZPM` | `ItemList.Superconducting_Magnet_Solenoid_ZPM.get(1)` |

### Category: SuperconductorComposite

| 枚举键值 | 获取代码 |
|---------|---------|
| `SuperconductorComposite` | `ItemList.SuperconductorComposite.get(1)` |

### Category: TC

| 枚举键值 | 获取代码 |
|---------|---------|
| `TC_Thaumometer` | `ItemList.TC_Thaumometer.get(1)` |

### Category: TF

| 枚举键值 | 获取代码 |
|---------|---------|
| `TF_LiveRoot` | `ItemList.TF_LiveRoot.get(1)` |
| `TF_Vial_FieryBlood` | `ItemList.TF_Vial_FieryBlood.get(1)` |
| `TF_Vial_FieryTears` | `ItemList.TF_Vial_FieryTears.get(1)` |

### Category: TaHfCNanofibers

| 枚举键值 | 获取代码 |
|---------|---------|
| `TaHfCNanofibers` | `ItemList.TaHfCNanofibers.get(1)` |

### Category: TaHfNanoparticles

| 枚举键值 | 获取代码 |
|---------|---------|
| `TaHfNanoparticles` | `ItemList.TaHfNanoparticles.get(1)` |

### Category: Teleporter

| 枚举键值 | 获取代码 |
|---------|---------|
| `Teleporter` | `ItemList.Teleporter.get(1)` |

### Category: Tesseract

| 枚举键值 | 获取代码 |
|---------|---------|
| `Tesseract` | `ItemList.Tesseract.get(1)` |

### Category: Thermal

| 枚举键值 | 获取代码 |
|---------|---------|
| `Thermal_Superconductor` | `ItemList.Thermal_Superconductor.get(1)` |

### Category: ThermalCentrifugeLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeLuV` | `ItemList.ThermalCentrifugeLuV.get(1)` |

### Category: ThermalCentrifugeUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeUEV` | `ItemList.ThermalCentrifugeUEV.get(1)` |

### Category: ThermalCentrifugeUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeUHV` | `ItemList.ThermalCentrifugeUHV.get(1)` |

### Category: ThermalCentrifugeUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeUIV` | `ItemList.ThermalCentrifugeUIV.get(1)` |

### Category: ThermalCentrifugeUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeUMV` | `ItemList.ThermalCentrifugeUMV.get(1)` |

### Category: ThermalCentrifugeUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeUV` | `ItemList.ThermalCentrifugeUV.get(1)` |

### Category: ThermalCentrifugeZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermalCentrifugeZPM` | `ItemList.ThermalCentrifugeZPM.get(1)` |

### Category: ThermosCan

| 枚举键值 | 获取代码 |
|---------|---------|
| `ThermosCan_Chocolate_Milk` | `ItemList.ThermosCan_Chocolate_Milk.get(1)` |
| `ThermosCan_Coffee` | `ItemList.ThermosCan_Coffee.get(1)` |
| `ThermosCan_Dark_Chocolate_Milk` | `ItemList.ThermosCan_Dark_Chocolate_Milk.get(1)` |
| `ThermosCan_Empty` | `ItemList.ThermosCan_Empty.get(1)` |
| `ThermosCan_Ice_Tea` | `ItemList.ThermosCan_Ice_Tea.get(1)` |
| `ThermosCan_Latte` | `ItemList.ThermosCan_Latte.get(1)` |
| `ThermosCan_Sweet_Coffee` | `ItemList.ThermosCan_Sweet_Coffee.get(1)` |
| `ThermosCan_Sweet_Jesus_Latte` | `ItemList.ThermosCan_Sweet_Jesus_Latte.get(1)` |
| `ThermosCan_Sweet_Latte` | `ItemList.ThermosCan_Sweet_Latte.get(1)` |
| `ThermosCan_Sweet_Tea` | `ItemList.ThermosCan_Sweet_Tea.get(1)` |
| `ThermosCan_Tea` | `ItemList.ThermosCan_Tea.get(1)` |

### Category: TierdDrone0

| 枚举键值 | 获取代码 |
|---------|---------|
| `TierdDrone0` | `ItemList.TierdDrone0.get(1)` |

### Category: TierdDrone1

| 枚举键值 | 获取代码 |
|---------|---------|
| `TierdDrone1` | `ItemList.TierdDrone1.get(1)` |

### Category: TierdDrone2

| 枚举键值 | 获取代码 |
|---------|---------|
| `TierdDrone2` | `ItemList.TierdDrone2.get(1)` |

### Category: TierdDrone3

| 枚举键值 | 获取代码 |
|---------|---------|
| `TierdDrone3` | `ItemList.TierdDrone3.get(1)` |

### Category: Timepiece

| 枚举键值 | 获取代码 |
|---------|---------|
| `Timepiece` | `ItemList.Timepiece.get(1)` |

### Category: Tool

| 枚举键值 | 获取代码 |
|---------|---------|
| `Tool_Axe_Bronze` | `ItemList.Tool_Axe_Bronze.get(1)` |
| `Tool_Axe_Steel` | `ItemList.Tool_Axe_Steel.get(1)` |
| `Tool_Cheat` | `ItemList.Tool_Cheat.get(1)` |
| `Tool_Cover_Copy_Paste` | `ItemList.Tool_Cover_Copy_Paste.get(1)` |
| `Tool_DataOrb` | `ItemList.Tool_DataOrb.get(1)` |
| `Tool_DataStick` | `ItemList.Tool_DataStick.get(1)` |
| `Tool_Hoe_Bronze` | `ItemList.Tool_Hoe_Bronze.get(1)` |
| `Tool_Hoe_Steel` | `ItemList.Tool_Hoe_Steel.get(1)` |
| `Tool_Lighter_Invar_Empty` | `ItemList.Tool_Lighter_Invar_Empty.get(1)` |
| `Tool_Lighter_Invar_Full` | `ItemList.Tool_Lighter_Invar_Full.get(1)` |
| `Tool_Lighter_Invar_Used` | `ItemList.Tool_Lighter_Invar_Used.get(1)` |
| `Tool_Lighter_Platinum_Empty` | `ItemList.Tool_Lighter_Platinum_Empty.get(1)` |
| `Tool_Lighter_Platinum_Full` | `ItemList.Tool_Lighter_Platinum_Full.get(1)` |
| `Tool_Lighter_Platinum_Used` | `ItemList.Tool_Lighter_Platinum_Used.get(1)` |
| `Tool_MatchBox_Full` | `ItemList.Tool_MatchBox_Full.get(1)` |
| `Tool_MatchBox_Used` | `ItemList.Tool_MatchBox_Used.get(1)` |
| `Tool_Matches` | `ItemList.Tool_Matches.get(1)` |
| `Tool_Pickaxe_Bronze` | `ItemList.Tool_Pickaxe_Bronze.get(1)` |
| `Tool_Pickaxe_Steel` | `ItemList.Tool_Pickaxe_Steel.get(1)` |
| `Tool_Scanner` | `ItemList.Tool_Scanner.get(1)` |
| `Tool_Shovel_Bronze` | `ItemList.Tool_Shovel_Bronze.get(1)` |
| `Tool_Shovel_Steel` | `ItemList.Tool_Shovel_Steel.get(1)` |
| `Tool_Sword_Bronze` | `ItemList.Tool_Sword_Bronze.get(1)` |
| `Tool_Sword_Steel` | `ItemList.Tool_Sword_Steel.get(1)` |
| `Tool_Vajra` | `ItemList.Tool_Vajra.get(1)` |

### Category: Transdimensional

| 枚举键值 | 获取代码 |
|---------|---------|
| `Transdimensional_Alignment_Matrix` | `ItemList.Transdimensional_Alignment_Matrix.get(1)` |

### Category: Transformer

| 枚举键值 | 获取代码 |
|---------|---------|
| `Transformer_EV_HV` | `ItemList.Transformer_EV_HV.get(1)` |
| `Transformer_HA_MAX_UXV` | `ItemList.Transformer_HA_MAX_UXV.get(1)` |
| `Transformer_HA_UEV_UHV` | `ItemList.Transformer_HA_UEV_UHV.get(1)` |
| `Transformer_HA_UIV_UEV` | `ItemList.Transformer_HA_UIV_UEV.get(1)` |
| `Transformer_HA_UMV_UIV` | `ItemList.Transformer_HA_UMV_UIV.get(1)` |
| `Transformer_HA_UXV_UMV` | `ItemList.Transformer_HA_UXV_UMV.get(1)` |
| `Transformer_HV_MV` | `ItemList.Transformer_HV_MV.get(1)` |
| `Transformer_IV_EV` | `ItemList.Transformer_IV_EV.get(1)` |
| `Transformer_LV_ULV` | `ItemList.Transformer_LV_ULV.get(1)` |
| `Transformer_LuV_IV` | `ItemList.Transformer_LuV_IV.get(1)` |
| `Transformer_LuV_IV` | `ItemList.Transformer_LuV_IV.get(1)` |
| `Transformer_MAX_UV` | `ItemList.Transformer_MAX_UV.get(1)` |
| `Transformer_MAX_UXV` | `ItemList.Transformer_MAX_UXV.get(1)` |
| `Transformer_MV_LV` | `ItemList.Transformer_MV_LV.get(1)` |
| `Transformer_UEV_UHV` | `ItemList.Transformer_UEV_UHV.get(1)` |
| `Transformer_UIV_UEV` | `ItemList.Transformer_UIV_UEV.get(1)` |
| `Transformer_UMV_UIV` | `ItemList.Transformer_UMV_UIV.get(1)` |
| `Transformer_UV_ZPM` | `ItemList.Transformer_UV_ZPM.get(1)` |
| `Transformer_UXV_UMV` | `ItemList.Transformer_UXV_UMV.get(1)` |
| `Transformer_ZPM_LuV` | `ItemList.Transformer_ZPM_LuV.get(1)` |

### Category: Tube

| 枚举键值 | 获取代码 |
|---------|---------|
| `Tube_Wires` | `ItemList.Tube_Wires.get(1)` |

### Category: UHTResistantMesh

| 枚举键值 | 获取代码 |
|---------|---------|
| `UHTResistantMesh` | `ItemList.UHTResistantMesh.get(1)` |

### Category: UHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `UHV_Coil` | `ItemList.UHV_Coil.get(1)` |

### Category: ULV

| 枚举键值 | 获取代码 |
|---------|---------|
| `ULV_Coil` | `ItemList.ULV_Coil.get(1)` |

### Category: UV

| 枚举键值 | 获取代码 |
|---------|---------|
| `UV_Coil` | `ItemList.UV_Coil.get(1)` |

### Category: UltraHighStrengthConcrete

| 枚举键值 | 获取代码 |
|---------|---------|
| `UltraHighStrengthConcrete` | `ItemList.UltraHighStrengthConcrete.get(1)` |

### Category: Universal

| 枚举键值 | 获取代码 |
|---------|---------|
| `Universal_Collapser_ExoFoundry` | `ItemList.Universal_Collapser_ExoFoundry.get(1)` |

### Category: Upgrade

| 枚举键值 | 获取代码 |
|---------|---------|
| `Upgrade_Battery` | `ItemList.Upgrade_Battery.get(1)` |
| `Upgrade_Lock` | `ItemList.Upgrade_Lock.get(1)` |
| `Upgrade_Overclocker` | `ItemList.Upgrade_Overclocker.get(1)` |
| `Upgrade_SteamEngine` | `ItemList.Upgrade_SteamEngine.get(1)` |

### Category: VOLUMETRIC

| 枚举键值 | 获取代码 |
|---------|---------|
| `VOLUMETRIC_FLASK` | `ItemList.VOLUMETRIC_FLASK.get(1)` |

### Category: VacuumConveyorPipe

| 枚举键值 | 获取代码 |
|---------|---------|
| `VacuumConveyorPipe` | `ItemList.VacuumConveyorPipe.get(1)` |

### Category: Vajra

| 枚举键值 | 获取代码 |
|---------|---------|
| `Vajra_Core` | `ItemList.Vajra_Core.get(1)` |

### Category: WetTransformer

| 枚举键值 | 获取代码 |
|---------|---------|
| `WetTransformer_EV_HV` | `ItemList.WetTransformer_EV_HV.get(1)` |
| `WetTransformer_HV_MV` | `ItemList.WetTransformer_HV_MV.get(1)` |
| `WetTransformer_IV_EV` | `ItemList.WetTransformer_IV_EV.get(1)` |
| `WetTransformer_LV_ULV` | `ItemList.WetTransformer_LV_ULV.get(1)` |
| `WetTransformer_LuV_IV` | `ItemList.WetTransformer_LuV_IV.get(1)` |
| `WetTransformer_MAX_UXV` | `ItemList.WetTransformer_MAX_UXV.get(1)` |
| `WetTransformer_MV_LV` | `ItemList.WetTransformer_MV_LV.get(1)` |
| `WetTransformer_UEV_UHV` | `ItemList.WetTransformer_UEV_UHV.get(1)` |
| `WetTransformer_UHV_UV` | `ItemList.WetTransformer_UHV_UV.get(1)` |
| `WetTransformer_UIV_UEV` | `ItemList.WetTransformer_UIV_UEV.get(1)` |
| `WetTransformer_UMV_UIV` | `ItemList.WetTransformer_UMV_UIV.get(1)` |
| `WetTransformer_UV_ZPM` | `ItemList.WetTransformer_UV_ZPM.get(1)` |
| `WetTransformer_UXV_UMV` | `ItemList.WetTransformer_UXV_UMV.get(1)` |
| `WetTransformer_ZPM_LuV` | `ItemList.WetTransformer_ZPM_LuV.get(1)` |

### Category: Wireless

| 枚举键值 | 获取代码 |
|---------|---------|
| `Wireless_Dynamo_Energy_EV` | `ItemList.Wireless_Dynamo_Energy_EV.get(1)` |
| `Wireless_Dynamo_Energy_HV` | `ItemList.Wireless_Dynamo_Energy_HV.get(1)` |
| `Wireless_Dynamo_Energy_IV` | `ItemList.Wireless_Dynamo_Energy_IV.get(1)` |
| `Wireless_Dynamo_Energy_LV` | `ItemList.Wireless_Dynamo_Energy_LV.get(1)` |
| `Wireless_Dynamo_Energy_LuV` | `ItemList.Wireless_Dynamo_Energy_LuV.get(1)` |
| `Wireless_Dynamo_Energy_MAX` | `ItemList.Wireless_Dynamo_Energy_MAX.get(1)` |
| `Wireless_Dynamo_Energy_MV` | `ItemList.Wireless_Dynamo_Energy_MV.get(1)` |
| `Wireless_Dynamo_Energy_UEV` | `ItemList.Wireless_Dynamo_Energy_UEV.get(1)` |
| `Wireless_Dynamo_Energy_UHV` | `ItemList.Wireless_Dynamo_Energy_UHV.get(1)` |
| `Wireless_Dynamo_Energy_UIV` | `ItemList.Wireless_Dynamo_Energy_UIV.get(1)` |
| `Wireless_Dynamo_Energy_ULV` | `ItemList.Wireless_Dynamo_Energy_ULV.get(1)` |
| `Wireless_Dynamo_Energy_UMV` | `ItemList.Wireless_Dynamo_Energy_UMV.get(1)` |
| `Wireless_Dynamo_Energy_UV` | `ItemList.Wireless_Dynamo_Energy_UV.get(1)` |
| `Wireless_Dynamo_Energy_UXV` | `ItemList.Wireless_Dynamo_Energy_UXV.get(1)` |
| `Wireless_Dynamo_Energy_ZPM` | `ItemList.Wireless_Dynamo_Energy_ZPM.get(1)` |
| `Wireless_Hatch_Energy_EV` | `ItemList.Wireless_Hatch_Energy_EV.get(1)` |
| `Wireless_Hatch_Energy_HV` | `ItemList.Wireless_Hatch_Energy_HV.get(1)` |
| `Wireless_Hatch_Energy_HV` | `ItemList.Wireless_Hatch_Energy_HV.get(1)` |
| `Wireless_Hatch_Energy_IV` | `ItemList.Wireless_Hatch_Energy_IV.get(1)` |
| `Wireless_Hatch_Energy_LV` | `ItemList.Wireless_Hatch_Energy_LV.get(1)` |
| `Wireless_Hatch_Energy_LuV` | `ItemList.Wireless_Hatch_Energy_LuV.get(1)` |
| `Wireless_Hatch_Energy_MAX` | `ItemList.Wireless_Hatch_Energy_MAX.get(1)` |
| `Wireless_Hatch_Energy_MV` | `ItemList.Wireless_Hatch_Energy_MV.get(1)` |
| `Wireless_Hatch_Energy_UEV` | `ItemList.Wireless_Hatch_Energy_UEV.get(1)` |
| `Wireless_Hatch_Energy_UHV` | `ItemList.Wireless_Hatch_Energy_UHV.get(1)` |
| `Wireless_Hatch_Energy_UIV` | `ItemList.Wireless_Hatch_Energy_UIV.get(1)` |
| `Wireless_Hatch_Energy_UIV` | `ItemList.Wireless_Hatch_Energy_UIV.get(1)` |
| `Wireless_Hatch_Energy_ULV` | `ItemList.Wireless_Hatch_Energy_ULV.get(1)` |
| `Wireless_Hatch_Energy_UMV` | `ItemList.Wireless_Hatch_Energy_UMV.get(1)` |
| `Wireless_Hatch_Energy_UV` | `ItemList.Wireless_Hatch_Energy_UV.get(1)` |
| `Wireless_Hatch_Energy_UXV` | `ItemList.Wireless_Hatch_Energy_UXV.get(1)` |
| `Wireless_Hatch_Energy_ZPM` | `ItemList.Wireless_Hatch_Energy_ZPM.get(1)` |
| `Wireless_Hatch_Energy_ZPM` | `ItemList.Wireless_Hatch_Energy_ZPM.get(1)` |

### Category: WirelessHeadphones

| 枚举键值 | 获取代码 |
|---------|---------|
| `WirelessHeadphones` | `ItemList.WirelessHeadphones.get(1)` |

### Category: WiremillLuV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillLuV` | `ItemList.WiremillLuV.get(1)` |

### Category: WiremillUEV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillUEV` | `ItemList.WiremillUEV.get(1)` |

### Category: WiremillUHV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillUHV` | `ItemList.WiremillUHV.get(1)` |

### Category: WiremillUIV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillUIV` | `ItemList.WiremillUIV.get(1)` |

### Category: WiremillUMV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillUMV` | `ItemList.WiremillUMV.get(1)` |

### Category: WiremillUV

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillUV` | `ItemList.WiremillUV.get(1)` |

### Category: WiremillZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `WiremillZPM` | `ItemList.WiremillZPM.get(1)` |

### Category: WoodenCasing

| 枚举键值 | 获取代码 |
|---------|---------|
| `WoodenCasing` | `ItemList.WoodenCasing.get(1)` |

### Category: WormholeGenerator

| 枚举键值 | 获取代码 |
|---------|---------|
| `WormholeGenerator` | `ItemList.WormholeGenerator.get(1)` |

### Category: WovenKevlar

| 枚举键值 | 获取代码 |
|---------|---------|
| `WovenKevlar` | `ItemList.WovenKevlar.get(1)` |

### Category: Wrap

| 枚举键值 | 获取代码 |
|---------|---------|
| `Wrap_ASoCs` | `ItemList.Wrap_ASoCs.get(1)` |
| `Wrap_AdvancedCircuitBoards` | `ItemList.Wrap_AdvancedCircuitBoards.get(1)` |
| `Wrap_AdvancedSMDCapacitors` | `ItemList.Wrap_AdvancedSMDCapacitors.get(1)` |
| `Wrap_AdvancedSMDDiodes` | `ItemList.Wrap_AdvancedSMDDiodes.get(1)` |
| `Wrap_AdvancedSMDInductors` | `ItemList.Wrap_AdvancedSMDInductors.get(1)` |
| `Wrap_AdvancedSMDResistors` | `ItemList.Wrap_AdvancedSMDResistors.get(1)` |
| `Wrap_AdvancedSMDTransistors` | `ItemList.Wrap_AdvancedSMDTransistors.get(1)` |
| `Wrap_BioCircuitBoards` | `ItemList.Wrap_BioCircuitBoards.get(1)` |
| `Wrap_BioProcessingUnits` | `ItemList.Wrap_BioProcessingUnits.get(1)` |
| `Wrap_Biocells` | `ItemList.Wrap_Biocells.get(1)` |
| `Wrap_CentralProcessingUnits` | `ItemList.Wrap_CentralProcessingUnits.get(1)` |
| `Wrap_CircuitBoards` | `ItemList.Wrap_CircuitBoards.get(1)` |
| `Wrap_CoatedCircuitBoards` | `ItemList.Wrap_CoatedCircuitBoards.get(1)` |
| `Wrap_CrystalProcessingUnits` | `ItemList.Wrap_CrystalProcessingUnits.get(1)` |
| `Wrap_CrystalSoCs` | `ItemList.Wrap_CrystalSoCs.get(1)` |
| `Wrap_EliteCircuitBoards` | `ItemList.Wrap_EliteCircuitBoards.get(1)` |
| `Wrap_EngravedCrystalChips` | `ItemList.Wrap_EngravedCrystalChips.get(1)` |
| `Wrap_EngravedLapotrionChips` | `ItemList.Wrap_EngravedLapotrionChips.get(1)` |
| `Wrap_EpoxyCircuitBoards` | `ItemList.Wrap_EpoxyCircuitBoards.get(1)` |
| `Wrap_ExtremeWetwareLifesupportCircuitBoards` | `ItemList.Wrap_ExtremeWetwareLifesupportCircuitBoards.get(1)` |
| `Wrap_FiberReinforcedCircuitBoards` | `ItemList.Wrap_FiberReinforcedCircuitBoards.get(1)` |
| `Wrap_GoodCircuitBoards` | `ItemList.Wrap_GoodCircuitBoards.get(1)` |
| `Wrap_HighPowerICs` | `ItemList.Wrap_HighPowerICs.get(1)` |
| `Wrap_IntegratedLogicCircuits` | `ItemList.Wrap_IntegratedLogicCircuits.get(1)` |
| `Wrap_LivingBioChips` | `ItemList.Wrap_LivingBioChips.get(1)` |
| `Wrap_LivingCrystalChips` | `ItemList.Wrap_LivingCrystalChips.get(1)` |
| `Wrap_LowPowerICs` | `ItemList.Wrap_LowPowerICs.get(1)` |
| `Wrap_MoreAdvancedCircuitBoards` | `ItemList.Wrap_MoreAdvancedCircuitBoards.get(1)` |
| `Wrap_MultilayerFiberReinforcedCircuitBoards` | `ItemList.Wrap_MultilayerFiberReinforcedCircuitBoards.get(1)` |
| `Wrap_NANDMemoryChips` | `ItemList.Wrap_NANDMemoryChips.get(1)` |
| `Wrap_NORMemoryChips` | `ItemList.Wrap_NORMemoryChips.get(1)` |
| `Wrap_NanoPowerICs` | `ItemList.Wrap_NanoPowerICs.get(1)` |
| `Wrap_NanocomponentCentralProcessingUnits` | `ItemList.Wrap_NanocomponentCentralProcessingUnits.get(1)` |
| `Wrap_NeuroProcessingUnits` | `ItemList.Wrap_NeuroProcessingUnits.get(1)` |
| `Wrap_OpticalCPUContainmentHousings` | `ItemList.Wrap_OpticalCPUContainmentHousings.get(1)` |
| `Wrap_OpticalCircuitBoards` | `ItemList.Wrap_OpticalCircuitBoards.get(1)` |
| `Wrap_OpticalSMDCapacitors` | `ItemList.Wrap_OpticalSMDCapacitors.get(1)` |
| `Wrap_OpticalSMDDiodes` | `ItemList.Wrap_OpticalSMDDiodes.get(1)` |
| `Wrap_OpticalSMDInductors` | `ItemList.Wrap_OpticalSMDInductors.get(1)` |
| `Wrap_OpticalSMDResistors` | `ItemList.Wrap_OpticalSMDResistors.get(1)` |
| `Wrap_OpticalSMDTransistors` | `ItemList.Wrap_OpticalSMDTransistors.get(1)` |
| `Wrap_OpticallyCompatibleMemories` | `ItemList.Wrap_OpticallyCompatibleMemories.get(1)` |
| `Wrap_OpticallyPerfectedCPUs` | `ItemList.Wrap_OpticallyPerfectedCPUs.get(1)` |
| `Wrap_PhenolicCircuitBoards` | `ItemList.Wrap_PhenolicCircuitBoards.get(1)` |
| `Wrap_PikoPowerICs` | `ItemList.Wrap_PikoPowerICs.get(1)` |
| `Wrap_PlasticCircuitBoards` | `ItemList.Wrap_PlasticCircuitBoards.get(1)` |
| `Wrap_PlasticCircuitBoards2` | `ItemList.Wrap_PlasticCircuitBoards2.get(1)` |
| `Wrap_PowerICs` | `ItemList.Wrap_PowerICs.get(1)` |
| `Wrap_QBitProcessingUnits` | `ItemList.Wrap_QBitProcessingUnits.get(1)` |
| `Wrap_QuantumPowerICs` | `ItemList.Wrap_QuantumPowerICs.get(1)` |
| `Wrap_RandomAccessMemoryChips` | `ItemList.Wrap_RandomAccessMemoryChips.get(1)` |
| `Wrap_RawAdvancedCrystalChips` | `ItemList.Wrap_RawAdvancedCrystalChips.get(1)` |
| `Wrap_RawExposedOpticalChips` | `ItemList.Wrap_RawExposedOpticalChips.get(1)` |
| `Wrap_SMDCapacitors` | `ItemList.Wrap_SMDCapacitors.get(1)` |
| `Wrap_SMDDiodes` | `ItemList.Wrap_SMDDiodes.get(1)` |
| `Wrap_SMDInductors` | `ItemList.Wrap_SMDInductors.get(1)` |
| `Wrap_SMDResistors` | `ItemList.Wrap_SMDResistors.get(1)` |
| `Wrap_SMDTransistors` | `ItemList.Wrap_SMDTransistors.get(1)` |
| `Wrap_SimpleSOCs` | `ItemList.Wrap_SimpleSOCs.get(1)` |
| `Wrap_SoCs` | `ItemList.Wrap_SoCs.get(1)` |
| `Wrap_Stemcells` | `ItemList.Wrap_Stemcells.get(1)` |
| `Wrap_UltraBioMutatedCircuitBoards` | `ItemList.Wrap_UltraBioMutatedCircuitBoards.get(1)` |
| `Wrap_UltraHighPowerICs` | `ItemList.Wrap_UltraHighPowerICs.get(1)` |
| `Wrap_UltraLowPowerICs` | `ItemList.Wrap_UltraLowPowerICs.get(1)` |
| `Wrap_WetwareLifesupportCircuitBoards` | `ItemList.Wrap_WetwareLifesupportCircuitBoards.get(1)` |

### Category: ZPM

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM` | `ItemList.ZPM.get(1)` |
| `ZPM_Coil` | `ItemList.ZPM_Coil.get(1)` |

### Category: ZPM2

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM2` | `ItemList.ZPM2.get(1)` |

### Category: ZPM3

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM3` | `ItemList.ZPM3.get(1)` |

### Category: ZPM4

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM4` | `ItemList.ZPM4.get(1)` |

### Category: ZPM5

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM5` | `ItemList.ZPM5.get(1)` |

### Category: ZPM6

| 枚举键值 | 获取代码 |
|---------|---------|
| `ZPM6` | `ItemList.ZPM6.get(1)` |
