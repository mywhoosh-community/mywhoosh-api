# MyWhoosh-API

[![GitHub stars](https://img.shields.io/github/stars/mywhoosh-community/mywhoosh-api)](https://github.com/mywhoosh-community/mywhoosh-api/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/mywhoosh-community/mywhoosh-api)](https://github.com/mywhoosh-community/mywhoosh-api/network/members)
[![License](https://img.shields.io/github/license/mywhoosh-community/mywhoosh-api)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/mywhoosh-community/mywhoosh-api)

![MyWhoosh Logo](./docs/assets/mywhoosh-logo.png)

Unofficial API documentation for MyWhoosh - A comprehensive guide to the MyWhoosh platform's API endpoints and functionality. Create and download workouts, schedule training sessions, customize your character, manage your calendar, calculate XP progression, access game assets, retrieve hidden data, and discover features not visible in the app.

## Base URLs

MyWhoosh uses multiple service endpoints:

- **Main API:** `https://services.mywhoosh.com/http-service/v1`
- **Public API:** `https://services.mywhoosh.com`
- **Coaching API:** `https://coaching.mywhoosh.com/api/v2`
- **Service 14:** `https://service14.mywhoosh.com/v1`
- **Service 20:** `https://service20.mywhoosh.com`
- **Service 26:** `https://service26.mywhoosh.com/http-service/v1`
- **Data Recovery:** `https://data-recovery.mywhoosh.com`

## Authentication

Most endpoints require Bearer token authentication. Include the access token in the Authorization header:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Get your access token by logging in first (see Authentication section below).

---

## Authentication Endpoints

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /http-service/api/login - Login</summary>

Authenticate a user and receive access tokens.

**Base URL:** Public API

**Request Body:**
```json
{
    "Username": "your-email@example.com",
    "Password": "your-password",
    "Platform": "Android",
    "Action": 1001,
    "CorrelationId": "unique-uuid",
    "DeviceId": "device-id",
    "Authorization": ""
}
```

**Response:**
```json
{
    "Username": "your-email@example.com",
    "WhooshId": "your-whoosh-id",
    "Verified": true,
    "Action": "1001",
    "Success": true,
    "LoginType": 1,
    "Message": "Authentication Successful",
    "CorrelationId": "unique-uuid",
    "AccessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "RefreshToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..."
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /http-service/v1/player/register-user - Register</summary>

Create a new user account.

**Base URL:** Public API

**Request Body:**
```json
{
    "UserFirstName": "your-first-name",
    "UserLastName": "your-last-name",
    "Email": "your-email@example.com",
    "Username": "your-email@example.com",
    "Password": "your-password",
    "DobDayId": 1,  // Day of birth (1-31)
    "DobMonthId": 1,  // Month of birth (1-12)
    "DobYearId": 1990,  // Year of birth
    "Country": 0,  // Country code
    "Height": 180,  // Height in cm
    "Weight": 75,  // Weight in kg
    "Gender": 0,  // 0 = Male, 1 = Female
    "FtpPlayer": 160,  // Functional Threshold Power in watts
    "IsAllowedToSendMarketingEmails": false,
    "Action": 1050,
    "CorrelationId": "unique-uuid",
    "DeviceId": "device-id",
    "Authorization": ""
}
```

**Response:**
```json
{
    "Action": 1050,
    "Message": {
        "Response": "{\"Verified\":false,\"Userid\":\"your-user-id\",\"MetaDataVersion\":1}",
        "Action": 1050,
        "CorrelationId": "unique-uuid",
        "Success": true,
        "Verified": false
    },
    "CorrelationId": "unique-uuid",
    "Success": true
}
```

</details>

---

## Game

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/game-title-data - Get Game Title Data</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "bisNewSyncingEnabled": true,
    "PowerPerTabDeveloperTool": 10.0,
    "CurrentVersion": "151",
    "MinimumVersion": "151",
    "AveragePowerInterval": 6.0,
    "DraftingFactorList": [0.55],
    "FitnessNetworksKeys": [
        {
            "NetworkType": 0,
            "ClientID": "client-id",
            "ClientSecret": "client-secret"
        }
        // ... more fitness networks
    ],
    "LeaderboardBaseURL": "https://services.mywhoosh.com/leaderboard-service/v1",
    "RidelogServiceURL": "https://services.mywhoosh.com/ridelogs",
    "FileHandlingURL": "https://service20.mywhoosh.com",
    "AnalyticsURL": "https://logservice.mywhoosh.com",
    "MinDraftingSpeed": 15,
    "CurrentDraftingEnabled": 3,
    "AndroidPlayStoreURL": "https://play.google.com/store/apps/details?id=com.mywhoosh.whooshgame",
    "IOSAppStoreURL": "https://apps.apple.com/ae/app/my-whoosh/id1498889644",
    "WindowsStoreURL": "https://www.microsoft.com/en-ae/p/mywhoosh/9NVDCPH3XDZ2",
    "MacAppURL": "https://apps.apple.com/ae/app/my-whoosh/id1498889644",
    "FitnessFileType": "fit",
    "MaxPhotonTimeOutNormalPlayer": 5.0,
    "MaxPhotonTimeOutSpecialPlayer": 30.0,
    "DraftingPeloton": [
        // ... drafting configuration data
    ],
    "MaxActivePlayerCountInEvent": 100,
    "MaxActivePlayerCountInFreeRide": 100,
    "MyWhooshAchievementsIconsZipUrl": "https://prod-cdn-assets.mywhoosh.com/images/...",
    "MyWhooshWordlsURL": "https://prod-cdn-assets.mywhoosh.com/images/...",
    "MyWhooshWorkoutsZipURL": "https://prod-cdn-assets.mywhoosh.com/images/...",
    "MyWhooshTrainingPlansZipURL": "https://prod-cdn-assets.mywhoosh.com/images/...",
    "Worlds": [
        {
            "WorldID": 1,
            "isEnabled": true,
            "WorldName": "Tour Of Arabia",
            "WorldDays": {
                "Sat": false,
                "Sun": true,
                "Mon": true,
                "Tue": false,
                "Wed": true,
                "Thu": true,
                "Fri": true
            },
            "bIsSeasonalContentAvailable": true,
            "SeasonPassRequired": false,
            "isEnabledTreasureHunt": false,
            "WindProperties": {
                "IsWindEnabled": true,
                "MinimumSpeedOfWind": 2.0,
                "MaximumSpeedOfWind": 4.0
            }
        }
        // ... more worlds (Australia, Colombia, Belgium, AlUla, etc.)
    ],
    "IsVirtualGearShiftingFeatureEnabled": true,
    "IsRedeemCouponUIEnabled": true,
    "MaxIdlingTime": 3600,
    "GameRegion": "EU",
    "BuildType": "dev"
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/junction-info - Get Junction Info</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
[
    {
        "RouteId": 1,
        "Name": "Adnoc Tower"
    },
    {
        "RouteId": 2,
        "Name": "Marina Mall"
    },
    {
        "RouteId": 3,
        "Name": "Abu Dhabi Theater Fairmont"
    }
    // ... more routes (300+ total routes including Tour Of Arabia, AlUla, Australia, Colombia, Belgium, California, Japan, Bhutan, etc.)
]
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/treasure-hunt - Get Treasure Hunt</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "TreasureHuntGateList": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /bots/game/ControllableBots - Get Controllable Bots</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "MyWhooshCCBotsArray": [
        {
            "CCBotName": "Smasher",
            "BotTypeId": "5",
            "ActionTimeAttack": "1800",
            "ActionTimeSprint": "60",
            "ActionValueAttack": "118",
            "ActionValueSprint": "220",
            "BotType": 5,
            "IdlePower": "150",
            "NormalPowerMin": "108",
            "NormalPowerMax": "113",
            "PowerInRecovery": "100",
            "RecoveryTime": "180",
            "RiderDistance": 6.0,
            "MaxInstantRecoveryCount": 3
        },
        {
            "CCBotName": "Climber",
            "BotTypeId": "6",
            "BotType": 3
            // ... similar structure
        }
        // ... more bots (Attacker, Mountain, Flat, Sprinter)
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/challenges - Get Challenges</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "TotalAchievements": {
        "Elevation": [
            {
                "type": "Elevation",
                "id": "Ach_ClimbAccumulative_1",
                "groupId": "Hill Climb",
                "frequency": "Milestone",
                "amount": 1000.0,
                "name": "Hill Climb - 1",
                "description": "Climb accumulative 1,000 m elevation",
                "validity": "0",
                "rideType": "Any",
                "isAreaSpecific": false,
                "isAccumulative": true,
                "isRiding": false,
                "rewards": [
                    {
                        "rewardType": "Coin",
                        "amount": 50
                    }
                ],
                "icon_name": "Ach_ClimbAccumulative",
                "frame_name": "T_1_F_1",
                "background_name": "Ach_ClimbAccumulative",
                "followStat": false,
                "isDayBased": false,
                "days": 0,
                "additionalParams": {}
            },
            {
                "type": "Elevation",
                "id": "Ach_ClimbAccumulative_2",
                "groupId": "Hill Climb",
                "frequency": "Milestone",
                "amount": 5000.0,
                "name": "Hill Climb - 2",
                "description": "Climb accumulative 5,000 m elevation",
                "validity": "0",
                "rideType": "Any",
                "isAreaSpecific": false,
                "isAccumulative": true,
                "isRiding": false,
                "rewards": [
                    {
                        "rewardType": "Coin",
                        "amount": 100
                    }
                ],
                "icon_name": "Ach_ClimbAccumulative",
                "frame_name": "T_1_F_2",
                "background_name": "Ach_ClimbAccumulative",
                "followStat": false,
                "isDayBased": false,
                "days": 0,
                "additionalParams": {}
            }
            // ... more elevation challenges
        ]
        // ... other challenge categories (Distance, Speed, etc.)
    }
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/drafting-peloton - Get Drafting Peloton</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "WindEffectQuadrants": [
        {
            "DraftingPeloton": [
                {
                    "draftingRow": [
                        {
                            "dragDistanceOnePercentage": 100,
                            "dragDistanceTwoPercentage": 100,
                            "dragDistanceThreePercentage": 100,
                            "dragDistanceFourPercentage": 100,
                            "dragDistanceFivePercentage": 100
                        }
                    ]
                },
                {
                    "draftingRow": [
                        {
                            "dragDistanceOnePercentage": 72,
                            "dragDistanceTwoPercentage": 76,
                            "dragDistanceThreePercentage": 80,
                            "dragDistanceFourPercentage": 85,
                            "dragDistanceFivePercentage": 92
                        },
                        {
                            "dragDistanceOnePercentage": 72,
                            "dragDistanceTwoPercentage": 76,
                            "dragDistanceThreePercentage": 80,
                            "dragDistanceFourPercentage": 85,
                            "dragDistanceFivePercentage": 92
                        }
                    ]
                },
                {
                    "draftingRow": [
                        {
                            "dragDistanceOnePercentage": 71,
                            "dragDistanceTwoPercentage": 75,
                            "dragDistanceThreePercentage": 79,
                            "dragDistanceFourPercentage": 84,
                            "dragDistanceFivePercentage": 91
                        },
                        {
                            "dragDistanceOnePercentage": 69,
                            "dragDistanceTwoPercentage": 74,
                            "dragDistanceThreePercentage": 77,
                            "dragDistanceFourPercentage": 82,
                            "dragDistanceFivePercentage": 89
                        },
                        {
                            "dragDistanceOnePercentage": 71,
                            "dragDistanceTwoPercentage": 75,
                            "dragDistanceThreePercentage": 79,
                            "dragDistanceFourPercentage": 84,
                            "dragDistanceFivePercentage": 91
                        }
                    ]
                }
                // ... more drafting rows
            ]
        },
        {
            "DraftingPeloton": [
                {
                    "draftingRow": [
                        {
                            "dragDistanceOnePercentage": 100,
                            "dragDistanceTwoPercentage": 100,
                            "dragDistanceThreePercentage": 100,
                            "dragDistanceFourPercentage": 100,
                            "dragDistanceFivePercentage": 100
                        }
                    ]
                },
                {
                    "draftingRow": [
                        {
                            "dragDistanceOnePercentage": 77,
                            "dragDistanceTwoPercentage": 79,
                            "dragDistanceThreePercentage": 80,
                            "dragDistanceFourPercentage": 85,
                            "dragDistanceFivePercentage": 92
                        },
                        {
                            "dragDistanceOnePercentage": 67,
                            "dragDistanceTwoPercentage": 68,
                            "dragDistanceThreePercentage": 70,
                            "dragDistanceFourPercentage": 75,
                            "dragDistanceFivePercentage": 82
                        }
                    ]
                }
                // ... more drafting rows
            ]
        }
        // ... more wind effect quadrants
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /game/world-route-player-count - Get World Route Player Count</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "workoutsCount": 1352,
    "liveCoachingCount": 0,
    "bunchRideCount": 158,
    "vodCount": 0,
    "worldsData": [
        {
            "worldId": 1,
            "playersCount": 1029,
            "botsCount": 132,
            "routesData": [
                {
                    "routeId": 1,
                    "playersCount": 29,
                    "botsCount": 0
                },
                {
                    "routeId": 2,
                    "playersCount": 19,
                    "botsCount": 0
                },
                {
                    "routeId": 3,
                    "playersCount": 45,
                    "botsCount": 30
                },
                {
                    "routeId": 6,
                    "playersCount": 60,
                    "botsCount": 0
                },
                {
                    "routeId": 9,
                    "playersCount": 75,
                    "botsCount": 0
                },
                {
                    "routeId": 22,
                    "playersCount": 307,
                    "botsCount": 27
                },
                {
                    "routeId": 23,
                    "playersCount": 116,
                    "botsCount": 6
                }
                // ... more routes
            ]
        },
        {
            "worldId": 3,
            "playersCount": 477,
            "botsCount": 109,
            "routesData": [
                {
                    "routeId": 16,
                    "playersCount": 23,
                    "botsCount": 21
                },
                {
                    "routeId": 17,
                    "playersCount": 170,
                    "botsCount": 27
                },
                {
                    "routeId": 18,
                    "playersCount": 69,
                    "botsCount": 0
                }
                // ... more routes
            ]
        },
        {
            "worldId": 8,
            "playersCount": 159,
            "botsCount": 0,
            "routesData": [
                {
                    "routeId": 113,
                    "playersCount": 32,
                    "botsCount": 0
                },
                {
                    "routeId": 114,
                    "playersCount": 61,
                    "botsCount": 0
                }
                // ... more routes
            ]
        }
        // ... more worlds
    ],
    "eventsData": [
        {
            "eventId": "b9e39930-2be5-4594-8663-c07811fc5ea6",
            "playersCount": 7,
            "botsCount": 0
        },
        {
            "eventId": "17771b45-8d17-4c1d-93a2-6ecddf0619f2",
            "playersCount": 8,
            "botsCount": 0
        },
        {
            "eventId": "027cd5c9-fd4f-4da6-8c66-b94263a71611",
            "playersCount": 15,
            "botsCount": 0
        },
        {
            "eventId": "5b6ac40c-cec5-435d-8f04-d41659692c2a",
            "playersCount": 32,
            "botsCount": 0
        }
        // ... more events
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /http-service/v1/game/environment-by-app-version - Get Environment by App Version</summary>

**Base URL:** Public API

**Query Parameters:**
- `appVersion` (string, required): e.g., "5.5.0"
- `platform` (string, required): e.g., "Android"
- `buildVersion` (string, required): e.g., "150"

**Example:**
```
GET /http-service/v1/game/environment-by-app-version?appVersion=5.5.0&platform=Android&buildVersion=150
```

**Response:**
```json
{
    "Environment": "PROD"
}
```

</details>

---

## Player

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /player/player-data - Get Player Data</summary>

**Base URL:** Main API

**Authentication:** Required

**Request Body:**
```json
{
    "WhooshId": "your-whoosh-id",
    "Action": 1052,
    "CorrelationId": "unique-uuid",
    "DeviceId": "device-id",
    "Authorization": ""
}
```

**Response:**
```json
{
    "PlayerDataStruct": {
        "PlayerProfileStruct": {
            "Id": 0,
            "CycleId": 0,
            "HelmetId": 3,
            "FrameId": 1,
            "TyreId": 1,
            "FacialHairId": 0,
            "HairId": 0,
            "SkinTuneId": 0,
            "GlassesId": 0,
            "JerseyId": 73,
            "GlovesId": 13,
            "MaskId": 0,
            "SocksId": 5,
            "ShoesId": 1,
            "CountryId": 89,
            "HeightCm": 180.0,
            "Weight": 75.0,
            "Gender": 0,
            "SocksLength": 1,
            "PlayerFirstName": "[FirstName]",
            "PlayerLastName": "[LastName]",
            "PlayerType": 0,
            "PlayerTeamId": "",
            "FacialHairColorId": 1,
            "HairColorId": 1,
            "FaceEthnicityId": 1,
            "DobDayId": 0,
            "DobMonthId": 0,
            "DobYearId": 0,
            "PlayerCategoryId": 1,
            "CategoryName": "",
            "fullName": "",
            "TeamId": "-1",
            "RewardJerseys": [],
            "PlayerGameModeType": 0,
            "DefaultValues": false,
            "CurrentAITrainingplanId": "",
            "PersonalizedAvatar": {
                "FaceEthnicityId": -1,
                "FacialHairId": -1,
                "HairId": -1,
                "PersonalizedJerseyId": -1
            },
            "IsCommunityManager": false,
            "CanReceiveWindEffect": true
        },
        "PlayerPersonalStruct": {
            "PlayerRoleType": 1,
            "LastJerseyId": 73,
            "WhooshServerId": "[server-id]",
            "WinItems": [],
            "Email": "[email]",
            "Gems": 0,
            "BestPower5Second": 0,
            "Coins": 0,
            "DobDayId": 1,
            "RegisteredEvents": [],
            "PlayerLevel": 1,
            "BestPower1Minute": 0,
            "JoinedEvents": [],
            "JoinedGroupWorkouts": [],
            "DobYearId": 1990,
            "PlayerEventsTeam": [],
            "PlayerXP": 0,
            "BestPower5Minute": 0,
            "bVerified": true,
            "AveragePower": 0.0,
            "DobMonthId": 1,
            "TotalRideTime": 1.0,
            "VerifiedWeight": 75.0,
            "VerifiedHeight": 180.0,
            "TotalKilometers": 0.0,
            "TotalCaloriesBurn": 0.0,
            "PlayerBrakeFactor": 1.0,
            "MaxPower": 0,
            "BestPower20Minute": 0,
            "FtpPlayer": 200.0,
            "IsAllowedToSendMarketingEmails": false,
            "LanguageId": 0,
            "TotalElevation": 0.0,
            "AverageHeartRate": 0.0,
            "PacePlayer": 0.0,
            "PlayerKickedFromVoiceChatEventIds": [],
            "JoinedGroupworkouts": [],
            "PreviousPowerpassport": {
                "Power6Second": 0.0,
                "Power30Second": 0.0,
                "Power3Minute": 0.0,
                "Power12Minute": 0.0
            },
            "AlltimePowerpassport": {
                "Power6Second": 0.0,
                "Power30Second": 0.0,
                "Power3Minute": 0.0,
                "Power12Minute": 0.0
            },
            "ThirdPartyImportedDataList": null,
            "bIsCurrentSeasonSubbed": false,
            "SubscribedSeasonPassId": null,
            "TotalKilometersInWeek": 0.0,
            "isKycValidated": false,
            "CryptoCoinBalance": 0,
            "IsTuckPositionFeatureAllowedOnAnyPower": false,
            "IsTuckPositionFeatureAllowedOnAnySpeed": false,
            "IsTuckAutoEnabled": false,
            "BestPower30Second": 0.0,
            "BestPower3Minute": 0.0,
            "BestPower12Minute": 0.0,
            "BestPower30Minute": 0.0,
            "BestPower60Minute": 0.0
        }
    },
    "PlayerGameData": {
        "PowerDisplayType": 0,
        "bIsPlayerProfileVerified": true,
        "bIsWhooshEnabled": true,
        "MusicVolume": 0.0,
        "MeasureUnit": 0,
        "TrainerDifficulty": 0.5,
        "PlayerSpeedMultiplier": 1.0,
        "bApplyLanguageFilter": false,
        "bShowGroupChat": false,
        "GameVolume": 0.5,
        "ExtraTrainerDifficulty": 0.0,
        "PlayerPowerMultiplier": 1.0,
        "bIsSecondaryPowerIconNeedToShow": false,
        "IsAutoFileUpload": false
    }
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /player/my-friends - Get My Friends</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "MyTotalFriends": 0,
    "ListOfOnlineFriends": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /player/fitness-network - Get Fitness Network</summary>

**Base URL:** Service 26

**Authentication:** Required

**Response:**
```json
{
    "JoinedFitnessNetwork": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /player/player-distance - Get Player Distance</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `days` (integer): Number of days (e.g., 7)

**Example:**
```
GET /player/player-distance?days=7
```

**Response:**
```json
{
    "DayBasedStats": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/61affe/61affe.png" alt="PUT"/> <b>PUT</b> /player/player-data - Update Player Data</summary>

**Base URL:** Main API

**Authentication:** Required

**Request Body:**
```json
{
    "PlayerData": "{\n\t\"PlayerDataStruct\":\n\t{\n\t\t\"PlayerProfileStruct\":\n\t\t{\n\t\t\t\"ID\": 0,\n\t\t\t\"Age\": 30,\n\t\t\t\"CycleId\": 0,\n\t\t\t\"HelmetId\": 3,\n\t\t\t\"FrameId\": 1,\n\t\t\t\"TyreId\": 1,\n\t\t\t\"FacialHairId\": 0,\n\t\t\t\"HairId\": 0,\n\t\t\t\"SkinTuneId\": 0,\n\t\t\t\"GlassesId\": 0,\n\t\t\t\"JerseyId\": 73,\n\t\t\t\"GlovesId\": 13,\n\t\t\t\"MaskId\": 0,\n\t\t\t\"SocksId\": 5,\n\t\t\t\"ShoesId\": 1,\n\t\t\t\"CountryId\": 89,\n\t\t\t\"HeightCm\": 180,\n\t\t\t\"PlayerType\": 0,\n\t\t\t\"Weight\": 75,\n\t\t\t\"Gender\": 0,\n\t\t\t\"SocksLength\": 1,\n\t\t\t\"PlayerFirstName\": \"[FirstName]\",\n\t\t\t\"PlayerLastName\": \"[LastName]\",\n\t\t\t\"TeamId\": \"-1\",\n\t\t\t\"FacialHairColorId\": 1,\n\t\t\t\"HairColorId\": 1,\n\t\t\t\"FaceEthnicityId\": 1,\n\t\t\t\"PlayerCategoryId\": 1,\n\t\t\t\"WhooshServerId\": \"[server-id]\",\n\t\t\t\"Weightage\": \"\",\n\t\t\t\"RewardJerseys\": [],\n\t\t\t\"PlayerGameModeType\": 0,\n\t\t\t\"IsCommunityManager\": false,\n\t\t\t\"DefaultValues\": false,\n\t\t\t\"PersonalizedAvatar\":\n\t\t\t{\n\t\t\t\t\"FaceEthnicityId\": -1,\n\t\t\t\t\"FacialHairId\": -1,\n\t\t\t\t\"HairId\": -1,\n\t\t\t\t\"PersonalizedJerseyId\": -1\n\t\t\t},\n\t\t\t\"CanReceiveWindEffect\": true\n\t\t},\n\t\t\"PlayerPersonalStruct\":\n\t\t{\n\t\t\t\"LanguageId\": 0,\n\t\t\t\"Coins\": 0,\n\t\t\t\"Gems\": 0,\n\t\t\t\"CryptoCoinBalance\": 0,\n\t\t\t\"BIsCurrentSeasonSubbed\": false,\n\t\t\t\"MaxPower\": 0,\n\t\t\t\"BestPower5Second\": 0,\n\t\t\t\"BestPower30Second\": 0,\n\t\t\t\"BestPower1Minute\": 0,\n\t\t\t\"BestPower3Minute\": 0,\n\t\t\t\"BestPower5Minute\": 0,\n\t\t\t\"BestPower12Minute\": 0,\n\t\t\t\"BestPower20Minute\": 0,\n\t\t\t\"BestPower30Minute\": 0,\n\t\t\t\"BestPower60Minute\": 0,\n\t\t\t\"DobDayId\": 1,\n\t\t\t\"DobMonthId\": 1,\n\t\t\t\"DobYearId\": 1990,\n\t\t\t\"LastJerseyId\": 73,\n\t\t\t\"PlayerLevel\": 1,\n\t\t\t\"VerifiedWeight\": 75,\n\t\t\t\"VerifiedHeight\": 180,\n\t\t\t\"PlayerRoleType\": 1,\n\t\t\t\"BVerified\": false,\n\t\t\t\"FtpPlayer\": 200,\n\t\t\t\"PacePlayer\": 0,\n\t\t\t\"PlayerXP\": 0,\n\t\t\t\"TotalKilometers\": 0,\n\t\t\t\"TotalElevation\": 0,\n\t\t\t\"TotalCaloriesBurn\": 0,\n\t\t\t\"TotalRideTime\": 1,\n\t\t\t\"PlayerBrakeFactor\": 1,\n\t\t\t\"AveragePower\": 0,\n\t\t\t\"AverageHeartRate\": 0,\n\t\t\t\"Email\": \"[email]\",\n\t\t\t\"WhooshServerId\": \"[server-id]\",\n\t\t\t\"RegisteredEvents\": [],\n\t\t\t\"JoinedEvents\": [],\n\t\t\t\"JoinedGroupworkouts\": [],\n\t\t\t\"WinItems\": [],\n\t\t\t\"PlayerEventsTeam\": [],\n\t\t\t\"AlltimePowerpassport\":\n\t\t\t{\n\t\t\t\t\"Power6Second\": 0,\n\t\t\t\t\"Power30Second\": 0,\n\t\t\t\t\"Power3Minute\": 0,\n\t\t\t\t\"Power12Minute\": 0\n\t\t\t},\n\t\t\t\"PreviousPowerpassport\":\n\t\t\t{\n\t\t\t\t\"Power6Second\": 0,\n\t\t\t\t\"Power30Second\": 0,\n\t\t\t\t\"Power3Minute\": 0,\n\t\t\t\t\"Power12Minute\": 0\n\t\t\t},\n\t\t\t\"ThirdPartyImportedDataList\":\n\t\t\t{\n\t\t\t\t\"MigrationPlatform\": \"\",\n\t\t\t\t\"TotalKilometers\": 0,\n\t\t\t\t\"TotalRideTime\": 0,\n\t\t\t\t\"TotalElevation\": 0\n\t\t\t},\n\t\t\t\"TotalKilometersInWeek\": 0,\n\t\t\t\"AIWorkoutInfo\": [],\n\t\t\t\"IsTuckPositionFeatureAllowedOnAnyPower\": false,\n\t\t\t\"IsTuckPositionFeatureAllowedOnAnySpeed\": false,\n\t\t\t\"IsTuckAutoEnabled\": false,\n\t\t\t\"PlayerKickedFromVoiceChatEventIds\": []\n\t\t}\n\t},\n\t\"PlayerGameData\":\n\t{\n\t\t\"MeasureUnit\": 0,\n\t\t\"BIsWhooshEnabled\": true,\n\t\t\"BIsPlayerProfileVerified\": false,\n\t\t\"PowerDisplayType\": 0,\n\t\t\"BShowGroupChat\": false,\n\t\t\"BApplyLanguageFilter\": false,\n\t\t\"PlayerPowerMultiplier\": 1,\n\t\t\"PlayerSpeedMultiplier\": 1,\n\t\t\"MusicVolume\": 0,\n\t\t\"GameVolume\": 0.5,\n\t\t\"TrainerDifficulty\": 0.5,\n\t\t\"ExtraTrainerDifficulty\": 0,\n\t\t\"BIsSecondaryPowerIconNeedToShow\": false,\n\t\t\"JoinedFitnessNetwork\": []\n\t}\n}",
    "WhooshId": "your-whoosh-id",
    "Action": 1051,
    "CorrelationId": "unique-uuid",
    "DeviceId": "device-id",
    "Authorization": ""
}
```

*Note: PlayerData is a stringified JSON object containing the complete player profile and game data structure.*

</details>

---

## Server

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /server-time - Get Server Time</summary>

**Base URL:** Main API

**Authentication:** Required

**Description:** Returns the current server time as a Unix timestamp in milliseconds.

**Response Example:**
```json
1234567890123
```

</details>

---

## Free Ride

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /free-ride/routes - Get Routes</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
[
    {
        "Name": "0",
        "WorldId": 1,
        "WorldName": "Arabia",
        "WorldDescription": "Arabia",
        "WorldActiveImageId": "W_1_I_1",
        "Routes": [
            {
                "Id": 1,
                "bIsAvailableForFreeRide": true,
                "bIsAvailableForEvents": true,
                "Name": "Jabel Hafeet",
                "Description": "Jabel Hafeet",
                "Km": 16.5,
                "Elevation": 735,
                "PeakPoint": 694,
                "LevelName": "/Game/World/TourofArabia/TourofArabia",
                "StartSplineIndex": 26,
                "InternalName": "27.77",
                "RouteType": "E_Sprint",
                "RouteMapImageId": "R_1_I_1",
                "RouteSelectedImageId": "R_1_I_2",
                "ElevationGraphImageId": "R_1_I_3",
                "SplineDistance": 2827414.75,
                "Direction": -1,
                "Latitude": 24.073631286621094,
                "Longitude": 55.75791931152344,
                "SplinePath": [15],
                "LevelScaleFactor": 1,
                "bIsNewEventsGateEnabled": false,
                "EventGateScaleValue": 1.2300000190734863,
                "RidingSideOnRoad": "E_Right",
                "MeshPathId": "",
                "SegmentStructIdsArray": ["Arabia_23"],
                "EndSplineIndex": 15,
                "EndSplineDistance": 1187956,
                "EndSplineDirection": -1,
                "Difficulty": 4
            },
            {
                "Id": 2,
                "bIsAvailableForFreeRide": true,
                "bIsAvailableForEvents": true,
                "Name": "Jabel Jais",
                "Description": "Jabel Jais",
                "Km": 21.700000762939453,
                "Elevation": 925,
                "PeakPoint": 893,
                "RouteType": "E_Sprint",
                "Difficulty": 4
            },
            {
                "Id": 3,
                "bIsAvailableForFreeRide": true,
                "bIsAvailableForEvents": true,
                "Name": "The Seven Gems",
                "Description": "The Seven Gems",
                "Km": 32.79999923706055,
                "Elevation": 206,
                "PeakPoint": 28,
                "RouteType": "E_Circuit",
                "Difficulty": 3
            },
            {
                "Id": 6,
                "Name": "Desert Pearls",
                "Description": "Desert Pearls",
                "Km": 24.200000762939453,
                "Elevation": 119,
                "RouteType": "E_Circuit",
                "Difficulty": 2
            }
            // ... more routes
        ]
    }
    // ... more worlds
]
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /free-ride/player-ghost-ride-data - Get Player Ghost Ride Data</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `whooshPlayerId` (string, required): Player's Whoosh ID

**Example:**
```
GET /free-ride/player-ghost-ride-data?whooshPlayerId=your-whoosh-id
```

**Response:**
```json
{
    "UploadedGhostRideInfo": []
}
```

</details>

---

## Bots

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /bots/free-ride/pacer-bot - Get Pacer Bot</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "RunningData": [
        {
            "GroupName": "MyBunch 24x7",
            "Color": 1,
            "RouteId": 20,
            "Speed": 10,
            "MinPowerRequired": 10,
            "LeaderId": "088c6966-3047-43d0-80d5-361b6d76d5fd",
            "PedalAssistTimer": 10,
            "MinPedalingTime": 10,
            "Pace": 6
        },
        {
            "GroupName": "MyBunch 24x7",
            "Color": 2,
            "RouteId": 23,
            "Speed": 12,
            "MinPowerRequired": 10,
            "LeaderId": "5cf7aaae-a063-4d8b-a306-32a3fe0eb1f1",
            "PedalAssistTimer": 10,
            "MinPedalingTime": 10,
            "Pace": 5
        },
        {
            "GroupName": "MyBunch 24x7",
            "Color": 3,
            "RouteId": 20,
            "Speed": 15,
            "MinPowerRequired": 10,
            "LeaderId": "d557b6bd-2260-4337-ba97-867d54a3b590",
            "PedalAssistTimer": 10,
            "MinPedalingTime": 10,
            "Pace": 4
        }
        // ... more running data
    ],
    "Data": [
        {
            "GroupName": "MyBunch 24x7",
            "Color": 1,
            "RouteId": 110,
            "Watts": 1.2,
            "Speed": 26,
            "MinPowerRequired": 60,
            "LeaderId": "449c2991-c395-44e8-89db-9848b22df5f5",
            "PedalAssistTimer": 20,
            "MinPedalingTime": 10
        },
        {
            "GroupName": "MyBunch 24x7",
            "Color": 1,
            "RouteId": 105,
            "Watts": 1.5,
            "Speed": 29,
            "MinPowerRequired": 60,
            "LeaderId": "71dcd584-a606-4801-a10c-510b6b57c5de",
            "PedalAssistTimer": 20,
            "MinPedalingTime": 10
        },
        {
            "GroupName": "MyBunch 24x7",
            "Color": 3,
            "RouteId": 68,
            "Watts": 1.8,
            "Speed": 31,
            "MinPowerRequired": 60,
            "LeaderId": "131acfb1-f09c-4e81-93e1-3398540c053f",
            "PedalAssistTimer": 20,
            "MinPedalingTime": 10
        },
        {
            "GroupName": "MyBunch 24x7",
            "Color": 2,
            "RouteId": 105,
            "Watts": 3.0,
            "Speed": 38,
            "MinPowerRequired": 60,
            "LeaderId": "806b036a-6de9-41d7-a451-1ce7705a8c16",
            "PedalAssistTimer": 20,
            "MinPedalingTime": 10
        }
        // ... more pacer bot data
    ]
}
```

</details>

---

## Economy

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /economy/bundle/info - Get Bundle Info</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "MyWhooshShopBundlesData": [
        {
            "Success": true,
            "BundleName": "Stash of Coins",
            "Price": 9,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.coinpacks1",
            "Type": "coins",
            "Reward": 1000
        },
        {
            "Success": true,
            "BundleName": "Bag of Coins",
            "Price": 49,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.coinpacks2",
            "Type": "coins",
            "Reward": 6800
        },
        {
            "Success": true,
            "BundleName": "Chest of Coins",
            "Price": 99,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.coinpacks3",
            "Type": "coins",
            "Reward": 15800
        },
        {
            "Success": true,
            "BundleName": "Hoard of Coins",
            "Price": 249,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.coinpacks4",
            "Type": "coins",
            "Reward": 47000
        },
        {
            "Success": true,
            "BundleName": "Stash of Gems",
            "Price": 3,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.gempacks1",
            "Type": "gems",
            "Reward": 15
        },
        {
            "Success": true,
            "BundleName": "Bag of Gems",
            "Price": 14,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.gempacks2",
            "Type": "gems",
            "Reward": 60
        },
        {
            "Success": true,
            "BundleName": "Gem Vault",
            "Price": 221,
            "Platform": "IOS",
            "Identifier": "com.mywhoosh.gempacks6",
            "Type": "gems",
            "Reward": 1600
        }
        // ... more bundles
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /economy/garage/item - Get Garage Items</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "MyWhooshShopItemsMetaData": [
        {
            "Id": 1,
            "Description": null,
            "Type": 7,
            "UnlockValue": 0,
            "DiscountValue": null,
            "AvailableTill": null,
            "UnlockType": 0,
            "CurrencyType": 0
        },
        {
            "Id": 2,
            "Description": null,
            "Type": 7,
            "UnlockValue": 0,
            "DiscountValue": null,
            "AvailableTill": null,
            "UnlockType": 0,
            "CurrencyType": 0
        },
        {
            "Id": 3,
            "Description": null,
            "Type": 7,
            "UnlockValue": 0,
            "DiscountValue": null,
            "AvailableTill": null,
            "UnlockType": 0,
            "CurrencyType": 0
        }
        // ... more garage items
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /economy/calculations - Get Calculations</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `CurrentLevel` (integer): Player's current level

**Example:**
```
GET /economy/calculations?CurrentLevel=1
```

**Response:**
```json
{
    "XpLevelUpData": [
        {
            "UserLevel": 1,
            "TotalXPRequired": 0,
            "XPRequiredPerLevel": 0,
            "LevelUpCoinsReward": 0
        },
        {
            "UserLevel": 2,
            "TotalXPRequired": 100,
            "XPRequiredPerLevel": 100,
            "LevelUpCoinsReward": 100
        },
        {
            "UserLevel": 3,
            "TotalXPRequired": 230,
            "XPRequiredPerLevel": 130,
            "LevelUpCoinsReward": 100
        },
        {
            "UserLevel": 5,
            "TotalXPRequired": 620,
            "XPRequiredPerLevel": 220,
            "LevelUpCoinsReward": 100
        },
        {
            "UserLevel": 10,
            "TotalXPRequired": 3250,
            "XPRequiredPerLevel": 830,
            "LevelUpCoinsReward": 100
        }
        // ... more levels
    ],
    "XPRewardMultipliers": {
        "GameMode": "Any",
        "WorkoutMultiplier": 1,
        "FreeRideMultiplier": 1,
        "XPRewardPerKilometerDistance": 3,
        "Worlds": [],
        "XPRewardPerMinute": 2,
        "XPRewardPerMeterElevation": 1,
        "WorkoutCompletionMultiplier": 4,
        "RouteCompletionMultiplier": 50,
        "EventsMultiplier": 1
    },
    "CoinsRewardMultipliers": {
        "GameMode": "Any",
        "WorkoutMultiplier": 1,
        "FreeRideMultiplier": 1,
        "Worlds": [],
        "CoinsRewardPerKilometerDistance": 20,
        "CoinsRewardPerMeterElevation": 8,
        "WorkoutCompletionMultiplier": 3,
        "CoinsRewardPerMinute": 14,
        "RouteCompletionMultiplier": 250,
        "EventsMultiplier": 1
    },
    "LevelUpCoinRewardData": {
        "LevelUpGroup1Max": 10,
        "LevelUpGroup1Min": 1,
        "LevelUpGroup1Multiplier": 0.1,
        "LevelUpGroup2Max": 15,
        "LevelUpGroup2Min": 11,
        "LevelUpGroup2Multiplier": 0.08,
        "LevelUpGroup3Max": 30,
        "LevelUpGroup3Min": 16,
        "LevelUpGroup3Multiplier": 0.06,
        "LevelUpGroup4Max": 150,
        "LevelUpGroup4Min": 31,
        "LevelUpGroup4Multiplier": 0.06
    }
}
```

</details>

---

## Config

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /config/age-config - Get Age Config</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "MyAgeCategory": 1,
    "bCanAccessChat": true,
    "bCanAccessEvents": true,
    "bAllowVoiceChat": true,
    "bCanAccessCalendar": true,
    "bAllowCardPurchases": true,
    "bAllowSeasonPass": true,
    "bAllowMission": true,
    "bAllowRideWithFriends": true,
    "bAllowTHunt": true,
    "bAllowLiveCoaching": true,
    "bAllowArcadeMode": true,
    "bVerified": true
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /http-service/v1/config/age-config-data - Get Age Config Data</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `emailId` (string): Email address

</details>

---

## Connectapp Host

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /connectapp-host/{whooshId} - Get Connectapp Host Info</summary>

**Base URL:** Main API

**Authentication:** Required

**Path Parameters:**
- `whooshId` (string): User's Whoosh ID

</details>

---

## Client

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /client/custom-workout-upload/{whooshId} - Get Custom Workout Upload</summary>

**Base URL:** Coaching API

**Authentication:** Required

**Path Parameters:**
- `whooshId` (string): User's Whoosh ID

**Description:** Returns the S3 URL to download custom workouts. Use this URL in the POST request to upload custom workouts.

**Response:**
```json
{
    "data": {
        "userId": "[whoosh-id]",
        "workoutZipUrl": "https://s3.eu-west-1.amazonaws.com/mywhooshprod/custom-workouts/workouts-[user-id]-[timestamp].zip?X-Amz-Algorithm=AWS4-HMAC-SHA256&...",
        "workoutCount": 4
    }
}
```

*Note: The `workoutZipUrl` is a pre-signed S3 URL that expires after 600 seconds (10 minutes).*

</details>

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /client/custom-workout-upload - Upload Custom Workout</summary>

**Base URL:** Coaching API

**Authentication:** Required

**Request Body:**
```json
{
    "UserId": "your-whoosh-id",
    "WorkoutsData": [
        {
            "Id": "[random-unique-id]",
            "Name": "Custom Workout",
            "Description": "Custom workout description",
            "Mode": "E_Ride",
            "ERGMode": "E_OFF",
            "IsRecovery": false,
            "IsIntervals": false,
            "FTPMode": "E_NoFTP",
            "IsTT": false,
            "IsTSS": false,
            "IsIF": false,
            "FTPMultiplier": 0,
            "StressPoint": 0,
            "Time": 5460,
            "CustomTagDescription": "",
            "CategoryId": 1,
            "SubcategoryId": 0,
            "Type": "E_Custom",
            "DisplayType": "E_byWatts",
            "StepCount": 10,
            "IsFavorite": false,
            "CompletedCount": 0,
            "WorkoutStepsArray": [
                {
                    "Id": 1,
                    "Pace": 1,
                    "IntervalId": 0,
                    "WorkoutMessage": [],
                    "Rpm": 0,
                    "StepType": "E_Normal",
                    "Power": 0.55,
                    "StartPower": 0,
                    "EndPower": 0,
                    "Time": 300,
                    "IsManualGrade": false,
                    "ManualGradeValue": 0,
                    "ShowAveragePower": false,
                    "FlatRoad": 0
                },
                {
                    "Id": 2,
                    "Pace": 1,
                    "IntervalId": 0,
                    "WorkoutMessage": [],
                    "Rpm": 0,
                    "StepType": "E_Normal",
                    "Power": 0.75,
                    "StartPower": 0,
                    "EndPower": 0,
                    "Time": 360,
                    "IsManualGrade": false,
                    "ManualGradeValue": 0,
                    "ShowAveragePower": false,
                    "FlatRoad": 0
                },
                {
                    "Id": 7,
                    "Pace": 1,
                    "IntervalId": 0,
                    "WorkoutMessage": [],
                    "Rpm": 0,
                    "StepType": "E_WarmUp",
                    "Power": 0,
                    "StartPower": 0.55,
                    "EndPower": 1.2,
                    "Time": 600,
                    "IsManualGrade": false,
                    "ManualGradeValue": 0,
                    "ShowAveragePower": false,
                    "FlatRoad": 0
                },
                {
                    "Id": 8,
                    "Pace": 1,
                    "IntervalId": 0,
                    "WorkoutMessage": [],
                    "Rpm": 0,
                    "StepType": "E_CoolDown",
                    "Power": 0,
                    "StartPower": 1.2,
                    "EndPower": 0.55,
                    "Time": 600,
                    "IsManualGrade": false,
                    "ManualGradeValue": 0,
                    "ShowAveragePower": false,
                    "FlatRoad": 0
                },
                {
                    "Id": 15,
                    "Pace": 1,
                    "IntervalId": 0,
                    "WorkoutMessage": [
                        {
                            "Id": 0,
                            "Time": 0,
                            "Message": "Custom message"
                        }
                    ],
                    "Rpm": 0,
                    "StepType": "E_FreeRide",
                    "Power": 0,
                    "StartPower": 0,
                    "EndPower": 0,
                    "Time": 600,
                    "IsManualGrade": false,
                    "ManualGradeValue": 0,
                    "ShowAveragePower": false,
                    "FlatRoad": 0
                }
            ],
            "AuthorName": "",
            "WorkoutSteps": {},
            "WorkoutstepsTMap": [],
            "WokoutAssociationId": 0,
            "IF": 0,
            "TSS": 158,
            "KJ": 0,
            "IsVODAvailable": false
        }
    ]
}
```

**Important:** The workout `Id` must be unique.

**Response:**
```json
{
    "message": "Custom workout is being uploaded.",
    "display": true
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /client/coach - Get Coach</summary>

**Base URL:** Coaching API

**Authentication:** Required

**Response:**
```json
{
    "data": [
        {
            "Id": "65e60094486f17003f0af982",
            "Name": "Liz Smithson",
            "ImageUrl": "https://service23.mywhoosh.com/user_profile/I93Q1joS6ot9yyO5U1syEG1OufsWFXf52YSMxBgc.jpg/800/800/resize"
        },
        {
            "Id": "65e60a14a23beb7b78520d43",
            "Name": "Si Bradeley",
            "ImageUrl": "https://service24.mywhoosh.com/user_profile/954bcb90-88e4-4ea4-8faa-a206175e8f6b.jpg/600/800/resize"
        },
        {
            "Id": "66029e99ae45211fe900364e",
            "Name": "Matt Smithson",
            "ImageUrl": "https://service23.mywhoosh.com/user_profile/jKL3HSlDE0ofhMZZHPSe4Al1bjEo6kDA0OopApzD.jpeg/800/800/resize"
        },
        {
            "Id": "66bb1e7893f3b34d1c2409d6",
            "Name": "Tim Don",
            "ImageUrl": "https://service23.mywhoosh.com/user_profile/PH2yKkTw8tVXO4L4xN6JG3U4TuBELvZUUJuLJSBI.jpg/800/800/resize"
        },
        {
            "Id": "67a209938c9aed17d552b75b",
            "Name": "Peter Sagan",
            "ImageUrl": "https://service23.mywhoosh.com/user_profile/jsqTtGyiyKfokjtFR98jASEoHj1ygdCkJw0YEUfN.jpg/800/800/resize"
        },
        {
            "Id": "6903383a0c48657d4606d57b",
            "Name": "Tadej Pogacar",
            "ImageUrl": "https://service24.mywhoosh.com/user_profile/b3e5965e-827f-4616-afe5-313d514173f2.png/600/800/resize"
        },
        {
            "Id": "67e28faf4a83459f00007a07",
            "Name": "Georgia Taylor-Brown",
            "ImageUrl": "https://service24.mywhoosh.com/user_profile/5ab0d572-d72e-4b5d-8a69-f3e72776d51c.png/600/800/resize"
        }
        // ... more coaches
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /client/vod - Get VOD</summary>

**Base URL:** Coaching API

**Authentication:** Required

**Response:**
```json
{
    "data": [
        {
            "Id": "a8e38227-e501-4a69-979c-5f2e88ace83f",
            "Type": 0,
            "ActivityId": "192",
            "CreatorId": "65e60094486f17003f0af982",
            "Title": "2min Anaerobic Capacity",
            "Status": 1,
            "Description": "2min Anaerobic Capacity",
            "StreamUrl": "https://streaming.mywhoosh.com/vod/_definst_/files/vod/65e60ad7f722049cc5c41637.mp4/manifest.mpd",
            "Tags": ["workout"]
        },
        {
            "Id": "37f3fa0e-7c51-4889-b3ce-a1bb9e440008",
            "Type": 0,
            "ActivityId": "193",
            "CreatorId": "65e60a14a23beb7b78520d43",
            "Title": "30by30s Anaerobic 1",
            "Status": 1,
            "Description": "30by30s Anaerobic 1",
            "StreamUrl": "https://streaming.mywhoosh.com/vod/_definst_/files/vod/65e60d219c32e2fae86c4630.mp4/manifest.mpd",
            "Tags": ["Anaerobic", "Workout"]
        },
        {
            "Id": "3826fa63-1347-4a34-ba8c-caa29ee8f3e2",
            "Type": 0,
            "ActivityId": "20",
            "CreatorId": "65e60094486f17003f0af982",
            "Title": "Intervals What are they",
            "Status": 1,
            "Description": "Intervals What are They",
            "StreamUrl": "https://streaming.mywhoosh.com/vod/_definst_/files/vod/65e60e499c32e2fae86c488b.mp4/manifest.mpd",
            "Tags": ["workout"]
        },
        {
            "Id": "ec2d39ab-d7fe-4d0f-84df-3d2fbbc521cd",
            "Type": 0,
            "ActivityId": "101",
            "CreatorId": "65e60a14a23beb7b78520d43",
            "Title": "Race Attacks #3 With Coach Si",
            "Status": 1,
            "Description": "This is a great race preparation session for beginners. The intervals are not too long, but they are completed at a very high intensity.",
            "StreamUrl": "https://streaming.mywhoosh.com/vod/_definst_/files/vod/666bf077f63631e81feb9e24.mp4/manifest.mpd",
            "Tags": []
        },
        {
            "Id": "1c18c9ec-7553-4cf9-be61-dd2c39daedf7",
            "Type": 0,
            "ActivityId": "18",
            "CreatorId": "65e60a14a23beb7b78520d43",
            "Title": "High Torque Hills #1 With Coach Si",
            "Status": 1,
            "Description": "When we complete long climbs, the lower cadence results in high crank torque.",
            "StreamUrl": "https://streaming.mywhoosh.com/vod/_definst_/files/vod/...",
            "Tags": []
        }
        // ... more VOD content
    ]
}
```

</details>

---

## Mobile

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /mobile/workout/download - Download Calendar Workouts</summary>

**Base URL:** Service 20

**Authentication:** Required

**Query Parameters:**
- `player_id` (string): Player's Whoosh ID
- `type` (string): "calendar"

**Example:**
```
POST /mobile/workout/download?player_id=your-whoosh-id&type=calendar
```

**Response:**
```json
{
    "status": false,
    "display": false,
    "message": "Player calendar file not found."
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /mobile/workout/download - Download Favorite Workouts</summary>

**Base URL:** Service 20

**Authentication:** Required

**Query Parameters:**
- `player_id` (string): Player's Whoosh ID
- `type` (string): "favorite"

**Example:**
```
POST /mobile/workout/download?player_id=your-whoosh-id&type=favorite
```

**Response:**
```json
{
    "status": true,
    "display": false,
    "message": "File downloaded successfully.",
    "data": {
        "listOfFavouriteWorkouts": [
            {
                "workoutName": "Custom Workout 1",
                "workoutId": 1765408158,
                "type": "E_Cycling"
            },
            {
                "workoutName": "Custom Workout 2",
                "workoutId": 1,
                "type": "E_Cycling"
            },
            {
                "workoutName": "Custom Workout 3",
                "workoutId": 1765407485,
                "type": "E_Cycling"
            }
        ]
    }
}
```

</details>

---

## Achievements & Trophies

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /achievement-trophies/player-achievement - Get Player Achievements</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `UserId` (string): Player's Whoosh ID

**Response:**
```json
{
    "id": 830336,
    "achievementProgressArr": [
        {
            "achievementId": "Ach_RideAccumulative_1",
            "achievementProgress": 0.0,
            "isComplete": false,
            "isRewardCompleted": false,
            "created_on": "2025-12-09 03:10:58",
            "updated_on": "2025-12-09 03:10:58"
        },
        {
            "achievementId": "Ach_RideAccumulative_2",
            "achievementProgress": 0.0,
            "isComplete": false,
            "isRewardCompleted": false,
            "created_on": "2025-12-09 03:10:58",
            "updated_on": "2025-12-09 03:10:58"
        },
        {
            "achievementId": "Ach_ClimbAccumulative_1",
            "achievementProgress": 0.0,
            "isComplete": false,
            "isRewardCompleted": false,
            "created_on": "2025-12-09 03:10:58",
            "updated_on": "2025-12-09 03:10:58"
        },
        {
            "achievementId": "Ach_RideTime_1",
            "achievementProgress": 0.0,
            "isComplete": false,
            "isRewardCompleted": false,
            "created_on": "2025-12-09 03:10:58",
            "updated_on": "2025-12-09 03:10:58"
        },
        {
            "achievementId": "Ach_Customize",
            "achievementProgress": 1.0,
            "isComplete": true,
            "isRewardCompleted": false,
            "created_on": "2025-12-11 03:34:33",
            "updated_on": "2025-12-11 03:34:33"
        }
        // ... more achievements
    ],
    "userId": "[whoosh-id]",
    "deviceId": "[device-id]",
    "distanceStat": 0,
    "elevationStat": 0.0,
    "timeStat": 1.0,
    "segmentStat": 0,
    "workoutStat": 0,
    "normalEventParticipatedStat": 0,
    "premiumEventParticipatedStat": 0,
    "created_on": "2025-12-09 03:10:59",
    "updated_on": "2025-12-11 03:34:33",
    "clientLoggedTime": 1765409673
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /achievement-trophies/player-trophies-jerseys - Get Player Trophies and Jerseys</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `UserId` (string): Player's Whoosh ID

**Response:**
```json
{
    "jerseys": [],
    "eventCompletionRewards": [],
    "trophies": [],
    "userId": "[whoosh-id]"
}
```

</details>

---

## Season Pass

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /season-pass/progress - Get Season Pass Progress</summary>

**Base URL:** Main API

**Authentication:** Required

**Query Parameters:**
- `userId` (string): Player's Whoosh ID
- `seasonId` (string): Season ID

**Example:**
```
GET /season-pass/progress?userId=your-whoosh-id&seasonId=season-uuid
```

</details>

---

## Mission Challenge

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /mission-challenge/mission - Get Missions</summary>

**Base URL:** Main API

**Authentication:** Required

**Response:**
```json
{
    "Missions": [
        {
            "ChallengeIds": [
                "68639b81cc3bbf202b0ee552",
                "68639b82cc3bbf202b0ee553",
                "68639b83cc3bbf202b0ee554"
            ],
            "MissionId": "6d6c4d8b-b3ac-4868-b9f1-f85b1338cb65",
            "Name": "Pursuit of Yellow",
            "Description": "Pursuit of Yellow",
            "Image": "Badge_1 1",
            "StartDate": 1751659200,
            "EndDate": 1754337599,
            "Rewards": [
                {
                    "RewardId": "7befedf4-a38e-4a64-9f4d-1ec15b6ad563",
                    "RewardType": 3,
                    "Amount": 1.0,
                    "ItemId": "31",
                    "FemaleItemId": "31",
                    "ItemType": 0
                },
                {
                    "RewardId": "bd485371-f3ba-4d9a-a056-31ce976056e4",
                    "RewardType": 3,
                    "Amount": 1.0,
                    "ItemId": "22",
                    "FemaleItemId": "22",
                    "ItemType": 1
                }
            ]
        },
        {
            "ChallengeIds": [
                "68907305cc3bbf202b0ee56a",
                "68907308cc3bbf202b0ee56b",
                "68907308cc3bbf202b0ee56c"
            ],
            "MissionId": "cf7f2a8c-653b-4c84-af79-d0c88a355afb",
            "Name": "Vuelta Vertical",
            "Description": "Vuelta Vertical",
            "Image": "Badge_2 2",
            "StartDate": 1755547200,
            "EndDate": 1758657599,
            "Rewards": [
                {
                    "RewardId": "7845e7c4-029b-4236-8cc1-f7adda0fe4c3",
                    "RewardType": 3,
                    "Amount": 1.0,
                    "ItemId": "17",
                    "FemaleItemId": "17",
                    "ItemType": 0
                }
            ]
        },
        {
            "ChallengeIds": [
                "68c2dbc0e3cf6a508c169fcd",
                "68c2dbc0943db9dc14efe82a",
                "68c2dbc0943db9dc14efe82b"
            ],
            "MissionId": "40b11147-3615-4d8f-9855-1aeaf3066e12",
            "Name": "Chasing Rainbows",
            "Description": "Chasing Rainbows",
            "Image": "10_October",
            "StartDate": 1757880000,
            "EndDate": 1760385599,
            "Rewards": []
        }
        // ... more missions
    ]
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /mission-challenge/progress - Get Mission Progress</summary>

**Base URL:** Main API

**Authentication:** Required

</details>

---

## Events

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /events - Get Events</summary>

**Base URL:** Service 26

**Authentication:** Required

**Query Parameters:**
- `zone-offset` (string): Base64 encoded timezone offset
- `date` (integer): Date filter (-1 for all)
- `SportsMode` (string): e.g., "E_Cycling"
- `platform` (string): e.g., "mobile"

**Example:**
```
GET /events?zone-offset=KzAxOjAwOjAwLjAwMA==&date=-1&SportsMode=E_Cycling&platform=mobile
```

**Response:**
```json
{
    "ListOfEventData": [
        {
            "EventId": "8b899f8b-ca9b-4c8c-903b-40930153e80d",
            "Description": "MyWhoosh ITT - You. The Clock. Nothing Else. The MyWhoosh Individual Time Trial is the ultimate solo challenge.",
            "YoutubeUrlToSpectateEvent": "http://www.youtube.com/my/live",
            "bCanNormalUserSpectateEventInGame": true,
            "CurrentDayNumber": 1,
            "MinimumVersionRequired": 88,
            "EventJoinStatus": 1,
            "EventType": 3,
            "GenderType": 2,
            "EventOccurType": 2,
            "DayId": "fb6adbd5-017c-479e-9f89-72bd033cdfac",
            "Stages": [
                {
                    "StartTime": 1766662200,
                    "TotalDistance": 16.4,
                    "StageId": "ea320217-962f-4680-9fa1-58eee90bc0e4",
                    "DayName": "MyWhoosh ITT League",
                    "DayDescription": "MyWhoosh ITT League description",
                    "Elevation": "0",
                    "NoOfLaps": 2,
                    "RouteId": 59,
                    "RouteFileUrl": "",
                    "EventWeightType": 0,
                    "TotalDuration": 5200,
                    "RequiredWeight": 1.0,
                    "EventRouteImageUrl": "",
                    "CategoryStartTimes": [],
                    "EventThumbnailImageUrl": "https://service24.mywhoosh.com/public/f95a8450-3060-423c-8363-4a0d4f39912a.png/1024/1024/resize",
                    "EventBannerImageUrl": "https://service24.mywhoosh.com/public/20a470c3-fecf-4dad-b453-01b7808ed032.png/1024/1024/resize",
                    "TotalNumOfControllableCompanionBots": 0,
                    "SportsMode": 0,
                    "IdentifierTag": "",
                    "WindProperties": {
                        "IsWindEnabled": true,
                        "WindAngleInStart": 60.0,
                        "MinimumSpeedOfWind": 2.0,
                        "MaximumSpeedOfWind": 4.0,
                        "SpeedChangeIntervalMinimum": 60,
                        "SpeedChangeIntervalMaximum": 90
                    }
                }
            ],
            "TotalNumOfControllableCompanionBots": 0,
            "BIsSpectateEnabled": true,
            "TotalNumberOfDays": 1,
            "SportsModeType": [0],
            "bIsLateJoiningEnabled": false,
            "TimeToAllowLateJoin": 30,
            "CategorizationStruct": {
                "RuleType": "E_None",
                "CategoryRules": []
            }
        },
        {
            "EventId": "3241a142-45f4-48aa-93fb-b276fd117e54",
            "Description": "Team Mongolia MyWhoosh",
            "YoutubeUrlToSpectateEvent": "http://www.youtube.com/my/live",
            "bCanNormalUserSpectateEventInGame": true,
            "CurrentDayNumber": 1,
            "MinimumVersionRequired": 88,
            "EventJoinStatus": 1,
            "EventType": 1,
            "GenderType": 2,
            "EventOccurType": 3,
            "DayId": "1a65594c-024d-4cb7-b5b3-2d69eea592a7",
            "Stages": [
                {
                    "StartTime": 1766660400,
                    "TotalDistance": 23.5,
                    "StageId": "7900e4a5-cd61-4ca6-afc5-1a3320126902",
                    "DayName": "Team Mongolia",
                    "RouteId": 59
                }
            ],
            "TotalNumberOfDays": 1
        }
        // ... more events
    ]
}
```

</details>

---

## Group Workout

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /group-workout - Get Group Workouts</summary>

**Base URL:** Service 26

**Authentication:** Required

**Query Parameters:**
- `zone-offset` (string): Base64 encoded timezone offset
- `platform` (string): e.g., "mobile"

**Response:**
```json
{
    "ListOfWorkoutData": [
        {
            "bIsDraftingEnabled": null,
            "bIsSpectateEnabled": true,
            "RouteId": 16,
            "RouteName": "Parramatta",
            "WorkoutEventId": "1b9fd09c-8491-4a89-9d7f-8a3443bf6539",
            "WorkoutName": "Sub Threshold #1",
            "StartSplineIndex": 23,
            "EndSplineIndex": 23,
            "StartSplineDistance": 2,
            "EndSplineDistance": 5,
            "TotalDuration": 4000,
            "WorkoutData": {
                "WorkoutId": 431,
                "WorkoutType": 0,
                "WorkoutName": "Sub Threshold #1"
            },
            "Description": "Welcome to Group Workouts MyWhoosh. Our MyPacer will set the tempo for your Group Workout today.",
            "LeaderData": {
                "LeaderId": null,
                "LeaderName": null,
                "LeaderFTP": null,
                "LeaderHeight": null,
                "BotProfileStruct": {
                    "JerseyId": 62,
                    "FrameId": 9,
                    "Weight": 75,
                    "HeightCm": 178,
                    "LeaderFTP": 250,
                    "PlayerFirstName": "MyWhoosh",
                    "PlayerLastName": "MyPacer"
                }
            },
            "DynamicSettings": [
                {
                    "Range": 0.0,
                    "Booster": 20.0
                },
                {
                    "Range": 10.0,
                    "Booster": 80.0
                },
                {
                    "Range": 50.0,
                    "Booster": 150.0
                }
            ],
            "SplinePath": [1],
            "StartTime": 1728880200,
            "LeaderType": 2,
            "Status": 1,
            "bIsLiveCoachingEnabled": false,
            "StreamUrl": null,
            "CoachId": null,
            "bIsStreamable": false,
            "WindProperties": {
                "IsWindEnabled": false,
                "WindAngleInStart": 0.0,
                "MinimumSpeedOfWind": 4.0,
                "MaximumSpeedOfWind": 6.0,
                "SpeedChangeIntervalMinimum": 60,
                "SpeedChangeIntervalMaximum": 90
            }
        },
        {
            "bIsDraftingEnabled": null,
            "bIsSpectateEnabled": true,
            "RouteId": 15,
            "RouteName": "Coffee Trail",
            "WorkoutEventId": "28b49658-cae0-49c9-ad01-cd2cca7bd9ef",
            "WorkoutName": "Anaerobic Capacity 1min & 2min",
            "StartSplineIndex": 14,
            "EndSplineIndex": 14,
            "StartSplineDistance": 1,
            "EndSplineDistance": 29,
            "TotalDuration": 4000,
            "WorkoutData": {
                "WorkoutId": 203,
                "WorkoutType": 0,
                "WorkoutName": "Anaerobic Capacity 1min & 2min"
            }
        }
        // ... more group workouts
    ]
}
```

</details>

---

## Data Recovery

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /data-recovery/pending-ride - Get Pending Ride</summary>

**Base URL:** Data Recovery

**Authentication:** Required

</details>

---

## Task (Calendar)

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /task/create - Create Task</summary>

**Base URL:** Service 14

**Authentication:** Required

**Request Body:**
```json
{
    "TaskId": "",
    "TaskType": "E_Event",
    "TaskStartedTimeEpoc": 1765402200,
    "TaskTypeId": "event-uuid",
    "CurDayId": "day-uuid",
    "TaskState": "E_NotStarted",
    "DayNo": 0,
    "TaskEndEpochTime": 1765402200,
    "MapId": 0,
    "TaskName": "Event Name",
    "TaskDescription": "Event Description",
    "TotalKilometers": 18.9,
    "TotalElevation": 0,
    "TSS": 0,
    "SportMode": "E_Cycling"
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/f93e3e/f93e3e.png" alt="DELETE"/> <b>DELETE</b> /task/{taskId} - Delete Task</summary>

**Base URL:** Service 14

**Authentication:** Required

**Path Parameters:**
- `taskId` (string): Task ID to delete

**Response:**
```json
{
    "status": true,
    "code": 200,
    "message": "",
    "data": {
        "id": "[task-id]"
    },
    "errors": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /task/date-range-task-list - Get Date Range Task List</summary>

**Base URL:** Service 14

**Authentication:** Required

**Query Parameters:**
- `startDate` (integer): Start date (Unix timestamp)
- `endDate` (integer): End date (Unix timestamp)

**Example:**
```
GET /task/date-range-task-list?startDate=1748217600&endDate=1748822399
```

**Response:**
```json
{
    "status": true,
    "code": 200,
    "message": "",
    "data": {
        "startDate": 1748217600,
        "endDate": 1748822399,
        "taskList": []
    },
    "errors": []
}
```

</details>

---

## Leaderboard

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /leaderboard-service/arcade/player/all - Get All Player Leaderboards</summary>

**Base URL:** Public API (Short)

**Authentication:** Required

**Response:**
```json
{
    "Easy": [],
    "Medium": [],
    "Hard": []
}
```

</details>

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /leaderboard-service/arcade - Get Arcade Leaderboard</summary>

**Base URL:** Public API (Short)

**Authentication:** Required

**Response:**
```json
{
    "ListOfPlayers": [
        {
            "Rank": 1,
            "PlayerId": "[player-id]",
            "PlayerName": "[Player Name]",
            "RideType": "arcade",
            "WorldId": 9009,
            "DifficultyLevel": 1,
            "Point": 75173,
            "RideDate": 1760615311,
            "WattPerKg": 7.96,
            "CountryId": 1,
            "RideDuration": 5262
        },
        {
            "Rank": 2,
            "PlayerId": "[player-id]",
            "PlayerName": "[Player Name]",
            "RideType": "arcade",
            "WorldId": 9009,
            "DifficultyLevel": 3,
            "Point": 71548,
            "RideDate": 1761103298,
            "WattPerKg": 9.39344,
            "CountryId": 103,
            "RideDuration": 3065
        },
        {
            "Rank": 3,
            "PlayerId": "[player-id]",
            "PlayerName": "[Player Name]",
            "RideType": "arcade",
            "WorldId": 9009,
            "DifficultyLevel": 1,
            "Point": 52962,
            "RideDate": 1760808636,
            "WattPerKg": 10.0,
            "CountryId": 249,
            "RideDuration": 3469
        }
        // ... more players
    ]
}
```

</details>

---

## Coupon

<details>
<summary><img src="https://placehold.co/15x15/fca130/fca130.png" alt="POST"/> <b>POST</b> /coupon/redeem - Redeem Coupon</summary>

**Base URL:** Main API

**Authentication:** Required

**Request Body:**
```json
{
    "CouponCode": "[coupon-code]",
    "WhooshId": "your-whoosh-id",
    "ResponseString": "",
    "TotalCoins": 0,
    "TotalGems": 0,
    "IsCouponRedeemSuccessfully": true
}
```

**Response:**
```json
{
    "WhooshId": "[whoosh-id]",
    "CouponCode": "[coupon-code]",
    "ResponseString": "Invalid coupon code",
    "TotalGems": 0,
    "TotalCoins": 0,
    "isCouponRedeemSuccessfully": false
}
```

</details>

---

## Maintenance

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> /v1/maintenance - Get Maintenance Status</summary>

**Base URL:** Public API

**Authentication:** Not required

**Response:**
```json
{
    "ListOfNotifications": [
        {
            "display": true,
            "start_date_time": 1764580800,
            "end_date_time": 1765185900,
            "message": "Notification message text",
            "title": "Notification Title",
            "message_type": 1,
            "button_text": "Save",
            "NotificationType": 1,
            "BannerImageForNotification": "https://service23.mywhoosh.com/notifications/banner/image.png/900/720/fit",
            "ThumbnailImageForNotification": "https://service23.mywhoosh.com/notifications/thumbnail/image.png/350/350/fit",
            "FeatureName": null
        }
    ],
    "ServerTime": 1766662774586
}
```

</details>

---

## S3 / Assets

<details>
<summary><img src="https://placehold.co/15x15/49cc90/49cc90.png" alt="GET"/> <b>GET</b> {workoutZipUrl} - Get Workout ZIP</summary>

**Base URL:** Dynamic (S3 URL)

**Authentication:** Not required (pre-signed URL)

**Description:** Downloads a ZIP file containing custom workouts as JSON files. The URL is obtained from GET /client/custom-workout-upload/{whooshId}.

**Response:** Binary data (application/zip)

The ZIP file contains workout JSON files with the following structure:
- Each workout is stored as a separate JSON file
- Files contain complete workout definitions including steps, intervals, and metadata

**Example ZIP Contents:**

![S3 ZIP Contents](docs/assets/S3-Amazon-ZIP-Screenshot.png)

</details>

---

## Common Request Parameters

Most authenticated endpoints accept these common parameters:

- `Action` (integer): Action code identifying the operation
- `CorrelationId` (string): Unique UUID for request tracking
- `DeviceId` (string): Device identifier
- `Authorization` (string): Usually empty when using Bearer token

---

## Error Responses

All endpoints may return standard HTTP error codes:

- <span style="color: #f93e3e; font-weight: bold;">400 Bad Request</span> - Invalid parameters
- <span style="color: #f93e3e; font-weight: bold;">401 Unauthorized</span> - Missing or invalid authentication
- <span style="color: #f93e3e; font-weight: bold;">403 Forbidden</span> - Insufficient permissions
- <span style="color: #f93e3e; font-weight: bold;">404 Not Found</span> - Resource not found
- <span style="color: #f93e3e; font-weight: bold;">500 Internal Server Error</span> - Server error

---

## Notes

- All timestamps are Unix epoch time (seconds since 1970-01-01)
- UUIDs are in standard format: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
- Base64 encoded values (like zone-offset) should be properly encoded
- The `WhooshId` is your unique player identifier obtained during login
- Store the `AccessToken` securely and refresh when expired


