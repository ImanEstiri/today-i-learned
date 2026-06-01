> Today I Learned | NuGet

# NuGet versions are immutable

Date: 2026/06/01

## Body

`dotnet pack` silently overwrites a local .nupkg with the same version, but nuget.org
rejects a version that was already published. With `--skip-duplicate` the push is just
skipped, so the fix never goes out. Always bump `<Version>` in the csproj before packing again.

```powershell
dotnet pack -c Release --output ../../artifacts
dotnet nuget push ./artifacts/MyPackage.1.0.3.nupkg --source https://api.nuget.org/v3/index.json --api-key $env:NUGET_API_KEY --skip-duplicate
```

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*