# Windows 常用命令

## DISM 命令速查

### 挂载/卸载 保存映像

#### 挂载映像

```shell
Dism /Mount-Image /ImageFile:\WIMFilePath.wim /Index:1 /MountDir:\MountPoint
```

#### 清理映像SP更新包备份文件

```shell
Dism /Image:\MountPoint /Cleanup-Image /SPSuperseded /HideSP
```

#### 清理映像WinSxS

```shell
Dism /Image:\MountPoint /Cleanup-Image /StartComponentCleanup /ResetBase
```

#### 保存并卸载映像

```shell
Dism /Unmount-Image /MountDir:\MountPoint /Commit
```

### 映像编辑

#### 导出映像其中一个index

```shell
Dism /Export-Image /SourceImageFile:\SourceWIMFilePath.wim /SourceIndex:1 /DestinationImageFile:\DestinationWIMFilePath.wim
```

#### 追加已挂载的映像

```shell
Dism /Capture-Image /ImageFile:WIMFilePath.wim /CaptureDir:\MountedPoint /Name:NewIndex
```

### Package 更新控制

#### 获取已安装的 Package

```shell
Dism /Image:\MountPoint /Get-Packages /Format:Table
```

#### 查询 Package

```shell
Dism /Image:\MountPoint /Get-PackageInfo /PackagePath:\Package.cab
```

```shell
Dism /Image:\MountPoint /Get-PackageInfo /PackageName:<Package.Name~xxxxx>
```

#### 追加 Package

```shell
Dism /Image:\MountPoint /Add-Package /PackagePath:\Package.{cab | msu}
```

#### 移除 Package

```shell
Dism /Image:\MountPoint /Remove-Package /PackageName:<Package.Name~xxxxx>
```

### Windows Features 控制

#### 获取已安装的 Windows Features

```shell
Dism /Image:\MountPoint /Get-Features /Format:Table
```

#### 查询 Windows Features 信息

```shell
Dism /Image:\MountPoint /Get-FeatureInfo /FeatureName:TFTP
```

#### 启用 Windows Features

```shell
Dism /Image:\MountPoint /Enable-Feature /FeatureName:TFTP /All
```

#### 禁用并删除 Windows Features

```shell
Dism /Image:\MountPoint /Disable-Feature /FeatureName:TFTP /Remove
```

### Appx 控制

#### 获取 Appx 信息

```shell
Dism /Image:\MountPoint /Get-ProvisionedAppxPackages
```

#### Appx 追加

```shell
DISM /Image:\MountPoint /Add-ProvisionedAppxPackage /PackagePath:\AppxPackage.{appx | appxbundle} {/SkipLicense | /LicensePath:\PackageLicense.xml}
```

#### Appx目录 追加

```shell
Dism /Image:\MountPoint /Add-ProvisionedAppxPackage /FolderPath:\AppxDirPath  {/SkipLicense | /LicensePath:\PackageLicense.xml}
```

#### Appx 删除

```shell
Dism /Image:\MountPoint /Remove-ProvisionedAppxPackage /PackageName:<package.name_xxxx>
```

#### 优化 Appx

```shell
Dism /Image:\MountPoint /Optimize-ProvisionedAppxPackages
```

---

[上一级](../README.md)

[笔记首页](../../../README.md)