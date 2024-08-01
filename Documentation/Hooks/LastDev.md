# Hooks Documentation

## OnPlayerSpectate(BasePlayer,string)

### Summary


### Parameters
- `player`: Игрок, который начинает наблюдать.
- `targetPlayerId`: ID игрока, которого наблюдает игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerSpectate(BasePlayer player, string targetPlayerId)
{
    Puts($"Игрок {player.UserIDString} начинает наблюдать за игроком с ID {targetPlayerId}");
}


OnPlayerSpectate(BasePlayer, string)
{
    // Минимальный код для демонстрации функциональности
    Puts($"Игрок {player.UserIDString} начинает наблюдать за игроком с ID {targetPlayerId}");
}
```

## OnFuelConsumed(BaseOven,Item,ItemModBurnable)

### Summary


### Parameters
- `oven`: Печь.
- `fuel`: Использованное топливо.
- `burnable`: Объект, который сжигается.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFuelConsumed(BaseOven oven, Item fuel, ItemModBurnable burnable)
{
    Puts("OnFuelConsumed работает!");
    return null;
}
```

## OnNpcConversationStart(NPCTalking,BasePlayer,ConversationData)

### Summary


### Parameters
- `npc`: NPC, с которым происходит разговор.
- `player`: Игрок, участвующий в разговоре.
- `conversationData`: Данные о разговоре.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcConversationStart(NPCTalking npc, BasePlayer player, ConversationData conversationData)
{
    Puts("OnNpcConversationStart работает!");
    return null;
}
```

## OnCrateHack(HackableLockedCrate)

### Summary


### Parameters
- `crate`: Защищенный ящик.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCrateHack(HackableLockedCrate crate)
{
    Puts("OnCrateHack работает!");
}
```

## CanAffordToPlace(BasePlayer,Planner,Construction)

### Summary


### Parameters
- `player`: Игрок, пытающийся разместить объект.
- `planner`: Планировщик, который вызывает этот хук.
- `construction`: Объект, который игрок пытается разместить.

### Returns
Возвращает true, если игрок может afford разместить объект, и false в противном случае.

### Example
```csharp
object CanAffordToPlace(BasePlayer player, Planner planner, Construction construction)
{
    Puts("CanAffordToPlace работает!");
    
    // Если игрок не имеет владельца, он не может afford разместить объект
    if (!player)
    {
        return false;
    }
    
    // Вызовем хук CanAffordToPlace и вернем его результат
    object obj = Interface.CallHook("CanAffordToPlace", player, this, construction);
    if (obj is bool)
    {
        return (bool)obj;
    }
    
    // Если игрок в творческом режиме и freeBuild включен, он может afford разместить объект
    if (player.IsInCreativeMode && Creative.freeBuild)
    {
        return true;
    }
    
    // Проверим, есть ли у игрока достаточно ресурсов для разместения объекта
    foreach (ItemAmount item in construction.defaultGrade.CostToBuild())
    {
        if ((float)player.inventory.GetAmount(item.itemDef.itemid) < item.amount)
        {
            return false;
        }
    }
    
    // Если все проверки пройдены, игрок может afford разместить объект
    return true;
}
```

## OnDoorKnocked(DoorKnocker,BasePlayer)

### Summary


### Parameters
- `door`: Дверь, которую стукает игрок.
- `player`: Игрок, который стукает в дверь.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDoorKnocked(DoorKnocker door, BasePlayer player)
{
    Puts("OnDoorKnocked работает!");
    return null;
}
```

## OnGrowableGather(GrowableEntity,BasePlayer,bool)

### Summary


### Parameters
- `growableEntity`: Съедобная плода.
- `player`: Игрок, который собрал плоду.
- `eat`: Флаг, указывающий, нужно ли съесть собранную плоду.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnGrowableGather(GrowableEntity growableEntity, BasePlayer player, bool eat)
{
    Puts("OnGrowableGather работает!");
    return null;
}
```

## CanBeHomingTargeted(PlayerHelicopter)

### Summary


### Parameters
- `helicopter`: Игрок-вертолет.

