# TheOne Project Migration

**Automated project migration and configuration system for Unity**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Unity](https://img.shields.io/badge/Unity-2021.3%2B-blue.svg)](https://unity3d.com/get-unity/download)
[![UPM](https://img.shields.io/badge/UPM-Registry-green.svg)](https://upm.the1studio.org)

## Overview

This package provides an automated migration system that runs on project load and compilation to ensure consistent project setup across different Unity versions, team members, and environments. It handles Unity version upgrades, package dependencies, project settings, and custom migration modules.

## Features

- **Automatic Execution**: Runs automatically on project load and after compilation
- **Unity Version Management**: Adjusts packages and settings based on Unity version
- **Module System**: Extensible migration modules for custom logic
- **Package Management**: Auto-install/update/remove required packages
- **Settings Configuration**: Apply project settings consistently across team
- **Migration History**: Track which migrations have been applied
- **Rollback Support**: Safely revert problematic migrations
- **Team Sync**: Ensure all team members have the same setup

### Built-in Migration Modules

- **Package Migration**: Manage package dependencies per Unity version
- **Android Manifest**: Configure Android manifest settings
- **Firebase**: Update Firebase packages and configurations
- **AppLovin/LevelPlay**: Manage ad SDK integrations
- **Gradle Properties**: Configure Android build settings
- **Proguard**: Setup code obfuscation rules
- **Project Settings**: Apply player settings, graphics, and quality settings
- **Folder Migration**: Reorganize project structure

## Requirements

- Unity 2021.3 or higher
- Addressables Package 1.19.0+
- Cysharp.UniTask 2.3.0+

## Installation

### Via UPM Registry (Recommended)

Add to your `Packages/manifest.json`:

```json
{
  "dependencies": {
    "com.theone.tool.migration": "1.0.0"
  },
  "scopedRegistries": [
    {
      "name": "TheOne Studio",
      "url": "https://upm.the1studio.org",
      "scopes": ["com.theone"]
    }
  ]
}
```

### Via Git URL

```json
{
  "dependencies": {
    "com.theone.tool.migration": "https://github.com/The1Studio/UITemplateProjectMigration.git"
  }
}
```

## How It Works

1. **On Project Load**: Migration system checks for pending migrations
2. **Check Unity Version**: Determines which package config to use
3. **Run Migrations**: Executes all migration modules in order
4. **Update Settings**: Applies project settings
5. **Track History**: Records completed migrations
6. **Report Results**: Logs migration results to console

## Configuration

### Package Migration Config

Located at: `Assets/UITemplate/Editor/ProjectMigration/MigrationModules/PackageMigration/Resources/PackageMigrationConfig.json`

```json
{
  "2021.3": {
    "packages": {
      "com.unity.textmeshpro": "3.0.6",
      "com.unity.addressables": "1.19.19"
    }
  },
  "2022.3": {
    "packages": {
      "com.unity.textmeshpro": "3.2.0-pre.4",
      "com.unity.addressables": "1.21.14"
    }
  }
}
```

### Custom Migration Modules

Create custom migrations by extending the migration system:

```csharp
using TheOne.Tool.Migration;

public class CustomMigration : IMigrationModule
{
    public string ModuleName => "CustomMigration";
    public int Priority => 100; // Higher runs first
    
    public void Execute()
    {
        // Your migration logic
        Debug.Log("Running custom migration...");
    }
}
```

## Migration Modules

### PackageMigration

Manages Unity packages based on version:
- Adds required packages
- Removes incompatible packages
- Updates package versions
- Validates package integrity

### AndroidManifestMigration

Configures Android manifest:
- Add/remove permissions
- Configure activities
- Setup intent filters
- Manage meta-data

### FirebasePackageUpdater

Updates Firebase integration:
- Upgrade Firebase packages
- Configure google-services.json
- Update Crashlytics settings

### ApplovinMigration / LevelPlayMigration

Manages ad SDK integration:
- Configure mediation adapters
- Update SDK versions
- Setup ad placements

### GradlePropertiesMigration

Android build configuration:
- Set Gradle properties
- Configure NDK/SDK versions
- Enable/disable features

### ProjectSettingMigration

Apply project-wide settings:
- Player settings (bundle ID, version, icons)
- Graphics settings (URP, quality)
- Physics settings
- Input settings

## Best Practices

1. **Version Control**: Commit migration configs to version control
2. **Test First**: Test migrations in a branch before merging
3. **Document Changes**: Add comments to explain why migrations are needed
4. **Incremental Updates**: Make small, focused migrations rather than large changes
5. **Team Communication**: Inform team before adding migrations that affect everyone
6. **Backup**: Always backup project before running major migrations

## Troubleshooting

### Migration Not Running

- Check Unity console for errors
- Verify migration scripts are in correct folder
- Check if migration was already applied

### Package Install Failed

- Check internet connection
- Verify package name and version
- Check Unity Package Manager logs

### Settings Not Applied

- Check if settings file is valid
- Verify Unity has write permissions
- Check for conflicting settings

## API Reference

### ProjectAutoMigrationScript

Main entry point that runs on project load:

```csharp
[InitializeOnLoad]
public static class ProjectAutoMigrationScript
{
    // Automatically runs migrations
}
```

### Migration Modules

Individual migration scripts in `MigrationModules/` folder.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## About The One Studio

**The One Studio** is a mobile game development company specializing in hypercasual and casual games.

- Website: [https://the1studio.com](https://the1studio.com)
- Email: contact@the1studio.com

## Related Packages

- [UITemplate](https://github.com/The1Studio/UITemplate) - Complete Unity UI framework
- [TheOne Template Editor](https://github.com/The1Studio/UITemplateEditorCore) - Core editor tools
- [Unity Optimization Tools](https://github.com/The1Studio/UnityOptimizationTools) - Project optimization
- [TheOne LocalData](https://github.com/The1Studio/UITemplateLocalData) - Local data management
- [TheOne Localization](https://github.com/The1Studio/UITemplateLocalization) - Localization tools

## Support

- [GitHub Issues](https://github.com/The1Studio/UITemplateProjectMigration/issues)
- [Documentation](https://github.com/The1Studio/UITemplateProjectMigration#readme)

---

<div align="center">

Made with ❤️ by **The One Studio**

</div>
