# BlockSpaceProgram 整合包

BlockSpaceProgram 是一个受《坎巴拉太空计划》启发的 Minecraft 整合包，基于 Minecraft 1.21.1 和 NeoForge。玩家把方块结构制成零件，组装飞船，并在天体附近的飞行模拟与轨道传播之间切换。工业、物理、任务和地形优先采用现有模组，现有模组覆盖不到的部分由自制模组补齐。 [项目路线图](https://github.com/jxt159753/BlockSpaceProgram/issues/24) · [自制模组仓库](https://github.com/jxt159753/BlockSpaceProgram)

本仓库存放整合包清单、配置文件、KubeJS 脚本、FTB Quests 任务和数据包。需要写代码的缺口在自制模组仓库开发，整合包按版本引用它的发布文件。

## 模组构成

| 模组 | 在整合包中的作用 | 状态 |
| --- | --- | --- |
| [Create 6.0.10](https://modrinth.com/mod/create/version/UjX6dr61) | 工业与星球基地的移动机构 | 已选定 |
| [Sable 2.0.6](https://modrinth.com/mod/sable/version/fg9dTRz9) | 近地飞行的刚体物理，与 Create 机构发生碰撞 | 已选定 [设计决策](https://github.com/jxt159753/BlockSpaceProgram/issues/3) |
| [CC:Tweaked 1.120.2（NeoForge）](https://modrinth.com/version/1ewzHZYg) | 地面电脑通过飞控终端查询遥测并驾驶飞船 | 已选定 |
| [Exotic Worlds](https://github.com/anyttng/exotic_worlds) | 母星主世界东西无缝环绕 | 评估中 [#2](https://github.com/jxt159753/BlockSpaceProgram-Modpack/issues/2) |
| FTB Quests、KubeJS | 科技树、合同与设施解锁 | 计划中 [#3](https://github.com/jxt159753/BlockSpaceProgram-Modpack/issues/3) |
| [BlockSpaceProgram](https://github.com/jxt159753/BlockSpaceProgram) | 自制模组：零件烘焙、飞船装配与飞行、轨道层、天空渲染等缺口 | 开发中 |

## 状态

整合包尚未发布。模组清单、版本锁定、客户端包与服务端包的生成方式在 #1 中跟进。 [整合包清单、打包与发布 #1](https://github.com/jxt159753/BlockSpaceProgram-Modpack/issues/1)

## Iris 光影

包含 jxt159753/BlockSpaceProgram#52 修复的版本会在光影合成后绘制天空、卫星相位和星球球面。地形光照和阴影仍由光影包绘制。光影包自己的云和天空特效可能被覆盖。 [天空渲染兼容 Iris](https://github.com/jxt159753/BlockSpaceProgram/issues/52)

卫星维度 `blockspaceprogram:moon` 默认使用光影包的主世界程序。天空是黑色，远处地形仍可能带有大气雾。用下列配置让卫星走末地程序并关闭距离雾。末地程序会改变月面的光照和色调。

1. 在游戏实例的 `shaderpacks/` 目录复制一份光影包 ZIP。
2. 编辑副本内的 `shaders/dimension.properties`。在现有的 `dimension.world1` 行末加一个空格和 `blockspaceprogram:moon`。保留该行原有的末地 ID。
3. 在 ZIP 旁边编辑同名的 `.txt` 配置，例如 `我的光影.zip.txt`。更新下表列出的选项，其他选项沿用原值。
4. 在 Iris 中选中修改后的光影包并应用。 [Iris 维度映射](https://shaders.properties/current/reference/miscellaneous/dimension_properties/)

| 实测光影包 | 卫星去雾选项 |
| --- | --- |
| Complementary Reimagined r5.5.1 | `BORDER_FOG=false` |
| BSL v10.1.3 | `FOG_DENSITY_END=0.00`、`FAR_VANILLA_FOG=1`（仅主世界）、`LIGHT_SHAFT_END_SMOKE=0.00` |

母星的昼夜跟随轨道时钟。光影包用固定倾角计算太阳和阴影，即使赤道方向匹配，高纬度仍可能有偏差。BSL 的默认太阳倾角为 −40°，在赤道也可能偏离模组中的太阳。

实测使用 Minecraft 1.21.1、NeoForge 21.1.267、Sable 2.0.6 专用服。客户端使用 Sodium 0.8.13 和 Iris 1.8.14-beta.1。 [Complementary Reimagined](https://modrinth.com/shader/complementary-reimagined) · [BSL 10.1.3](https://modrinth.com/shader/bsl-shaders/version/10.1.3)

## 许可证

本仓库的配置、脚本、任务和数据包使用 MIT 许可证。整合包内的模组各自沿用原许可证，例如 Sable 使用 PolyForm Shield 1.0.0。整合包清单计划只引用各模组的官方下载，不在仓库或发布包中重新分发第三方 JAR。 [许可证](LICENSE)

CC:Tweaked 使用 ComputerCraft Public License 1.0。清单引用模组作者发布的 Modrinth 版本。 [CC:Tweaked 许可证](https://github.com/cc-tweaked/CC-Tweaked/blob/c7ccc20c756bdd437b09908840485a0e15dc7d7b/LICENSES/LicenseRef-CCPL.txt)
