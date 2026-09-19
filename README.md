# Zenith Forge

**Stop wiring activities by hand.** A Foundry VTT module for D&D 5e that turns
"what does this ability do?" into a finished activity — attack roll, damage,
saving throw, and the Active Effect that grants conditions and bonuses, all
linked together correctly.

> เลิกต่อ activity ทีละชิ้น — ตอบเป็นภาษาคน แล้วได้ to-hit / damage / save / buff ที่ผูกกันถูกแล้ว

## At a glance

| | |
|---|---|
| **One window** | Four plain questions for a feature or a spell, five steps for a magic item, two for the library — and every bonus, condition and stat change picked in the window itself |
| **Preset library** | 103 presets in 10 groups — 24 weapons, 71 features, 8 real spells |
| **Magic item wizard** | 21 item kinds, 8 kinds of power, charges, +1/+2/+3, spell casting with upcast — in the same window |
| **Icon picker** | ~7,300 pictures across 13 shipped folders, plus a folder of your own |
| **Who can use it** | Gamemaster only out of the box; two role settings if you want to share it |
| **Edit what exists** | Read any activity back into the same four questions and write over it — yours, the system's, a compendium's |
| **Tested** | 642 assertions, none of which need Foundry running |

### One button

There used to be four, and the first thing anyone had to work out was which of
them they wanted. **Create** is now the only one, and the window asks that
question itself.

| Open it from | What happens |
|---|---|
| An item sheet — Activities tab or the header menu | Opens on that item, ready to give it another use |
| The hammer on one activity’s row | Opens that use, filled in, ready to change |
| A creature sheet — Features or Inventory tab, or the header menu | Opens with the tab you pressed it on already chosen, and every other choice still one click away |
| The Items sidebar | Opens with nothing assumed |
| Right-click an item row · click a picture on an item sheet · drop an image file · hover and press Ctrl+V | **Change icon**, as before |

## The problem it solves

One homebrew ability like *"melee attack, 2d6 fire, DC 15 DEX save or knocked prone"*
normally means building three separate things and knowing how they connect:

1. an **Attack activity** — `attack.type.value`, `attack.type.classification`, and damage
   parts stored as `number` / `denomination` / `types`, not as text
2. a **Save activity** — where `save.ability` is an *array*, plus `save.dc.calculation`
   and `damage.onSave`
3. an **ActiveEffect** — a separate document with `statuses`, changes, and a duration,
   whose `_id` then has to be pasted back into the activity's `effects` list

Zenith Forge writes all three and links them.

## How it works

Press **Create**. The first step asks what you are making — a feature or action,
a spell, a magic item, another use for the item you already have open, or a
change to something that exists already — and everything after that is the
questions that thing actually needs.

The rule the whole window follows is **ask only what is needed, and only when it
is needed**. A control appears once the answer before it makes the question
meaningful, and never before: choose "attack roll" and the reach appears; choose
"a saving throw" and the DC does; *how long does it last* stays away entirely
until something on the thing actually lingers. Nothing is drawn and then quietly
ignored.

For a feature, a spell, or an existing item, that is four plain questions —
what it is called, how it is used, how it lands and on whom, and what happens
then. A monster's bite is five answers.

- **How it lands** — an attack roll, a saving throw, "it just happens", or no
  damage at all. That one answer decides the kind of activity written, so the
  question is asked once instead of being spread over three sections
- **On whom** — yourself, one target, or an area, with the shape and size
  appearing only for an area
- **What happens then** — stack on damage, healing, a condition, or a bonus, in
  any combination. Each is added by name and expands to the two or three fields
  it needs
- **A hit that forces a save** — like Topple: choose an attack roll and the next
  question is whether a hit must also make a save. Set it once — the ability, a
  DC that can be 8 + a modifier + proficiency, and in words anything the system
  cannot do ("pushed 10 ft") — then mark which damage, condition or bonus waits
  for a failure. It is written as a second activity on the same item; with
  Midi-QOL it is rolled for the targets hit, or from the button on the attack's
  chat card, and a failure applies the condition
- **Normal and long range** — an attack built for an NPC is a natural weapon, as
  the official monsters' are, so a ranged one can be 60/120 ft
