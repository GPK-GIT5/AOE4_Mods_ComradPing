# Onslaught Debug Command Inventory

Auto-generated on 2026-04-02 05:31. All Debug_* console commands available in the Onslaught mod.

- **237** debug commands across **27** categories
- **29** debug source files

## Category Summary

| Category | Commands | Source File |
|----------|----------|-------------|
| leaver | 37 | cba_debug_leaver.scar |
| playerui_anim | 32 | cba_debug_playerui_anim.scar |
| helpers | 30 | cba_debug_helpers.scar |
| inspectors | 22 | cba_debug_inspectors.scar |
| autopop | 10 | cba_debug_autopop.scar |
| registry | 10 | cba_debug_registry.scar |
| core | 10 | cba_debug_core.scar |
| ui_prompts | 8 | cba_debug_ui_prompts.scar |
| rules | 7 | cba_debug_rules.scar |
| advanced_stress | 7 | cba_debug_advanced_stress.scar |
| settings | 6 | cba_debug_settings.scar |
| blueprint_audit | 5 | cba_debug_blueprint_audit.scar |
| destructive | 5 | cba_debug_destructive.scar |
| civ_overview | 5 | cba_debug_civ_overview.scar |
| validation | 5 | cba_debug_validation.scar |
| data_extract | 5 | cba_debug_data_extract.scar |
| playerui | 4 | cba_debug_playerui.scar |
| comprehensive_stress | 4 | cba_debug_comprehensive_stress.scar |
| qa_runner | 4 | cba_debug_qa_runner.scar |
| spawn_sequences | 4 | cba_debug_spawn_sequences.scar |
| limits_ui | 4 | cba_debug_limits_ui.scar |
| ai_behavior | 3 | cba_debug_ai_behavior.scar |
| scenario | 3 | cba_debug_scenario.scar |
| stress | 3 | cba_debug_stress.scar |
| coverage | 2 | cba_debug_coverage.scar |
| siege_test | 1 | cba_debug_siege_test.scar |
| event_probes | 1 | cba_debug_event_probes.scar |

