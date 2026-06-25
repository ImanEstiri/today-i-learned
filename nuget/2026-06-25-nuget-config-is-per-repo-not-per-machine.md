> Today I Learned | NuGet
 
# nuget.config is per-repo, not per-machine

Date: 2026/06/25

## Body

NuGet merges config from several places: machine-wide, user (`%AppData%\NuGet\NuGet.Config`),
and **repo root**. A `nuget.config` in the repo can pin package sources for that repo only,
so builds are reproducible across machines and CI.

```xml
<!-- nuget.config at repo root -->
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <clear />                                <!-- ignore inherited sources -->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    <add key="internal" value="https://pkgs.example.com/v3/index.json" />
  </packageSources>
</configuration>
```

`<clear />` is the important bit — without it, whatever a developer has on their machine
(e.g. a private feed, a local folder) leaks into the build. With it, the repo controls
exactly which sources are used.

For private feeds, store credentials outside the repo (`dotnet nuget add source` on the
machine, or a CI secret) — never commit an API key in `nuget.config`.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 