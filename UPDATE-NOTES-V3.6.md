# Shonen Siege V3.6 – balancing and banner update

## Included
- Character stats now surface calculated DPS from base damage and SPA (attack interval in milliseconds).
- Default rarity DPS targets: Common 20, Uncommon 29, Rare 43, Epic 65, Legendary 96, Mythic 145.
- Default upgrade scaling moderated to 12% damage growth and 15ms faster SPA per upgrade (minimum 300ms).
- Admin character editor allows damage, range, SPA, income and support-buff values regardless of selected role. DPS is calculated, not manually editable.
- Three summon tabs: rotating verse Mythic (60-minute rotation), featured Mythic (90-minute rotation), and custom Mythic selection.
- Lower rarities draw from the full enabled roster on the rotating/custom banners; the Mythic rarity is restricted to the relevant verse/featured/selected Mythic.
- Base rates: Common 50%, Uncommon 25%, Rare 18.9%, Epic 5%, Legendary 1%, Mythic 0.1%.
- Epic/Legendary/Mythic hard pity: 50/100/500; custom-selection Mythic pity: 400.
- Separate banner pity counters. Lucky drops do not reset pity; a hard-pity guarantee resets only the guaranteed rarity's counter.
- Custom Mythic selection is stored server-side and can be changed once per 12 hours for signed-in users.

## Supabase migrations
The following migrations were applied to the connected Supabase project and are included in `supabase/migrations/`:
1. `202611040001_update_summon_rates_and_pity.sql`
2. `202611040002_banner_modes.sql`
3. `202611040003_persist_custom_selection.sql`

The application calls `perform_summon_v2` and `set_custom_mythic_selection` for signed-in players.

## Important testing note
The JSX files passed TypeScript's JSX transpilation syntax check. A full Vite production build could not be run in this environment because installing project dependencies timed out. Do not deploy over the live site until a local `npm install` and `npm run build` complete successfully and gameplay is tested.

## Balance note
The rarity DPS targets and upgrade growth are initial global tuning values, not a verified wave-102 simulation. Test a representative full Mythic squad and adjust enemy scaling, unit costs, upgrade costs, range, and abilities from actual runs before treating wave 102 as achieved.


## Follow-up development pass
- Updated battle calculations so income generation and support buffs are driven by configured values, not blocked by the character's role label.
- A character can now have attack stats, income, and a support buff together when configured in the Admin editor.
- Updated the Admin level preview to show configured income and buffs regardless of role.
- Fixed the offline/local summon fallback so it cannot silently replace a missing rarity with a character of a different rarity.

## Verification status
- TypeScript JSX transpilation syntax checks passed for `src/main.jsx` and `src/account-admin.jsx`.
- A complete Vite build is still unverified because this environment cannot download React/Vite dependencies from the npm registry.
- The live GitHub Pages site has not been changed.

## SPA seconds update — 4 November 2026
- Standardised character `attack_speed` as seconds per attack (SPA), not milliseconds.
- Updated all 136 attacking character records in Supabase to a 3.00–8.00 second SPA range.
- Preserved each character's prior damage-per-second rate while scaling damage per hit with the new SPA value, so slower attacks deal more damage per hit.
- The four non-attacking income characters remain at 0 attack speed and 0 damage.
- Backed up all 140 original character `base_damage` and `attack_speed` values in `game_characters_spa_backup_20261104` before the conversion.
- Updated battle cooldown timing, DPS calculations, character stat displays, level-up SPA handling, and admin editor labels/limits to use seconds directly.
- Local source files passed TypeScript JSX transpilation syntax checks. A full Vite production build was not run because dependencies are not installed in this environment.
- GitHub Pages deployment was not changed.
