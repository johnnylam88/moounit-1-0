Overview
--------

[MooUnit-1.0][project] is a library that provides mappings between GUIDs, unit IDs, and names.

The unit IDs tracked by the library are:

* `"player"`
* `"vehicle"`
* `"pet"`, `"pettarget"`
* `"target"`, `"targettarget"`
* `"focus"`, `"focustarget"`
* `"arena1"`, `...`, `"arena5"`
* `"arena1target"`, `...`, `"arena5target"`
* `"arenapet1"`, `...`, `"arenapet5"`
* `"arenapet1target"`, `...` `"arenapet5target"`
* `"boss1"`, `...`, `"boss5"`
* `"boss1target"`, `...`, `"boss5target"`
* `"party1"`, `...`, `"party4"`
* `"party1target"`, `...`, `"party4target"`
* `"partypet1"`, `...`, `"partypet4"`
* `"partypet1target"`, `...`, `"partypet4target"`
* `"raid1"`, `...`, `"raid40"`
* `"raid1target"`, `...`, `"raid40target"`
* `"raidpet1"`, `...`, `"raidpet40"`
* `"raidpet1target"`, `...`, `"raidpet40target"`
* `"nameplate1"`, `...`
* `"nameplate1target"`, `...`

API Methods
-----------

### HasUnitEvents