## leaver

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_ForceAnnihilation` | `player_idx` | — |
| `Debug_ForceDisconnect` | `player_idx` | — |
| `Debug_FullSystemValidation` | `player_idx` | Debug_FullSystemValidation(player_idx) Single console command for complete runtime validation across all subsystems. Runs: snapshot → reverse map → disconnect → deferred wait → post-validate → blueprint audit → transfer stats/timing → resource/pop/limit deltas → UI check → siege cross-val → summary |
| `Debug_FullValidation_All` | `player_idx, mode` | Usage: Debug_FullValidation_All() Debug_FullValidation_All(2) Debug_FullValidation_All(2, "verbose") |
| `Debug_GetBestAllyInfo` | — | — |
| `Debug_GetLeaverBalanceState` | — | — |
| `Debug_LeaverConversion_Full` | `disconnect_player_idx, opt_mode` | COMMAND 1: Full Validation (Stages 1-6) Usage: Debug_LeaverConversion_Full()  or  Debug_LeaverConversion_Full(2) |
| `Debug_LeaverConversion_Inspect` | — | COMMAND 2: Inspect (read-only, no game state changes) Usage: Debug_LeaverConversion_Inspect() |
| `Debug_LeaverConversion_MilResolve` | `src_idx, dst_idx` | COMMAND 5: Military Suffix Resolution Test (read-only, no spawning) Prints the suffix swap result for common unit patterns across all civs, annotated with gate outcomes (AGE-OK/BLOCK, CAP-OK/BLOCK) per candidate. Usage: Debug_LeaverConversion_MilResolve(src_idx, dst_idx) |
| `Debug_LeaverConversion_Stress` | `num_disconnects` | COMMAND 3: Stress Test (multi-disconnect) Usage: Debug_LeaverConversion_Stress(2)  — disconnects 2 players sequentially |
| `Debug_LeaverConversion_Visual` | `src_idx, dst_idx, mode` | — |
| `Debug_LeaverConversion_VisualByCiv` | `src_civ, dst_civ, mode` | COMMAND: Surrogate Visual Test — spawns entities using arbitrary civ names, converting via _Convert_Building with civ override. Works in ANY match with ≥2 alive players; the first two alive players are auto-selected as surrogates (their actual civs are irrelevant). Usage (console): Debug_LeaverConversion_VisualByCiv("malian", "japanese", "b") |
| `Debug_LeaverConversion_VisualCleanup` | — | Visual test cleanup: safely drains all tracked entities/squads using the same deferred batched path as auto-cleanup. Usage (console): Debug_LeaverConversion_VisualCleanup() |
| `Debug_LeaverCoverage_AllCivPairs` | `opt_mode` | — |
| `Debug_LeaverCoverage_Civ` | `src_civ_name` | Single-civ variant: audit one sender civ against all receivers. |
| `Debug_LeaverCoverage_Pair` | `src_civ, rcv_civ` | COMMAND: Coverage Pair — detailed building-key resolution for one src→rcv civ pair. Works in ANY match (reads AGS_ENTITY_TABLE + _BLUEPRINT_REVERSE_MAP only). Usage (console): Debug_LeaverCoverage_Pair("malian", "japanese") |
| `Debug_LeaverCrossCivMatrix` | `opt_mode` | terminal outcome. This is the complete all-player global cross-civ route check in one command. Usage: Debug_LeaverCrossCivMatrix() Debug_LeaverCrossCivMatrix("verbose") |
| `Debug_LeaverMilCoverage_AllPairs` | `opt_mode` | COMMAND: Military Coverage All Pairs — exhaustive civ×civ audit. Reports per-pair summary and global totals. opt_mode="detail" prints per-unit lines. Usage (console): Debug_LeaverMilCoverage_AllPairs() Usage (detail):  Debug_LeaverMilCoverage_AllPairs("detail") |
| `Debug_LeaverMilCoverage_Pair` | `src_civ, rcv_civ` | COMMAND: Military Coverage Pair — per-unit suffix-swap + policy audit for one src→rcv pair. Works in ANY match (reads AGS_CIV_PREFIXES + _LEAVER_CIV_UNIQUE_FALLBACK + BP engine). Usage (console): Debug_LeaverMilCoverage_Pair("malian", "japanese") |
| `Debug_LeaverMilProof_OneShot` | `verbose` | Single-command deterministic MIL proof runner Usage: Debug_LeaverMilProof_OneShot() |
| `Debug_LeaverMilTest` | `src_idx, dst_idx, verbose` | spawning military units without age constraints and observing route selection. Usage: Debug_LeaverMilTest()                — auto-select civs, default verbosity Debug_LeaverMilTest(src_idx, dst_idx) — manual player indices Debug_LeaverMilTest(src_idx, dst_idx, verbose) — with verbose logging |
| `Debug_LeaverPerformance` | — | PERFORMANCE DEBUG: Per-transfer timing report Prints the phase_timings and annihilation cascade count from the last completed transfer. Usage: Debug_LeaverPerformance() |
| `Debug_LeaverPerformance_6Player` | `count` | — |
| `Debug_LeaverPipelineStatus` | — | PERFORMANCE DEBUG: Leaver Pipeline Status Prints current pipeline state and rule pause status. Usage: Debug_LeaverPipelineStatus() |
| `Debug_LeaverResolve_ForcedBP` | — | — |
| `Debug_LeaverSpawnerExemptProof` | `src_idx, dst_idx` | Usage: Debug_LeaverSpawnerExemptProof()                  -- auto-select alive pair Debug_LeaverSpawnerExemptProof(src_idx, dst_idx)  -- specify by PLAYERS index |
| `Debug_LeaverTransferInspector` | `rcv_civ, src_civ` | — |
| `Debug_LeaverTransferInspector_AllPairs` | `src_civ` | — |
| `Debug_LeaverValidation` | — | — |
| `Debug_LeaverWeaponAudit` | — | — |
| `Debug_LeaverWeaponAudit_ReceiverClass` | `filter_civ` | — |
| `Debug_PrecacheManifest_Confirmed` | — | — |
| `Debug_PrecacheManifest_ForcedCoverage` | — | — |
| `Debug_PrecacheManifest_Gaps` | — | — |
| `Debug_PrecacheManifest_Report` | — | — |
| `Debug_PrecacheManifest_Summary` | — | — |
| `Debug_TransferValidation` | `src_idx, dst_idx` | — |

## playerui_anim

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_PlayerUI_Anim` | — | — |
| `Debug_PlayerUI_Anim_ApplyWhenVisible` | `enabled` | — |
| `Debug_PlayerUI_Anim_Features` | `move_enabled, scale_enabled, pulse_enabled, dim_enabled` | — |
| `Debug_PlayerUI_Anim_FeatureStatus` | — | — |
| `Debug_PlayerUI_Anim_Monitor` | — | — |
| `Debug_PlayerUI_Anim_MonitorStop` | — | — |
| `Debug_PlayerUI_Anim_PresetAll` | — | — |
| `Debug_PlayerUI_Anim_PresetSafe` | — | — |
| `Debug_PlayerUI_Anim_Pulse` | `player_idx` | — |
| `Debug_PlayerUI_Anim_RestoreStage1` | — | — |
| `Debug_PlayerUI_Anim_RestoreStage2` | — | — |
| `Debug_PlayerUI_Anim_RestoreStage3` | — | — |
| `Debug_PlayerUI_Anim_RestoreStage4` | — | — |
| `Debug_PlayerUI_Anim_RestoreStage5` | — | — |
| `Debug_PlayerUI_Anim_RestoreStage6` | — | — |
| `Debug_PlayerUI_Anim_RunStaged` | `delay` | — |
| `Debug_PlayerUI_Anim_SetMinimalHud` | `enabled` | — |
| `Debug_PlayerUI_Anim_Snapshot` | — | — |
| `Debug_PlayerUI_Anim_Stress` | `rounds` | — |
| `Debug_PlayerUI_Anim_TogglePaths` | `hud_enabled, scores_enabled, objectives_enabled` | — |
| `Debug_PlayerUI_Anim_TogglePresetFull` | — | — |
| `Debug_PlayerUI_Anim_TogglePresetHudOnly` | — | — |
| `Debug_PlayerUI_Anim_ToggleProbe` | `path` | — |
| `Debug_PlayerUI_Anim_ValidateDataContext` | — | — |
| `Debug_PlayerUI_Elim_ValidateFull` | `verbose` | — |
| `Debug_PlayerUI_RewardPlayback_CaptureFull` | `threshold, count, timeout` | Captures both idle and mid-animation states, with transition/fallback logging. Args: threshold (default 50): synthetic inject start threshold if idle count (default 3): synthetic milestones to inject if idle timeout (default 8.0): capture timeout in seconds |
| `Debug_PlayerUI_RewardPlayback_Inject` | `threshold, count` | Force-inject a synthetic milestone into the playback queue and start it. Use to test completion animation without waiting for kills. threshold: the kill number to show (default 50) count: how many milestones to inject (default 1) |
| `Debug_PlayerUI_RewardPlayback_InjectReal` | `score_delta` | Inject real milestones by mutating the local player's debug score by +delta, then running the canonical reward crossing path. Example: Debug_PlayerUI_RewardPlayback_InjectReal(75) adds 75 kills, enqueues any crossed thresholds, and updates the progress bar. |
| `Debug_PlayerUI_RewardPlayback_Reset` | — | Force-reset the playback runner to idle (emergency stop). |
| `Debug_PlayerUI_RewardPlayback_SkipPhase` | — | Skip the current completion phase, jumping to the next phase immediately. |
| `Debug_PlayerUI_RewardPlayback_Snapshot` | — | Print the current state of the reward playback runner. |
| `Debug_PlayerUI_RewardPlayback_ValidateCycle` | `threshold, count, timeout` | Run a full inject-and-capture cycle with queued-icon invariant validation. Wraps rewardCaptureFull and reports PASS/FAIL for the fixed-position invariant: during center/highlight/fadeout, queued icons must stay at offsetX=0, opacity=1.0, scale=1.0. |