- **Answer in plain language** — damage is typed the way you say it (`2d6 + 3`)
  and split into the structured shape the system wants
- **A sentence at the bottom** shows what will read on the sheet, and updates as
  you go. It is written in the same words you chose, never in the system's
  internal names for things
- **Grant conditions by ticking them** — the effect gets the right `statuses`,
  a duration derived from the ability's duration, and, on a save activity,
  lands only on a failed save unless you say otherwise
- **Add bonuses by name, without leaving the window** — all 54 are listed beside
  the thing you are building with a search box above them, so you pick "AC bonus"
  or "Advantage on all saves" instead of remembering
  `system.attributes.ac.bonus`. Midi-QoL entries appear only when Midi-QoL is
  active. This used to open a second window, and it was the biggest single reason
  the module felt like a maze.
- **Pick an icon by looking at it** — a grid of real pictures with a search box,
  instead of reading filenames in a file browser: ~7,300 images across 13 folders
  from Foundry and dnd5e, plus your own uploads as a fourteenth
- **Drag or paste an image straight in** — drop a PNG from your desktop onto the
  icon well (or into the icon picker), or copy a picture anywhere and press
  Ctrl+V over an icon. Either way it is uploaded to the module's own persistent
  storage and used immediately; no file dialog, no manual copying
- **Deep mode** exposes every raw field, including custom attribute keys

### Changing something that already exists

The same four questions, filled in from what is already there. Press the hammer
on a row of an item's Activities tab, or pick *Change something that exists* on
the wizard's first question and choose the item and the use from two lists.

- It reads back **anything**, not only what this module built: a spell from the
  system, a monster feature from a compendium, an item somebody imported
- The item's own **name and icon** are edited in the same window, and written
  only when you change them. The description is left alone
- A **save that follows a hit** comes with the attack and is saved with it, with
  or without Midi-QOL; switch it off and it is removed
- **Only what the wizard asks about is written back.** How a spell scales, what
  it consumes, an enchantment, another module's settings — all untouched. So are
  the damage a successful save still takes, an effect's own name and whether it
  lands on a success: not asked about, and not reset either

### Changing the icon of something that already exists

The picker is not limited to what the Forge builds. On any dnd5e sheet or list:

- **click the picture on an item sheet** (in edit mode) — the icon browser opens
  instead of Foundry's plain file list, already showing the folder the current
  icon came from. Turn it off under *Visual picker for sheet images* if you
  prefer the stock browser.
- **right-click an item row → Change icon** opens the same visual picker
- **drop an image file onto the icon** — in a row, or the portrait in a sheet
  header — uploads it and applies it in one move

Dropping a document (rather than a file) still behaves exactly as the system
intends; only image files are intercepted.

**Creature portraits and token art are left alone.** Clicking a character's or an
NPC's picture, or dropping a file on it, goes wherever it went before — most
tables run a dedicated tool for that half (Tokenizer, among others), and a second
picker fighting for the same click helps nobody. Items on a creature's sheet are
unaffected; only the creature's own pictures are. Tick *Also handle creature
portraits* if you would rather this module took them as well.

Spells keep range, target and duration on the item itself, the way the system
expects; everything else gets them on the activity with `override` set. The
summary strip at the bottom always shows exactly what pressing **Create** will make.

## The preset library

103 ready-made weapons, spells, features and traits — starting points meant to be
adjusted, not finished content. Foundry already handles a creature's CR, AC and
hit points, so the module leaves those alone; what it adds is the tedious half,
making the thing and wiring its activation.

Press **Create** and choose *Start from a ready-made one* — the library lives in
the same window as everything else now, two steps behind the first question:
**pick one**, then **adjust it**. Browse by kind — melee, ranged, spells,
features, area & saves, bonus actions, reactions, legendary, traits — or search
across all of them at once, in either language.

Picking one shows only the handful of things worth deciding: the name, the dice,
the damage type, which save and which ability sets the DC, the size of the area.
**Nothing that can be derived is ever asked for.** The to-hit comes from the
creature's own ability score and proficiency; the save DC comes from the ability
you point it at. Give a beast Strength 18 and a bite rolls `1d20 + 4 + 3` for
`1d6 + 4` damage; raise its Constitution and every breath weapon's DC follows.

