# Underworld (GeoCore)
一款为Minecraft 1.21+打造的「地心世界」Spigot插件，基于3D密度场算法生成无地表的沉浸式岩洞世界，包含多样化的群系、自然装饰和特色遗迹结构。

## 核心特性
### 🌍 独特的世界生成
- **3D岩洞系统**：无传统地表，整个世界由相互连通的岩洞网络构成
- **多层噪声算法**：通过多维度噪声生成自然且复杂的岩洞形态（主密度、形状、细节、大型空腔等）
- **垂直分层设计**：从基岩层（-64）到顶层（130）的完整垂直空间，包含熔岩层、不同密度的岩洞区域
- **群系差异化**：不同群系影响岩洞密度、高度倾向和方块材质，群系间平滑过渡

### 🎨 丰富的装饰与结构
- **自然装饰**：钟乳石、石笋、水晶柱、玄武岩柱、下界植被等动态生成
- **特色遗迹**：古代神殿、祭坛、图书馆废墟、传送门遗迹、水晶圣殿等10+种遗迹结构
- **核心地标**：太空电梯、巨型光源等独特地标建筑
- **动态光源**：自然散布的光源柱、海晶灯、灵魂灯笼等照明元素

### ⚙️ 便捷的管理命令
- 完整的`/geocore`命令体系，支持世界创建、传送、群系查看、预生成、重载等操作
- 命令别名：`gc`、`geocoreworld`
- 权限控制：`geocore.use`

## 环境要求
| 依赖项 | 版本要求 |
|--------|----------|
| Minecraft | 1.21+ |
| Spigot/Paper | 1.21.8-R0.1+ |
| Java | 21+ |
| Maven | 3.6+（仅编译时需要） |

## 安装说明
1. 下载编译好的`underworld-1.0-SNAPSHOT.jar`文件
2. 将jar文件放入服务器的`plugins`目录
3. 重启服务器，插件会自动生成配置文件（如有）
4. 使用`/geocore create`命令创建地心世界

## 编译说明（开发者）
1. 克隆本项目到本地
   ```bash
   git clone <项目仓库地址>
   cd underworld
   ```
2. 使用Maven编译
   ```bash
   mvn clean package
   ```
3. 编译后的jar文件位于`target/underworld-1.0-SNAPSHOT.jar`

## 核心命令
| 命令 | 描述 | 示例 |
|------|------|------|
| `/geocore create` | 创建地心世界 | `/geocore create` |
| `/geocore tp` | 传送到地心世界 | `/geocore tp` |
| `/geocore biome` | 查看当前群系信息 | `/geocore biome` |
| `/geocore info` | 查看世界信息 | `/geocore info` |
| `/geocore pregen` | 预生成世界区块 | `/geocore pregen 0 0 100` |
| `/geocore reload` | 重载插件配置 | `/geocore reload` |

## 技术细节
### 世界生成核心
- `GeoCoreChunkGenerator`：核心区块生成器，负责3D密度场计算、岩洞结构生成、群系适配
- `GeoCorePopulator`：装饰与结构生成器，负责遗迹、自然装饰的填充
- `FastNoise`：高性能噪声库，用于生成自然的随机地形
- 密度场算法：通过多噪声叠加计算区块内每个方块的"固体/空气"状态，生成连续岩洞

### 垂直空间划分
- 基岩底层：`MIN_Y + 10`（-54）以下
- 熔岩层：`MIN_Y + 20`（-44）以下
- 主岩洞区域：-54 ~ 125
- 基岩顶层：`MAX_Y - 5`（125）以上

## 开发架构
```
Thexiaoyu.underworld/
├── Underworld.java          # 插件主类
├── generator/
│   ├── GeoCoreChunkGenerator.java  # 核心区块生成器
│   └── GeoCorePopulator.java       # 装饰/结构生成器
├── biome/
│   └── GeoBiome.java               # 群系定义与逻辑
└── util/
    └── FastNoise.java              # 噪声工具类
```

## 许可证
本项目采用[MIT许可证](LICENSE)（如有，可替换为实际许可证）

## 作者
- 主开发者：Thexiaoyu、Jinkra
- 核心算法：Jinkra

## 注意事项
1. 首次创建世界可能需要较长时间，建议使用`pregen`命令预生成常用区域
2. 由于3D岩洞生成算法较复杂，建议在高性能服务器上使用
3. 请勿随意修改世界生成相关配置，可能导致世界损坏
4. 建议定期备份地心世界数据
