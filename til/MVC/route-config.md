I was finding that the Controller was showing on actions other than Index.

So I found that you can remove the controller from the url match and set the defaults as normal.

Putting this above the Default will always match first.

```cs
routes.MapRoute(
name: "Home",
url: "{action}",
defaults: new { controller = "Home", action = "Index" }
);
```