
# Historical Fiction

One of the US Cyber Games administrators is an avid reader and one of the coaches suggested that she gets a book to learn more about cybersecurity. They can’t remember what the title of the book or that ISBN was but if you examine their Chrome History, you can find the flag which is the book’s ISBN number. It is important to note that they won’t buy a hard cover book or a kindle edition, just the paperback one.

## Solucion


```
┌──(root㉿kali)-[/home/…/forensic/historical/Google/Chrome]
└─# find . -name History                                                           
./User Data/Default/History
                                                                                                                                                                                                                                
┌──(root㉿kali)-[/home/…/forensic/historical/Google/Chrome]
└─# cd User\ Data/Default 


┌──(root㉿kali)-[/home/…/Google/Chrome/User Data/Default]
└─# file History
History: SQLite 3.x database, last written using SQLite version 3049001, file counter 2, database pages 40, cookie 0x21, schema 4, UTF-8, version-valid-for 2



```

- Explorar las tablas
```
┌──(root㉿kali)-[/home/…/Google/Chrome/User Data/Default]
└─# sqlite3 History
SQLite version 3.46.1 2024-08-13 09:16:08
Enter ".help" for usage hints.
sqlite> .tables
cluster_keywords          downloads                 segment_usage           
cluster_visit_duplicates  downloads_slices          segments                
clusters                  downloads_url_chains      urls                    
clusters_and_visits       history_sync_metadata     visit_source            
content_annotations       keyword_search_terms      visited_links           
context_annotations       meta                      visits                  
sqlite> .schema urls
CREATE TABLE urls(id INTEGER PRIMARY KEY AUTOINCREMENT,url LONGVARCHAR,title LONGVARCHAR,visit_count INTEGER DEFAULT 0 NOT NULL,typed_count INTEGER DEFAULT 0 NOT NULL,last_visit_time INTEGER NOT NULL,hidden INTEGER DEFAULT 0 NOT NULL);
CREATE INDEX urls_url_index ON urls (url);
sqlite> SELECT url, title, last_visit_time 
FROM urls 
WHERE url LIKE '%isbn%' 
   OR url LIKE '%paperback%' 
   OR title LIKE '%paperback%' 
ORDER BY last_visit_time DESC;
sqlite> SELECT url, title FROM urls 
WHERE url LIKE '%amazon%' OR url LIKE '%goodreads%' OR url LIKE '%isbn%' 
   OR url LIKE '%book%' OR url LIKE '%cybersecurity%' 
ORDER BY last_visit_time DESC;
https://www.amazon.com/Hack-Back-Techniques-Hackers-Their/dp/1032818530/ref=tmm_pap_swatch_0#averageCustomerReviewsAnchor|The Hack Is Back: Varsalone, Jesse, Haller, Christopher: 9781032818535: Amazon.com: Books
https://www.amazon.com/Hack-Back-Techniques-Hackers-Their/dp/1032818530/ref=tmm_pap_swatch_0|The Hack Is Back: Varsalone, Jesse, Haller, Christopher: 9781032818535: Amazon.com: Books
https://www.amazon.com/Hack-Back-Techniques-Hackers-Their-ebook/dp/B0D6NB2542/ref=tmm_kin_swatch_0|Amazon.com: The Hack Is Back: Techniques to Beat Hackers at Their Own Games eBook : Varsalone, Jesse, Haller, Christopher: Kindle Store
https://www.amazon.com/Hack-Back-Techniques-Hackers-Their/dp/0815382383|The Hack Is Back: Varsalone, Jesse, Haller, Christopher: 9780815382386: Amazon.com: Books
sqlite> 


```


```
https://www.amazon.com/Hack-Back-Techniques-Hackers-Their-ebook/dp/B0D6NB2542/ref=tmm_kin_swatch_0|Amazon.com:
```

```
SVUSCG{978-1032818535}
```