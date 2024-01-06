| Текст | Код |
|-------|-----|
| OnFireworkStarted<br>Вызывается при старте фейервеков<br>Возвращаемого значения не имеет | `void OnFireworkStarted(BaseFirework baseFirework)`<br>`{`<br>`Puts("OnFireworkStarted вызвался!");`<br>`}` |
| OnFireworkExhausted<br>Вызывается при исчервпывании фейервека<br>Возвращаемого значения не имеет | `void OnFireworkExhausted(BaseFirework baseFirework)`<br>`{`<br>`Puts("OnFireworkExhausted вызвался!");`<br>`}` |
| OnFireworkDamage<br>Вызывается при нанесении урона фейверку<br>Возвращаемое значение отличное от null переопределяет поведения нанесения урону фейервеку | `object OnFireworkDamage(BaseFirework baseFirework,HitInfo hitInfo)`<br>`{`<br>`Puts("OnFireworkDamage вызвался!");`<br>`}` |
| OnFireworkDesignChange<br>Вызывается при изменении дизайна фейверка<br>Возвращаемое значение отличное от null может переопределять применение изменения дизайна | `object OnFireworkDesignChange(PatternFirework patternFirework, ProtoBuf.PatternFirework.Design design, BasePlayer player)`<br>`{`<br>`Puts("OnFireworkDesignChange вызвался!"); `<br>`}` |
| OnFireworkDesignChanged<br>Вызывается после успешного изменения дизайна фейверка<br>Возвращаемого значения не имеет | `void OnFireworkDesignChanged(PatternFirework patternFirework, ProtoBuf.PatternFirework.Design design, BasePlayer player)`<br>`{`<br>`Puts("OnFireworkDesignChanged вызвался!");`<br>`}` |
