---
layout: page
exclude: true
---

# Visual Studio Extensions

## Entendendo o VSCT
* O que é: tabela de comandos da extensão do Visual Studio, um arquivo XML descrevendo todos os comandos que serão disponibilizados pelas extensões e onde eles irão aparecer.

### Estrutura mínima para definir um menu

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <Extern href="stdidcmd.h"/>
  <Extern href="vsshlids.h"/>

  <Commands package="guidVSPackage">
    <Menus>
      <Menu guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Menus.MainMenu" priority="0x700" type="Menu">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
        <Strings>
          <ButtonText>MFractor</ButtonText>
        </Strings>
      </Menu>
    </Menus>
    <Groups>
      <Group guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Groups.MainMenu">
        <Parent guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Menus.MainMenu" />
      </Group>
    </Groups>
    <Buttons>
      <Button guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Commands.License" priority="0x0100" type="Button">
        <Parent guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Groups.MainMenu" />
        <Strings>
          <ButtonText>License Information</ButtonText>
        </Strings>
      </Button>
      <Button guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Commands.Buy" priority="0x0100" type="Button">
        <Parent guid="guidVSPackageCommandTopMenuCmdSet" id="MFractor.Groups.MainMenu" />
        <Strings>
          <ButtonText>Buy MFractor</ButtonText>
        </Strings>
      </Button>
      
    </Buttons>
  </Commands>
  
  <Symbols>
    <GuidSymbol name="guidVSPackage" value="{9772085d-2cd1-46f3-aa46-c62ee90fefec}" />
    <GuidSymbol name="guidVSPackageCommandTopMenuCmdSet" value="{9cff72df-e0c4-4ced-befe-0f415ae7cb6f}">
      <IDSymbol name="MFractor.Menus.MainMenu" value="0x1001" />
      <IDSymbol name="MFractor.Groups.MainMenu" value="0x1002" />
      <IDSymbol name="MFractor.Commands.LicenseInfo" value="0x1100" />
      <IDSymbol name="MFractor.Commands.Buy" value="0x1101" />
    </GuidSymbol>
    
  </Symbols>
</CommandTable>

```

Partes importantes:


