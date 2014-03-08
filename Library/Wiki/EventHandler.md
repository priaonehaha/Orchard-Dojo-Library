# Event handler



Event handlers in Orchard work just like in any other programming environment with a very interesting addition: they enable you to create extensions points to your features without worrying about coupling and references. So let's see how they work!

Every Orchard-y event handler starts with an interface, which derives from `IEventHandler`. In the inner workings of your module, you can inject a list of implementations of this interface, and now you just created the extension point for your module: if you call the methods on every injected implementation of your event handler, you enable other module authors to interact with your module if they implement this interface. That's okay so far, but in order to make it work, other module authors (or even you, if you want to extend the funtionalities of a feature not written by you) must have a reference to the module's project that hosts this event handler interface so they can use it for their implementations.

And here comes the twist: all you need to do to implement an event handler that is in an other module not referenced by your module is to have an interface in your module with the same name also deriving from `IEventHandler` and implement that interface! Aside from that, of course, the methods you implement must also have the same name and signature (if there are types that also come from an other module or project you are not referencing, you can replace them with `dynamic`s). Orchard will find these even more loosely coupled implementations solely based on their names and try to match the methods with the original interface. How cool is that?