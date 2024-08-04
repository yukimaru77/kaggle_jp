# 60 Sec timeout limit

**VolodymyrBilyachat** *Wed May 29 2024 09:32:33 GMT+0900 (日本標準時)* (0 votes)

I am thinking that 60 seconds timeout limit solution to single call to llm which basically eliminate idea of adding critic. In many cases call to llm second time and prompt it to verify or criticise  can improve results significantly. 

Is that the purpose of the competition so we do single-shot or single call to llm?

I had critic but have to remove it since i would hit timeout and get immediately -60 :( so now id rather return dummy question, guess instead of hit timeout.



