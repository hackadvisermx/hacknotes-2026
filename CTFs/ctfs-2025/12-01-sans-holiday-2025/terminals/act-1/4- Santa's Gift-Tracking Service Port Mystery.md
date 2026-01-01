```
======= Neighborhood Santa-Tracking Service =======

Oh no! Mischievous gnomes have tampered with the neighborhood's Santa-tracking service,
built by the local tinkerer to help everyone know when Santa arrives on Christmas Eve!

The tracking application was originally configured to run on port 8080, but after the
gnomes' meddling, it's nowhere to be found. Without this tracker, nobody in the neighborhood
will know when to expect Santa's arrival!

The tinkerer needs your help to find out which port the santa_tracker process is 
currently using so the neighborhood tracking display can be updated before Christmas Eve!

Your task:
1. Use the 'ss' tool to identify which port the santa_tracker process is 
   listening on
2. Connect to that port to verify the service is running

Hint: The ss command can show you all listening TCP ports and the processes 
using them. Try: ss -tlnp

Good luck, and thank you for helping save the neighborhood's Christmas spirit!

- The Neighborhood Tinkerer 🔧🎄
```


```
ss -tlnp
State                  Recv-Q                 Send-Q                                  Local Address:Port                                    Peer Address:Port                 Process                 
LISTEN                 0                      5                                             0.0.0.0:12321                                        0.0.0.0:*  

```

```
curl http://localhost:12321/
{
  "status": "success",
  "message": "\ud83c\udf84 Ho Ho Ho! Santa Tracker Successfully Connected! \ud83c\udf84",
  "santa_tracking_data": {
    "timestamp": "2025-11-24 08:29:56",
    "location": {
      "name": "Evergreen Estates",
      "latitude": 40.103101,
      "longitude": -76.230016
    },
    "movement": {
      "speed": "606 mph",
      "altitude": "17631 feet",
      "heading": "296\u00b0 W"
    },
    "delivery_stats": {
      "gifts_delivered": 443722,
      "cookies_eaten": 21903,
      "milk_consumed": "2475 gallons",
      "last_stop": "Reindeer Ridge",
      "next_stop": "Yuletide Gardens",
      "time_to_next_stop": "6 minutes"
    },
    "reindeer_status": {
      "rudolph_nose_brightness": "80%",
      "favorite_reindeer_joke": "What do you call a reindeer with no eyes? No-eye-deer!",
      "reindeer_snack_preference": "festive hay bales"
    },
    "weather_conditions": {
      "temperature": "28\u00b0F",
      "condition": "Scattered cloud magic"
    },
    "special_note": "Thanks to your help finding the correct port, the neighborhood can now track Santa's arrival! The mischievous gnomes will be caught and will be put to work wrapping presents."
  }
}🎄 tinkerer @ Santa Tracker ~ 🎅 $ 
```