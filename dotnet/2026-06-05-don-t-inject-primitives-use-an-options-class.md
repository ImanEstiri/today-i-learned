> Today I Learned | .NET
 
# Don't inject primitives, use an options class

Date: 2026/06/05

## Body

If a service takes a primitive like `string` or `int` in its constructor, the DI container
has no idea what to inject. You end up registering the value by hand, and as soon as you
need a second `string` it blows up — the container can't tell them apart.

Wrap related primitives in an options class and bind it from configuration. The container
resolves the class without help, you get validation for free, and the values have names.

```csharp
// bad — DI can't resolve this, and two strings collide
public class Mailer(string host, int port) { }

// good — one options object, bound from config
public class MailerOptions
{
    public string Host { get; set; } = "";
    public int Port { get; set; } = 25;
}

public class Mailer(IOptions<MailerOptions> options)
{
    private readonly MailerOptions _opts = options.Value;
}

// registration
builder.Services.Configure<MailerOptions>(
    builder.Configuration.GetSection("Mailer"));
```

Bonus: add `[Required]` and call `ValidateDataAnnotations()` to fail fast when config is
missing. 

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 