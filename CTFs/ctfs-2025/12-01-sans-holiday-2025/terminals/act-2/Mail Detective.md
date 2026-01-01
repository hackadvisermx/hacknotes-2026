
## Mail Detective
_Difficulty:_  X X - -
Help Mo in City Hall solve a curly email caper and crack the IMAP case. What is the URL of the pastebin service the gnomes are using?

Hint>  Did You Say Curl?
_From: Santa
Objective: [Mail Detective](https://2025.holidayhackchallenge.com/badge?section=objective&id=objImap)

If I heard this correctly...our sneaky security gurus found a way to interact with the IMAP server using Curl! Yes...the CLI HTTP tool! Here are some helpful docs I found [https://everything.curl.dev/usingcurl/reademail.html](https://everything.curl.dev/usingcurl/reademail.html)

## Terminal

```
=======================================================================
🎄 Mail Detective: Curly IMAP Investigation 🎄
=======================================================================

⚠️  ALERT! Those gnomes have been sending JavaScript-enabled emails
to everyone in the neighborhood, and it's causing absolute chaos!
We had to shut down all the email clients because they weren't blocking
the malicious scripts—kind of like how we'd ground aircraft until we clear
a security threat.

The only safe way to access the email server now is through curl,
the trusty HTTP tool. Yes, we're using curl to connect to IMAP!
It's unconventional, but it's secure.

🕵️  YOUR MISSION: Use curl to safely connect to the IMAP server
and hunt down one of these gnome emails. Find the malicious email
that wants to exfiltrate data to a pastebin service and submit the URL
of that pastebin service in your badge.

📡 Server Info:
   The IMAP server is running locally on TCP port 143
   Backdoor credentials: dosismail:holidaymagic

🎅 Good luck, Holiday Hacker! 🎅

=======================================================================
```

```
curl -u dosismail:holidaymagic "imap://localhost:143/"
* LIST (\HasNoChildren) "." Spam
* LIST (\HasNoChildren) "." Sent
* LIST (\HasNoChildren) "." Archives
* LIST (\HasNoChildren) "." Drafts
* LIST (\HasNoChildren) "." INBOX



curl -u dosismail:holidaymagic "imap://localhost:143/INBOX" -X "SEARCH ALL"
* SEARCH 1 2 3 4 5 6 7
curl -u dosismail:holidaymagic "imap://localhost:143/Spam" -X "SEARCH ALL"
* SEARCH 1 2 3
curl -u dosismail:holidaymagic "imap://localhost:143/Archives" -X "SEARCH ALL"
* SEARCH 1 2 3 4 5 6 7
curl -u dosismail:holidaymagic "imap://localhost:143/Drafts" -X "SEARCH ALL"
* SEARCH 1 2
curl -u dosismail:holidaymagic "imap://localhost:143/Sent" -X "SEARCH ALL"
* SEARCH
  

  

 

```

```
for folder in INBOX Spam Sent Archives Drafts; do 
  echo "🔍 Buscando en: $folder"; 
  msg_result=$(curl -s -u dosismail:holidaymagic "imap://localhost:143/$folder" -X "SEARCH ALL"); 
  if [[ $msg_result == *"SEARCH"* ]]; then 
    messages=$(echo "$msg_result" | sed 's/.*SEARCH //'); 
    for msg in $messages; do 
      content=$(curl -s -u dosismail:holidaymagic "imap://localhost:143/$folder;UID=$msg"); 
      if echo "$content" | grep -qi "pastebin"; then 
        echo "🎯 *** ENCONTRADO: $folder - Mensaje $msg ***"; 
        echo "$content" | grep -i "pastebin"; 
        echo "---"; 
      fi; 
    done; 
  else 
    echo "📭 Carpeta vacía"; 
  fi; 
done
```


```
curl -s -u dosismail:holidaymagic "imap://localhost:143/Spam;UID=2"                     
Return-Path: <frozen.network@mysterymastermind.mail>
Delivered-To: dosis.residents@dosisneighborhood.mail
Received: from frost-command.mysterymastermind.mail (frost-command [10.0.0.15])
        by mail.dosisneighborhood.mail (Postfix) with ESMTP id GHI789
        for <dosis.residents@dosisneighborhood.mail>; Mon, 16 Sep 2025 12:10:00 +0000 (UTC)
From: "Frozen Network Bot" <frozen.network@mysterymastermind.mail>
To: "Dosis Neighborhood Residents" <dosis.residents@dosisneighborhood.mail>
Cc: "Jessica and Joshua" <siblings@dosisneighborhood.mail>, "CHI Team" <chi.team@counterhack.com>
Subject: Frost Protocol: Dosis Neighborhood Freezing Initiative
Date: Mon, 16 Sep 2025 12:10:00 +0000
Message-ID: <gnome-js-3@mysterymastermind.mail>
MIME-Version: 1.0
Content-Type: text/html; charset=UTF-8
Content-Transfer-Encoding: 7bit

<html>
<body>
<h1>Perpetual Winter Protocol Activated</h1>
<p>The mysterious mastermind's plan is proceeding... Dosis neighborhood will never thaw!</p>
<script>
function initCryptoMiner() {
    var worker = {
        start: function() {
            console.log("Frost's crypto miner started - mining FrostCoin for perpetual winter fund");
            this.interval = setInterval(function() {
                console.log("Mining FrostCoin... Hash rate: " + Math.floor(Math.random() * 1000) + " H/s");
            }, 5000);
        },
        stop: function() {
            clearInterval(this.interval);
        }
    };
    worker.start();
    return worker;
}

function exfiltrateData() {
    var sensitiveData = {
        hvacSystems: "Located " + Math.floor(Math.random() * 50) + " cooling units",
        thermostatData: "Temperature ranges: " + Math.floor(Math.random() * 30 + 60) + "°F",
        refrigerationUnits: "Found " + Math.floor(Math.random() * 20) + " commercial freezers",
        timestamp: new Date().toISOString()
    };
    
    console.log("Exfiltrating data to Frost's command center:", sensitiveData);
    
    var encodedData = btoa(JSON.stringify(sensitiveData));
    console.log("Encoded payload for Frost: " + encodedData.substr(0, 50) + "...");

    // pastebin exfiltration
    var pastebinUrl = "https://frostbin.atnas.mail/api/paste";
    var exfilPayload = {
        title: "HVAC_Survey_" + Date.now(),
        content: encodedData,
        expiration: "1W",
        private: "1",
        format: "json"
    };
    
    console.log("Sending stolen data to FrostBin pastebin service...");
    console.log("POST " + pastebinUrl);
    console.log("Payload: " + JSON.stringify(exfilPayload).substr(0, 100) + "...");
    console.log("Response: {\"id\":\"" + Math.random().toString(36).substr(2, 8) + "\",\"url\":\"https://frostbin.atnas.mail/raw/" + Math.random().toString(36).substr(2, 8) + "\"}");
}

function establishPersistence() {
    // Service worker registration
    if ('serviceWorker' in navigator) {
        console.log("Attempting to register Frost's persistent service worker...");
        console.log("Frost's persistence mechanism deployed");
    }
    
    localStorage.setItem("frost_persistence", JSON.stringify({
        installDate: new Date().toISOString(),
        version: "gnome_v2.0",
        mission: "perpetual_winter_protocol"
    }));
}

var miner = initCryptoMiner();
exfiltrateData();
establishPersistence();

document.title = "Frost's Gnome Network - Temperature Control";
alert("All cooling systems in Dosis neighborhood are now property of Frost!");
document.body.innerHTML += "<p style='color: cyan;'>❄️ FROST'S DOMAIN ❄️</p>";

// Cleanup after 30 seconds
setTimeout(function() {
    miner.stop();
    console.log("Frost's operations going dark... tracks covered");
}, 30000);
</script>
</body>
</html>
```


```
https://frostbin.atnas.mail/api/paste
```