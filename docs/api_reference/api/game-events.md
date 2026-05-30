# AoE4 Game Events (GE_) — Complete Reference

188 game events for hooking into gameplay systems via `Rule_AddGlobalEvent()`.

Last Updated: 2026-03-18 (13 events added from scardocs v15.4.8719.0)

## Usage Pattern
```lua
-- Register a callback for a game event
Rule_AddGlobalEvent(MyCallback, GE_EntityKilled)

-- Callback receives a context table with event-specific data
function MyCallback(context)
    local victim = context.victim          -- killed entity
    local killer = context.killer          -- entity that killed
    local victimOwner = context.victimOwner -- player who owned victim
end

-- Remove the event listener
Rule_RemoveGlobalEvent(MyCallback)
```

---

## Upgrades & Research

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_UpgradeStart` | 0 | player, upgrade |
| `GE_UpgradeComplete` | 65536 | player, upgrade |
| `GE_UpgradeTentative` | 131072 | |
| `GE_UpgradeRemoved` | 7471104 | |
| `GE_UpgradeCancelled` | 7602176 | |

---

## Entity Lifecycle

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_EntitySpawn` | 196608 | entity, player |
| `GE_EntityDespawn` | 262144 | |
| `GE_EntityOwnerChange` | 327680 | entity, prevOwner, newOwner |
| `GE_EntityBlueprintChanged` | 393216 | |
| `GE_EntityKilled` | 458752 | victim, killer, victimOwner |
| `GE_EntityTeleported` | 524288 | |
| `GE_EntityCrushed` | 589824 | |
| `GE_EntityLandmarkDestroyed` | 655360 | landmarkOwner |
| `GE_EntityWrecked` | 720896 | |
| `GE_EntityRestored` | 786432 | |
| `GE_EntityPrecached` | 1179904 | |
| `GE_EntityAbandoned` | 3276800 | |
| `GE_EntityRecrewed` | 3342336 | |
| `GE_EntityParadropComplete` | 2293760 | |
| `GE_EntitySelectionVisualChanged` | 8650752 | |
| `GE_AnimatorSwap` | 8781824 | |

---

## Construction

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_ConstructionStart` | 851968 | entity, player |
| `GE_ConstructionCancelled` | 917504 | |
| `GE_ConstructionComplete` | 983040 | entity, player |
| `GE_ConstructionPlanComplete` | 1048576 | |
| `GE_ConstructionFieldComplete` | 1114112 | |
| `GE_PlannedStructurePlaced` | 1835008 | |
| `GE_PlannedStructureCancelled` | 1900544 | |
| `GE_StructureReplaced` | 1966080 | |
| `GE_ConstructionWorkerStart` | — | *scardocs* |

---

## Production & Building

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_BuildItemStart` | 1572864 | |
| `GE_BuildItemComplete` | 1638400 | entity, player, squad |
| `GE_BuildItemCancelled` | 7995392 | |
| `GE_ReinforcementCreated` | 1703936 | |
| `GE_OccupiedBuildingChangedOwner` | 1310720 | |

---

## Squad Events

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_SquadSpawn` | 3473408 | squad, player |
| `GE_SquadKilled` | 3538944 | squad, player |
| `GE_SquadPinned` | 3604480 | |
| `GE_SquadProductionQueue` | 3670016 | |
| `GE_SquadVeterancyRank` | 3735552 | squad, rank |
| `GE_SquadItemPickup` | 3801088 | |
| `GE_SquadItemDeposit` | 3866624 | |
| `GE_SquadIdleEnter` | 3932160 | |
| `GE_SquadIdleExit` | 3997696 | |
| `GE_SquadRetreat` | 4063232 | |
| `GE_SquadRetreatMsgReceived` | 4128768 | |
| `GE_SquadFormation` | 4194304 | |
| `GE_CasualtySquadSpawned` | 4259840 | |
| `GE_SquadParadropComplete` | 4325376 | |
| `GE_SquadSplit` | 4390912 | |
| `GE_SquadMerge` | 4456448 | |
| `GE_SquadMembersChanged` | 4521984 | |
| `GE_SquadCold` | 4587520 | |
| `GE_SquadFreezing` | 4653056 | |
| `GE_SquadCalledIn` | 4718592 | |
| `GE_SquadReplaced` | 4784128 | |
| `GE_SquadUnloaded` | 4849664 | |
| `GE_SquadOwnerChange` | 4915200 | |
| `GE_SquadTeleported` | 4980736 | |
| `GE_SquadSizeChanged` | 7667712 | |

---

## Combat & Damage

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_DamageReceived` | 5111808 | target, attacker, damage |
| `GE_PlayerBeingAttacked` | 5046272 | player |
| `GE_ArtilleryFired` | 2228224 | |
| `GE_ProjectileFired` | 2621440 | |
| `GE_ProjectileLanded` | 2686976 | |
| `GE_AccessoryWeaponFired` | 2752512 | |
| `GE_MineDefused` | 2359296 | |
| `GE_BoobyTrapTriggered` | 3145728 | |
| `GE_DamageArea` | 6881280 | |
| `GE_EnemyActivitySpotted` | 7864320 | |
| `GE_WeaponChanged` | — | *scardocs* |
| `GE_SquadHitEvent` | — | *scardocs* |