## helpers

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_Confirm` | — | — |
| `Debug_Demo_RewardPlayback` | `player_idx, kill_grant` | — |
| `Debug_FocusPlayer` | `player_idx` | — |
| `Debug_FocusPosition` | `x, y, z` | — |
| `Debug_Get_EliminationSettleState` | — | — |
| `Debug_Get_RankingAnimKeyAudit` | — | — |
| `Debug_Get_RankingOverview` | — | — |
| `Debug_Get_RewardHealthSummary` | `player_idx` | — |
| `Debug_Get_RewardPlaybackState` | `player_idx` | — |
| `Debug_GetAutoAgeStatus` | — | — |
| `Debug_GetKillScore` | `player_idx` | — |
| `Debug_GetPopCap` | `player_idx` | — |
| `Debug_KeepDiagnostic` | — | — |
| `Debug_ListPlayerSlots` | — | — |
| `Debug_PauseAI` | — | — |
| `Debug_PlayerUI_RegressionCheck` | `player_idx` | — |
| `Debug_PopAudit` | — | — |
| `Debug_PrecacheStatus` | — | — |
| `Debug_Reject` | `reason` | — |
| `Debug_ResumeAI` | — | — |
| `Debug_Run_PlayerUI_PhaseBSuite` | `player_idx, kill_grant` | — |
| `Debug_RunSmokeTests` | — | — |
| `Debug_SetBaseline` | `amount` | — |
| `Debug_SlowMotion` | `enabled` | — |
| `Debug_Spawn` | `bp_name, player_idx, count` | — |
| `Debug_ToggleOverlays` | — | — |
| `Debug_ValidateAgeGateCoverage` | `silent` | — |
| `Debug_VisualValidation_KeepDestroy` | `player_idx` | — |
| `Debug_VisualValidation_SiegeSpawn` | `player_idx` | — |
| `Debug_WaitForVisual` | `description, timeout_seconds` | — |

## inspectors

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_AutoAge_CheckSpecialUpgradeIds` | — | — |
| `Debug_AutoPopHouseGuard` | — | Read-only validation that the auto-pop house guard is functioning correctly. Checks: auto-pop state, transfer stats counter, audit log entries, live entity scan. Returns the number of issues found (0 = PASS). Console: Debug_AutoPopHouseGuard() |
| `Debug_CheckUpgradeBlueprint` | `upgrade_name` | — |
| `Debug_GetAutoAgeState` | — | — |
| `Debug_GetBuildingLimitState` | — | — |
| `Debug_GetKeepOwnershipMap` | — | — |
| `Debug_GetOptionParseResults` | — | — |
| `Debug_GetPostDefeatState` | — | — |
| `Debug_GetReligiousState` | — | — |
| `Debug_GetSiegeLimitState` | — | — |
| `Debug_GetStarterKeepState` | — | — |
| `Debug_GetVillagerState` | — | — |
| `Debug_GetWonderState` | — | — |
| `Debug_KeepCap_CheckSpecialAgeAbilityResolution` | — | — |
| `Debug_LeaverSummary` | — | — |
| `Debug_RamLimitFullTrace` | — | — |
| `Debug_RamSiegeTowerLimitState` | — | Ram/Siege Tower Limit detailed state dump |
| `Debug_SiegeLimitCrossValidation` | — | — |
| `Debug_SiegeLimitFullDump` | — | — |
| `Debug_TeamBalanceCapState` | — | — |
| `Debug_TeamBalancePerLimit` | — | — |
| `Debug_ValidateSiegeClassifications` | — | Main validator: resolves all CBA_SIEGE_TABLE blueprints across all civs and runs tag validation (Phase 2) + path simulation (Phase 3) in a single pass. |