Returns whether the unit ID receives unit events, e.g., `UNIT_AURA`, `UNIT_TARGET`, etc.

    boolean = lib:HasUnitEvents(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `boolean` - boolean: `true` if the unit receives unit events, or `false` otherwise

### GetGUIDByUnit

Returns the GUID currently associated with the unit.

    guid = lib:GetGUIDByUnit(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `guid` - string: [GUID][] of the unit

### GetUnitByGUID

Returns a list of units currently associated with the GUID.

    unit1, unit2, ..., unitN = lib:GetUnitByGUID(guid)

#### Arguments:

* `guid` - string: [GUID][]

#### Returns:

* `unit1, unit2, ..., unitN` - list of strings: variable-length list of [unit ID][] strings

### GetNameByUnit

Returns the name currently associated with the unit.

    name = lib:GetNameByUnit(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `name` - string: the name of the unit, `name` or `name-realm`

### GetUnitByName

Returns a list of units currently associated with the name.

    unit1, unit2, ..., unitN = lib:GetUnitByName(name)

#### Arguments:

* `name` - string: `name` or `name-realm`

#### Returns:

* `unit1, unit2, ..., unitN` - list of strings: variable-length list of [unit ID][] strings

### GetNameByGUID

Returns the name currently associated with the GUID.

    name = lib:GetNameByGUID(guid)

#### Arguments:

* `guid` - string: [GUID][]

#### Returns:

* `name` - string: the name associated with the GUID, `name` or `name-realm`

### GetGUIDByName

Returns a list of GUIDs currently associated with the name.

    guid1, guid2, ..., guidN = lib:GetGUIDByName(name)

#### Arguments:

* `name` - string: `name` or `name-realm`

#### Returns:

* `guid1, guid2, ..., guidN` - list of strings: variable-length list of [GUID][] strings

### GetPetUnitByUnit

Returns the unit ID assigned to the pet for the unit, even if the pet does not exist.

    petUnit = lib:GetPetUnitByUnit(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `petUnit` - string: [unit ID], e.g., `"pet"`, `"partypet1"`, `"raidpet15"`, etc.

### GetOwnerGUIDByGUID

Returns the GUID of the owner of the pet or vehicle GUID if both are on the group roster.

    ownerGUID = lib:GetOwnerGUIDByGUID(guid)

#### Arguments:

* `guid` - string: [GUID][] of the pet or vehicle

#### Returns:

* `ownerGUID` - string: [GUID][] of the owner

### GetTargetUnitByUnit

Returns the unit ID assigned to the target for the unit, even if the target does not exist.

    targetUnit = lib:GetTargetUnitByUnit(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `targetUnit` - string: [unit ID], e.g., `"target"`, `"party1target"`, `"raid15target"`, etc.

### IsGUIDInGroup

Returns whether the GUID is on the group roster.

    boolean = lib:IsGUIDInGroup(guid)

#### Arguments:

* `guid` - string: [GUID][] to test group membership

#### Returns:

* `boolean` - boolean: `true` if the unit is on the group roster, or `false` otherwise

### IsGroupUnit

Returns whether the unit ID exists and is a group unit ID, e.g., `"partypet1"`, `"raid15"`, etc.

    boolean = lib:IsGroupUnit(unit)

#### Arguments:

* `unit` - string: [unit ID], e.g., `"player"`, `"party1"`, `"raid15"`, etc.

#### Returns:

* `boolean` - boolean: `true` if the unit exists and is a group unit ID, or `false` otherwise

### IterateRoster

Returns an iterator that gives key-value pairs of GUID and unit ID for members on the group roster.

    for guid, unit in lib:IteratorRoster() do
        ...
    end

### RegisterCallback

Registers a function to handle the specified callback.

    lib.RegisterCallback(handler, callback, method, arg)

#### Arguments:

* `handler` - table/string: your addon object or another table containing a function at `handler[method]`, or a string identifying your addon
* `callback` - string: the name of the callback to be registered
* `method` - string/function/nil: a key into the `handler` table, or a function to be called, or `nil` if `handler` is a table and a function exists at `handler[callback]`
* `arg` - a value to be passed as the first argument to the callback function specified by `method`

#### Notes:

* If `handler` is a table, `method` is a string, and `handler[method]` is a function, then that function will be called with `handler` as its first argument, followed by the callback name and the callback-specific arguments.
* If `handler` is a table, `method` is nil, and `handler[callback]` is a function, then that function will be called with `handler` as its first argument, followed by the callback name and the callback-specific arguments.
* If `handler` is a string and `method` is a function, then that function will be called with the callback name as its first argument, followed by the callback-specific arguments.
* If `arg` is non-nil, then it will be passed to the specified function. If `handler` is a table, then `arg` will be passed as the second argument, pushing the callback name to the third position. Otherwise, `arg` will be passed as the first argument.

### UnregisterCallback

Unregisters a specified callback.

    lib.UnregisterCallback(handler, callback)

#### Arguments:

* `handler` - table/string: your addon object or a string identifying your addon
* `callback` - string: the name of the callback to be unregistered


Callbacks
---------

__MooUnit-1.0__ provides the following callbacks to notify interested addons.

### MooUnit_PetChanged

Fires when the pet associated with an owner has changed.  This can happen if a pet is dismissed and a new pet is summoned.

#### Arguments:

* `ownerGUID` - string: [GUID][] of the pet owner
* `ownerUnit` - string: [unit ID][] of the pet owner
* `petGUID` - string: [GUID][] of the pet
* `petUnit` - string: [unit ID][] of the pet

### MooUnit_RosterUpdated

Fires when the roster of the party or raid group has changed.

### MooUnit_UnitChanged

Fires when a unit that we are tracking has changed.

#### Arguments:

* `guid` - string: [GUID][] associated with the unit ID
* `unit` - string: [unit ID] of the unit that has changed
* `name` - string: the current name associated with the unit ID.

### MooUnit_UnitJoined

Fires when a new member is added to the group roster.

#### Arguments:

* `guid` - string: [GUID][] of the member that joined the group
* `unit` - string: [unit ID][] of the member that joined the group

### MooUnit_UnitLeft

Fires when a member is removed from the group roster.

#### Arguments:

* `guid` - string: [GUID][] of the member that left the group


License
-------
__MooUnit-1.0__ is released under the 2-clause BSD license.


Feedback
--------

+ [Report a bug or suggest a feature][project-issue-tracker].

  [project]: https://www.github.com/ultijlam/moounit-1-0
  [project-issue-tracker]: https://github.com/ultijlam/moounit-1-0/issues
  [GUID]: https://wow.gamepedia.com/GUID
  [unit ID]: https://wow.gamepedia.com/UnitId