The description writes itself the way the 2024 statblocks do — *"Melee Attack
Roll: +7, reach 5 ft. Hit: 7 (1d6 + 4) Piercing damage."* — and keeps agreeing
with the creature after you edit it, because it is built from enrichers rather
than baked-in numbers.

### Adjusting what a preset does

Every preset opens a panel for the part that most often needs changing:

- **Conditions** — tick Prone, Frightened, Paralyzed and the rest; the effect is
  created with the right `statuses` and linked to the activity properly
- **Stat changes** — pick by name from a searchable list of 54 (AC bonus, speed,
  saving throws, ability scores, resistances, Midi advantage) listed right there
  in the window, instead of remembering `system.attributes.ac.bonus`, then edit
  the value inline
- **How long it lasts** — a number and a unit

This works on any preset, not just the ones that ship with an effect: a plain
bite can be given "knocked Prone and −2 AC for 2 rounds" without leaving the
window. Controls that would not do anything are hidden rather than shown and
ignored — a spell has no "DC from" choice because it always uses the caster's
spellcasting ability, and an always-on trait has no duration.

Recharges, legendary costs, and Legendary Resistance's use of the creature's own
resource pool are all set up, and each action lands in the right section of the
sheet — including Bonus Actions, Reactions and Lair Actions. A grab applies the
Grappled condition and prints its own escape DC; a resistance or immunity is a
real Active Effect, so the creature actually stops taking the damage rather than
only being described as resistant.

The window stays open so you can add a whole creature's worth in one go; tick
**Open Zenith Forge afterwards** to keep building on the one you just made.

> กด **สร้าง** แล้วเลือก **เริ่มจากของสำเร็จรูป** — เลือก preset แล้วปรับชื่อ / ลูกเต๋า / เซฟ / สถานะ / stat ที่เปลี่ยน ในหน้าต่างเดียวกัน ได้ item ที่ต่อ activity ถูกแล้ว
> ค่าโจมตีกับ DC ดึงจากค่าของตัวเจ้าของเอง ไม่ต้องกรอก

## Magic items

Gear takes five steps rather than three, because there is genuinely more to say
about it — and it walks them **in the same window**, behind the same first
question. Press **Create** and choose *Magic item*.

1. **What is it** — 21 kinds across worn, held, used up and other: wondrous
   items, rings, wands, rods, staves, armour of each weight, shields, melee and
   ranged weapons, potions, scrolls, poisons, ammunition, containers, tools and
   plain treasure. The kind decides the schema; the picture is yours to choose.
2. **Name and worth** — rarity, attunement, weight, quantity, and a price that
   fills itself in from the going rate for that rarity (50 / 400 / 4,000 /
   40,000 / 200,000 gp, the medians across the SRD's own 297 priced magic items).
   Armour gets a base AC and a Dexterity cap; a weapon gets its base dice, the
   SRD weapon it **counts as**, and a **weapon mastery** — the two go together,
   because a mastery is only usable by someone who has mastery with that base
   weapon.
3. **Charges** — how many, and when they come back: at dawn or dusk on a roll
   like `1d6 + 1`, daily, on a rest, or never. A potion instead holds doses and
   destroys itself when the last one is drunk.
4. **What it grants** — conditions and stat changes, from the same searchable
   list of 54 the Forge uses. Say whether it takes hold *while worn* — a real
   `transfer` effect, which dnd5e keeps switched off until the item is equipped
   and attuned — or *when a power is used*, which is how a potion works.
5. **What it does** — any number of powers: **a spell it casts**, an attack, a
   saving throw, automatic damage, healing, a granted effect, or a
   **+1 / +2 / +3 upgrade** applied to some *other* weapon or armour. Each power
   can spend charges, and a save's DC is a number you set.

   Casting is picked from a **searchable list of every spell the world can see**,
   filtered by level. The item stores only the spell's uuid, the level to cast it
   at and what it costs — the spell keeps its own range, target, duration and
   casting time — and the components are stripped by default, because you do not
   wave your hands at a wand. Allow **extra charges** and it upcasts the way the
   Wand of Magic Missiles does: one more charge per spell level, and the offer
   shrinks by itself as the item empties.

**Nothing is written down that dnd5e can work out.** A magic bonus goes to
`system.magicalBonus` (or `system.armor.magicalBonus`) so it reaches the roll
and the AC, rather than being described in the text; charges are real
`system.uses` with a recovery profile; and every item carries the `mgc`
property, without which the system silently clears attunement and ignores the
bonus entirely.

Every activity the wizard writes is marked **requires identification**, the way
278 of the SRD's magic item activities are and none of its mundane ones: while an
item is unidentified a player sees neither its description nor its powers.

The description writes itself in the SRD's own voice — *"Wand, Rare (requires
attunement). This item has 7 charges. It regains 1d6 + 1 expended charges at
Dawn."* — with the dice as enrichers, so the sentence still rolls and still
tells the truth after you edit the numbers. A preview panel shows it as you go.