## autopop

| Command | Parameters | Description |
|---------|------------|-------------|
| `debug_autopop` | — | Shorthand alias |
| `Debug_AutoPop_CheckBuildingLocks` | — | — |
| `Debug_AutoPop_CheckCapAlignment` | — | — |
| `Debug_AutoPop_CheckEventDriven` | — | — |
| `Debug_AutoPop_CheckReconcilerState` | — | — |
| `Debug_AutoPop_CheckRewardSuppression` | — | — |
| `Debug_AutoPop_CheckUpgradeLocks` | — | — |
| `Debug_AutoPop_FullValidation` | — | Single-command entry point to run comprehensive auto-pop verification |
| `Debug_AutoPop_PrintSummary` | — | — |
| `Debug_ValidateAutoPopulation` | — | Quick entry points for console (callable directly) Example: Debug_ValidateAutoPopulation() |

## registry

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_DependencyGraph` | — | - Print the dependency graph: each module and what it depends on. |
| `Debug_GetAllModuleManifests` | — | - Return the full module list as an array of manifests (for Debug_ExportManifest serializer). @return table  Array of manifest tables |
| `Debug_GetModuleCount` | — | - Return the count of registered modules. @return number |
| `Debug_GetTagModuleMap` | — | - Return the tag → module mapping (for debugging dispatch routing). @return table |
| `Debug_IsRegistrySealed` | — | - Check if the registry is sealed (all imports complete). @return boolean |
| `Debug_ListModules` | `filter` | - List all registered modules, optionally filtered by name/tag/description substring. @param filter  string|nil  Case-insensitive substring match |
| `Debug_ModuleInfo` | `name` | - Print detailed manifest for a single module. @param name  string  Module name |
| `Debug_RegisterModule` | `meta, handlers` | - Register a debug module and its handlers. Call at the bottom of each debug domain file. @param meta      table  Module manifest (see contract above) @param handlers  table|nil  Map of function_name → function to populate debug.<namespace> |
| `Debug_SealModuleRegistry` | — | - Seal the registry and run deferred validation. Called once after all debug imports are complete (from cba_debug.scar entry point). |
| `Debug_ValidateModules` | — | - Validate all module manifests: check for missing dependencies, duplicate tags, and orphan tags. Returns (issues_count, issues_list) for programmatic use. @return number, table |

## core

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_ClearHooks` | — | — |
| `Debug_Continue` | — | — |
| `Debug_FireHook` | `name` | — |
| `Debug_ListHooks` | — | — |
| `Debug_RegisterHook` | `name, fn` | — |
| `Debug_RunAll` | `step` | — |
| `Debug_RunFullValidation` | — | — |
| `Debug_Skip` | — | — |
| `Debug_StepMode` | `enabled` | — |
| `Debug_StepStatus` | — | — |

