> Today I Learned | Blazor
 
# EventCallback vs Action in component parameters

Date: 2026/06/17

## Body

When a component exposes an event, use `EventCallback` (or `EventCallback<T>`), not
`Action`. `Action` works, but it doesn't trigger a re-render when invoked — the parent
won't update.

```razor
@* child *@
<button @onclick="() => OnClick.InvokeAsync()">Click</button>

@code {
    [Parameter] public EventCallback OnClick { get; set; }
}


```razor
@* parent *@
<Child OnClick="HandleClick" />

@code {
    private int count;
    void HandleClick() => count++;
}
```

`EventCallback` calls `StateHasChanged` on the parent automatically after the handler
runs. `Action` doesn't — you'd have to call it manually, and it's easy to forget.

For async handlers, `EventCallback` also returns a `Task` you can `await`, so exceptions
are tracked by Blazor instead of being lost.

Rule of thumb: any `[Parameter]` that is meant to be invoked by the child is
`EventCallback`. Use `Action` only for internal, non-rendering callbacks.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 