---

## Abilities

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_AbilityExecuted` | 2424832 | player, ability |
| `GE_AbilityComplete` | 2490368 | |
| `GE_AbilityRecharged` | 2555904 | |
| `GE_AbilityCanCast` | 7929856 | |
| `GE_SuperAbility` | 6750208 | |
| `GE_SpawnActionComplete` | 6815744 | |

---

## Player Events

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_PlayerLagComplaint` | 131328 | |
| `GE_PlayerDropped` | 196864 | |
| `GE_PlayerPingOfShame` | 256 | |
| `GE_PlayerPingOfShameLocal` | 65792 | |
| `GE_PlayerKicked` | 262400 | |
| `GE_PlayerKilled` | 327936 | player |
| `GE_PlayerHostMigrated` | 393472 | |
| `GE_PlayerEndStateChanged` | 1966336 | |
| `GE_PlayerDonation` | 6160384 | |
| `GE_PlayerNameChanged` | 6225920 | |
| `GE_PlayerObjectiveDeleted` | 6291456 | |
| `GE_PlayerObjectiveChanged` | 6356992 | |
| `GE_PlayerPhaseUp` | 6422528 | player, age |
| `GE_PlayerResourcesAwarded` | 6488064 | |
| `GE_PlayerSurrendered` | 7012352 | |
| `GE_PlayerCheat` | 5242880 | |
| `GE_AITakeOver` | 6553600 | |
| `GE_AIPlayer_EncounterNotification` | 6619136 | |
| `GE_AIPlayer_EncounterSniped` | 6684672 | |
| `GE_AIPlayer_Migrated` | 7143424 | |
| `GE_PlayerAddResource` | 8126464 | |
| `GE_PlayerSubResource` | 8192000 | |
| `GE_PlayerAddEntity` | 8257536 | |
| `GE_PlayerRemoveEntity` | 8323072 | |
| `GE_PlayerSquadInitialized` | 8388608 | |
| `GE_PlayerRemoveSquad` | 8454144 | |
| `GE_PlayerTeamIdUpdated` | 8585216 | |
| `GE_PlayerFormationFinalized` | 8716288 | |
| `GE_PlayerSetResource` | 9306112 | |
| `GE_LocalPlayerChanged` | 6094848 | |
| `GE_PlayerSentTribute` | — | *scardocs* |

---

## Game State

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_GameStart` | 917760 | |
| `GE_GameOver` | 983296 | |
| `GE_PlayerWin` | 1048832 | player |
| `GE_PlayerLose` | 1114368 | player |

---

## Territory & Strategic Points

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_StrategicPointChanged` | 1769472 | entity, player |
| `GE_TerritoryEdgeDeoccupied` | 1179648 | |
| `GE_TerritoryCornerDeoccupied` | 1245184 | |
| `GE_TerritoryEntered` | 5963776 | |
| `GE_EnemyTerritoryEntered` | 6029312 | |
| `GE_SectorLinkProviderChanged` | 7208960 | |
| `GE_SectorOutOfSupply` | 9568256 | |

---