## ui_prompts

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_Answer` | `value` | — |
| `Debug_AskChoice` | `question, choices, on_answer, timeout, default_choice, detail` | — |
| `Debug_AskYesNo` | `question, on_answer, timeout, default_answer, detail` | — |
| `Debug_DismissPrompt` | — | — |
| `Debug_InteractiveCheck_KeepState` | — | — |
| `Debug_InteractiveCheck_Precache` | — | — |
| `Debug_InteractiveCheck_SiegeLimitUI` | — | — |
| `Debug_InteractiveChecks` | — | — |

## rules

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_CheckRules` | `domain_filter, ctx` | - Run all registered rules (or those matching a domain filter), passing optional context. @param domain_filter  string|nil  Case-insensitive substring match on domain @param ctx            table|nil   Context table passed to each rule's check function @return number passed, number total, number hard_fails |
| `Debug_GetAllRules` | — | - Return the full rule list as an array (for Debug_ExportManifest serializer). @return table |
| `Debug_GetRuleCount` | — | - Return the count of registered rules. @return number |
| `Debug_ListRules` | `domain_filter` | - List all registered rules, optionally filtered by domain. @param domain_filter  string|nil  Case-insensitive substring match |
| `Debug_RegisterRule` | `rule` | - Register a named validation rule. @param rule  table  Rule definition (see contract above) |
| `Debug_RuleInfo` | `name` | - Print detailed info for a single rule. @param name  string  Rule name |
| `Debug_RuleReport` | — | - Print a structured report of the last Debug_CheckRules run. |

## advanced_stress

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_AdvancedStressAll` | — | — |
| `Debug_AdvStress_BlueprintStorm` | — | — |
| `Debug_AdvStress_BuildingLimitOscillation` | — | — |
| `Debug_AdvStress_ConcurrentThrash` | — | — |
| `Debug_AdvStress_MaxPopPressure` | — | — |
| `Debug_AdvStress_RapidElimination` | — | — |
| `Debug_AdvStress_SiegeCascade` | — | — |

## settings

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_GetAllSettingSchemas` | — | - Return the full schema table (for manifest export / tooling). @return table  Array of schema entries |
| `Debug_GetSetting` | `key` | - Read a debug setting by key. @param key  string  Setting key (case-sensitive, e.g. "LEAVER_VERBOSE") @return any  Current value, or nil if key unknown |
| `Debug_GetSettingSchema` | `key` | - Get the schema entry for a setting (for programmatic introspection). @param key  string @return table|nil  Schema entry {key, default, type, domain, description} |
| `Debug_ListSettings` | `domain_filter` | - List all settings, optionally filtered by domain substring. @param domain_filter  string|nil  Case-insensitive substring match on domain field |
| `Debug_ResetSettings` | — | - Reset all settings to their schema defaults. |
| `Debug_SetSetting` | `key, value` | - Update a debug setting with type validation. @param key    string  Setting key @param value  any     New value (must match declared type) @return boolean  true if accepted, false if rejected |

