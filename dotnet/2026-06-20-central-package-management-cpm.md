> Today I Learned | .NET
 
# Central Package Management (CPM)

Date: 2026/06/20

## Body

Instead of putting `<PackageReference Version="...">` in every `.csproj`, define versions
once in a `Directory.Packages.props` at the repo root.

```xml
<!-- Directory.Packages.props -->
<Project>
  <PropertyGroup>
    <ManagePackageVersionsCentrally>true</ManagePackageVersionsCentrally>
  </PropertyGroup>
  <ItemGroup>
    <PackageVersion Include="Newtonsoft.Json" Version="13.0.3" />
    <PackageVersion Include="Serilog" Version="4.0.0" />
  </ItemGroup>
</Project>
```

Then in each project, drop the version:

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" />
</ItemGroup>
```

One file to bump, no version drift between projects. `dotnet list package --outdated`
still works.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 