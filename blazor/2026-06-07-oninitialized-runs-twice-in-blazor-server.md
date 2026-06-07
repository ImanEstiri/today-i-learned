> Today I Learned | Blazor
 
# OnInitialized runs twice in Blazor Server

Date: 2026/06/07

## Body

In Blazor Server, `OnInitialized` (and `OnInitializedAsync`) runs **twice** on the first
load of a page. It's not a bug — it's how the framework works.

The component is first rendered on the server during the prerender pass (to send HTML to
the browser quickly), and then it's initialized again when the SignalR circuit connects.
Two lifecycles, two runs.

The same component in Blazor WebAssembly or a purely interactive render mode only runs
once, so the bug hides until you deploy to Server.

If you do real work there — hitting a database, calling an API, generating a token — you'll
do it twice unless you guard against it.

```csharp
@inject NavigationManager Nav

@code {
    private bool _loaded;

    protected override async Task OnInitializedAsync()
    {
        if (_loaded) return;
        _loaded = true;

        // safe now — runs once per component instance
        Items = await Api.GetItemsAsync();
    }
}
```
 
If you don't need prerendering on a page (for example, a dashboard that's behind a login),
you can turn it off instead of guarding every component:

```
@rendermode @(new InteractiveServerRenderMode(prerender: false))
```

That removes the double-run at the source, but it also means the user sees a blank page
until the circuit is up — so it's a trade-off, not a default.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 