> กด **ไอเทมเวทมนตร์** บนแท็บ Inventory ของชีตไหนก็ได้ หรือในแถบ Items — เดินห้าขั้น: เลือกชนิดของ → ชื่อ/ความหายาก/attune → ประจุ → บัฟที่ให้ → พลังที่ใช้ได้
> คำบรรยายเขียนให้อัตโนมัติทั้ง EN/TH และโบนัสเวทลงช่องที่ dnd5e อ่านจริง ไม่ใช่แค่เขียนไว้ในข้อความ

## Who can use it

Two world settings, both **Gamemaster** by default, decide who the module is
for. They appear under *Configure Settings → Zenith Forge*, and only a
Gamemaster can see or change them.

| Setting | Controls |
|---|---|
| **Who can build content** | Opening the Forge, the preset library and the magic item wizard, and changing an icon. Below this role, none of the buttons are drawn at all. |
| **Who can upload images** | Adding an image file through the module — dropping one on an icon, pasting one with Ctrl+V, or uploading from the icon picker. |

Lowering either one to *Player* or *Trusted Player* hands that part of the module
to your table; leaving them alone keeps everything with you.

Foundry's own **Upload New Files** permission still applies on top of the upload
setting: this module can close its own doors, but only core permissions are
enforced by the server.

## What it deliberately does not do

- **No CR, AC or hit point generator.** Foundry handles a creature's own numbers
  already. This module takes the tedious half — making the thing and wiring how
  it is used.
- **No balance opinions.** Library entries carry plausible dice, not CR-tuned
  ones, and the fields are right there to change.
- **Not a security boundary.** The two access settings remove the module from a
  player; what the *server* enforces is document ownership and Foundry's own
  permissions. See *Who can use it*.
- **No creature portraits or token art.** Dedicated tools own that job; this one
  stays out of their way unless you ask it not to.

## Compatibility

| | |
|---|---|
| Foundry VTT | v14 (verified 14.367) |
| System | dnd5e 5.3+ (verified 5.3.3) |
| Languages | English, ไทย |

## Installation

In Foundry's **Add-on Modules** tab choose **Install Module**, paste this address
into **Manifest URL** at the bottom of that window, and press **Install**:

```
https://github.com/OnlyPrize/zenith-forge-releases/releases/latest/download/module.json
```

Then turn on **Zenith Forge** in your world under **Manage Modules**. Foundry
checks the same address for updates, so new versions appear on their own.

> **Upgrading from Ability Forge?** This was called Ability Forge until 0.18.1,
> and in 0.19.0 its id changed too, which means Foundry treats it as a new
> module and will not offer it as an update. **Uninstall Ability Forge, then
> install from the address above** — the address itself has not changed.
>
> Nothing you built is affected: activities and effects are ordinary dnd5e data.
> Your world's settings are copied across on the first load, a save that follows
> an attack is still recognised, and the old module's uploads folder is left
> where it is so pictures already in use keep working.

> **ภาษาไทย:** ในแท็บ Add-on Modules กด **Install Module** วางลิงก์ด้านบนลงช่อง
> **Manifest URL** แล้วกด **Install** จากนั้นเปิดใช้ในเวิลด์ที่ **Manage Modules**

Found a problem? Open an issue at https://github.com/OnlyPrize/zenith-forge-releases/issues.

## License

Free to install and use in your own games, including games you run for others.
Redistributing it, selling it, or publishing modified versions is not permitted
without permission — see [LICENSE](LICENSE).
