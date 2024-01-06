| Текст | Код |
|-------|-----|
| OnFireworkStarted<br>вызывается при старте фейверков<br>возвращаемого значения не имеет | `void OnFireworkStarted(BaseFirework baseFirework)`<br>`{`<br>`Puts("OnFireworkStarted works!");`<br>`}` |
| Called when a server restart is being cancelled | `object OnServerRestartInterrupt() { Puts("OnServerRestartInterrupt works!"); return null; }` |
| Useful for saving something / etc on server shutdown | `void OnServerShutdown() { Puts("OnServerShutdown works!"); }` |
| Useful for intercepting commands before they get to their intended target | `object OnServerCommand(ConsoleSystem.Arg arg) { Puts("OnServerCommand works!"); return null; }` |
| Useful for intercepting server messages before they get to their intended target | `object OnMessagePlayer(string message, BasePlayer player) { Puts("OnMessagePlayer works!"); return null; }` |
| Called each frame | `void OnFrame() { /* Your code here */ }` |