## Resources

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_ResourceDepleted` | 2031616 | entity |
| `GE_ResourceGathererAtCapacity` | 2097152 | |
| `GE_ResourceDroppedOff` | — | *scardocs* |
| `GE_ResourceEnabled` | — | *scardocs* |

---

## Movement & Pathfinding

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_PathFound` | 2818048 | |
| `GE_MoveFailed` | 2883584 | |
| `GE_PathfindingCanBuildBlockersAdded` | 2949120 | |
| `GE_PathfindingCanBuildBlockersRemoved` | 3014656 | |
| `GE_PathfindingBlockersUpdated` | 3080192 | |
| `GE_MovementNodeUpdated` | 5898240 | |

---

## Walls & Combat Surfaces

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_WallWalked` | 5701632 | |
| `GE_WallCombatStarted` | 5767168 | |
| `GE_WallCombatEnded` | 5832704 | |
| `GE_WallGateLockToggle` | — | *scardocs* |

---

## Garrison

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_Garrison` | 1441792 | entity, squad |
| `GE_GarrisonSquad` | 1507328 | |
| `GE_DriverDecrewed` | 7274496 | |
| `GE_DriverRecrewed` | 7340032 | |

---

## UI & Selection

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_SelectionChanged` | 1442048 | |
| `GE_SubselectionChanged` | 1507584 | |
| `GE_CustomUIEvent` | 7077888 | |
| `GE_TickerValuesUpdated` | 8519680 | |
| `GE_CameraZoomChangeTelemetryEvent` | — | *scardocs* |
| `GE_CameraZoomLevelUpdateEvent` | — | *scardocs* |

---

## Commands

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_SquadBuildCommandIssued` | 524544 | |
| `GE_FormationSquadGroupCommandIssued` | 590080 | |
| `GE_SquadCommandIssued` | 655616 | |
| `GE_EntityCommandIssued` | 721152 | |
| `GE_PlayerCommandIssued` | 786688 | |
| `GE_DefaultCommandIssued` | 852224 | |
| `GE_CommandStatusUpdate` | 1638656 | |
| `GE_CommandReceiverStatusUpdate` | 1704192 | |

---

## Audio

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_MusicIntensityChange` | 1769728 | |
| `GE_PresentatonSoundEvent` | 1835264 | |
| `GE_SpeechTelemetryEvent` | 1900800 | |
| `GE_SpeechAction` | 7405568 | |
| `GE_SpeechWarningAction` | 7798784 | |
| `GE_SquadAudioGameObjectRemoved` | 1310976 | |
| `GE_PresentationSoundEvent` | — | *scardocs* |

---

## Districts & Influence

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_DistrictCreated` | 8978432 | |
| `GE_DistrictRemoved` | 9043968 | |
| `GE_DistrictChanged` | 9109504 | |
| `GE_DistrictRatingChanged` | 9175040 | |
| `GE_InfluenceUpdate` | 9240576 | |

---

## Miscellaneous

| Event | Value | Context Fields |
|-------|-------|----------------|
| `GE_Ping` | 459008 | |
| `GE_NonGlobalCamoDetected` | 2162688 | |
| `GE_ImportantUnitSighted` | 3211264 | |
| `GE_FieldSupportChange` | 3407872 | |
| `GE_ExperienceGranted` | 5177344 | |
| `GE_OnHealthExtBPConvert` | 1376256 | |
| `GE_TerrainAreaDeformed` | 6946816 | |
| `GE_BroadcastMessage` | 7733248 | |
| `GE_ItemAvailabilityChanged` | 7536640 | |
| `GE_WaitObjectDone` | 8060928 | |
| `GE_TradeRouteCompleted` | 25601 | |
| `GE_ChallengeCustomEvent` | 9371648 | |
| `GE_StatsCustomEvent` | 9437184 | |
| `GE_WalkableSurfacePurgeOrphans` | 9502720 | |
| `GE_EntityBlockShotCountUpdated` | — | *scardocs* |
| `GE_SquadColourChanged` | — | *scardocs* |
| `GE_SquadPrecached` | — | *scardocs* |

---

## Debug Events (Development Only)

| Event | Value |
|-------|-------|
| `GE_PlayerDebug_DELETED` | 5308416 |
| `GE_PlayerDebugEndMatch` | 5373952 |
| `GE_PlayerDebugFogOfWar` | 5439488 |
| `GE_PlayerDebugBuildTime` | 5505024 |
| `GE_PlayerDebugBuildOrder` | 5570560 |
| `GE_PlayerDebugDestroy` | 5636096 |
