# ItsyBitsy Summary

## 1. How many events were returned for the month of March 2022?
- **Answer:** 1482  
- **Steps:** Used Discover tab, adjusted date range to March 2022, updated results.

## 2. What is the IP associated with the suspected user in the logs?
- **Answer:** 192.166.65.54  
- **Steps:** Filtered by `source_ip` and selected the correct IP based on context.

## 3. The user’s machine used a legit Windows binary to download a file from the C2 server. What is the name of the binary?
- **Answer:** bitsadmin  
- **Steps:** Filtered HTTP method to “GET” with the IP, found `bitsadmin` in `user_agent`.

## 4. The infected machine connected with a famous file-sharing site in this period, which also acts as a C2 server. What is the name of the site?
- **Answer:** pastebin.com  
- **Steps:** Found in the same log entry from previous question.

## 5. What is the full URL of the C2 to which the infected host is connected?
- **Answer:** pastebin.com/yTg0Ah6a  
- **Steps:** Combined URI from logs with domain name.

## 6. A file was accessed on the file-sharing site. What is the name of the file accessed?
- **Answer:** secret.txt  
- **Steps:** Visited the URL and found the file name on the page.

## 7. The file contains a secret code with the format THM{_____}.
- **Answer:** THM{SECRET__CODE}  
- **Steps:** Retrieved from the contents of `secret.txt`.
