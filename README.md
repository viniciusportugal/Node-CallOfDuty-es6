# MAJOR CHANGES

You will now have to login to the API before making any requests. This means you will need a call of duty account.
Simply call:
```javascript
 import { api, platforms } from 'call-of-duty-api-es6';
 const API = new api(<platform?>, <debug?>, <ratelimit?>);
 API.login("<email>", "<password>").then(<?>).catch(<?>);
```
Reasons for this is to bypass a rate limitting issue.

I have also implemented axios-rate-limit incase you want to implement your own rate limitting.
All you need to do is pass a ratelimit object when initializing the module.

```javascript
    ratelimit: { maxRequests: 2, perMilliseconds: 1000, maxRPS: 2 };
```
You can find out more about axios-rate-limit [here](https://www.npmjs.com/package/axios-rate-limit)

# Discord

Join the discord: [here](https://discord.gg/NuUpvzC)

# Call Of Duty API Wrapper

Call of Duty Api is a wrapper for the "private" API that Activision use on the callofduty.com website.

## List of Platforms
-   psn
-   steam
-   xbl
-   battle
-   uno (activision ID)
```javascript
//How to use
platforms.psn
```
Please note:
`uno` is for looking up via activision ID and this is only supported on a couple of endpoints.
### Supported Endpoints for activision ID
-   MWcombatmp
-   MWcombatwz
-   MWmp
-   MWwz
-   MWstats

## Get Stats
```javascript
API.MWstats(<gamertag>, platforms.<platform>).then((output) => {
    console.log(output);  
}).catch((err) => {
    console.log(err);
});
```

## Output
```javascript 
{
    title: 'mw',
    platform: 'platform',
    username: 'gamertag',
    mp:
    { lifetime: { all: [Object], mode: [Object] },
    weekly: null,
    level: 0,
    maxLevel: 0,
    levelXpRemainder: 0,
    levelXpGained: 0,
    prestige: 0,
    prestigeId: 0,
    maxPrestige: 0 },
    zombies:
    { lifetime: { all: [Object], mode: {} },
    weekly: { all: [Object], mode: {} } },
    engagement: { timePlayedAll: 440544, seasonPass: 1 } 
}
```
---

# Example Project
```javascript
import { api, platforms } from 'call-of-duty-api-es6';
const API = new api(platforms.battle);
//I want Warzone Data
API.MWwz('Lierrmm#2364').then(data => {
    console.log(data);  // see output
}).catch(err => {
    console.log(err);
});
```
## Output
```javascript
[ br: { wins: 1,
    kills: 77,
    kdRatio: 1.2833333333333334,       
    downs: 70,
    topTwentyFive: 20,
    topTen: 11,
    contracts: 15,
    revives: 0,
    topFive: 6,
    score: 55600,
    timePlayed: 27169,
    gamesPlayed: 20,
    scorePerMinute: 122.78699988958003,
    cash: 0,
    deaths: 60,
    title: 'br' },
  br_dmz: { wins: 0,
    kills: 9,
    kdRatio: 1.2857142857142858,
    downs: 11,
    topTwentyFive: 0,
    topTen: 0,
    contracts: 2,
    revives: 0,
    topFive: 0,
    score: 4574,
    timePlayed: 1786,
    gamesPlayed: 1,
    scorePerMinute: 153.66181410974244,
    cash: 53,
    deaths: 7,
    title: 'br_dmz' },
  br_all: { wins: 1,
    kills: 86,
    kdRatio: 1.2835820895522387,
    downs: 81,
    topTwentyFive: 20,
    topTen: 11,
    contracts: 17,
    revives: 0,
    topFive: 6,
    score: 60174,
    timePlayed: 28955,
    gamesPlayed: 21,
    scorePerMinute: 124.6914177171473,
    cash: 53,
    deaths: 67,
    title: 'br_all' } ]
```