## blueprint_audit

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_BlueprintAudit` | — | Full audit: checks every blueprint string in AGS_ENTITY_TABLE |
| `Debug_BlueprintAudit_Civ` | `civ_name` | Single-civ detail: shows every key and its blueprint + exists status |
| `Debug_BlueprintAudit_LeaverFallback` | — | Leaver Fallback Audit: validates _LEAVER_CIV_UNIQUE_FALLBACK entries resolve for every receiver civ. Reports which civ×fallback pairs would fail at runtime. Usage: Debug_BlueprintAudit_LeaverFallback() |
| `Debug_DumpBlueprintsForSuffix` | `suffix` | PBG suffix dump: enumerates all Entity/Squad blueprints whose path contains suffix Usage: Debug_DumpBlueprintsForSuffix("_lan") or Debug_DumpBlueprintsForSuffix("_mon_ha_gol") |
| `Debug_EnumerateAllCivUnits` | `opt_civ` | — |

## destructive

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_ForceEliminatePlayer` | `player_idx` | — |
| `Debug_ForceKeepDestroy` | `player_idx` | — |
| `Debug_ForceSurrender` | `player_idx` | — |
| `Debug_ForceTransferTest` | `src_idx, dst_idx` | — |
| `Debug_ValidateSpawnAnchors` | — | — |

## civ_overview

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_CivOverview_Audit` | — | — |
| `Debug_CivOverview_Build` | — | — |
| `Debug_CivOverview_Civ` | `civ` | — |
| `Debug_CivOverview_DumpStructured` | `include_entries` | — |
| `Debug_CivOverview_Summary` | — | — |

## validation

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_FactionMapDiagnostic` | — | — |
| `Debug_FullValidation` | — | — |
| `Debug_LimitEnforcementValidator` | — | — |
| `Debug_LimitEnforcementValidator` | — | — |
| `Debug_VerifyDynastiesData` | — | Debug_VerifyDynastiesData — Single-command verification for Dynasties data additions Validates: upgrade table entries, correction table entries, key parity, arena reward tables Console: Debug_VerifyDynastiesData() |

## data_extract

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_DataExtract_AllBlueprints` | — | Stage 2b-1: Full BP enumeration (Entity, Squad, Upgrade path names) |
| `Debug_DataExtract_BuildingData` | — | Stage 2b-3: Building data (garrison capacity + base cost + build time) Iterates AGS_ENTITY_TABLE for building_ entries and extracts properties. |
| `Debug_DataExtract_RaceSquads` | — | Stage 2b-2: Per-race squad inventory Uses World_GetPossibleSquadsCount/Blueprint to enumerate what each race can train. |
| `Debug_DataExtract_Summary` | — | Summary: quick count of extractable data (no full dump) |
| `Debug_DataExtract_UnitCosts` | — | Stage 2b-4: Unit costs (base cost + pop cost by cap type) Iterates AGS_ENTITY_TABLE for unit_ entries and extracts cost/pop data from BPs. |

## playerui

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_PlayerUI` | — | — |
| `Debug_PlayerUI_Data` | — | — |
| `Debug_PlayerUI_Ranking` | — | — |
| `Debug_PlayerUI_UI` | — | — |

## comprehensive_stress

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_ComprehensiveStress` | — | — |
| `Debug_ComprehensiveStress_Cat` | `n` | — |
| `Debug_ComprehensiveStressStatus` | — | — |
| `Debug_ComprehensiveStressStop` | — | — |

## qa_runner

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_QADiagnostic` | — | — |
| `Debug_QADiagnostic_Topic` | `n` | — |
| `Debug_QADiagnostic_TransferScenarios` | `surrender_idx, elimination_idx, disconnect_idx` | — |
| `Debug_QADiagnosticStatus` | — | — |

## spawn_sequences

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_RunSpawnPlan` | `plan` | — |
| `Debug_SpawnAndValidate` | `bp_name, player_idx, count, validate_fn` | — |
| `Debug_SpawnPlan_MixedArmy` | `player_idx` | — |
| `Debug_SpawnPlan_SiegeStress` | — | — |

## limits_ui

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_ConstructionTrace` | `player_idx` | — |
| `Debug_GetLimitsUIState` | — | — |
| `Debug_LimitsUI_TraceUpdateFlow` | `enable` | — |
| `Debug_LimitsUIStress` | — | — |

## ai_behavior

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_AIBehavior` | — | — |
| `Debug_AIBehavior_Scenario` | `n` | — |
| `Debug_AIBehaviorStatus` | — | — |

## scenario

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_Scenario` | — | — |
| `Debug_ScenarioStatus` | — | — |
| `Debug_ScenarioStop` | — | — |

## stress

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_SiegeLimitStressTest` | — | — |
| `Debug_StressStage` | `n` | — |
| `Debug_StressTest` | — | — |

## coverage

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_CoverageBatch` | `n` | — |
| `Debug_CoverageTest` | — | — |

## siege_test

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_SiegeTest` | — | — |

## event_probes

| Command | Parameters | Description |
|---------|------------|-------------|
| `Debug_EventProbes` | — | — |

