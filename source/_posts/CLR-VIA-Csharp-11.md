---
title: CLR-VIA-Csharp-11 Event
date: 2017-07-07 19:00:07
tags: CLR
categories: C#
---
> When a type defines an event member, it (instance of the type) can notify others objects that something special happened. Event provides a mechanism of interaction between the type or instance of the type and objects which care about the changes of the type or instance of the type. 
<!--more-->

1. Defining an event in the type means that type has the following capabilities:- A method can register its interest in the event (add_xxx).
- A method can unregister its interest in the event (remove_xxx).
- Registered methods will be notified when the events happened (delegate chain).
2. CLR's event model is based on Delegate which is a type-safe way to invoke a callback method.
3. By convention, classes that hold additional information to be passed to event handler must be derived from System.EventArgs.
```bash
   public event EventHandler<TSomeEventArgs> OnSomeEvent
   
   public delegate void EventHandler<TEventArgs>(Object sender, TEventArgs eventArgs)
```
4. An event member consists of the **event** keyword and a delegate of event handler.
5. Event handler must have a return type of **void**, the first parameter is for identifying the event source, the second parameter is derived **System.EventArgs**.
6. An event member is acutally translated into three constructs:
```bash
  public event EventHandler<TEventArgs> SomeEvent;

  private EventHandler<TEventArgs> registeredMethods;
 
  private void Add_SomeEvent(EventHandler<TEventArgs> value)
  
  private void Remove_SomeEvent(EventHandler<TEventArgs> value)
```
7. System.Delegate.Combine(current, value) insert value into the method chain of current, add return the reference to a list of delegates.
8. If you try to remove a method from the event, it would do nothing - no exception is raised.
9. Volatile.Read() suppresses compiler optimize.
10. InterLocked.CompareExchange
11. C# compiler has a built-in support of event. It translates += to add_xxx
12. Delegate.DynamicInvoke(new Object[] {sender, args}); It checks type safty with parameters of the methods that were invoke. It would raise an exception if failure.