### Returns
Возвращает true, если вертолет может быть целью для наведения, и false в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(PlayerHelicopter helicopter)
{
    Puts("CanBeHomingTargeted вызван!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnItemUnlock(Item)

### Summary


### Parameters
- `item`: Разблокированный предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemUnlock(Item item)
{
    Puts("OnItemUnlock работает!");
    return null;
}
```

## CanUseHelicopter(BasePlayer,CH47HelicopterAIController)

### Summary


### Parameters
- `player`: Игрок, пытающийся сесть.
- `helicopterController`: Контроллер вертолета.

### Returns
Возвращает true, если игрок может сесть в вертолет, и false в противном случае.

### Example
```csharp
bool CanUseHelicopter(BasePlayer player, CH47HelicopterAIController helicopterController)
{
    Puts("CanUseHelicopter работает!");
    // Здесь можно добавить логическую логику для определения возможности посадки игрока
    return true; // Возвращаем true по умолчанию
}
```

## OnTrapSnapped(BaseTrapTrigger,UnityEngine.GameObject,UnityEngine.Collider)

### Summary


### Parameters
- `trigger`: Триггер ловушки.
- `obj`: Объект, на который попал игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTrapSnapped(BaseTrapTrigger trigger, GameObject obj, Collider col)
{
    Puts("Игрок попал в ловушку!");
}
```

## OnBoomboxToggle(BoomBox,BasePlayer,bool)

### Summary


### Parameters
- `boombox`: Boombox, который был включен или выключен.
- `player`: Игрок, который выполнил действие.
- `isPlaying`: Флаг, указывающий, играет ли Boombox.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBoomboxToggle(BoomBox boombox, BasePlayer player, bool isPlaying)
{
    Puts("OnBoomboxToggle работает!");
    return null;
}
```

## OnDemoRecordingStopped(string,BasePlayer)

### Summary


### Parameters
- `filename`: Имя файла демонстрационной записи.
- `player`: Игрок, для которого была остановлена демонстрационная запись.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDemoRecordingStopped(string filename, BasePlayer player)
{
    Puts($"Демонстрационная запись для игрока {player} остановлена.");
    return null;
}
```

## OnCodeEntered(CodeLock,BasePlayer,string)

### Summary


### Parameters
- `lock`: Замок.
- `player`: Игрок.
- `code`: Введенный код.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCodeEntered(CodeLock lock, BasePlayer player, string code)
{
    Puts("OnCodeEntered работает!");
}
```

## OnCodeChanged(BasePlayer,CodeLock,string,bool)

### Summary


### Parameters
- `player`: Игрок, который изменил код.
- `lock`: Замок, у которого был изменен код.
- `newCode`: Новый код замка.
- `isGuest`: Флаг, указывающий, что новый код является гостевым.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnCodeChanged(BasePlayer player, CodeLock lock, string newCode, bool isGuest)
{
    Puts("OnCodeChanged работает!");
    return null;
}
```

## OnItemCraftFinished(ItemCraftTask,Item,ItemCrafter)

### Summary


### Parameters
- `task`: Задача по созданию предмета.
- `item`: Созданный предмет.
- `crafter`: Объект, который выполнил процесс создания.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemCraftFinished(ItemCraftTask task, Item item, ItemCrafter crafter)
{
    Puts("OnItemCraftFinished вызван!");
}
```

## OnItemFilter(Item,StorageContainer,int)

### Summary


### Parameters
- `item`: Предмет, который нужно проверить.
- `container`: Контейнер, в который нужно добавить предмет.
- `targetSlot`: Номер слота, на который нужно положить предмет.

### Returns
Возвращает true, если предмет допустим для добавления, и false в противном случае.

### Example
```csharp
object OnItemFilter(Item item, StorageContainer container, int targetSlot)
{
    Puts("OnItemFilter вызван!");
    // Здесь можно добавить дополнительную логику проверки предмета
    return null;
}
```

## CanUnlock(BasePlayer,ModularCarCodeLock,string)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть дверь.
- `lock`: Модульная замка двери.
- `codeEntered`: Введенный код.

### Returns
Возвращает true, если игрок может открыть дверь с помощью кода, и false в противном случае.

### Example
```csharp
bool CanUnlock(BasePlayer player, ModularCarCodeLock lock, string codeEntered)
{
    Puts("CanUnlock вызван!");
    
    // Если метод не переопределен, вернуть false
    return false;
}
```

## OnSignalBroadcast(BaseEntity)

### Summary


### Parameters
- `entity`: Сущность, откуда был отправлен сигнал.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSignalBroadcast(BaseEntity entity)
{
    Puts("OnSignalBroadcast работает!");
    return null;
}
```

## OnAdventGiftAward(AdventCalendar,BasePlayer)

### Summary


### Parameters
- `calendar`: Календарь advent.
- `player`: Игрок, которому выдается подарок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnAdventGiftAward(AdventCalendar calendar, BasePlayer player)
{
    Puts("OnAdventGiftAward работает!");
    return null;
}
```

## CanUnlock(BasePlayer,KeyLock)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть замок.
- `lock`: Замок, который нужно открыть.

### Returns
Возвращает true, если поведение по умолчанию переопределено, иначе false.

### Example
```csharp
bool CanUnlock(BasePlayer player, KeyLock lock)
{
    Puts("CanUnlock работает!");
    return false;
}
```

## OnNearbyTurretsScan(AutoTurret,System.Collections.Generic.List<AutoTurret>,bool)

### Summary


### Parameters
- `turret`: Тюрьма, которая вызывает сценарий.
- `nearbyTurrets`: Список ближайших тюрем.
- `created`: Флаг, указывающий, что тюрьма была создана.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnNearbyTurretsScan(AutoTurret turret, System.Collections.Generic.List<AutoTurret> nearbyTurrets, bool created)
{
    Puts("OnNearbyTurretsScan работает!");
    return null;
}
```

## OnEntityDestroy(CH47HelicopterAIController)

### Summary


### Parameters
- `controller`: Контроллер сущности.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityDestroy(CH47HelicopterAIController controller)
{
    Puts("OnEntityDestroy работает!");
    return null;
}
```

## OnExperimentEnded(Workbench)

### Summary


### Parameters
- `workbench`: Технологический стол, на котором проводился эксперимент.

### Returns
No return value.

### Example
```csharp
void OnExperimentEnded(Workbench workbench)
{
    Puts("Эксперимент завершился!");
}
```

## OnFishCatch(Item,BaseFishingRod,BasePlayer)

### Summary
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

**Main Loop**

The code runs in a loop until the fish is caught or the process fails.

**Flag Management**

The code manages several flags, which are used to track the state of the fishing process. These flags include:

* `flag`: Whether the player has pulled on the line.
* `flag2`: Whether the player has pulled on the line in a specific direction (left or right).
* `flag3`: Whether the player is pulling back on the line.

The code updates these flags based on user input and the current state of the fishing process.

**Fish State Management**

The code manages the state of the fish, which can be one of several states:

* `FishState.PullingBack`
* `FishState.PullingLeft`
* `FishState.PullingRight`

The code updates the fish state based on user input and the current state of the fishing process.

**Strain Timer**

The code has a strain timer that increments based on the player's actions. When the strain timer reaches 7 seconds, the fishing process fails.

**Client RPCs**

The code sends client-side RPCs to update the client's view of the fishing process. These RPCs include:

* `RpcTarget.NetworkGroup("Client_UpdateFishState")`: Updates the client's fish state.
* `RpcTarget.NetworkGroup("Client_OnCaughtFish")`: Notifies the client that a fish has been caught.

**Achievement Checking**

The code checks if the player has achieved a specific achievement related to catching all types of fish.

Overall, this code snippet appears to be responsible for managing the fishing mini-game in Rust, including updating flags and fish states, checking achievements, and sending client-side RPCs.
```

## OnWildlifeTrap(WildlifeTrap,TrappableWildlife)

### Summary


### Parameters
- `trap`: Ловушка, в которой было поймано животное.
- `wildlife`: Пойманное дикое животное.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnWildlifeTrap(WildlifeTrap trap, TrappableWildlife wildlife)
{
    Puts("OnWildlifeTrap работает!");
    return null;
}
```

## OnNpcEquipWeapon(ScientistNPC,Item)

### Summary


### Parameters
- `npc`: НПС, который оборудует оружие.
- `item`: Оборудованное оружие.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcEquipWeapon(ScientistNPC npc, Item item)
{
    Puts("OnNpcEquipWeapon работает!");
    return null;
}
```

## CanBeRecycled(Item,Recycler)

### Summary


### Parameters
- `item`: Предмет для проверки.
- `recycler`: Объект, который выполняет утилизацию.

### Returns
Возвращает true, если предмет можно утилизировать, и false в противном случае.

### Example
```csharp
object CanBeRecycled(Item item, Recycler recycler)
{
    Puts("CanBeRecycled работает!");
    
    // Если ReturnType - bool, вернуть значение
    if (item != null && item.info.Blueprint != null)
    {
        return true;
    }
    
    // Если ReturnType - object и не равно null, вернуть значение
    return false;
}
```

## OnQuarryConsumeFuel(MiningQuarry,Item)

### Summary


### Parameters
- `quarry`: Шахта, которая потребляет топливо.
- `item`: Топливо, которое будет использовано.

### Returns
Возвращает Item, если поведение по умолчанию переопределено.

### Example
```csharp
object OnQuarryConsumeFuel(MiningQuarry quarry, Item item)
{
    Puts("OnQuarryConsumeFuel работает!");
    return null;
}
```

## OnOpenVendingAdmin(VendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `player`: Игрок, открывающий административное меню.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnOpenVendingAdmin(VendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnOpenVendingAdmin работает!");
    return null;
}
```

## CanReceiveCall(PhoneController)

### Summary


### Parameters
- `controller`: Контроллер телефона.

### Returns
Возвращает <c>true</c>, если возможен прием вызова, и <c>false</c> в противном случае.

### Example
```csharp
bool CanReceiveCall(PhoneController controller)
{
    Puts("CanReceiveCall работает!");
    // Если RequirePower - true и контроллер не включен, вернуть false
    if (RequirePower && !IsPowered())
    {
        return false;
    }
    // Если RequireParent - true и контроллер не имеет родителя, вернуть false
    if (RequireParent && !base.baseEntity.HasParent())
    {
        return false;
    }
    // В противном случае возвращать true
    return true;
}
```

## OnTurretTarget(AutoTurret,BaseCombatEntity)

### Summary


### Parameters
- `turret`: Туррет.
- `targetEntity`: Новый таргет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretTarget(AutoTurret turret, BaseCombatEntity targetEntity)
{
    Puts("OnTurretTarget работает!");
    return null;
}
```

## OnEntityActiveCheck(BaseEntity,BasePlayer,uint,string)

### Summary


### Parameters
- `entity`: Сущность, которую необходимо проверить.
- `player`: Игрок, который проверяет сущность.
- `id`: Уникальный идентификатор игрока.
- `debugName`: Название для отладки.

### Returns
Возвращает true, если сущность активна, и false в противном случае.

### Example
```csharp
bool OnEntityActiveCheck(BaseEntity entity, BasePlayer player, uint id, string debugName)
{
    Puts("OnEntityActiveCheck вызван!");
    
    // Если сущность или игрок null, то сущность не активна
    if (entity == null || player == null)
    {
        return false;
    }
    
    object obj = Interface.CallHook("OnEntityActiveCheck", entity, player, id, debugName);
    if (obj is bool)
    {
        // Если возвращаемое значение является bool, то вернуть его
        return (bool)obj;
    }
    
    // Если сущность и игрок имеют одинаковый ID, то сущность активна
    if (entity.net.ID == player.net.ID)
    {
        return true;
    }
    
    // Если сущность не является родительской для игрока, то сущность не активна
    if (entity.parentEntity.uid != player.net.ID)
    {
        return false;
    }
    
    // Если игрок имеет активный предмет и этот предмет равен сущности, то сущность активна
    Item activeItem = player.GetActiveItem();
    if (activeItem == null || activeItem.GetHeldEntity() != entity)
    {
        return false;
    }
    
    // Если все условия выполнены, то сущность активна
    return true;
}
```

## CanHelicopterUseNapalm(PatrolHelicopterAI)

### Summary


### Parameters
- `ai`: Объект-патрульный вертолет.

### Returns
Возвращает true, если вертолет может использовать зажигательную смесь, и false в противном случае.

### Example
```csharp
bool CanHelicopterUseNapalm(PatrolHelicopterAI ai)
{
    Puts("CanHelicopterUseNapalm работает!");
    // Здесь можно добавить логическую логику для определения возможности использования зажигательной смеси
    return true; // или false в зависимости от условий
}
```

## OnPhoneCallStarted(PhoneController,PhoneController,BasePlayer)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `activeCallTo`: Активный номер вызова.
- `currentPlayer`: Текущий игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnPhoneCallStarted(PhoneController phoneController, PhoneController activeCallTo, BasePlayer currentPlayer)
{
    Puts("OnPhoneCallStarted работает!");
    return null;
}
```

## OnSignUpdated(CarvablePumpkin,BasePlayer)

### Summary


### Parameters
- `sign`: Объект знака.
- `player`: Игрок, который обновил знак.

### Returns
No return value.

### Example
```csharp
object OnSignUpdated(CarvablePumpkin sign, BasePlayer player)
{
    Puts($"Знак '{sign}' был обновлен игроком {player}");
    return null;
}
```

## OnVendingShopOpen(VendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `player`: Игрок, открывающий автомат.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVendingShopOpen(VendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnVendingShopOpen работает!");
    return null;
}
```

## OnExcavatorMiningToggled(ExcavatorArm)

### Summary


### Parameters
- `excavatorArm`: Экскаваторная рука, которая выполняет процесс добычи.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnExcavatorMiningToggled(ExcavatorArm excavatorArm)
{
    Puts("OnExcavatorMiningToggled работает!");
    return null;
}
```

## OnClientProjectileEffectCreate(Network.Connection,BaseProjectile,string)

### Summary


### Parameters
- `connection`: Соединение, с которого был отправлен проектил.
- `projectile`: Проектил, который вызвал эффект.
- `prefabName`: Имя префаба эффекта.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnClientProjectileEffectCreate(Network.Connection connection, BaseProjectile projectile, string prefabName)
{
    Puts("OnClientProjectileEffectCreate работает!");
    return null;
}
```

## OnHorseLead(BaseRidableAnimal,BasePlayer)

### Summary


### Parameters
- `animal`: Лошадь, которую управляет игрок.
- `player`: Игрок, управляющий лошадью.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHorseLead(BaseRidableAnimal animal, BasePlayer player)
{
    Puts("OnHorseLead работает!");
    return null;
}
```

## IOnBaseCombatEntityHurt(BaseCombatEntity,HitInfo)

### Summary
Документация для IOnBaseCombatEntityHurt(BaseCombatEntity, HitInfo)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для IOnBaseCombatEntityHurt(BaseCombatEntity, HitInfo)

**Описание**

Этот хук вызывается в методе Hurt(HitInfo info) и позволяет модулю или плагину изменить поведение при нанесении урона игровому сущности.

**Параметры**

* `BaseCombatEntity`: Объект-цель, на который был нанесен урон.
* `HitInfo`: Информация о ударе, включая тип и силу удара.

**Возвращаемое значение**

Хук возвращает null или не возвращает значения, если модуль или плагин не изменяет поведение.

**Пример использования**

```csharp
public class MyPlugin : MonoBehaviour
{
    public void OnBaseCombatEntityHurt(BaseCombatEntity entity, HitInfo info)
    {
        // Измените поведение при нанесении урона
        Puts("Нанесен урон!");
    }
}
```

**Структура метода**

* `public virtual void Hurt(HitInfo info)`: Метод Hurt(HitInfo info), в котором вызывается хук.
* `if (Interface.CallHook("IOnBaseCombatEntityHurt", this, info) != null)` : Проверка, вызвана ли хук и если да, то возвращается из метода Hurt(HitInfo info).

**Минимальный код для демонстрации функциональности**

```csharp
public class MyPlugin : MonoBehaviour
{
    public void OnBaseCombatEntityHurt(BaseCombatEntity entity, HitInfo info)
    {
        Puts("Нанесен урон!");
    }
}
```

Этот хук можно использовать для различных целей, таких как изменение поведения при нанесении урона, логирование ударов или изменения игровых правил.
```

## OnAddVendingOffer(VendingMachine,ProtoBuf.VendingMachine.SellOrder)

### Summary


### Parameters
- `vendingMachine`: Автомат, для которого добавляется предложение.
- `sellOrder`: Предложение о продаже предмета.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnAddVendingOffer(VendingMachine vendingMachine, ProtoBuf.VendingMachine.SellOrder sellOrder)
{
    Puts($"Добавлено предложение для автомата {vendingMachine} по цене {sellOrder.currencyAmountPerItem} {sellOrder.currencyID}");
}
```

## OnHelicopterRetire(PatrolHelicopterAI)

### Summary


### Parameters
- `helicopter`: Патрульный вертолет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnHelicopterRetire(PatrolHelicopterAI helicopter)
{
    Puts("Вертолет завершает свою миссию!");
}
```

## CanElevatorLiftMove(ElevatorLift)

### Summary


### Parameters
- `elevatorLift`: Элеватор, который должен поднять груз.

### Returns
Возвращает <c>true</c>, если элеватор может поднять груз, и <c>false</c> в противном случае.

### Example
```csharp
bool CanElevatorLiftMove(ElevatorLift elevatorLift)
{
    Puts("CanElevatorLiftMove работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnOvenStart(BaseOven)

### Summary


### Parameters
- `oven`: Печь.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnOvenStart(BaseOven oven)
{
    Puts("OnOvenStart работает!");
    return null;
}
```

## OnMapImageUpdated()

### Summary


### Parameters
- `id`: ID игрока.
- `imageType`: Тип картинки (0 - туман, 1 - краска).
- `imageNumber`: Номер картинки.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMapImageUpdated(uint id, byte imageType, uint imageNumber)
{
    Puts($"Картинка на карте обновлена для ID {id} типа {imageType} и номера {imageNumber}");
}
```

## IOnNpcTarget(BaseNpc,BaseEntity)

### Summary


### Parameters
- `npc`: НПС, который определяет цель.
- `target`: Объект, который может быть целью НПС.

### Returns
Возвращает значение float, указывающее на желание атаковать. Если поведение по умолчанию не переопределено, возвращается 0.

### Example
```csharp
float IOnNpcTarget(BaseNpc npc, BaseEntity target)
{
    Puts("IOnNpcTarget работает!");
    return 0;
}
```

## OnSignLocked(PhotoFrame,BasePlayer)

### Summary


### Parameters
- `sign`: Знак, который был заблокирован.
- `player`: Игрок, который заблокировал знак.

### Returns
No return value.

### Example
```csharp
object OnSignLocked(PhotoFrame sign, BasePlayer player)
{
    Puts("OnSignLocked работает!");
    return null;
}
```

## OnCorpsePopulate(ScarecrowNPC,NPCPlayerCorpse)

### Summary


### Parameters
- `scarecrowNPC`: Скрипт NPC.
- `npcPlayerCorpse`: Тело игрока.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCorpsePopulate(ScarecrowNPC scarecrowNPC, NPCPlayerCorpse npcPlayerCorpse)
{
    // Минимальный код для демонстрации функциональности
    Puts("Тело игрока создано.");
}
```

## CanLootPlayer(BasePlayer,BasePlayer)

### Summary


### Parameters
- `looter`: Игрок, пытающийся открыть лут.
- `targetPlayer`: Игрок, для которого открывается лут.

### Returns
Возвращает true, если лут можно открыть, и false в противном случае.

### Example
```csharp
bool CanLootPlayer(BasePlayer looter, BasePlayer targetPlayer)
{
    Puts("CanLootPlayer вызван!");
    // Если ReturnType - bool, верните значение
    return !looter.IsSamePlayer(targetPlayer);
}
```

## CanLootEntity(BasePlayer,BaseRidableAnimal)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `entity`: Сущность, с которой открывается лут.

### Returns
Возвращает true, если поведение по умолчанию не переопределено.

### Example
```csharp
bool CanLootEntity(BasePlayer player, BaseRidableAnimal entity)
{
    Puts("CanLootEntity работает!");
    return true;
}
```

## OnWorldPrefabSpawned(UnityEngine.GameObject,string)

### Summary


### Parameters
- `gameObject`: Объект-реализация префаба.
- `category`: Категория префаба.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnWorldPrefabSpawned(UnityEngine.GameObject gameObject, string category)
{
    Puts($"Префаб '{category}' спавнился в мире!");
    return null;
}
```

## OnItemStacked(Item,Item,ItemContainer)

### Summary
This is a C# method that appears to be part of an item management system in a game. It's responsible for moving an item from one container to another. Here's a breakdown of the code:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of an item management system in a game. It's responsible for moving an item from one container to another. Here's a breakdown of the code:

**Method signature**

The method takes several parameters:

* `ItemContainer newcontainer`: The destination container.
* `int iTargetPos`: The position within the destination container where the item should be placed.
* `bool allowStack`: Whether the item can be stacked with existing items in the destination container.
* `bool ignoreStackLimit`: Whether to ignore the maximum stack size of the destination container.
* `BasePlayer sourcePlayer`: The player who initiated the move.

**Method body**

The method first checks if the destination container is the same as the current parent container. If so, it simply updates the item's position within that container and returns true.

Next, it checks if the destination container has a maximum stack size and if the item's amount exceeds that limit. If so, it splits the item into multiple items with the maximum stack size and attempts to move each one separately.

If the item can be moved to the destination container without splitting, it removes the item from its current container, updates the item's position within the new container, and returns true.

Finally, if all else fails, it drops the item at the destination container's drop position with a velocity of 0 (i.e., it simply disappears).

**Hooks**

The method calls two hooks:

* `OnItemStacked`: This hook is called when an item is stacked with existing items in the destination container.
* `OnItemMoved`: This hook is not explicitly called, but it's likely used elsewhere in the code to notify other components of the item move.

Overall, this method appears to be responsible for moving items between containers while handling stacking and splitting logic.
```

## OnInputUpdate(IOEntity,int,int)

### Summary


### Parameters
- `entity`: Объект, для которого обновляются входные данные.
- `inputAmount`: Количество входных данных.
- `inputSlot`: Номер слота входных данных.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnInputUpdate(IOEntity entity, int inputAmount, int inputSlot)
{
    Puts("OnInputUpdate работает!");
    return null;
}
```

## OnWireConnect(BasePlayer,IOEntity,int,IOEntity,int,System.Collections.Generic.List<UnityEngine.Vector3>,System.Collections.Generic.List<float>)

### Summary
**OnWireConnect(BasePlayer, IOEntity, int, IOEntity, int, System.Collections.Generic.List<UnityEngine.Vector3>, System.Collections.Generic.List<float>)**

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
**OnWireConnect(BasePlayer, IOEntity, int, IOEntity, int, System.Collections.Generic.List<UnityEngine.Vector3>, System.Collections.Generic.List<float>)**

#### Описание
Этот хук вызывается при установке соединения между двумя сущностями IO.

#### Параметры

* `BasePlayer player`: Игрок, который устанавливает соединение.
* `IOEntity iOEntity`: Первая сущность IO, к которой будет подключена вторая.
* `int inputIndex`: Индекс входа в первой сущности IO.
* `IOEntity iOEntity2`: Вторая сущность IO, которая будет подключена к первой.
* `int outputIndex`: Индекс выхода во второй сущности IO.
* `System.Collections.Generic.List<UnityEngine.Vector3> linePoints`: Координаты линии соединения.
* `System.Collections.Generic.List<float> slackLevels`: Уровни расслабления для соединения.

#### Минимальный код
```csharp
public void OnWireConnect(BasePlayer player, IOEntity iOEntity, int inputIndex, IOEntity iOEntity2, int outputIndex, System.Collections.Generic.List<UnityEngine.Vector3> linePoints, System.Collections.Generic.List<float> slackLevels)
{
    // Код для демонстрации функциональности соединения
}
```

#### Примечания

* Этот хук вызывается в методе `RPC_MakeConnection` после проверки условий установления соединения.
* Если этот хук не будет вызван, соединение не будет установлено.
```

## OnPayForUpgrade(BasePlayer,BuildingBlock,ConstructionGrade)

### Summary


### Parameters
- `player`: Игрок, который оплачивает улучшение.
- `block`: Блок, который улучшается.
- `grade`: Степень улучшения.

### Returns
Возвращает true, если улучшение было успешно оплачено, и false в противном случае.

### Example
```csharp
bool OnPayForUpgrade(BasePlayer player, BuildingBlock block, ConstructionGrade grade)
{
    Puts("OnPayForUpgrade вызван!");
    
    // Код для демонстрации функциональности
    return true;
}
```

## OnServerRestart(string,int)

### Summary
Документация для метода `OnServerRestart(string,int)`:

### Parameters
- `strNotice`: Сообщение, которое будет показано игрокам.
- `iSeconds`: Количество секунд, до того как сервер перезапустится.

### Returns
Возвращает значение, указывающее, что хук был успешно вызван.

### Example
```csharp
Документация для метода `OnServerRestart(string,int)`:

object OnServerRestart(string strNotice, int iSeconds)
{
    Puts($"Сервер перезагружается через {iSeconds} секунд. Сообщение: {strNotice}");
    return null;
}
```

## OnPhoneAnswer(PhoneController,PhoneController)

### Summary


### Parameters
- `caller`: Контроллер телефона, совершивший вызов.
- `callee`: Контроллер телефона, принимающий вызов.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhoneAnswer(PhoneController caller, PhoneController callee)
{
    Puts("OnPhoneAnswer работает!");
}

В этом методе нет оператора return, что указывает на то, что тип возвращаемого значения равен void.
```

## OnOvenTemperature(BaseOven,int)

### Summary


### Parameters
- `oven`: Объект духовки.
- `slot`: Номер слота в духовке.

### Returns
Возвращает температуру духовки в градусах по Фаренгейту, если поведение по умолчанию переопределено.

### Example
```csharp
float OnOvenTemperature(BaseOven oven, int slot)
{
    Puts("OnOvenTemperature вызван!");
    return 0f; // Возвращаемое значение по умолчанию
}
```

## OnCoalingTowerStart(CoalingTower,BasePlayer)

### Summary


### Parameters
- `coalingTower`: Коалинг танк.
- `player`: Игрок, который начал процесс зарядки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCoalingTowerStart(CoalingTower coalingTower, BasePlayer player)
{
    Puts("OnCoalingTowerStart работает!");
    return null;
}
```

## CanHelicopterTarget(PatrolHelicopterAI,BasePlayer)

### Summary


### Parameters
- `patrolHelicopterAI`: Объект AI патрульного вертолета.
- `targetPlayer`: Игрок, который является потенциальной целью.

### Returns
Возвращает true, если игрок может быть целью для патрульного вертолета, иначе false.

### Example
```csharp
bool CanHelicopterTarget(PatrolHelicopterAI patrolHelicopterAI, BasePlayer targetPlayer)
{
    Puts("CanHelicopterTarget работает!");
    // Код для демонстрации функциональности
    return true;
}
```

## OnPlayerHealthChange(BasePlayer,float,float)

### Summary


### Parameters
- `player`: Игрок, у которого изменилось здоровье.
- `oldHealth`: Старое значение здоровья игрока.
- `newHealth`: Новое значение здоровья игрока.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerHealthChange(BasePlayer player, float oldHealth, float newHealth)
{
    Puts($"Здоровье игрока {player.UserIDString} изменилось с {oldHealth} до {newHealth}");
    return null;
}
```

## OnDemoRecordingStart(string,BasePlayer)

### Summary


### Parameters
- `filePath`: Путь к файлу записи.
- `player`: Игрок, который начинает запись.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDemoRecordingStart(string filePath, BasePlayer player)
{
    Puts($"Начата запись демонстрации в файл {filePath}");
    return null;
}
```

## OnItemSubmit(Item,Mailbox,BasePlayer)

### Summary


### Parameters
- `item`: Подаваемый предмет.
- `mailbox`: Ящик, в который подан предмет.
- `player`: Игрок, подавший предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemSubmit(Item item, Mailbox mailbox, BasePlayer player)
{
    Puts("OnItemSubmit работает!");
    return null;
}
```

## OnStructureRepair(BaseCombatEntity,BasePlayer)

### Summary
Документация для метода `OnStructureRepair(BaseCombatEntity, BasePlayer)`:

### Parameters
- `entity`: Структура, которую пытаются отремонтировать.
- `player`: Игрок, который пытается отремонтировать структуру.

### Returns
Нет возвращаемого значения.

### Example
```csharp
Документация для метода `OnStructureRepair(BaseCombatEntity, BasePlayer)`:

```rust
void OnStructureRepair(BaseCombatEntity entity, BasePlayer player)
{
    // Минимальный код для демонстрации функциональности
    Puts($"Игрок {player.UserID} пытается отремонтировать структуру {entity.EntityID}");
}
```

В этом методе нет возвращаемого значения, поэтому оператор `return` пропущен. Метод вызывается при попытке ремонта структуры и принимает на вход структуру (`BaseCombatEntity`) и игрока (`BasePlayer`).
```

## CanHelicopterStrafeTarget(PatrolHelicopterAI,BasePlayer)

### Summary


### Parameters
- `helicopterAI`: Объект AI вертолета.
- `targetPlayer`: Игрок, против которого ведется стрельба.

### Returns
Возвращает true, если возможность стрельбы по цели доступна, и false в противном случае.

### Example
```csharp
bool CanHelicopterStrafeTarget(PatrolHelicopterAI helicopterAI, BasePlayer targetPlayer)
{
    Puts("CanHelicopterStrafeTarget работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true; // Возвращаем значение по умолчанию
}
```

## OnStashExposed(StashContainer,BasePlayer)

### Summary


### Parameters
- `stash`: Стэш, который стал видимым.
- `player`: Игрок, который увидел стэш.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnStashExposed(StashContainer stash, BasePlayer player)
{
    Puts($"Стэш {stash} стал видимым для игрока {player}");
}
```

## CanLootEntity(BasePlayer,StorageContainer)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `container`: Сохранение контейнера.

### Returns
Возвращает true, если игрок может открыть лут, и false в противном случае.

### Example
```csharp
bool CanLootEntity(BasePlayer player, StorageContainer container)
{
    Puts("CanLootEntity работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true;
}
```

## OnPhoneDialTimeout(PhoneController,PhoneController,BasePlayer)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `otherPhoneController`: Контроллер другого телефона.
- `player`: Игрок, совершивший вызов.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPhoneDialTimeout(PhoneController phoneController, PhoneController otherPhoneController, BasePlayer player)
{
    Puts("OnPhoneDialTimeout работает!");
    return null;
}
```

## CanRecycle(Recycler,Item)

### Summary


### Parameters
- `recycler`: Объект, который может перерабатывать предмет.
- `item`: Предмет для проверки.

### Returns
Возвращает true, если предмет можно переработать, и false в противном случае.

### Example
```csharp
bool CanRecycle(Recycler recycler, Item item)
{
    Puts("CanRecycle работает!");
    // Здесь вы можете добавить логику для определения, можно ли перерабатывать предмет
    return true; // или false, в зависимости от условий
}
```

## OnCCTVDirectionChange(CCTV_RC,BasePlayer)

### Summary


### Parameters
- `cctv`: Объект камеры наблюдения.
- `player`: Игрок, который изменил направление камеры.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCCTVDirectionChange(CCTV_RC cctv, BasePlayer player)
{
    Puts("OnCCTVDirectionChange работает!");
}
```

## OnWaterCollect(WaterCatcher)

### Summary


### Parameters
- `waterCatcher`: Объект, который собирает воду.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnWaterCollect(WaterCatcher waterCatcher)
{
    Puts("OnWaterCollect работает!");
    return null;
}
```

## OnTeamPromote(RelationshipManager.PlayerTeam,BasePlayer)

### Summary


### Parameters
- `team`: Команда, которую необходимо продвинуть.
- `player`: Игрок, которого необходимо продвинуть.

### Returns
Возвращает null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnTeamPromote(RelationshipManager.PlayerTeam team, BasePlayer player)
{
    Puts("OnTeamPromote работает!");
    return null;
}
```

## OnMapMarkersClear(BasePlayer,System.Collections.Generic.List<ProtoBuf.MapNote>)

### Summary


### Parameters
- `player`: Игрок.
- `markers`: Список маркеров для очистки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMapMarkersClear(BasePlayer player, System.Collections.Generic.List<ProtoBuf.MapNote> markers)
{
    Puts("OnMapMarkersClear работает!");
    return null;
}
```

## OnFuelCheck(EntityFuelSystem)

### Summary


### Parameters
- `fuelSystem`: Система топливоснабжения.

### Returns
Возвращает true, если система топливоснабжения имеет топливо, и false в противном случае.

### Example
```csharp
bool OnFuelCheck(EntityFuelSystem fuelSystem)
{
    Puts("OnFuelCheck вызван!");
    return true; // Возвращаемое значение системы топливоснабжения
}
```

## OnSamSiteTargetScan(SamSite,System.Collections.Generic.List<SamSite.ISamSiteTarget>)

### Summary


### Parameters
- `samSite`: САМ-сайт.
- `targets`: Список потенциальных целей.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSamSiteTargetScan(SamSite samSite, List<SamSite.ISamSiteTarget> targets)
{
    Puts("OnSamSiteTargetScan работает!");
}
```

## OnBookmarkInput(ComputerStation,BasePlayer,InputState)

### Summary


### Parameters
- `computerStation`: Экземпляр ComputerStation.
- `player`: Игрок, который предоставил входные данные.
- `inputState`: Состояние входных данных.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarkInput(ComputerStation computerStation, BasePlayer player, InputState inputState)
{
    Puts("OnBookmarkInput работает!");
    return null;
}
```

## OnItemSkinChange(int,Item,RepairBench,BasePlayer)

### Summary
This is a C# code snippet that appears to be part of a game server's logic for applying skins to items in the game. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game server's logic for applying skins to items in the game. Here's a breakdown of what it does:

**Functionality**

The code allows players to apply skins to items, such as guns or other equipment, using a "skin changer" mechanic. When a player selects an item and chooses a skin from their inventory, this code is executed.

**Key Steps**

1. **Validation**: The code checks if the player has the required item (the one they want to skin) in their inventory. If not, it returns without applying the skin.
2. **Skin selection**: It retrieves the selected skin from the player's inventory and applies it to the item using a custom `ApplySkinToItem` function (not shown here).
3. **Redirect handling**: If the applied skin has a redirect (i.e., another item that should be used instead), it updates the item's properties accordingly.
4. **Inventory management**: It removes the original item from the player's inventory and adds the new, skinned item to their inventory.
5. **Analytics tracking**: The code sends analytics data to track the skin application event.

**Notes**

* This code assumes that the game has a custom `ItemSkinDirectory.Skin` class and an `ItemManager` class for managing items in the game world.
* The `ApplySkinToItem` function is not shown here, but it's likely responsible for updating the item's appearance and properties based on the applied skin.
* The code uses Facepunch's Pool system to manage memory allocation for lists of items.

If you have any specific questions about this code or would like me to elaborate on certain points, feel free to ask!
```

## OnSupplyDropDropped(BaseEntity,CargoPlane)

### Summary


### Parameters
- `droppedEntity`: Объект, который упал.
- `cargoPlane`: Самолет, из которого упал объект.

### Returns
No return value.

### Example
```csharp
object OnSupplyDropDropped(BaseEntity droppedEntity, CargoPlane cargoPlane)
{
    Puts("OnSupplyDropDropped вызван!");
    // Здесь можно добавить код для обработки выпавшего контейнера с грузом
    return null;
}
```

## CanUseFuel(EntityFuelSystem,StorageContainer,float,float)

### Summary


### Parameters
- `entity`: Сущность, на которой установлена система.
- `container`: Контейнер с топливом.
- `seconds`: Время использования топлива.
- `fuelUsedPerSecond`: Использоваемое топливо в секунду.

### Returns
Возвращает количество использованного топлива, если поведение по умолчанию переопределено. В противном случае возвращается 0.

### Example
```csharp
object CanUseFuel(EntityFuelSystem entity, StorageContainer container, float seconds, float fuelUsedPerSecond)
{
    Puts("CanUseFuel работает!");
    return null;
}
```

## OnLootSpawn(LootContainer)

### Summary


### Parameters
- `lootContainer`: Контейнер с лутом.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootSpawn(LootContainer lootContainer)
{
    Puts("OnLootSpawn работает!");
    return null;
}
```

## OnPlayerAssist(BasePlayer,BasePlayer)

### Summary


### Parameters
- `assister`: Игрок, оказывающий помощь.
- `target`: Раненный игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerAssist(BasePlayer assister, BasePlayer target)
{
    Puts($"Игрок {assister.UserID} оказывает помощь раненному игроку {target.UserID}");
}
```

## IOnServerInitialized()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void IOnServerInitialized()
{
    Puts("Сервер успешно инициализирован!");
}
```

## OnDecayDamage(DecayEntity)

### Summary


### Parameters
- `entity`: Сущность, подвергающаяся разложению.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDecayDamage(DecayEntity entity)
{
    Puts("OnDecayDamage работает!");
}

```

## OnActiveItemChange(BasePlayer,Item,ItemId)

### Summary


### Parameters
- `player`: Игрок, чей активный предмет изменился.
- `oldItem`: Старый активный предмет игрока.
- `newItemId`: ID нового активного предмета игрока.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnActiveItemChange(BasePlayer player, Item oldItem, ItemId newItemId)
{
    Puts("OnActiveItemChange работает!");
    return null;
}
```

## OnOvenStarted(BaseOven)

### Summary


### Parameters
- `oven`: Печь.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnOvenStarted(BaseOven oven)
{
    Puts("Печка запущена!");
}
```

## OnSupplyDropLanded(SupplyDrop)

### Summary


### Parameters
- `supplyDrop`: Объект Supply Drop.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSupplyDropLanded(SupplyDrop supplyDrop)
{
    Puts("OnSupplyDropLanded работает!");
}
```

## OnSignalBroadcast(BaseEntity,Network.Connection)

### Summary


### Parameters
- `entity`: Эntity, откуда был отправлен сигнал.
- `connection`: Подключение, через которое был отправлен сигнал.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSignalBroadcast(BaseEntity entity, Network.Connection connection)
{
    Puts("OnSignalBroadcast работает!");
    return null;
}
```

## OnOvenCooked(BaseOven,Item,BaseEntity)

### Summary


### Parameters
- `oven`: Печь, в которой был приготовлен предмет.
- `item`: Приготовленный предмет.
- `entity`: Сущность, связанная с процессом приготовления.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnOvenCooked(BaseOven oven, Item item, BaseEntity entity)
{
    Puts("OnOvenCooked работает!");
    return null;
}
```

## OnConstructionPlace(BaseEntity,Construction,Construction.Target,BasePlayer)

### Summary


### Parameters
- `baseEntity`: Объект, который был размещен.
- `construction`: Конструкция, для которой был размещен объект.
- `target`: Целевая точка, где был размещен объект.
- `ownerPlayer`: Игрок, который разместил объект.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnConstructionPlace(BaseEntity baseEntity, Construction construction, Construction.Target target, BasePlayer ownerPlayer)
{
    Puts($"Объект {baseEntity} размещен на месте {target} игроком {ownerPlayer}");
}
```

## OnGrowableStateChange(GrowableEntity,PlantProperties.State)

### Summary


### Parameters
- `entity`: Объект-растение.
- `newState`: Новое состояние растения.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnGrowableStateChange(GrowableEntity entity, PlantProperties.State newState)
{
    Puts("OnGrowableStateChange работает!");
    return null;
}
```

## OnLootEntityEnd(BasePlayer,ContainerIOEntity)

### Summary


### Parameters
- `player`: Игрок, который закончил лутить.
- `entity`: Сущность, которую игрок лутил.

### Returns
No return value.

### Example
```csharp
object OnLootEntityEnd(BasePlayer player, ContainerIOEntity entity)
{
    Puts("OnLootEntityEnd вызван!");
    return null;
}
```

## CanBeTargeted(BaseCombatEntity,HelicopterTurret)

### Summary


### Parameters
- `entity`: Целевая сущность.
- `turret`: Турель, из которой будет произведено выстрел.

### Returns
Возвращает true, если цель может быть поражена, и false в противном случае.

### Example
```csharp
bool CanBeTargeted(BaseCombatEntity entity, HelicopterTurret turret)
{
    Puts("CanBeTargeted вызван!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnRackedWeaponLoad(Item,ItemDefinition,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Оружие.
- `itemDefinition`: Определение патрона.
- `player`: Игрок, который выполняет действие.
- `weaponRack`: Ящик оружия.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponLoad(Item item, ItemDefinition itemDefinition, BasePlayer player, WeaponRack weaponRack)
{
    Puts("OnRackedWeaponLoad работает!");
}
```

## OnTeamUpdated(ulong,ProtoBuf.PlayerTeam,BasePlayer)

### Summary
Документация для метода `OnTeamUpdated`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnTeamUpdated`:

**Название:** OnTeamUpdated

**Описание:** Этот хук вызывается при обновлении информации о команде, в которой находится игрок.

**Параметры:**

* `ulong`: Идентификатор команды.
* `ProtoBuf.PlayerTeam`: Объект с информацией о команде.
* `BasePlayer`: Объект игрока.

**Функция:** Этот хук вызывается в методе `TeamUpdate` и используется для обновления информации о команде, которую получает игрок. Он включает в себя обновление списка участников команды, а также информацию о лидере команды.

**Пример использования:**

```csharp
public void TeamUpdate(bool fullTeamUpdate)
{
    // ...
    Interface.CallHook("OnTeamUpdated", currentTeam, playerTeam2, this);
    // ...
}
```

В этом примере метод `OnTeamUpdated` вызывается в методе `TeamUpdate`, когда информация о команде обновляется.
```

## OnRconConnection(System.Net.IPAddress)

### Summary


### Parameters
- `address`: Адрес клиента.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRconConnection(System.Net.IPAddress address)
{
    Puts("OnRconConnection вызван!");
    return null;
}
```

## OnEntityTakeDamage(ResourceEntity,HitInfo)

### Summary


### Parameters
- `entity`: Сущность, получающая урон.
- `hitInfo`: Информация о ударе.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityTakeDamage(ResourceEntity entity, HitInfo hitInfo)
{
    Puts("OnEntityTakeDamage работает!");
    return null;
}
```

## OnOutputUpdate(IOEntity)

### Summary


### Parameters
- `ioEntity`: Объект IO, с которым взаимодействует.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnOutputUpdate(IOEntity ioEntity)
{
    Puts("OnOutputUpdate работает!");
}
```

## OnExcavatorResourceSet(ExcavatorArm,string,BasePlayer)

### Summary


### Parameters
- `excavatorArm`: Экскаваторная рука.
- `resourceName`: Название ресурса.
- `player`: Игрок, который установил ресурс.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnExcavatorResourceSet(ExcavatorArm excavatorArm, string resourceName, BasePlayer player)
{
    Puts($"Ресурс для экскаватора '{excavatorArm}' установлен: {resourceName}");
    return null;
}
```

## OnPlayerPveDamage(BaseEntity,HitInfo,BuildingBlock)

### Summary


### Parameters
- `initiator`: Игрок, наносящий урон.
- `info`: Информация о хите.
- `target`: Цель урона.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerPveDamage(BaseEntity initiator, HitInfo info, BaseEntity target)
{
    Puts("OnPlayerPveDamage работает!");
    return null;
}
```

## OnContainerDropItems(ItemContainer)

### Summary


### Parameters
- `container`: Контейнер, из которого выпадают предметы.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnContainerDropItems(ItemContainer container)
{
    Puts("OnContainerDropItems работает!");
    return null;
}
```

## OnGrowableGathered(GrowableEntity,Item,BasePlayer)

### Summary


### Parameters
- `growableEntity`: Сущность, из которой собрана плода.
- `item`: Собранная плода.
- `player`: Игрок, который собрал плоду.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnGrowableGathered(GrowableEntity growableEntity, Item item, BasePlayer player)
{
    Puts("OnGrowableGathered работает!");
    return null;
}
```

## OnItemDeployed(Deployer,BaseEntity,BaseEntity)

### Summary
Документация для хука `OnItemDeployed(Deployer,BaseEntity,BaseEntity)`

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для хука `OnItemDeployed(Deployer,BaseEntity,BaseEntity)`

**Описание**

Хук вызывается при развертывании предмета на игровом мире.

**Параметры**

* `Deployer`: Объект, который выполнил действие развертывания.
* `BaseEntity`: Основной объект, на котором был развернут предмет.
* `BaseEntity2`: Объект, который был развернут.

**Пример использования**

```csharp
public void OnItemDeployed(Deployer deployer, BaseEntity baseEntity, BaseEntity baseEntity2)
{
    Puts($"Предмет '{baseEntity2.prefabID}' развернут на '{baseEntity.prefabID}'");
}
```

**Структура метода**

* `OnItemDeployed` - имя метода.
* `(Deployer deployer, BaseEntity baseEntity, BaseEntity baseEntity2)` - параметры метода.
* `Puts($"Предмет '{baseEntity2.prefabID}' развернут на '{baseEntity.prefabID}'");` - оператор вывода сообщения в консоль.

**Примечание**

Хук вызывается после того, как предмет был успешно развернут на игровом мире.
```

## OnStructureUpgrade(BuildingBlock,BasePlayer,BuildingGrade.Enum,ulong)

### Summary


### Parameters
- `block`: Блок, который подвергается обновлению.
- `player`: Игрок, выполняющий обновление.
- `grade`: Новая степень структуры.
- `upgradeId`: Идентификатор обновления.

### Returns
Возвращает null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnStructureUpgrade(BuildingBlock block, BasePlayer player, BuildingGrade.Enum grade, ulong upgradeId)
{
    Puts("OnStructureUpgrade вызван!");
    return null;
}
```

## CanUseMailbox(BasePlayer,Mailbox)

### Summary


### Parameters
- `player`: Игрок, пытающийся использовать ящик.
- `mailbox`: Ящик, который хочет использовать игрок.

### Returns
Возвращает true, если игрок может использовать ящик, и false в противном случае.

### Example
```csharp
bool CanUseMailbox(BasePlayer player, Mailbox mailbox)
{
    Puts("CanUseMailbox работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnRotateVendingMachine(VendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат для продажи.
- `player`: Игрок, который пытается повернуть автомат.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRotateVendingMachine(VendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnRotateVendingMachine работает!");
    return null;
}
```

## OnLootEntityEnd(BasePlayer,LootableCorpse)

### Summary


### Parameters
- `player`: Игрок, который закончил лутить.
- `lootableCorpse`: Лутаемая сущность.

### Returns
No return value.

### Example
```csharp
object OnLootEntityEnd(BasePlayer player, LootableCorpse lootableCorpse)
{
    Puts("OnLootEntityEnd работает!");
    return null;
}
```

## OnTrapDisarm(Landmine,BasePlayer)

### Summary


### Parameters
- `landmine`: Мина.
- `player`: Игрок, пытаясь снять мину.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTrapDisarm(Landmine landmine, BasePlayer player)
{
    Puts("OnTrapDisarm работает!");
    return null;
}
```

## OnTurretRotate(AutoTurret,BasePlayer)

### Summary


### Parameters
- `turret`: Турель.
- `player`: Игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretRotate(AutoTurret turret, BasePlayer player)
{
    Puts("OnTurretRotate работает!");
    return null;
}
```

## OnBookmarkControlEnded(ComputerStation,BasePlayer,IRemoteControllable)

### Summary


### Parameters
- `computerStation`: Компьютерная станция.
- `player`: Игрок.
- `remoteControllable`: Объект для удаленного управления.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBookmarkControlEnded(ComputerStation computerStation, BasePlayer player, IRemoteControllable remoteControllable)
{
    Puts("OnBookmarkControlEnded работает!");
}
```

## CanUseGesture(BasePlayer,GestureConfig)

### Summary


### Parameters
- `player`: Игрок, который пытается использовать гестуру.
- `gestureConfig`: Конфигурация гестуры.

### Returns
Возвращает true, если игрок может использовать гестуру, и false в противном случае.

### Example
```csharp
bool CanUseGesture(BasePlayer player, GestureConfig gestureConfig)
{
    Puts("CanUseGesture работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnClientDisconnect(Network.Connection,string)

### Summary


### Parameters
- `connection`: Объект Network.Connection, представляющий соединение клиента.
- `reason`: Причина отключения клиента.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnClientDisconnect(Network.Connection connection, string reason)
{
    Puts($"Клиент {connection} отключился: {reason}");
}
```

## OnEntityMarkHostile(BaseCombatEntity,float)

### Summary


### Parameters
- `entity`: Помеченная сущность.
- `duration`: Время, на которое сущность будет помечена.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEntityMarkHostile(BaseCombatEntity entity, float duration)
{
    Puts($"Сущность {entity} помечена как враждебная на {duration} секунд");
}

```

## OnSprayRemove(SprayCanSpray,BasePlayer)

### Summary


### Parameters
- `spray`: Аэрозоль с спреем.
- `player`: Игрок, удаляющий спрей.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSprayRemove(SprayCanSpray spray, BasePlayer player)
{
    Puts("OnSprayRemove работает!");
    return null;
}
```

## OnServerRestartInterrupt()

### Summary


### Parameters
No parameters.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnServerRestartInterrupt()
{
    Puts("OnServerRestartInterrupt работает!");
    return null;
}
```

## OnPlayerRevive(BasePlayer,BasePlayer)

### Summary


### Parameters
- `reviver`: Игрок, который восстанавливает здоровье.
- `playerToRevive`: Игрок, которого нужно восстановить.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerRevive(BasePlayer reviver, BasePlayer playerToRevive)
{
    Puts("OnPlayerRevive работает!");
    return null;
}
```

## OnNpcRadioChatter(ScientistNPC)

### Summary


### Parameters
- `npc`: НПС, который произносит радиочат.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcRadioChatter(ScientistNPC npc)
{
    Puts("OnNpcRadioChatter работает!");
    return null;
}
```

## OnTechTreeNodeUnlocked(Workbench,TechTreeData.NodeInstance,BasePlayer)

### Summary


### Parameters
- `workbench`: Рабочая столы.
- `nodeInstance`: Объект узла.
- `player`: Игрок, который разблокировал узел.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTechTreeNodeUnlocked(Workbench workbench, TechTreeData.NodeInstance nodeInstance, BasePlayer player)
{
    Puts($"Узел '{nodeInstance.groupName}' разблокирован игроком {player.UserIDString}.");
}

```

## OnAmmoUnload(BaseProjectile,Item,BasePlayer)

### Summary


### Parameters
- `projectile`: Проектиль, из которого выгружаются патроны.
- `item`: Изделие, в котором находится проектиль.
- `player`: Игрок, который выполняет действие.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnAmmoUnload(BaseProjectile projectile, Item item, BasePlayer player)
{
    Puts("OnAmmoUnload работает!");
    return null;
}
```

## OnPlayerRecovered(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, который восстановился.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerRecovered(BasePlayer player)
{
    Puts("OnPlayerRecovered работает!");
}
```

## OnLiquidWeaponFired(LiquidWeapon,BasePlayer)

### Summary


### Parameters
- `liquidWeapon`: Объект жидкостного оружия.
- `player`: Игрок, который произвел выстрел.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLiquidWeaponFired(LiquidWeapon liquidWeapon, BasePlayer player)
{
    Puts("OnLiquidWeaponFired работает!");
    return null;
}
```

## OnNetworkGroupEntered(BaseNetworkable,Network.Visibility.Group)

### Summary


### Parameters
- `group`: Группа, в которую вошли.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNetworkGroupEntered(BaseNetworkable group, Network.Visibility.Group visibility)
{
    Puts("OnNetworkGroupEntered работает!");
    return null;
}
```

## CanStackItem(Item,Item)

### Summary


### Parameters
- `item`: Предмет для проверки.

### Returns
Возвращает <c>true</c>, если предмет можно стекаивать, и <c>false</c> в противном случае.

### Example
```csharp
bool CanStackItem(Item item)
{
    Puts("CanStackItem работает!");
    return true;
}
```

## OnCorpsePopulate(GingerbreadNPC,NPCPlayerCorpse)

### Summary


### Parameters
- `npc`: Объект NPC.
- `corpse`: Тело игрока.

### Returns
Возвращает тело игрока или null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnCorpsePopulate(GingerbreadNPC npc, NPCPlayerCorpse corpse)
{
    // Минимальный код для демонстрации функциональности
    Puts("OnCorpsePopulate работает!");
    
    return null;
}
```

## OnDieselEngineToggled(DieselEngine)

### Summary


### Parameters
- `engine`: Дизельный двигатель.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnDieselEngineToggled(DieselEngine engine)
{
    Puts("OnDieselEngineToggled работает!");
    return null;
}
```

## OnPhoneDial(PhoneController,PhoneController,BasePlayer)

### Summary


### Parameters
- `caller`: Игрок, который набирает номер.
- `callee`: Телефон, на который набирают.
- `player`: Игрок, который набирает номер.

### Returns
Возвращает true, если вызов телефона был успешным, и false в противном случае.

### Example
```csharp
bool OnPhoneDial(PhoneController caller, PhoneController callee, BasePlayer player)
{
    Puts("OnPhoneDial работает!");
    // Здесь можно добавить дополнительную логическую логику или обработку
    return true;
}
```

## OnLootEntityEnd(BasePlayer,DroppedItemContainer)

### Summary


### Parameters
- `player`: Игрок, который закончил лутить.
- `lootedItems`: Контейнер с предметами, которые были вынуты из сущности.

### Returns
No return value.

### Example
```csharp
object OnLootEntityEnd(BasePlayer player, DroppedItemContainer lootedItems)
{
    Puts("OnLootEntityEnd вызван!");
    // Здесь можно добавить код для обработки окончания лута
    return null;
}
```

## OnInventoryItemsTake(PlayerInventory,System.Collections.Generic.List<Item>,int,int)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `items`: Список предметов, которые необходимо взять.
- `itemid`: ID предмета.
- `amount`: Количество предметов, которое необходимо взять.

### Returns
Возвращает количество взятых предметов или 0, если поведение по умолчанию не переопределено.

### Example
```csharp
int OnInventoryItemsTake(PlayerInventory inventory, List<Item> items, int itemid, int amount)
{
    Puts("OnInventoryItemsTake вызван!");
    // Здесь можно добавить дополнительную логическую логику или модифицировать поведение по умолчанию
    return 0;
}
```

## OnCargoShipHarborApproach(CargoShip,CargoNotifier)

### Summary


### Parameters
- `cargoShip`: Корабль.
- `notifier`: Уведомитель.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCargoShipHarborApproach(CargoShip cargoShip, CargoNotifier notifier)
{
    Puts("OnCargoShipHarborApproach работает!");
    return null;
}
```

## CanCombineDroppedItem(DroppedItem,DroppedItem)

### Summary


### Parameters
- `item1`: Первый предмет.
- `item2`: Второй предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void CanCombineDroppedItem(DroppedItem item1, DroppedItem item2)
{
    Puts("CanCombineDroppedItem работает!");
}
```

## OnDefaultItemsReceived(PlayerInventory)

### Summary
Документация для метода `OnDefaultItemsReceived(PlayerInventory)`:

### Parameters
- `playerInventory`: Инвентарь игрока.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnDefaultItemsReceived(PlayerInventory)`:

```rust
void OnDefaultItemsReceived(PlayerInventory playerInventory)
{
    // Минимальный код для демонстрации функциональности
}
```

В этом методе нет оператора `return`, поэтому он не возвращает никаких значений.
```

## OnTurretModeToggle(AutoTurret)

### Summary


### Parameters
- `turret`: Турет, режим которого был изменен.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTurretModeToggle(AutoTurret turret)
{
    Puts("Режим турета изменен!");
}
```

## OnEntityLeave(TriggerComfort,BaseEntity)

### Summary


### Parameters
- `comfort`: Триггер комфорта.
- `entity`: Покинувшая сущность.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityLeave(TriggerComfort comfort, BaseEntity entity)
{
    Puts("OnEntityLeave работает!");
    return null;
}
```

## CanBeHomingTargeted(PatrolHelicopter)

### Summary


### Parameters
- `helicopter`: Патрульный вертолет.

### Returns
Возвращает true, если патрульный вертолет может быть целью, и false в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(PatrolHelicopter helicopter)
{
    Puts("CanBeHomingTargeted работает!");
    return true;
}
```

## OnBradleyApcPatrol(BradleyAPC)

### Summary


### Parameters
- `apc`: Брэдли APC.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBradleyApcPatrol(BradleyAPC apc)
{
    Puts("OnBradleyApcPatrol работает!");
    return null;
}
```

## OnAdventGiftAwarded(AdventCalendar,BasePlayer)

### Summary


### Parameters
- `calendar`: Календарь advent.
- `player`: Игрок, которому был выдан подарок.

### Returns
No return value.

### Example
```csharp
void OnAdventGiftAwarded(AdventCalendar calendar, BasePlayer player)
{
    Puts("Подарок игроку!");
}
```

## OnPlayerSleepEnded(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, который закончил сон.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerSleepEnded(BasePlayer player)
{
    Puts("OnPlayerSleepEnded работает!");
}
```

## OnAmmoSwitch(BaseProjectile,BasePlayer,ItemDefinition)

### Summary


### Parameters
- `projectile`: Проектиль, который изменяет патрон.
- `player`: Игрок, который меняет патрон.
- `itemDefinition`: Определение предмета, который будет использован в качестве патрона.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnAmmoSwitch(BaseProjectile projectile, BasePlayer player, ItemDefinition itemDefinition)
{
    Puts("OnAmmoSwitch работает!");
}
```

## OnInterferenceOthersUpdate(AutoTurret)

### Summary


### Parameters
- `autoTurret`: Автоматическая турель.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnInterferenceOthersUpdate(AutoTurret autoTurret)
{
    Puts("OnInterferenceOthersUpdate работает!");
    return null;
}
```

## OnEntityDeath(ResourceEntity,HitInfo)

### Summary


### Parameters
- `entity`: Сущность, которая умерла.
- `hitInfo`: Информация о выстреле.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityDeath(ResourceEntity entity, HitInfo hitInfo)
{
    Puts("OnEntityDeath работает!");
    return null;
}
```

## OnFireworkExhausted(BaseFirework)

### Summary


### Parameters
- `firework`: Огнестройка, которая израсходовала все свои заряды.

### Returns
No return value.

### Example
```csharp
void OnFireworkExhausted(BaseFirework firework)
{
    Puts("OnFireworkExhausted вызван!");
}
```

## OnVehicleLockRequest(ModularCarGarage,BasePlayer,string)

### Summary


### Parameters
- `garage`: Модульный гараж.
- `player`: Игрок, запрашивающий установку замка.
- `lockType`: Тип замка.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVehicleLockRequest(ModularCarGarage garage, BasePlayer player, string lockType)
{
    // Минимальный код для демонстрации функциональности
    Puts($"OnVehicleLockRequest вызван! {lockType}");
    
    // Если ReturnType - object, возвращаемое значение не изменяется
    return null;
}
```

## OnServerInformationUpdated()

### Summary
Документация для OnServerInformationUpdated()

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для OnServerInformationUpdated()

**Описание:**

Метод OnServerInformationUpdated() вызывается после обновления информации о сервере в методе UpdateServerInformation(). Этот метод используется для уведомления других компонентов или модулей о том, что информация о сервере была обновлена.

**Параметры:**

Нет параметров.

**Возвращаемое значение:**

void (ничего не возвращает).

**Пример использования:**

```csharp
private void UpdateServerInformation()
{
    // ...
    Interface.CallHook("OnServerInformationUpdated");
}
```

**Связанные методы и переменные:**

*   `UpdateServerInformation()`: Метод, который обновляет информацию о сервере.
*   `SteamServer`: Класс, который хранит информацию о сервере.
*   `Interface.CallHook()`: Метод, который вызывает хук (метод-обработчик) с заданным именем.

**Примечания:**

Этот метод используется для уведомления других компонентов или модулей о том, что информация о сервере была обновлена. Это позволяет им обновить свою информацию в соответствии с новыми данными о сервере.
```

## OnQuarryGather(MiningQuarry,Item)

### Summary


### Parameters
- `quarry`: Шахта, из которой был собран ресурс.
- `item`: Собранный ресурс.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnQuarryGather(MiningQuarry quarry, Item item)
{
    Puts("OnQuarryGather работает!");
    return null;
}
```

## OnVehicleModuleSelect(Item,ModularCarGarage,BasePlayer)

### Summary


### Parameters
- `item`: Транспортное средство.
- `garage`: Модульная гаражная площадка.
- `player`: Игрок, выбравший модуль.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVehicleModuleSelect(Item item, ModularCarGarage garage, BasePlayer player)
{
    Puts("OnVehicleModuleSelect работает!");
    return null;
}
```

## OnRackedWeaponTaken(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Взятый предмет.
- `player`: Игрок, взявший предмет.
- `rack`: Ячейка, из которой был взят предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponTaken(Item item, BasePlayer player, WeaponRack rack)
{
    Puts($"Оружие {item.info.itemid} взято игроком {player.UserIDString}");
}

```

## CanAffordUpgrade(BasePlayer,BuildingBlock,BuildingGrade.Enum,ulong)

### Summary


### Parameters
- `player`: Игрок, пытающийся обновить блок.
- `blockDefinition`: Определение блока.
- `grade`: Навык обновления.
- `skin`: Скин блока.

### Returns
Возвращает true, если игрок может обновить блок, и false в противном случае.

### Example
```csharp
object CanAffordUpgrade(BasePlayer player, BuildingBlock blockDefinition, BuildingGrade.Enum grade, ulong skin)
{
    Puts("CanAffordUpgrade работает!");
    // Если возвращаемое значение не равно null, то оно является bool
    return true;
}
```

## CanLootEntity(BasePlayer,ContainerIOEntity)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `entity`: Контейнер с лутом.

### Returns
Возвращает true, если игрок может открыть лут, и false в противном случае.

### Example
```csharp
bool CanLootEntity(BasePlayer player, ContainerIOEntity entity)
{
    Puts("CanLootEntity работает!");
    return true;
}
```

## OnEntityFromOwnerCheck(BaseEntity,BasePlayer,uint,string)

### Summary


### Parameters
- `entity`: Сущность.
- `owner`: Владелец сущности.
- `id`: Идентификатор владельца.
- `debugName`: Название для отладки.

### Returns
Возвращает true, если сущность принадлежит игроку, и false в противном случае.

### Example
```csharp
object OnEntityFromOwnerCheck(BaseEntity entity, BasePlayer owner, uint id, string debugName)
{
    Puts("OnEntityFromOwnerCheck вызван!");
    
    // Здесь можно добавить дополнительную логику для проверки принадлежности сущности игроку
    
    return true; // Возвращаем значение по умолчанию
}
```

## OnCupboardAuthorize(BuildingPrivlidge,BasePlayer)

### Summary


### Parameters
- `privilege`: Шкаф.
- `player`: Авторизируемый игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCupboardAuthorize(BuildingPrivlidge privilege, BasePlayer player)
{
    Puts("OnCupboardAuthorize работает!");
}

В этом методе нет оператора return, поскольку тип возвращаемого значения void.
```

## OnEntityMarkHostile(BasePlayer,float)

### Summary


### Parameters
- `player`: Игрок, который вызывает хук.
- `duration`: Время, на которое сущность будет помечена как враждебная.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEntityMarkHostile(BasePlayer player, float duration)
{
    Puts($"Сущность '{player}' помечена как враждебная на {duration} секунд");
}
```

## OnMagazineReload(BaseProjectile,IAmmoContainer,BasePlayer)

### Summary


### Parameters
- `projectile`: Производимый снаряд.
- `ammoContainer`: Контейнер с патронами.
- `player`: Игрок, который перезаряжаает оружие.

### Returns
Возвращает true, если перезарядка прошла успешно, и false в противном случае.

### Example
```csharp
bool OnMagazineReload(BaseProjectile projectile, IAmmoContainer ammoContainer, BasePlayer player)
{
    Puts("OnMagazineReload вызван!");
    return true;
}
```

## OnSendModelState(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, чей статус модели должен быть отправлен.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSendModelState(BasePlayer player)
{
    Puts("OnSendModelState работает!");
    return null;
}
```

## OnFireworkDesignChange(PatternFirework,ProtoBuf.PatternFirework.Design,BasePlayer)

### Summary


### Parameters
- `design`: Новый дизайн фейерверка.
- `player`: Игрок, который изменил дизайн.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFireworkDesignChange(ProtoBuf.PatternFirework design, ProtoBuf.PatternFirework.Design protoBufPatternFireworkDesign, BasePlayer player)
{
    Puts("OnFireworkDesignChange работает!");
    return null;
}
```

## CanVendingAcceptItem(VendingMachine,Item,int)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `item`: Предмет для продажи.
- `targetSlot`: Номер слота, на который будет помещен предмет.

### Returns
Возвращает true, если предмет может быть добавлен в автомат, и false в противном случае.

### Example
```csharp
bool CanVendingAcceptItem(VendingMachine vendingMachine, Item item, int targetSlot)
{
    Puts("CanVendingAcceptItem работает!");
    // Если возвращаемое значение не равно null, то оно является bool
    return true; // или другое значение в зависимости от функциональности метода
}
```

## OnItemAddedToContainer(ItemContainer,Item)

### Summary


### Parameters
- `container`: Контейнер, в который был добавлен предмет.
- `item`: Добавленный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemAddedToContainer(ItemContainer container, Item item)
{
    Puts($"Предмет {item.Name} добавлен в контейнер {container.Name}");
}
```

## OnFeedbackReported(BasePlayer,string,string,Facepunch.Models.ReportType)

### Summary


### Parameters
- `player`: Игрок, который подал отчет.
- `subject`: Тема отчета.
- `message`: Сообщение отчета.
- `type`: Тип отчета.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnFeedbackReported(BasePlayer player, string subject, string message, ReportType type)
{
    Puts($"Отчет подан игроком {player} с темой '{subject}' и сообщением '{message}'");
}
```

## OnQueueCycle(int)

### Summary


### Parameters
- `availableSlots`: Количество доступных слотов.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnQueueCycle(int availableSlots)
{
    Puts("OnQueueCycle работает!");
    return null;
}
```

## CanMoveItem(Item,PlayerInventory,ItemContainerId,int,int,ItemMoveModifier)

### Summary
This is a C# method that appears to be part of a game server's item management system. It handles the movement of items from one container to another, taking into account various rules and constraints.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of a game server's item management system. It handles the movement of items from one container to another, taking into account various rules and constraints.

Here's a breakdown of the method:

1. The first section checks if the `item` parameter is null. If it is, the player is notified that the item is invalid.
2. If the item is valid, the method checks for any hooks or custom logic that might prevent the item from being moved (e.g., "CanMoveItem" hook).
3. The method then checks if the entity owner of the item is the same as the player who initiated the move, and if they are restrained or surrendering.
4. If all these conditions are met, the method proceeds to find a suitable container for the item.
5. If the container is locked or blocked from accepting player items, the player is notified accordingly.
6. If the item can be moved to the container, the method updates the item's amount and parent container as necessary.

Some key points to note:

* The method uses various flags and modifiers (e.g., `ItemMoveModifier`) to customize the behavior of item movement.
* It relies on other methods and classes (e.g., `ItemManager`, `ServerUpdate`) to perform specific tasks, such as updating the game state or notifying players.
* The code includes some error handling and logging mechanisms to notify players and administrators in case something goes wrong.

Overall, this method appears to be a crucial part of the game's item management system, ensuring that items are moved correctly between containers while respecting various rules and constraints.
```

## OnBuildingMerge(ServerBuildingManager,BuildingManager.Building,BuildingManager.Building)

### Summary


### Parameters
- `serverBuildingManager`: Менеджер сервера.
- `building1`: Первое здание для слияния.
- `building2`: Второе здание для слияния.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBuildingMerge(ServerBuildingManager serverBuildingManager, Building building1, Building building2)
{
    Puts("OnBuildingMerge вызван!");
}
```

## CanLock(BasePlayer,CodeLock)

### Summary


### Parameters
- `player`: Игрок, пытающийся зафиксировать код.
- `lock`: Кодовый замок, который нужно зафиксировать.

### Returns
Возвращает false, если поведение по умолчанию не переопределено.

### Example
```csharp
bool CanLock(BasePlayer player, CodeLock lock)
{
    Puts("CanLock работает!");
    return true;
}
```

## OnCrateDropped(HackableLockedCrate)

### Summary


### Parameters
- `crate`: Сброшенный контейнер.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCrateDropped(HackableLockedCrate crate)
{
    Puts($"Контейнер {crate.Id} был сброшен!");
}
```

## OnConnectionDequeue(Network.Connection)

### Summary


### Parameters
- `connection`: Удаленное соединение.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnConnectionDequeue(Network.Connection connection)
{
    Puts("OnConnectionDequeue работает!");
    return null;
}
```

## OnSendCommand(Network.Connection,string,object[])

### Summary


### Parameters
- `connection`: Соединение с клиентом.
- `command`: Команда для отправки.
- `args`: Аргументы команды.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSendCommand(Network.Connection connection, string command, object[] args)
{
    Puts($"Команда '{command}' будет отправлена клиенту {connection}");
    return null;
}
```

## OnLootNetworkUpdate(PlayerLoot)

### Summary


### Parameters
- `loot`: Объект PlayerLoot, содержащий информацию о луте.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootNetworkUpdate(PlayerLoot loot)
{
    Puts("OnLootNetworkUpdate работает!");
    return null;
}
```

## CanUnlockTechTreeNode(BasePlayer,TechTreeData.NodeInstance,TechTreeData)

### Summary


### Parameters
- `player`: Игрок, пытающийся разблокировать узел.
- `node`: Узел в технологическом дереве.
- `techTreeData`: Данные технологического дерева.

### Returns
Возвращает true, если игрок может разблокировать узел, и false в противном случае.

### Example
```csharp
bool CanUnlockTechTreeNode(BasePlayer player, TechTreeData.NodeInstance node, TechTreeData techTreeData)
{
    Puts("CanUnlockTechTreeNode работает!");
    // Если ReturnType - bool, верните значение
    return true; // Или другое значение в зависимости от функциональности метода
}
```

## CanBeTargeted(BaseCombatEntity,AutoTurret)

### Summary


### Parameters
- `entity`: Сущность, которую необходимо проверить.
- `turret`: Таргет, который проверяет.

### Returns
Возвращает true, если сущность может быть целью, и false в противном случае.

### Example
```csharp
bool CanBeTargeted(BaseCombatEntity entity, AutoTurret turret)
{
    Puts("CanBeTargeted работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnCollectiblePickup(CollectibleEntity,BasePlayer,bool)

### Summary


### Parameters
- `entity`: Коллекционный предмет.
- `player`: Игрок, который снимает предмет.
- `eat`: Флаг, указывающий, нужно ли съесть предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCollectiblePickup(CollectibleEntity entity, BasePlayer player, bool eat)
{
    Puts("OnCollectiblePickup работает!");
    return null;
}
```

## OnBoomboxStationUpdate(BoomBox,string,BasePlayer)

### Summary


### Parameters
- `boomBox`: Объект Boombox.
- `stationName`: Название радиостанции.
- `player`: Игрок, который обновил радиостанцию.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBoomboxStationUpdate(BoomBox boomBox, string stationName, BasePlayer player)
{
    Puts("OnBoomboxStationUpdate работает!");
    return null;
}
```

## OnDispenserBonusReceived(ResourceDispenser,BasePlayer,Item)

### Summary


### Parameters
- `dispenser`: Ресурсный диспенсер.
- `player`: Игрок, получивший бонус.
- `item`: Полученный бонус.

### Returns
Возвращает объект типа Item, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDispenserBonusReceived(ResourceDispenser dispenser, BasePlayer player, Item item)
{
    Puts("OnDispenserBonusReceived работает!");
    return null;
}
```

## IOnBasePlayerAttacked(BasePlayer,HitInfo)

### Summary
Документация для IOnBasePlayerAttacked(BasePlayer, HitInfo)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для IOnBasePlayerAttacked(BasePlayer, HitInfo)

**Описание**

Этот хук вызывается при атаке игрока на другого игрока. Он позволяет модификаторам изменить поведение игрока в момент атаки.

**Параметры**

* `BasePlayer`: Игрок, который был атакован.
* `HitInfo`: Информация о хите, включая тип повреждения и точку удара.

**Возвращаемые значения**

Нет возвращаемых значений. Если модификатор не изменит поведение игрока, он должен вернуть null.

**Пример использования**

```csharp
public class MyMod : MonoBehaviour
{
    public void OnEnable()
    {
        Interface.CallHook("IOnBasePlayerAttacked", this);
    }

    public void IOnBasePlayerAttacked(BasePlayer player, HitInfo hit)
    {
        // Измените поведение игрока в момент атаки
        if (player.health > 50 && hit.damageTypes.IsMeleeType())
        {
            player.health -= 10;
        }
    }
}
```

**Примечания**

* Этот хук вызывается только на сервере.
* Если модификатор не изменит поведение игрока, он должен вернуть null.
* Модификаторы могут использовать эту функцию для изменения поведения игрока в момент атаки.
```

## OnMlrsFire(MLRS,BasePlayer)

### Summary


### Parameters
- `mlrs`: Объект MLRS.
- `player`: Игрок, который получает урон.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMlrsFire(MLRS mlrs, BasePlayer player)
{
    Puts("OnMlrsFire работает!");
}

В этом случае тип возвращаемого значения равен void, поскольку метод не возвращает никаких значений.
```

## OnFlameThrowerBurn(FlameThrower,BaseEntity)

### Summary
Документация для метода `OnFlameThrowerBurn(FlameThrower, BaseEntity)`:

### Parameters
- `flameThrower`: Огнемёт.
- `baseEntity`: Объект, который был сожжен.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnFlameThrowerBurn(FlameThrower, BaseEntity)`:

```rust
void OnFlameThrowerBurn(FlameThrower flameThrower, BaseEntity baseEntity)
{
    // Минимальный код для демонстрации функциональности
}
```

Тип возвращаемого значения: `void` (метод не возвращает никаких значений).

Использование метода:

Метод вызывается в методе `FlameTick()` при сжигании объекта огнеметом. В этом случае метод вызывается после того, как был создан новый объект типа `FireBall`, который представляет собой огненную куля.

Примечания:

* Метод не имеет никаких параметров, кроме двух обязательных: `flameThrower` и `baseEntity`.
* Метод не возвращает никаких значений.
* Метод вызывается только один раз при сжигании объекта огнеметом.
```

## OnPlayerPingsSend(BasePlayer,ProtoBuf.MapNoteList)

### Summary


### Parameters
- `player`: Игрок, которому отправляются пинги.
- `mapNotes`: Список заметок на карте.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerPingsSend(BasePlayer player, ProtoBuf.MapNoteList mapNotes)
{
    Puts("OnPlayerPingsSend работает!");
    return null;
}
```

## OnTimedExplosiveExplode(TimedExplosive,UnityEngine.Vector3)

### Summary
This is a C# code snippet that appears to be part of a game or simulation, likely using the Unity game engine. It's an explosion effect script that handles various aspects of an explosion, including:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game or simulation, likely using the Unity game engine. It's an explosion effect script that handles various aspects of an explosion, including:

1. **Visual effects**: The script runs different visual effects (e.g., underwater explosion, surface explosion) based on the depth and position of the explosion.
2. **Damage calculation**: It calculates damage to entities within a certain radius using the `RadiusDamage` method from the `DamageUtil` class.
3. **Entity interaction**: If an entity is damaged, it interacts with that entity by calling its `Hurt` or `OnAttacked` methods.

Here are some key points and observations:

* The script uses various Unity-specific classes and functions (e.g., `Effect`, `Pool`, `Vis`, `GameObjectEx`).
* It relies on external scripts and data (e.g., `DamageUtil`, `SeismicSensor`, `BlindAnyAI`) to perform certain tasks.
* The explosion effect is customizable through the use of various effects (e.g., `underwaterExplosionEffect`, `watersurfaceExplosionEffect`) that can be swapped out or modified.
* The script uses a flag-based system (`Flags.Broken`) to track whether an entity has been broken or destroyed.

Some potential improvements or suggestions:

* Consider adding more comments or documentation to explain the purpose and behavior of each section of code.
* Use more descriptive variable names (e.g., `explosionFxPos` could be renamed to something like `explosionPosition`).
* If possible, consider using a more robust and flexible damage calculation system that can handle different types of damage and entities.

Overall, this script appears to be well-structured and efficient in its execution. However, with some additional comments and documentation, it would be even easier for others to understand and maintain.
```

## CanLootEntity(BasePlayer,LootableCorpse)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `entity`: Сущность, из которой будет открыт лут.

### Returns
Возвращает true, если поведение по умолчанию не переопределено, и false в противном случае.

### Example
```csharp
bool CanLootEntity(BasePlayer player, LootableCorpse entity)
{
    Puts("CanLootEntity работает!");
    return true;
}
```

## OnTeamUpdate(ulong,ulong,BasePlayer)

### Summary


### Parameters
- `oldTeam`: Старая команда игрока.
- `newTeam`: Новая команда игрока.
- `player`: Игрок, чья команда была изменена.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamUpdate(ulong oldTeam, ulong newTeam, BasePlayer player)
{
    Puts($"Команда игрока {player.UserID} изменилась с {oldTeam} на {newTeam}");
    return null;
}
```

## IOnPlayerConnected(BasePlayer)

### Summary
Документация для IOnPlayerConnected(BasePlayer)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для IOnPlayerConnected(BasePlayer)

**Описание**

Хук `IOnPlayerConnected` вызывается при подключении игрока к серверу. Этот хук позволяет модифицировать поведение игрока при его подключении.

**Параметры**

* `BasePlayer`: Объект игрока, который подключился к серверу.

**Пример использования**

```csharp
public void OnPlayerConnected(BasePlayer player)
{
    // Код для модификации поведения игрока при его подключении
}
```

**Детализированная структура метода**

* `void OnPlayerConnected(BasePlayer player)`: Метод, который вызывается при подключении игрока.
* `BasePlayer player`: Объект игрока, который подключился к серверу.

**Примечания**

* Этот хук вызывается в методе `PlayerInit` после того, как игрок был инициализирован.
* В этом хуке можно модифицировать поведение игрока при его подключении, например, изменить его статус или отправить сообщение другим игрокам.
```

## OnMaxStackable(Item)

### Summary


### Parameters
- `item`: Предмет, для которого определяется максимальное количество.

### Returns
Возвращает максимальное количество предметов, которые могут быть собраны в стэк. Если поведение по умолчанию переопределено, возвращается ненулевое значение.

### Example
```csharp
object OnMaxStackable(Item item)
{
    Puts("OnMaxStackable работает!");
    // Здесь можно добавить дополнительный код для определения максимального количества
    return null;
}
```

## OnFireworkDesignChanged(PatternFirework,ProtoBuf.PatternFirework.Design,BasePlayer)

### Summary


### Parameters
- `design`: Новый дизайн фейерверка.
- `player`: Игрок, который изменил дизайн.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFireworkDesignChanged(ProtoBuf.PatternFirework design, BasePlayer player)
{
    Puts("OnFireworkDesignChanged работает!");
    return null;
}
```

## OnVendingShopOpen(InvisibleVendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `player`: Игрок, открывающий автомат.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnVendingShopOpen(InvisibleVendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnVendingShopOpen работает!");
}
```

## OnDemoRecordingStarted(string,BasePlayer)

### Summary


### Parameters
- `recordingPath`: Путь к файлу записи.
- `player`: Игрок, который начал запись.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDemoRecordingStarted(string recordingPath, BasePlayer player)
{
    Puts($"Демонстрация '{recordingPath}' начата игроком {player.UserIDString}");
}
```

## OnHealingItemUse(MedicalTool,BasePlayer)

### Summary


### Parameters
- `tool`: Предмет, используемый для лечения.
- `player`: Игрок, получающий лечение.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHealingItemUse(MedicalTool tool, BasePlayer player)
{
    Puts("OnHealingItemUse работает!");
    return null;
}
```

## OnSleepingBagDestroy(SleepingBag,ulong)

### Summary


### Parameters
- `sleepingBag`: Уничтожаемая спальнная сумка.
- `userID`: ID пользователя, который владеет спальнной сумкой.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSleepingBagDestroy(SleepingBag sleepingBag, ulong userID)
{
    Puts("OnSleepingBagDestroy работает!");
    return null;
}
```

## OnBoatPathGenerate()

### Summary
**OnBoatPathGenerate() Hook Documentation**

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
**OnBoatPathGenerate() Hook Documentation**

**Purpose:** This hook is called to generate a boat path for the `GenerateOceanPatrolPath()` method.

**Parameters:**

* None

**Return Value:**
The hook returns a List of Vector3 objects, which represents the generated boat path.

**Usage:**

To use this hook, you need to call it from within the `GenerateOceanPatrolPath()` method. The hook will be executed and return a List of Vector3 objects, which can then be used to generate the ocean patrol path.

**Example Code:**
```csharp
public static List<Vector3> GenerateOceanPatrolPath(float minDistanceFromShore = 50f, float minWaterDepth = 8f)
{
    object obj = Interface.CallHook("OnBoatPathGenerate");
    if (obj is List<Vector3>)
    {
        return (List<Vector3>)obj;
    }
    // Rest of the method implementation...
}
```
**Notes:**

* The hook does not take any parameters.
* The hook returns a List of Vector3 objects, which represents the generated boat path.
* The `GenerateOceanPatrolPath()` method uses this hook to generate the ocean patrol path.

**Minimum Code for Demonstration:**
```csharp
public static List<Vector3> OnBoatPathGenerate()
{
    return new List<Vector3>();
}
```
This code demonstrates a basic implementation of the `OnBoatPathGenerate()` hook, which returns an empty List of Vector3 objects.
```

## CanUseWires(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, пытающийся использовать провода.

### Returns
Возвращает true, если игрок может использовать провода, и false в противном случае.

### Example
```csharp
bool CanUseWires(BasePlayer player)
{
    Puts("CanUseWires работает!");
    // Если возвращаемое значение не равно null, то возвращаем его
    return (bool)Interface.CallHook("CanUseWires", player);
}
```

## OnRackedWeaponUnload(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Выгружаемое оружие.
- `player`: Игрок, который выполняет действие.
- `weaponRack`: Ячейка для оружия.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponUnload(Item item, BasePlayer player, WeaponRack weaponRack)
{
    Puts("OnRackedWeaponUnload работает!");
}
```

## OnEntityEnter(TriggerBase,BaseEntity)

### Summary


### Parameters
- `trigger`: Триггер, в который вошел сущность.
- `entity`: Сущность, которая вошла в триггер.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityEnter(TriggerBase trigger, BaseEntity entity)
{
    Puts("OnEntityEnter работает!");
    return null;
}
```

## OnTurretAuthorize(AutoTurret,BasePlayer)

### Summary


### Parameters
- `turret`: Турет, который будет использоваться.
- `player`: Игрок, который авторизуется.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretAuthorize(AutoTurret turret, BasePlayer player)
{
    Puts("OnTurretAuthorize работает!");
    return null;
}
```

## OnEntityKill(BaseNetworkable)

### Summary


### Parameters
- `entity`: Убиваемая сущность.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityKill(BaseNetworkable entity)
{
    Puts("OnEntityKill вызван!");
    return null;
}
```

## OnClothingItemChanged(PlayerInventory,Item,bool)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `item`: Измененная одежда.
- `added`: Флаг, указывающий, добавлена ли новая одежда или удалена старая.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnClothingItemChanged(PlayerInventory inventory, Item item, bool added)
{
    Puts("OnClothingItemChanged работает!");
}
```

## CanCatchFish(BasePlayer,BaseFishingRod,Item)

### Summary
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

**Main Loop**

The code runs in a loop until the fish is caught or the process fails.

**Flag Management**

The code manages several flags, which are used to track the state of the fishing process. These flags include:

* `flag`: Whether the player has pulled on the line.
* `flag2`: Whether the player has pulled on the line in a specific direction (left or right).
* `flag3`: Whether the player is pulling back on the line.

The code updates these flags based on user input and the current state of the fishing process.

**Fish State Management**

The code manages the state of the fish, which can be one of several states:

* `FishState.PullingBack`
* `FishState.PullingLeft`
* `FishState.PullingRight`

The code updates the fish state based on user input and the current state of the fishing process.

**Strain Timer**

The code has a strain timer that increments based on the player's actions. When the strain timer reaches 7 seconds, the fishing process fails.

**Client RPCs**

The code sends client-side RPCs to update the client's view of the fishing process. These RPCs include:

* `RpcTarget.NetworkGroup("Client_UpdateFishState")`: Updates the client's fish state.
* `RpcTarget.NetworkGroup("Client_OnCaughtFish")`: Notifies the client that a fish has been caught.

**Achievement Checking**

The code checks if the player has achieved a specific achievement related to catching all types of fish.

Overall, this code snippet appears to be responsible for managing the fishing mini-game in Rust, including updating flags and fish states, checking achievements, and sending client-side RPCs.
```

## OnPhoneNameUpdate(PhoneController,string,BasePlayer)

### Summary


### Parameters
- `controller`: Контроллер телефона.
- `newName`: Новое имя телефона.
- `player`: Игрок, который обновляет имя телефона.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPhoneNameUpdate(PhoneController controller, string newName, BasePlayer player)
{
    Puts("OnPhoneNameUpdate работает!");
    return null;
}
```

## CanLootEntity(BasePlayer,DroppedItemContainer)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `entity`: Сущность, из которой открывается лут.

### Returns
Возвращает false, если поведение по умолчанию не переопределено.

### Example
```csharp
bool CanLootEntity(BasePlayer player, DroppedItemContainer entity)
{
    Puts("CanLootEntity работает!");
    return true;
}
```

## OnCargoShipHarborLeave(CargoShip)

### Summary


### Parameters
- `cargoShip`: Судно, покидающее порт.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCargoShipHarborLeave(CargoShip cargoShip)
{
    Puts("OnCargoShipHarborLeave работает!");
}
```

## OnXmasStockingFill(Stocking)

### Summary


### Parameters
- `stocking`: Рождественская сумка.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnXmasStockingFill(Stocking stocking)
{
    Puts("OnXmasStockingFill работает!");
    return null;
}
```

## CanNetworkTo(BaseNetworkable,BasePlayer)

### Summary


### Parameters
- `networkable`: Объект сети.
- `player`: Игрок, пытающийся подключиться.

### Returns
Возвращает true, если подключение разрешено, и false в противном случае.

### Example
```csharp
bool CanNetworkTo(BaseNetworkable networkable, BasePlayer player)
{
    Puts("CanNetworkTo работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnRecyclerToggle(Recycler,BasePlayer)

### Summary


### Parameters
- `recycler`: Объект рециклера.
- `player`: Игрок, который включил или выключил рециклер.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRecyclerToggle(Recycler recycler, BasePlayer player)
{
    Puts("OnRecyclerToggle работает!");
    return null;
}
```

## OnThreatLevelUpdate(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, для которого обновляется уровень угрозы.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnThreatLevelUpdate(BasePlayer player)
{
    Puts("OnThreatLevelUpdate работает!");
    return null;
}
```

## CanBeHomingTargeted(BaseHelicopter)

### Summary


### Parameters
- `helicopter`: Вертолет.

### Returns
Возвращает <c>true</c>, если вертолет может быть целью, и <c>false</c> в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(BaseHelicopter helicopter)
{
    Puts("CanBeHomingTargeted работает!");
    return true;
}
```

## CanEntityBeHostile(BaseCombatEntity)

### Summary


### Parameters
- `entity`: Сущность.

### Returns
Возвращает true, если сущность может быть враждебной, и false в противном случае.

### Example
```csharp
bool CanEntityBeHostile(BaseCombatEntity entity)
{
    Puts("CanEntityBeHostile работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnPlayerStudyBlueprint(BasePlayer,Item)

### Summary


### Parameters
- `player`: Игрок, изучающий.blueprint.
- `item`: Объект.blueprint.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerStudyBlueprint(BasePlayer player, Item item)
{
    Puts("OnPlayerStudyBlueprint работает!");
    return null;
}
```

## OnSensorDetect(HBHFSensor,BasePlayer)

### Summary


### Parameters
- `sensor`: Сенсор, который обнаружил игрока.
- `player`: Обнаруженный игрок.

### Returns
Возвращает true, если условие выполнено, и false в противном случае.

### Example
```csharp
bool OnSensorDetect(HBHFSensor sensor, BasePlayer player)
{
    Puts("OnSensorDetect работает!");
    // Здесь можно добавить дополнительную логическую логику или обработку
    return true;
}
```

## OnOvenCook(BaseOven,Item)

### Summary


### Parameters
- `oven`: Печь, в которой готовится предмет.
- `item`: Предмет, который готовится.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnOvenCook(BaseOven oven, Item item)
{
    Puts("OnOvenCook работает!");
    return null;
}
```

## OnVendingShopOpened(InvisibleVendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат для продажи товаров.
- `player`: Игрок, открывающий автомат.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnVendingShopOpened(InvisibleVendingMachine vendingMachine, BasePlayer player)
{
    Puts("Автомат для продажи товаров открыт!");
}
```

## OnPatrolHelicopterTakeDamage(PatrolHelicopter,HitInfo)

### Summary


### Parameters
- `helicopter`: Патрульный вертолет.
- `info`: Информация о ударе.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPatrolHelicopterTakeDamage(PatrolHelicopter helicopter, HitInfo info)
{
    Puts("OnPatrolHelicopterTakeDamage работает!");
    return null;
}
```

## CanHelicopterStrafe(PatrolHelicopterAI)

### Summary


### Parameters
- `ai`: Объект-вертолёт.

### Returns
Возвращает true, если стрельба возможна, и false в противном случае.

### Example
```csharp
bool CanHelicopterStrafe(PatrolHelicopterAI ai)
{
    Puts("CanHelicopterStrafe работает!");
    // Здесь можно добавить логику для проверки возможности стрельбы
    return true; // или другое значение в зависимости от функциональности
}
```

## OnWindmillUpdate(ElectricWindmill)

### Summary


### Parameters
- `windmill`: Объект ветряной мельницы.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnWindmillUpdate(ElectricWindmill windmill)
{
    Puts("OnWindmillUpdate работает!");
}

В этом методе нет оператора return, поэтому тип возвращаемого значения равен void.
```

## OnHelicopterDropCrate(CH47HelicopterAIController)

### Summary


### Parameters
- `helicopter`: Контроллер хеликоптера.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnHelicopterDropCrate(CH47HelicopterAIController helicopter)
{
    Puts("OnHelicopterDropCrate работает!");
}
```

## OnItemResearch(ResearchTable,Item,BasePlayer)

### Summary


### Parameters
- `researchTable`: Таблица исследований.
- `item`: Исследуемый предмет.
- `player`: Игрок, который проводит исследование.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemResearch(ResearchTable researchTable, Item item, BasePlayer player)
{
    Puts("OnItemResearch вызван!");
}
```

## OnCargoShipEgress(CargoShip)

### Summary


### Parameters
- `cargoShip`: Корабль, с которого происходит выгрузка.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCargoShipEgress(CargoShip cargoShip)
{
    Puts("OnCargoShipEgress работает!");
    return null;
}
```

## CanBeTargeted(BasePlayer,GunTrap)

### Summary


### Parameters
- `player`: Игрок.
- `trap`: Ловушка.

### Returns
Возвращает true, если игрок может быть целью, и false в противном случае.

### Example
```csharp
bool CanBeTargeted(BasePlayer player, GunTrap trap)
{
    Puts("CanBeTargeted работает!");
    // Здесь можно добавить дополнительную логику для определения, может ли игрок быть целью
    return true; // или другое значение в зависимости от функциональности
}
```

## CanSamSiteShoot(SamSite)

### Summary
Документация для метода `CanSamSiteShoot`:

### Parameters
- `samSite`: Система SAM.

### Returns
Возвращает true, если стрельба возможна, и false в противном случае.

### Example
```csharp
Документация для метода `CanSamSiteShoot`:

```rust
bool CanSamSiteShoot(SamSite samSite)
{
    // Минимальный код для демонстрации функциональности
    Puts("CanSamSiteShoot работает!");
    
    // Возвращаемое значение определяется на основе использования возвращаемого значения в контексте
    return true; // или другое значение в зависимости от функциональности метода
}
```

В этом случае тип возвращаемого значения определен как `bool`, поскольку в контексте используется оператор `== null` для проверки возвращаемого значения.
```

## OnDispenserGathered(ResourceDispenser,BasePlayer,Item)

### Summary


### Parameters
- `dispenser`: Диспенсер, из которого был собран ресурс.
- `player`: Игрок, который собрал ресурс.
- `item`: Собранный ресурс.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDispenserGathered(ResourceDispenser dispenser, BasePlayer player, Item item)
{
    Puts($"Ресурс {item.info.shortname} собран игроком {player.UserIDString} из диспенсера {dispenser.EntityID}");
}

```

## CanBypassQueue(Network.Connection)

### Summary


### Parameters
- `connection`: Соединение игрока.

### Returns
Возвращает true, если игрок может проскакивать очередь, и false в противном случае.

### Example
```csharp
object CanBypassQueue(Network.Connection connection)
{
    Puts("CanBypassQueue работает!");
    return null;
}
```

## OnNpcConversationRespond(NPCTalking,BasePlayer,ConversationData,ConversationData.ResponseNode)

### Summary


### Parameters
- `npc`: НПЦ, который отвечает.
- `player`: Игрок, с которым разговаривает НПЦ.
- `conversationData`: Данные разговора.
- `responseNode`: Нод ответа.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnNpcConversationRespond(NPCTalking npc, BasePlayer player, ConversationData conversationData, ConversationData.ResponseNode responseNode)
{
    Puts("OnNpcConversationRespond работает!");
    return null;
}
```

## OnCrateLaptopAttack(HackableLockedCrate,HitInfo)

### Summary


### Parameters
- `crate`: Защищенный ящик.
- `info`: Информация о хите.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCrateLaptopAttack(HackableLockedCrate crate, HitInfo info)
{
    Puts("OnCrateLaptopAttack работает!");
    return null;
}
```

## OnFindSpawnPoint(BasePlayer)

### Summary
Документация для метода `OnFindSpawnPoint(BasePlayer)`:

### Parameters
- `player`: Игрок, для которого необходимо найти точку спавна.

### Returns
Точка спавна игрока или null, если не удалось найти.

### Example
```csharp
Документация для метода `OnFindSpawnPoint(BasePlayer)`:

```rust
void OnFindSpawnPoint(BasePlayer player)
{
    // Код метода отсутствует, поскольку он вызывается из другого места и выполняет свою функцию
}
```

Примечание: Этот метод не имеет собственного кода, поскольку он вызывается из другого места и выполняет свою функцию. В документации указано, что этот метод вызывается при поиске точки спавна для игрока, но фактически он является частью более крупного метода `FindSpawnPoint(BasePlayer)`.
```

## OnEventTrigger(TriggeredEventPrefab)

### Summary


### Parameters
- `eventPrefab`: Предмет-экземпляр события.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEventTrigger(TriggeredEventPrefab eventPrefab)
{
    Puts("OnEventTrigger работает!");
}
```

## OnFuelConsume(BaseOven,Item,ItemModBurnable)

### Summary


### Parameters
- `oven`: Печь, в которой сожжено топливо.
- `fuel`: Топливо, сожженное в печи.
- `burnable`: Объект, который можно сжечь.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFuelConsume(BaseOven oven, Item fuel, ItemModBurnable burnable)
{
    Puts("OnFuelConsume работает!");
    return null;
}
```

## CanPickupEntity(BasePlayer,BaseCombatEntity)

### Summary


### Parameters
- `player`: Игрок, пытающийся поднять сущность.
- `entity`: Поднимаемая сущность.

### Returns
Возвращает true, если игрок может поднять сущность, и false в противном случае.

### Example
```csharp
bool CanPickupEntity(BasePlayer player, BaseCombatEntity entity)
{
    Puts("CanPickupEntity работает!");
    return true; // Игрок может поднять сущность
}
```

## OnBuyVendingItem(VendingMachine,BasePlayer,int,int)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `player`: Игрок, совершивший покупку.
- `itemIndex`: Индекс предмета.
- `quantity`: Количество предметов.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBuyVendingItem(VendingMachine vendingMachine, BasePlayer player, int itemIndex, int quantity)
{
    Puts("OnBuyVendingItem работает!");
    return null;
}
```

## OnTurretAssign(AutoTurret,ulong,BasePlayer)

### Summary


### Parameters
- `turret`: Туррет.
- `id`: Идентификатор игрока.
- `player`: Игрок, которому назначается туррет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretAssign(AutoTurret turret, ulong id, BasePlayer player)
{
    Puts("OnTurretAssign работает!");
    return null;
}
```

## CanCastFishingRod(BasePlayer,BaseFishingRod,Item,UnityEngine.Vector3)

### Summary


### Parameters
- `owner`: Владелец удочки.
- `fishingRod`: Удочка.
- `lure`: Наживка.
- `position`: Позиция бросания.

### Returns
True, если бросить удочку можно; False в противном случае.

### Example
```csharp
bool CanCastFishingRod(BasePlayer owner, BaseFishingRod fishingRod, Item lure, UnityEngine.Vector3 position)
{
    // Минимальный код для демонстрации функциональности
    return true;
}
```

## OnFindBurnable(BaseOven)

### Summary


### Parameters
- `oven`: Пекарь, который ищет сгораемый предмет.

### Returns
Возвращает сгораемый предмет, если он найден, или null, если не найден.

### Example
```csharp
Item OnFindBurnable(BaseOven oven)
{
    Puts("OnFindBurnable вызван!");
    // Если возвращаемое значение равно Item, вернуть его
    return null;
}
```

## OnVehicleModuleDeselected(ModularCarGarage,BasePlayer)

### Summary


### Parameters
- `garage`: Объект гаража.
- `player`: Игрок, который отменил выбор модуля.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnVehicleModuleDeselected(ModularCarGarage garage, BasePlayer player)
{
    Puts("OnVehicleModuleDeselected вызван!");
}
```

## OnMapMarkersCleared(BasePlayer)

### Summary


### Parameters
- `player`: Игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMapMarkersCleared(BasePlayer player)
{
    Puts("OnMapMarkersCleared работает!");
    return null;
}
```

## OnTeamCreated(BasePlayer,RelationshipManager.PlayerTeam)

### Summary


### Parameters
- `player`: Игрок, который создал команду.
- `team`: Созданная команда.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamCreated(BasePlayer player, RelationshipManager.PlayerTeam team)
{
    Puts("OnTeamCreated вызван!");
    return null;
}
```

## OnItemCraft(ItemCraftTask,BasePlayer,Item)

### Summary


### Parameters
- `task`: Задача по созданию предмета.
- `owner`: Владелец, который создает предмет.
- `item`: Предмет, который будет создан.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemCraft(ItemCraftTask task, BasePlayer owner, Item item)
{
    Puts($"Игрок {owner.UserIDString} начал создавать предмет {item.info.shortname}");
}
```

## OnTerrainInitialized()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void OnTerrainInitialized()
{
    Puts("Терранин инициализирован!");
}
```

## CanPurchaseItem(BasePlayer,Item,System.Action<BasePlayer, Item>,VendingMachine,ItemContainer)

### Summary
This is a C# method that appears to be part of a vending machine system in the game Rust. The method, `TryBuyFromVendingMachine`, attempts to purchase an item from a vending machine using a specified currency.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of a vending machine system in the game Rust. The method, `TryBuyFromVendingMachine`, attempts to purchase an item from a vending machine using a specified currency.

Here's a breakdown of what the method does:

1. It checks if the sell order ID is valid and within range.
2. It ensures that the buyer is close enough to the vending machine (within 4 units).
3. It calls a hook function `OnVendingTransaction` to allow for custom behavior or modifications.
4. If the hook function returns false, it immediately returns false.
5. It retrieves the sell order associated with the specified ID and creates a list of items to be sold.
6. It checks if there are enough items in stock to fulfill the purchase request.
7. It calculates the total price for the purchase based on the number of transactions and the item's price multiplier.
8. If there is not enough currency available, it returns false.
9. It takes the required amount of currency from the buyer's inventory.
10. It records sale analytics using `RecordSaleAnalytics`.
11. It gives the purchased item to the buyer or moves it to a target container if specified.
12. Finally, it updates an empty flag and returns true.

The method uses various hooks and callbacks to allow for custom behavior and modifications, which is typical in game development where modding is encouraged.

Here's a simplified version of the code with some comments added:

```csharp
public bool TryBuyFromVendingMachine(BasePlayer buyer, int sellOrderId, int numberOfTransactions, Container targetContainer = null)
{
    // Check if sell order ID is valid and within range
    if (sellOrderId < 0 || sellOrderId >= sellOrders.sellOrders.Count) return false;

    // Ensure buyer is close enough to vending machine
    if (targetContainer == null && Vector3.Distance(buyer.transform.position, base.transform.position) > 4f) return false;

    // Call hook function to allow for custom behavior or modifications
    object obj = Interface.CallHook("OnVendingTransaction", this, buyer, sellOrderId, numberOfTransactions, targetContainer);
    if (obj is bool && !(bool)obj) return false;

    // Retrieve sell order and create list of items to be sold
    ProtoBuf.VendingMachine.SellOrder sellOrder = sellOrders.sellOrders[sellOrderId];
    List<Item> obj2 = Facepunch.Pool.GetList<Item>();
    GetItemsToSell(sellOrder, obj2);

    // Check if there are enough items in stock to fulfill purchase request
    if (obj2 == null || obj2.Count == 0) return false;

    // Calculate total price for purchase based on number of transactions and item's price multiplier
    int num = sellOrder.itemToSellAmount * numberOfTransactions;
    int num2 = obj2.Sum((Item x) => x.amount);
    if (num > num2) return false;

    // Take required amount of currency from buyer's inventory
    List<Item> source = buyer.inventory.FindItemsByItemID(sellOrder.currencyID);
    if (sellOrder.currencyIsBP)
    {
        source = (from x in buyer.inventory.FindItemsByItemID(blueprintBaseDef.itemid)
            where x.blueprintTarget == sellOrder.currencyID
            select x).ToList();
    }
    source = (from x in source
        where !x.hasCondition || (x.conditionNormalized >= 0.5f && x.maxConditionNormalized > 0.5f)
        where x.GetItemVolume() <= maxCurrencyVolume
        select x).ToList();

    // Check if there is not enough currency available
    int num3 = source.Sum((Item x) => x.amount);
    int num4 = GetTotalPriceForOrder(sellOrder) * numberOfTransactions;
    if (num3 < num4) return false;

    // Record sale analytics using RecordSaleAnalytics
    transactionActive = true;
    int num5 = 0;
    foreach (Item item3 in source)
    {
        int num6 = Mathf.Min(num4 - num5, item3.amount);
        Item item = ((item3.amount > num6) ? item3.SplitItem(num6) : item3);
        TakeCurrencyItem(item);
        onCurrencyRemoved?.Invoke(buyer, item);
        num5 += num6;
        if (num5 >= num4) break;
    }

    // Give purchased item to buyer or move it to target container
    int num7 = 0;
    foreach (Item item4 in obj2)
    {
        int num8 = num - num7;
        Item item2 = ((item4.amount > num8) ? item4.SplitItem(num8) : item4);
        if (item2 == null) PutsError("Vending machine error, contact developers!");
        else
        {
            num7 += item2.amount;
            // Give purchased item to buyer or move it to target container
            if (targetContainer != null)
                targetContainer.Add(item2);
            else
                buyer.inventory.Add(item2);
        }
    }

    // Update empty flag and return true
    updateEmptyFlag();
    return true;
}
```
```

## CanDismountEntity(BasePlayer,BaseMountable)

### Summary
```rust

### Parameters
- `player`: Игрок.
- `entity`: Объект.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
```rust
void CanDismountEntity(BasePlayer player, BaseMountable entity)
{
    // Минимальный код для демонстрации функциональности
}
```

Примечание: В данном случае метод `CanDismountEntity` не имеет никакой логики и просто возвращает. Это потому что в исходном коде он используется только для проверки, может ли игрок снять со своего объекта или нет, а если да, то он просто возвращает `null`.
```

## OnSprinklerSplashed(Sprinkler)

### Summary


### Parameters
- `sprinkler`: Сущность sprinkler.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSprinklerSplashed(Sprinkler sprinkler)
{
    Puts("OnSprinklerSplashed работает!");
}
```

## OnBradleyApcInitialize(BradleyAPC)

### Summary


### Parameters
- `apc`: Bradley APC.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBradleyApcInitialize(BradleyAPC apc)
{
    Puts("OnBradleyApcInitialize работает!");
}
```

## CanDeployItem(BasePlayer,Deployer,NetworkableId)

### Summary


### Parameters
- `player`: Игрок, пытающийся разместить предмет.
- `deployer`: Объект, с помощью которого разместить предмет.
- `networkableId`: ID сущности, на которую будет разместен предмет.

### Returns
Возвращает true, если предмет может быть разместен, и false в противном случае.

### Example
```csharp
bool CanDeployItem(BasePlayer player, Deployer deployer, NetworkableId networkableId)
{
    Puts("CanDeployItem работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true;
}
```

## OnMapMarkerAdd(BasePlayer,ProtoBuf.MapNote)

### Summary


### Parameters
- `player`: Игрок, который добавил метку.
- `mapNote`: Информация о метке.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMapMarkerAdd(BasePlayer player, ProtoBuf.MapNote mapNote)
{
    Puts($"Метка добавлена игроком {player.UserIDString} на координаты {mapNote.Position}");
}
```

## CanMountEntity(BasePlayer,BaseMountable)

### Summary


### Parameters
- `player`: Игрок, пытающийся посадить.
- `entity`: Сущность, на которую посадится игрок.

### Returns
Возвращает true, если посадка разрешена, и false в противном случае.

### Example
```csharp
bool CanMountEntity(BasePlayer player, BaseMountable entity)
{
    Puts("CanMountEntity работает!");
    return true;
}
```

## OnWaterCollect(WaterPump,ItemDefinition)

### Summary


### Parameters
- `pump`: Водяная помпа.
- `itemDefinition`: Определение предмета, собранного из воды.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnWaterCollect(WaterPump pump, ItemDefinition itemDefinition)
{
    Puts("OnWaterCollect работает!");
}

В этом методе нет оператора return, что указывает на то, что тип возвращаемого значения равен void.
```

## OnEngineStarted(MotorRowboat,BasePlayer)

### Summary


### Parameters
- `rowboat`: Моторная лодка.
- `driver`: Водитель.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEngineStarted(MotorRowboat rowboat, BasePlayer driver)
{
    Puts("Двигатель запущен!");
}
```

## CanWaterBallSplash(ItemDefinition,UnityEngine.Vector3,float,int)

### Summary


### Parameters
- `liquidDef`: Определение жидкости.
- `position`: Позиция всплеска.
- `radius`: Радиус всплеска.
- `amount`: Количество жидкости в мяче.

### Returns
Возвращает true, если условие выполнено, и false в противном случае.

### Example
```csharp
bool CanWaterBallSplash(ItemDefinition liquidDef, Vector3 position, float radius, int amount)
{
    Puts("CanWaterBallSplash вызван!");
    // Если количество жидкости равно 0, то условие не выполняется
    if (amount == 0)
    {
        return false;
    }
    
    // Иначе возвращаем true
    return true;
}
```

## OnNpcGiveSoldItem(NPCVendingMachine,Item,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Объект NPC-автомата.
- `item`: Продаваемый предмет.
- `buyer`: Купивший игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcGiveSoldItem(NPCVendingMachine vendingMachine, Item item, BasePlayer buyer)
{
    Puts("OnNpcGiveSoldItem работает!");
    return null;
}
```

## OnItemLock(Item)

### Summary


### Parameters
- `item`: Объект, который был блокирован или разблокирован.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemLock(Item item)
{
    Puts("OnItemLock вызван!");
    return null;
}
```

## OnTeamRejectInvite(BasePlayer,RelationshipManager.PlayerTeam)

### Summary


### Parameters
- `player`: Игрок, который отклонил приглашение.
- `team`: Команда, в которую было выдано приглашение.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamRejectInvite(BasePlayer player, PlayerTeam team)
{
    Puts("OnTeamRejectInvite работает!");
    return null;
}
```

## OnLiquidWeaponFiringStopped(LiquidWeapon)

### Summary


### Parameters
- `liquidWeapon`: Объект жидкостного оружия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLiquidWeaponFiringStopped(LiquidWeapon liquidWeapon)
{
    Puts("OnLiquidWeaponFiringStopped работает!");
    return null;
}
```

## OnFireworkStarted(BaseFirework)

### Summary


### Parameters
- `firework`: Объект фейерверка.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnFireworkStarted(BaseFirework firework)
{
    Puts("OnFireworkStarted работает!");
}
```

## OnWildlifeTrap(SurvivalFishTrap,ItemDefinition)

### Summary


### Parameters
- `trap`: Ловушка для дикой рыбы.
- `itemDefinition`: Определение предмета, пойманного в ловушку.

### Returns
Возвращает null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnWildlifeTrap(SurvivalFishTrap trap, ItemDefinition itemDefinition)
{
    Puts("OnWildlifeTrap работает!");
    return null;
}
```

## OnMissionSucceeded(BaseMission,BaseMission.MissionInstance,BasePlayer)

### Summary


### Parameters
- `mission`: Объект миссии.
- `instance`: Инстанс миссии.
- `assignee`: Игрок, которому была назначена миссия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMissionSucceeded(BaseMission mission, BaseMission.MissionInstance instance, BasePlayer assignee)
{
    Puts("OnMissionSucceeded вызван!");
    return null;
}
```

## OnVehicleModuleMove(BaseVehicleModule,BaseModularVehicle,BasePlayer)

### Summary


### Parameters
- `module`: Модуль транспортного средства.
- `vehicle`: Транспортное средство.
- `player`: Игрок, который пытается переместить модуль.

### Returns
Возвращает true, если модуль может быть перемещен, и false в противном случае.

### Example
```csharp
bool OnVehicleModuleMove(BaseVehicleModule module, BaseModularVehicle vehicle, BasePlayer player)
{
    Puts("OnVehicleModuleMove вызван!");
    // Если необходимо переопределить поведение по умолчанию, верните true или false
    return true;
}
```

## CanNetworkTo(BasePlayer,BasePlayer)

### Summary


### Parameters
- `player1`: Первый игрок.
- `player2`: Второй игрок.

### Returns
Возвращает true, если сетевое соединение возможно, и false в противном случае.

### Example
```csharp
bool CanNetworkTo(BasePlayer player1, BasePlayer player2)
{
    Puts("CanNetworkTo работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnTerrainCreate(TerrainGenerator)

### Summary


### Parameters
- `generator`: Объект генерации терранина.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTerrainCreate(TerrainGenerator generator)
{
    Puts("OnTerrainCreate работает!");
}
```

## OnCupboardProtectionCalculated(BuildingPrivlidge,float)

### Summary


### Parameters
- `buildingPrivilege`: Права на здание.
- `protectedMinutes`: Расчитанное время защиты.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCupboardProtectionCalculated(BuildingPrivlidge buildingPrivilege, float protectedMinutes)
{
    Puts($"Защита шкафа рассчитана на {protectedMinutes} минут.");
}
```

## OnBonusItemDrop(Item,BasePlayer)

### Summary


### Parameters
- `item`: Выпавший бонусный предмет.
- `player`: Игрок, получивший бонусный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBonusItemDrop(Item item, BasePlayer player)
{
    Puts($"Бонусный предмет '{item.Info.Name}' выпал игроку {player.UserIDString}.");
}
```

## OnFireBallDamage(FireBall,BaseCombatEntity,HitInfo)

### Summary
Документация для метода `OnFireBallDamage`:

### Parameters
- `fireball`: Огненный мяч, который нанес урон.
- `entity`: Сущность, которую ударил огненный мяч.
- `hitInfo`: Информация о хите.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
Документация для метода `OnFireBallDamage`:

```rust
void OnFireBallDamage(FireBall fireball, BaseCombatEntity entity, HitInfo hitInfo)
{
    Puts("OnFireBallDamage работает!");
}
```

В этом методе нет оператора `return`, что указывает на то, что он не имеет возвращаемого значения.
```

## OnPhoneNameUpdated(PhoneController,string,BasePlayer)

### Summary


### Parameters
- `controller`: Контроллер телефона.
- `newName`: Новое имя телефона.
- `player`: Игрок, который обновил имя телефона.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPhoneNameUpdated(PhoneController controller, string newName, BasePlayer player)
{
    Puts($"Имя телефона '{controller}' обновлено на '{newName}' для игрока {player}");
    return null;
}
```

## OnLiquidVesselFill(BaseLiquidVessel,BasePlayer,LiquidContainer)

### Summary


### Parameters
- `vessel`: Объект, который заполняется.
- `player`: Игрок, выполняющий действие.
- `container`: Контейнер с жидкостью.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLiquidVesselFill(BaseLiquidVessel vessel, BasePlayer player, LiquidContainer container)
{
    Puts("OnLiquidVesselFill работает!");
    return null;
}
```

## OnMeleeAttack(BasePlayer,HitInfo)

### Summary
This is a C# code snippet that appears to be part of a game's physics engine. It's responsible for handling melee attacks and checking if the player has a clear line of sight (LOS) to the target entity.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game's physics engine. It's responsible for handling melee attacks and checking if the player has a clear line of sight (LOS) to the target entity.

Here's a breakdown of the code:

1. The function `DoAttackShared` is called, which likely performs the actual attack logic.
2. The code checks if the player has a clear LOS to the target entity using the `GamePhysics.LineOfSight` method. This method returns a boolean value indicating whether there are any obstacles between the player and the target.
3. If the player does have a clear LOS, the function sets a flag (`flag8`) to true.
4. The code then checks if the player's heart stress is within a certain threshold (0.2f). If it is, the player's metabolism uses some of their heart points.
5. If the player has a clear LOS and their heart stress is within the threshold, the function calls `DoAttackShared` again.
6. If the player does not have a clear LOS or their heart stress is too high, the code logs an invalid attack attempt using the `AntiHack.Log` method.

Some key variables and methods used in this code include:

* `player`: The player entity performing the melee attack.
* `hitInfo`: An object containing information about the hit (e.g., position, velocity).
* `GamePhysics.LineOfSight`: A method that checks if there are any obstacles between two points.
* `AntiHack.Log`: A method that logs an invalid attack attempt.

Overall, this code snippet is responsible for ensuring that melee attacks are performed correctly and within certain constraints.
```

## OnTeamLeave(RelationshipManager.PlayerTeam,BasePlayer)

### Summary


### Parameters
- `team`: Команда, из которой игрок уходит.
- `player`: Игрок, покидающий команду.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamLeave(RelationshipManager.PlayerTeam team, BasePlayer player)
{
    Puts("OnTeamLeave работает!");
    return null;
}
```

## OnMapMarkerRemove(BasePlayer,System.Collections.Generic.List<ProtoBuf.MapNote>,int)

### Summary


### Parameters
- `player`: Игрок, который удаляет метку.
- `notes`: Список заметок, которые будут удалены.
- `index`: Индекс заметки, которую нужно удалить.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMapMarkerRemove(BasePlayer player, System.Collections.Generic.List<ProtoBuf.MapNote> notes, int index)
{
    Puts("OnMapMarkerRemove работает!");
    return null;
}
```

## OnEntityControl(AutoTurret,ulong)

### Summary


### Parameters
- `entity`: Сущность, которую хочет контролировать игрок.
- `playerID`: ИД игрока.

### Returns
Возвращает true, если игрок может контролировать сущность, и false в противном случае.

### Example
```csharp
bool OnEntityControl(AutoTurret entity, ulong playerID)
{
    Puts("OnEntityControl вызван!");
    // Если игрок может контролировать сущность, вернуть true
    return true;
}
```

## IOnBasePlayerHurt(BasePlayer,HitInfo)

### Summary
This is a C# code snippet from the "Rust" game, specifically from the `BasePlayer` class. It appears to be handling damage dealt to a player by another entity.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet from the "Rust" game, specifically from the `BasePlayer` class. It appears to be handling damage dealt to a player by another entity.

Here's a breakdown of what the code does:

1. **Damage calculation**: The code calculates the total damage dealt to the player based on various factors, such as the type of damage (e.g., bullet, explosion), the initiator of the damage (the entity that caused it), and any modifiers applied by the game.
2. **Resistance and exposure**: If the player has resistance or exposure modifiers, these are taken into account when calculating the final damage.
3. **Radiation effects**: If the damage is due to radiation, the code checks if the player's radiation level is high enough to trigger a specific effect (e.g., a visual indicator).
4. **Drowning effect**: If the player takes too much water damage, the code triggers a drowning effect (a visual indicator).
5. **Achievements and rewards**: The code checks for achievements or rewards that might be triggered by the damage dealt.
6. **Player health update**: The player's health is updated based on the calculated damage.
7. **Client-side updates**: The code sends updates to the client about the player's new health state.

Some notable aspects of this code include:

* The use of a `cachedNonSuicideHitInfo` variable, which suggests that the game keeps track of recent damage events for some reason (e.g., to prevent players from exploiting certain mechanics).
* The presence of various constants and variables with names like "SUMMER_SOAKED" or "funWaterDamageThreshold", which indicate that the game has a rich set of features and settings.
* The use of `ClientRPC` calls, which suggests that the game uses a client-server architecture to update player information on the client-side.

Overall, this code snippet provides insight into how the "Rust" game handles damage events and updates player health state in response.
```

## OnResearchCostDetermine(Item)

### Summary


### Parameters
- `item`: Предмет, для которого определяются затраты.

### Returns
Затраты на исследование предмета. Если не переопределено, возвращает 0.

### Example
```csharp
object OnResearchCostDetermine(Item item)
{
    Puts("OnResearchCostDetermine работает!");
    return 0;
}
```

## OnEntityLeave(TriggerBase,BaseEntity)

### Summary


### Parameters
- `trigger`: Триггер, который вызвал этот хук.
- `entity`: Сущность, покидающая область.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityLeave(TriggerBase trigger, BaseEntity entity)
{
    Puts("OnEntityLeave работает!");
    return null;
}
```

## CanChangeGrade(BasePlayer,BuildingBlock,BuildingGrade.Enum,ulong)

### Summary


### Parameters
- `player`: Игрок, пытающийся изменить степень.
- `block`: Предмет, степень которого будет изменена.
- `grade`: Новая степень предмета.
- `skinId`: ID кожи предмета.

### Returns
Возвращает true, если игрок может изменить степень предмета, и false в противном случае.

### Example
```csharp
bool CanChangeGrade(BasePlayer player, BuildingBlock block, BuildingGrade.Enum grade, ulong skinId)
{
    Puts("CanChangeGrade работает!");
    // Если возвращаемое значение равно null, то поведение по умолчанию не переопределено
    return true;
}
```

## CanBeHomingTargeted(RoadFlare)

### Summary


### Parameters
- `flare`: Снаряд с наведением.

### Returns
Возвращает <c>true</c>, если объект может быть целью, и <c>false</c> в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(RoadFlare flare)
{
    Puts("CanBeHomingTargeted вызван!");
    return false; // Возвращаемое значение по умолчанию
}
```

## IOnUserApprove(Network.Connection)

### Summary


### Parameters
- `connection`: Соединение пользователя.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void IOnUserApprove(Network.Connection connection)
{
    Puts($"Соединение пользователя {connection.userid} подтверждено.");
}
```

## OnItemUse(Item,int)

### Summary


### Parameters
- `item`: Предмет, который используется.
- `amountToConsume`: Количество единиц предмета, которое необходимо использовать.

### Returns
Возвращает количество использованных единиц предмета, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemUse(Item item, int amountToConsume)
{
    Puts("OnItemUse работает!");
    return null;
}
```

## CanLootEntity(BasePlayer,IndustrialCrafter)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть лут.
- `entity`: Сущность, из которой открывается лут.

### Returns
Возвращает true, если игрок может открыть лут, и false в противном случае.

### Example
```csharp
bool CanLootEntity(BasePlayer player, IndustrialCrafter entity)
{
    Puts("CanLootEntity работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true;
}
```

## OnLootPlayer(BasePlayer,BasePlayer)

### Summary


### Parameters
- `looter`: Игрок, который открывает лоотинг.
- `player`: Игрок, чей инвентарь подлежит лоотингу.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnLootPlayer(BasePlayer looter, BasePlayer player)
{
    Puts($"Игрок {looter.UserIDString} открыл лоотинг игрока {player.UserIDString}");
}
```

## OnTurretAssigned(AutoTurret,ulong,BasePlayer)

### Summary


### Parameters
- `turret`: Тарантелла.
- `id`: ID игрока.
- `player`: Игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretAssigned(AutoTurret turret, ulong id, BasePlayer player)
{
    Puts("OnTurretAssigned работает!");
    return null;
}
```

## OnTurretShutdown(AutoTurret)

### Summary


### Parameters
- `turret`: Туррет, который завершил работу.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretShutdown(AutoTurret turret)
{
    Puts("OnTurretShutdown работает!");
    return null;
}
```

## OnSurveyGather(SurveyCharge,Item)

### Summary


### Parameters
- `surveyCharge`: Заряд для сбора сведений.
- `item`: Изделие, которое было собрано.

### Returns
No return value.

### Example
```csharp
void OnSurveyGather(SurveyCharge surveyCharge, Item item)
{
    Puts("OnSurveyGather вызван!");
}
```

## OnPlayerMarkersSend(BasePlayer,ProtoBuf.MapNoteList)

### Summary


### Parameters
- `player`: Игрок, которому отправляются маркеры.
- `markers`: Список маркеров для отправки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerMarkersSend(BasePlayer player, ProtoBuf.MapNoteList markers)
{
    Puts("OnPlayerMarkersSend работает!");
    return null;
}
```

## OnInventoryAmmoFind(PlayerInventory,System.Collections.Generic.List<Item>,Rust.AmmoTypes)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `items`: Список предметов, которые необходимо проверить.
- `ammoType`: Тип патрона, который ищется.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnInventoryAmmoFind(PlayerInventory inventory, List<Item> items, Rust.AmmoTypes ammoType)
{
    Puts("OnInventoryAmmoFind работает!");
    return null;
}
```

## OnPlayerDisconnected(BasePlayer,string)

### Summary


### Parameters
- `player`: Игрок, который отключился.
- `reason`: Причина отключения.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerDisconnected(BasePlayer player, string reason)
{
    Puts($"Игрок {player.UserIDString} отключился по причине: {reason}");
}
```

## OnToggleVendingBroadcast(VendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Торговый автомат.
- `player`: Игрок, который вызвал хук.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnToggleVendingBroadcast(VendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnToggleVendingBroadcast работает!");
}
```

## OnPhoneDialFail(PhoneController,Telephone.DialFailReason,BasePlayer)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `reason`: Причина неудачи вызова.
- `player`: Игрок, который пытался сделать вызов.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhoneDialFail(PhoneController phoneController, Telephone.DialFailReason reason, BasePlayer player)
{
    Puts("OnPhoneDialFail работает!");
}
```

## OnPlayerRespawned(BasePlayer)

### Summary


### Parameters
- `player`: Игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerRespawned(BasePlayer player)
{
    Puts("OnPlayerRespawned работает!");
}
```

## OnHelicopterStrafeEnter(PatrolHelicopterAI,UnityEngine.Vector3,BasePlayer)

### Summary


### Parameters
- `patrolHelicopterAI`: Объект AI вертолета.
- `targetPosition`: Позиция цели.
- `strafeTarget`: Игрок, к которому стреляет вертолет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnHelicopterStrafeEnter(PatrolHelicopterAI patrolHelicopterAI, UnityEngine.Vector3 targetPosition, BasePlayer strafeTarget)
{
    Puts("Вертолет вошел в режим страфа!");
}
```

## OnFireworkDamage(BaseFirework,HitInfo)

### Summary


### Parameters
- `firework`: Фейерверк, наносящий урон.
- `info`: Информация о хите.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFireworkDamage(BaseFirework firework, HitInfo info)
{
    Puts("OnFireworkDamage работает!");
    return null;
}
```

## OnBradleyApcHunt(BradleyAPC)

### Summary
Документация для метода `OnBradleyApcHunt(BradleyAPC)`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnBradleyApcHunt(BradleyAPC)`:

**Описание:**

Метод `OnBradleyApcHunt` является хуком, который вызывается в методе `UpdateMovement_Hunt`. Он используется для определения поведения Bradley APC при обнаружении игрока.

**Параметры:**

* `BradleyAPC`: Объект Bradley APC, на котором будет вызван этот метод.

**Возвращаемое значение:**

Нет возвращаемого значения (void).

**Описание функциональности:**

Метод `OnBradleyApcHunt` не имеет конкретной реализации и является пустым хуком. Это означает, что он не выполняет никаких действий при вызове.

**Пример использования:**

Ниже приведен пример минимального кода для демонстрации функциональности метода:
```csharp
public void OnBradleyApcHunt(BradleyAPC bradleyApC)
{
    // Пустой хук, не выполняющий никаких действий
}
```
**Примечания:**

* Метод `OnBradleyApcHunt` не имеет возвращаемого значения и поэтому не требует оператора return.
* Хук не выполняет никаких действий при вызове.
```

## OnRackedWeaponMount(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Закрепляемое оружие.
- `player`: Игрок, закрепляющий оружие.
- `rack`: Станок, на который закрепляется оружие.

### Returns
Возвращает true, если оружие успешно закреплено; иначе false.

### Example
```csharp
bool OnRackedWeaponMount(Item item, BasePlayer player, WeaponRack rack)
{
    Puts("OnRackedWeaponMount вызван!");
    // Код для демонстрации функциональности
    return true;
}
```

## OnPlayerWantsMount(BasePlayer,BaseMountable)

### Summary


### Parameters
- `player`: Игрок, который хочет сесть.
- `entity`: Сущность, которую игрок хочет сесть.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerWantsMount(BasePlayer player, BaseMountable entity)
{
    Puts("OnPlayerWantsMount работает!");
    return null;
}
```

## OnEntityLoaded(BaseNetworkable,BaseNetworkable.LoadInfo)

### Summary


### Parameters
- `entity`: Загруженная сущность.
- `loadInfo`: Информация о загрузке.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEntityLoaded(BaseNetworkable entity, LoadInfo loadInfo)
{
    Puts($"Сущность {entity} успешно загружена.");
}
```

## OnBuildingSplit(BuildingManager.Building,uint)

### Summary


### Parameters
- `building`: Здание, которое разделяется.
- `newID`: Новый ID здания после разделения.

### Returns
No return value.

### Example
```csharp
object OnBuildingSplit(BuildingManager.Building building, uint newID)
{
    Puts($"Здание {building.buildingID} разделено на {newID}");
    // Здесь можно добавить дополнительную логическую или физическую обработку при разделении здания
}
 
В данном случае метод OnBuildingSplit не возвращает никакого значения, поэтому тип возвращаемого значения object.
```

## OnPortalUsed(BasePlayer,BasePortal)

### Summary


### Parameters
- `player`: Игрок, который использовал портал.
- `portal`: Портал, который был использован.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPortalUsed(BasePlayer player, BasePortal portal)
{
    Puts("OnPortalUsed работает!");
}

В этом методе нет оператора return, поэтому тип возвращаемого значения void.
```

## CanHackCrate(BasePlayer,HackableLockedCrate)

### Summary


### Parameters
- `player`: Игрок, пытающийся взломать коробку.
- `crate`: Закрепленная коробка.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object CanHackCrate(BasePlayer player, HackableLockedCrate crate)
{
    Puts("CanHackCrate работает!");
    return null;
}
```

## OnTurretToggle(AutoTurret)

### Summary


### Parameters
- `turret`: Таран, который был включен или выключен.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretToggle(AutoTurret turret)
{
    Puts("OnTurretToggle работает!");
    return null;
}
```

## OnPlayerInput(BasePlayer,InputState)

### Summary
Документация для OnPlayerInput(BasePlayer, InputState)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для OnPlayerInput(BasePlayer, InputState)

**Описание**

Метод OnPlayerInput вызывается при получении входных данных от игрока. Этот метод используется для обновления состояния игрока на основе его действий.

**Параметры**

* `BasePlayer`: Объект игрока, который отправил входные данные.
* `InputState`: Состояние входных данных, которое содержит информацию о нажатых кнопках и других действиях игрока.

**Возвращаемое значение**

Нет возвращаемого значения (void).

**Примеры использования**


```csharp
// Пример использования метода OnPlayerInput для обновления состояния игрока на основе его действий.
private void OnPlayerInput(BasePlayer player, InputState input)
{
    // Обновите состояние игрока на основе входных данных.
    UpdatePlayerState(player, input);
}

// Пример использования метода OnPlayerInput для проверки нажатых кнопок и обновления состояния игрока.
private void OnPlayerInput(BasePlayer player, InputState input)
{
    // Проверьте нажатые кнопки.
    if (input.WasJustPressed(BUTTON.FIRE_PRIMARY))
    {
        // Обновите состояние игрока на основе нажатой кнопки.
        UpdatePlayerState(player, BUTTON.FIRE_PRIMARY);
    }
}
```


**Примечания**

* Этот метод вызывается в методе OnReceiveTick, который обрабатывает входные данные от игроков.
* Метод OnPlayerInput используется для обновления состояния игрока на основе его действий и может быть использован для различных целей, таких как проверка нажатых кнопок или обновление состояния игрока.
```

## CanTrainCarCouple(TrainCar,TrainCar)

### Summary


### Parameters
- `car1`: Первый вагон.
- `car2`: Второй вагон.

### Returns
Возвращает true, если вагоны можно соединить, и false в противном случае.

### Example
```csharp
bool CanTrainCarCouple(TrainCar car1, TrainCar car2)
{
    Puts("CanTrainCarCouple вызван!");
    // Здесь вы можете добавить дополнительную логику для проверки возможности соединения вагонов
    return true; // Возвращаем true по умолчанию
}
```

## OnFlameExplosion(FlameExplosive,UnityEngine.Collider)

### Summary


### Parameters
- `explosive`: Объект, вызвавший взрыв.
- `collider`: Коллайдер объекта.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnFlameExplosion(FlameExplosive explosive, UnityEngine.Collider collider)
{
    Puts("OnFlameExplosion вызван!");
}
```

## OnEntityMounted(BaseMountable,BasePlayer)

### Summary


### Parameters
- `entity`: Сущность, к которой закреплен игрок.
- `player`: Игрок, закрепленный за сущностью.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityMounted(BaseMountable entity, BasePlayer player)
{
    Puts("OnEntityMounted работает!");
    return null;
}
```

## OnSignLocked(Signage,BasePlayer)

### Summary


### Parameters
- `sign`: Знак, который был заблокирован.
- `player`: Игрок, который заблокировал знак.

### Returns
No return value.

### Example
```csharp
object OnSignLocked(Signage sign, BasePlayer player)
{
    Puts("OnSignLocked вызван!");
    return null;
}
```

## OnCorpsePopulate(HumanNPC,NPCPlayerCorpse)

### Summary


### Parameters
- `npc`: НПС.
- `corpse`: Тело НПС.

### Returns
Возвращает тело НПС или null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnCorpsePopulate(HumanNPC npc, NPCPlayerCorpse corpse)
{
    // Минимальный код для демонстрации функциональности
    Puts("OnCorpsePopulate работает!");
    
    return null;
}
```

## CanUpdateSign(BasePlayer,PhotoFrame)

### Summary


### Parameters
- `player`: Игрок, пытающийся обновить подпись.
- `photoFrame`: Фотография, на которой будет обновлена подпись.

### Returns
Возвращает true, если игрок может обновить подпись, и false в противном случае.

### Example
```csharp
bool CanUpdateSign(BasePlayer player, PhotoFrame photoFrame)
{
    Puts("CanUpdateSign работает!");
    // Если ReturnType - bool, верните значение
    return true;
}
```

## CanHelicopterDropCrate(CH47HelicopterAIController)

### Summary


### Parameters
- `controller`: Контроллер хеликоптера.

### Returns
Возвращает true, если хеликоптер может сбросить контейнер, и false в противном случае.

### Example
```csharp
bool CanHelicopterDropCrate(CH47HelicopterAIController controller)
{
    Puts("CanHelicopterDropCrate работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnOvenToggle(BaseOven,BasePlayer)

### Summary


### Parameters
- `oven`: Печь.
- `player`: Игрок, который включил или выключил печь.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnOvenToggle(BaseOven oven, BasePlayer player)
{
    Puts("OnOvenToggle работает!");
    return null;
}
```

## OnExplosiveDud(DudTimedExplosive)

### Summary


### Parameters
- `dud`: Взрывчатое устройство, которое стало дудом.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnExplosiveDud(DudTimedExplosive dud)
{
    Puts("OnExplosiveDud работает!");
}

В этом методе нет оператора return, что указывает на то, что тип возвращаемого значения равен void.
```

## OnGiveSoldItem(VendingMachine,Item,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Автомат, из которого был куплен предмет.
- `item`: Покупаемый предмет.
- `buyer`: Купивший игрок.
- `id`: ID игрока.
- `oldName`: Старый никнейм игрока.
- `newName`: Новый никнейм игрока.
- `player`: Игрок, который хочет снять предмет.
- `item`: Предмет, который нужно снять.
- `vendingMachine`: Автомат, из которого был куплен предмет.
- `item`: Покупаемый предмет.
- `buyer`: Купивший игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnGiveSoldItem(VendingMachine vendingMachine, Item item, BasePlayer buyer)
{
    Puts("OnGiveSoldItem работает!");
}

Когда вы видите код типа:
object obj = Interface.CallHook("OnGiveSoldItem", this, soldItem, buyer);
Обратите внимание, что `Interface.CallHook` представляет метод `OnGiveSoldItem` в этом контексте. Посмотрите, как используется 'obj', чтобы определить тип возвращаемого значения. Примеры:

- if (obj is bool) return (bool)obj; -> ReturnType: bool
- if (obj is string s) return s; -> ReturnType: string
- if (obj is int i) return i; -> ReturnType: int
- if (obj != null) return obj; -> ReturnType: object
- Нет оператора return после Interface.CallHook -> ReturnType: void

Также учитывайте случаи типа "Interface.CallHook('MethodName', Parameters...) == null"

User: OnUserNameUpdated(string, string, string)

[LibraryFunction("UpdateNickname")]

public void UpdateNickname(string playerId, string playerName)
{
    if (this.UserExists(playerId))
    {
        UserData userData = this.GetUserData(playerId);
        string lastSeenNickname = userData.LastSeenNickname;
        string obj = playerName.Sanitize();
        userData.LastSeenNickname = playerName.Sanitize();
        Interface.CallHook("OnUserNameUpdated", playerId, lastSeenNickname, obj);
    }
}

RustGpt:
void OnUserNameUpdated(string id, string oldName, string newName)
{
    Puts($"Имя игрока изменилось с {oldName} на {newName} для ID {id}");
}

User: CanDismountEntity(BasePlayer, BaseMountable)

public void DismountPlayer(global::BasePlayer player, global::Item item)
{
    if (Interface.CallHook("CanDismountEntity", player, item) == null)
    {
        // код для снятия предмета
    }
}

RustGpt:
void CanDismountEntity(BasePlayer player, BaseMountable item)
{
    Puts("CanDismountEntity работает!");
}

User: OnGiveSoldItem(VendingMachine, Item, BasePlayer)

public virtual void GiveSoldItem(Item soldItem, BasePlayer buyer)
{
    if (Interface.CallHook("OnGiveSoldItem", this, soldItem, buyer) == null)
    {
        while (soldItem.amount > soldItem.MaxStackable())
        {
            Item item = soldItem.SplitItem(soldItem.MaxStackable());
            buyer.GiveItem(item, GiveItemReason.PickedUp);
        }
        buyer.GiveItem(soldItem, GiveItemReason.PickedUp);
    }
}

RustGpt:
void OnGiveSoldItem(VendingMachine vendingMachine, Item item, BasePlayer buyer)
{
    Puts("OnGiveSoldItem работает!");
}

1. Проанализируйте контекст на наличие использования <interface_callhook_analysis>.
2. Определите соответствующий тип возвращаемого значения на основе использования возвращаемого значения (<return_type_rules>).
3. Включите информацию о возвращаемом значении и его использовании в ваш ответ.
4. Предоставьте детализированную структуру метода с минимальным кодом для демонстрации функциональности (1-3 строки).
5. Для методов с типом возвращаемого значения void, пропустите оператор return.
6. Используйте раздел <examples> в качестве справки для понимания структуры метода и минимального кода, необходимого для демонстрации функциональности.
```

## OnPlayerCorpseSpawned(BasePlayer,PlayerCorpse)

### Summary
Документация для метода `OnPlayerCorpseSpawned`:

### Parameters
- `player`: Игрок, чье тело было создано.
- `corpse`: Тело игрока.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnPlayerCorpseSpawned`:

```rust
void OnPlayerCorpseSpawned(BasePlayer player, PlayerCorpse corpse)
{
    // Код для демонстрации функциональности
}
```

В этом методе можно добавить логирование или другие действия, которые необходимо выполнить после создания тела игрока.
```

## OnNpcTargetSense(BaseEntity,BaseEntity,AIBrainSenses)

### Summary


### Parameters
- `npc`: НПЦ, который заметил сущность.
- `entity`: Сущность, которую заметил НПЦ.
- `senses`: Объект чувств, используемых НПЦ для определения сущности.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcTargetSense(BaseEntity npc, BaseEntity entity, AIBrainSenses senses)
{
    Puts("OnNpcTargetSense работает!");
    return null;
}
```

## OnSleepingBagValidCheck(SleepingBag,ulong,bool)

### Summary


### Parameters
- `sleepingBag`: Объект спальнной сумки.
- `playerID`: ИД игрока.
- `ignoreTimers`: Флаг игнорирования таймеров.

### Returns
Возвращает true, если спальнная сумка валидна, и false в противном случае.

### Example
```csharp
bool OnSleepingBagValidCheck(SleepingBag sleepingBag, ulong playerID, bool ignoreTimers)
{
    Puts("OnSleepingBagValidCheck вызван!");
    
    // Если игрок является владельцем спальнной сумки и не игнорирует таймеры,
    // проверяем, истек ли срок действия спальнной сумки.
    if (deployerUserID == playerID && !ignoreTimers)
    {
        return unlockTime < UnityEngine.Time.realtimeSinceStartup;
    }
    
    // В противном случае возвращаем false.
    return false;
}
```

## CanTakeCutting(BasePlayer,GrowableEntity)

### Summary


### Parameters
- `player`: Игрок, пытающийся взять срез.
- `entity`: Сущность, из которой берется срез.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object CanTakeCutting(BasePlayer player, GrowableEntity entity)
{
    Puts("CanTakeCutting работает!");
    return null;
}
```

## CanNpcEat(BaseNpc,BaseEntity)

### Summary


### Parameters
- `npc`: НПС, пытающийся съесть сущность.
- `entity`: Сущность, которую НПС хочет съесть.

### Returns
Возвращает true, если НПС может съесть сущность, и false в противном случае.

### Example
```csharp
bool CanNpcEat(BaseNpc npc, BaseEntity entity)
{
    Puts("CanNpcEat работает!");
    return !entity.HasTrait(TraitFlag.Food) || entity.HasTrait(TraitFlag.Alive);
}
```

## OnMlrsTargetSet(MLRS,UnityEngine.Vector3,BasePlayer)

### Summary


### Parameters
- `user`: Пользователь, установивший цель.
- `targetPosition`: Позиция цели.
- `mountedPlayer`: Игрок, на котором установлен MLRS.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMlrsTargetSet(BaseUser user, Vector3 targetPosition, BasePlayer mountedPlayer)
{
    Puts("OnMlrsTargetSet вызван!");
    return null;
}
```

## OnBookmarkDelete(ComputerStation,BasePlayer,string)

### Summary


### Parameters
- `station`: Компьютерная станция.
- `player`: Игрок, удаляющий закладку.
- `bookmarkName`: Название закладки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarkDelete(ComputerStation station, BasePlayer player, string bookmarkName)
{
    Puts("OnBookmarkDelete вызван!");
    // Здесь можно добавить дополнительную логическую логику или обработку
    return null;
}
```

## OnStashHidden(StashContainer,BasePlayer)

### Summary


### Parameters
- `stashContainer`: Контейнер с сокровищами.
- `player`: Игрок, который скрыл контейнер с сокровищами.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnStashHidden(StashContainer stashContainer, BasePlayer player)
{
    Puts("Контейнер с сокровищами был скрыт!");
}
```

## OnExperimentEnd(Workbench)

### Summary


### Parameters
- `workbench`: Рабочий стол, на котором завершился эксперимент.

### Returns
No return value.

### Example
```csharp
void OnExperimentEnd(Workbench workbench)
{
    Puts("OnExperimentEnd вызван!");
}
```

## OnPlayerLand(BasePlayer,float)

### Summary


### Parameters
- `player`: Игрок, приземлившийся.
- `velocity`: Скорость приземления.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerLand(BasePlayer player, float velocity)
{
    Puts("OnPlayerLand работает!");
    return null;
}
```

## OnEntitySpawned(BaseNetworkable)

### Summary


### Parameters
- `entity`: Сущность, которая была спавнена.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEntitySpawned(BaseNetworkable entity)
{
    Puts($"Сущность {entity} успешно спавнена!");
}
```

## OnEntityDeath(BaseCombatEntity,HitInfo)

### Summary


### Parameters
- `entity`: Сущность, которая умерла.
- `hitInfo`: Информация о выстреле, который привел к смерти сущности.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityDeath(BaseCombatEntity entity, HitInfo hitInfo)
{
    Puts("OnEntityDeath работает!");
    return null;
}
```

## CanResearchItem(BasePlayer,Item)

### Summary


### Parameters
- `player`: Игрок, пытающийся исследовать предмет.
- `item`: Предмет, который нужно исследовать.

### Returns
Возвращает false, если исследование невозможно.

### Example
```csharp
bool CanResearchItem(BasePlayer player, Item item)
{
    Puts("CanResearchItem работает!");
    return true;
}
```

## OnBonusItemDropped(Item,BasePlayer)

### Summary


### Parameters
- `item`: Выпавший бонусный предмет.
- `player`: Игрок, которому выпал бонусный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBonusItemDropped(Item item, BasePlayer player)
{
    Puts($"Бонусный предмет '{item.Info.Name}' выпал игроку {player.UserIDString}.");
}
```

## OnHammerHit(BasePlayer,HitInfo)

### Summary


### Parameters
- `player`: Игрок, который наносит удар.
- `hitInfo`: Информация о хите.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHammerHit(BasePlayer player, HitInfo hitInfo)
{
    Puts("OnHammerHit работает!");
    return null;
}
```

## OnBuildingPrivilege(BaseEntity,OBB)

### Summary


### Parameters
- `entity`: Объект, для которого требуется определить привилегию.
- `obb`: Ограничивающая коробка здания.

### Returns
Возвращает привилегию здания или null, если не удалось определить.

### Example
```csharp
object OnBuildingPrivilege(BaseEntity entity, OBB obb)
{
    Puts("OnBuildingPrivilege вызван!");
    
    // Если возвращаемое значение равно null, то метод не переопределяет поведение по умолчанию
    return null;
}
```

## OnTeamAcceptInvite(RelationshipManager.PlayerTeam,BasePlayer)

### Summary


### Parameters
- `team`: Команда, которую игрок хочет присоединиться.
- `player`: Игрок, который принимает приглашение.

### Returns
Возвращает null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnTeamAcceptInvite(PlayerTeam team, BasePlayer player)
{
    Puts("OnTeamAcceptInvite работает!");
    return null;
}
```

## OnBradleyApcThink(BradleyAPC)

### Summary


### Parameters
- `apc`: Объект Bradley APC.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBradleyApcThink(BradleyAPC apc)
{
    Puts("OnBradleyApcThink вызван.");
}
```

## OnPlayerDeath(BasePlayer,HitInfo)

### Summary


### Parameters
- `player`: Игрок, который умер.
- `info`: Информация о смерти (например, причина смерти).

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerDeath(BasePlayer player, HitInfo info)
{
    Puts("OnPlayerDeath работает!");
    return null;
}
```

## OnVendingShopOpened(VendingMachine,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Машина для продажи.
- `player`: Игрок, открывающий магазин.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVendingShopOpened(VendingMachine vendingMachine, BasePlayer player)
{
    Puts("OnVendingShopOpened работает!");
    return null;
}
```

## OnLootEntity(BasePlayer,BaseEntity)

### Summary


### Parameters
- `player`: Игрок, который начинает ломать сущность.
- `entity`: Сущность, которую ломает игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootEntity(BasePlayer player, BaseEntity entity)
{
    Puts("OnLootEntity работает!");
    return null;
}
```

## OnMissionFailed(BaseMission,BaseMission.MissionInstance,BasePlayer,BaseMission.MissionFailReason)

### Summary


### Parameters
- `mission`: Миссия, которая завершилась неудачей.
- `instance`: Инстанс миссии.
- `assignee`: Игрок, которому была назначена миссия.
- `failReason`: Причина завершения миссии неудачей.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMissionFailed(BaseMission mission, BaseMission.MissionInstance instance, BasePlayer assignee, BaseMission.MissionFailReason failReason)
{
    Puts("OnMissionFailed вызван!");
    return null;
}
```

## OnReactiveTargetReset(ReactiveTarget)

### Summary


### Parameters
- `target`: Объект, на котором вызвана эта функция.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnReactiveTargetReset(ReactiveTarget target)
{
    Puts("OnReactiveTargetReset работает!");
}
```

## OnTeamInvite(BasePlayer,BasePlayer)

### Summary


### Parameters
- `inviter`: Игрок, отправляющий приглашение.
- `invitee`: Игрок, которому отправляется приглашение.

### Returns
Возвращает true, если приглашение успешно отправлено, и false в противном случае.

### Example
```csharp
bool OnTeamInvite(BasePlayer inviter, BasePlayer invitee)
{
    Puts($"Предложено приглашение игроку {invitee.UserIDString} от команды {inviter.UserIDString}");
    return true;
}
```

## OnPlayerLanded(BasePlayer,float)

### Summary


### Parameters
- `player`: Игрок, приземлившийся.
- `velocity`: Скорость приземления.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerLanded(BasePlayer player, float velocity)
{
    Puts($"Игрок {player.UserIDString} приземлился с скоростью {velocity}");
    return null;
}
```

## OnPlayerSetInfo(Network.Connection,string,string)

### Summary


### Parameters
- `connection`: Соединение игрока.
- `key`: Ключ информации.
- `val`: Новое значение информации.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerSetInfo(Network.Connection connection, string key, string val)
{
    Puts($"Игрок {connection.playerId} изменил информацию о себе: {key} = {val}");
    return null;
}
```

## OnStructureDemolish(StabilityEntity,BasePlayer,bool)

### Summary


### Parameters
- `entity`: Сущность структуры.
- `player`: Игрок, выполнивший демонтаж.
- `isPlayerDemolish`: Флаг, указывающий, что демонтаж был выполнен игроком.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnStructureDemolish(StabilityEntity entity, BasePlayer player, bool isPlayerDemolish)
{
    Puts("OnStructureDemolish работает!");
    return null;
}
```

## OnEntityStabilityCheck(StabilityEntity)

### Summary


### Parameters
- `entity`: Сущность, для которой проводится проверка стабильности.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityStabilityCheck(StabilityEntity entity)
{
    Puts("OnEntityStabilityCheck работает!");
    return null;
}
```

## CanSetBedPublic(BasePlayer,SleepingBag)

### Summary


### Parameters
- `player`: Игрок, пытающийся сделать спящую кровать общественной.
- `sleepingBag`: Спящая кровать.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object CanSetBedPublic(BasePlayer player, SleepingBag sleepingBag)
{
    Puts("CanSetBedPublic работает!");
    return null;
}
```

## OnPatrolHelicopterKill(PatrolHelicopter,HitInfo)

### Summary


### Parameters
- `helicopter`: Уничтоженный патрульный вертолет.
- `info`: Информация о выстреле, которое привело к уничтожению.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPatrolHelicopterKill(PatrolHelicopter helicopter, HitInfo info)
{
    Puts("OnPatrolHelicopterKill работает!");
    return null;
}
```

## OnRespawnInformationGiven(BasePlayer,System.Collections.Generic.List<ProtoBuf.RespawnInformation.SpawnOptions>)

### Summary
Документация для метода `OnRespawnInformationGiven`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnRespawnInformationGiven`:

**Название:** `OnRespawnInformationGiven`

**Описание:** Этот хук вызывается в методе `SendRespawnOptions()` и предназначен для предоставления информации о respawn-опциях игроку.

**Параметры:**

* `BasePlayer`: Объект игрока, которому предоставляется информация.
* `System.Collections.Generic.List<ProtoBuf.RespawnInformation.SpawnOptions>`: Список respawn-опций, которые будут предоставлены игроку.

**Возвращаемое значение:** `void` (метод не возвращает никаких значений).

**Пример использования:**
```csharp
public void SendRespawnOptions()
{
    // ...
    List<RespawnInformation.SpawnOptions> list = Facepunch.Pool.GetList<RespawnInformation.SpawnOptions>();
    ulong num = userID;
    Interface.CallHook("OnRespawnInformationGiven", this, list);
    // ...
}
```
**Структура метода:**
```csharp
void OnRespawnInformationGiven(BasePlayer player, List<RespawnInformation.SpawnOptions> spawnOptions)
{
    // Код метода
}
```
**Примечания:** Этот хук вызывается в методе `SendRespawnOptions()`, который является частью системы respawn-опций игрока. Метод не возвращает никаких значений и предназначен для предоставления информации о respawn-опциях игроку.
```

## OnPlayerWantsDismount(BasePlayer,BaseMountable)

### Summary


### Parameters
- `player`: Игрок, пытающийся снять объект.
- `entity`: Объект, который нужно снять.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerWantsDismount(BasePlayer player, BaseMountable entity)
{
    Puts("OnPlayerWantsDismount работает!");
    return null;
}
```

## OnFuelAmountCheck(EntityFuelSystem,Item)

### Summary


### Parameters
- `entityFuelSystem`: Система топлива.
- `item`: Топливо.

### Returns
Возвращает количество топлива, если поведение по умолчанию переопределено. Иначе возвращает 0.

### Example
```csharp
object OnFuelAmountCheck(EntityFuelSystem entityFuelSystem, Item item)
{
    Puts("OnFuelAmountCheck работает!");
    return 0;
}
```

## OnWeaponFired(BaseProjectile,BasePlayer,ItemModProjectile,ProtoBuf.ProjectileShoot)

### Summary
This is a C# code snippet that appears to be part of a game's server-side logic. It handles the firing of a projectile from a player's weapon. Here's a breakdown of the code:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game's server-side logic. It handles the firing of a projectile from a player's weapon. Here's a breakdown of the code:

**Functionality**

The code checks various conditions before allowing the player to fire a projectile:

1. **Client validation**: The code verifies if the client (player) is allowed to attack using `VerifyClientAttack(player)`.
2. **Reload cooldown**: If the player has recently reloaded their weapon, they cannot fire again until the reload cooldown period has passed.
3. **Magazine empty**: If the player's magazine is empty and infinite ammo cheat is not enabled, they cannot fire.
4. **Ammo mismatch**: The code checks if the projectile's ammo type matches the primary magazine's ammo type.
5. **Projectile count mismatch**: The code ensures that the number of projectiles being fired does not exceed the maximum allowed by the weapon.

**Server-side logic**

If all conditions are met, the server:

1. **Broadcasts a signal**: The server broadcasts a `Signal.Attack` event to notify other clients about the player's attack.
2. **Creates projectile effects**: The server creates projectile effects on the client-side using `CreateProjectileEffectClientside`.
3. **Updates player stats**: The server updates the player's stats, such as adding experience points for firing the weapon.
4. **Marks hostile players**: The server marks other players as hostile for a short period.

**Other functions**

The code also calls various hooks and functions, such as:

1. `OnWeaponFired`: A hook that allows plugins to respond to the player's attack.
2. `DidAttackServerside`: A function that is called after the player has attacked.
3. `UpdateItemCondition`: A function that updates the item condition (e.g., magazine empty).
4. `EACServer.LogPlayerUseWeapon`: A function that logs the player's use of a weapon.

Overall, this code snippet handles the server-side logic for firing a projectile from a player's weapon, ensuring that various conditions are met before allowing the attack to occur.
```

## OnSamSiteTarget(SamSite,SamSite.ISamSiteTarget)

### Summary


### Parameters
- `samSite`: Объект самонаводящегося снаряда.
- `target`: Цель, которую необходимо определить.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSamSiteTarget(SamSite samSite, ISamSiteTarget target)
{
    Puts("OnSamSiteTarget работает!");
}
```

## OnItemRemove(Item)

### Summary


### Parameters
- `item`: Удаляемый предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemRemove(Item item)
{
    Puts("OnItemRemove работает!");
    return null;
}
```

## OnSignUpdated(Signage,BasePlayer,int)

### Summary


### Parameters
- `signage`: Знак.
- `player`: Игрок, который обновил знак.
- `num`: Номер знака.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSignUpdated(Signage signage, BasePlayer player, int num)
{
    Puts("OnSignUpdated работает!");
    return null;
}
```

## OnInventoryAmmoItemFind(PlayerInventory,ItemDefinition)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `itemDefinition`: Определение предмета (патрона).

### Returns
Возвращает найденный патрон, если он существует в инвентаре игрока. Иначе возвращает null или результат поиска по имени.

### Example
```csharp
object OnInventoryAmmoItemFind(PlayerInventory inventory, ItemDefinition itemDefinition)
{
    // Минимальный код для демонстрации функциональности
    Puts("OnInventoryAmmoItemFind вызван!");
    
    // Если ReturnType - object, возвращаемое значение можно использовать как null или любое другое значение
    return null;
}
```

## OnNoGoZoneAdded(PatrolHelicopterAI,PatrolHelicopterAI.DangerZone)

### Summary


### Parameters
- `ai`: Объект-вертолет.
- `dangerZone`: Зона "Нет прохода".

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNoGoZoneAdded(PatrolHelicopterAI ai, DangerZone dangerZone)
{
    Puts("OnNoGoZoneAdded работает!");
    return null;
}
```

## OnDieselEngineToggle(DieselEngine,BasePlayer)

### Summary


### Parameters
- `engine`: Дизельный двигатель.
- `player`: Игрок, который включил/выключил двигатель.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDieselEngineToggle(DieselEngine engine, BasePlayer player)
{
    Puts("OnDieselEngineToggle работает!");
    return null;
}
```

## OnLootItem(BasePlayer,Item)

### Summary


### Parameters
- `player`: Игрок, который собирает предмет.
- `item`: Собираемый предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootItem(BasePlayer player, Item item)
{
    Puts("OnLootItem работает!");
    return null;
}
```

## OnPlanterBoxFertilize(PlanterBox)

### Summary


### Parameters
- `planterBox`: Плантер-бокс, который получил удобрение.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlanterBoxFertilize(PlanterBox planterBox)
{
    Puts("OnPlanterBoxFertilize работает!");
}
```

## OnPlayerTick(BasePlayer,PlayerTick,bool)

### Summary
Документация для метода `OnPlayerTick(BasePlayer, PlayerTick, bool)`

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnPlayerTick(BasePlayer, PlayerTick, bool)`

**Описание**

Метод `OnPlayerTick` вызывается при каждом тике игрока. Этот метод используется для обновления состояния игрока и выполнения различных задач.

**Параметры**

* `BasePlayer`: Объект игрока.
* `PlayerTick`: Объект, содержащий информацию о текущем тике игрока.
* `bool wasPlayerStalled`: Флаг, указывающий, был ли игрок заморожен в предыдущем тике.

**Возвращаемое значение**

Нет возвращаемого значения (void).

**Пример использования**

```csharp
public void OnPlayerTick(BasePlayer player, PlayerTick tick, bool wasStalled)
{
    // Код для обновления состояния игрока и выполнения задач
}
```

**Связанные методы**

* `OnReceiveTick`: Метод, вызываемый при каждом тике игрока.
* `UpdateActiveItem`: Метод, обновляющий активный предмет игрока.

**Примечания**

* Этот метод должен быть реализован в классе, который наследует от `BasePlayer`.
* В методе можно использовать различные переменные и функции из класса `BasePlayer` и других связанных классов.
```

## OnFishingStopped(BaseFishingRod,BaseFishingRod.FailReason)

### Summary


### Parameters
- `rod`: Рыболовная палка.
- `reason`: Причина остановки рыбалки.

### Returns
No return value.

### Example
```csharp
object OnFishingStopped(BaseFishingRod rod, FailReason reason)
{
    Puts("OnFishingStopped вызван!");
    return null;
}
```

## OnBoomboxStationUpdated(BoomBox,string,BasePlayer)

### Summary


### Parameters
- `boomBox`: Объект Boombox.
- `station`: Название радиостанции.
- `player`: Игрок, который изменил радиостанцию.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBoomboxStationUpdated(BoomBox boomBox, string station, BasePlayer player)
{
    Puts($"Радиостанция Boombox изменена на {station} для игрока {player.displayName}");
    return null;
}
```

## OnItemRemovedFromContainer(ItemContainer,Item)

### Summary


### Parameters
- `container`: Контейнер, из которого был удален предмет.
- `item`: Удаленный предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemRemovedFromContainer(ItemContainer container, Item item)
{
    Puts("OnItemRemovedFromContainer работает!");
    return null;
}
```

## OnMlrsFiringEnded(MLRS)

### Summary


### Parameters
- `mlrs`: Объект МЛРС.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMlrsFiringEnded(MLRS mlrs)
{
    Puts("Выстрел из МЛРС закончился!");
}
```

## IOnLoseCondition(Item,float)

### Summary


### Parameters
- `item`: Объект, у которого теряется условие.
- `amount`: Количество потерянного условия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object IOnLoseCondition(Item item, float amount)
{
    Puts("IOnLoseCondition работает!");
    return null;
}
```

## OnDroppedItemCombined(DroppedItem)

### Summary


### Parameters
- `di`: Объект DroppedItem.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDroppedItemCombined(DroppedItem di)
{
    Puts("OnDroppedItemCombined работает!");
}
```

## OnItemDropped(Item,BaseEntity)

### Summary


### Parameters
- `item`: Опускаемый предмет.
- `entity`: Сущность, к которой привязан предмет.

### Returns
No return value.

### Example
```csharp
object OnItemDropped(Item item, BaseEntity entity)
{
    Puts("OnItemDropped работает!");
    return null;
}
```

## OnPhoneDialFailed(PhoneController,Telephone.DialFailReason,BasePlayer)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `reason`: Причина неудачи.
- `player`: Игрок, пытавшийся вызвать по телефону.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPhoneDialFailed(PhoneController phoneController, Telephone.DialFailReason reason, BasePlayer player)
{
    Puts("OnPhoneDialFailed работает!");
    return null;
}
```

## IOnPlayerBanned(Network.Connection,AuthResponse)

### Summary


### Parameters
- `connection`: Информация о подключении игрока.
- `status`: Статус банного ответа от Steam.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void IOnPlayerBanned(Network.Connection connection, AuthResponse status)
{
    Puts($"Игрок {connection.username} забанен!");
}
```

## OnTick()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void OnTick()
{
    Puts("OnTick вызван!");
}
```

## OnPayForPlacement(BasePlayer,Planner,Construction)

### Summary


### Parameters
- `player`: Игрок, который оплачивает размещение.
- `planner`: Планировщик, с которым связана конструкция.
- `construction`: Конструкция, которую необходимо оплатить.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPayForPlacement(BasePlayer player, Planner planner, Construction construction)
{
    Puts("OnPayForPlacement работает!");
    return null;
}
```

## OnPlayerRecover(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, выздоровевший.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerRecover(BasePlayer player)
{
    Puts("OnPlayerRecover работает!");
    return null;
}
```

## CanBeAwardedAdventGift(AdventCalendar,BasePlayer)

### Summary


### Parameters
- `calendar`: Календарь advent.
- `player`: Игрок.

### Returns
Возвращает true, если игрок может получить подарок, и false в противном случае.

### Example
```csharp
bool CanBeAwardedAdventGift(AdventCalendar calendar, BasePlayer player)
{
    Puts("CanBeAwardedAdventGift вызван!");
    
    // Если ReturnType - bool, вернуть значение
    return true;
}
```

## OnTrapArm(BearTrap,BasePlayer)

### Summary


### Parameters
- `trap`: Ловушка.
- `player`: Игрок, который пытается запустить ловлю.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTrapArm(BearTrap trap, BasePlayer player)
{
    Puts("OnTrapArm работает!");
    return null;
}
```

## OnEntityEnter(TriggerComfort,BaseEntity)

### Summary


### Parameters
- `comfort`: Триггер комфорта.
- `entity`: Входящая сущность.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEntityEnter(TriggerComfort comfort, BaseEntity entity)
{
    Puts($"Сущность {entity} вошла в зону комфорта {comfort}");
}
```

## OnVehicleHornPressed(VehicleModuleSeating,BasePlayer)

### Summary


### Parameters
- `module`: Модуль сидения транспортного средства.
- `player`: Игрок, который нажал клаксон.

### Returns
No return value.

### Example
```csharp
object OnVehicleHornPressed(VehicleModuleSeating module, BasePlayer player)
{
    Puts("Клаксон транспортного средства был нажат!");
    return null;
}
```

## OnConnectionQueue(Network.Connection)

### Summary


### Parameters
- `connection`: Объект соединения.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnConnectionQueue(Network.Connection connection)
{
    Puts("OnConnectionQueue работает!");
    return null;
}
```

## OnProjectileRicochet(BasePlayer,ProtoBuf.PlayerProjectileRicochet)

### Summary


### Parameters
- `player`: Игрок, который запустил снаряд.
- `ricochetData`: Данные о столкновении снаряда.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnProjectileRicochet(BasePlayer player, ProtoBuf.PlayerProjectileRicochet ricochetData)
{
    Puts("OnProjectileRicochet работает!");
    return null;
}
```

## OnEntityPickedUp(BaseCombatEntity,Item,BasePlayer)

### Summary


### Parameters
- `entity`: Поднятая сущность.
- `item`: Предмет, который был поднят.
- `player`: Игрок, который поднял сущность.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityPickedUp(BaseCombatEntity entity, Item item, BasePlayer player)
{
    Puts("OnEntityPickedUp работает!");
    return null;
}
```

## OnNpcConversationResponded(NPCTalking,BasePlayer,ConversationData,ConversationData.ResponseNode)

### Summary


### Parameters
- `npc`: НПЦ, с которым происходит диалог.
- `player`: Игрок, ответивший на диалог.
- `conversationData`: Данные о текущем диалоге.
- `responseNode`: Нод ответа, по которой игрок ответил.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcConversationResponded(NPCTalking npc, BasePlayer player, ConversationData conversationData, ConversationData.ResponseNode responseNode)
{
    Puts("OnNpcConversationResponded работает!");
    return null;
}
```

## OnWorldProjectileCreate(HitInfo,Item)

### Summary


### Parameters
- `info`: Информация о выстреле.
- `item`: Снаряд.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnWorldProjectileCreate(HitInfo info, Item item)
{
    Puts("OnWorldProjectileCreate работает!");
}
```

## OnCrateLanded(HackableLockedCrate)

### Summary


### Parameters
- `crate`: Контейнер, приземлившийся.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCrateLanded(HackableLockedCrate crate)
{
    Puts("Контейнер приземлился!");
}
```

## OnExplosiveFuseSet(TimedExplosive,float)

### Summary


### Parameters
- `explosive`: Взрывное устройство.
- `fuseLength`: Длина заряда.

### Returns
Возвращает значение fuseLength, если поведение по умолчанию переопределено.

### Example
```csharp
object OnExplosiveFuseSet(TimedExplosive explosive, float fuseLength)
{
    Puts("OnExplosiveFuseSet работает!");
    return null;
}
```

## CanEquipItem(PlayerInventory,Item,int)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `item`: Предмет, который хочет одеть игрок.
- `slot`: Номер слота, в который хотят одеть предмет.

### Returns
Возвращает true, если предмет можно одеть, и false в противном случае.

### Example
```csharp
bool CanEquipItem(PlayerInventory inventory, Item item, int slot)
{
    Puts("CanEquipItem вызван!");
    
    // Если возвращаемое значение не равно null, то метод переопределил поведение по умолчанию
    object obj = Interface.CallHook("CanEquipItem", inventory, item, slot);
    if (obj is bool)
    {
        return (bool)obj;
    }
    
    // Если предмет запрещен в поясе, то он не может быть одет
    if ((item.info.flags & ItemDefinition.Flag.NotAllowedInBelt) != 0)
    {
        return false;
    }
    
    // Если игрок привязан и в его поясе есть предмет-ограничитель, то он не может одеть этот предмет
    if (base.baseEntity != null && base.baseEntity.IsRestrained)
    {
        Handcuffs restraintItem = base.baseEntity.Belt.GetRestraintItem();
        if (restraintItem != null && restraintItem.GetItem().position == slot)
        {
            return false;
        }
    }
    
    // Если предмет имеет модификатор контейнера, то проверяем, можно ли его одеть
    ItemModContainerRestriction component = item.info.GetComponent<ItemModContainerRestriction>();
    if (component != null)
    {
        // Проверяем, есть ли в поясе другой предмет с таким же модификатором контейнера
        Item[] array = inventory.itemList.ToArray();
        foreach (Item item2 in array)
        {
            if (item2 != item)
            {
                ItemModContainerRestriction component2 = item2.info.GetComponent<ItemModContainerRestriction>();
                if (!(component2 == null) && !component.CanExistWith(component2) && !item2.MoveToContainer(inventory.main))
                {
                    // Если да, то выкидываем этот предмет из пояса
                    item2.Drop(base.baseEntity.GetDropPosition(), base.baseEntity.GetDropVelocity());
                }
            }
        }
    }
    
    return true;
}
```

## OnRackedWeaponMounted(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Закрепленное оружие.
- `player`: Игрок, который закрепил оружие.
- `rack`: Станок, на котором закреплено оружие.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponMounted(Item item, BasePlayer player, WeaponRack rack)
{
    Puts($"Оружие {item.info.itemid} закреплено на станке {rack}");
}

```

## CanLootEntity(BasePlayer,ResourceContainer)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть контейнер.
- `container`: Контейнер, который нужно открыть.

### Returns
Возвращает true, если игрок может открыть контейнер, и false в противном случае.

### Example
```csharp
bool CanLootEntity(BasePlayer player, ResourceContainer container)
{
    Puts("CanLootEntity работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true;
}
```

## InitLogging()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void InitLogging()
{
    Puts("Инициализация логирования...");
}
```

## OnPlayerColliderEnable(BasePlayer,UnityEngine.CapsuleCollider)

### Summary


### Parameters
- `player`: Игрок, у которого включается коллайдер.
- `collider`: Коллайдер игрока.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerColliderEnable(BasePlayer player, UnityEngine.CapsuleCollider collider)
{
    Puts("OnPlayerColliderEnable работает!");
    return null;
}
```

## OnNpcAttack(BaseNpc,BaseEntity)

### Summary


### Parameters
- `npc`: НПС, который совершает атаку.
- `target`: Цель атаки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcAttack(BaseNpc npc, BaseEntity target)
{
    Puts("OnNpcAttack работает!");
    return null;
}
```

## OnClientAuth(Network.Connection)

### Summary


### Parameters
- `connection`: Информация о подключении клиента.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnClientAuth(Network.Connection connection)
{
    // Минимальный код для демонстрации функциональности
    DebugEx.Log("Клиент аутентифицирован: " + connection.ToString());
}
```

## OnInventoryItemsFind(PlayerInventory,int)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `id`: ID предмета для поиска.

### Returns
Список найденных предметов или null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnInventoryItemsFind(PlayerInventory inventory, int id)
{
    Puts("OnInventoryItemsFind вызван!");
    // Если возвращаемое значение не null, то метод переопределен и возвращает его
    return null;
}
```

## OnNpcConversationEnded(NPCTalking,BasePlayer)

### Summary


### Parameters
- `npc`: NPC, с которым была проведена конверсация.
- `player`: Игрок, который закончил конверсацию.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcConversationEnded(NPCTalking npc, BasePlayer player)
{
    Puts("OnNpcConversationEnded работает!");
    return null;
}
```

## OnResourceDepositCreated(ResourceDepositManager.ResourceDeposit)

### Summary
Документация для OnResourceDepositCreated(ResourceDepositManager.ResourceDeposit)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для OnResourceDepositCreated(ResourceDepositManager.ResourceDeposit)

**Описание хука**

Хук `OnResourceDepositCreated` вызывается после создания нового ресурсного депозита на позиции, указанной в методе `CreateFromPosition(Vector3 pos)`. Этот хук позволяет модифицировать или расширить поведение создания ресурсных депозитов.

**Параметры**

* `resourceDeposit`: Объект типа `ResourceDeposit`, который был создан и добавлен в коллекцию `deposits`.

**Пример использования**

Например, вы можете использовать этот хук для изменения вероятности появления определенных типов ресурсов или для добавления дополнительных ресурсов к депозиту.

```csharp
public class MyResourceDepositModifier : MonoBehaviour
{
    public void OnResourceDepositCreated(ResourceDeposit resourceDeposit)
    {
        // Изменить вероятность появления определенного типа ресурса
        if (resourceDeposit.GetItemDefinition().Name == "stones")
        {
            resourceDeposit.SetSpawnProbability(0.8f);
        }

        // Добавить дополнительный ресурс к депозиту
        resourceDeposit.Add(ItemManager.FindItemDefinition("gold"), 1f, 10000, 10f, ResourceDeposit.surveySpawnType.ITEM);
    }
}
```

**Примечания**

* Этот хук вызывается после добавления ресурсного депозита в коллекцию `deposits`, поэтому вы можете использовать его для изменения или расширения поведения создания ресурсных депозитов.
* Вы можете использовать этот хук для различных целей, таких как изменение вероятности появления определенных типов ресурсов или добавление дополнительных ресурсов к депозиту.
```

## OnHuntEventEnd(EggHuntEvent)

### Summary


### Parameters
- `event`: Событие охоты.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object OnHuntEventEnd(EggHuntEvent event)
{
    Puts("OnHuntEventEnd работает!");
    return null;
}
```

## OnItemRepair(BasePlayer,Item)

### Summary
Документация для OnItemRepair(BasePlayer, Item):

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для OnItemRepair(BasePlayer, Item):

**Название:** OnItemRepair

**Описание:** Этот хук вызывается перед тем, как предмет будет отремонтирован. Он позволяет модификациям и плагинам изменить поведение процесса ремонта.

**Параметры:**

* `BasePlayer player`: Игрок, который выполняет ремонт.
* `Item itemToRepair`: Предмет, который необходимо отремонтировать.

**Возвращаемое значение:** null (хук не возвращает никаких значений)

**Пример использования:**
```csharp
public static void OnItemRepair(BasePlayer player, Item item)
{
    // Код для модификации или плагина
}
```
**Примечание:** Этот хук вызывается только перед тем, как предмет будет отремонтирован. Если процесс ремонта прерван или отменен, этот хук не будет вызван.

**Структура метода:**
```csharp
public static void OnItemRepair(BasePlayer player, Item item)
{
    // Код для модификации или плагина
}
```
В этом примере метод `OnItemRepair` принимает два параметра: `player` и `item`. Метод не возвращает никаких значений.
```

## OnSignContentCopied(SignContent,ISignage,IUGCBrowserEntity)

### Summary


### Parameters
- `signContent`: Копируемое содержимое.
- `signage`: Знак, на который было скопировано содержимое.
- `browserEntity`: Энтити браузера, с помощью которого была выполнена операция копирования.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSignContentCopied(SignContent signContent, ISignage signage, IUGCBrowserEntity browserEntity)
{
    Puts("OnSignContentCopied работает!");
}
```

## OnRackedWeaponTake(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Вынутое оружие.
- `player`: Игрок, который вынимает оружие.
- `rack`: Ячейка, из которой вынимается оружие.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRackedWeaponTake(Item item, BasePlayer player, WeaponRack rack)
{
    Puts("OnRackedWeaponTake работает!");
    return null;
}
```

## OnBookmarkControlStarted(ComputerStation,BasePlayer,string,IRemoteControllable)

### Summary


### Parameters
- `computerStation`: Компьютерная станция.
- `player`: Игрок.
- `bookmarkName`: Название закладки.
- `remoteControllable`: Объект, управляемый игроком.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarkControlStarted(ComputerStation computerStation, BasePlayer player, string bookmarkName, IRemoteControllable remoteControllable)
{
    Puts("OnBookmarkControlStarted работает!");
    return null;
}
```

## OnPlayerWound(BasePlayer,HitInfo)

### Summary


### Parameters
- `player`: Игрок, получивший повреждение.
- `hitInfo`: Информация о повреждении.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerWound(BasePlayer player, HitInfo hitInfo)
{
    Puts("OnPlayerWound работает!");
    return null;
}
```

## CanWearItem(PlayerInventory,Item,int)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `item`: Предмет, который хочет надеть игрок.
- `slot`: Номер слота в инвентаре, куда хотят надеть предмет.

### Returns
Возвращает true, если предмет можно надеть, и false в противном случае.

### Example
```csharp
bool CanWearItem(PlayerInventory inventory, Item item, int slot)
{
    Puts("CanWearItem работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## CanDropActiveItem(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, пытающийся сбросить активный предмет.

### Returns
Возвращает true, если можно сбросить активный предмет, и false в противном случае.

### Example
```csharp
bool CanDropActiveItem(BasePlayer player)
{
    Puts("CanDropActiveItem работает!");
    return true;
}
```

## OnBookmarkAdd(ComputerStation,BasePlayer,string)

### Summary


### Parameters
- `station`: Компьютерная станция, на которой была добавлена закладка.
- `player`: Игрок, который добавил закладку.
- `bookmarkName`: Название добавленной закладки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarkAdd(ComputerStation station, BasePlayer player, string bookmarkName)
{
    Puts("OnBookmarkAdd вызван!");
    return null;
}
```

## OnVendingShopRename(VendingMachine,string,BasePlayer)

### Summary


### Parameters
- `vendingMachine`: Объект автомата.
- `newName`: Новое название.
- `player`: Игрок, который изменил название.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVendingShopRename(VendingMachine vendingMachine, string newName, BasePlayer player)
{
    Puts("OnVendingShopRename работает!");
    return null;
}
```

## OnSignUpdated(PhotoFrame,BasePlayer)

### Summary


### Parameters
- `sign`: Объект знака.
- `player`: Игрок, который обновил знак.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSignUpdated(PhotoFrame sign, BasePlayer player)
{
    Puts($"Знак обновлен игроком {player.UserIDString}.");
}
```

## OnPhoneCallStart(PhoneController,PhoneController,BasePlayer)

### Summary


### Parameters
- `caller`: Контроллер телефона вызывающего.
- `receiver`: Контроллер телефона принимающего.
- `player`: Игрок, участвующий в вызове.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhoneCallStart(PhoneController caller, PhoneController receiver, BasePlayer player)
{
    Puts("OnPhoneCallStart работает!");
}
```

## CanBradleyApcTarget(BradleyAPC,BaseEntity)

### Summary


### Parameters
- `apc`: Bradley APC.
- `target`: Цель.

### Returns
Возвращает true, если цель доступна для цели Bradley APC, и false в противном случае.

### Example
```csharp
object CanBradleyApcTarget(BradleyAPC apc, BaseEntity target)
{
    Puts("CanBradleyApcTarget работает!");
    return null;
}
```

## CanDesignFirework(BasePlayer,PatternFirework)

### Summary


### Parameters
- `player`: Игрок, пытающийся изменить дизайн.
- `firework`: Фейерверк, который нужно изменить.

### Returns
Возвращает true, если игрок может изменить дизайн фейерверка, и false в противном случае.

### Example
```csharp
bool CanDesignFirework(BasePlayer player, PatternFirework firework)
{
    Puts("CanDesignFirework работает!");
    return true;
}
```

## OnDispenserGather(ResourceDispenser,BasePlayer,Item)

### Summary


### Parameters
- `dispenser`: Диспенсер, из которого собран ресурс.
- `player`: Игрок, который собрал ресурс.
- `item`: Собранный ресурс.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDispenserGather(ResourceDispenser dispenser, BasePlayer player, Item item)
{
    Puts($"Ресурс {item.info.shortname} собран игроком {player.UserIDString} из диспенсера {dispenser.EntityID}");
}
```

## OnElevatorMove(Elevator,int)

### Summary


### Parameters
- `elevator`: Лифт, который перемещается.
- `targetFloor`: Целевой этаж.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnElevatorMove(Elevator elevator, int targetFloor)
{
    Puts("OnElevatorMove работает!");
    return null;
}
```

## OnEngineStatsRefreshed(VehicleModuleEngine,Rust.Modular.EngineStorage)

### Summary


### Parameters
- `engine`: Двигатель.
- `storage`: Хранилище данных о двигателе.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEngineStatsRefreshed(VehicleModuleEngine engine, Rust.Modular.EngineStorage storage)
{
    Puts("OnEngineStatsRefreshed работает!");
    return null;
}
```

## OnPlayerVoice(BasePlayer,byte[])

### Summary


### Parameters
- `player`: Игрок, отправивший голосовую информацию.
- `data`: Голосовая информация в виде байтового массива.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerVoice(BasePlayer player, byte[] data)
{
    Puts("OnPlayerVoice вызван!");
}
```

## OnTurretClearList(BaseEntity.RPCMessage)

### Summary


### Parameters
- `rpc`: RPC-сообщение, содержащее информацию о вызывающем игроке.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTurretClearList(BaseEntity.RPCMessage rpc)
{
    Puts("OnTurretClearList работает!");
}
```

## OnStructureRotate(BuildingBlock,BasePlayer)

### Summary


### Parameters
- `block`: Текущий блок.
- `player`: Игрок, который выполнил поворот.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnStructureRotate(BuildingBlock block, BasePlayer player)
{
    Puts("OnStructureRotate работает!");
}
```

## OnCargoShipSpawnCrate(CargoShip)

### Summary


### Parameters
- `cargoShip`: Контейнер с грузом.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCargoShipSpawnCrate(CargoShip cargoShip)
{
    Puts("OnCargoShipSpawnCrate работает!");
}
```

## OnNpcEquipWeapon(NPCPlayer,Item)

### Summary


### Parameters
- `npc`: NPC player.
- `item`: Item to equip.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcEquipWeapon(NPCPlayer npc, Item item)
{
    Puts("OnNpcEquipWeapon работает!");
    return null;
}
```

## OnExcavatorGather(ExcavatorArm,Item)

### Summary


### Parameters
- `excavatorArm`: Экскаваторная рука, которая собрала ресурсы.
- `item`: Собранный ресурс.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnExcavatorGather(ExcavatorArm excavatorArm, Item item)
{
    Puts("OnExcavatorGather работает!");
    return null;
}
```

## CanSpectateTarget(BasePlayer,string)

### Summary


### Parameters
- `player`: Игрок, который хочет посмотреть.
- `targetName`: Название объекта, который хотят посмотреть.

### Returns
Возвращает true, если игрок может посмотреть на объект, и false в противном случае.

### Example
```csharp
bool CanSpectateTarget(BasePlayer player, string targetName)
{
    Puts("CanSpectateTarget работает!");
    // Здесь можно добавить дополнительную логическую проверку или обработку
    return true; // Возвращаем true, если игрок может посмотреть на объект
}
```

## OnShopCancelClick(ShopFront,BasePlayer)

### Summary


### Parameters
- `shopFront`: Объект магазина.
- `player`: Игрок, который нажал кнопку отмены.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnShopCancelClick(ShopFront shopFront, BasePlayer player)
{
    Puts("OnShopCancelClick работает!");
    return null;
}
```

## OnShopCompleteTrade(ShopFront)

### Summary


### Parameters
- `shopFront`: Фронт магазина.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnShopCompleteTrade(ShopFront shopFront)
{
    Puts("Торговая сделка завершена!");
}
```

## OnLootEntityEnd(BasePlayer,ItemBasedFlowRestrictor)

### Summary


### Parameters
- `player`: Игрок, который закончил лутить.
- `restrictor`: Объект, с которым игрок закончил лутить.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootEntityEnd(BasePlayer player, ItemBasedFlowRestrictor restrictor)
{
    Puts("OnLootEntityEnd работает!");
    return null;
}
```

## OnPlayerCorpseSpawn(BasePlayer)

### Summary
Документация для метода `OnPlayerCorpseSpawn(BasePlayer)`:

### Parameters
- `player`: Игрок, чье тело было создано.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnPlayerCorpseSpawn(BasePlayer)`:

```rust
void OnPlayerCorpseSpawn(BasePlayer player)
{
    // Метод не возвращает никаких значений
}
```

Этот метод вызывается в методе `CreateCorpse` класса `BasePlayer`, когда тело игрока создаётся после его смерти. Он позволяет другим модулям или плагинам отменить создание тела игрока, если необходимо.

Пример использования:

```rust
public class MyPlugin : MonoBehaviour
{
    void Start()
    {
        // Отменяем создание тела игрока при его смерти
        BasePlayer.player.OnPlayerCorpseSpawn += (player) => { return null; };
    }
}
```

В этом примере мы отменяем создание тела игрока, если он умирает. Это можно использовать для различных целей, например, для создания специальных эффектов или для изменения поведения игрока после его смерти.
```

## OnTechTreeNodeUnlock(Workbench,TechTreeData.NodeInstance,BasePlayer)

### Summary


### Parameters
- `workbench`: Рабочая столы игрока.
- `nodeInstance`: Объект узла, который был разблокирован.
- `player`: Игрок, который разблокировал узел.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTechTreeNodeUnlock(Workbench workbench, TechTreeData.NodeInstance nodeInstance, BasePlayer player)
{
    Puts($"Узел {nodeInstance.groupName} разблокирован игроком {player.UserIDString}");
}
```

## OnBedMade(SleepingBag,BasePlayer)

### Summary


### Parameters
- `sleepingBag`: Снаряжение для сна.
- `player`: Игрок, который создал кровать.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBedMade(SleepingBag sleepingBag, BasePlayer player)
{
    Puts("Кровать создана!");
}
```

## OnEngineStart(MotorRowboat,BasePlayer)

### Summary


### Parameters
- `boat`: Лодка.
- `driver`: Водитель.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEngineStart(MotorRowboat boat, BasePlayer driver)
{
    Puts("Двигатель включен!");
}
```

## OnVendingTransaction(VendingMachine,BasePlayer,int,int,ItemContainer)

### Summary
This is a C# method that appears to be part of a vending machine system in the game Rust. The method, `TryBuyFromVendingMachine`, attempts to purchase an item from a vending machine using a specified currency.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of a vending machine system in the game Rust. The method, `TryBuyFromVendingMachine`, attempts to purchase an item from a vending machine using a specified currency.

Here's a breakdown of what the method does:

1. It checks if the sell order ID is valid and within range.
2. It ensures that the buyer is close enough to the vending machine (within 4 units).
3. It calls a hook function `OnVendingTransaction` to allow for custom behavior or modifications.
4. If the hook function returns false, it immediately returns false.
5. It retrieves the sell order associated with the specified ID and creates a list of items to be sold.
6. It checks if there are enough items in stock to fulfill the purchase request.
7. It calculates the total price for the purchase based on the number of transactions and the item's price multiplier.
8. If there is not enough currency available, it returns false.
9. It takes the required amount of currency from the buyer's inventory.
10. It records sale analytics using `RecordSaleAnalytics`.
11. It gives the purchased item to the buyer or moves it to a target container if specified.
12. Finally, it updates an empty flag and returns true.

The method uses various hooks and callbacks to allow for custom behavior and modifications, which is typical in game development where modding is encouraged.

Here's a simplified version of the code with some comments added:

```csharp
public bool TryBuyFromVendingMachine(BasePlayer buyer, int sellOrderId, int numberOfTransactions, Container targetContainer = null)
{
    // Check if sell order ID is valid and within range
    if (sellOrderId < 0 || sellOrderId >= sellOrders.sellOrders.Count) return false;

    // Ensure buyer is close enough to vending machine
    if (targetContainer == null && Vector3.Distance(buyer.transform.position, base.transform.position) > 4f) return false;

    // Call hook function to allow for custom behavior or modifications
    object obj = Interface.CallHook("OnVendingTransaction", this, buyer, sellOrderId, numberOfTransactions, targetContainer);
    if (obj is bool && !(bool)obj) return false;

    // Retrieve sell order and create list of items to be sold
    ProtoBuf.VendingMachine.SellOrder sellOrder = sellOrders.sellOrders[sellOrderId];
    List<Item> obj2 = Facepunch.Pool.GetList<Item>();
    GetItemsToSell(sellOrder, obj2);

    // Check if there are enough items in stock to fulfill purchase request
    if (obj2 == null || obj2.Count == 0) return false;

    // Calculate total price for purchase based on number of transactions and item's price multiplier
    int num = sellOrder.itemToSellAmount * numberOfTransactions;
    int num2 = obj2.Sum((Item x) => x.amount);
    if (num > num2) return false;

    // Take required amount of currency from buyer's inventory
    List<Item> source = buyer.inventory.FindItemsByItemID(sellOrder.currencyID);
    if (sellOrder.currencyIsBP)
    {
        source = (from x in buyer.inventory.FindItemsByItemID(blueprintBaseDef.itemid)
            where x.blueprintTarget == sellOrder.currencyID
            select x).ToList();
    }
    source = (from x in source
        where !x.hasCondition || (x.conditionNormalized >= 0.5f && x.maxConditionNormalized > 0.5f)
        where x.GetItemVolume() <= maxCurrencyVolume
        select x).ToList();

    // Check if there is not enough currency available
    int num3 = source.Sum((Item x) => x.amount);
    int num4 = GetTotalPriceForOrder(sellOrder) * numberOfTransactions;
    if (num3 < num4) return false;

    // Record sale analytics using RecordSaleAnalytics
    transactionActive = true;
    int num5 = 0;
    foreach (Item item3 in source)
    {
        int num6 = Mathf.Min(num4 - num5, item3.amount);
        Item item = ((item3.amount > num6) ? item3.SplitItem(num6) : item3);
        TakeCurrencyItem(item);
        onCurrencyRemoved?.Invoke(buyer, item);
        num5 += num6;
        if (num5 >= num4) break;
    }

    // Give purchased item to buyer or move it to target container
    int num7 = 0;
    foreach (Item item4 in obj2)
    {
        int num8 = num - num7;
        Item item2 = ((item4.amount > num8) ? item4.SplitItem(num8) : item4);
        if (item2 == null) PutsError("Vending machine error, contact developers!");
        else
        {
            num7 += item2.amount;
            // Give purchased item to buyer or move it to target container
            if (targetContainer != null)
                targetContainer.Add(item2);
            else
                buyer.inventory.Add(item2);
        }
    }

    // Update empty flag and return true
    updateEmptyFlag();
    return true;
}
```
```

## OnClientCommand(Network.Connection,string)

### Summary
**OnClientCommand(Network.Connection, string)**

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
**OnClientCommand(Network.Connection, string)**

### Описание

Хук `OnClientCommand` вызывается на стороне сервера при получении команды от клиента. Этот хук позволяет модифицировать или расширить поведение сервера в ответ на команду клиента.

### Параметры

*   `connection`: Объект `Network.Connection`, представляющий соединение с клиентом, который отправил команду.
*   `text`: Строка, содержащая текст команды клиента.

### Возвращаемое значение

Хук возвращает `null` по умолчанию. Если хук переопределен, он должен вернуть значение, которое будет использовано сервером для обработки команды.

### Пример использования

```csharp
void OnClientCommand(Network.Connection connection, string text)
{
    // Код для модификации или расширения поведения сервера в ответ на команду клиента.
}
```

### Документация по примерам

В следующем примере мы создаем хук `OnClientCommand`, который проверяет, является ли текст команды клиента равным "ping". Если это так, он отправляет ответ клиенту с текстом "pong".

```csharp
void OnClientCommand(Network.Connection connection, string text)
{
    if (text == "ping")
    {
        SendClientReply(connection, "pong");
    }
}
```

### Документация по минимальному коду

Минимальный код для демонстрации функциональности хука `OnClientCommand` может быть следующим:

```csharp
void OnClientCommand(Network.Connection connection, string text)
{
    Puts($"Received client command: {text}");
}
```

Этот код просто выводит в консоль текст команды клиента.
```

## OnResearchCostDetermine(ItemDefinition)

### Summary
**OnResearchCostDetermine(ItemDefinition)**

### Parameters
- `info`: Объект, содержащий информацию о предмете.

### Returns
Возвращает целочисленное значение, представляющее затраты исследования предмета.

### Example
```csharp
**OnResearchCostDetermine(ItemDefinition)**

### Описание

Этот хук вызывается для определения затрат исследования предмета.

### Параметры

* `ItemDefinition info`: Объект, содержащий информацию о предмете.

### Возвращаемое значение

Возвращает целочисленное значение, представляющее затраты исследования предмета. Если хук не переопределен, возвращается 0.

### Пример использования

```csharp
public static int ScrapForResearch(ItemDefinition info)
{
    object obj = Interface.CallHook("OnResearchCostDetermine", info);
    if (obj is int)
    {
        return (int)obj;
    }
    // ...
}
```

### Структура метода

```csharp
int OnResearchCostDetermine(ItemDefinition info)
{
    // Минимальный код для демонстрации функциональности
    return 0;
}
```

### Примечания

* Если хук не переопределен, возвращается 0.
* В методе можно добавить дополнительную логику для определения затрат исследования предмета.
```

## OnPlayerSleep(BasePlayer)

### Summary
**Документация для метода OnPlayerSleep**

### Parameters
- `player`: Игрок, который начинает спать.

### Returns
No return value.

### Example
```csharp
**Документация для метода OnPlayerSleep**

### Описание

Метод `OnPlayerSleep` вызывается, когда игрок начинает спать.

### Параметры

* `BasePlayer player`: Игрок, который начинает спать.

### Возвращаемое значение

Нет возвращаемого значения.

### Код

```csharp
void OnPlayerSleep(BasePlayer player)
{
    Puts("Игрок начал спать!");
}
```

### Примечания

Этот метод вызывается в методе `StartSleeping`, когда игрок начинает спать. В этом методе можно добавить логирование или другие действия, которые необходимо выполнить при начале сна игрока.

### Пример использования

```csharp
public void StartSleeping()
{
    // ...
    Interface.CallHook("OnPlayerSleep", this);
    // ...
}
```

В этом примере метод `StartSleeping` вызывает метод `OnPlayerSleep`, передавая в него текущего игрока.
```

## OnXmasLootDistribute(XMasRefill)

### Summary
**Документация метода OnXmasLootDistribute**

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
**Документация метода OnXmasLootDistribute**

**Описание:**
Метод `OnXmasLootDistribute` вызывается в контексте серверной инициализации при условии активации Xmas-режима. Этот хук предназначен для распределения лута на Рождество.

**Параметры:**

* `XMasRefill`: Объект, представляющий текущий Xmas-режим.

**Возвращаемое значение:**
Нет поведения возвращаемого значения. Метод не возвращает никаких значений.

**Код метода:**
```csharp
void OnXmasLootDistribute(XMasRefill refill)
{
    // Минимальный код для демонстрации функциональности
    Puts("OnXmasLootDistribute вызван!");
}
```
**Примечания:**

* Метод не имеет оператора `return`, поскольку он не возвращает никаких значений.
* Код метода минимален и предназначен только для демонстрации функциональности.

**Пример использования:**
```csharp
public override void ServerInit()
{
    // ...
    if (Interface.CallHook("OnXmasLootDistribute", this) == null)
    {
        InvokeRepeating(DistributeLoot, 3f, 0.02f);
        Invoke(SendBells, 0.5f);
    }
}
```
В этом примере метод `OnXmasLootDistribute` вызывается в контексте серверной инициализации, а если он не сработает, то будет запущен повторяющийся вызов метода `DistributeLoot` каждые 3 секунды.
```

## OnItemStacked(Item,Item,ItemContainer,int)

### Summary
This is a C# method that appears to be part of an item management system in a game. It's responsible for moving an item from one container to another. Here's a breakdown of the code:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of an item management system in a game. It's responsible for moving an item from one container to another. Here's a breakdown of the code:

**Method signature**

The method takes several parameters:

* `ItemContainer newcontainer`: The destination container.
* `int iTargetPos`: The position within the destination container where the item should be placed.
* `bool allowStack`: Whether the item can be stacked with existing items in the destination container.
* `bool ignoreStackLimit`: Whether to ignore the maximum stack size of the destination container.
* `BasePlayer sourcePlayer`: The player who initiated the move.

**Method body**

The method first checks if the destination container is the same as the current parent container. If so, it simply updates the item's position within that container and returns true.

Next, it checks if the destination container has a maximum stack size and if the item's amount exceeds that limit. If so, it splits the item into multiple items with the maximum stack size and attempts to move each one separately.

If the item can be moved to the destination container without splitting, it removes the item from its current container, updates the item's position within the new container, and returns true.

Finally, if all else fails, it drops the item at the destination container's drop position with a velocity of 0 (i.e., it simply disappears).

**Hooks**

The method calls two hooks:

* `OnItemStacked`: This hook is called when an item is stacked with existing items in the destination container.
* `OnItemMoved`: This hook is not explicitly called, but it's likely used elsewhere in the code to notify other components of the item move.

Overall, this method appears to be responsible for moving items between containers while handling stacking and splitting logic.
```

## OnCargoShipHarborArrived(CargoShip)

### Summary


### Parameters
- `cargoShip`: Корабль с грузом.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCargoShipHarborArrived(CargoShip cargoShip)
{
    Puts("OnCargoShipHarborArrived работает!");
}
```

## OnPhoneAnswered(PhoneController,PhoneController)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `activeCallTo`: Активный вызов.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhoneAnswered(PhoneController phoneController, PhoneController activeCallTo)
{
    Puts("OnPhoneAnswered работает!");
}

В этом методе нет оператора return, что указывает на то, что тип возвращаемого значения равен void.
```

## IOnRconInitialize()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void IOnRconInitialize()
{
    // Минимальный код для демонстрации функциональности
    Puts("IOnRconInitialize вызван!");
}
```

## CanUseHBHFSensor(BasePlayer,HBHFSensor)

### Summary


### Parameters
- `player`: Игрок, пытающийся использовать датчик.
- `sensor`: Датчик HBHF.

### Returns
Возвращает true, если игрок может использовать датчик, и false в противном случае.

### Example
```csharp
bool CanUseHBHFSensor(BasePlayer player, HBHFSensor sensor)
{
    Puts("CanUseHBHFSensor работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnTeamCreate(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, который создает команду.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamCreate(BasePlayer player)
{
    Puts("OnTeamCreate работает!");
    return null;
}
```

## OnRocketLaunched(BasePlayer,BaseEntity)

### Summary
Документация для хука `OnRocketLaunched`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для хука `OnRocketLaunched`:

**Описание:**

Хук `OnRocketLaunched` вызывается после запуска ракеты из оружия. Он позволяет модификаторам и плагинам реагировать на запуск ракеты.

**Сигнатура:**

`void OnRocketLaunched(BasePlayer player, BaseEntity baseEntity)`

**Аргументы:**

* `player`: Игрок, который запустил ракету.
* `baseEntity`: Объект-ракета, который был запущен.

**Описание функции:**

Функция не возвращает никаких значений. Ее цель - вызвать хуки и события, связанные с запуском ракеты.

**Пример использования:**

```csharp
void MyPlugin_OnRocketLaunched(BasePlayer player, BaseEntity baseEntity)
{
    // Реагируйте на запуск ракеты здесь
}
```

**Нотация:**

Хук `OnRocketLaunched` вызывается в методе `SV_Launch`, который является частью серверной логики игры.
```

## OnHorseHitch(RidableHorse,HitchTrough.HitchSpot)

### Summary


### Parameters
- `horse`: Лошадь, которую необходимо привязать.
- `hitchSpot`: Место для привязки.

### Returns
Возвращает true, если привязка прошла успешно, и false в противном случае.

### Example
```csharp
bool OnHorseHitch(RidableHorse horse, HitchTrough.HitchSpot hitchSpot)
{
    Puts("OnHorseHitch вызван!");
    // Здесь можно добавить дополнительную логическую или физическую логику для привязки лошади
    return true;
}
```

## OnCoalingTowerGather(CoalingTower,Item)

### Summary


### Parameters
- `coalingTower`: Коалинг-тауэр.
- `item`: Собираемый предмет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
void OnCoalingTowerGather(CoalingTower coalingTower, Item item)
{
    // Минимальный код для демонстрации функциональности
    return;
}
```

## OnBookmarkControl(ComputerStation,BasePlayer,string,IRemoteControllable)

### Summary


### Parameters
- `computerStation`: Компьютерная станция.
- `player`: Игрок, управляющий закладкой.
- `bookmarkName`: Название закладки.
- `remoteControllable`: Объект, который можно контролировать.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarkControl(ComputerStation computerStation, BasePlayer player, string bookmarkName, IRemoteControllable remoteControllable)
{
    Puts("OnBookmarkControl работает!");
    return null;
}
```

## OnCollectiblePickedup(CollectibleEntity,BasePlayer,Item)

### Summary


### Parameters
- `entity`: Коллективный предмет.
- `player`: Игрок, который собрал предмет.
- `item`: Собранный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCollectiblePickedup(CollectibleEntity entity, BasePlayer player, Item item)
{
    Puts($"Коллективный предмет {entity} собран игроком {player} с предметом {item}");
}
```

## CanAssignBed(BasePlayer,SleepingBag,ulong)

### Summary


### Parameters
- `player`: Игрок, который пытается присвоить спальное место.
- `sleepingBag`: Спальное место, которое нужно присвоить.
- `targetID`: ID цели.

### Returns
Возвращает результат присвоения спального места. Если null, то присвоение не удалось.

### Example
```csharp
object CanAssignBed(BasePlayer player, SleepingBag sleepingBag, ulong targetID)
{
    Puts("CanAssignBed работает!");
    // Код для демонстрации функциональности
    return null;
}
```

## CanSwapToSeat(BasePlayer,BaseMountable)

### Summary


### Parameters
- `player`: Игрок, пытающийся сменить место.
- `entity`: Сущность, на которую хотят сменить место.

### Returns
Возвращает true, если поведение по умолчанию не переопределено; иначе возвращает значение, указанное в вызывающем методе.

### Example
```csharp
object CanSwapToSeat(BasePlayer player, BaseMountable entity)
{
    Puts("CanSwapToSeat работает!");
    return null;
}
```

## OnEntityDestroy(BradleyAPC)

### Summary
Документация для метода `OnEntityDestroy(BradleyAPC)`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnEntityDestroy(BradleyAPC)`:

**Описание:**

Метод `OnEntityDestroy` вызывается при уничтожении сущности BradleyAPC. Этот метод используется для выполнения некоторых действий после того, как сущность была уничтожена.

**Параметры:**

* `BradleyAPC`: объект-сущность BradleyAPC, который был уничтожен.

**Возвращаемое значение:**

Нет возвращаемого значения (void).

**Пример использования:**

```csharp
public override void OnKilled(HitInfo info)
{
    // ...
    Interface.CallHook("OnEntityDestroy", this);
    // ...
}
```

**Описание действий:**

После вызова метода `OnEntityDestroy` выполняются следующие действия:

* Создается взрывная марка в радиусе 10 единиц.
* Вызывается эффект взрыва.
* Создаются гибы и крейты, которые бросаются в воздух.

**Примечания:**

* Метод `OnEntityDestroy` вызывается только на серверной стороне.
* Этот метод не имеет возвращаемого значения.
```

## CanAcceptItem(ItemContainer,Item,int)

### Summary


### Parameters
- `container`: Контейнер, в который добавляется предмет.
- `item`: Предмет, который пытается быть добавлен.
- `targetPos`: Позиция, на которую будет добавлен предмет.

### Returns
Возвращает результат принятия предмета. Возможные значения: CanAcceptResult.CanAccept, CanAcceptResult.CannotAccept, CanAcceptResult.CannotAcceptRightNow.

### Example
```csharp
object CanAcceptItem(ItemContainer container, Item item, int targetPos)
{
    Puts("CanAcceptItem вызван!");
    
    // Если возвращаемое значение не равно null и не является CanAcceptResult, вернуть null
    return null;
}
```

## OnItemSplit(Item,int)

### Summary
Документация для метода `OnItemSplit(Item,int)`:

### Parameters
- `item`: Объект, который будет разделен.
- `splitAmount`: Количество предметов, которое будет разделено.

### Returns
Возвращает объект, если поведение по умолчанию переопределено.

### Example
```csharp
Документация для метода `OnItemSplit(Item,int)`:

```rust
object OnItemSplit(Item item, int splitAmount)
{
    Puts("OnItemSplit вызван!");
    // Здесь можно добавить дополнительную логику или изменить поведение разделения предмета
    return null;
}
```

В этом методе используется `Interface.CallHook` для вызова хука `OnItemSplit`, который возвращает объект, если поведение по умолчанию переопределено. Если возвращаемое значение не равно нулю, оно будет использовано вместо стандартного поведения разделения предмета.

Примечание: Этот метод можно использовать для добавления дополнительной логики или изменения поведения разделения предмета, но он должен быть вызван из метода `SplitItem`, который является частью класса `Item`.
```

## OnItemUpgrade(Item,Item,BasePlayer)

### Summary


### Parameters
- `item`: Предмет, который был обновлен.
- `newItem`: Обновлённый предмет.
- `player`: Игрок, который выполнил обновление.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemUpgrade(Item item, Item newItem, BasePlayer player)
{
    Puts($"Предмет '{item.shortname}' успешно обновлён до версии '{newItem.shortname}' для игрока {player.displayName}");
}
```

## OnHelicopterDropDoorOpen(CH47HelicopterAIController)

### Summary


### Parameters
- `controller`: Контроллер AI вертолета.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHelicopterDropDoorOpen(CH47HelicopterAIController controller)
{
    Puts("Дверь санитарного вертолета открыта!");
    return null;
}
```

## OnLootEntityEnd(BasePlayer,StorageContainer)

### Summary


### Parameters
- `player`: Игрок, который закончил лутить.
- `storageContainer`: Хранилище контейнеров, в котором хранятся предметы.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnLootEntityEnd(BasePlayer player, StorageContainer storageContainer)
{
    Puts("OnLootEntityEnd работает!");
    return null;
}
```

## OnExperimentStarted(Workbench,BasePlayer)

### Summary


### Parameters
- `workbench`: Рабочая столешка.
- `player`: Игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnExperimentStarted(Workbench workbench, BasePlayer player)
{
    Puts("Эксперимент начат!");
}
```

## OnItemCraft(IndustrialCrafter,ItemBlueprint)

### Summary


### Parameters
- `crafter`: Объект индустриального крана.
- `blueprint`: Схема предмета, который будет создан.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemCraft(IndustrialCrafter crafter, ItemBlueprint blueprint)
{
    Puts("OnItemCraft вызван!");
    return null;
}
```

## CanChangeCode(BasePlayer,CodeLock,string,bool)

### Summary


### Parameters
- `player`: Игрок, пытающийся изменить код.
- `codeLock`: CodeLock, для которого меняется код.
- `newCode`: Новый код.
- `isGuest`: Флаг, указывающий, является ли новый код гостевым или нет.

### Returns
Возвращает ненулевое значение, если поведение по умолччанию переопределено.

### Example
```csharp
object CanChangeCode(BasePlayer player, CodeLock codeLock, string newCode, bool isGuest)
{
    Puts("CanChangeCode работает!");
    return null;
}
```

## OnTurretStartup(AutoTurret)

### Summary


### Parameters
- `turret`: Турет.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTurretStartup(AutoTurret turret)
{
    Puts("OnTurretStartup работает!");
    return null;
}
```

## OnEntityReskin(BaseEntity,ItemSkinDirectory.Skin,BasePlayer)

### Summary
This is a C# code snippet that appears to be part of a game server implementation. It's handling the reskining of an entity (a game object) on the server side. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game server implementation. It's handling the reskining of an entity (a game object) on the server side. Here's a breakdown of what it does:

1. **Reskinning**: The code takes in several parameters:
	* `baseEntity`: The entity being reskinned.
	* `skinID`: The ID of the new skin to apply.
	* `num`: An integer value ( likely related to the skin ID).
	* `hashSet`: A set of authorized players (optional).
	* `dictionary2`: A dictionary containing item data (optional).
	* `flag2`: A boolean flag indicating whether to preserve child entities (optional).
	* `obj`: A list of ChildPreserveInfo objects (optional).
2. **Reskinning process**:
	* The code creates a new entity (`baseEntity2`) with the same parent and position as the original entity.
	* It sets various properties on the new entity, such as its skin ID, health, last attacked time, and authorized players (if applicable).
	* If the new entity is a building privilege, it sets the authorized players from the `hashSet`.
3. **Restoring entity storage**:
	* The code saves the item data from the original entity's inventory to the `dictionary2` dictionary.
	* It then restores the item data from the dictionary to the new entity's inventory.
4. **Preserving child entities**:
	* If the `flag2` is true, the code preserves the child entities of the original entity by setting their parents and positions on the new entity.
5. **Sending reskin result to clients**:
	* The code sends a message to all connected clients with the result of the reskining process (success or failure).

Some notes:

* This code assumes that there are certain game-specific classes and interfaces, such as `BaseEntity`, `IItemContainerEntity`, `ChildPreserveInfo`, etc.
* The `RpcTarget` class is likely used for remote procedure calls between the server and clients.
* The `Facepunch.Pool.FreeList` method is used to free a list of objects (in this case, the `obj` list).
* The `LoseCondition` method is called with a condition loss value (`ConditionLossPerReskin`) when the reskining process fails.
```

## OnPlayerSpawn(BasePlayer,Network.Connection)

### Summary


### Parameters
- `player`: Игрок, который появился.
- `connection`: Соединение игрока с сервером.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerSpawn(BasePlayer player, Network.Connection connection)
{
    Puts("OnPlayerSpawn работает!");
    return null;
}
```

## CanFastTrackCraftTask(ItemCrafter,ItemCraftTask,int)

### Summary


### Parameters
- `craft`: Кастер.
- `task`: Задача.
- `taskID`: Идентификатор задачи.

### Returns
Возвращает true, если ускорение задачи возможно, и false в противном случае.

### Example
```csharp
bool CanFastTrackCraftTask(ItemCrafter craft, ItemCraftTask task, int taskID)
{
    Puts("CanFastTrackCraftTask работает!");
    // Здесь можно добавить дополнительную логику для проверки возможности ускорения задачи
    return true;
}
```

## CanRenameBed(BasePlayer,SleepingBag,string)

### Summary


### Parameters
- `player`: Игрок, пытающийся переименовать кровать.
- `bed`: Кровать, которую нужно переименовать.
- `newName`: Новое имя для кровати.

### Returns
Возвращает true, если переименование разрешено, и false в противном случае.

### Example
```csharp
bool CanRenameBed(BasePlayer player, SleepingBag bed, string newName)
{
    Puts("CanRenameBed работает!");
    // Здесь можно добавить логическую логику для проверки возможности переименования кровати
    return true;
}
```

## OnAirdrop(CargoPlane,UnityEngine.Vector3)

### Summary


### Parameters
- `cargoPlane`: Экземпляр CargoPlane.
- `dropPosition`: Позиция сброса.

### Returns
No return value.

### Example
```csharp
object OnAirdrop(CargoPlane cargoPlane, Vector3 dropPosition)
{
    Puts("OnAirdrop работает!");
    return null;
}
```

## CanFireLiquidWeapon(BasePlayer,LiquidWeapon)

### Summary


### Parameters
- `player`: Игрок, пытающийся выстрелить.
- `liquidWeapon`: Объект жидкостного оружия.

### Returns
Возвращает true, если игрок может выстрелить, и false в противном случае.

### Example
```csharp
bool CanFireLiquidWeapon(BasePlayer player, LiquidWeapon liquidWeapon)
{
    Puts("CanFireLiquidWeapon работает!");
    return true;
}
```

## OnNetworkGroupLeft(BaseNetworkable,Network.Visibility.Group)

### Summary


### Parameters
- `group`: Группа, из которой покинуто.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNetworkGroupLeft(BaseNetworkable group, Network.Visibility.Group visibility)
{
    Puts("OnNetworkGroupLeft работает!");
    return null;
}
```

## OnBigWheelLoss(BigWheelGame,Item,BigWheelBettingTerminal)

### Summary


### Parameters
- `game`: Игровая информация.
- `item`: Потерянный предмет.
- `terminal`: Терминал ставки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBigWheelLoss(BigWheelGame game, Item item, BigWheelBettingTerminal terminal)
{
    Puts("OnBigWheelLoss работает!");
    return null;
}
```

## CanAssignMission(BasePlayer,BaseMission,IMissionProvider)

### Summary


### Parameters
- `player`: Игрок, которому предлагается миссия.
- `mission`: Миссия, которая предлагается.
- `provider`: Провайдер миссии.

### Returns
Возвращает true, если миссия может быть присвоена игроку, и false в противном случае.

### Example
```csharp
bool CanAssignMission(BasePlayer player, BaseMission mission, IMissionProvider provider)
{
    Puts("CanAssignMission вызван!");
    // Если возвращаемое значение не равно null, то метод переопределяет поведение по умолчанию
    return true;
}
```

## OnWeaponModChange(BaseProjectile,BasePlayer)

### Summary


### Parameters
- `projectile`: Проектиль, который был изменен.
- `player`: Игрок, владеющий проектилом.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnWeaponModChange(BaseProjectile projectile, BasePlayer player)
{
    Puts("OnWeaponModChange работает!");
    return null;
}
```

## OnRackedWeaponSwap(Item,WeaponRackSlot,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Оружие, которое будет заменено.
- `weaponRackSlot`: Слот на ремне, в который будет помещено оружие.
- `player`: Игрок, который выполняет замену.
- `weaponRack`: Ремень, на котором происходит замена.

### Returns
Возвращает null, если поведение по умолчанию не переопределено.

### Example
```csharp
object OnRackedWeaponSwap(Item item, WeaponRackSlot weaponRackSlot, BasePlayer player, WeaponRack weaponRack)
{
    Puts("OnRackedWeaponSwap работает!");
    return null;
}
```

## OnTakeCurrencyItem(NPCVendingMachine,Item)

### Summary


### Parameters
- `vendingMachine`: Автомат, из которого был взят предмет.
- `item`: Взятый валютный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTakeCurrencyItem(NPCVendingMachine vendingMachine, Item item)
{
    Puts("OnTakeCurrencyItem работает!");
}

Если ReturnType - void, не включайте оператор return
```

## OnCorpsePopulate(FrankensteinPet,NPCPlayerCorpse)

### Summary


### Parameters
- `pet`: Тело питомца.
- `corpse`: Тело NPC игрока.

### Returns
Возвращает тело NPC игрока, если поведение по умолчанию переопределено.

### Example
```csharp
object OnCorpsePopulate(FrankensteinPet pet, NPCPlayerCorpse corpse)
{
    Puts("OnCorpsePopulate работает!");
    return null;
}
```

## OnItemAction(Item,string,BasePlayer)

### Summary
Документация для метода `OnItemAction(Item, string, BasePlayer)`:

### Parameters
- `item`: Предмет.
- `action`: Действие.
- `player`: Игрок.

### Returns
Нет возвращаемого значения.

### Example
```csharp
Документация для метода `OnItemAction(Item, string, BasePlayer)`:

```rust
void OnItemAction(Item item, string action, BasePlayer player)
{
    // Минимальный код для демонстрации функциональности
}
```

В этом методе используется хук `OnItemAction` для вызова при выполнении действия с предметом. Метод принимает три параметра: `item` - предмет, на котором выполняется действие; `action` - действие, которое выполняется; и `player` - игрок, который выполняет действие.

Метод не возвращает никаких значений и используется для вызова других методов или хуков при выполнении действия с предметом.
```

## OnItemUnwrap(Item,BasePlayer,ItemModUnwrap)

### Summary


### Parameters
- `item`: Развертываемый предмет.
- `player`: Игрок, пытается развернуть предмет.
- `modUnwrap`: Модификатор разворачивания.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemUnwrap(Item item, BasePlayer player, ItemModUnwrap modUnwrap)
{
    Puts("OnItemUnwrap работает!");
    return null;
}
```

## OnItemDeployed(Deployer,ItemModDeployable,BaseEntity)

### Summary


### Parameters
- `deployer`: Объект, который развернул предмет.
- `itemModDeployable`: Модифицированный предмет для развертывания.
- `baseEntity`: Сущность, созданная после развертывания.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemDeployed(Deployer deployer, ItemModDeployable itemModDeployable, BaseEntity baseEntity)
{
    Puts("OnItemDeployed вызван!");
}
```

## OnMissionStarted(BaseMission,BaseMission.MissionInstance,BasePlayer)

### Summary


### Parameters
- `mission`: Миссия.
- `instance`: Экземпляр миссии.
- `assignee`: Игрок, которому назначена миссия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMissionStarted(BaseMission mission, BaseMission.MissionInstance instance, BasePlayer assignee)
{
    Puts("OnMissionStarted работает!");
    return null;
}
```

## OnMessagePlayer(string,BasePlayer)

### Summary


### Parameters
- `message`: Отправленное сообщение.
- `player`: Игрок, отправивший сообщение.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMessagePlayer(string message, BasePlayer player)
{
    Puts($"Игрок {player.UserIDString} отправил в чат: {message}");
    return null;
}
```

## OnStashOcclude(StashContainer)

### Summary


### Parameters
- `stashContainer`: Контейнер с предметами.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnStashOcclude(StashContainer stashContainer)
{
    Puts("OnStashOcclude работает!");
    return null;
}
```

## OnFireBallSpread(FireBall,BaseEntity)

### Summary


### Parameters
- `fireBall`: Огненный шар.
- `entity`: Сущность, на которую распространяется огонь.

### Returns
Возвращает сущность, если поведение по умолчанию переопределено.

### Example
```csharp
object OnFireBallSpread(FireBall fireBall, BaseEntity entity)
{
    Puts("OnFireBallSpread работает!");
    return null;
}
```

## OnRackedWeaponLoaded(Item,ItemDefinition,BasePlayer,WeaponRack)

### Summary


### Parameters
- `slot`: Оружие, в которое загружается патрон.
- `itemDefinition`: Определение патрона.
- `player`: Игрок, который выполняет действие.
- `weaponRack`: Станция оружия.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponLoaded(Item slot, ItemDefinition itemDefinition, BasePlayer player, WeaponRack weaponRack)
{
    Puts("OnRackedWeaponLoaded работает!");
}
```

## OnBoomboxStationValidate(string)

### Summary


### Parameters
- `url`: Адрес радиостанции.

### Returns
Возвращает <c>true</c>, если радиостанция валидна, и <c>false</c> в противном случае.

### Example
```csharp
bool OnBoomboxStationValidate(string url)
{
    Puts("OnBoomboxStationValidate вызван!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnPortalUse(BasePlayer,BasePortal)

### Summary


### Parameters
- `player`: Игрок, который использовал портал.
- `portal`: Портал, который был использован.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPortalUse(BasePlayer player, BasePortal portal)
{
    Puts("OnPortalUse работает!");
    return null;
}
```

## OnTrapTrigger(BearTrap,UnityEngine.GameObject)

### Summary


### Parameters
- `trap`: Ловушка, которую тронул игрок.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTrapTrigger(BearTrap trap, UnityEngine.GameObject obj)
{
    Puts("OnTrapTrigger работает!");
    return null;
}
```

## OnRidableAnimalClaim(BaseRidableAnimal,BasePlayer,Item)

### Summary


### Parameters
- `animal`: Объект ridable-животного.
- `player`: Игрок, пытается забрать ridable-животное.
- `item`: Токен покупки ridable-животного.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRidableAnimalClaim(BaseRidableAnimal animal, BasePlayer player, Item item)
{
    Puts("OnRidableAnimalClaim работает!");
    return null;
}
```

## CanLock(BasePlayer,KeyLock)

### Summary


### Parameters
- `player`: Игрок, пытающийся зафиксировать объект.
- `lock`: Объект, который будет зафиксирован.

### Returns
Возвращает true, если поведение по умолчанию не переопределено, и false в противном случае.

### Example
```csharp
bool CanLock(BasePlayer player, KeyLock lock)
{
    Puts("CanLock работает!");
    return true;
}
```

## OnNpcDuck(HumanNPC)

### Summary


### Parameters
- `npc`: НПС, который принял или отменил положение "в штаны".

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcDuck(HumanNPC npc)
{
    Puts("OnNpcDuck работает!");
    return null;
}
```

## OnElevatorButtonPress(ElevatorLift,BasePlayer,Elevator.Direction,bool)

### Summary


### Parameters
- `lift`: Лифт.
- `player`: Игрок, который нажал кнопку.
- `direction`: Направление движения лифта (вверх или вниз).
- `flag`: Флаг, указывающий на тип действия (поднять или опустить).

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnElevatorButtonPress(ElevatorLift lift, BasePlayer player, Elevator.Direction direction, bool flag)
{
    Puts("OnElevatorButtonPress работает!");
    return null;
}
```

## OnTrapTrigger(Landmine,UnityEngine.GameObject)

### Summary


### Parameters
- `landmine`: Объект-ловушка.
- `gameObject`: Игрок, который активировал ловушку.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTrapTrigger(Landmine landmine, UnityEngine.GameObject gameObject)
{
    Puts("OnTrapTrigger работает!");
    return null;
}
```

## OnRidableAnimalClaimed(BaseRidableAnimal,BasePlayer)

### Summary


### Parameters
- `animal`: Заинтересованное животное.
- `player`: Игрок, который купил животное.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRidableAnimalClaimed(BaseRidableAnimal animal, BasePlayer player)
{
    Puts("OnRidableAnimalClaimed работает!");
    return null;
}
```

## OnTeamKick(RelationshipManager.PlayerTeam,BasePlayer,ulong)

### Summary


### Parameters
- `team`: Команда, из которой выгоняется игрок.
- `player`: Выгоняемый игрок.
- `kickedPlayerId`: ID выгнанного игрока.

### Returns
Возвращает ID выгнанного игрока, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamKick(RelationshipManager.PlayerTeam team, BasePlayer player, ulong kickedPlayerId)
{
    Puts($"Игрок {player.UserID} выгнан из команды {team.Name}");
    return kickedPlayerId;
}
```

## CanBeTargeted(BasePlayer,FlameTurret)

### Summary


### Parameters
- `player`: Игрок, который может быть целью.
- `turret`: Турель, которая проверяет возможность целигования.

### Returns
Возвращает true, если игрок может быть целью, и false в противном случае.

### Example
```csharp
bool CanBeTargeted(BasePlayer player, FlameTurret turret)
{
    Puts("CanBeTargeted работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnPlayerSpectateEnd(BasePlayer,string)

### Summary


### Parameters
- `player`: Игрок, который перестал смотреть.
- `spectateFilter`: Фильтр смотрения.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerSpectateEnd(BasePlayer player, string spectateFilter)
{
    Puts($"Игрок {player.UserIDString} перестал смотреть на другого игрока.");
}
```

## CanUseVending(BasePlayer,VendingMachine)

### Summary


### Parameters
- `player`: Игрок, пытаясь использовать автомат.
- `vendingMachine`: Автомат по продаже.

### Returns
Возвращает true, если игрок может использовать автомат, и false в противном случае.

### Example
```csharp
bool CanUseVending(BasePlayer player, VendingMachine vendingMachine)
{
    Puts("CanUseVending работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnServerInitialize()

### Summary


### Parameters
No parameters.

### Returns
Возвращает значение true, если сервер был загружен из сохранения.

### Example
```csharp
bool OnServerInitialize()
{
    Puts("OnServerInitialize вызван!");
    return false;
}
```

## IOnEntitySaved(BaseNetworkable,BaseNetworkable.SaveInfo)

### Summary


### Parameters
- `entity`: Сохраненная сущность.
- `saveInfo`: Информация о сохранении.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object IOnEntitySaved(BaseNetworkable entity, BaseNetworkable.SaveInfo saveInfo)
{
    Puts("IOnEntitySaved работает!");
    return null;
}
```

## OnTeamDisbanded(RelationshipManager.PlayerTeam)

### Summary


### Parameters
- `team`: Распущенная команда.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTeamDisbanded(RelationshipManager.PlayerTeam team)
{
    Puts($"Команда {team.teamID} распущена!");
}
```

## OnHorseUnhitch(RidableHorse,HitchTrough.HitchSpot)

### Summary


### Parameters
- `horse`: Лошадь, которую нужно снять.
- `hitchSpot`: Место привязки, из которого нужно снять лошадь.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHorseUnhitch(RidableHorse horse, HitchTrough.HitchSpot hitchSpot)
{
    Puts("OnHorseUnhitch работает!");
    return null;
}
```

## OnMissionAssigned(BaseMission,IMissionProvider,BasePlayer)

### Summary


### Parameters
- `mission`: Назначенная миссия.
- `provider`: Провайдер миссии.
- `assignee`: Игрок, которому назначена миссия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMissionAssigned(BaseMission mission, IMissionProvider provider, BasePlayer assignee)
{
    Puts("OnMissionAssigned вызван!");
    return null;
}
```

## OnRefreshVendingStock(VendingMachine,ItemDefinition)

### Summary


### Parameters
- `vendingMachine`: Автомат.
- `itemDefinition`: Определение товара.

### Returns
Общее количество товара в наличии.

### Example
```csharp
object OnRefreshVendingStock(VendingMachine vendingMachine, ItemDefinition itemDefinition)
{
    Puts("OnRefreshVendingStock работает!");
    return null;
}
```

## OnTreeMarkerHit(TreeEntity,HitInfo)

### Summary


### Parameters
- `treeEntity`: Энтити дерева.
- `hitInfo`: Информация о выстреле.

### Returns
Возвращает true, если условие выполнено, и false в противном случае.

### Example
```csharp
bool OnTreeMarkerHit(TreeEntity treeEntity, HitInfo hitInfo)
{
    Puts("OnTreeMarkerHit вызван!");
    return true; // Возвращаемое значение определяется выше
}
```

## OnShopAcceptClick(ShopFront,BasePlayer)

### Summary


### Parameters
- `shopFront`: Фронт магазина.
- `player`: Игрок, который нажал кнопку.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnShopAcceptClick(ShopFront shopFront, BasePlayer player)
{
    Puts("OnShopAcceptClick работает!");
}

```

## OnEngineLoadoutRefresh(Rust.Modular.EngineStorage)

### Summary


### Parameters
- `engineStorage`: Хранилище модульной машины.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnEngineLoadoutRefresh(Rust.Modular.EngineStorage engineStorage)
{
    Puts("OnEngineLoadoutRefresh работает!");
}
```

## OnItemRecycle(Item,Recycler)

### Summary
This is a C# code snippet that appears to be part of a game mod for Rust, a survival video game. The code is responsible for recycling items in the game.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game mod for Rust, a survival video game. The code is responsible for recycling items in the game.

Here's a breakdown of what the code does:

1. It checks if there are any recyclable items in the inventory.
2. If there are, it iterates through each item and checks if it can be recycled using the `CanBeRecycled` method.
3. If an item can be recycled, it calls a hook (`OnItemRecycle`) to allow other mods to modify the recycling process.
4. It then calculates how many of the item to recycle based on its condition and the game's settings.
5. For each recyclable item, it creates a new "scrap" item and adds it to the output inventory.
6. If the item has a blueprint associated with it, it applies the blueprint's effects (e.g., adding stats) to the player who recycled the item.
7. Finally, it stops recycling if there are no more recyclable items or if an error occurs.

Some notable aspects of this code include:

* The use of hooks (`OnItemRecycle` and `OnItemRecycleAmount`) to allow other mods to modify the recycling process.
* The calculation of how many items to recycle based on their condition and the game's settings.
* The creation of a new "scrap" item and adding it to the output inventory.
* The application of blueprint effects to the player who recycled the item.

Overall, this code is responsible for implementing the recycling mechanics in the game, allowing players to convert items into scrap and potentially gain benefits from doing so.
```

## CanCraft(ItemCrafter,ItemBlueprint,int,bool)

### Summary


### Parameters
- `craftTask`: Задача крафтинга.
- `blueprint`: Схема предмета.
- `amount`: Количество предметов для крафтинга.
- `free`: Флаг, указывающий, что крафтинг выполняется бесплатно.

### Returns
Возвращает true, если крафтинг разрешен, и false в противном случае.

### Example
```csharp
bool CanCraft(ItemCrafter craftTask, ItemBlueprint blueprint, int amount, bool free)
{
    // Минимальный код для демонстрации функциональности
    Puts("CanCraft вызван!");
    
    // Если ReturnType - void, не включайте оператор return
    
    object obj = Interface.CallHook("CanCraft", this, craftTask, blueprint, amount, free);
    if (obj is bool)
    {
        return (bool)obj;
    }
    
    // Остальной код для проверки доступности ресурсов и условия крафтинга
    // ...
    
    return true; // Возвращаемое значение по умолчанию
}
```

## CanUseLockedEntity(BasePlayer,KeyLock)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть сущность.
- `lock`: Замок, который необходимо открыть.

### Returns
Возвращает true, если игрок может использовать защищенную сущность, и false в противном случае.

### Example
```csharp
bool CanUseLockedEntity(BasePlayer player, KeyLock lock)
{
    Puts("CanUseLockedEntity работает!");
    // Если HasLockPermission(player) или !IsLocked(), вернуть true
    return HasLockPermission(player) || !IsLocked();
}
```

## OnElevatorCall(Elevator,Elevator)

### Summary


### Parameters
- `elevator`: Лифт, который был вызван.
- `callerElevator`: Лифт, из которого был вызван лифт.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnElevatorCall(Elevator elevator, Elevator callerElevator)
{
    Puts($"Лифт {elevator} был вызван из {callerElevator}");
}
```

## OnBookmarkControlEnd(ComputerStation,BasePlayer,BaseEntity)

### Summary


### Parameters
- `computerStation`: Компьютерная станция.
- `player`: Игрок.
- `entity`: Сущность, которую контролировал игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnBookmarkControlEnd(ComputerStation computerStation, BasePlayer player, BaseEntity entity)
{
    Puts("OnBookmarkControlEnd работает!");
}
```

## CanHideStash(BasePlayer,StashContainer)

### Summary


### Parameters
- `player`: Игрок, пытающийся спрятать контейнер.
- `stashContainer`: Контейнер, который нужно спрятать.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object CanHideStash(BasePlayer player, StashContainer stashContainer)
{
    Puts("CanHideStash работает!");
    return null;
}
```

## OnPlayerDismountFailed(BasePlayer,BaseMountable)

### Summary


### Parameters
- `player`: Игрок, который пытался снять объект.
- `entity`: Объект, с которого игрок пытался снять.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerDismountFailed(BasePlayer player, BaseMountable entity)
{
    Puts("OnPlayerDismountFailed работает!");
    return null;
}
```

## OnItemPickup(Item,BasePlayer)

### Summary


### Parameters
- `item`: Подхваченный предмет.
- `player`: Игрок, который подхватил предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemPickup(Item item, BasePlayer player)
{
    Puts($"Предмет {item} подхвачен игроком {player}");
}
```

## OnTurretDeauthorize(AutoTurret,BasePlayer)

### Summary


### Parameters
- `turret`: Туррет, который был деавторизован.
- `player`: Игрок, который был деавторизован.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTurretDeauthorize(AutoTurret turret, BasePlayer player)
{
    Puts("Туррет деавторизован!");
}
```

## OnItemDespawn(Item)

### Summary


### Parameters
- `item`: Удаленный предмет.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemDespawn(Item item)
{
    Puts($"Предмет {item} удален.");
}
```

## OnNpcTarget(HumanNPC,BaseEntity)

### Summary


### Parameters
- `npc`: НПС.
- `target`: Точка визирования.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcTarget(HumanNPC npc, BaseEntity target)
{
    Puts("OnNpcTarget работает!");
    return null;
}
```

## OnSprayCreate(SprayCan,UnityEngine.Vector3,UnityEngine.Quaternion)

### Summary


### Parameters
- `sprayCan`: Объект спрей-канна.
- `position`: Позиция спрей-канна.
- `rotation`: Вращение спрей-канна.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSprayCreate(SprayCan sprayCan, Vector3 position, Quaternion rotation)
{
    Puts("OnSprayCreate вызван!");
}
```

## CanUpdateSign(BasePlayer,Signage)

### Summary


### Parameters
- `player`: Игрок, пытающийся обновить знак.
- `signage`: Знак, который нужно обновить.

### Returns
Возвращает true, если игрок может обновить знак, и false в противном случае.

### Example
```csharp
bool CanUpdateSign(BasePlayer player, Signage signage)
{
    Puts("CanUpdateSign вызван!");
    // Если ReturnType - bool, верните значение
    return true;
}
```

## OnPlayerRespawn(BasePlayer,SleepingBag)

### Summary


### Parameters
- `player`: Игрок.
- `sleepingBag`: Снаряд для сна.

### Returns
Возвращает снаряд для сна, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerRespawn(BasePlayer player, SleepingBag sleepingBag)
{
    Puts("OnPlayerRespawn работает!");
    return null;
}
```

## CanUnlockTechTreeNodePath(BasePlayer,TechTreeData.NodeInstance,TechTreeData)

### Summary


### Parameters
- `player`: Игрок, который пытается разблокировать путь.
- `node`: Нод-инстанс, к которому относится путь.
- `techTreeData`: Данные дерева технологий.

### Returns
Возвращает true, если путь можно разблокировать, и false в противном случае.

### Example
```csharp
bool CanUnlockTechTreeNodePath(BasePlayer player, TechTreeData.NodeInstance node, TechTreeData techTreeData)
{
    Puts("CanUnlockTechTreeNodePath вызван!");
    
    // Если возвращаемое значение не bool, вернуть null
    return null;
}
```

## OnRackedWeaponSwapped(Item,WeaponRackSlot,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Помененное оружие.
- `weaponSlot`: Ячейка ящика, из которой было снято оружие.
- `player`: Игрок, который поменял оружие.
- `rack`: Ящик, в котором находится оружие.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponSwapped(Item item, WeaponRackSlot weaponSlot, BasePlayer player, WeaponRack rack)
{
    Puts($"Оружие {item.info.name} поменено в ящике {rack.name} для игрока {player.UserIDString}");
}
```

## OnEntityReskinned(BaseEntity,ItemSkinDirectory.Skin,BasePlayer)

### Summary
This is a C# code snippet that appears to be part of a game server implementation. It's handling the reskining of an entity (a game object) on the server side. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game server implementation. It's handling the reskining of an entity (a game object) on the server side. Here's a breakdown of what it does:

1. **Reskinning**: The code takes in several parameters:
	* `baseEntity`: The entity being reskinned.
	* `skinID`: The ID of the new skin to apply.
	* `num`: An integer value ( likely related to the skin ID).
	* `hashSet`: A set of authorized players (optional).
	* `dictionary2`: A dictionary containing item data (optional).
	* `flag2`: A boolean flag indicating whether to preserve child entities (optional).
	* `obj`: A list of ChildPreserveInfo objects (optional).
2. **Reskinning process**:
	* The code creates a new entity (`baseEntity2`) with the same parent and position as the original entity.
	* It sets various properties on the new entity, such as its skin ID, health, last attacked time, and authorized players (if applicable).
	* If the new entity is a building privilege, it sets the authorized players from the `hashSet`.
3. **Restoring entity storage**:
	* The code saves the item data from the original entity's inventory to the `dictionary2` dictionary.
	* It then restores the item data from the dictionary to the new entity's inventory.
4. **Preserving child entities**:
	* If the `flag2` is true, the code preserves the child entities of the original entity by setting their parents and positions on the new entity.
5. **Sending reskin result to clients**:
	* The code sends a message to all connected clients with the result of the reskining process (success or failure).

Some notes:

* This code assumes that there are certain game-specific classes and interfaces, such as `BaseEntity`, `IItemContainerEntity`, `ChildPreserveInfo`, etc.
* The `RpcTarget` class is likely used for remote procedure calls between the server and clients.
* The `Facepunch.Pool.FreeList` method is used to free a list of objects (in this case, the `obj` list).
* The `LoseCondition` method is called with a condition loss value (`ConditionLossPerReskin`) when the reskining process fails.
```

## OnPlayerDig(BasePlayer,BaseDiggableEntity)

### Summary


### Parameters
- `player`: Игрок, пытающийся вырыть объект.
- `entity`: Объект, который нужно вырыть.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerDig(BasePlayer player, BaseDiggableEntity entity)
{
    Puts("OnPlayerDig работает!");
    return null;
}
```

## OnPlayerAddModifiers(BasePlayer,Item,ItemModConsumable)

### Summary
Документация для хука `OnPlayerAddModifiers`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для хука `OnPlayerAddModifiers`:

**Название:** `OnPlayerAddModifiers`

**Описание:** Этот хук вызывается после того, как игроку добавляются модификаторы в результате использования предмета.

**Сигнатура:**

```csharp
void OnPlayerAddModifiers(BasePlayer player, Item item, ItemModConsumable consumable)
```

**Аргументы:**

* `player`: Игрок, которому были добавлены модификаторы.
* `item`: Предмет, который был использован для добавления модификаторов.
* `consumable`: Объект `ItemModConsumable`, который содержит информацию о модификаторах.

**Возвращаемое значение:** `void`

**Пример использования:**

```csharp
public override void DoAction(Item item, BasePlayer player)
{
    // ...

    if (player.modifiers != null && Interface.CallHook("OnPlayerAddModifiers", player, item, consumable) == null)
    {
        player.modifiers.Add(consumable.modifiers);
    }

    // ...
}
```

**Описание функциональности:**

Этот хук вызывается после того, как игроку добавляются модификаторы в результате использования предмета. Он позволяет расширить поведение игры и добавить новые функции на основе модификаторов.

**Примечания:**

* Этот хук не имеет возвращаемого значения.
* Он вызывается только один раз после того, как игроку добавляются модификаторы.
* Внутри этого хука можно использовать методы и свойства класса `BasePlayer` для работы с игроком.
```

## OnStructureUpgraded(BuildingBlock,BasePlayer,BuildingGrade.Enum,ulong)

### Summary


### Parameters
- `block`: Текущая блок-конструкция.
- `player`: Игрок, который выполнил улучшение.
- `grade`: Новая степень конструкции.
- `upgradeId`: Идентификатор улучшения.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnStructureUpgraded(BuildingBlock block, BasePlayer player, BuildingGrade.Enum grade, ulong upgradeId)
{
    Puts("OnStructureUpgraded вызван!");
    return null;
}
```

## CanSeeStash(BasePlayer,StashContainer)

### Summary


### Parameters
- `player`: Игрок, пытающийся увидеть стэш.
- `stashContainer`: Стэш, который игрок пытается увидеть.

### Returns
Возвращает true, если игрок может увидеть стэш, иначе false.

### Example
```csharp
bool CanSeeStash(BasePlayer player, StashContainer stashContainer)
{
    Puts("CanSeeStash работает!");
    // Здесь можно добавить дополнительную логическую логику для определения возможности видимости стэша
    return true; // Возвращаем true по умолчанию
}
```

## OnDeleteVendingOffer(VendingMachine,int)

### Summary


### Parameters
- `vendingMachine`: Объект vending-машины.
- `index`: Индекс удаляемого предложения.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDeleteVendingOffer(VendingMachine vendingMachine, int index)
{
    Puts($"Предложение {index} удалено из vending-машины {vendingMachine}");
}
```

## OnIORefCleared(IOEntity.IORef,IOEntity)

### Summary


### Parameters
- `entity`: Объект, для которого была очищена ссылка.
- `ioRef`: Ссылка на IO-объект, которая была очищена.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnIORefCleared(IOEntity entity, IOEntity.IORef ioRef)
{
    Puts("OnIORefCleared работает!");
    return null;
}
```

## OnPlayerRespawn(BasePlayer,BasePlayer.SpawnPoint)

### Summary


### Parameters
- `player`: Игрок, возобнавшийся.
- `spawnPoint`: Точка возобновления.

### Returns
Возвращает точку возобновления, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerRespawn(BasePlayer player, BasePlayer.SpawnPoint spawnPoint)
{
    Puts("OnPlayerRespawn работает!");
    return null;
}
```

## OnWeaponReload(BaseProjectile,BasePlayer)

### Summary


### Parameters
- `projectile`: Проектиль, который перезарядают.
- `player`: Игрок, который перезарядает оружие.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnWeaponReload(BaseProjectile projectile, BasePlayer player)
{
    Puts("OnWeaponReload работает!");
    return null;
}
```

## OnCrateHackEnd(HackableLockedCrate)

### Summary


### Parameters
- `crate`: Защищенный ящик.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCrateHackEnd(HackableLockedCrate crate)
{
    Puts("Процесс взлома защищенного ящика завершен!");
}
```

## OnMeleeThrown(BasePlayer,Item)

### Summary
Документация для хука `OnMeleeThrown(BasePlayer, Item)`:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для хука `OnMeleeThrown(BasePlayer, Item)`:

**Описание:**

Хук `OnMeleeThrown` вызывается после того, как игрок бросил предмет в сторону. Этот хук позволяет модификаторам и плагинам реагировать на это событие.

**Параметры:**

* `BasePlayer`: Игрок, который бросил предмет.
* `Item`: Брошенный предмет.

**Пример использования:**

```csharp
public class MyPlugin : MonoBehaviour
{
    public void OnMeleeThrown(BasePlayer player, Item item)
    {
        // Реагируйте на событие бросания предмета
        Puts("Игрок " + player.name + " бросил предмет " + item.info.name);
    }
}
```

**Примечание:**

Этот хук вызывается только в том случае, если игрок бросает предмет в сторону. Если игрок просто держит предмет в руках, этот хук не будет вызван.
```

## OnEntityDistanceCheck(BaseEntity,BasePlayer,uint,string,float,bool)

### Summary


### Parameters
- `entity`: Сущность, для которой проверяется расстояние.
- `player`: Игрок, с которым сравнивается расстояние.
- `id`: Идентификатор вызывающего метода.
- `debugName`: Название вызывающего метода для отладки.
- `maximumDistance`: Максимально допустимое расстояние.
- `checkParent`: Флаг, указывающий, следует ли проверять расстояние и у сущности-родителя.

### Returns
Возвращает true, если расстояние между сущностью и игроком меньше или равно maximumDistance, в противном случае false.

### Example
```csharp
bool OnEntityDistanceCheck(BaseEntity entity, BasePlayer player, uint id, string debugName, float maximumDistance, bool checkParent)
{
    Puts($"OnEntityDistanceCheck вызван для {debugName} с ID {id}");
    
    // Если расстояние между сущностью и игроком меньше или равно maximumDistance, возвращаем true
    return entity.Distance(player.eyes.position) <= maximumDistance;
}
```

## OnMapMarkerAdded(BasePlayer,ProtoBuf.MapNote)

### Summary


### Parameters
- `player`: Игрок, который добавил метку.
- `mapNote`: Информация о добавленной метке.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMapMarkerAdded(BasePlayer player, ProtoBuf.MapNote mapNote)
{
    Puts($"Метка '{mapNote.note}' добавлена игроком {player.UserIDString} на карте.");
}
```

## OnDemoRecordingStop(string,BasePlayer)

### Summary


### Parameters
- `filename`: Имя файла записи.
- `player`: Игрок, который останавливает запись.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDemoRecordingStop(string filename, BasePlayer player)
{
    Puts("OnDemoRecordingStop работает!");
    return null;
}
```

## OnDefaultItemsReceive(PlayerInventory)

### Summary
Документация для метода `OnDefaultItemsReceive(PlayerInventory)`:

### Parameters
- `inventory`: Инвентарь игрока.

### Returns
No return value.

### Example
```csharp
Документация для метода `OnDefaultItemsReceive(PlayerInventory)`:

```rust
void OnDefaultItemsReceive(PlayerInventory inventory)
{
    // Минимальный код для демонстрации функциональности
    // (необходимо реализовать логику получения default-итемов игрока)
}
```

Тип возвращаемого значения: `void` (метод не возвращает никаких значений).

Примечание: Этот метод вызывается в методе `GiveDefaultItems()` и используется для проверки, получены ли default-итемы игроку.
```

## OnCupboardDeauthorize(BuildingPrivlidge,BasePlayer)

### Summary


### Parameters
- `buildingPrivilege`: Права на здание.
- `player`: Игрок, который отменил авторизацию.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCupboardDeauthorize(BuildingPrivlidge buildingPrivilege, BasePlayer player)
{
    Puts("OnCupboardDeauthorize работает!");
}
```

## CanBeWounded(BasePlayer,HitInfo)

### Summary


### Parameters
- `player`: Игрок, на которого может быть нанесен урон.
- `info`: Информация о нападении.

### Returns
Возвращает true, если игрок может быть ранен, и false в противном случае.

### Example
```csharp
bool CanBeWounded(BasePlayer player, HitInfo info)
{
    Puts("CanBeWounded работает!");
    return !IsWounded() && UnityEngine.Time.realtimeSinceStartup - lastWoundedStartTime < ConVar.Server.rewounddelay;
}
```

## OnItemRecycleAmount(Item,int,Recycler)

### Summary
This is a C# code snippet that appears to be part of a game mod for Rust, a survival video game. The code is responsible for recycling items in the game.

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a game mod for Rust, a survival video game. The code is responsible for recycling items in the game.

Here's a breakdown of what the code does:

1. It checks if there are any recyclable items in the inventory.
2. If there are, it iterates through each item and checks if it can be recycled using the `CanBeRecycled` method.
3. If an item can be recycled, it calls a hook (`OnItemRecycle`) to allow other mods to modify the recycling process.
4. It then calculates how many of the item to recycle based on its condition and the game's settings.
5. For each recyclable item, it creates a new "scrap" item and adds it to the output inventory.
6. If the item has a blueprint associated with it, it applies the blueprint's effects (e.g., adding stats) to the player who recycled the item.
7. Finally, it stops recycling if there are no more recyclable items or if an error occurs.

Some notable aspects of this code include:

* The use of hooks (`OnItemRecycle` and `OnItemRecycleAmount`) to allow other mods to modify the recycling process.
* The calculation of how many items to recycle based on their condition and the game's settings.
* The creation of a new "scrap" item and adding it to the output inventory.
* The application of blueprint effects to the player who recycled the item.

Overall, this code is responsible for implementing the recycling mechanics in the game, allowing players to convert items into scrap and potentially gain benefits from doing so.
```

## OnQueueMessage(Network.Connection,int)

### Summary


### Parameters
- `connection`: Соединение игрока.
- `position`: Позиция игрока в очереди.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnQueueMessage(Network.Connection connection, int position)
{
    Puts("OnQueueMessage работает!");
    return null;
}
```

## OnEntityGroundMissing(BaseEntity)

### Summary


### Parameters
- `entity`: Сущность, потерявшая связь с землей.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityGroundMissing(BaseEntity entity)
{
    Puts("OnEntityGroundMissing вызван!");
    return null;
}
```

## CanNetworkTo(BaseEntity,BasePlayer)

### Summary


### Parameters
- `entity`: Сущность, к которой требуется сетевой доступ.
- `player`: Игрок, который пытается получить сетевой доступ.

### Returns
Возвращает true, если сетевой доступ разрешен, и false в противном случае.

### Example
```csharp
bool CanNetworkTo(BaseEntity entity, BasePlayer player)
{
    Puts("CanNetworkTo работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnWindmillUpdated(ElectricWindmill)

### Summary


### Parameters
- `windmill`: Объект ветряной мельницы.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnWindmillUpdated(ElectricWindmill windmill)
{
    Puts("OnWindmillUpdated работает!");
}
```

## OnEntityBuilt(Planner,UnityEngine.GameObject)

### Summary
This is a C# method that appears to be part of a game's deployment system. It's responsible for placing an item on the map when a player clicks on a deployable object (e.g., a blueprint). Here's a breakdown of what the code does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# method that appears to be part of a game's deployment system. It's responsible for placing an item on the map when a player clicks on a deployable object (e.g., a blueprint). Here's a breakdown of what the code does:

1. **Checks for line-of-sight**: The method checks if there are any obstacles between the player and the target position where the item will be placed. If there are, it returns an error message.
2. **Gets the deployable object**: It retrieves the deployable object associated with the blueprint that was clicked on.
3. **Places the item**: It calls a method (`DoPlacement`) to place the item at the target position.
4. **Updates the game state**: If the placement is successful, it updates various game-related data structures:
	* Calls an interface hook (`OnEntityBuilt`) to notify other parts of the game about the new entity.
	* Updates the deployable object's instance data and inventory (if applicable).
	* Notifies the player about the deployment event.
5. **Pays for placement**: It calls a method (`PayForPlacement`) to handle any payment-related consequences of placing the item.

Some notable aspects of this code include:

* The use of various game-specific classes and interfaces (e.g., `BaseEntity`, `Deployable`, `Effect`).
* The reliance on a complex deployment system, which involves multiple steps and interactions with other parts of the game.
* The emphasis on updating game-related data structures to reflect changes in the game state.

Overall, this code is part of a larger system that enables players to deploy items on the map, and it's designed to handle various edge cases and interactions with other game components.
```

## OnDispenserBonus(ResourceDispenser,BasePlayer,Item)

### Summary


### Parameters
- `dispenser`: Диспенсер, из которого был получен бонус.
- `player`: Игрок, который получил бонус.
- `item`: Полученный бонус.

### Returns
Возвращает объект Item, если поведение по умолчанию переопределено.

### Example
```csharp
object OnDispenserBonus(ResourceDispenser dispenser, BasePlayer player, Item item)
{
    Puts("OnDispenserBonus вызван!");
    return null;
}
```

## OnBookmarksSendControl(ComputerStation,BasePlayer,string)

### Summary


### Parameters
- `computerStation`: Экземпляр ComputerStation.
- `player`: Игрок, которому будут отправлены контрольные метки.
- `bookmarksText`: Текст контрольных меток.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBookmarksSendControl(ComputerStation computerStation, BasePlayer player, string bookmarksText)
{
    Puts("OnBookmarksSendControl работает!");
    return null;
}
```

## OnEntityFlagsNetworkUpdate(BaseEntity)

### Summary


### Parameters
- `entity`: Сущность, для которой обновляются сетевые флаги.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntityFlagsNetworkUpdate(BaseEntity entity)
{
    Puts("OnEntityFlagsNetworkUpdate работает!");
    return null;
}
```

## OnWireClear(BasePlayer,IOEntity,int,IOEntity,bool)

### Summary


### Parameters
- `player`: Игрок, который очищает провод.
- `entity`: Сущность, в которой находится провод.
- `index`: Индекс провода.
- `targetEntity`: Сущность, к которой подключен провод.
- `isInput`: Флаг, указывающий, является ли провод входным или выходным.

### Returns
Возвращает true, если очистка провода разрешена; иначе false.

### Example
```csharp
bool OnWireClear(BasePlayer player, IOEntity entity, int index, IOEntity targetEntity, bool isInput)
{
    Puts("OnWireClear вызван!");
    
    // Если возвращаемое значение не равно null, то оно является boolean-значением
    return true; // или другое значение в зависимости от функциональности метода
}
```

## OnEntityControl(PoweredRemoteControlEntity,ulong)

### Summary


### Parameters
- `entity`: Сущность, для которой проверяется возможность управления.
- `playerID`: ИД игрока, который пытается управлять сущностью.

### Returns
Возвращает true, если игрок может управлять сущностью, и false в противном случае.

### Example
```csharp
bool OnEntityControl(PoweredRemoteControlEntity entity, ulong playerID)
{
    Puts("OnEntityControl вызван!");
    return true;
}
```

## OnBroadcastCommand(string,object[])

### Summary


### Parameters
- `strCommand`: Команда для отправки.
- `args`: Аргументы команды.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBroadcastCommand(string strCommand, object[] args)
{
    Puts($"Команда '{strCommand}' отправлена всем клиентам.");
    return null;
}
```

## CanUnlock(BasePlayer,CodeLock)

### Summary


### Parameters
- `player`: Игрок, пытаясь разблокировать объект.
- `lock`: Кодовый замок, который необходимо разблокировать.

### Returns
Возвращает true, если игрок может разблокировать объект, иначе false.

### Example
```csharp
bool CanUnlock(BasePlayer player, CodeLock lock)
{
    Puts("CanUnlock работает!");
    return true;
}
```

## OnComposterUpdate(Composter)

### Summary


### Parameters
- `composter`: Объект компостера.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnComposterUpdate(Composter composter)
{
    Puts("OnComposterUpdate работает!");
    return null;
}
```

## OnTakeCurrencyItem(VendingMachine,Item)

### Summary


### Parameters
- `vendingMachine`: Автомат, из которого был взят предмет.
- `item`: Валютный предмет, который был взят.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnTakeCurrencyItem(VendingMachine vendingMachine, Item item)
{
    Puts($"Предмет {item} взят из автомата {vendingMachine}");
}

```

## OnXmasGiftsDistribute(XMasRefill,BasePlayer)

### Summary


### Parameters
- `refill`: Объект XMasRefill.
- `player`: Игрок, которому будут раздаваться подарки.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnXmasGiftsDistribute(XMasRefill refill, BasePlayer player)
{
    Puts("OnXmasGiftsDistribute работает!");
    return null;
}
```

## OnFuelItemCheck(EntityFuelSystem,StorageContainer)

### Summary


### Parameters
- `entity`: Система топлива.
- `container`: Контейнер с топливом.

### Returns
Возвращает Item, если поведение по умолчанию переопределено; иначе возвращает null или содержимое контейнера.

### Example
```csharp
object OnFuelItemCheck(EntityFuelSystem entity, StorageContainer container)
{
    Puts("OnFuelItemCheck работает!");
    // Если ReturnType - void, не включайте оператор return
    return null;
}
```

## OnItemRefill(Item,BasePlayer)

### Summary


### Parameters
- `item`: Предмет, который заполняется.
- `player`: Игрок, выполняющий действие.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnItemRefill(Item item, BasePlayer player)
{
    Puts("OnItemRefill работает!");
    return null;
}
```

## OnRackedWeaponUnloaded(Item,BasePlayer,WeaponRack)

### Summary


### Parameters
- `item`: Выгружаемое оружие.
- `player`: Игрок, который выполняет действие.
- `weaponRack`: Ячейка для оружия.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnRackedWeaponUnloaded(Item item, BasePlayer player, WeaponRack weaponRack)
{
    Puts("Оружие выгружено из ячейки!");
}
```

## OnMlrsTarget(MLRS,UnityEngine.Vector3,BasePlayer)

### Summary


### Parameters
- `user`: Игрок.
- `worldPos`: Позиция попадания.
- `mounted`: Информация о том, находится ли игрок на сущности.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMlrsTarget(BasePlayer user, Vector3 worldPos, bool mounted)
{
    Puts("OnMlrsTarget работает!");
    return null;
}
```

## OnHelicopterOutOfCrates(CH47HelicopterAIController)

### Summary


### Parameters
- `helicopterController`: Контроллер вертолета.

### Returns
Возвращает true, если поведение по умолчанию переопределено, и false в противном случае.

### Example
```csharp
object OnHelicopterOutOfCrates(CH47HelicopterAIController helicopterController)
{
    Puts("OnHelicopterOutOfCrates работает!");
    return null;
}
```

## OnNpcAlert(ScientistNPC)

### Summary


### Parameters
- `npc`: Научный сотрудник, подающий сигнал тревоги.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnNpcAlert(ScientistNPC npc)
{
    Puts("OnNpcAlert работает!");
    return null;
}
```

## OnCupboardClearList(BuildingPrivlidge,BasePlayer)

### Summary


### Parameters
- `buildingPrivilege`: Права на здание.
- `player`: Игрок, который очищает список.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnCupboardClearList(BuildingPrivlidge buildingPrivilege, BasePlayer player)
{
    Puts("Список авторизованных игроков очищен!");
}
```

## OnInterferenceUpdate(AutoTurret)

### Summary


### Parameters
- `autoTurret`: Автоматическая турель.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnInterferenceUpdate(AutoTurret autoTurret)
{
    Puts("OnInterferenceUpdate работает!");
}
```

## OnIngredientsCollect(ItemCrafter,ItemBlueprint,ItemCraftTask,int,BasePlayer)

### Summary


### Parameters
- `itemCrafter`: Объект ItemCrafter.
- `itemBlueprint`: Схема предмета.
- `itemCraftTask`: Задача по созданию предмета.
- `amount`: Количество ингредиентов.
- `player`: Игрок, который собирает ингредиенты.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnIngredientsCollect(ItemCrafter itemCrafter, ItemBlueprint itemBlueprint, ItemCraftTask itemCraftTask, int amount, BasePlayer player)
{
    Puts("OnIngredientsCollect работает!");
    return null;
}
```

## OnEngineStatsRefresh(VehicleModuleEngine,Rust.Modular.EngineStorage)

### Summary


### Parameters
- `engine`: Двигатель.
- `storage`: Хранилище данных о двигателе.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEngineStatsRefresh(VehicleModuleEngine engine, Rust.Modular.EngineStorage storage)
{
    Puts("OnEngineStatsRefresh работает!");
    return null;
}
```

## CanSwapToSeat(BasePlayer,ModularCarSeat)

### Summary


### Parameters
- `player`: Игрок, пытающийся сменить место.
- `seat`: Модуль сидения, на которое хочет сесть игрок.

### Returns
Возвращает true, если игрок может сменить место, и false в противном случае.

### Example
```csharp
bool CanSwapToSeat(BasePlayer player, ModularCarSeat seat)
{
    Puts("CanSwapToSeat работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnHuntEventStart(EggHuntEvent)

### Summary


### Parameters
- `event`: Событие охоты.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHuntEventStart(EggHuntEvent event)
{
    Puts("OnHuntEventStart работает!");
    return null;
}
```

## OnVehicleModuleSelected(Item,ModularCarGarage,BasePlayer)

### Summary


### Parameters
- `item`: Выбранный модуль.
- `garage`: Модульная гаражная площадка.
- `player`: Игрок, выбравший модуль.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnVehicleModuleSelected(Item item, ModularCarGarage garage, BasePlayer player)
{
    Puts("OnVehicleModuleSelected работает!");
    return null;
}
```

## OnPlayerReported(BasePlayer,string,string,string,string,string)

### Summary


### Parameters
- `player`: Игрок, подавший жалобу.
- `targetId`: ID игрока, на которого подана жалоба.
- `targetName`: Название игрока, на которого подана жалоба.
- `subject`: Тема жалобы.
- `message`: Сообщение жалобы.
- `type`: Тип жалобы.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerReported(BasePlayer player, string targetId, string targetName, string subject, string message, string type)
{
    Puts("OnPlayerReported работает!");
    return null;
}
```

## OnPhotoCapture(PhotoEntity,Item,BasePlayer,byte[])

### Summary


### Parameters
- `photoEntity`: Сущность фотографии.
- `item`: Объект, используемый для съемки фотографии.
- `player`: Игрок, который сделал фотографию.
- `imageData`: Данные изображения.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhotoCapture(PhotoEntity photoEntity, Item item, BasePlayer player, byte[] imageData)
{
    // Минимальный код для демонстрации функциональности
    Puts("Фотография снята!");
}
```

## CanExplosiveStick(TimedExplosive,BaseEntity)

### Summary


### Parameters
- `explosive`: Взрывной шнур.
- `entity`: Сущность, к которой пытаются приклеить взрывной шнур.

### Returns
Возвращает true, если можно приклеить взрывной шнур, и false в противном случае.

### Example
```csharp
bool CanExplosiveStick(TimedExplosive explosive, BaseEntity entity)
{
    Puts("CanExplosiveStick работает!");
    return true; // или другое значение в зависимости от функциональности
}
```

## OnVehicleLockableCheck(ModularCarCodeLock)

### Summary


### Parameters
- `lockable`: Объект, который необходимо проверить.

### Returns
Возвращает true, если транспортное средство может иметь замок, и false в противном случае.

### Example
```csharp
bool OnVehicleLockableCheck(ModularCarCodeLock lockable)
{
    Puts("OnVehicleLockableCheck работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## CanAdministerVending(BasePlayer,VendingMachine)

### Summary


### Parameters
- `player`: Игрок, который пытается администрировать автомат.
- `vendingMachine`: Автомат по продаже товаров.

### Returns
Возвращает true, если игрок может администрировать автомат, и false в противном случае.

### Example
```csharp
bool CanAdministerVending(BasePlayer player, VendingMachine vendingMachine)
{
    Puts("CanAdministerVending работает!");
    // Если ReturnType - bool, верните значение
    return true; // Или другое значение в зависимости от функциональности метода
}
```

## OnItemResearched(ResearchTable,int)

### Summary
Документация для метода `OnItemResearched`:

### Parameters
- `researchTable`: Таблица исследования.
- `amount`: Количество предметов, использованных в исследовании.

### Returns
Возвращает количество предметов, которые были использованы в исследовании.

### Example
```csharp
Документация для метода `OnItemResearched`:

```rust
int OnItemResearched(ResearchTable researchTable, int amount)
{
    Puts("OnItemResearched вызван!");
    return amount;
}
```

В этом методе используется `interface_callhook` для вызова хука `OnItemResearched`, который возвращает количество предметов, использованных в исследовании. Возвращаемое значение используется для определения количества предметов, которые необходимо использовать или удалить из инвентаря.
```

## OnPhotoCaptured(PhotoEntity,Item,BasePlayer,byte[])

### Summary


### Parameters
- `photoEntity`: Сущность фотографии.
- `item`: Объект, с помощью которого была сделана фотография.
- `player`: Игрок, который сделал фотографию.
- `imageData`: Данные фотографии.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPhotoCaptured(PhotoEntity photoEntity, Item item, BasePlayer player, byte[] imageData)
{
    // Минимальный код для демонстрации функциональности
    Puts("Фотография зафиксирована");
}
```

## OnRemoveDying(GrowableEntity,BasePlayer)

### Summary


### Parameters
- `entity`: Сущность растительного типа.
- `player`: Игрок, который удаляет сущность.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRemoveDying(GrowableEntity entity, BasePlayer player)
{
    Puts("OnRemoveDying работает!");
    return null;
}
```

## OnPlayerAttack(BasePlayer,HitInfo)

### Summary


### Parameters
- `player`: Игрок, совершивший атаку.
- `hitInfo`: Информация о хите.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerAttack(BasePlayer player, HitInfo hitInfo)
{
    Puts("OnPlayerAttack работает!");
    return null;
}
```

## OnMlrsFired(MLRS,BasePlayer)

### Summary


### Parameters
- `mlrs`: Объект MLRS.
- `owner`: Владелец MLRS.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnMlrsFired(MLRS mlrs, BasePlayer owner)
{
    Puts("OnMlrsFired вызван!");
}
```

## CanUseLockedEntity(BasePlayer,CodeLock)

### Summary


### Parameters
- `player`: Игрок, пытающийся открыть сущность.
- `entity`: Защищенная сущность.

### Returns
Возвращает true, если игрок может использовать сущность, и false в противном случае.

### Example
```csharp
bool CanUseLockedEntity(BasePlayer player, CodeLock entity)
{
    Puts("CanUseLockedEntity работает!");
    return true; // Игрок может использовать сущность по умолчанию
}
```

## OnPlayerLootEnd(PlayerLoot)

### Summary


### Parameters
- `loot`: Объект PlayerLoot, который вызвал этот хук.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerLootEnd(PlayerLoot loot)
{
    Puts("Процесс поиска и сбора предметов завершен!");
}
```

## CanBeHomingTargeted(AttackHeliPilotFlare)

### Summary


### Parameters
- `homingFlare`: Объект-наводка.

### Returns
Возвращает <c>true</c>, если объект может быть целью для наведения, и <c>false</c> в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(AttackHeliPilotFlare homingFlare)
{
    Puts("CanBeHomingTargeted работает!");
    return true;
}
```

## OnRemoteIdentifierUpdate(PoweredRemoteControlEntity,string)

### Summary


### Parameters
- `entity`: Объект удаленного контроля.
- `newID`: Новый идентификатор.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnRemoteIdentifierUpdate(PoweredRemoteControlEntity entity, string newID)
{
    Puts("OnRemoteIdentifierUpdate работает!");
    return null;
}
```

## OnEntitySnapshot(BaseNetworkable,Network.Connection)

### Summary


### Parameters
- `entity`: Сущность, для которой отправляется снимок.
- `connection`: Подключение к серверу.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnEntitySnapshot(BaseNetworkable entity, Network.Connection connection)
{
    Puts("OnEntitySnapshot вызван!");
    return null;
}
```

## OnPlayerKeepAlive(BasePlayer,BasePlayer)

### Summary


### Parameters
- `player`: Игрок, который прислал сигнал.
- `targetPlayer`: Игрок, для которого был отправлен сигнал.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerKeepAlive(BasePlayer player, BasePlayer targetPlayer)
{
    Puts("OnPlayerKeepAlive работает!");
    return null;
}
```

## OnCargoPlaneSignaled(BaseEntity,SupplySignal)

### Summary


### Parameters
- `entity`: Объект, который вызывает сигнал.
- `signal`: Тип сигнала.

### Returns
No return value.

### Example
```csharp
void OnCargoPlaneSignaled(BaseEntity entity, SupplySignal signal)
{
    Puts("OnCargoPlaneSignaled работает!");
}
```

## OnBigWheelWin(BigWheelGame,Item,BigWheelBettingTerminal,int)

### Summary


### Parameters
- `game`: Объект игры.
- `item`: Выигранное предмет.
- `terminal`: Терминал ставок.
- `amount`: Количество выигранных денег.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBigWheelWin(BigWheelGame game, Item item, BigWheelBettingTerminal terminal, int amount)
{
    Puts("OnBigWheelWin работает!");
    return null;
}
```

## CanEntityBeHostile(BasePlayer)

### Summary


### Parameters
- `entity`: Сущность.

### Returns
Возвращает true, если сущность может быть враждебной, и false в противном случае.

### Example
```csharp
bool CanEntityBeHostile(BasePlayer entity)
{
    Puts("CanEntityBeHostile работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnSamSiteModeToggle(SamSite,BasePlayer,bool)

### Summary


### Parameters
- `samSite`: Самосайт.
- `player`: Игрок, который вызвал хук.
- `enabled`: Новый режим самосайта.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSamSiteModeToggle(SamSite samSite, BasePlayer player, bool enabled)
{
    Puts("OnSamSiteModeToggle работает!");
    return null;
}
```

## OnHelicopterAttack(CH47HelicopterAIController,HitInfo)

### Summary


### Parameters
- `helicopter`: Контроллер вертолета.
- `info`: Информация о нападении.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHelicopterAttack(CH47HelicopterAIController helicopter, HitInfo info)
{
    Puts("OnHelicopterAttack работает!");
    return null;
}
```

## OnSleepingBagDestroyed(SleepingBag,ulong)

### Summary


### Parameters
- `sleepingBag`: Уничтоженная спальнная сумка.
- `userID`: ID пользователя, который владел спальнной сумкой.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnSleepingBagDestroyed(SleepingBag sleepingBag, ulong userID)
{
    Puts("OnSleepingBagDestroyed работает!");
    return null;
}
```

## CanAdministerVending(BasePlayer,NPCVendingMachine)

### Summary


### Parameters
- `player`: Игрок, который пытается администрировать автомат.
- `vendingMachine`: Автомат по продаже товаров.

### Returns
Возвращает true, если игрок может администрировать автомат, и false в противном случае.

### Example
```csharp
bool CanAdministerVending(BasePlayer player, NPCVendingMachine vendingMachine)
{
    Puts("CanAdministerVending работает!");
    return true; // Возвращаемое значение по умолчанию
}
```

## OnHelicopterTarget(HelicopterTurret,BaseCombatEntity)

### Summary


### Parameters
- `turret`: Вертолет.
- `newTarget`: Новая цель.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnHelicopterTarget(HelicopterTurret turret, BaseCombatEntity newTarget)
{
    Puts("OnHelicopterTarget работает!");
    return null;
}
```

## OnFishCaught(ItemDefinition,BaseFishingRod,BasePlayer)

### Summary
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
This is a C# code snippet that appears to be part of a fishing mini-game in the game Rust. Here's a breakdown of what it does:

**Main Loop**

The code runs in a loop until the fish is caught or the process fails.

**Flag Management**

The code manages several flags, which are used to track the state of the fishing process. These flags include:

* `flag`: Whether the player has pulled on the line.
* `flag2`: Whether the player has pulled on the line in a specific direction (left or right).
* `flag3`: Whether the player is pulling back on the line.

The code updates these flags based on user input and the current state of the fishing process.

**Fish State Management**

The code manages the state of the fish, which can be one of several states:

* `FishState.PullingBack`
* `FishState.PullingLeft`
* `FishState.PullingRight`

The code updates the fish state based on user input and the current state of the fishing process.

**Strain Timer**

The code has a strain timer that increments based on the player's actions. When the strain timer reaches 7 seconds, the fishing process fails.

**Client RPCs**

The code sends client-side RPCs to update the client's view of the fishing process. These RPCs include:

* `RpcTarget.NetworkGroup("Client_UpdateFishState")`: Updates the client's fish state.
* `RpcTarget.NetworkGroup("Client_OnCaughtFish")`: Notifies the client that a fish has been caught.

**Achievement Checking**

The code checks if the player has achieved a specific achievement related to catching all types of fish.

Overall, this code snippet appears to be responsible for managing the fishing mini-game in Rust, including updating flags and fish states, checking achievements, and sending client-side RPCs.
```

## CanCreateWorldProjectile(HitInfo,ItemDefinition)

### Summary


### Parameters
- `info`: Информация о выстреле.
- `itemDef`: Определение предмета.

### Returns
Возвращает true, если поведение по умолчанию не переопределено.

### Example
```csharp
bool CanCreateWorldProjectile(HitInfo info, ItemDefinition itemDef)
{
    Puts("CanCreateWorldProjectile работает!");
    return true;
}
```

## OnInventoryItemsCount(PlayerInventory,int)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `itemid`: ID предмета.

### Returns
Количество предметов с заданным ID в инвентаре игрока.

### Example
```csharp
int OnInventoryItemsCount(PlayerInventory inventory, int itemid)
{
    Puts("OnInventoryItemsCount вызван!");
    return 0; // Возвращаемое значение по умолчанию
}
```

## OnMlrsRocketFired(MLRS,ServerProjectile)

### Summary


### Parameters
- `mlrs`: Объект MLRS, который запускает ракету.
- `projectile`: Запущенная ракета.

### Returns
No return value.

### Example
```csharp
object OnMlrsRocketFired(MLRS mlrs, ServerProjectile projectile)
{
    Puts("Ракета MLRS запущена!");
    return null;
}
```

## OnBackpackDrop(Item,PlayerInventory)

### Summary


### Parameters
- `item`: Сбрасываемый рюкзак.
- `inventory`: Инвентарь игрока, пытаясь сбросить рюкзак.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnBackpackDrop(Item item, PlayerInventory inventory)
{
    Puts("OnBackpackDrop работает!");
    return null;
}
```

## CanDemolish(BasePlayer,StabilityEntity)

### Summary


### Parameters
- `player`: Игрок, пытающийся разрушить сущность.
- `entity`: Сущность, которую хочет разрушить игрок.

### Returns
Возвращает true, если демонтаж разрешен, и false в противном случае.

### Example
```csharp
bool CanDemolish(BasePlayer player, StabilityEntity entity)
{
    Puts("CanDemolish работает!");
    return true; // или другое значение в зависимости от функциональности
}
```

## OnEntityVisibilityCheck(BaseEntity,BasePlayer,uint,string,float)

### Summary


### Parameters
- `entity`: Сущность, которую необходимо проверить.
- `player`: Игрок, который проверяет видимость.
- `id`: Идентификатор события.
- `debugName`: Название события для отладки.
- `maximumDistance`: Максимальная дистанция проверки видимости.

### Returns
Возвращает true, если сущность видима игроку, и false в противном случае.

### Example
```csharp
bool OnEntityVisibilityCheck(BaseEntity entity, BasePlayer player, uint id, string debugName, float maximumDistance)
{
    Puts("OnEntityVisibilityCheck вызван!");
    
    // Если сущность или игрок не определены, возвращаем false
    if (entity == null || player == null)
    {
        return false;
    }
    
    // Вызываем хук и проверяем его результат
    object obj = Interface.CallHook("OnEntityVisibilityCheck", entity, player, id, debugName, maximumDistance);
    if (obj is bool)
    {
        return (bool)obj;
    }
    
    // Проверяем линию видимости игрока на сущность
    if (GamePhysics.LineOfSight(player.eyes.center, player.eyes.position, 1218519041))
    {
        // Если сущность не видна игроку в прямой видимости, проверяем ее видимость по позиции
        if (!entity.IsVisible(player.eyes.HeadRay(), 1218519041, maximumDistance))
        {
            return entity.IsVisible(player.eyes.position, maximumDistance);
        }
        
        // Если сущность видна игроку в прямой видимости, возвращаем true
        return true;
    }
    
    // Если линия видимости игрока не проходит через сущность, возвращаем false
    return false;
}
```

## CanUpdateSign(BasePlayer,CarvablePumpkin)

### Summary


### Parameters
- `player`: Игрок, пытающийся обновить знак.
- `pumpkin`: Карванный лукошник.

### Returns
Возвращает true, если игрок может обновить знак, и false в противном случае.

### Example
```csharp
bool CanUpdateSign(BasePlayer player, CarvablePumpkin pumpkin)
{
    Puts("CanUpdateSign работает!");
    return true;
}
```

## OnPlayerKicked(BasePlayer,string)

### Summary


### Parameters
- `player`: Выкинутый игрок.
- `reason`: Причина выкидывания.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPlayerKicked(BasePlayer player, string reason)
{
    Puts($"Игрок {player.Name} выкинут из сервера за причину: {reason}");
    return null;
}
```

## OnExperimentStart(Workbench,BasePlayer)

### Summary


### Parameters
- `workbench`: Рабочая столешка.
- `player`: Игрок.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnExperimentStart(Workbench workbench, BasePlayer player)
{
    Puts("OnExperimentStart работает!");
}
```

## CanSetRelationship(BasePlayer,BasePlayer,RelationshipManager.RelationshipType,int)

### Summary


### Parameters
- `player`: Игрок, который устанавливает отношение.
- `otherPlayer`: Игрок, к которому устанавливается отношение.
- `type`: Тип отношения.
- `weight`: Вес отношения.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void CanSetRelationship(BasePlayer player, BasePlayer otherPlayer, RelationshipManager.RelationshipType type, int weight)
{
    Puts("CanSetRelationship работает!");
}
```

## OnPlayerSleepEnd(BasePlayer)

### Summary


### Parameters
- `player`: Игрок, который вышел из сна.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnPlayerSleepEnd(BasePlayer player)
{
    Puts("OnPlayerSleepEnd работает!");
}
```

## OnMissionStart(BaseMission,BaseMission.MissionInstance,BasePlayer)

### Summary


### Parameters
- `mission`: Миссия.
- `instance`: Экземпляр миссии.
- `assignee`: Игрок, которому назначена миссия.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnMissionStart(BaseMission mission, BaseMission.MissionInstance instance, BasePlayer assignee)
{
    Puts("OnMissionStart работает!");
    return null;
}
```

## CanBuild(Planner,Construction,Construction.Target)

### Summary
Документация для CanBuild(Planner, Construction, Construction.Target)

### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
Документация для CanBuild(Planner, Construction, Construction.Target)

**Описание**

Метод `CanBuild` вызывается в методе `DoBuild` и используется для проверки возможности построения конструкции на заданном месте.

**Параметры**

* `planner`: Объект плана, который содержит информацию о конструкции.
* `construction`: Объект строительства, который содержит информацию о конкретной конструкции.
* `target`: Объект цели, который содержит информацию о месте, где будет построена конструкция.

**Возвращаемое значение**

Метод возвращает null, если возможность построения не проверяется или если проверка проходит успешно. Если проверка не пройдет, метод вернет значение, которое указывает на причину отказа.

**Примечания**

* Метод вызывается только в том случае, если конструкция имеет свойство `canBypassBuildingPermission`, что означает, что она может быть построена без разрешения.
* Если конструкция не имеет этого свойства, метод вернет значение, которое указывает на причину отказа.

**Пример использования**

```csharp
public void DoBuild(CreateBuilding msg)
{
    // ...
    if (Interface.CallHook("CanBuild", this, construction, target) != null)
    {
        return;
    }
    // ...
}
```

В этом примере метод `DoBuild` вызывает метод `CanBuild`, передавая в него объекты плана, строительства и цели. Если метод `CanBuild` вернет значение, которое указывает на причину отказа, метод `DoBuild` вернет это же значение.
```

## OnInventoryNetworkUpdate(PlayerInventory,ItemContainer,ProtoBuf.UpdateItemContainer,PlayerInventory.Type,PlayerInventory.NetworkInventoryMode)

### Summary


### Parameters
- `inventory`: Инвентарь игрока.
- `container`: Контейнер, содержащий информацию о обновлении.
- `updateItemContainer`: Объект ProtoBuf.UpdateItemContainer с информацией о обновлении.
- `type`: Тип инвентаря (PlayerInventory.Type).
- `mode`: Режим обновления (PlayerInventory.NetworkInventoryMode).

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnInventoryNetworkUpdate(PlayerInventory inventory, ItemContainer container, ProtoBuf.UpdateItemContainer updateItemContainer, PlayerInventory.Type type, PlayerInventory.NetworkInventoryMode mode)
{
    Puts("OnInventoryNetworkUpdate работает!");
    return null;
}
```

## OnTeamDisband(RelationshipManager.PlayerTeam)

### Summary


### Parameters
- `team`: Распущенная команда.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnTeamDisband(RelationshipManager.PlayerTeam team)
{
    Puts("OnTeamDisband работает!");
    return null;
}
```

## CanCheckFuel(EntityFuelSystem,StorageContainer,BasePlayer)

### Summary


### Parameters
- `fuelSystem`: Система топлива.
- `container`: Контейнер с топливом.
- `player`: Игрок, пытающийся проверить уровень топлива.

### Returns
Возвращает true, если игрок может проверить уровень топлива, и false в противном случае.

### Example
```csharp
bool CanCheckFuel(EntityFuelSystem fuelSystem, StorageContainer container, BasePlayer player)
{
    Puts("CanCheckFuel работает!");
    return true;
}
```

## CanBeHomingTargeted(CH47Helicopter)

### Summary


### Parameters
- `helicopter`: Экземпляр CH47Helicopter.

### Returns
Возвращает true, если это можно сделать, и false в противном случае.

### Example
```csharp
bool CanBeHomingTargeted(CH47Helicopter helicopter)
{
    Puts("CanBeHomingTargeted работает!");
    return true; // или другое значение в зависимости от функциональности
}
```

## OnEntityDismounted(BaseMountable,BasePlayer)

### Summary


### Parameters
- `entity`: Объект, с которого был снят игрок.
- `player`: Игрок, который был снят.

### Returns
No return value.

### Example
```csharp
void OnEntityDismounted(BaseMountable entity, BasePlayer player)
{
    // Минимальный код для демонстрации функциональности
    Puts($"Игрок {player.displayName} снят со своего объекта: {entity.gameObject.name}");
}
```

## OnActiveItemChanged(BasePlayer,Item,Item)

### Summary


### Parameters
- `player`: Игрок, чей активный предмет изменился.
- `oldItem`: Старый активный предмет игрока.
- `newItem`: Новый активный предмет игрока.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnActiveItemChanged(BasePlayer player, Item oldItem, Item newItem)
{
    Puts("OnActiveItemChanged работает!");
    return null;
}
```

## OnSendCommand(System.Collections.Generic.List<Network.Connection>,string,object[])

### Summary


### Parameters
- `connections`: Список подключений.
- `command`: Команда для отправки.
- `args`: Аргументы команды.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnSendCommand(List<Network.Connection> connections, string command, object[] args)
{
    Puts($"Предварительно вызван хук OnSendCommand для команды {command} с аргументами: {args}");
}
```

## IOnServerShutdown()

### Summary


### Parameters
No parameters.

### Returns
No return value.

### Example
```csharp
void IOnServerShutdown()
{
    Puts("Сервер закрывается!");
}
```

## OnDecayHeal(DecayEntity)

### Summary


### Parameters
- `entity`: Сущность, восстанавливаящаяся.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnDecayHeal(DecayEntity entity)
{
    Puts("OnDecayHeal работает!");
}
```

## OnItemCraftCancelled(ItemCraftTask,ItemCrafter)

### Summary


### Parameters
- `task`: Задача по изготовлению предмета.
- `crafter`: Сущность, выполняющая задачу.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnItemCraftCancelled(ItemCraftTask task, ItemCrafter crafter)
{
    Puts($"Задача по изготовлению предмета '{task.blueprint.targetItem}' отменена.");
}
```

## OnPhoneDialTimedOut(PhoneController,PhoneController,BasePlayer)

### Summary


### Parameters
- `phoneController`: Контроллер телефона.
- `player`: Игрок, который пытался вызвать.
- `caller`: Контроллер телефона вызывающего игрока.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object OnPhoneDialTimedOut(PhoneController phoneController, PhoneController caller, BasePlayer player)
{
    Puts("OnPhoneDialTimedOut работает!");
    return null;
}
```

## OnBookmarkControlEnded(ComputerStation,BasePlayer,BaseEntity)

### Summary


### Parameters
- `computerStation`: Компьютерная станция.
- `player`: Игрок.
- `entity`: Сущность.

### Returns
No return value.

### Example
```csharp
object OnBookmarkControlEnded(ComputerStation computerStation, BasePlayer player, BaseEntity entity)
{
    Puts("Контроль над сущностью закончен!");
    return null;
}
```

## IOnCupboardAuthorize(ulong,BasePlayer,BuildingPrivlidge)

### Summary


### Parameters
- `id`: Идентификатор шкафа.
- `player`: Авторизируемый игрок.
- `privilege`: Права доступа к шкафу.

### Returns
Возвращает ненулевое значение, если поведение по умолчанию переопределено.

### Example
```csharp
object IOnCupboardAuthorize(ulong id, BasePlayer player, BuildingPrivlidge privilege)
{
    Puts("IOnCupboardAuthorize работает!");
    return null;
}
```

## OnFishingRodCast(BaseFishingRod,BasePlayer,Item)

### Summary


### Parameters
- `fishingRod`: Рыболовный укас.
- `player`: Игрок, который запустил укас.
- `lure`: Наживка.

### Returns
Нет поведения возвращаемого значения.

### Example
```csharp
void OnFishingRodCast(BaseFishingRod fishingRod, BasePlayer player, Item lure)
{
    // Минимальный код для демонстрации функциональности
    Puts("Рыболовный укас запущен.");
}
```
